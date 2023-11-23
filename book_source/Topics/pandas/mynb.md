# Useful API


### Both DataFrame and Series
|API|Comments|  
|---|--------|
|`describe()`|Outputs useful statistical information about the data|  
|`unique()`|Returns only unique rows/values in the data. TODO: validate on DF |  
|`drop_duplicates()`|Removes all duplicate rows/values in the data|  
|`isnull()`|Replaces all values that are NaN with True. False otherwise|  
|`notnull()`|Replaces all values that are NaN with False. Tue otherwise|  
|`dropna()`|Removes all rows that have any NaN value|  
|`fillna(value)`|Fills all values that are NaN with the value given|  
|`apply(fn)`|Applies the function to all values (TODO: Validate works on DF) |  
|`index`|The name of the index|  
|`nunique()`|Gets a count of the unique rows/values in the data|  
|`copy()`|Makes a copy of the DF. Should be used judiciously|  
|`take(iterable)`|Returns the rows found in the iterable TODO: Series?| 
|`concat()`|Not the same as 'append'. TODO: Series. Describe better.|  

**Question**: How to append multiple columns to a DataFrame?  


### DataFrame only
|API|Comments|  
|---|--------|
|`columns`|An iterable of all the column names|  
|`loc[rows, cols]`|Returns a value, Series or DataFrame filtered as specified|  
|`set_index('col')`|Sets the index of the DF to 'col'|  
|`reset_index()`|Restores the index of the DF to the default ordinal values|  
|`sort_index()`|Sorts the DF by the index. TODO: is this Series too?|  
|`sort_values(by='col')`|Sorts the DF by the values in column, ascending|  
|`nlargest(count, 'col')`|Returns a DataFrame, sorted by 'col', descending, of size count|  
|`nsmallest(count, 'col')`|Returns a DataFrame, sorted by 'col', ascending, of size count|  
|`groupby('groupcol')['value_col'].xxx()`|Returns a Series where the index are the values in 'groupcol', the values are computed from the column 'value_col' and the computation is 'xxx' which is one of many mathematical functions.|  
|`rename(dict)`|Uses the dictionary to rename the columns|  

### Available on DataFrame, Series and Groupby Result
|Math API|Comments|  
|--------|--------|  
|`min()`|Finds the minimum value|  
|`max()`|Finds the maximum value|  
|`mean()`|Finds the average/mean value|  
|`idxmin()`|Finds the index of the minimum value|  
|`idxmax()`|Finds the index of the maximum value|  

### Math methods
`add`, `sub`, `mul`, `div`, `mod`, `pow`  
```python
# do element-by-element math
result = df1.add(df2)
```

### Series only
|API|Comments|  
|---|--------|
|`nlargest(count)`|Returns a sorted Series, descending, of size count|  
|`nsmallest(count)`|Returns a sorted Series, ascending, of size count|  
|`isin(iterable)`|Returns a boolean Series, True if the value is found in the iterable|  

### File Related
* setting None into a DataFrame may go to np.NaN if column is numeric
* read_csv and parse_dates to get TimeSeries
* Reading Unicode files: with ('filename.txt, encoding='utf-8')
    * This is helpful when copying content from Google Docs or Word
|API|Comments|  
|---|--------|  
|`to_csv()`|Saves the DF as a CSV file. Handy during Final Project preprocessing step.|  
|`read_csv()`| TODO: More details on date formatting|  

* Series
    * `s.isin(list)` # a mask
    * (most of the DataFrame methods): 
* Iterating through a DataFrame  
* `df[ X ]` where X can be:  
    * 'column_name' - returns a Series  
    * Boolean Series - acts as a mask and returns a DataFrame  
    * `['col1', 'col2']` - using a list of column names returns a DataFrame  
    * Does a slice work? `['col1':'col2']`   
* `df.loc[ row, col ]` where row/col can be:  
    * index value (or column name)  
    * list of values  
    * slice of values  
    * Will a boolean mask work?  
* API on DataFrame  
    * `describe`  
    * `unique`, 
    * `index`, `columns`  
    * `copy`  
    * `to_csv`:  
    * Math: `add`, `sub`, `mul`, `div`, `mod`, `pow` : elementwise math of two dataframes  
    * `min`, `max`, `idxmin`, `idxmax` : returns a Series with information for each column    
    * `nunique`:  
    * `dropna`:  
    * `isnull` and `notnull`  
    * `nlargest(count, 'col')`  
    * `nsmallest(count, 'col')`  
    * `groupby`  
    * `sort_values('col')`  
    * `concat([df1, df2])` vs `append` which is deprecated.  
    * `sort_index`  
    * `set_index` and `reset_index`  
    * `rename(dict)` where dict is `{ 'orig': 'New_name' }`  
    * `apply` 
    * `plot`  
    * `boxplot`  
    * 
* `df = df.apply(pd.to_numeric, errors='coerce')` : forces values to be numeric




```python
import pandas as pd

# do details and examples of
# unique vs drop_duplicates (on df and series)
# groupby()
# .loc[]

df
```

# Standard Cleaning DF
* read_csv  
* dropna or fillna  
* keep select columns with `df = df[ col_list ]`  
* perhaps coerce column dtypes: `df = df.apply(pd.to_numeric, errors='coerce')`  
* rename columns to something short and readable: `df = df.rename(dict)`  


# read_csv
In Pandas version 2.0, there is a date_format.
But, the version NCHS has installed is older. (v 1.3)
To see the version, you can print(pd._version)

Older versions support data_parser=fun. Where it is best to use pd.to_datetime(date_string, format=’%Y-%m-%d’).
So this will parse MM-YYYY-DD, such as 03-2023-31: 
df = pd.read_csv('data.csv', index_col='date', parse_dates=True, date_parser=lambda s: pd.to_datetime(s, format='%m-%Y-%d'))
When parse_dates == True, then we will parse the index.

parse_dates: bool, list of Hashable, list of lists or dict of {Hashablelist}, default False
The behavior is as follows:
•	bool. If True -> try parsing the index.
•	list of int or names. e.g. If [1, 2, 3] -> try parsing columns 1, 2, 3 each as a separate date column.
•	list of list. e.g. If [[1, 3]] -> combine columns 1 and 3 and parse as a single date column.
•	dict, e.g. {'foo' : [1, 3]} -> parse columns 1, 3 as date and call result ‘foo’
If a column or index cannot be represented as an array of datetime, say because of an unparsable value or a mixture of timezones, the column or index will be returned unaltered as an object data type. For non-standard datetime parsing, use to_datetime() after read_csv().


# more than one way to do this
```python
for n in df2: # iterates through the columns
    print(n)
```

# iterates through the tuples (col_name, col_series)
```python
for col_name, col_series in df2.iteritems():
    print(col_name)
    print(col_series)
```

# identical to the above
```python
for col_name, col_series in df2.items():
    print(col_name)
    print(col_series)
```

# dataframe Plot
|  x : label or position, default None
 |      Only used if data is a DataFrame.
 |  y : label, position or list of label, positions, default None
 |      Allows plotting of one column versus another. Only used if data is a
 |      DataFrame.
 |  kind : str
 |      The kind of plot to produce:
 |  
 |      - 'line' : line plot (default)
 |      - 'bar' : vertical bar plot
 |      - 'barh' : horizontal bar plot
 |      - 'hist' : histogram
 |      - 'box' : boxplot
 |      - 'kde' : Kernel Density Estimation plot
 |      - 'density' : same as 'kde'
 |      - 'area' : area plot
 |      - 'pie' : pie plot
 |      - 'scatter' : scatter plot (DataFrame only)
 |      - 'hexbin' : hexbin plot (DataFrame only)
 |  ax : matplotlib axes object, default None
 |      An axes of the current figure.
 |  subplots : bool, default False
 |      Make separate subplots for each column.


```python
import pandas as pd
df = pd.DataFrame()
help(df.plot)
```


```python

```
