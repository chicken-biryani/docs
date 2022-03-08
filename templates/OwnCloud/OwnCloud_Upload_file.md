<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OwnCloud/OwnCloud_Upload_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #owncloud #cloud #storage

## Input

### Install packages


```python
!pip install pyocclient
```

### Import library


```python
import naas
import owncloud
```

## Model

### Connect to your ownCloud


```python
oc = owncloud.Client('https://cloud.damken.com')

oc.login('YOURNAME', 'YOURPASS')
```

### Create a folder


```python
oc.mkdir('testdir')
```

### Upload this file to your ownCloud


```python
oc.put_file('testdir/upload_to_owncloud.ipynb', 'upload_to_owncloud.ipynb')
```

### Get sharable link to the file


```python
link_info = oc.share_file_with_link('testdir/upload_to_owncloud.ipynb')
```

## Output

### Display result


```python
print ("Here is your link: " + link_info.get_link())
```


```python

```
