<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Send_comments_from_post_in_gsheet.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #linkedin #post #comments #gsheet #naas_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

In this template, you will extract comments from post and divide them in 2 categories :
- People in your network
- People not in your network

Then, data will be sent in 3 sheets to trigger specific actions:
- POST_COMMENTS : total of comments from post
- MY_NETWORK : People in your network
- NOT_MY_NETWORK : People not in your network

Check the other templates to create a full workflow

## Input

### Import libraries


```python
from naas_drivers import linkedin, gsheet
import random
import time
import pandas as pd
from datetime import datetime
```

### Variables

#### LinkedIn

##### Get your cookies
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
LI_AT = 'YOUR_COOKIE_LI_AT'  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = 'YOUR_COOKIE_JSESSIONID'  # EXAMPLE ajax:8379907400220387585
```

##### Enter your post URL


```python
POST_URL = "POST_URL"
```

#### Gsheet

##### Enter your gsheet info

- Your spreadsheet id is located in your gsheet url after "https://docs.google.com/spreadsheets/d/" and before "/edit"
- Remember that you must share your gsheet with our service account to connect : naas-share@naas-gsheets.iam.gserviceaccount.com
- You must create your sheet before sending data into it


```python
# Spreadsheet id
SPREADSHEET_ID = "SPREADSHEET_ID"

# Sheet names
SHEET_POST_COMMENTS = "POST_COMMENTS"
SHEET_MY_NETWORK = "MY_NETWORK"
SHEET_NOT_MY_NETWORK = "NOT_MY_NETWORK"
```

### Constant


```python
DATETIME_FORMAT = "%Y-%m-%d %H:%M:%S"
```

### Get likes from post


```python
df_posts = linkedin.connect(LI_AT, JSESSIONID).post.get_comments(POST_URL)
df_posts["DATE_EXTRACT"] = datetime.now().strftime(DATETIME_FORMAT)
```

## Model

### Get network for profiles


```python
df_network = pd.DataFrame()

for _, row in df_posts.iterrows():
    profile_id = row.PROFILE_ID
    # Get network information to know distance between you and people who likes the post
    tmp_network = linkedin.connect(LI_AT, JSESSIONID).profile.get_network(profile_id)
    # Concat dataframe
    df_network = pd.concat([df_network, tmp_network], axis=0)
    # Time sleep in made to mimic human behavior, here it is randomly done between 2 and 5 seconds
    time.sleep(random.randint(2, 5))

df_network.head(5)
```

### Merge posts likes and network data


```python
df_all = pd.merge(df_posts, df_network, on=["PROFILE_URN", "PROFILE_ID"], how="left")
df_all = df_all.sort_values(by=["FOLLOWERS_COUNT"], ascending=False)
df_all = df_all[df_all["DISTANCE"] != "SELF"].reset_index(drop=True)
df_all.head(5)
```

### Split my network or not


```python
# My network
my_network = df_all[df_all["DISTANCE"] == "DISTANCE_1"].reset_index(drop=True)
my_network["DATE_EXTRACT"] = datetime.now().strftime(DATETIME_FORMAT)
my_network.head(5)
```


```python
# Not in my network
not_my_network = df_all[df_all["DISTANCE"] != "DISTANCE_1"].reset_index(drop=True)
not_my_network["DATE_EXTRACT"] = datetime.now().strftime(DATETIME_FORMAT)
not_my_network.head(5)
```

## Output

### Save post comments in gsheet


```python
gsheet.connect(SPREADSHEET_ID).send(df_posts, sheet_name=SHEET_POST_COMMENTS, append=False)
```

### Save people from my network in gsheet


```python
gsheet.connect(SPREADSHEET_ID).send(my_network, sheet_name=SHEET_MY_NETWORK, append=False)
```

### Save people not in my network in gsheet


```python
gsheet.connect(SPREADSHEET_ID).send(not_my_network, sheet_name=SHEET_NOT_MY_NETWORK, append=False)
```
