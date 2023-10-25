# JSON

## Introduction

In this lesson, you'll continue investigating new formats for data. Specifically, you'll investigate one of the most popular data formats for the web: JSON files.

## Objectives
You will be able to:

* Describe features of the JSON format and the Python `json` module
* Use Python to load and parse JSON documents


## JSON Format

JSON stands for JavaScript Object Notation. Similar to CSV, JSON is a **plain text** data format. However the structure of JSON — based on the syntax of JavaScript — is more complex.

Here's a brief preview of a JSON file:  

<img src="images/json_preview.png" width="850">

As you can see, JSON is not a tabular format with one set of rows and one set of columns. JSON files are often nested in a hierarchical structure and will have data structures analogous to Python dictionaries and lists. Here's all of the built-in supported data types in JSON and their counterparts in Python: 

<img src="images/json_python_datatypes.png" width=500>


## `json` Module

In theory we could write our own custom code to split that string on `{`, `"`, `:` etc. and parse the contents of the file into the appropriate Python data structures.

Instead, we'll go ahead and use a pre-built Python module designed for this purpose. It will give us a powerful starting point for accessing and manipulating the data in JSON files. This module is called `json`.

You can find full documentation for this module [here](https://docs.python.org/3/library/json.html).

To use the `json` module, start by importing it:


```python
import json
```

### `json.load`

To load data from a JSON file, you first open the file using Python's built-in `open` function. Then you pass the file object to the `json.load` function, which returns a Python object representing the contents of the file.

In the cell below, we open the campaign finance JSON file previewed above:


```python
with open('nyc_2001_campaign_finance.json') as f:
    data = json.load(f)
print(type(data))
```

    <class 'dict'>


As you can see, this loaded the data as a dictionary. You can begin to investigate the contents of a JSON file by using our traditional Python methods.

### Parsing a JSON File

Since we have a dictionary, check its keys:


```python
data.keys()
```




    dict_keys(['meta', 'data'])



Investigate what data types are stored within the values associated with those keys:


```python
for v in data.values():
    print(type(v))
```

    <class 'dict'>
    <class 'list'>


#### Parsing Metadata

Then we can dig a level deeper. What are the keys of the nested dictionary?


```python
data['meta'].keys()
```




    dict_keys(['view'])



And what is the type of the value associated with that key?


```python
type(data['meta']['view'])
```




    dict



Again, what are the keys of that twice-nested dictionary?


```python
data['meta']['view'].keys()
```




    dict_keys(['id', 'name', 'attribution', 'averageRating', 'category', 'createdAt', 'description', 'displayType', 'downloadCount', 'hideFromCatalog', 'hideFromDataJson', 'indexUpdatedAt', 'newBackend', 'numberOfComments', 'oid', 'provenance', 'publicationAppendEnabled', 'publicationDate', 'publicationGroup', 'publicationStage', 'rowClass', 'rowsUpdatedAt', 'rowsUpdatedBy', 'tableId', 'totalTimesRated', 'viewCount', 'viewLastModified', 'viewType', 'columns', 'grants', 'metadata', 'owner', 'query', 'rights', 'tableAuthor', 'tags', 'flags'])



That is a lot of keys. One way we might try to view all of that information is using the `pandas` package to make a table.


```python
import pandas as pd
pd.set_option("max_colwidth", 120)
pd.DataFrame(
    data=data['meta']['view'].values(),
    index=data['meta']['view'].keys(),
    columns=["value"]
)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>id</th>
      <td>8dhd-zvi6</td>
    </tr>
    <tr>
      <th>name</th>
      <td>2001 Campaign Payments</td>
    </tr>
    <tr>
      <th>attribution</th>
      <td>Campaign Finance Board (CFB)</td>
    </tr>
    <tr>
      <th>averageRating</th>
      <td>0</td>
    </tr>
    <tr>
      <th>category</th>
      <td>City Government</td>
    </tr>
    <tr>
      <th>createdAt</th>
      <td>1315950830</td>
    </tr>
    <tr>
      <th>description</th>
      <td>A listing of public funds payments for candidates for City office during the 2001 election cycle</td>
    </tr>
    <tr>
      <th>displayType</th>
      <td>table</td>
    </tr>
    <tr>
      <th>downloadCount</th>
      <td>1470</td>
    </tr>
    <tr>
      <th>hideFromCatalog</th>
      <td>False</td>
    </tr>
    <tr>
      <th>hideFromDataJson</th>
      <td>False</td>
    </tr>
    <tr>
      <th>indexUpdatedAt</th>
      <td>1536596254</td>
    </tr>
    <tr>
      <th>newBackend</th>
      <td>False</td>
    </tr>
    <tr>
      <th>numberOfComments</th>
      <td>0</td>
    </tr>
    <tr>
      <th>oid</th>
      <td>4140996</td>
    </tr>
    <tr>
      <th>provenance</th>
      <td>official</td>
    </tr>
    <tr>
      <th>publicationAppendEnabled</th>
      <td>False</td>
    </tr>
    <tr>
      <th>publicationDate</th>
      <td>1371845179</td>
    </tr>
    <tr>
      <th>publicationGroup</th>
      <td>240370</td>
    </tr>
    <tr>
      <th>publicationStage</th>
      <td>published</td>
    </tr>
    <tr>
      <th>rowClass</th>
      <td></td>
    </tr>
    <tr>
      <th>rowsUpdatedAt</th>
      <td>1371845177</td>
    </tr>
    <tr>
      <th>rowsUpdatedBy</th>
      <td>5fuc-pqz2</td>
    </tr>
    <tr>
      <th>tableId</th>
      <td>932968</td>
    </tr>
    <tr>
      <th>totalTimesRated</th>
      <td>0</td>
    </tr>
    <tr>
      <th>viewCount</th>
      <td>233</td>
    </tr>
    <tr>
      <th>viewLastModified</th>
      <td>1536605717</td>
    </tr>
    <tr>
      <th>viewType</th>
      <td>tabular</td>
    </tr>
    <tr>
      <th>columns</th>
      <td>[{'id': -1, 'name': 'sid', 'dataTypeName': 'meta_data', 'fieldName': ':sid', 'position': 0, 'renderTypeName': 'meta_...</td>
    </tr>
    <tr>
      <th>grants</th>
      <td>[{'inherited': False, 'type': 'viewer', 'flags': ['public']}]</td>
    </tr>
    <tr>
      <th>metadata</th>
      <td>{'rdfSubject': '0', 'rdfClass': '', 'attachments': [{'filename': 'Data_Dictionary_Public_Funds_Payments_FINAL.xlsx',...</td>
    </tr>
    <tr>
      <th>owner</th>
      <td>{'id': '5fuc-pqz2', 'displayName': 'NYC OpenData', 'profileImageUrlLarge': '/api/users/5fuc-pqz2/profile_images/LARG...</td>
    </tr>
    <tr>
      <th>query</th>
      <td>{}</td>
    </tr>
    <tr>
      <th>rights</th>
      <td>[read]</td>
    </tr>
    <tr>
      <th>tableAuthor</th>
      <td>{'id': '5fuc-pqz2', 'displayName': 'NYC OpenData', 'profileImageUrlLarge': '/api/users/5fuc-pqz2/profile_images/LARG...</td>
    </tr>
    <tr>
      <th>tags</th>
      <td>[finance, campaign finance board, cfb, nyccfb, campaign finance, elections, contributions, politics, campaign, funding]</td>
    </tr>
    <tr>
      <th>flags</th>
      <td>[default, restorable, restorePossibleForType]</td>
    </tr>
  </tbody>
</table>
</div>



So, it looks like the information under the `meta` key is essentially all of the metadata about the dataset, including the category, attribution, tags, etc.

Now let's look at the main data.

#### Parsing Data

This time, let's look at the value associated with the `data` key. Recall that we previously identified that this had a `list` data type, so let's look at the length:


```python
len(data['data'])
```




    285



Now let's look at a couple different values:


```python
data['data'][0]
```




    [1,
     'E3E9CC9F-7443-43F6-94AF-B5A0F802DBA1',
     1,
     1315925633,
     '392904',
     1315925633,
     '392904',
     '{\n  "invalidCells" : {\n    "1519001" : "TOTALPAY",\n    "1518998" : "PRIMARYPAY",\n    "1519000" : "RUNOFFPAY",\n    "1518999" : "GENERALPAY",\n    "1518994" : "OFFICECD",\n    "1518996" : "OFFICEDIST",\n    "1518991" : "ELECTION"\n  }\n}',
     None,
     'CANDID',
     'CANDNAME',
     None,
     'OFFICEBORO',
     None,
     'CANCLASS',
     None,
     None,
     None,
     None]




```python
data['data'][1]
```




    [2,
     '9D257416-581A-4C42-85CC-B6EAD9DED97F',
     2,
     1315925633,
     '392904',
     1315925633,
     '392904',
     '{\n}',
     '2001',
     'B4',
     'Aboulafia, Sandy',
     '5',
     None,
     '44',
     'P',
     '45410.00',
     '0',
     '0',
     '45410.00']




```python
data['data'][2]
```




    [3,
     'B80D7891-93CF-49E8-86E8-182B618E68F2',
     3,
     1315925633,
     '392904',
     1315925633,
     '392904',
     '{\n}',
     '2001',
     '445',
     'Adams, Jackie R',
     '5',
     None,
     '7',
     'P',
     '11073.00',
     '0',
     '0',
     '11073.00']



This looks more like some kind of tabular data, where the first (`0`-th) row is some kind of header. Again, let's use pandas to make this into a more-readable table format:


```python
pd.DataFrame(data['data'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
      <th>16</th>
      <th>17</th>
      <th>18</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>E3E9CC9F-7443-43F6-94AF-B5A0F802DBA1</td>
      <td>1</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n  "invalidCells" : {\n    "1519001" : "TOTALPAY",\n    "1518998" : "PRIMARYPAY",\n    "1519000" : "RUNOFFPAY",\n ...</td>
      <td>None</td>
      <td>CANDID</td>
      <td>CANDNAME</td>
      <td>None</td>
      <td>OFFICEBORO</td>
      <td>None</td>
      <td>CANCLASS</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>9D257416-581A-4C42-85CC-B6EAD9DED97F</td>
      <td>2</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>B4</td>
      <td>Aboulafia, Sandy</td>
      <td>5</td>
      <td>None</td>
      <td>44</td>
      <td>P</td>
      <td>45410.00</td>
      <td>0</td>
      <td>0</td>
      <td>45410.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>B80D7891-93CF-49E8-86E8-182B618E68F2</td>
      <td>3</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>445</td>
      <td>Adams, Jackie R</td>
      <td>5</td>
      <td>None</td>
      <td>7</td>
      <td>P</td>
      <td>11073.00</td>
      <td>0</td>
      <td>0</td>
      <td>11073.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>BB012003-78F5-406D-8A87-7FF8A425EE3F</td>
      <td>4</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>HF</td>
      <td>Addabbo, Joseph P</td>
      <td>5</td>
      <td>None</td>
      <td>32</td>
      <td>P</td>
      <td>75350.00</td>
      <td>73970.00</td>
      <td>0</td>
      <td>149320.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>945825F9-2F5D-47C2-A16B-75B93E61E1AD</td>
      <td>5</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>IR</td>
      <td>Alamo-Estrada, Agustin</td>
      <td>5</td>
      <td>None</td>
      <td>14</td>
      <td>P</td>
      <td>25000.00</td>
      <td>2400.00</td>
      <td>0</td>
      <td>27400.00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>280</th>
      <td>281</td>
      <td>C50E6A4C-BDE9-4F12-97F4-95D467013540</td>
      <td>281</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>537</td>
      <td>Wilson, John H</td>
      <td>5</td>
      <td>None</td>
      <td>13</td>
      <td>P</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>281</th>
      <td>282</td>
      <td>04C6D19F-FF63-47B0-B26D-3B8F98B4C16B</td>
      <td>282</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>559</td>
      <td>Wooten, Donald T</td>
      <td>5</td>
      <td>None</td>
      <td>42</td>
      <td>P</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>282</th>
      <td>283</td>
      <td>A451E0E9-D382-4A97-AAD8-D7D382055F8D</td>
      <td>283</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>280</td>
      <td>Yassky, David</td>
      <td>5</td>
      <td>None</td>
      <td>33</td>
      <td>P</td>
      <td>75350.00</td>
      <td>75350.00</td>
      <td>0</td>
      <td>150700.00</td>
    </tr>
    <tr>
      <th>283</th>
      <td>284</td>
      <td>E84BCD0C-D6F4-450F-B55B-3199A265C781</td>
      <td>284</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>274</td>
      <td>Zapiti, Mike</td>
      <td>5</td>
      <td>None</td>
      <td>22</td>
      <td>P</td>
      <td>12172.00</td>
      <td>0</td>
      <td>0</td>
      <td>12172.00</td>
    </tr>
    <tr>
      <th>284</th>
      <td>285</td>
      <td>5BBC9676-2119-4FB5-9DAB-DE3F71B7681A</td>
      <td>285</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>1315925633</td>
      <td>392904</td>
      <td>{\n}</td>
      <td>2001</td>
      <td>442</td>
      <td>Zett, Lori M</td>
      <td>5</td>
      <td>None</td>
      <td>24</td>
      <td>P</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>285 rows × 19 columns</p>
</div>



We still have some work to do to understand what all of the columns are supposed to mean, but now we have a general sense of what the data looks like.

### Extracting a Value from a JSON File

Now, let's say that our task is:

> Extract the description of the dataset

We know from our initial exploration that this JSON file contains `meta` and `data`, and that `meta` has this kind of high-level information whereas `data` has the actual records relating to campaign finance.

Let's look at the keys of `meta` again:


```python
data['meta']['view'].keys()
```




    dict_keys(['id', 'name', 'attribution', 'averageRating', 'category', 'createdAt', 'description', 'displayType', 'downloadCount', 'hideFromCatalog', 'hideFromDataJson', 'indexUpdatedAt', 'newBackend', 'numberOfComments', 'oid', 'provenance', 'publicationAppendEnabled', 'publicationDate', 'publicationGroup', 'publicationStage', 'rowClass', 'rowsUpdatedAt', 'rowsUpdatedBy', 'tableId', 'totalTimesRated', 'viewCount', 'viewLastModified', 'viewType', 'columns', 'grants', 'metadata', 'owner', 'query', 'rights', 'tableAuthor', 'tags', 'flags'])



Ok, `description` is the 7th one. Let's pull the value associated with the `description` key:


```python
data['meta']['view']['description']
```




    'A listing of public funds payments for candidates for City office during the 2001 election cycle'



This is the general process you will use when extracting information from a JSON file.

## Summary
As you can see, there's a lot going on here with the deeply nested structure of JSON data files.
