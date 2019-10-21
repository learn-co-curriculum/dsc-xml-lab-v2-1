
# XML - Lab

## Introduction

In this lab, you'll practice navigating XML data structures.

## Objectives
You will be able to:
* Use the XML module to load and parse XML data


## XML


```python
import xml.etree.ElementTree as ET
```

### Create an XML tree and retrieve the root tag.


```python
#Your code here
tree = ET.parse('nyc_2001_campaign_finance.xml')
root = tree.getroot()
```

### How many direct descendents does the root tag have?


```python
#Answer: 1
count = 0 
for child in root:
    count += 1
print(count)
```

    1


### How many different types of tags are there within the entire XML file?


```python
# Your code here
tags = []
for element in root.iter():
    tags.append(element.tag)
print(len(set(tags)))
```

    13


### Create a DataFrame listing the number of each type of tag. 
Sort the DataFrame in descending order by the tag count. The first entry should demonstrate there are 286 row tags in the XML file.   
(Your DataFrame will be a single column, so could also be thought of as a Series.)


```python
import pandas as pd
```


```python
#Your code here
tags = {}
for element in root.iter():
    tags[element.tag] = tags.get(element.tag, 0) + 1
df = pd.DataFrame.from_dict(tags, orient='index')
df.columns = ['count']
df = df.sort_values(by='count', ascending=False)
df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>row</th>
      <td>286</td>
    </tr>
    <tr>
      <th>candid</th>
      <td>285</td>
    </tr>
    <tr>
      <th>candname</th>
      <td>285</td>
    </tr>
    <tr>
      <th>canclass</th>
      <td>285</td>
    </tr>
    <tr>
      <th>election</th>
      <td>284</td>
    </tr>
  </tbody>
</table>
</div>



## Summary

Congratulations! You've started exploring XML data structures used for the web and got to practice data munging and exploring!
