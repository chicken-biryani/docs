With this template, you can get data from USD EUR ticker available in [Yahoo finance](https://finance.yahoo.com/quote/USDEUR=x/).<br> 

**Author:** [Carlo Occhiena](https://www.linkedin.com/in/carloocchiena/)

## Input

### Import libraries


```python
from naas_drivers import yahoofinance, plotly
```

### Input parameters
👉 Here you can change the ticker, timeframe and add moving averages analysiss


```python
ticker = "EURUSD=X"
date_from = -365
date_to = "today"
interval = '1d'
moving_averages = [20, 50]
```

## Model

### Get dataset from Yahoo Finance


```python
df_yahoo = yahoofinance.get(ticker,
                            date_from=date_from,
                            date_to=date_to,
                            interval=interval,
                            moving_averages=moving_averages)
df_yahoo
```

## Output

### Display chart


```python
# Get last value
last_date = df_yahoo.loc[df_yahoo.index[-1], "Date"].strftime("%Y-%m-%d")
last_value = df_yahoo.loc[df_yahoo.index[-1], "Close"]

# Create chart
chart = plotly.linechart(df_yahoo,
                         x="Date",
                         y=["Close", "MA20", "MA50"],
                         showlegend=True,
                         title=f"<b>{ticker} rate as of {last_date}</b><br><span style='font-size: 13px;'>Last value: {last_value}</span>")

chart.update_layout(
    title_font=dict(family="Arial", size=18, color="black"),
    legend_font=dict(family="Arial", size=11, color="black"),
    margin_pad=10,
)
```
