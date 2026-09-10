# Predicting U.S. Electricity Generation

A time-series forecasting project comparing **Seasonal ARIMA (SARIMA)** and a **Long Short-Term Memory (LSTM)** neural network on monthly U.S. electricity generation data.

This was a collaborative **DAEN 430** final project by **Maddie Bird, Henry Supp, and Jade Winebright**.

## Project overview

The dataset contains **142 monthly observations from January 1985 through October 1996**. The goal was to forecast electricity generation while accounting for the strong annual seasonal pattern in the series.

We compared two approaches:

- **SARIMA:** a classical time-series model that explicitly models autoregressive, differencing, moving-average, and seasonal components.
- **LSTM:** a stacked recurrent neural network using a **12-month sliding window** to learn temporal and seasonal patterns.

To avoid time-series leakage, both approaches used a **chronological 80/20 train/test split**.

## Results

| Model | Test RMSE | Test MASE |
|---|---:|---:|
| SARIMA | **8.484** | **0.844** |
| LSTM | 27.946 | 2.724 |

For this dataset, **SARIMA performed substantially better**. With only 142 observations and a strong, regular 12-month seasonal pattern, the classical model was more accurate, faster to train, and easier to interpret. The comparison also illustrates an important modeling lesson: a more complex model is not automatically the better model, especially when data is limited.

## Repository structure

```text
.
├── README.md
├── data/
│   └── electricity.csv
├── code/
│   ├── 01_sarima_forecast.ipynb
│   └── 02_lstm_forecast.ipynb
├── presentation/
│   └── Presentation Slides.pdf
└── requirements.txt
```

## Methods

### SARIMA

The SARIMA workflow:

1. Converts the monthly observations into a time-series object with frequency 12.
2. Preserves chronological order in the train/test split.
3. Uses `auto.arima(..., seasonal = TRUE)` to select the model order.
4. Forecasts the held-out test period.
5. Evaluates the forecast against the actual observations.

### LSTM

The LSTM workflow:

1. Scales the data using a `MinMaxScaler` fit on the training set only.
2. Creates supervised sequences using the previous **12 months** to predict the next month.
3. Uses a stacked architecture with **32-unit** and **16-unit** LSTM layers.
4. Applies **L2 regularization**, **0.2 dropout**, and **early stopping** to control overfitting.
5. Produces one-step forecasts and evaluates them on the held-out test period.

## Running the project

Clone the repository and run the notebooks **from the repository root** so the relative path `data/electricity.csv` works correctly.

### Python / LSTM

```bash
pip install -r requirements.txt
```

Then open `code/02_lstm_forecast.ipynb`.

### R / SARIMA

Install the R package once if it is not already available:

```r
install.packages("forecast")
```

Then open `code/01_sarima_forecast.ipynb` with an R kernel.

## Key takeaway

The project demonstrates model selection based on the characteristics of the data rather than model complexity. On a small, strongly seasonal dataset, SARIMA captured the underlying structure more effectively than the LSTM.

## Data source

Makridakis, Wheelwright, and Hyndman (1998), as cited in the course project materials.
