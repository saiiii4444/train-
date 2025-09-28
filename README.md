# Monthly Performance of SNCF TER and Intercités – Raju's Power BI Project

This project analyses the punctuality and service levels of SNCF’s regional (TER) and long‑distance Intercités trains. It builds on my friend Harishankar’s original work, but the data files, scripts and dashboards here have been adapted and extended for my own use. Monthly figures from the SNCF Open Data portal track the number of trains scheduled, trains that ran, cancellations and late arrivals. I compute ‘regularity’—the percentage of trains arriving on time at their terminus. A train counts as ‘on time’ if the delay at the terminus is less than 5 minutes for journeys under 90 minutes, 10 minutes for journeys between 1½ and 3 hours, or 15 minutes for journeys over 3 hours【137233211135598†L42-L51】.

## Files

| File | Purpose |
|---|---|
| **intercites_monthly.csv** | Aggregated monthly regularity metrics for **Intercités** services. Columns include the average regularity, total trains scheduled, trains that ran, cancellations and late arrivals per month. |
| **ter_monthly.csv** | Aggregated monthly metrics for **TER** services. The data is the sum of all French regions for each month. |
| **train_performance_monthly.csv** | A merged view combining, for each month, the average regularity of Intercités and TER. This is useful for comparative visualisation. |
| **train_performance_trend.png** | A line chart comparing the monthly regularity of Intercités (blue) and TER (orange) from 2013 to mid‑2025. |
| **train_performance_average.png** | A bar chart summarising the average regularity across the entire period for each service type. |
| **analysis.ipynb** | A Jupyter notebook used to scrape and clean the raw data and create the charts. You can run it to reproduce the results. |

## Data source

The raw data was downloaded from the **SNCF Open Data** portal. Two datasets were used:

* **Régularité mensuelle Intercités :** This dataset gives monthly punctuality statistics for each Intercités route since January 2014. Regularity is calculated at the train’s final destination; a train counts as late only if its delay exceeds the threshold above【137233211135598†L42-L51】. A copy of the full dataset is available on [ressources.data.sncf.com](https://ressources.data.sncf.com/).
* **Régularité mensuelle TER :** This dataset provides similar metrics for regional TER trains from January 2013. Figures are aggregated by region and follow the same “on‑time” threshold【21633491631463†L42-L50】.

Both datasets were downloaded as CSV files, then aggregated by month using a simple Python script. The script groups by month and calculates the mean regularity and sums the number of trains scheduled, run, cancelled and late.

## How to use these files in Power BI

1. **Import the CSV files:** Open Power BI Desktop and choose “Get Data → CSV”. Select `intercites_monthly.csv` and `ter_monthly.csv`. Power BI will recognise the semicolon (`;`) delimiter automatically, but if not, choose `File origin → Unicode (UTF‑8)` and `Delimiter → Semicolon` in the import dialogue.
2. **Create relationships:** If you wish to compare both services side by side, load `train_performance_monthly.csv` which already contains both regularity columns. Alternatively, import each dataset separately and create a relationship on the `date` field.
3. **Build visualisations:** Use a “Line and clustered column chart” to plot `regularite_intercites` and `regularite_ter` over time. To show average punctuality, create a “Bar chart” and use the **Average of regularity** measure.
4. **Add filters:** Power BI slicers can be used to filter by time period (e.g., 2019–2025) or to focus on a particular region or route if you decide to work with the detailed raw data.

The accompanying images (`train_performance_trend.png` and `train_performance_average.png`) provide examples of the kind of dashboards you can create. I’ve also included the raw PNGs of the dashboards from my friend’s original report for completeness.

## Contact

**Author:** Raju (Student, Antibes)  
**Inspiration:** Adapted from a project by Harishankar Murugan  
I hope this helps anyone looking to explore SNCF’s service performance using simple, transparent code and Power BI dashboards.

