# Bar Charts
Bar charts are good when:  
* The x-axis is categorical and does not have a natural order (e.g. Country names).  
* There are very few points to show (e.g. 4 or less)  
* There isn't an obvious relationship to the prior value on the x-axis (because they are categorical).  
* You want to use color to emphasize the height or illustrate a relationship to another value.   
  
Bar charts are NOT good when:  
* You're attempting to show a correlation. (e.g. more X means more Y)  
* There are a lot of points to show (e.g. 15 or more)

## Positive vs Negative Bars
In this example bar chart you'll see that the positive values have green bars
while the negative values have red bars. The example below only uses two colors
to emphasize the direction of change. We use a bar chart here depsite there being
many different years to plot because the green/red colors emphasize the relative changes nicely.


````{tab-set}
```{tab-item} Image
![bar chart](../_static/annual_change.png)
```
```{tab-item} Code
```python
def pos_neg_bar_chart(df):
    # first create a figure with one axis
    fig, ax = plt.subplots(1)
    
    # create a color column
    df['color'] = df['Annual Change'].apply(lambda v: 'green' if v >= 0 else 'red')

    # create the bar chart with slightly wider bars
    df.plot(kind='bar', x='date', y='Annual Change', width=0.8, color=df['color'], ax=ax, label='Positive Change')
    plt.xticks(np.arange(0, 61, 10))
    plt.xlabel('Year')
    plt.ylabel('Change in %')
    plt.title('Annual Change in Inflation from 1961-2021')

    # slant the dates to be at an angle
    fig.autofmt_xdate()
```

```{tab-item} Data
Here are the first few lines of data in the DataFrame.  
![bar chart](../_static/inflation_data.jpg)
```

```{tab-item} Comments
* The x-axis label has only a few years listed because of the method `plt.xticks(np.arange(0, 61, 10))`. This reduces the number of ticks in the graph and makes it much more readable.  
* The years on the x-axis look nice due to the `xticks` call as well as `fig.autofmt_xdate()`. One could instead use `plot.xticks(rotation=45)` to provide a custom rotation of the x-label.  
* The Title and y-axis labels use the phrase `Change in` meaning that the value is relative to the prior year. The chart does not plot the actual inflation rate of that year (which is almost always positive).    
```

````

## Overlayed Bars
This is a bar chart that has the values overlayed one on top of the other. The values are NOT stacked. This means that the
base of the tall bar is at the bottom: the top of the bar has a height as denoted on the y-axis.
This example shows how to overlay bar charts as well as to annotate the bars with a values. 

````{tab-set}
```{tab-item} Image
![bar chart](../_static/annotated_bars.png)
```
```{tab-item} Plot Code
```python
def annotated_bars(df):
    # generate a 'payback' column
    df['payback'] = df['return'] / df['investment']
    
    # get the custom-sized figure and axis for annotation work.
    fig, ax = plt.subplots(1, figsize=(15,5))
    
    # Graphs two bar charts on the same axis, one overlayed on top of the other. 
    # One value must be known to be greater than the other if it is to be seen.
    # Plot the larger value first so that it doesn't completely hide the smaller value.
    plt.bar(x=df['year'], height=df['return'], color='#10E0D0', label='Return')

    # add annotations before plotting the second set of values
    add_value_labels(ax, df['payback'], fmt='x{:.2f}')

    # plot the shorter bars second, on top of the taller bars
    plt.bar(x=df['year'], height=df['investment'], color='#A030A0', label='Investment')
        
    # Adds formatting specifications like a legend and title
    plt.xlabel('Year')
    plt.ylabel('Dollars')
    plt.xticks([int(y) for y in df['year']], rotation=-45)
    plt.legend()
    plt.title('Investments & Returns')
```
```{tab-item} Annotation Code
Code source: <a href="https://stackoverflow.com/questions/28931224/how-to-add-value-labels-on-a-bar-chart" target="_blank">
StackOverflow</a>
```python
def add_value_labels(ax, values, fmt="{:.1f}", spacing=2):
    """
    Add labels to the end of each bar in a bar chart.

    Arguments:
        ax (matplotlib.axes.Axes): The matplotlib object containing the axes
            of the plot to annotate.
        values: the sequence of values to show
        fmt: a customizable format string used to print the values
        spacing (int): The distance in pixels between the labels and the bars
    """
    # For each bar: Place a label
    for index, rect in enumerate(ax.patches):
        # Get X and Y placement of label from rect.
        y_value = rect.get_height()
        x_value = rect.get_x() + rect.get_width() / 2

        # Number of points between bar and label. Change to your liking.
        space = spacing
        # Vertical alignment for positive values
        va = 'bottom'

        # If value of bar is negative: Place label below bar
        if y_value < 0:
            # Invert space to place label below
            space *= -1
            # Vertically align label at top
            va = 'top'

        # Format the value into a label
        label = fmt.format(values[index])

        # Create annotation
        ax.annotate(
            label,                      # Use `label` as label
            (x_value, y_value),         # Place label at end of the bar
            xytext=(0, space),          # Vertically shift label by `space`
            textcoords="offset points", # Interpret `xytext` as offset in points
            ha='center',                # Horizontally center label
            va=va)                      # Vertically align label differently for
                                        # positive and negative values.
```
```{tab-item} Data
Here is the complete set of data in the DataFrame. Notice how the annotated values are not present in this 
initial dataframe. Instead, the plotting code calculates the "payback factor" and adds this column before
plotting. 
![bar chart](../_static/annotation_data.jpg)
```

```{tab-item} Comments
* We broke out the annotation code separately because there is a lot going on there.  
* The overlayed bars is accomplished by plotting two bar charts, one with shorter bars on top of another with taller bars. The second plot covers up the first. If the second plot has values greater than the first, then the first plot's bars will be hidden.  
* The annotation code gets a bunch of rectangles (via `ax.patches`) that reveals the location of each bar in the plot. In creating this figure we have plotted multiple bar charts, so we need to annotate immediately after the first chart is plotted, otherwise we'd get many more rectangles due to the second plot.  
* We use custom colors for the bars using the `#RRGGBB` syntax.  
* The figure would be too narrow for our tastes, so we increase the figure size when calling `subplots`.  
```

````
## Sorted Bars
Bar charts usually have an x-axis that doesn't have a natural sorting order. However, sorting by the height of the bars is a valuable way to present data and insight.  

````{tab-set}
```{tab-item} Image
![bar chart](../_static/sorted_bars.png)
```
```{tab-item} Code
```python
def sorted_plt_bars(df):
    # we need the axis and a larger figure size to make this plot look nice
    fig, ax = plt.subplots(1, figsize=(12, 5))

    # remove any background grid that might be present (generally only needed if seaborn was used previously)
    ax.grid(False)

    # sort the dataframe. Here we assign back to df. Altneratively, we could have done `inplace=True`.
    df = df.sort_values(by='a_value', ascending=False)

    # no color parameter provided means that we default to a single blue color.
    bar = plt.bar(x=df['state'], height=df['a_value'])

    # this adds the value of the bar to the center of the bar
    ax.bar_label(bar, label_type='center')

    # make the x-axis values be slanted to ease the readability
    plt.xticks(rotation=60)

    # every plot needs good labels
    plt.title('Best "A Value" by State')
    plt.ylabel('A Value')
    plt.xlabel('')
```
```{tab-item} Data
This is the first 11 rows of the **orginal** data (which was unsorted).  

![bar chart](../_static/sorted_data.jpg)
```
```{tab-item} Comments
* When there are a good number of bars, the viewer will benefit if the bars are sorted.   
* In this chart, text is added inside the bar to provide the bar's value. Without a grid background (which can be added when using seaborn), it can be hard to know what the precise value is. There are multiple ways to add text. In this example, we use the `ax.bar_label` API. But, one can also use `plt.text` or `ax.annotate` methods.  
* The x-axis label is purposely set to an empty string because the viewer can clearly the x-axis values and understand their meaning.  
* The colors of the bars can be cusomized using the `color` named parameter. You can set all the bars to one identical color, or pass in a sequence of values such as `df['color']` (if you create a meaningful and correct color column in the dataframe).  
```
```` 

## Stacked Bars
Sometimes the addition of multiple values has meaning and you'll want to stack one bar on top of another. This allows you to see
multiples values and their sum total. We still sort the bars by a specific value to provide some added insight.   

````{tab-set}
```{tab-item} Image
![bar chart](../_static/stacked_bars.png)
```
```{tab-item} Code
```python
def stacked_df_plot_kind(df):
    # create a figure of a good size
    fig, ax = plt.subplots(1, figsize=(12, 5))
    
    # sort by one of the values in the dataframe
    df = df.sort_values(by='a_value', ascending=False)

    # x-axis of a bar chart is taken from the index, so set the index to the state
    df = df.set_index('state') 

    # tell matplotl;ib to plot a bar chart where the bars are stacked
    df.plot(kind='bar', stacked=True, ax=ax)

    # set labels to make it all readable
    plt.xticks(rotation=60)
    plt.title('Stacked Bar')
    plt.xlabel('')
    plt.ylabel('Both Values')
```

```{tab-item} Data
This is the first 11 rows of the **orginal** data (which was unsorted).  

![bar chart](../_static/sorted_data.jpg)
```

```{tab-item} Comments
* We could have chosen to sort by the sum total of the values charted. It all depends on what you're trying to illustrate.  
* If the DataFrame has more columns, each column's value will be stacked into this bar chart. Here, we have only two columns that are not the index value.  
```

````

## Side-by-side Bars
Sometimes you want to compare two values side-by-side across a set of categories.    

````{tab-set}
```{tab-item} Image
![bar chart](../_static/side-by-side-bars.png)
```
```{tab-item} Code
```python
def df_plot_kind(df):
    fig, ax = plt.subplots(1, figsize=(12, 5))
    # get the first 10 rows
    df = df.sort_values(by='b_value', ascending=True).loc[:10]

    # x-axis is taken from the index, so set that to the state
    df = df.set_index('state')

    # default to a single blue color. use color='red' for all red bars.
    # https://matplotlib.org/2.0.2/examples/color/colormaps_reference.html 
    df.plot(kind='bar', stacked=False, width=0.8, colormap='Spectral', ax=ax)

    plt.xticks(rotation=60)
    plt.title('Top 10 States')
    plt.ylabel('Both Values')
    plt.xlabel('')
    plt.legend(['A Value', 'B Value'])
```

```{tab-item} Data
This is the first 11 rows of the **orginal** data (which was unsorted).  

![bar chart](../_static/sorted_data.jpg)
```

```{tab-item} Comments
* More horizonal space is needed for side-by-side bar charts. You shouldn't show too many bars in one plot; we filter this chart down to just 10 states.  
* The width of each bar can give the chart a different feel. Here we increase the width a bit.  
* The color of each bar can be set manually via the named parameter `color`. Instead, we chose to use `colormap` which has a lot of different options, including gradients.  
```

````

## Horizontal Bar Chart
If we want to plot our bars horizontally, we can leverage the `barh` method.   

````{tab-set}
```{tab-item} Image
![bar chart](../_static/horiz_bars.png)
```
```{tab-item} Code
```python
def df_horiz_plot(df):
    fig, ax = plt.subplots(1, figsize=(8, 10))
    df = df.sort_values(by='state', ascending=False)

    # x-axis is taken from the index, so set that to the state
    df = df.set_index('state')
 
    # plot using the barh API
    df.plot.barh(stacked=False, width=0.6, ax=ax)
    plt.xticks(rotation=60)
    plt.title('State Values')
    plt.xlabel('Values')
    plt.ylabel('State')
    plt.legend(['A Value', 'B Value'])
```

```{tab-item} Data
This is the first 11 rows of the **orginal** data (which was unsorted).  

![bar chart](../_static/sorted_data.jpg)
```

```{tab-item} Comments
* DataFrame has a plot object. On this <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.html" target="_blank">plot object</a> we can call the following methods:  
    * area  
    * bar  
    * barh  
    * box  
    * ... and a bunch more ...
```

````
## Seaporn Bar Chart
Seaborn doesn't add much to Bar Charts. But, it does have fancy colors and a different background.   

````{tab-set}
```{tab-item} Image
![bar chart](../_static/seaborn_bars.png)
```
```{tab-item} Code
```python
def sorted_bars(df):
    fig, ax = plt.subplots(1, figsize=(12, 5))
    # sets the background grid style
    sns.set_style("darkgrid")
    df = df.sort_values(by='a_value', ascending=False)

    # default to various colors. use color='navy' to set all bars to the same color.
    # or, we can colormap='xxx' using values as found here:
    #     https://matplotlib.org/2.0.2/examples/color/colormaps_reference.html
    bar = sns.barplot(data=df, x='state', y='a_value', ax=ax)
    plt.xticks(rotation=60)
    
    plt.title('Best "A Value" by State')
    plt.ylabel('A Value')
    plt.xlabel('')
```

```{tab-item} Data
This is the first 11 rows of the **orginal** data (which was unsorted).  

![bar chart](../_static/sorted_data.jpg)
```

```{tab-item} Comments
* The background is a dark grid, as set by `sns.set_style`. 
* The color of each bar is set using a `colormap` which has a lot of different options, including gradients.  
```

````
# Future Work
Question: Can the annotation code method be used to annotate a geospatial plot?  
Question: Can we manually relocate Alaska and Hawaii in the geometry space to fake a small Alaska?  Also, draw a box around them.  
(Note that Krithika also had a Correlation Heat Map)
(Ria had Exhibit of geospatial that looks to be "stolen" from somewhere, but looks good!)