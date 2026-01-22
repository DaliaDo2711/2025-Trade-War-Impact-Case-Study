# 2025-Trade-War-Impact-Case-Study
Data Visualization using Python

Geopolitical Risk and Portfolio Resilience Analysis

## Quick Links
- Google Colab Notebook: https://drive.google.com/file/d/1WzgzTG90VAL9lSd-09AQd_-sgE5UxQff/view?usp=sharing 
---

## Project Overview
This case study analyzes how U.S. companies across different sectors were affected by a **trade war initiated in early 2025**. Using Bloomberg-provided company fundamentals, factor exposures, and market performance data, the project examines which business characteristics demonstrated **resilience** and which created **vulnerability** during periods of heightened geopolitical risk.

The analysis focuses on sector performance, risk–return behavior, factor exposure patterns, ESG disclosure, and employment structure to provide **actionable insights for portfolio managers** facing future trade tensions.

---

## Project Motivation
Geopolitical trade conflicts can introduce sudden shocks to financial markets, disrupting supply chains, pricing power, and investor sentiment. While trade wars are macroeconomic events, their impacts are often **uneven across sectors and business models**.

This project aims to:
- Identify which sectors and company profiles were most resilient during the 2025 trade war
- Understand how factor exposures and firm characteristics influenced performance
- Translate analytical findings into portfolio strategy recommendations

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

## Analysis & Key Findings

### Sector-Level Performance
- Technology and Consumer Discretionary sectors dominated market capitalization
- These sectors also showed stronger average returns, suggesting pricing power and adaptability
- More defensive sectors (Utilities, Materials, Real Estate) had smaller market cap representation

### Risk vs Return
- Beta showed **no strong relationship** with total return during the trade war period
- Traditional CAPM-style risk measures were less informative during geopolitical shocks

### Factor Exposure Analysis
Correlation analysis revealed:
- Positive association between returns and **Momentum** and **Value** exposures
- Negative association between returns and **Volatility**, **Leverage**, and **Earnings Variability**
- Profitability and dividend-related factors showed moderate resilience

### ESG & Employment Structure
- ESG disclosure scores varied widely across firms
- Employment-heavy companies showed mixed performance, suggesting sector-dependent labor sensitivity
- Workforce scale alone did not predict returns, but interacted with sector exposure

---

## Visualizations Included
- Sector distribution by company count (BICS Level 1)
- Market capitalization distribution (log scale)
- ESG disclosure score distribution
- Beta (Y-1) distribution
- Beta vs Total Return scatter plot by sector
- Factor exposure vs return correlation heatmap
- Total Return (Y-1) distribution
- Employee count vs Total Return bubble plot
- Factor exposure distributions
- Factor correlation matrix

---

## Key Takeaways
- Market responses to trade war shocks are **multi-dimensional**
- Beta alone is insufficient for understanding performance during geopolitical stress
- Factor exposures provide stronger explanatory power than traditional risk metrics
- Resilient portfolios favored companies with:
  - Lower leverage
  - Lower volatility
  - Strong momentum
  - Value characteristics
- Sector exposure and business structure matter more than firm size alone

---

## Portfolio Implications
For portfolio managers preparing for future trade tensions:
- Overweight sectors with pricing power and adaptive supply chains
- De-emphasize beta during event-driven volatility
- Apply multi-factor strategies emphasizing stability and valuation strength
- Monitor labor-intensive firms for policy and cost sensitivity

---
