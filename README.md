# 401k Tableau Dashboard using Google Sheets, BigQuery and Jupyter Notebook with Tableau Desktop connectors and APIs

Follow the steps laid out in the <a href='https://medium.com/@rydernguyen/401k-tableau-dashboard-using-google-sheets-bigquery-and-jupyter-notebook-with-tableau-desktop-65615a3408b2?source=friends_link&sk=3a4bca1fd00065f9b849e8f1d67721b6' target='_blank'>Medium story</a> & clone the repository.

# Useful user defined functions to work with Google Sheets
## Update rows by converting dataframe to list of list and use values_update method
def gsheets_update_rows(sheetname,df):
    lst = []
    for i in df.itertuples():
        lst.append(list(i))
    
    workbook.values_update(
        f'{sheetname}!A2',
        params={'valueInputOption': 'USER_ENTERED'},
        body={'values': lst})

## Update column names by using values_update method
def gsheets_update_names(sheetname,lst):
    workbook.values_update(
    f'{sheetname}!A1',
    params={'valueInputOption': 'USER_ENTERED'},
    body={'values': [lst]})
    
# Useful BigQuery python commands
## Write to a BigQuery table
pd.to_gbq('table_name',if_exists='param')
## Read from a BigQuery table using legacy syntax
pd.read_gbq(sql, dialect='legacy')
## Run queries on BigQuery directly from Jupyter 
query_job = bigquery_client.query("""[SQL CODE]""") <br>
results = query_job.result()
