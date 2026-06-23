# Explainable Neural Networks for S&P 500 Volatility-Regime Forecasting

This repository contains the reproducible notebook for forecasting five-day S&P 500 volatility regimes and evaluating multiple time-series XAI methods.

## Contents

- `notebooks/sp500_volatility_xai.ipynb`: cleaned, execution-ready analysis notebook
- `requirements.txt`: Python dependencies
- `outputs/`: generated figures, tables, and run metadata; contents are ignored by Git
- `external/`: location for the external C-SHAP repository; contents are ignored by Git

## Setup

Use Python 3.11 or 3.12. From the repository root:

```bash
python -m venv .venv
```

Activate the environment:

```bash
# macOS/Linux
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Install the dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Clone the official C-SHAP implementation as an external dependency:

```bash
git clone https://github.com/SaxionAMI/CSHAP-for-time-series.git external/CSHAP-for-time-series
```

Start Jupyter from the repository root:

```bash
jupyter lab
```

Open `notebooks/sp500_volatility_xai.ipynb`, then select **Restart Kernel and Run All Cells**. The notebook downloads market data from Yahoo Finance and writes generated artifacts to `outputs/`.

## Reproducibility notes

- The random seed is fixed in the notebook configuration.
- The data split is chronological: 70% training, 15% validation, and 15% test data.
- Target thresholds and feature scaling are fitted using the training period only.
- Classification thresholds and the neural model selected for explanation are determined using validation balanced accuracy.
- The notebook records its configuration and package versions in `outputs/run_metadata.json`.
- GPU and CPU runs can still differ slightly because some low-level numerical operations are hardware dependent.

## Generated outputs

The notebook generates model-performance tables, probability plots, local explanation figures, explanation-evaluation tables, C-SHAP figures, and run metadata. Generated files are excluded from version control by default to keep the repository compact.

## Data and external code

S&P 500 market data are downloaded at runtime through `yfinance`. C-SHAP is loaded from the separately cloned external repository and is not vendored into this project.
