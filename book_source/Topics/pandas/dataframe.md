# DataFrame
Here we will review common and useful actions with a DataFrame.  

First, it is helpful to understand how the Pandas [DataFrame documentation](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html) is structured. Painfully, it is not alphabetic! However, wonderfully, it is structured by activity.  

## Creating a DataFrame
* Constructor  

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