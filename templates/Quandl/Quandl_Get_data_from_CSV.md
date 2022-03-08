<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Quandl/Quandl_Get_data_from_CSV.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #quandl #marketdata #opendata

## Input

### Import librairies


```python
import matplotlib.pyplot as plt
import pandas as pd
import os 
```

## Model

### Read CSV with pandas


```python
data = pd.read_csv('https://www.quandl.com/api/v3/datasets/BITFINEX/BTCUSD.csv?api_key=bxrSXWimkiknuCcV71uL')
data
```

## Output

### Visualize & plot chart


```python
%matplotlib inline
```


```python
data.plot()
```
