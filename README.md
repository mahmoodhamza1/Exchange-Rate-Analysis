# 📈 Exchange Rate Analysis – R Shiny Application

An interactive R Shiny application for analyzing exchange rates through **time series visualization**, **time series decomposition**, and **volatility modeling**.  

The application allows users to:  
- Select a currency and date range to explore historical exchange rates.  
- Decompose exchange rates into **trend, seasonality, and irregular shocks** using STL decomposition.  
- Estimate and visualize conditional volatility using a **GARCH(1,1) model**.  

👉 [Click here to open the live application](https://dataandanalysis.shinyapps.io/ExchangeRateAnalysisApp/)   

---

## ⚙️ Methodology

### Data Handling
- Input dataset: `exchange_rate_dataset.csv`  
- Structure:  
  - `Date` column with daily frequency.  
  - Multiple columns representing exchange rates of different currencies against USD.  
- Pre-processing:  
  - Dates converted into R `Date` type.  
  - Missing values omitted.  
  - Data dynamically filtered based on user-selected **currency** and **date range**.  

### Time Series Visualization
- Built with **ggplot2**, dynamically rendered via **Shiny reactivity**.  
- Provides descriptive statistics: **mean, median, standard deviation, min, max**.  
- Purpose:  
  - Explore long-run appreciation or depreciation of a currency.  
  - Identify sudden shifts or periods of stability.  
  - Compare variability across time windows or currencies.  

### Time Series Decomposition (STL)
- Uses **STL (Seasonal-Trend decomposition using Loess)** for flexible decomposition.  
- Breaks series into:  
  - **Trend**: captures long-term directional changes in exchange rates.  
  - **Seasonal**: reveals recurring cycles (e.g., annual, weekly).  
  - **Remainder**: captures irregular shocks, residual volatility, and noise.  
- Summaries include:  
  - Seasonal effect range (max/min).  
  - Long-term mean and change in trend.  
  - Remainder variability and approximate number of outliers.  
- Significance: Helps distinguish between **structural drivers** of exchange rates vs. **short-term noise**.  

### Volatility Modeling (GARCH)
- Exchange rate **returns** computed as log differences.  
- Fitted with a **GARCH(1,1)** model using the `rugarch` package.  
- Outputs:  
  - Conditional volatility estimates over time.  
  - Summary statistics: **average, max, min volatility**.  
- Significance:  
  - Identifies volatility clustering, a hallmark of financial time series.  
  - Reveals periods of stress (crises, policy shocks) vs. stability.  
  - Useful for risk management, forecasting, and pricing currency derivatives.  

### Implementation in R Shiny
- **UI layer**: built with `fluidPage`, `sidebarLayout`, `tabsetPanel`.  
- **Server layer**: contains reactive pipelines for filtering, decomposition, and GARCH modeling.  
- **Outputs**:  
  - `renderPlot` for visualizations.  
  - `renderText` for statistical summaries.  
- The integration of **R’s econometric libraries** with **Shiny’s interactivity** allows for real-time exploration and dynamic model fitting.

---

## 📊 Results & Interpretation

- **Time Series View**  
  - Reveals the overall evolution of a currency.  
  - Summary statistics provide context on central tendency and variability.  
  - Sharp movements often align with macroeconomic or geopolitical events.  

- **Decomposition View**  
  - **Trend** highlights long-term direction (e.g., gradual appreciation or depreciation).  
  - **Seasonal component** uncovers recurring cycles (holidays, yearly trading effects).  
  - **Remainder** surfaces shocks (e.g., sudden market volatility, financial crises).  
  - Useful for analysts who want to separate predictable patterns from unexpected events.  

- **Volatility View**  
  - Shows conditional volatility over time, confirming **volatility clustering**.  
  - High-volatility periods often coincide with crises or major market events.  
  - Low-volatility periods indicate stable currency environments.  
  - Valuable for risk managers, traders, and policymakers monitoring market stability.  
