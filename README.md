# Stock Market Prediction with LSTM

Forecasts short-term Microsoft (MSFT) stock prices from one-minute intraday data using a stacked Long Short-Term Memory (LSTM) network built with TensorFlow/Keras.

## Overview

Stock prices are sequential, so this project uses an LSTM to learn from the previous 100 minutes of prices and predict the next one. The trained model is then used to forecast the next 30 minutes recursively.

## Data

- **Source:** [Alpha Vantage](https://www.alphavantage.co/) intraday API
- **Symbol:** MSFT, closing price at 1-minute intervals
- **Size:** 5,396 observations (most recent point: 9 June 2022)
- **Scaling:** MinMax scaling to the range 0 to 1
- **Split:** 65% train, 35% test (chronological)

## Model

| Setting | Value |
| ------- | ----- |
| Input | Previous 100 minutes of closing prices |
| Architecture | 3 stacked LSTM layers (50 units each) and a Dense output layer |
| Loss / optimizer | Mean squared error / Adam |
| Training | 100 epochs, batch size 64 |

## Run it

1. Get a free API key from Alpha Vantage.
2. Set it as an environment variable (do not paste it into the notebook):
   - macOS/Linux: `export ALPHAVANTAGE_API_KEY=your_key`
   - Windows: `set ALPHAVANTAGE_API_KEY=your_key`
3. Install and run:

```bash
git clone https://github.com/Nishtha-Tiku/Stock-Market-Prediction.git
cd Stock-Market-Prediction
pip install -r requirements.txt
jupyter notebook "Stock Market prediction.ipynb"
```

Data is fetched live, so results will differ from run to run.

## Limitations

- Uses past closing prices only
- One stock and a short time window
- Multi-step forecasts feed predictions back in, so errors build up
- Learning project, not financial advice

## Future work

- Compare against other baselines
- Add features such as volume and news sentiment
