# Kenya Food Price Early Warning: Forecasting Maize Prices with Deep Learning and Time Series Models

> Can a neural network give Kenyan households, farmers and planners an earlier warning of food price spikes than simpler statistical models? This project tests that question honestly, using open market price data.

**Author:** _Your Name_ · **Programme:** Zindua School, Data Science · **Date:** _Month Year_

---

## Table of Contents

1. [Problem Statement](#problem-statement)
2. [Who Is Affected](#who-is-affected)
3. [Objectives](#objectives)
4. [Data](#data)
5. [Approach](#approach)
6. [Models](#models)
7. [Evaluation](#evaluation)
8. [Repository Structure](#repository-structure)
9. [How to Run](#how-to-run)
10. [Results](#results)
11. [Limitations](#limitations)
12. [Acknowledgements and Data Attribution](#acknowledgements-and-data-attribution)

---

## Problem Statement

Maize is the staple food for most Kenyan households, and its price moves sharply from season to season and from market to market. Price spikes caused by drought, poor harvests, transport costs or supply shocks reach consumers and farmers before anyone has time to respond. Households cut back on meals, farmers sell or plant at the wrong time, and government and humanitarian agencies react to a crisis that is already under way.

Forecasting food prices is hard for three reasons:

- **Seasonality and shocks overlap.** Regular harvest cycles mix with irregular events such as droughts, so a model must separate the two.
- **Volatility is not constant.** Calm periods are followed by turbulent ones, which simple forecasts that assume stable variance handle poorly.
- **The data is small.** Monthly prices give only a few hundred observations per market, which is often too little for deep learning to beat simpler models.

This project builds and compares forecasting models on Kenyan market prices, then turns the best forecast into a **simple price-spike early-warning signal**. It also asks a question that is often skipped: **does a neural network actually outperform a simple seasonal baseline on small monthly data?**

## Who Is Affected

| Group | How price volatility affects them | How this project helps |
|---|---|---|
| **Low-income urban and rural households** | Food takes up a large share of spending, so price spikes force cuts in food quantity and quality | An earlier signal of rising prices |
| **Smallholder farmers** | Planting, storage and selling decisions depend on expected prices | Forecasts to support when to sell or store |
| **Traders and millers** | Stock purchasing and pricing depend on price direction | Short-term outlook per market |
| **County and national government** (e.g. NDMA, Ministry of Agriculture) | Need lead time to release strategic reserves or target support | A quantified early-warning indicator |
| **Humanitarian organisations** (e.g. WFP) | Plan cash and food assistance around price shocks | Market-level risk signals |

## Objectives

1. Build a clean, reproducible monthly price dataset for maize across selected Kenyan markets.
2. Forecast maize prices 1 to 3 months ahead with several model families and compare them fairly.
3. Model **price volatility** to identify when prices become unpredictable.
4. Test whether **rainfall** improves the forecasts (optional extension).
5. Convert forecasts into a **price-spike alert** and measure how often it gives a correct warning.
6. Report honestly where the complex models do and do not beat simple baselines.

## Data

| Source | What it provides | Access |
|---|---|---|
| **WFP Kenya Food Prices** via the [Humanitarian Data Exchange (HDX)](https://data.humdata.org/dataset/wfp-food-prices-for-kenya) | Market-level retail prices by commodity and date, from 2006 onwards | Public, Creative Commons Attribution for Intergovernmental Organisations (CC BY-IGO) licence, updated monthly |
| **CHIRPS** rainfall (optional) | Satellite-based rainfall estimates for exogenous features | Free download |
| **EPRA** fuel prices (optional) | Pump prices as a transport-cost proxy | Public reports |

**Data selection:** The WFP dataset has uneven coverage across markets and commodities. Markets and the primary commodity are therefore chosen **after a coverage audit**, keeping only series with long, mostly complete histories. Gaps are documented and handled explicitly (see the data-cleaning notebook) rather than filled silently.

## Approach

1. **Data audit and cleaning:** check coverage by market, commodity and month; standardise units; handle gaps and outliers; document every decision.
2. **Exploratory analysis:** seasonality, trend, regional differences, and periods of unusual volatility.
3. **Baselines first:** establish what "doing nothing clever" scores before any advanced model.
4. **Model development:** statistical, volatility and neural models trained under the same validation scheme.
5. **Walk-forward validation:** models are trained on the past and tested on the future in rolling windows. Random train/test splits are deliberately **not** used because they leak future information and overstate performance.
6. **Hyperparameter tuning** within the training window only.
7. **Early-warning layer:** define a spike (for example, a rise of at least a chosen percentage over the next 3 months, threshold tuned from the data), then evaluate the alert with precision and recall.
8. **Error analysis:** examine where and why each model fails, including during major shocks.

## Models

| Model | Role |
|---|---|
| **Naive** (last observed value) | Minimum baseline |
| **Seasonal naive** (same month last year) | Strong, simple baseline that any advanced model should beat |
| **Prophet** | Trend and seasonality decomposition with interpretable components |
| **ARCH / GARCH** | Models changing volatility in price changes, identifying unstable periods |
| **LSTM / GRU** | Sequence models that learn non-linear temporal patterns, with and without rainfall as an extra input |

Model families are compared under identical data splits and metrics.

## Evaluation

- **Forecast accuracy:** RMSE, MAE, MAPE, and MASE (relative to the seasonal naive baseline)
- **Validation:** expanding-window walk-forward cross-validation
- **Horizons:** 1, 2 and 3 months ahead
- **Early-warning quality:** precision, recall and F1 for spike alerts, with attention to missed spikes, since a missed warning is costlier than a false alarm
- **Statistical comparison:** a significance test on forecast errors between top models (for example, Diebold-Mariano), so that small gaps are not over-interpreted

## Repository Structure

```
kenya-food-price-forecasting/
├── data/
│   ├── raw/                 # Original downloads (not modified)
│   └── processed/           # Cleaned monthly series
├── notebooks/
│   ├── 01_data_audit_and_cleaning.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   ├── 03_baselines.ipynb
│   ├── 04_prophet.ipynb
│   ├── 05_garch_volatility.ipynb
│   ├── 06_lstm_gru.ipynb
│   ├── 07_model_comparison.ipynb
│   └── 08_early_warning.ipynb
├── src/                     # Reusable functions (loading, validation, metrics)
├── reports/figures/         # Saved charts
├── requirements.txt
└── README.md
```

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/kenya-food-price-forecasting.git
cd kenya-food-price-forecasting

# 2. Create an environment and install dependencies
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 3. Download the WFP Kenya food prices CSV from HDX into data/raw/
#    https://data.humdata.org/dataset/wfp-food-prices-for-kenya

# 4. Run the notebooks in order (01 to 08)
```

**Main libraries:** pandas, NumPy, scikit-learn, statsmodels, arch, Prophet, TensorFlow/Keras (or PyTorch), matplotlib, seaborn.

## Results

_To be completed after modelling._

| Model | 1-month RMSE | 3-month RMSE | MASE vs seasonal naive |
|---|---|---|---|
| Naive | | | |
| Seasonal naive | | | 1.00 |
| Prophet | | | |
| LSTM / GRU | | | |

**Key findings:** _Summarise which model performed best, whether rainfall helped, and how the early-warning alert performed._

## Limitations

- Retail price data is reported monthly and covers only the markets WFP monitors, so it may not represent all Kenyan regions.
- Some series contain gaps; results depend on how these are handled.
- A few hundred monthly observations per series limit what neural networks can learn, so they may not beat simpler models.
- Forecasts cannot anticipate shocks that have no precedent in the historical data.
- This is an academic project and **not** an operational forecasting service.

## Acknowledgements and Data Attribution

- Price data: **World Food Programme (WFP)**, distributed via the **Humanitarian Data Exchange (HDX)** under the CC BY-IGO licence. Please cite WFP and HDX when reusing it.
- Rainfall data (if used): **Climate Hazards Group, CHIRPS**.
- Project completed as a capstone at **Zindua School**.

## License

Code: _choose a licence, e.g. MIT_. Data remains subject to the licences of its original providers.
