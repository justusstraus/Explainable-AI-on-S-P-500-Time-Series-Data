# S&P 500 Volatility Regime Forecasting with XAI

This project forecasts whether the S&P 500 will enter a high-volatility regime over the next five trading days. The goal is not to provide a trading strategy, but to compare neural-network time-series models and explain their predictions with multiple XAI methods.

## Project summary

The prediction task is binary:

```text
1 = high-volatility regime
0 = normal/low-volatility regime
```

High volatility is defined as future five-day realized volatility above the 70th percentile of the training period. The threshold is estimated only on the training set to avoid look-ahead bias.

## Models

The main multivariate models use a 30-day lookback window with engineered financial features:

- LSTM
- 1D CNN
- Transformer Encoder

An additional univariate LSTM is trained on the `volatility_20` channel for the official decomposition-based C-SHAP method.

## Explainability methods

The project includes:

- Concept-level Shapley attribution
- WindowSHAP
- Integrated Gradients
- Official decomposition-based C-SHAP
- TP / FP / TN / FN C-SHAP case studies

## Data

The notebook downloads S&P 500 data using `yfinance` with ticker:

```text
^GSPC
```

The following features are engineered:

- daily log return
- absolute return
- squared return
- high-low range
- open-close range
- volume change
- moving-average gaps
- rolling volatility
- RSI

## C-SHAP dependency

This project uses the official C-SHAP implementation from:

https://github.com/SaxionAMI/CSHAP-for-time-series

The C-SHAP source code is not redistributed in this repository. To run the official C-SHAP section, clone the original repository:

```bash
git clone https://github.com/SaxionAMI/CSHAP-for-time-series.git
```

Then either:

1. place this notebook inside the cloned `CSHAP-for-time-series` folder, or
2. adjust the C-SHAP import path in the notebook.

Please follow the license terms of the original C-SHAP repository.

## Installation

Create an environment and install the required packages:

```bash
pip install -r requirements.txt
```

If you run the notebook inside the official C-SHAP repository, also install its requirements:

```bash
pip install -r requirements.txt
```

If packages such as `pywt` or `emd` are missing, install:

```bash
pip install PyWavelets emd
```

## Repository structure

```text
sp500-volatility-xai/
├── notebooks/
│   └── sp500_volatility_xai.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Running the notebook

Open:

```text
notebooks/sp500_volatility_xai.ipynb
```

Run the cells from top to bottom. The notebook creates an `outputs/` folder with figures and CSV files.

## Main outputs

The notebook saves:

- model performance table
- probability plots
- concept attribution plots
- WindowSHAP plots
- Integrated Gradients heatmaps
- official C-SHAP instance-level visualizations
- TP / FP / TN / FN C-SHAP figures

## Disclaimer

This project is for educational purposes only. It is not financial advice and should not be used for trading or investment decisions.
