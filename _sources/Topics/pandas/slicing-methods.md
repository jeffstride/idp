# DataFrame Indexing Methods

We will explore four methods that index data within a Pandas DataFrame. The abundance of approaches can be overwhelming and this write-up aims provide clarity. For additional information, refer to the [Pandas DataFrame Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).  

|API|Index/Position|Comment|  
|---|-----|-------|  
|`df[]`|rows by position, columns by name|One argument only|  
|`df.loc[]`|by index | `[inclusive : inclusive]` |  
|`df.iloc[]`|by position| Columns by position, too|  
|`df.take()`|by position| `axis=0` take rows</br>`axis=1` take columns| 

Except for `loc` the API are `[inclusive : exclusive]`.  

## Argument Types
|Type|Example|Notes|
|----|-------:|-----|
|Number| `df.iloc[3]`</br>`df.loc[3]`|Describes the position, or,</br>index|   
|Numerical Slice| `df[0:3]`</br>`df.loc[1:3]` |A slice using numbers (positional)</br> (index)|  
|Numerical List| `df.take([0, 3])`</br>`df.loc[[1,3]]`|List of numbers (positional)</br> (index)|
|Mask|`df[[True, False, True]]`|Any iterable of True/False values|
|String|`df['A']`|A column name (or index value)| 
|String Slice|`df.loc[:, 'C':'words']`|Represents a range of columns|  
|String List|`df[['C','D','words']]`|A list of column names|

## API Details
````{tab-set}

```{tab-item} df
* `df[]` takes a single argument only.  
* Slices are `[ Inclusive : Exclusive ]`.   
* The most common usage is to get a `Series` (column) from the `DataFrame` via `df['col_name']`.  
* One can add a column to a `DataFrame` with `df['new_column'] = list_of_values`  

It is important to note here that when a numerical slice is used, the values represent positions, not the index. When string values are used, the values represent column names.   

**Valid Argument Types:**  
* **Numerical Slice:** represents the Row **Positions**  
* **Mask:** represents which Rows to keep  
* **String:** column name  
* **String List:** list of column names  

**Invalid Argument Types:**  
* **Numerical List:** You cannot use `df[[0, 5, 8]]` to access a list of rows.  
* **String Slice:** You cannot use `df['first':'exclude_me']` to access a slice of columns. Instead, you must use a list of strings.  

**Examples:**  
|Valid|Results|Invalid|Note|  
|-----|----|-------|----|  
|`df[0:1]`|DataFrame</br>All columns, 1 row|`df[0]`|single number **NOT** allowed|  
|`df[1:3]`|DataFrame</br>All columns, 2 rows|`df[[0, 3]]`| List must be column names|  
|`df[2:10]`|DataFrame</br>All columns. Many rows| |All rows at those positions. If the slice is completely out of bounds, an empty DataFrame is returned.|
|`df[[True, False]]` |DataFrame</br>All columns, rows where mask==True| |Length of mask must be len(df)|  
|`df[['C', 'D']]`|DataFrame</br>All rows with columns 'C' and 'D'|  | The columns are ordered as they appear in the list.|  
|`df[['C']]`|DataFrame</br>All rows, one column 'C'|  |A list of just 1 still results in a DataFrame. |  
|`df['C']`|Series. Column 'C'|`df['C':'words']`|Column slices **NOT** allowed. |  
 
Note that, except for the last example, all valid API return a DataFrame.  
``` 
```{tab-item} df.loc
* `df.loc[rows, cols]` takes one or two arguments.  
* To get all rows, use an 'empty' slice: `df.loc[ : , 'Name']`  
* Each argument can describe multiple values or a single value.   
* The type returned depends on the argument types (vectors vs scalar <a href="#footnotes">[1][2]</a>).  
    * If both arguments are vectors, a `DataFrame` is returned.   
    * If exactly one argument is a vector, then a `Series` is returned.   
    * If both arguments are scalar, then the contents of the single cell is returned.    
* Slices are `[ Inclusive : Inclusive ]`.  
* One can set a value. `df.loc[1, 'Name'] = 5` will set the `DataFrame`'s value to 5 at index 1 and row 'Name'.  

The first argument describes the indices of the rows desired.   
The second argument describes the column names desired.  

**Valid Argument Types:**  
* **Slice**: For rows, the slice must match the index type. For columns, the slice indicates the names of the columns to include and every column between.   
* **Mask**: Represents which rows/cols to keep. Mask is an iterable of True/False values (such as a `Series` or a list)  
* **List**: A list of indices or column names to include.   


Examples: 
|Valid|Note|  
|-----|----| 
|`df.loc[0:3]`|Rows with indices 0 & 3, and everything in between|
|`df.loc[11:5]`|Since indices don't need to be sorted, this will have index 11 as the first row and index 5 as the last row, and all rows that are positioned between them.|  
|`df.loc[mask1, mask2]`|Gets all the rows where mask1 is True, and all the columns where mask2 is True. len(mask1) == count of rows. len(mask2) == count of columns.|  
|'df.loc[ : , df.columns != 'Bad']`|Gets all the rows and all the columns except for 'Bad'. df.columns is a list of column names. The result of comparing the list to 'Bad' is a list of True/False values... a mask|  
|`df.loc[ [0, 8, 11], ['One', 'Three'] ]`| Each list represents which row/column to keep. The result has the same order as that provided in the list.|  

  
```{admonition} Why Inclusive?
:class: note 
The reason this API is inclusive is because one will often want to get a set of columns that one knows about. It is better to say:  
> "I want all the columns starting with 'One' and ending with 'Last'"   

than it is to say:
> "I want all the columns starting with 'One' and goes until the column after the 'Last' column that I want named... gosh, what is the name of the column that I don't want?  

The same can be true for rows when the index is not sorted.  
```

```{tab-item} df.iloc
Under constructions.  
* `df.iloc[rows, cols]` takes 1 or 2 arguments.  
* Arguments are primarily **integers** that represent **position**, but can also be a boolean mask.  
* Arguments can also be a lambda for with the argument of the lambda is the calling object, either a DataFrame or Series.  
* There are no string arguments.  

**Valid Argument Types:**  
* **integer** that represents the position of the row or column.  
* **Numerical Slice** that represents the positions of the rows or columns.  
* **Numerical List** that represents the positions of the rows or columns.   

```
```{tab-item} df.take
under construction
```
````

## Examples

````{tab-set}

```{tab-item} Common
df = ![Default Index](../../_static/df_slice_1.png)  
|Result|API|
|------|---|
|![Default Index](../../_static/df_slice_1a.png)|`df[0:1]`</br>`df.loc[0:0]`</br>`df.iloc[0:1]`</br>`df.take([0])`|  
|![Default Index](../../_static/df_slice_1b.png)|`df[1:3]`</br>`df.loc[1:2]`</br>`df.iloc[1:3]`</br>`df.take([1,2])`|
|![Default Index](../../_static/df_slice_1c.png)|`mask=[True,False,True,False]`</br>`df[mask]`</br>`df.loc[mask]`</br>`df.loc[[0, 2]]`</br>`df.iloc[mask]`</br>`df.iloc[[0, 2]]`</br>`df.take([0, 2])`</br>`df[[0, 2]]` <span style="background-color: yellow">FAILS!!</span>|
|![Default Index](../../_static/df_slice_1d.png)|`mask=[False,False,True,True,True,False]`</br>`df[['C', 'D', 'words']]`</br>`df.loc[:, mask]`</br>`df.loc[:, 'C':'words']`</br>`df.loc[:, ['C', 'D', 'words']]`</br>`df.iloc[:, mask]`</br>`df.iloc[:, [0, 2]]`</br>`df.take([2, 3, 4], axis=1)`</br>`df['C':'words']` <span style="background-color: yellow">FAILS!!</span>| 
|![Default Index](../../_static/df_slice_1e.png)|`df.loc[:, mask]`</br>`df.loc[:, 'A':'A']`</br>`df.loc[:, ['A']]`</br>`df.iloc[:, 0:1]`</br>`df.iloc[:, mask]`</br>`df.iloc[:, [0]]`</br>`df.take([0], axis=1)`</br>`df.loc[:, 'A']` <span style="background-color: yellow">WRONG!! Returns Series</span>| 
|Series: Column 'A'</br><pre>0    1</br>1    2</br>2    3</br>3    4</br>Name: A, dtype: int64</pre>|`df['A']`</br>`df.loc[:, 'A']`</br>`df.loc[:, mask]`</br>`df.iloc[:, 0]`</br>`df.iloc[:, mask]`|  
|Series: 2nd Row with index 1</br><pre>A          2</br>B          6</br>C         10</br>D         14</br>words    cat</br>jumpy      2</br>Name: 1, dtype: object0</pre>|`df.loc[1, :]`</br>`df.iloc[1, :]`|  
|Scalar Value:</br>`7`|`df.loc[2, 'B']`</br>`df.iloc[2, 1]`|
```
```{tab-item} Unsorted Index
|DataFrame|Result|API|
|---------|------|---|
|![Default Index](../../_static/df_slice_2.png)|![Default Index](../../_static/df_slice_2a.png)|`df[0:1]`</br>`df.loc[9:9]`</br>`df.iloc[0:1]`</br>`df.take([0])`|  
|  |![Default Index](../../_static/df_slice_2b.png)|`df[1:3]`</br>`df.loc[2:11]`</br>`df.iloc[1:3]`</br>`df.take([1,2])`|
```
```{tab-item} String Index
|DataFrame|Result|API|
|---------|------|---|
|![Default Index](../../_static/df_slice_3.png)|![Default Index](../../_static/df_slice_3a.png)|`df[0:1]`</br>`df.loc['ax']`</br>`df.iloc[0:1]`</br>`df.take([0])`|  
|  |![Default Index](../../_static/df_slice_3b.png)|`df[1:3]`</br>`df.loc['cat':'dog']`</br>`df.iloc[1:3]`</br>`df.take([1,2])`|
```
````

## df.take()

`df.take()` is primarily a **positional** based indexer/slicer. It will return the **columns** or **rows** in the position specified by the inputs, which will either be a **single value**, **list**, or **slice**. It has another parameter, `axis`, which is set to _0 by default_. The default parameter refers to the **index/rows**, meaning we are selecting rows to extract. If you set `axis` to 1, then it will select **columns**.

````{tab-set}
```{tab-item} Series
Since `df.take()` is **positional** based, you **cannot** input labels. They must be integers. Additionally, it _ignores whatever custom index you may have applied_, even if it is an integer index. It will use the _underlying positional index_ to collect the data. Remember, you **need** to include the square brackets, because the function takes only lists.

```python
'''
Series based on a row
'''
s1 = df.take([1]) # returns a series representing row 1

'''
Series based on a column
'''
s2 = df.take([1], axis=1) # returns a series representing column 1
```

```{tab-item} Dataframe

```python
d1 = df.take([1, 3, 0]) # returns a dataframe containing rows 1, 3, and 0

# Setting `axis` to 1 indicates whether the list of indexes is for **rows** or **columns**
d2 = df.take([1, 3, 0], axis=1) # returns a dataframe containing columns 1, 3, and 0
```

```{tab-item} Exceptions and Oddities
* Make sure to look out for `IndexError` exceptions, which will arise if you _input a number that is not in the index_. This means you **can’t** use `len(df)` as a parameter in order to get the _last row of the dataframe_.
* You can use **negative indices**. This works similarly to slicing in lists in base python, where _the -1 index corresponds to the last value of the set_.
* `df.take([0])` returns the first (0 position) row.

````

## Footnotes
[1] **Vector** is intended to a data structure that can hold multiple values such as a list, slice, or array, even when these structures contain a single value.    
[2] **Scalar** is intended to mean a single value such as a string or integer. It is NOT a list, slice, or array. 