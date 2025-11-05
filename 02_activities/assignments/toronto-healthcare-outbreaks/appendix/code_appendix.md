# Code Appendix

This appendix contains all Python and Power BI code used to clean, analyze, and visualize the outbreak dataset.  


## Notes

- Python code handles cleaning, transformation, aggregation, visualization, and forecasting.  
- DAX measures are used in Power BI to create KPI cards and support visuals for active outbreak analysis.  
- Dataset: `outbreaks_combined_2016_2025.csv`  
- Ensure all library dependencies are installed for reproducibility: `pandas`, `numpy`, `matplotlib`, `seaborn`, `prophet`.

---

## Step 1: Import Libraries

```python
import os
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from prophet import Prophet


## Step 2: Load & Combine Datasets (2016–2025)

data_dir = "../outbreaks_data"
csv_files = [f"ob_report_{year}.csv" for year in range(2016, 2026)]

df_list = []

for file in csv_files:
    path = os.path.join(data_dir, file)
    temp_df = pd.read_csv(path)
    
    # Normalize column names
    temp_df.columns = temp_df.columns.str.strip().str.replace('  ', ' ').str.replace(' - ', '-')
    
    # Standardize causative agent column names
    temp_df.rename(columns={
        'Causative Agent - 1': 'Causative Agent-1',
        'Causative Agent - 2': 'Causative Agent-2'
    }, inplace=True)
    
    # Extract year from filename
    temp_df['Year'] = int(file.split('_')[2].split('.')[0])
    
    df_list.append(temp_df)

# Combine all DataFrames
df = pd.concat(df_list, ignore_index=True)


## Step 3: Clean and Standardize the Data

# A. Strip spaces from column names
df.columns = df.columns.str.strip()

# B. Standardize causative agent columns (again for safety)
df.rename(columns={
    'Causative Agent - 1': 'Causative Agent-1',
    'Causative Agent - 2': 'Causative Agent-2'
}, inplace=True)

# C. Convert date columns to datetime
df['Date Outbreak Began'] = pd.to_datetime(df['Date Outbreak Began'], errors='coerce')
df['Date Declared Over'] = pd.to_datetime(df['Date Declared Over'], errors='coerce')

# D. Extract month for trend analysis
df['month'] = df['Date Outbreak Began'].dt.to_period('M')

# E. Standardize text columns
df['Type of Outbreak'] = df['Type of Outbreak'].str.title().fillna('Unknown')
df['Outbreak Setting'] = df['Outbreak Setting'].str.title().fillna('Unknown')

# F. Fill missing values for causative agents
df['Causative Agent-1'] = df['Causative Agent-1'].fillna('Unknown')
df['Causative Agent-2'] = df['Causative Agent-2'].fillna('Unknown')

# G. Create Active Status column
df['Active Status'] = df['Date Declared Over'].notna().map({True: 'Resolved', False: 'Still Active'})

# H. Calculate duration in days
df['Duration'] = (df['Date Declared Over'] - df['Date Outbreak Began']).dt.days

# I. Remove empty or duplicate columns
columns_to_drop = ['Active']
df = df.loc[:, ~df.columns.duplicated(keep='last')]
df.drop(columns=columns_to_drop, inplace=True, errors='ignore')


### Step 3a: Preview Top Causative Agents

print("\nTop 10 causative agents:")
print(df['Causative Agent-1'].value_counts().head(10))


## Step 4: Exploratory Analysis
 
 ### Active Outbreaks by Setting and Type

active = df[df['Active Status'] == 'Still Active']
by_setting = active.groupby(['Outbreak Setting','Type of Outbreak']).size().reset_index(name='count')
pv = by_setting.pivot(index='Outbreak Setting', columns='Type of Outbreak', values='count').fillna(0)

fig, ax = plt.subplots(figsize=(10,6))
pv.plot(kind='bar', stacked=True, ax=ax)
ax.set_title("Active Outbreaks by Setting and Type")
ax.set_xlabel("Outbreak Setting")
ax.set_ylabel("Number of Active Outbreaks")
plt.tight_layout()
plt.show()

### Monthly Outbreak Trends

time_series = (
    df.dropna(subset=['Date Outbreak Began'])
      .groupby(['month','Type of Outbreak'])
      .size()
      .reset_index(name='count')
)

# Convert month to datetime for plotting
time_series['month'] = time_series['month'].dt.to_timestamp()
ts_pivot = time_series.pivot(index='month', columns='Type of Outbreak', values='count').fillna(0)

fig, ax = plt.subplots(figsize=(12,5))
ts_pivot.plot(ax=ax, linewidth=2, marker='o')
ax.set_title("Monthly Outbreaks (2016–2025)")
plt.tight_layout()
plt.show()

## Top 5 Causative Agents by Year
agents = df.groupby(['Year','Causative Agent-1']).size().reset_index(name='count')
top_agents = agents.groupby('Causative Agent-1')['count'].sum().sort_values(ascending=False).head(5).index
agents_top = agents[agents['Causative Agent-1'].isin(top_agents)]

fig, ax = plt.subplots(figsize=(12,5))
sns.lineplot(data=agents_top, x='Year', y='count', hue='Causative Agent-1', marker='o', ax=ax)
ax.set_title("Top 5 Causative Agents by Year (2016–2025)")
plt.tight_layout()
plt.show()

## Step 5: Scenario Modeling
active_current = df[df['Active Status'] == 'Still Active']
base_counts = active_current.groupby(['Outbreak Setting','Type of Outbreak']).size().reset_index(name='count')

scenarios = {'Base': 1.0, '+10%': 1.1, '+20%': 1.2, '+50%': 1.5}
scenario_pivots = {}

for name, factor in scenarios.items():
    temp = base_counts.copy()
    temp['sim_count'] = temp['count'] * factor
    scenario_pivots[name] = temp.pivot(index='Outbreak Setting', columns='Type of Outbreak', values='sim_count').fillna(0)

fig, axes = plt.subplots(1, len(scenarios), figsize=(16,5), sharey=True)
for ax, (name, pivot) in zip(axes, scenario_pivots.items()):
    pivot.plot(kind='bar', stacked=True, ax=ax, legend=False)
    ax.set_title(name)
plt.tight_layout()
plt.show()


## Step 6: Prophet Time Series Forecasting (Optional)
# Example forecasting for respiratory outbreaks
resp_ts = ts_pivot['Respiratory'].reset_index().rename(columns={'month':'ds','Respiratory':'y'})

model = Prophet(yearly_seasonality=True)
model.fit(resp_ts)
future = model.make_future_dataframe(periods=12, freq='M')
forecast = model.predict(future)

fig = model.plot(forecast)
plt.title("Prophet Forecast: Respiratory Outbreaks")
plt.show()


## Step 7: Export Cleaned Dataset
df.to_csv("outbreaks_combined_2016_2025.csv", index=False)




## Power BI: DAX Measures

-- Total number of active outbreaks
Total Active Outbreaks = CALCULATE(
    COUNTROWS('outbreaks_combined_2016_2025'),
    'outbreaks_combined_2016_2025'[Active Status] = "Still Active"
)

-- Most common causative agent
Most Common Causative Agent = 
TOPN(
    1, 
    SUMMARIZE('outbreaks_combined_2016_2025', 
              'outbreaks_combined_2016_2025'[Causative Agent-1], 
              "Count", COUNT('outbreaks_combined_2016_2025'[Causative Agent-1])), 
    [Count], DESC
)

-- Facility type with the most outbreaks
Facility Type with Most Outbreaks =
TOPN(
    1,
    SUMMARIZE('outbreaks_combined_2016_2025', 
              'outbreaks_combined_2016_2025'[Outbreak Setting], 
              "Count", COUNT('outbreaks_combined_2016_2025'[Outbreak Setting])),
    [Count], DESC
)

-- Date of the most recent outbreak
Date of Last Outbreak = CALCULATE(
    MAX('outbreaks_combined_2016_2025'[Date Outbreak Began]),
    'outbreaks_combined_2016_2025'[Active Status] = "Still Active"
)
