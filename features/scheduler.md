---
description: 'Make your notebook run, even when you sleep.'
---

# ⏰ Scheduler

{% embed url="https://www.youtube.com/watch?v=ONiILHFItzs&t=48s" %}

We use CRON tasks to schedule notebooks, find the syntax you need to on: [https://crontab.guru/](https://crontab.guru/)

{% hint style="info" %}
A job shouldn't last more than one hour, split your work :\)
{% endhint %}

## Add

Send in production this notebook and run it, every day at 9:00 :

```python
naas.scheduler.add(cron="0 9 * * *")
```

{% hint style="warning" %}
Note : the previous synthax is now deprecated. 

```python
naas.scheduler.add(recurrence="0 9 * * *")
```
{% endhint %}

### Other Notebook

You can also give a path to the function and that will deploy this file instead of the current one.





```python
naas.scheduler.add(path="path/to/my/super/notebook.ipynb", recurrence="0 9 * * *")
```

### Parameters

`notif_down` : Receive an email when the notebook run fails.

`notif_up` : Receive an email when the notebook runs well.

`next_url` : Url to call when the notebook success, it can be any service even if an Notebook API

```python
params = {"notif_down": "bob@naas.ai", "notif_up": "georges@naas.ai"}

naas.scheduler.add(recurrence="0 9 * * *", params=params)
```

### Debug

```python
naas.scheduler.add(recurrence="0 9 * * *", debug=True)
```

## List 

You can list all version of a file pushed into the production folder:

### Current file

```python
naas.scheduler.list()
```

### Other file 

```python
naas.scheduler.list(path="path/to/my/super/notebook.ipynb")
```

## Get 

You can get a version of a file pushed into the production:

### Get the last one

```python
naas.scheduler.get()
```

### With a file path

```python
naas.scheduler.get(path="path/to/my/super/notebook.ipynb")
```

### With history id

```python
naas.scheduler.get(histo="20201008101221879662")
```

### Combined

```python
naas.scheduler.get(path="path/to/my/super/notebook.ipynb", histo="20201008101221879662")
```

## Clear

You can clear the previous version of a file pushed into the production:

### One

```python
naas.scheduler.clear(histo="20201008101221879662")
```

### Other Notebook

```python
naas.scheduler.clear(path="path/to/my/super/notebook.ipynb", histo="20201008101221879662")
```

### All

```python
naas.scheduler.clear()
```

### All for filepath

```python
naas.scheduler.clear(path="path/to/my/super/notebook.ipynb")
```

## Get output

You can get the output of the production file:

### Get the last one

```python
naas.scheduler.get_output()
```

### With a file path

```python
naas.scheduler.get_output(path="path/to/my/super/notebook.ipynb")
```

## Clear output

You can clear the previous output of a file pushed into the production:

### One

```python
naas.scheduler.clear_output()
```

### Other Notebook

```python
naas.scheduler.clear_output(path="path/to/my/super/notebook.ipynb")
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path: 

### Current

```python
naas.scheduler.delete()
```

### Other file

```python
naas.scheduler.delete(path="path/to/my/super/notebook.ipynb")
```

### Debug

```python
naas.scheduler.delete(debug=True)
```

## List Schedulers

You don't remember how many Scheduled notebooks you have?

### Simple

```python
naas.scheduler.currents()
```

### Raw result 

```python
naas.scheduler.currents(raw=True)
```


