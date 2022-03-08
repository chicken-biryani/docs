## Input

### Import libraries


```python
try:
    from pipedrive.client import Client
except:
    !pip install pipedrive-python-lib
    from pipedrive.client import Client
import pandas as pd
```

### Enter your api KEY

<b>Domain & API Key</b>
<p>Go to Account - Personal Preferences - API Key Tab - Click on Generate New Token</p>
<p>Add the key to line 2 in below cell</p>


```python
DOMAIN = "https://your_domain.pipedrive.com"
API_KEY = "your_api_key"
```

### Connect to Pipedrive


```python
client = Client(domain=DOMAIN)
client.set_api_token(API_KEY)
```

## Model

### Get all contacts


```python
response = client.persons.get_all_persons() #returns all the records present in CRM
dataKey = response.get("data", None) #the key with all records
userInfo = {} #empty dictionary for storing data in user object
users = [] #empty list to store multiple user objects
```


```python
for dataKeyItem in dataKey: #Iterate through each record
    phonelist = []
    emaillist = []
    for phone in dataKeyItem["phone"]:
        phonelist.append(phone["value"])

    for email in dataKeyItem["email"]:
        emaillist.append(email["value"])

    userInfo = {
        "FirstName": dataKeyItem["first_name"],
        "LastName": dataKeyItem["last_name"],
        "Phone": phonelist,
        "Email": emaillist,
        "Company": dataKeyItem["org_name"],
        "Job" : dataKeyItem["your_field_api_key"] #once you create a field you will find the resepect field api key in Accounts - Data Fields section
    }
    users.append(userInfo)
```

## Output

### Display result


```python
#use below line to adjust the display of columns and rows
pd.set_option("display.max_rows", None, "display.max_columns", 4)

#the below dataframe has sample data from Pipedrive CRM.
personsDF = pd.DataFrame(users)
print(personsDF)
```
