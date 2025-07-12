# DESCRIPTION

This project provides a comprehensive pipeline for analyzing the sector-specific impact of Federal Reserve monetary policy on U.S. stock markets. It integrates data preprocessing, event study analysis, Vector Autoregression (VAR), and machine learning-based modeling (Random Forest and XGBoost) to identify and predict sector-level return behavior in response to macroeconomic conditions.

The workflow consists of the following components:

1. Data Preprocessing – Cleaning, aligning, and merging datasets to create a unified source (`fed_stock_data_preprocessed.csv`).
2. Event Study Analysis – Measuring abnormal returns around FOMC decision dates using market models.
3. Vector Autoregression (VAR) – Modeling dynamic interdependencies between macroeconomic variables and sector returns.
4. Random Forest Modeling – Identifying influential macroeconomic and market factors driving sectoral returns.
5. Gradient Boosting (XGBoost) – Building highly predictive models to forecast sector-specific returns.

# NSTALLATION

1. Download the project folder.
2. Ensure Python 3.8+ is installed.
3. Install required packages using pip:

pip install pandas numpy matplotlib seaborn statsmodels scikit-learn xgboost tqdm fredapi

4. The following datasets are required and should be placed in the same directory as the notebooks:

   - `history.csv`: Contains daily historical stock prices for S&P 500 companies (download from https://www.kaggle.com/datasets/ericstanley/us-stock-market-history-data-csv?select=dividends.csv). Includes columns such as `Date`, `Symbol`, `Close`, and `Volume`.
   - `sp500_companies.csv`: Contains company metadata including `Symbol`, `Company Name`, and `Sector`. This is used to map each ticker to its respective sector.
   - `fed_stock_data_preprocessed.csv`: Contains macroeconomic indicators such as `FedFundsRate`, `Treasury10Y`, `CPI`, `GDP`, `Unemployment`, and `VIX`. This dataset is aligned with market returns to investigate how macro conditions influence stock movements.
   - `fed_stock_data.csv`:
   - `merged_dataset.csv`:

5. These datasets are merged inside the preprocessing notebook to create a comprehensive DataFrame called `merged_data`. This merge operation aligns stock-level time series data with sector classifications and macroeconomic context using `Date` and `Symbol` as key fields.

To generate `fed_stock_data_preprocessed.csv`, macroeconomic data is downloaded directly from the FRED API. Be sure to set your API key via an environment variable or within the notebook.

# EXECUTION

1. Run 'Data_Preprocessing.ipynb':

   - Load raw data
   - Download FRED macro indicators
   - Merge and engineer features
   - Save `fed_stock_data_preprocessed.csv`

2. Run 'Event_Study_Analysis.ipynb':

   - Load datasets
   - Perform data merging to create `merged_data`
   - Define FOMC event windows
   - Estimate normal and abnormal returns
   - Compute AAR and CAR
   - Generate plots and summary tables
   - Output figures and results are saved to `plots/` and `results/`

3. Run 'Vector_Autoregression.ipynb':

   - Load the preprocessed `fed_stock_data_preprocessed.csv`
   - Apply Vector Autoregression (VAR) to model interactions between macroeconomic indicators and sector returns
   - Analyze Impulse Response Functions (IRFs) to understand how shocks in variables like interest rates or inflation propagate through different sectors
   - Use Forecast Error Variance Decomposition (FEVD) to identify which variables explain the most variation in sector returns
   - Output includes dynamic plots and tables that capture interdependencies over time

4. Run 'Random_Forest.ipynb':

   - Train sector-level models using macroeconomic and market features
   - Evaluate prediction performance (R², RMSE, directional accuracy)
   - Visualize feature importances across sectors

5. 'Run Gradient_Boosting.ipynb':
   - Train Gradient Boosting models for enhanced predictive accuracy
   - Tune hyperparameters using cross-validation
   - Benchmark against Random Forest results

# VISUALIZATION - Tableau

This Tableau dashboard provides a multi-model analysis of how U.S. stock market sectors respond to macroeconomic factors. It includes insights from Event Study, Random Forest, XGBoost, and VAR (Vector Autoregression).

Key Sections

1. Event Study Result
   - Displays cumulative abnormal return (CAR) for each sector around a defined event.
2. Random Forest Factor Importance

   - Shows relative importance of macroeconomic variables for sector performance using a Random Forest model.

3. VAR Analysis

   - Displays sector responses across a 12-month horizon to macroeconomic shocks, including CPI, Unemployment and Fed Fund Rate.

4. XGBoost Factor Analysis
   - Visualizes feature importance across sectors using XGBoost for more accurate factor interpretation.

Filter Panel (Top Right):

- Sector Filter: Use checkboxes to select one or more sectors to explore.
- Affects all charts for sector-specific analysis.

Macroeconomic Factors Used:

- CPI: Consumer Price Index (inflation)
- Fed Funds Rate: Federal Reserve's interest rate
- GDP: Gross Domestic Product
- Treasury10Y: 10-Year Treasury Yield
- Unemployment: U.S. unemployment rate
- VIX: Volatility Index (market risk perception)

# Usage:

Use this dashboard to explore how different sectors react to economic changes, identify leading macro factors, and perform scenario analysis for investment decisions.
