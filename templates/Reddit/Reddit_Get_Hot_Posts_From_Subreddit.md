This notebook explains how to get hot posts from a subreddit. A subreddit is a specific online community, and the posts associated with it, on the social media website Reddit

**Author:** [Yaswanthkumar GOTHIREDDY](https://www.linkedin.com/in/yaswanthkumargothireddy/)

## Input

### Install packages


```python
!pip install praw
```


```python
import praw
import pandas as pd
import numpy as np
from datetime import datetime
```

### Choose Subreddit topic 


```python
SUBREDDIT = "Python" #example: "CryptoCurrency"
```

### Setup App to connect to Reddit API

* To get data from reddit, you need to [create a reddit app](https://www.reddit.com/prefs/apps) which queries the reddit API.
* Select “script” as the type of app.
* Name your app and give it a description.
* Set-up the redirect uri to be http://localhost:8080.
* Once you click on “create app”, you will get a box showing you your "client_id" and "client_secrets".
* "user_agent" is the name of your app.

If you need help on setting up and getting your API credentials, please visit ---> [Get Reddit API Credentials](https://www.jcchouinard.com/get-reddit-api-credentials-with-praw/)


```python
MY_CLIENT_ID = 'EtAr0o-oKbVuEnPOFbrRqQ'
MY_CLIENT_SECRET = 'LmNpsZuFM-WXyZULAayVyNsOhMd_ug'
MY_USER_AGENT = 'script by u/naas'
```

## Model

#### Connect with the reddit API


```python
reddit = praw.Reddit(client_id=MY_CLIENT_ID, client_secret=MY_CLIENT_SECRET, user_agent=MY_USER_AGENT)
```

#### Get the subreddit level data


```python
posts =[]
for post in reddit.subreddit(SUBREDDIT).hot(limit=50):
    
    posts.append([post.title, post.score, post.id, post.subreddit, post.url, post.num_comments, post.selftext, post.created])
posts = pd.DataFrame(posts,columns=['title', 'score', 'id', 'subreddit', 'url', 'num_comments', 'body', 'created'])
```

* If you need more variables, check "vars()" function``
* Usage: 'vars(post)', you'll get post level variables 

#### Convert unix timestamp to interpretable date-time 


```python
posts['created']=pd.to_datetime(posts["created"],unit='s')
```

## Output


```python
posts.head()
```

Hint: Filter data using "created" variable for past 24 hours hot posts

## Additional Resources
- More info on the PRAW package used: https://praw.readthedocs.io/en/stable/
