# Retail Demand Forecasting & Inventory Optimisation

Forecasting daily sales for 1,782 store × product-family combinations at an Ecuadorian grocery chain, then turning those forecasts into inventory decisions that reduce stockouts and excess stock.

> **Status:** 🚧 In progress. Built step by step; see the roadmap below.

## Business problem

Retailers lose money in two directions: **stockouts** (lost sales and unhappy customers) and **overstock** (tied-up cash, waste, especially for perishables). Better demand forecasts let a business order closer to what it will actually sell.

**Goal:** forecast the next 16 days of sales for every store and product family, beat simple baseline methods, and estimate the business impact through an inventory simulation.

## Data

[Corporación Favorita: Store Sales, Time Series Forecasting](https://www.kaggle.com/competitions/store-sales-time-series-forecasting) (Kaggle)

| File | Contents |
|---|---|
| `train.csv` | Daily sales by store and product family, Jan 2013 – Aug 2017 (3M rows) |
| `stores.csv` | City, state, store type and cluster for 54 stores |
| `holidays_events.csv` | National, regional and local holidays |
| `oil.csv` | Daily oil price (Ecuador's economy is oil-dependent) |
| `transactions.csv` | Daily customer transactions per store |

## Roadmap

- [x] **1. Exploratory data analysis**: trends, seasonality, promotions, holidays ([notebook](notebooks/01_eda.ipynb))
- [ ] **2. Baselines**: naive and moving-average forecasts to beat
- [ ] **3. Feature engineering + LightGBM model**
- [ ] **4. Evaluation and error analysis**
- [ ] **5. Inventory simulation**: reorder points and stockouts avoided
- [ ] **6. Interactive Streamlit dashboard**
- [ ] **7. Final write-up of results**

## Key findings so far

- Average daily sales grew **~2.2×** from 2013 to 2017.
- Strong weekly cycle: weekends sell **20–30% above** an average day, and December runs **27% above** average.
- The top 5 product families account for **79%** of sales.
- Raw promo vs non-promo comparisons are misleading (promotions target high-volume families), so lift is measured within each family.

## Project structure

```
├── data/raw/          # Kaggle data (not committed; see setup)
├── notebooks/         # Step-by-step analysis notebooks
├── src/               # Reusable Python code (features, models)
├── app/               # Streamlit dashboard
├── requirements.txt   # Python dependencies
└── README.md
```

## How to run

```bash
git clone https://github.com/SanikaC05/retail-demand-forecasting.git
cd retail-demand-forecasting
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# Download the data (needs a Kaggle API key in ~/.kaggle/kaggle.json)
kaggle competitions download -c store-sales-time-series-forecasting -p data/raw
unzip data/raw/store-sales-time-series-forecasting.zip -d data/raw
```

Then open the notebooks in order.

## Tech stack

Python · pandas · scikit-learn · LightGBM · matplotlib / seaborn · Streamlit · Plotly
