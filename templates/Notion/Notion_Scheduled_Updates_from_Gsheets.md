<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Scheduled_Updates_from_Gsheets.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

This notebook does the following tasks: 
- Schedule the notebook to run every 15 minutes
- Connect with Gsheet and get all rows using the gsheet driver's get method
- Connect with NotionDB and get all pages using the Notion Databases driver's get method
- Compare the list of pages from notion db with the rows returned from gsheet and add non matching rows to a list
- Create new pages in Notion db for each row in the non matching list using the Notion Pages driver's create method
- For each created page, add the properties and values from gsheet and update in notion using the Notion Pages driver's update methods

**Tags:** #notion #Gsheets #productivity

Pre-requisite: 
1. Gsheets : Please share your Google Sheet with our service account
   For the driver to fetch the contents of your google sheet, you need to share it with the service account linked with Naas. 🔗 naas-share@naas-gsheets.iam.gserviceaccount.com 
2. Notion : Create a notion integration and use the secret key to share the database. <a href = 'https://docs.naas.ai/Notion-7435020d01a549a9a0060c47ea808fd4'> Refer the documentation here</a>

**Author:** [Pooja Srivastava](https://www.linkedin.com/in/pooja-srivastava-bb037649/)

## Input

### Import library


```python
import pandas as pd
import naas
from naas_drivers import notion
from naas_drivers import gsheet
```

### Scheduler


```python
#Schedule the notebook to run every 15 minutes
naas.scheduler.add(cron="*/15 * * * *")
```

### Setup Notion


```python
# Enter Notion Token API and Database URL
notion_token = "****"
notion_database_url = "https://www.notion.so/YOURDB"

#Unique column name for notion
col_unique_notion = 'Name'
```

### Setup Gsheet


```python
# Enter spreadsheet_id and sheet name
spreadsheet_id = "****"
sheet_name = "YOUR_SHEET"

#Unique column# for gsheets
col_unique_gsheet = 'Name'
```

## Model

### Get Gsheet and Notion data


```python
#Connect with Gsheet and get all data in a dataframe
gsheet.connect(spreadsheet_id)
df_gsheet = gsheet.get(sheet_name=sheet_name)
```


```python
#Connect with Notion db and get all pages in a dataframe
database = notion.connect(notion_token).database.get(notion_database_url)
df_notion = database.df()
```

### Compare Gsheet and Notion data


```python
#Iterate through all rows in Gsheet and find match in Notion db
#If no match is found then add data to df_difference dataframe

df_difference = pd.DataFrame()
for index,row in df_gsheet.iterrows():
    x = row[col_unique_gsheet]
    if not (x == df_notion[col_unique_notion]).any():
        df_difference = df_difference.append(df_gsheet.loc[index])
```

## Output

### Create a new page in Notion if it does not match with Gsheet


```python
#Create a new page in notion db for each row in df_difference dataframe
if(df_difference.empty == False):    
    for index, row in df_difference.iterrows():
        page = notion.connect(notion_token).page.create(database_id=notion_database_url, title=row[col_unique_gsheet])
        #Add all properties here and map with respective column in row
        page.select('Type', row['Type'])
        page.select('Status', row['Status'])
        page.rich_text('Summary', row['Summary'])
        page.update()
    print("The gsheets rows synced successfuly to Notion DB")
else:     
    print("No new rows in Gsheet to sync to Notion DB")
    
```
