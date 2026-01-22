# 2025-Trade-War-Impact-Case-Study
Data Visualization using Python

Geopolitical Risk and Portfolio Resilience Analysis

## Quick Links
- Google Colab Notebook: https://drive.google.com/file/d/1WzgzTG90VAL9lSd-09AQd_-sgE5UxQff/view?usp=sharing 
---

## Project Overview
This project analyzes how U.S. publicly traded companies were positioned prior to the 2025 U.S.–China trade war and examines which firm characteristics, factor exposures, and business structures may have influenced vulnerability or resilience once trade tensions escalated.

Using Bloomberg-style fundamentals and performance data, this study establishes a pre-trade-war baseline across sectors, market capitalization tiers, factor exposures, and firm characteristics. The goal is to provide portfolio managers with actionable insights into how geopolitical shocks interact with firm-level risk profiles.

---

## Project Motivation
Trade wars introduce sudden disruptions to global supply chains, pricing power, and investor expectations. Understanding company positioning **prior to the shock** is essential for:

- Interpreting market reactions during policy escalation  
- Identifying resilient vs vulnerable business models  
- Designing portfolios robust to geopolitical risk  

This project integrates sector exposure, factor profiles, firm size, and labor structure into a unified analytical framework.

---

## Dataset
The analysis uses two Bloomberg-exported datasets covering **1,594 U.S. companies**.

### Company Fundamentals & Factor Data
- File: `20250210_US_Port.xlsx`
- Contains data for 1,594 companies with 36 columns including::
  - Ticker and company name
  - Market capitalization
  - Sector classifications (GICS and BICS)
  - Valuation metrics (P/E, P/B, P/S)
  - Factor exposures (Size, Value, Momentum, Volatility, Profitability, etc.)
  - ESG disclosure scores
  - Employee counts (current and 5 years prior)
  - Performance metrics (Total Return, Beta)

### Price & Performance Data
- File: `AllListSmallPrices_20250411.par`
- Converted to CSV for merging and analysis

---

## Data Preparation & Cleaning

### Data Preparation
The original dataset was provided in Parquet format and downloaded from Google Drive.  
It was converted to CSV for portability and ease of reuse.

Original one-time preparation steps (run in Google Colab):

```python
! gdown 1URLvYwp6oLqegrYmej7imfpGPXXeSeaN
! gdown 1G1NWH2VkieWppoYuAW5yptzjZW4D_MNu
#Downloading...
#From: https://drive.google.com/uc?id=1URLvYwp6oLqegrYmej7imfpGPXXeSeaN
#To: /content/20250210_US_Port.xlsx
#100% 829k/829k [00:00<00:00, 110MB/s]
#Downloading...
#From: https://drive.google.com/uc?id=1G1NWH2VkieWppoYuAW5yptzjZW4D_MNu
#To: /content/AllListSmallPrices_20250411.par
#100% 48.8M/48.8M [00:00<00:00, 109MB/s]

#1. Data Preprocessing

import pandas as pd
df = pd.read_excel('20250210_US_Port.xlsx',skiprows=2)
price_data = pd.read_parquet('AllListSmallPrices_20250411.par')

price_data

# Load the Parquet file (make sure pyarrow or fastparquet is installed)
price_data = pd.read_parquet('AllListSmallPrices_20250411.par')

# Optional: preview the data structure
print("Data preview:")
print(df.head())

# Save to CSV
output_csv_path = "AllListSmallPrices_20250411.csv"
df.to_csv(output_csv_path, index=False)

print(f"✅ File saved as {output_csv_path}")

```

- Converted Parquet price data to CSV for portability
- Standardized ticker symbols across datasets
- Extracted a consistent `Ticker Symbol` key for merging

### Data Cleaning
The following steps were performed:
- Dropped columns with more than 30% missing values
- Filled remaining numeric missing values using median imputation
- Removed rows missing key identifiers (ticker or market cap)
- Merged fundamentals and price data into a unified dataset

The final cleaned dataset was exported as:
- `Merged_TradeWar_Cleaned.csv`

All data cleaning steps are fully documented in the notebook.

---

## Trade War Timeline
A structured timeline of major trade war events was created to provide context for market reactions.

The timeline includes:
- U.S. tariff announcements and escalations
- Chinese retaliatory measures
- Policy shifts and exemptions
- Key escalation points between February and April 2025

The timeline was visualized using Matplotlib to support event-driven interpretation of market behavior.

*Timeline research and formatting were assisted by ChatGPT for clarity and documentation.*

---
## Key Findings

### Market Structure
- Firm size is highly skewed: a small number of mega-cap firms dominate total market value.
- Small- and mid-cap firms account for most observations, making size a critical risk dimension.

### Sector Composition
- Financials and Technology are the most represented sectors.
- Industrials and Consumer Discretionary show broad exposure to global supply chains.
- Utilities and Real Estate are smaller and more concentrated.

### Pre-Trade-War Performance
- Small-cap firms outperformed mid- and large-caps prior to the trade war, reflecting elevated risk appetite.
- Returns were highly concentrated, with a long right tail driven by a small number of firms.

### Risk & Factor Drivers
- Beta (Y-1) clustered around 1 and explained little of the cross-sectional return variation.
- Momentum exhibited a strong positive correlation with returns.
- Value, dividend yield, and profitability were negatively correlated with performance, consistent with a risk-on market regime.

### Business Structure
- Workforce size showed no strong relationship with returns.
- Sector and business model mattered more than labor scale alone.
- Asset-light firms displayed greater dispersion and upside potential.

---

## Conclusions & Implications
The U.S. equity market entered the 2025 trade war in a momentum-driven, risk-seeking environment. Performance was driven more by factor positioning and business structure than by traditional risk measures such as beta.

This baseline context is essential for understanding how trade-war escalation later altered investor behavior and firm resilience.

**Portfolio implications:**
- Do not rely on momentum during geopolitical risk
- Use size as a risk control, not a return predictor
- Emphasize balance-sheet strength and operational flexibility
- Combine sector, factor, and structural signals for resilience analysis

---

## Key Takeaway
Establishing a clean pre-shock baseline reveals that market risk pricing before the trade war was fundamentally different from conditions during policy escalation, underscoring the importance of context in event-driven financial analysis.
---

## Visualizations Included

- **Trade War Timeline (2025)**  
  Key U.S.–China tariff escalation events visualized to provide macroeconomic context for the analysis.

- **Sector Distribution (BICS Level 1)**  
  Bar chart showing the number of firms by sector to illustrate market composition and exposure prior to the trade war.

- **Market Capitalization Distribution (Log Scale)**  
  Histogram highlighting the right-skewed nature of firm size and the dominance of mega-cap companies.

- **Market Cap Tier vs Total Return (Y-1)**  
  Comparison of average pre-trade-war returns across small-, mid-, and large-cap firms.

- **Beta (Y-1) Distribution**  
  Distribution of pre-trade-war market sensitivity to establish baseline risk exposure.

- **Beta vs Total Return (Y-1) with Regression Line**  
  Scatter plot with fitted regression to assess the relationship between market risk and returns before the trade war.

- **Factor Exposure vs Total Return (Y-1) Correlation Heatmap**  
  Heatmap showing how momentum, value, volatility, leverage, and other factor exposures related to returns in the pre-trade-war period.

- **Total Return (Y-1) Distribution**  
  Histogram illustrating dispersion, skewness, and concentration of firm-level returns prior to the trade war.

- **Employee Count vs Total Return (Bubble Plot)**  
  Scatter plot (bubble size = market cap) examining how workforce size and sector characteristics relate to pre-trade-war performance.

- **Factor Exposure Distributions**  
  Individual distributions of major factor exposures to confirm balance and dispersion across firms.

- **Factor Correlation Matrix**  
  Heatmap showing relationships among factor exposures and confirming limited multicollinearity.



