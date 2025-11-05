# Visualization 2 — Power BI: Spatial Dashboard of Active Outbreaks

**Dataset Used:** `outbreaks_combined_2016_2025.csv`

**Description:**  
- Dashboard focuses on **active outbreaks** across Toronto healthcare institutions.  
- Includes outbreak type, causative agent(s), start/end dates, facility type, and active status.  
- Interactive visuals allow drill-down by Year/Month and outbreak type.

**Software Used:** Power BI Desktop

**Visuals Created:**  
1. **Interactive Map:** Shows outbreak locations by institution, colored by type (Respiratory = `#2ca02c`, Enteric = blue, Other = orange).  
2. **KPI Cards:**  
   - Total Active Outbreaks  
   - Most Common Causative Agent  
   - Facility Type with Most Outbreaks  
   - Date of Last Outbreak  
3. **Stacked Column Chart:** Active outbreaks by facility type, stacked by outbreak type.  
4. **Bar Chart / Treemap:** Active outbreaks by causative agent, sorted descending.  
5. **Line / Area Chart:** Outbreak type trends over time.

**Design Notes:**  
- Consistent colors with Python visualization for accessibility.  
- Titles, readable fonts, intuitive icons for KPIs.  
- Tooltips provide institution, outbreak type, causative agent, and dates.  

**Reproducibility:**  
- PBIX file included.  
- README lists Power Query and DAX steps to reproduce dashboard.

**Key Takeaways / Insights:**  
- Highlights current spatial clusters of outbreaks.  
- Shows dominant causative agents.  
- Identifies facility types most affected by active outbreaks.
