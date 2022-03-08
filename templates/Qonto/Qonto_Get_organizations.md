<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Qonto/Qonto_Get_organizations.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #qonto #bank #organizations #positions #naas_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import library


```python
from naas_drivers import qonto
```

### Get your Qonto credentials
<a href='https://www.notion.so/naas-official/Qonto-driver-Get-your-credentials-0cc97828b4e7467c8bfbcf704a77e5f4'>How to get your credentials ?</a>


```python
QONTO_USER_ID = 'YOUR_USER_ID'
QONTO_SECRET_KEY = 'YOUR_SECRET_KEY'
```

## Model

### Get organizations


```python
df_organizations = qonto.connect(QONTO_USER_ID, QONTO_SECRET_KEY).organizations.get()
```

## Output

### Display result


```python
df_organizations
```
