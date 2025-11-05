# Epidemiology: A Decade of Infection Outbreaks in Toronto’s Healthcare System (2016–2025)

**Author:** Nneka Asuzu  
**Date:** October 2025  
**Tools Used:** Python (Pandas, NumPy, Matplotlib, Seaborn, Prophet), Power BI  
**Dataset:** [City of Toronto Open Data – Outbreaks in Toronto Healthcare Institutions](https://open.toronto.ca/dataset/outbreaks-in-toronto-healthcare-institutions/)  

---

## Project Overview

This project analyzes reported infection outbreaks in Toronto healthcare institutions (hospitals, long-term care homes, and retirement residences) between 2016 and 2025. Using Python and Power BI, the project visualizes outbreak trends both temporally and spatially to inform public health decision-making.

Two complementary visualizations are included:

1. **Python Time Series & Forecast** – monthly outbreak trends with forecasted future activity.  
2. **Power BI Dashboard** – interactive spatial and categorical view of current active outbreaks.

---

## Dataset

**Title:** Outbreaks in Toronto Healthcare Institutions (2016–2025)  
**Source:** City of Toronto Open Data Portal  
[Dataset Link](https://open.toronto.ca/dataset/outbreaks-in-toronto-healthcare-institutions/)  

**Description:**  
The dataset contains reported outbreaks of respiratory and gastroenteric infections across Toronto healthcare institutions. Key columns:

- `Institution Name` & `Institution Address` – facility identification  
- `Outbreak Setting` – type of institution (Hospital, LTCH, Retirement Home)  
- `Type of Outbreak` – respiratory, enteric, etc.  
- `Causative Agent-1` / `Causative Agent-2` – pathogens  
- `Date Outbreak Began` & `Date Declared Over` – outbreak timeline  
- `Active Status` – still active vs. resolved  
- `Duration` – outbreak length in days  

**Cleaning Steps:**  
1. Standardized column names and removed extra spaces  
2. Converted date columns and extracted `month`/`year` for trends  
3. Unified causative agent names and filled missing values  
4. Calculated `Active Status` and `Duration`  
5. Removed empty/duplicate columns for a clean dataset  

---

## Visualizations

### 1. Python: Outbreak Time Series & Forecast
- Software: Python (Pandas, Matplotlib, Seaborn, Prophet)  
- Audience: Public health analysts and infection control leads  
- Shows monthly outbreak trends and forecasted future outbreaks  
- Uses colorblind-friendly palettes and clear axis labels  
- Helps anticipate high-risk periods for resource allocation  

### 2. Power BI: Spatial Dashboard of Active Outbreaks
- Software: Power BI Desktop  
- Audience: Infection control managers, LTC administrators, public health decision-makers  
- Interactive map showing outbreak locations, stacked column & bar charts for outbreak type and causative agents  
- KPI cards summarize Total Active Outbreaks, Most Common Causative Agent, Facility Type with Most Outbreaks, Date of Last Outbreak  
- Filters/slicers enable drill-down by Year, Month, and Type of Outbreak  
- Color palette consistent with Python visualization (#2ca02c for respiratory, orange & blue for enteric, gray for other)  

---

## Reproducibility

- Cleaned CSV (`outbreaks_combined_2016_2025.csv`) included  
- Python notebook with full code and `requirements.txt`  
- Power BI PBIX file with applied DAX measures and visuals  
- README includes instructions and dataset link  

### **Full requirements.txt**

# Data manipulation
pandas>=2.1.0
numpy>=1.25.0

# Visualization
matplotlib>=3.8.0
seaborn>=0.12.2

# Forecasting
prophet>=1.2.2

# Additional dependencies for reproducibility
scipy>=1.11.0
python-dateutil>=2.9.0
pytz>=2025.10

> **Notes:**  
> - `prophet` is required for outbreak forecasting.  
> - `matplotlib` and `seaborn` are used for all visualizations, including scenario modeling plots.  
> - `pandas` and `numpy` handle dataset cleaning, transformation, and aggregation.  
> - The listed environment ensures reproducibility of all code, figures, and datasets.

---

## Insights

- Outbreaks show strong seasonal patterns, peaking in winter months  
- LTC homes experience the highest outbreak burden  
- Respiratory and enteric pathogens dominate current outbreaks  
- Spatial clustering reveals hotspots in certain neighborhoods  

---

## Repository Structure

