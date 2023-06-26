# Geospatial Plots

Geospatial plots are great at:  
1. Showing how an **area** is impacted relative to other **areas.**  
2. Revealing which area is impacted.  
3. Illustrateing a pattern in the location of something.

Geospatial plots are NOT good at:  
1. Showing correlations. (Use a line plot for this)  
2. Emphasizing the amount of difference between one area and another.  

## Contiguous States Only
Let's start off by showing the benefits of showing only the contiguous United States. 
Imagine that we are trying to show which states have the most electoral college votes
and perhaps we want to emphasize that California has the most by a long shot.

````{tab-set}
```{tab-item} Image
One the left, we see what many students show--the full 50 states.  
One the right, is a much improved image showing only the 48 contiguous states.  
![election image](../_static/geo_demo_clip.jpg)
```
```{tab-item} Code
```python
fig, (ax1, ax2) = plt.subplots(1,2, figsize=(15,5))

# Left Side: Plot the entire United States
gdf.plot(ax=ax1, column='Electoral Votes')

# Right Side: Plot the contiguous US with a legend
gdf.plot(ax=ax2, column='Electoral Votes', legend=True)
ax2.axis('off') # remove the box and the x,y ticks

# Set the extent of the axes to cut off Alaska and Hawaii
ax2.set_xlim(-130, -65)
ax2.set_ylim(24, 50)
```

```{tab-item} Data
This data is a merge of two different data sources: electoral_college.csv and a ShapeFile of the United States.  You'll note that in the code we were able to read column values `"707,558"` (a string with a literal comma as the thousands separator), by using the named parameter `thousands` in the `read_csv` call. Handy!! We also eliminated a duplicate column using `drop`.     
![election data](../_static/geo_elect_data.jpg)
```python
electoral = pd.read_csv('electoral_college.csv', thousands=',')
gdf = us_states.merge(electoral, left_on='NAME', right_on='State', how='left')
gdf = gdf.drop(columns='State') # this is a duplicate of 'NAME'
```

```{tab-item} Comments
In this example, we have two geospatial in one figure where there are just three differences.  
1. The box and ticks are hidden  
2. We clip off Alaska & Hawaii  
3. We show a legend  

By hiding Alaska and Hawaii, we can bring a much greater focus on the states. Providing a legend is very helpful. And, eliminating the box with longitude and latitude ticks removes an unnecessary distraction since we really don't care about the lat/long.  

In the chart on the right, we can easily see that California is large and brilliant yellow which ephasizes its impact. 
There are two ways to hide these states. One way is to eliminate them from the GeoDataFrame:  
`gdf = gdf[(gdf['NAME'] != 'Alaska') & (gdf['NAME'] != 'Hawaii')]`  
Another way is to set some limits on the x & y axes: `ax2.set_xlim(-130, -65)`
```
````

## Inset Alaska & Hawaii
Eliminating two states from the drawing isn't so great. We'd like to show Alaska and Hawaii like other maps do using an `inset`. This can be done, but it does get complicated rather quickly. The inset is a separate plot with separate arguments. When legends are shown, the size of the figure changes and the placement of the inset changes. I provide this code because it is educational to see and play with, but I recommend the method below this.  
```{admonition} Inset Image and Complicated Code
:class: dropdown
![election image](../_static/geo_inset_no_borders.jpg)
```python
def draw_us_inset(gdf, **args):
    # Create a new figure and axes for the main plot
    fig, ax = plt.subplots(1, figsize=(12,5))

    # Plot the entire United States
    gdf.plot(ax=ax, **args)

    # Set the extent of the main plot to cut off Alaska & Hawaii
    ax.set_xlim(-130, -65)
    ax.set_ylim(23, 50)

    # helper method to plot both insets without a border, no legend, correct vmin/vmax
    def inset(position, name, xlim=None):
        '''
        position = a list: [x, y, width, height] in % of figure size
        '''
        ax = fig.add_axes(position)
        state = gdf[gdf['NAME'] == name]
        args_no_legend = args
        args_no_legend['legend'] = False
        # The new plot for the inset needs to have the vmin/vmax set to the same
        # values as the main plot so the colors show correctly
        if 'column' in args:
            args_no_legend['vmin'] = gdf[args['column']].min()
            args_no_legend['vmax'] = gdf[args['column']].max()
            
        state.plot(ax=ax, **args_no_legend)
        
        # remove box around inset in 1-line comprehension
        [ ax.spines[side].set_visible(False) for side in ['top', 'bottom', 'left', 'right'] ]
        
        # clip our inset if needed
        if xlim:
            ax.set_xlim(xlim)
        ax.set_xticks([])
        ax.set_yticks([])

    inset([0.20, 0.20, 0.20, 0.20], 'Alaska', xlim=(-180, -130))
    inset([0.37, 0.19, 0.05, 0.15], 'Hawaii')

draw_us_inset(gdf, column='Electoral Votes')
```


## Modified Geometry
It becomes much easier to deal with plotting the full United States if the GeoDataFrame's geometry is modified to put Alaska and Hawaii in the "right" spot. The only drawbacks are:  
* If you do geospatial `sjoin`s, then it'll all get messed up geographically.  
* If you want to illustrate something on the Pacific Ocean, there are states in the way!  

````{tab-set}
```{tab-item} Image
![election image](../_static/geo_elect.jpg)
```
```{tab-item} Code
```python
from shapely.affinity import translate
from shapely.affinity import scale
from shapely.geometry import MultiPolygon

def modify_geometry(gdf, name_col='NAME'):
    '''
    Changes, in place, the geometry of Alaska & Hawaii in the GeoDataFrame to be "inset"
    name is the column that contains the name of the state.
    '''
    def scale_translate(state_name, ratio=1.0, offset=(0,0)):
        # get the geometry and save the index value using the walrus operator
        multi_poly = gdf.loc[(index:=gdf[gdf[name_col] == state_name].index[0]), 'geometry']

        # scale each polygon in the state's multi-polygon in both x & y direction
        multi_poly = MultiPolygon([scale(poly, ratio, ratio) for poly in multi_poly])
        # move the state by the offset values
        multi_poly = translate(multi_poly, xoff=offset[0], yoff=offset[1])
        # set the value using the 'at' method because 'loc' won't work
        gdf.at[index, 'geometry'] = multi_poly
        
    scale_translate('Alaska', ratio=0.35, offset=(26,-35))
    scale_translate('Hawaii', offset=(45, 5))

def plot_votes(gdf):
    fig, ax = plt.subplots(1, figsize=(10,5))

    # Plot the entire United States
    gdf.plot(ax=ax, column='Electoral Votes', legend=True)
    # remove the box and the x,y ticks
    ax.axis('off') 

    # Set the extent of the main plot to cut off Alaska's long tail of regions
    ax.set_xlim(-130, -65)
    # without this limit, we get Alaska's tail looking like it's part of Hawaii
    # It's better just to eliminate that portion of the plot
    ax.set_ylim(24, 50)
    
    plt.title('Electoral College Votes by State')

# Call the methods above to generate the plot using modified geometry
modify_geometry(gdf)
plot_votes(gdf)
```

```{tab-item} Data
This data is a merge of two different data sources: electoral_college.csv and a ShapeFile of the United States.  You'll note that in the code we were able to read column values `"707,558"` (a string with a literal comma as the thousands separator), by using the named parameter `thousands` in the `read_csv` call. Handy!! We also eliminated a duplicate column using `drop`.     
![election data](../_static/geo_elect_data.jpg)
```python
electoral = pd.read_csv('electoral_college.csv', thousands=',')
gdf = us_states.merge(electoral, left_on='NAME', right_on='State', how='left')
gdf = gdf.drop(columns='State') # this is a duplicate of 'NAME'
```

```{tab-item} Comments
When the geometry of the GeoDataFrame is modified, the plotting code is pretty simple and allows for further customizations without crazy code. A few points worthy of calling out:  
* We use a `walrus` operator (`:=`) to assign a sub-expression to a variable in the middle of a larger expression. This allows us to reuse the value again later on in the code. It would have been just as easy to write it with two lines of code instead of one, but... _Bragging Rights!_  
* When modifying the GeoDataFrame, we used the <a href='https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.at.html' target='_blank'>`at` method</a> instead of `loc`. Using loc results in an error: "ValueError: Must have equal len keys and value when setting with an iterable".  
```
````

## Annotated with Table Inset
The problem with the plot above is that it is very hard to see if there is any difference between Orgegon and Nevada; the colors are just too close! To fix that we will annotate each state with the count of the votes printed onto the state's location. 
````{tab-set}
```{tab-item} Image
![election image](../_static/geo_elect_annotated.jpg)
```
```{tab-item} Code
```python

def annotate_states(gdf, ax, value_col, not_states=None, name_col='NAME'):
    # annotate the states in the list, states, with values in col_name
    # Filter first so that we iterate through the rows that have the state name we want
    gdf_states = gdf if not_states is None else gdf[~gdf[name_col].isin(not_states)]
    for _, row in gdf_states.iterrows():
        # get the location of the state from the geometry
        x, y = row.geometry.centroid.x, row.geometry.centroid.y
        # add the text with an xytext offset that seems right for our plots size
        ax.annotate("{:.0f}".format(row[value_col]), (x, y), xytext=(-10, 0), textcoords='offset points')

def add_table_inset(fig, data):
    # x, y, width, height as % of figure
    ax_table = fig.add_axes([.77, .35, .15, .4])
    ax_table.axis('off')
    table = ax_table.table(cellText=data.values, colLabels=data.columns, cellLoc='center', loc='center')
    # Adjust the font size of the table
    table.auto_set_font_size(False)
    table.set_fontsize(10)
    table.scale(1, 1.5)

def plot_annotated_votes(gdf):
    fig, ax = plt.subplots(1, figsize=(10,5))

    # Plot the entire United States
    # Choose the 'cool' colormap so the black text appears nicely
    gdf.plot(ax=ax, column='Electoral Votes', legend=True, cmap='cool', 
             legend_kwds={'orientation':'horizontal'}, edgecolor='lightgray')
    # remove the box and the x,y ticks
    ax.axis('off') 

    # Set the extent of the main plot to cut off Alaska's long tail of regions
    ax.set_xlim(-130, -65)
    ax.set_ylim(24, 50)
    
    plt.title('Electoral College Votes by State')
    
    small = ['District of Columbia', 'Rhode Island', 'New Jersey', 'Delaware', 'Vermont', 'New Hampshire', 'Connecticut']
    annotate_states(gdf, ax, 'Electoral Votes', not_states=small)
    
    # Before we can show our table, we need a DataFrame the data.
    # Create the data of integer values of the smaller states, sorted by state name, with abbreviations
    df = gdf[gdf['NAME'].isin(small)].sort_values(by='NAME')
    d = { 'State': ['CN', 'DE', 'DC', 'NH', 'NJ', 'RI', 'VT'],
          'Votes': list(df['Electoral Votes'].apply(lambda n: int(n))) }
    
    # show a table of the values for the smaller states
    add_table_inset(fig, pd.DataFrame(data=d))
    
# Be sure we have our modified geometry before calling the code above
modify_geometry(gdf)
plot_annotated_votes(gdf)
```

```{tab-item} Data
This data is a merge of two different data sources: electoral_college.csv and a ShapeFile of the United States.  You'll note that in the code we were able to read column values `"707,558"` (a string with a literal comma as the thousands separator), by using the named parameter `thousands` in the `read_csv` call. Handy!! We also eliminated a duplicate column using `drop`.     
![election data](../_static/geo_elect_data.jpg)
```python
electoral = pd.read_csv('electoral_college.csv', thousands=',')
gdf = us_states.merge(electoral, left_on='NAME', right_on='State', how='left')
gdf = gdf.drop(columns='State') # this is a duplicate of 'NAME'
```

```{tab-item} Comments
We moved the legend to be horizontal, not because it was necessary, but because we can. This was accomplished by using the `legend_kwds` argument in the plot method. There are other ways to do this (as always).  

There are several issues that we address in this plotting solution: 
|Problem|Fix|  
|-------|---|  
|The black text doesn't show up well with the default colormap.|Change the `colormap` to 'cool'.|   
|The smaller states don't have room for the text. It all gets printed on top of each other and is unreadable.|Avoid annotating values on the states with a small geometry. We just manually do this, however, we could have used the 'CENSUSAREA' column to help us out with that. Doing it explicitly is good enough for us.|  
|The smaller states' values get lost when not shown!|Create an inset table that displays the values|  
|The dataframe of values is floating point|Use the apply method and a lambda to convert all the values to integer. There is probably another way... there always is!|
```
````

## Correlation Lost
Show how the correlation between population and electoral votes is lost in this type of plot. show how setting vmin, vmax can help. But, really we just need to do a line plot.

# Future Work
Question: Can the annotation code method be used to annotate a geospatial plot?  
Question: Can we manually relocate Alaska and Hawaii in the geometry space to fake a small Alaska?  Also, draw a box around them.  
(Note that Krithika also had a Correlation Heat Map)
(Ria had Exhibit of geospatial that looks to be "stolen" from somewhere, but looks good!)