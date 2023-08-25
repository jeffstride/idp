# DataFrame
Here we will review common and useful actions with a DataFrame.  

First, it is helpful to understand how the Pandas [DataFrame documentation](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html) is structured. Painfully, it is not alphabetic! However, wonderfully, it is structured by activity.  

## Creating a DataFrame
**Creating from a list of dictionaries**  
Each dictionary is a row in the `DataFrame`. Each key in the dictionary is the column name with a value for the cell. 
```python
d1 = { 'City':'New York', 'Pop': 8.6, 'Rating': 3 }
d2 = { 'City':'Seattle', 'Pop': .8, 'Rating': 4 }
d3 = { 'City':'Los Angeles', 'Pop': 3.9, 'Rating': 3.5 }
d4 = { 'City':'Houston', 'Pop': 2.1, 'Rating': 4.1 }
my_list = [d1, d2, d2, d4]
pd = pd.DataFrame(my_list)

# The above creates a DataFrame with 4 rows, 3 columns.
# The column names are: 'City', 'Pop', and 'Rating'
```

**Creating from a list of lists**  
In this list of lists, each inner list is a row.  
```python
# This will have 5 rows, 3 columns, using default indexing.
# The column names are provided in the constructor below
data = [["New York", 8.6, 20],
        ["Chicago", 2.7, 20],
        ["Los Angeles", 3.9, 20],
        ["Philadelphia", 1.5, 20],
        ["Houston", 2.1, 20]]
 
# Give names to the columns when constructing
df = pd.DataFrame(data, columns=["City", "Population", "Year(2020)"])
```

**Creating by adding columns**  
Here, we create an empty `DataFrame` and then add on columns.  
```python
df = pd.DataFrame()
# add a column with the name 'seat_number'
df['seat_number'] = [ 1, 2, 3, 4 ]
# add a columns with the name 'student_id`
df['student_id'] = [ 1113, 1125, 1427, 1211]

# df has 4 rows, 2 columns, using default indexing.
```

**Creating from a dictionary**  
The keys are the column names, the values are lists of column values. 
```python
data = { "New York": [8.6, 20],
         "Chicago": [2.7, 20],
         "Los Angeles": [3.9, 20],
         "Philadelphia": [1.5, 20],
         "Houston": [2.1, 20]
       }
# creates 5 columns, 2 rows, default indexing
df = pd.DataFrame(data)
```

**Creating from a List**  
This is highly unusual, but possible.  
```python
# to get a dataframe with 1 column from a list of values
list = [ 2, 4, 6, 8 ]
df = pd.DataFrame(list)
# The above code creates 4 rows, 1 column, using default indexing. Column name is 0.
``` 

## Accessing/Changing Attributes & Values
* renaming columns  
* index and reindexing  
* 

## Handy Solutions to Common problems
* `pd.read_csv` [documenation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html?highlight=read_csv#pandas.read_csv)
> Example: `pd.read_csv(name, thousands=',', na_values='---', usecols=['c1', 'c2'], dtype={'c1':np.float64, 'c2':np.int32}, skiprows=3)`  
* setting NaN (`na_values='---'`), or the comma separator (via `thousands=','` for currency  
* changing all columns to be numeric: `df = df.apply(pd.to_numeric, errors='coerce')`  
* one can reduce time & memory of reading a file using the argument `usecols=['col1_name', 'col4_name']'`    
* `dtype` argument can set the types of each columns  
* `skiprows=5` can be used to skip the first 5 lines of a CSV file if there are some header lines to be ignored  

* df.sort_index()
* df.sample(n=30)
* df.reset_index(inplace=True)
* df.melt(value_name='value', var_name='source', ignore_index=False)