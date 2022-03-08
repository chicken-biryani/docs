<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Search/Google_Search_Perform_search.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #googlesearch

## Input

### Install packages


```python
!pip install google
```

### Import library


```python
from googlesearch import search
```

### Variables


```python
query = "telsa"
```

## Model

Parameters : 

- query: This is the text that you want to search for.

- tld: This refers to the top level domain value like co.in or com which will specify which Google website we want to use.

- lang: This parameter stands for language.

- num: This is used to specify the number of results we want.

- start: This is to specify from where to start the results. We should keep it 0 to begin from the very start.

- stop: The last result to retrieve. Use None to keep searching forever.

- pause: This parameter is used to specify the number of seconds to pause between consecutive HTTP requests because if we hit too many requests, Google can block our IP address.

The above function will return a python generator (iterator) which has the search result URLs.

Source : https://www.studytonight.com/post/how-to-perform-google-search-using-python#

## Output

### Display the result of the search


```python
for i in search(query, tld="co.in", num=30, stop=10, pause=2):
    print(i)
```
