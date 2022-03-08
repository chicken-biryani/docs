<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Update_deal.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #hubspot #crm #sales #deal #naas_drivers

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

### Enter deal parameters to update


```python
deal_id = "3501002068"
dealname = "TEST"
dealstage = '5102584'
closedate = '2021-12-31' #date format must be %Y-%m-%d
amount = '100.50'
hubspot_owner_id = None
```

## Model

### With patch method


```python
update_deal = {"properties": 
                  {
                    "dealstage": dealstage,
                    "dealname": dealname,
                    "amount": amount,
                    "closedate": closedate,
                    "hubspot_owner_id": hubspot_owner_id,
                   }
                 }

deal1 = hubspot.connect(HS_API_KEY).deals.patch(deal_id,
                                                update_deal)
```

### With update method


```python
deal2 = hubspot.connect(HS_API_KEY).deals.update(
    deal_id,
    dealname,
    dealstage,
    closedate,
    amount,
    hubspot_owner_id
)
```

## Output

### Display results


```python
deal1
```


```python
deal2
```
