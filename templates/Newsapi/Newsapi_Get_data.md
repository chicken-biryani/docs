<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Newsapi/Newsapi_Get_data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #newsapi #news

## Input

### Import library


```python
from naas_drivers import newsapi
```

## Model

### Fill in the informations you want to have


```python
fields = ["image", "title"]
COMPANY = "TSLA"
```

## Output

### Display result


```python
newsapi.get(COMPANY, fields=fields)
```
