**Author:** [Carlo Occhiena](https://www.linkedin.com/in/carloocchiena/)

## Input

### Install and import libraries


```python
import datetime as dt
import pandas_datareader as pdr
try:
    import mplfinance as mpf
except:
    !pip install mplfinance
    import mplfinance as mpf
try:
    import yfinance as yfin
except:
    !pip install yfinance
    import yfinance as yfin
```

### Variables
datefrom, dateto, the list of cryptocurrencies you need.


```python
# update date range "start" as desired
start = dt.datetime(2021, 1, 1)
end = dt.datetime.now()
ticker = "ETH-USD"
```

## Model
candlestick chart, correlation heatmap, visual chart for all the currencies.


```python
# insert cryptoasset (in Yahoo format "NNN-CCC" es BTC-EUR or ETH-USD) here
yfin.pdr_override()
data = yfin.download(ticker, start, end)
data
```

## Output

### Create a candlestick chart for a given asset
👉 Completely customize the timeframe and asset you need


```python
mpf.plot(data, title=f"{ticker} trend",
         type="candle",
         volume=True,
         style="yahoo")
```


```python

```
