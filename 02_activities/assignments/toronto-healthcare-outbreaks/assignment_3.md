# Data Visualization

## Assignment 3: Final Project

### Requirements:
- We will finish this class by giving you the chance to use what you have learned in a practical context, by creating data visualizations from raw data. 
- Choose a dataset of interest from the [City of Toronto’s Open Data Portal](https://www.toronto.ca/city-government/data-research-maps/open-data/) or [Ontario’s Open Data Catalogue](https://data.ontario.ca/). 
- Using Python and one other data visualization software (Excel or free alternative, Tableau Public, any other tool you prefer), create two distinct visualizations from your dataset of choice.  

# Visualization 1 — Python: Respiratory Outbreak Time Series & Forecast
For each visualization, describe and justify: 
  
1. What software did you use to create your data visualization?
**Software used:** Python (Pandas, Prophet, Matplotlib/Seaborn)  

2. Who is your intended audience? 
**Intended audience:** Public health analysts and infection control leads.

3. What information or message are you trying to convey with your visualization? 
**What it shows / message:**  
A monthly time series of respiratory outbreaks (2016–2025) with a 12-month forecast generated using Prophet. The visualization highlights Toronto’s recurring winter peaks and projects future high-risk months so healthcare institutions can plan staffing and resource allocation proactively.
    
4. What aspects of design did you consider when making your visualization? How did you apply them? With what elements of your plots? 
**Design choices:**    
- Line chart with visible data points and shaded 95% confidence interval for the forecast.
- Month/year axis formatting for clarity and temporal readability.
- High-contrast, colorblind-friendly palette with labeled axes and a descriptive title.
- Minimal gridlines and annotations for clean visual focus.
    
5. How did you ensure that your data visualizations are reproducible? If the tool you used to make your data visualization is not reproducible, how will this impact your data visualization? 
**Reproducibility:**  
- All processing and visualization steps are included in a single Jupyter Notebook.
- The cleaned dataset (outbreaks_combined_2016_2025.csv) is available in the repository.
- Running the notebook from start to finish reproduces the exact figure.
- A requirements.txt file lists exact package versions to ensure consistent results.

6. How did you ensure that your data visualization is accessible?  
**Accessibility:**  
- Used colorblind-safe hues and thick line weights for clarity.
- Included descriptive titles, axis labels, and markdown narrative text.
- Exported the plot as a 300-DPI PNG for screen readability and printing.

7. Who are the individuals and communities who might be impacted by your visualization?  
**Impacted communities:**  
- Healthcare staff (infection prevention and control teams), long-term care operators, and Toronto Public Health officials who rely on outbreak surveillance for planning.

8. How did you choose which features of your chosen dataset to include or exclude from your visualization? 
**Feature selection rationale:**  
- Focused on Respiratory outbreaks only, as they represent the majority of institutional outbreaks and have strong seasonal trends. Data were aggregated monthly to reveal long-term patterns and stabilize variation.
    
9. What ‘underwater labour’ contributed to your final data visualization product?
**Underwater labour:**  
- Data cleaning (parsing inconsistent date formats, normalizing outbreak types, standardizing column names), verifying missing values, converting periods to timestamps for Prophet, and iterating Prophet hyperparameters for realistic seasonality.



# Visualization 2 — Power BI: Interactive Dashboard of Active Outbreaks
- For each visualization, describe and justify: 

1.  What software did you use to create your data visualization?
**Software used:** Power BI Desktop (Map, KPI Cards, Bar/Stacked Column, Area Chart)

2. Who is your intended audience? 
**Intended audience:**  Infection control managers, long-term care administrators, and public health decision-makers.

3. What information or message are you trying to convey with your visualization? 
**What it shows / message:**  
An interactive dashboard mapping current active outbreaks by facility, breaking down active outbreaks by causative agent, and comparing outbreak burden across facility types — enabling rapid situational awareness and resource prioritization

4. What aspects of design did you consider when making your visualization? How did you apply them? With what elements of your plots? 
**Design choices:**  
- Interactive map for spatial clustering; colors match Python visuals (Respiratory = #2ca02c, Enteric = blue, Other = orange).
- KPI cards with intuitive icons: Total Active Outbreaks, Most Common Causative Agent, Facility Type with Most Outbreaks, Date of Last Outbreak.
- Stacked column chart compares outbreak burden across facility types; bar chart ranks causative agents.
- Area chart shows outbreak trends over time by type.
- Slicers for Year/Month and Type of Outbreak enable interactive drill-downs.
    
5. How did you ensure that your data visualizations are reproducible? If the tool you used to make your data visualization is not reproducible, how will this impact your data visualization? 
**Reproducibility:**  
- Dashboard built directly from the cleaned CSV used in Python.
- Repository includes:
A. The CSV dataset.
B. The .pbix Power BI file.
C. A short README detailing Power Query transformations and DAX measures.
Anyone can reproduce the dashboard by opening the PBIX file and refreshing the data source.

6. How did you ensure that your data visualization is accessible?  
**Accessibility:**  
Colorblind-friendly palette, readable fonts, tooltips for screen readers, alt-text on visuals, printable PDF summary.

7. Who are the individuals and communities who might be impacted by your visualization?  
**Impacted communities:**  
Facility administrators, public health units, residents and families (indirectly through better outbreak response).
    
8. How did you choose which features of your chosen dataset to include or exclude from your visualization? 
**Feature selection rationale:**  
Spatial + categorical breakdown tells a different part of the story than the time series: *where* outbreaks are now and *what* is causing them. The map plus agent breakdown are complementary to the Python forecast.
    
9. What ‘underwater labour’ contributed to your final data visualization product?
**Underwater labour:**  
Geocoding addresses, creating DAX measures, building meaningful tooltips, polishing layout, applying consistent colors/icons.
---

## Why include both visualizations?
- **Python (time)** shows the *temporal* dynamics and provides predictive power (forecasting).  
- **Power BI (space & composition)** shows *real-time spatial distribution* and categorical composition for operational response.  
Together they form a complete story: when outbreaks are likely (Python) and where / what to target now (Power BI).


- This assignment is intentionally open-ended - you are free to create static or dynamic data visualizations, maps, or whatever form of data visualization you think best communicates your information to your audience of choice! 
- Total word count should not exceed **(as a maximum) 1000 words** 
 
### Why am I doing this assignment?:  
- This ongoing assignment ensures active participation in the course, and assesses the learning outcomes: 
* Create and customize data visualizations from start to finish in Python
* Apply general design principles to create accessible and equitable data visualizations
* Use data visualization to tell a story  
- This would be a great project to include in your GitHub Portfolio – put in the effort to make it something worthy of showing prospective employers!

### Rubric:

| Component         | Scoring  | Requirement                                                                 |
|-------------------|----------|-----------------------------------------------------------------------------|
| Data Visualizations | Complete/Incomplete | - Data visualizations are distinct from each other<br>- Data visualizations are clearly identified<br>- Different sources/rationales (text with two images of data, if visualizations are labeled)<br>- High-quality visuals (high resolution and clear data)<br>- Data visualizations follow best practices of accessibility |
| Written Explanations | Complete/Incomplete | - All questions from assignment description are answered for each visualization<br>- Explanations are supported by course content or scholarly sources, where needed |
| Code              | Complete/Incomplete | - All code is included as an appendix with your final submissions<br>- Code is clearly commented and reproducible |

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 11/02/2025`
* The branch name for your repo should be: `assignment-3`
* What to submit for this assignment:
    * A folder/directory containing:
        * This file (assignment_3.md)
        * Two data visualizations 
        * Two markdown files for each both visualizations with their written descriptions.
        * Link to your dataset of choice.
        * Complete and commented code as an appendix (for your visualization made with Python, and for the other, if relevant) 
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/visualization/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-3`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
