# Comparison of US and European Economies (1980–present)

A data mining project that analyzes and compares the economic evolution of the United States and the European Union since 1980 using time-series data from the FRED API.

---

## Purpose

This project aims to examine how the key economic sectors of the United States and Europe have evolved over more than four decades. By working with real data from the **Federal Reserve Bank of St. Louis (FRED)**, we identify periods of growth and decline across multiple indicators and relate those patterns to their historical context — recessions, financial crises, and global shocks.

---

## What the Project Does

### Data Sources
All data is retrieved via the [FRED API](https://fred.stlouisfed.org/docs/api/fred/). The indicators analyzed include:

| Category | USA Series | Europe Series |
|---|---|---|
| GDP (Real) | GDPC1 | CLVMNACSCAB1GQEU272020 |
| Inflation | CPIAUCSL | FPCPITOTLZGEUU |
| Interest Rates | FEDFUNDS | IRLTLT01EZQ156N |
| Industrial Production | IPB50001NQ | PRINTO01EZQ661N |
| Housing Price Index | USSTHPI | QXMN628BIS |
| Employment Rate | LREM64TTUSQ156N | LREM64TTEUQ156N |
| Public Debt (% of GDP) | GFDEGDQ188S | GCDODTOTLGDZSEMU |
| Imports | NA000342Q | XTIMVA01EZQ664N |
| Exports | NA000352Q | XTEXVA01EZQ664N |
| Recession Indicator | USREC | EUROREC |
| Dollar–Euro Exchange Rate | EXUSEU | — |

### Pipeline Overview

1. **Data Retrieval & Preprocessing**  
   - All series are harmonized to a common quarterly frequency (monthly series are averaged per quarter; annual series are interpolated using linear interpolation or KNN).  
   - Units are standardized (e.g., European imports/exports converted to millions of USD; all production indices rebased to 1980:Q1 = 100).  
   - Missing values in the European employment series are imputed using KNN (k=10).

2. **Exploratory Analysis**  
   - Descriptive statistics (mean, median, standard deviation, skewness, IQR) computed for both regions.  
   - Correlation heatmaps for internal US variables, internal European variables, and cross-region variable pairs.  
   - Quarter-over-quarter differencing correlations to identify co-movement patterns.

3. **Indicator Comparisons** (section by section)  
   - Recessions, GDP evolution, industrial production, employment, housing prices, trade (imports/exports), inflation, and interest rates — all compared side-by-side with recession periods shaded on charts.

4. **GDP Forecasting**  
   - ARIMA models are fitted automatically (`auto_arima`) for both US and European GDP.  
   - One-year-ahead predictions with 95% confidence intervals are generated and compared.

---

## Key Conclusions

### Recessions
- Since 1980, **Europe has been in recession 38% of the time** versus only **12% for the USA**. Out of 184 quarterly observations, Europe recorded 71 recession quarters.  
- Both economies share the following crises: the 1981–82 Iranian Revolution recession, the 2001 Dot-com crash, the 2008–09 mortgage crisis, and the 2020 COVID shock — all of which lasted shorter in the USA.

### GDP
- Both economies suffered their largest GDP drop during COVID-19: **−9% for the USA and −11% for Europe**.  
- Europe's decline was particularly significant because it entered COVID having already been in a recessionary period since early 2018.

### Industrial Production
- US industrial production diverged strongly between 1993 and 2000, driven by the IT revolution and the Dot-com bubble.  
- Since the 2008 peak, industrial production in both regions has **leveled off rather than grown further**.

### Employment
- A 12-percentage-point gap between US and European employment rates in 2000 had narrowed to just **2 points by 2020**.  
- The USA experienced a much sharper employment drop in 2008 (from 71% to 66%), while Europe's decline was more gradual.

### Housing Prices
- Housing prices **multiplied by approximately 7×** in both economies since their respective base years, far outpacing real GDP growth (≈300% in the USA, ≈200% in Europe).  
- This divergence between housing costs and economic output suggests that price appreciation has been driven by factors beyond productivity growth.

### Trade
- The **USA has imported more** than Europe throughout the period, while **Europe has consistently exported as much or more** than the USA, typically running a trade surplus.

### Inflation
- In 1980, both economies hit historic highs. US inflation exceeded European inflation until around 2002; since then they have moved in tandem.  
- Post-2020, both saw a sharp inflation spike driven by the COVID crisis.

### Interest Rates
- After the 1981 shock (more pronounced in the USA), both regions have trended downward.  
- Following the 2008 crisis, US rates fell close to **0%**; both regions raised rates sharply again after COVID.

### Correlations
- Most US economic variables are **highly correlated** with one another, reflecting a tightly coupled economy.  
- European variables show **moderate correlations**, with employment more closely tied to GDP and housing than in the USA.  
- **Cross-region**: exports and imports of both regions are strongly correlated, indicating significant bilateral trade. US public debt shows negative correlations with European GDP, housing, and employment.

### GDP Forecasting
- The ARIMA model for US GDP selected an AR(1)+MA(1) structure, reflecting greater historical stability.  
- The European model selected a simpler MA(1) structure, and its **95% confidence interval is roughly twice as wide** as the US interval — reflecting greater uncertainty due to both economic volatility and fewer historical data points (available from 1995 vs. 1947 for the USA).

---

## Requirements

- A free **FRED API key** — register at https://fred.stlouisfed.org/docs/api/fred/

Set your API key in the notebook:
```python
API_KEY = 'your_api_key_here'
```

---

## Authors

- May Yun Amorós Más  
- Jorge Tomás Linares  
- Senén Martínez Andreu
