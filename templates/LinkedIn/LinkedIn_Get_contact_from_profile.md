<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# LinkedIn - Get contact from profile
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Get_contact_from_profile.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #linkedin #profile #contact #naas_drivers

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

### Enter profile URL


```python
PROFILE_URL = "PROFILE_URL"
```

## Model

Get the information return in a dataframe.<br><br>
**Available columns :**
- PROFILE_URN : LinkedIn unique profile id
- PROFILE_ID : LinkedIn public profile id
- EMAIL
- CONNECTED_AT
- BIRTHDATE
- TWITER
- ADDRESS
- WEBSITES
- INTERESTS


```python
df = linkedin.connect(LI_AT, JSESSIONID).profile.get_contact(PROFILE_URL)
```

## Output

### Display result


```python
df
```