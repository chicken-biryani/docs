<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Cityfalcon/Cityfalcon_Get_data_from_API.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #cityfalcon #news

## Input

### Import library


```python
from naas_drivers import cityfalcon
```

### Variable


```python
API_KEY = "YOUR_API_KEY"
```

## Model

### Connect to cityfalcon


```python
CF = cityfalcon.connect(API_KEY).get("TSLA")
```

## Output

### Display result


```python
CF
```
