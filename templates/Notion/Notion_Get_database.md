<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Get_database.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #notion #productivity

## Input

### Import library


```python
from naas_drivers import notion
```

### Setup Notion
<a href='https://docs.naas.ai/drivers/notion'>How to get your Notion integration token ?</a>


```python
# Enter Token API
token = "*****"

# Enter Database URL
database_url = "https://www.notion.so/********"
```

## Model

### Get database from Notion


```python
database = notion.connect(notion_token).database.get(database_url, query={})
```

## Output

### Database object


```python
database
```

### Dataframe


```python
df_notion = database.df()
df_notion
```
