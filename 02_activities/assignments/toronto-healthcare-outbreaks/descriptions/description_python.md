# Visualization 1 — Python: Outbreak Time Series & Forecast

**Dataset Used:** `outbreaks_combined_2016_2025.csv` (cleaned from combined annual files)

**Description:**  
- Includes **all reported outbreaks** (respiratory and enteric) from 2016–2025.  
- Aggregated monthly counts to analyze temporal trends across all outbreak types.  
- Key columns used: Type of Outbreak, Causative Agent, Date Outbreak Began, Date Declared Over, Active Status, Duration, Institution Name.

**Software / Libraries:** Python, Pandas, NumPy, Matplotlib, Seaborn, Prophet

**Analysis / Visual Created:**  
- Monthly time series line/area chart showing counts of outbreaks over time.  
- Forecast using Prophet to project outbreak trends up to 12 months into the future.  
- Highlights seasonal peaks and temporal patterns across all types.

**Design Notes:**  
- Color palette is colorblind-friendly.  
- Axes labeled with month/year for clarity.  
- Markers on lines and shaded forecast confidence intervals improve interpretability.

**Reproducibility:**  
- Entire code in a single Jupyter notebook.  
- CSV and `requirements.txt` included for reproducibility.

**Key Takeaways / Insights:**  
- Outbreak counts show clear seasonality.  
- Forecast identifies periods with higher expected outbreak activity.  
- Useful for public health preparedness and resource allocation.
