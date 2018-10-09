
***This is the template for creating a readme lesson for Data Science. Please make sure to change the title to the appropriate topic, add an introduction, objectives (which should be taken from the lesson's outlined SWBATS), the lesson's content, and summary.***

> Note: If possible, structure the lesson's content according to the listed objectives. This helps to give a flow and framework for the material being presented to students.

# JSON and XML

## Introduction

In this lecture, we'll continue investigating new formats for datasets. Specifically, we'll investigate two of the most popular data formats for the web: JSON and XML including strenghts and weaknesses.

## Objectives
You will be able to:
* Effectively use the JSON module to load and parse JSON documents
* Read and access data stored in JSON and XML
* Compare  and contrast the JSON and XML as data interchange types


## XML

XML stands for 'Extensible Markup Language'. You may note the acronym's similarity to HTML; HyperText Markup Language. While HTML tells us how to display a page, XML is used to store the data and content of the page itself. Like HTML, xml uses tags to seperate and organize data in a hierarchical manner. Here's a brief preview of an XML file:  

<img src="xml_preview2.png" width=850>

## JSON

JSON stand for JavaScript Object Notation. It came after XML and was meant to streamline many data transportation issues at the time. It is now the common standard amongst data transfers on the web and has numerous parsing packages for numerous languages (including Python)! Here's a brief preview of the same file above now in JSON:  
<img src="json_preview.png" width=850>

## Loading XML and JSON Data
For both of these data formats, prebuilt modules exist that will give us a powerful starting point for accessing and manipulating the underlying data itself. As you'll see the newer version, JSON, is simpler and more flexible then its predecessor XML.

### The XML Module

You can check out the full details of the XML package here:  
https://docs.python.org/3.6/library/xml.html#  
but we'll be simply using a submodule, ElementTree:   
https://docs.python.org/3.6/library/xml.etree.elementtree.html#module-xml.etree.ElementTree  

Notice the nested structure of the XML file:  

<img src="xml_preview2.png" width=850>  

When parsing the data, we'll have to navigate through this hierarchical structure. This is the idea behind the `ElementTree` submodule that we'll be using. We'll start with a root note and then iterate over its children, each of which should have a tag (the name in <angle_brackets\>) and an associated attribute (the data between the two angle brackets <start\> data <stop\>).


```python
import xml.etree.ElementTree as ET
```

First we create 


```python
tree = ET.parse('nyc_2001_campaign_finance.xml')
root = tree.getroot()
```


```python
for child in root:
    print(child.tag, child.attrib)
```

    row {}



```python
import pandas as pd
```


```python
df = pd.read_html('nyc_2001_campaign_finance.xml')
df.head()

```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-3-37d170b78445> in <module>()
    ----> 1 df = pd.read_html('nyc_2001_campaign_finance.xml')
          2 df.head()


    ~/anaconda3/lib/python3.6/site-packages/pandas/io/html.py in read_html(io, match, flavor, header, index_col, skiprows, attrs, parse_dates, tupleize_cols, thousands, encoding, decimal, converters, na_values, keep_default_na, displayed_only)
        985                   decimal=decimal, converters=converters, na_values=na_values,
        986                   keep_default_na=keep_default_na,
    --> 987                   displayed_only=displayed_only)
    

    ~/anaconda3/lib/python3.6/site-packages/pandas/io/html.py in _parse(flavor, io, match, attrs, encoding, displayed_only, **kwargs)
        813             break
        814     else:
    --> 815         raise_with_traceback(retained)
        816 
        817     ret = []


    ~/anaconda3/lib/python3.6/site-packages/pandas/compat/__init__.py in raise_with_traceback(exc, traceback)
        401         if traceback == Ellipsis:
        402             _, _, traceback = sys.exc_info()
    --> 403         raise exc.with_traceback(traceback)
        404 else:
        405     # this version of raise is a syntax error in Python 3


    ValueError: No tables found



```python
## Objective 2 content
```

## Objective 3 Title


```python
## Objective 3 content
```

## Summary
Summary goes here
