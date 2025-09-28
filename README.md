# Monthly Performance of TER and Intercités (SNCF)

This folder contains a small analytics project exploring the **punctuality** of SNCF’s regional (TER) and long‑distance Intercités trains.  The underlying data comes from the French railway operator’s open data portal.  SNCF publishes monthly figures for the number of trains planned, trains that actually ran, cancellations, late arrivals and a ‘regularity’ indicator.  The indicator is the percentage of trains arriving on time at their terminal station — a train is “on time” if the delay at the terminus is less than 5 minutes for journeys under 90 minutes, 10 minutes for journeys between 1½ and 3 hours, or 15 minutes for journeys over 3 hours【137233211135598†L42-L51】.  For TER the same definition is used but the indicator is aggregated by region rather than by individual route【21634191631463†L42-L50】.

## Files

| File | Purpose |
|---|---|
| **`intercites_monthly.csv`** | Aggregated monthly regularity metrics for **Intercités** services.  Columns include the average regularity, total trains scheduled, trains that ran, cancellations and late arrivals per month. |
| **`ter_monthly.csv`** | Aggregated monthly metrics for **TER** services.  The data is the sum of all French regions for each month. |
| **`train_performance_monthly.csv`** | A merged view containing, for each month, the average regularity of Intercités and TER.  This is useful for comparative visualisation. |
| **`train_performance_trend.png`** | A line chart comparing the monthly punctuality of Intercités (blue) and TER (orange) from 2013 to mid‑2025. |
| **`train_performance_average.png`** | A bar chart summarising the average punctuality across the entire period for each service type. |
| **`analysis.ipynb`** | (Optional) A Jupyter notebook used to aggregate the raw data and create the charts.  You can run it to reproduce the results. |

## Data source

The raw data was downloaded from the **SNCF Open Data** portal.  Two datasets were used:

* **Régularité mensuelle Intercités :** This dataset gives monthly punctuality statistics for each Intercités route since January 2014.  Regularity is calculated at the train’s final destination; a train is considered late if it exceeds the threshold outlined above【137233211135598†L42-L51】.  A copy of the full dataset is available on [ressources.data.sncf.com](https://ressources.data.sncf.com/).
* **Régularité mensuelle TER :** This dataset provides similar metrics for regional TER trains from January 2013.  Figures are aggregated by region and follow the same “on‑time” threshold【21634191631463†L42-L50】.

Both datasets were downloaded as CSV files, then aggregated to monthly level using a simple Python script.  The script groups by month and calculates the mean punctuality and sums the number of trains scheduled, run, cancelled and late.

## How to use these files in Power BI

1. **Import the CSV files:** Open Power BI Desktop and choose *Get Data → Text/CSV*.  Select `intercites_monthly.csv` and `ter_monthly.csv`.  Power BI will recognise the semicolon (`;`) delimiter automatically, but if not, choose `Delimiter → Semicolon` in the import dialogue.
2. **Create relationships:** If you wish to compare both service types side by side, load `train_performance_monthly.csv` which already contains both regularity columns.  Alternatively, import each dataset separately and create a relationship on the `date` field.
3. **Build visualisations:** Use a *Line and clustered column chart* or *Line chart* to plot `regularite_intercites` and `regularite_ter` over time.  To show average punctuality, create a *Bar chart* and use the `Average of régularité` measure.
4. **Add filters:** Power BI slicers can be used to filter by date range (e.g., 2019–2025) or to focus on a particular region or route if you decide to work with the detailed raw data.

The accompanying images (`train_performance_trend.png` and `train_performance_average.png`) provide examples of the kind of dashboards you can create.