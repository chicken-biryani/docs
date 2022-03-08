<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Update_jobtitle_country_industry_from_linkedin.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #hubspot #crm #sales #contact #naas_drivers #linkedin #identity #scheduler #naas

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import library


```python
from naas_drivers import hubspot, linkedin
import naas
import pandas as pd
```

### Setup your HubSpot
👉 Access your [HubSpot API key](https://knowledge.hubspot.com/integrations/how-do-i-get-my-hubspot-api-key)


```python
HS_API_KEY = 'YOUR_HUBSPOT_API_KEY'
```

### Setup your LinkedIn
👉 Get <a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>your cookies</a>


```python
LI_AT = 'YOUR_COOKIE_LI_AT'  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = 'YOUR_COOKIE_JSESSIONID'  # EXAMPLE ajax:8379907400220387585
```

### Schedule your notebook everyday


```python
#-> Uncomment the 2 lines below (by removing the hashtag) to schedule your job everyday at 8:00 AM (NB: you can choose the time of your scheduling bot)
# import naas
# naas.scheduler.add(cron="0 8 * * *")

#-> Uncomment the line below (by removing the hashtag) to remove your scheduler
# naas.scheduler.delete()
```

## Model

### Get all contacts in Hubspot


```python
properties_list = [
    "hs_object_id",
    "firstname",
    "lastname",
    "linkedinbio",
    "jobtitle",
    "country",
    "industry",
]
hubspot_contacts = hubspot.connect(HS_API_KEY).contacts.get_all(properties_list)
hubspot_contacts
```

### Filter to get "jobtitle", "country", "industry" = "Not Defined" and "linkedinbio" = defined


```python
df_to_update = hubspot_contacts.copy()

# Cleaning
df_to_update = df_to_update.fillna("Not Defined")

# Filter on "Not defined"
df_to_update = df_to_update[(df_to_update.linkedinbio != "Not Defined") &
                            (df_to_update.jobtitle == "Not Defined") &
                            (df_to_update.country == "Not Defined") & 
                            (df_to_update.industry == "Not Defined")]

# Limit to last 50 contacts
df_to_update = df_to_update.sort_values(by="createdate", ascending=False)[:50].reset_index(drop=True)

df_to_update
```

### Get identity from Linkedin


```python
for _, row in df_to_update.iterrows():
    linkedinbio = row.linkedinbio
    
    # Get followers
    df = linkedin.connect(LI_AT, JSESSIONID).profile.get_identity(linkedinbio)
    jobtitle = df.loc[0, "OCCUPATION"]
    industry = df.loc[0, "INDUSTRY_NAME"]
    country = df.loc[0, "COUNTRY"]
        
    # Get linkedinbio
    df_to_update.loc[_, "jobtitle"] = jobtitle
    df_to_update.loc[_, "industry"] = industry
    df_to_update.loc[_, "country"] = country
    
df_to_update
```

## Output

### Update jobtitle, country, industry in Hubspot


```python
for _, row in df_to_update.iterrows():
    # Init data
    data = {}
    
    # Get data
    hs_object_id = row.hs_object_id
    jobtitle = row.jobtitle
    industry = row.industry
    country = row.country

    # Update 
    if jobtitle != None:
        data = {"properties": 
                {"jobtitle": jobtitle,
                 "industry": industry,
                 "country": country}
               }
    hubspot.connect(HS_API_KEY).contacts.patch(hs_object_id, data)
```
