<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Get_contacts_associated_to_deal.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #hubspot #crm #sales #deal #contact #naas_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import library


```python
from naas_drivers import hubspot
```

### Setup your HubSpot
👉 Access your [HubSpot API key](https://knowledge.hubspot.com/integrations/how-do-i-get-my-hubspot-api-key)


```python
HS_API_KEY = 'YOUR_HUBSPOT_API_KEY'
```

### Enter deal ID


```python
deal_id = '3452242690'
```

## Model

### Get association


```python
result = hubspot.connect(HS_API_KEY).associations.get('deal', 
                                                      deal_id,
                                                      'contact')
```

## Output

### Display result


```python
result
```
