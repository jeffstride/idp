# DataFrame Slicing Methods

In this discussion, we will explore four methods for slicing data within a Pandas DataFrame:

1. `df[]`
2. `df.loc[]`
3. `df.iloc[]`
4. `df.take()`

Pandas is a powerful library that provides various ways to access and manipulate data. However, the abundance of methods can be overwhelming when choosing the most efficient one. This write-up aims to clarify the differences between these four slicing methods.

For additional information, refer to the [Pandas DataFrame Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).


## df[]
This is the _simplest_ and most _straightforward_ slicing method. df[] allows for both position and label-based slicing. You can use positional indices to select either single rows or a selection of multiple rows. You cannot just use a single row index argument. If you want a single row, you have to refer to a slice which only will include that one row.

We will use this dataframe for the following examples

```python
df = pd.DataFrame({'col1': [1, 2, 3, 4], 
                   'col2': [5, 6, 7, 8], 
                   'col3': [9, 10, 11, 12], 
                   'col4': [13, 14, 15, 16]})

```
Remember that the _first argument is inclusive, but the second is exclusive_

````{tab-set}

```{tab-item} Positional
In the first example, we use slicing to return a single row. You **cannot** just use a single row index argument. If you want a single row, you have to refer to a slice which only will include that one row.

Positional selection works even with a custom index, relying on the row's position rather than its label. You can also omit one or both parameters (df[1:], df[:3], and df[:]): a left-sided value includes rows including and beyond the specified position, right-sided value includes up to but not including the specified value, and a single colon includes all rows.

```python
'''
Single row:
'''
s1 = df[2:3]  # Returns a series containing values of the 3rd col [3, 7, 11, 15]

'''
Multiple rows:
'''
d1 = df[0:2]  # Returns a DataFrame containing two rows [1, 5, 9, 13] and [2, 6, 10, 14]
d2 = df[1:] # Returns a DataFrame containg three rows [2, 6, 10, 14], [3, 7, 11, 15], and [4, 8, 12, 16]
d3 = df[:2] # Returns a DataFrame containg two rows [1, 5, 9, 13] and [2, 6, 10, 14]
df4 = df[:] # Returns a DataFrame containg all columns
```

```{tab-item} Label-Based Selection
You can use the **labels** of columns or the custom indexes of rows to select data

Keep in mind that these are the labels assigned to the **custom index**. These labels are both **inclusive**. You cannot do this type of slicing (involving the colon) using column labels with this method. You would  instead use the `.loc` method. 

To select multiple columns with this method, we can use a **list** containing the labels of the column names. This is not a range of columns to be sliced. The function will only _return the columns contained in the list_. 

```python 
'''
Single column or named row
'''
s2 = df[['col1']] # returns a series containing the values of 'col1'

'''
Multiple rows (based on index label)
'''
df2 = df.set_index(['a', 'b', 'c', 'd']) # Returns dataframe with the indexes renamed to the rows a, b, and c
df3 = df2[a:c] # Returns a DataFrame containing the rows 'a', 'b', and 'c'

'''
Multiple Columns using a list
'''
d3 = df[['col1', 'col3']] # returns a dataframe containing the rows 'col1' and 'col3'
```

```{tab-item} Exceptions and Oddities
Some things to keep in mind when using this function:
* The inclusivity of breakpoints in slicing is **not consistent** in this function. When selecting based on position, it is similar to typical python: **inclusive** for the first argument, **exclusive** for the second. However, when selecting based on label, both terms are **inclusive**.
* A commonly used convention is to put a second set of  brackets around single term inputs, such as `d3 = df[['col1']]` in order to avoid ambiguity or confusion related to lists.
* The ambiguous nature of this function can lead to confusion. For example, if you were trying to access the row at the first positional index using `df[1]`, but you also had a custom integer index, confusion on what the 1 refers to could arise. Using more specific slicing methods such as `.iloc` or `.take` can help clear up this.
* `df[0]` will return an error. This is because it is expecting a column reference. When it is a slice, then the code filters down to the rows. To get the first row, call `df[0:1]`

````


## df.loc[]

df.loc is an **index/label** based slicer. It is designed to _decrease ambiguity_ in comparison to the simple `df[]` function. Throughout the examples, the following dataframe will be used: 

```python
df = pd.DataFrame({'col1': [2, 4, 6, 8],
                   'col2': [1, 3, 5, 7],
                   'col3': [10, 20, 30, 40],
                   'col4': [15, 25, 35, 45]})
```
`.loc` is structured in a way in which there are two _‘parameters’_ separated by commas. The first determines the _slice to take out of the rows_, and the second determines the _slice to take out of the columns_. These ‘parameters’ can either be **single values**, **lists**, or **slices**. We will review all of the argument types and categorize them based on return type.

````{tab-set}
```{tab-item} Single Value

This will return the value which is contained in **row 2** (by index, so effectively the 3rd row) of **column 1**, **3**. Since `.loc` is **label based**, the row parameter _does not have to be an integer_, as this example assumes a default index. If there was a custom index set, you could call `v1 = df.loc[‘c’, ‘col1’]`.

```python
v1 = df.loc[2, 'col1']  # Returns a single value from row 2 and column 'col1'
```

```{tab-item} Series 
Series based on row/column: Both of these lines will return a series of either a **row** or a **column**. Since the row parameter comes first, _you can forgo the column parameter if you were only looking for a single row_. However, if you are looking for a single column, _you need to include a `:`_, which just refers to all of the rows.

```python
''' 
Series based on a row:
'''
s1 = df.loc[1] # returns the second row as a series

'''
Series based on column:
'''
s2 = df.loc[:, 'col1']  # Returns 'col1' as a series (the first column)

'''
Series based on a section of a row:
'''
s3 = df.loc[1, ['col1', 'col3']] # returns a series of elements contained in row 1 of columns 1 and 3
s4 = df.loc[1, 'col1':'col3'] # returns a series of elements contained in row 1 of columns 1, 2, and 3

'''
Series based on a section of a column:
'''
s5 = df.loc[[1, 3], 'col1'] # returns a series of elements contained in rows 1 and 3 of column 1
s6 = df.loc[1:3, 'col1'] # returns a series of elements contained in rows 1, 2, and 3 of column 1
```

```{tab-item} DataFrame
This will be _very similar to the examples earlier_. However, **both** ‘parameters’ will be either a **slicer** or **list**. 

You can ‘mix and match’ **slicers** and **lists**. Remember this assumes a default index, but it will work fine if you utilize a custom index and use the index labels rather than numerical values. This applies to all examples. Slicing parameters are still **inclusive**.
```python
d1 = df.loc[[1, 3], ['col1', 'col3']] # returns a dataframe contained in either row 1 or 3 of column 1 and 3
d2 = df.loc[1: 3, 'col1': 'col3'] # returns a dataframe contained in either row 1, 2, or 3 of column 1, 2, and 3
d3 = df.loc[[1, 3], 'col1': 'col3'] # returns a dataframe contained in either row 1 or 3 of column 1, 2, and 3
```

```{tab-item} Exceptions and Oddities
* When indexing with integer based indices, _especially a custom index_, care is necessary in order to ensure you are referring to the right things (**positional** or **label** index?). Remember, if you are looking for positional indices, utilize `.iloc`.
* Assuming a default index, `df.loc[0]` will return the first row of the dataframe in a series.
* Square brackets are used simply because it is _consistent with the python convention of these brackets_, referring to slicing.

````



## Df.iloc[]

All numbers in the comments of the sample programs refer to the **index** positions of the rows/columns, meaning row 1 refers to the **second** row of the dataframe

`df.iloc` is an **integer** index based slicing function. It **only** takes integer numbers into its arguments. However, it is _very similar to the `.loc` function_, in that there are two arguments, one for the **row** and one for the **column**. The  difference is that while `.loc`'s arguments for its slicers are **inclusive**, the arguments for `.iloc`’s slicers are similar to base python. The first argument is **inclusive** while the second is **exclusive**. The positional nature makes `.iloc` very convenient when dealing with _large dataframes with confusing labels and custom indices_. Sometimes, locating a **value** or **slice** based on its **position** in the dataframe is more straightforward.

````{tab-set}
```{tab-item} Single Value

This will return the value which is contained in **row 2** of **column 1**, **7**. 

```python
v1 = df.iloc[2, 1] # returns the value in the 2x1 spot in the dataframe
```

```{tab-item} Series
```python
'''
Series based on a row
'''
s1 = df.iloc[1] # returns a series containing the row 1

'''
Series based on a column
'''
s2 = df.iloc[:, 2] # returns a series containing the column 2

'''
Series based on a section of a row
'''
s3 = df.iloc[1: [1, 3]] # retuns a series of the elements contained in row 1 of column 1 and 3
s4 = df.iloc[1:, 1:3] # retuns a series of the elements contained in row 1 of column 1, 2, and 3

'''
Series based on a section of a column:
'''
s5 = df.iloc[[1, 3], 1] # returns a series of the elements contained in rows 1 and 3 of column 1
s6 = df.iloc[1:3, 1] # returns a series of the elements contained in rows 1, 2, and 3 of column 1
```
```{tab-item} Dataframe
This will be very similar to the examples earlier. However, instead, both ‘parameters’ will have either a **slicer** or **list**. 

Like in `.loc`, you can ‘mix and match’ slicers and lists. 

```python
d1 = df.loc[[1, 3], [1, 3]] # returns a dataframe contained in either row 1 or 3 of column 1 and 3
d2 = df.loc[1: 3, 1: 3] # returns a dataframe contained in either row 1, 2, or 3 of column 1, 2, and 3
d3 = df.loc[[1, 3], 1: 3] # returns a dataframe contained in either row 1 or 3 of column 1, 2, and 3
```

```{tab-item} Exceptions and Oddities
* If you ever, for some reason, need to utilize a label based index using `.iloc`, you can use the function `df.columns.get_loc('your_column’)` in order to get the **positional** location of that **column**, and input that value into your `.iloc` function. However, this is obviously **not recommended**, as simply using `.loc` would be better.
* Assuming a _default index_, `df.iloc[0]` will return the first row of the dataframe in a series, just like `.loc`.
* If both ‘parameters’ of `.iloc` are single values, then it will return a **single value**. If one is a single value and the other is a slice or list, then it will return a **series**. If both are slices or lists, it will return a **dataframe**. This is applicable to `.loc`.

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
## Comparisions & Summary:
These 4 slicing methods are **all effective** if used right. The first step to determining the correct method is figuring out whether you are trying to slice **positionally** or based on **labels**, but there are other factors. This table will help you determine which to use.


| Method   | Purpose                        | Weaknesses                               | Return Types       | Inclusive vs. Exclusive | Arguments                             | Additional Considerations                             |
|----------|--------------------------------|------------------------------------------|--------------------|-------------------------|---------------------------------------|-------------------------------------------------------|
| `df[]`   | General-purpose tool            | Ambiguous syntax, confusing arguments    | Series, DataFrames | Inclusive:exclusive      | 1 parameter: Single values, lists, slices | Slices of row labels use `:`, for column labels, use lists |
| `df.loc` | Choose based on labels           | Does not access positional values        | Single values, Series, DataFrames | Inclusive | 2 parameters: Single values, lists, slices with mixing    | Slices of labels possible, e.g., `df.loc['col1':'col3']`  |
| `df.iloc`| Choose based on positional index | Cannot access labels                     | Single values, Series, DataFrames | Inclusive:exclusive      | 2 parameters: Single values, lists, slices with mixing    | None                                                     |
| `df.take`| Choose based on positional index | Can be unnecessarily confusing           | Series, DataFrames | None                    | 2 parameters: List of positions, axis parameter            | None                                                     |