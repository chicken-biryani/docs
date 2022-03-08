<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Get_guests_from_event.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #linkedin #event #guests #naas_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import library


```python
from naas_drivers import linkedin
```

### Get your cookies
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
LI_AT = 'YOUR_COOKIE_LI_AT'  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = 'YOUR_COOKIE_JSESSIONID'  # EXAMPLE ajax:8379907400220387585
```

### Enter event URL


```python
EVENT_URL = "EVENT_URL"
```

## Model

Note : works only if you are in the attendees list

Get the information returned in a dataframe.<br><br>
**Available columns :**
- PROFILE_URN : LinkedIn unique profile id
- PROFILE_ID : LinkedIn public profile id
- NAME : First and last name
- OCCUPATION : Text below the name in the profile page
- LOCATION : Text before the first comma in the location field below profile 
- DISTANCE : Field next to the profile name


```python
df = linkedin.connect(LI_AT, JSESSIONID).event.get_guests(EVENT_URL)
```

## Output

### Display result


```python
df
```
