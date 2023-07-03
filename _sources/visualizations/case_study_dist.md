# Case Study on Distance
This page will present graphs for a 'fake' research project. It will show you both good graphs and bad graphs and a brief summary of what the graph means. It will provide the code used to generate the graphs as well a short discussion on the code: how the code works, why the code was selected, and potential pitfalls to watch out for when generating your own.  

This exercise is intended to show how one can be creative in examining and visualizing data to surface true insights.  

This exercise is **NOT** intended to show how to *clean* the data nor how to *test* the code.  

```{admonition} See Imports
:class: dropdown
Here are the imports and Seaborn initialization used in the code on this page. Furthermore, the code herein does not include saving the image to a file. Because the code was developed in Jupyter Notebook, we include `%matplotlib inline`.
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.ticker as mtick

import seaborn as sns

import scipy.integrate as integrate
from scipy.optimize import curve_fit

sns.set()

# This if for Jupyter Notebook only
%matplotlib inline
```

## Background of Hypothetical Project
This a hypothetical research project on **contrived data**. This dataset was **created** and is not real-life data. We pretend that this data was collected in the following hypothetical situation:  
* A random set of people (18 or older) were asked to throw a baseball. The distance was measured.  
* The person gave their age and gender. For simplicity, only male/female genders were considered.  
* The person was allowed to select a _single_ sport that they felt best represented their past (or present) athletic training. If a sport was selected, the person was supposed to have reached at least a high school varsity level in that selected sport.  
* The distance unit is yards. (but this metric is left out of all plots)  

A total of 1866 people's responses were recorded.

Here is a sample of the data. These are the people with the top 10 and bottom 10 distance values:  
![Distance Data](../_static/distance_data.jpg)  

Note that our is "clean" and is not riddled with `NaN` or errors. 
- - - 

## Worthless Graphs
Here are a set of common and essentially worthless graphs. A Final Report with only these plots in their report would be poor. These graphs are simple and not very insightful. Furthermore, one of the plots is mislabeled and misleading.    
````{tab-set}
```{tab-item} Average
The most common question would be to see the average distance thrown by gender. Here is the basic bar plot of that data. The small 'tick' or 'bar' at the top represents a range showing 95% confidence that the 'true mean' is within the range of the black bar. It assumes that the data we have is a sample from the true population and that it isn't 100% representative. With the count of data points present, the bar represents with 95% confidence where would the mean actuall fall in the true population. 

Is the bar helpful? <a href="https://youtu.be/a2xZrXzuwyk" target="_blank">I think NOT!! (click for Video Reference)</a>  

![bar chart](../_static/dist_bar_avg.jpg)  

The default is to have `ci=95` or not defined at all. What you see below is 
'sd' (St. Dev) is much better because we are not so focused on our confidence in the average so much as the variance in the distance. 
```python
def sns_bar_stats(df, ci):
    # display the line with something other than the default %95 confidence interval.
    sns.barplot(data=df, x='gender', y='distance', ci=ci)
    plt.ylabel('Distance')
    plt.xlabel('')
    plt.title('Average Distance')
```
```{tab-item} Distance vs Sport  
The idea was to show how each sport compares against other sport by showing how many people
were able to throw the ball at each specific distance. There are too many lines for one to make
much sense of anything. Furthermore, the x-axis is mislabeled! It presents itself as the distance
a person threw the ball, but in reality it represents a 'bin' (or a range of distances). There are
40 bins, each representing a range of 3. The graph makes it looks like the x-axis is the actual distance 
thrown instead of a bin number.  
![bar chart](../_static/distance_v_sport_line.jpg)  

```{admonition} See Data and Code
:class: dropdown
To understand the code a bit better, let's take a peek at what `df_buckets` looks like after it is created in the code below:  
![Bucket Data](../_static/dist_sport_hist_data.jpg)  

```python
def sport_hist(df):
    df_buckets = pd.DataFrame()
    # Define bin edges
    bins = range(0, 140, 3)
    sports = df['sport'].unique()
    # remove 'None' from the list of sports
    sports = [ s for s in sports if s != 'None']
    
    for sport in sports:
        # get histogram values by having numpy put into bins for us
        df2 = df[df['sport'] == sport]['distance']
        bars, bins = np.histogram(df2, bins=bins)
        df_buckets[sport] = bars
    
    # Set up plot
    sns.lineplot(data=df_buckets)
    plt.title('Distance vs Sport')
    plt.xlabel('Distance')
    plt.ylabel('Count')
    plt.legend()
```
```{tab-item} Gender w/ Sport & Age
This plot isn't *horrible* as it combines all three features into a single plot. The sports are identified by the color of the dots where we can clearly see that 'None' dominates the base of the plot. The age of the person is denoted by the size of the dots where it appears that the base of the plot is wider. If you squint, it kind of looks like two skinny spikes, sharper and redder at the top. It would mean that those who hadn't done any sport at all and are older throw the shortest. Those who played baseball and are younger throw the farthest.   

However, there are still many questions and issues. The spikes are far apart and don't leverage the graphing space well. The colors are hard to discern from one another (e.g. perhaps XCountry folks throw the farthest). It doesn't tell us how much farther one sport throws over another, the average distance, the variance, or many other interesting statistics about the data. The spikes are too skinner and compact to illucidate truly useful information.   

![Relplot by Gender, Sport and Age](../_static/dist_relplot_with_sport_age.jpg)  

```python
def scatter_plot(df):
    '''
    Create a scatter plot by gender with sports in color, age in size.
    '''
    sns.relplot(data=df, x='gender', y='distance', hue='sport', size='age')
    plt.title('Distance versus Gender w/ Sport & Age')
    plt.xlabel('')
    plt.ylabel('Distance')
```
```{tab-item} Stacked Bars
This plot shows the count of people at various distances. We can see that the male gender has a curve that looks to be a 'normal distribution'. Stacked on top of the male gender is the female gender. The stacking of the bars allows us to get an idea of the distribution of the entire sample set, but it doesn't allow us to see how the female gender is distributed.   
![Stacked Bar Chart](../_static/dist_stacked_bars.jpg)  

```python
def stacked_hist(df):
    male_data = df[df['gender'] == 'Male']['distance']
    female_data = df[df['gender'] == 'Female']['distance']
    plt.hist([male_data, female_data], histtype='barstacked', bins=10, alpha=0.7, color=['blue', 'pink'])
    plt.xlabel('Distance')
    plt.ylabel('Count')
    plt.title('Counts at Each Distance')
    plt.legend(['Male', 'Female'])
```
```{tab-item} Sports Histogram
This plot turned out so bad that I didn't even attempt to fix the fact that the x-axis labels are occluded, the y-axis ranges don't match, the color of all the bars are blue (don't differentiate themselves), and that there are gaps the bars. It is just ugly and upon first inspection, I knew that I didn't want to go any further with this plot. 
![Sport Histogram](../_static/dist_sport_hist.jpg) 

To get the bars to line up uniformly, we explicitly set the bins using `range(0, 140, 3)`. 
We generated a new `DataFrame` called `df_buckets` and set the height of the bars to be the count of people
within that bin. This is done for us using `np.histogram`.  Then, we enumerated through each sport and
plotted a histogram. We set the y-axis label on each axis so that we'd know which sport that subplot
was presenting. 
```{admonition} See Code
:class: dropdown
```python
def sport_hist_by_sides(df):
    df_buckets = pd.DataFrame()
    # Define bin edges
    bins = range(0, 140, 3)
    sports = df['sport'].unique()
    
    for sport in sports:
        # get histogram values by having numpy put into bins for us
        df2 = df[df['sport'] == sport]['distance']
        bars, bins = np.histogram(df2, bins=bins)
        df_buckets[sport] = bars
    
    fig, axes = plt.subplots(len(sports), figsize=(8, 15))
    for i, sport in enumerate(sports):
        # plot a sport histogram on each subplot
        data = df[df['sport'] == sport]
        axes[i].hist(data['distance'], bins=bins)
        axes[i].set_ylabel(sport)
```
````

## Data by Gender
It is always a good idea to get a firm idea of what the data comprises. In these next few plots we show how the data differs by gender. 

````{tab-set}
```{tab-item} Pie
The following pie chart shows us how many men and women there are. We can see that in this (fake) study, we had more men than women likely due to some bias in how the data was collected.

![Gender Pie](../_static/dist_gender_pie.png) 

The code to generate this pie chart will was the same as the more complicated pie charts below. In short, it was:  
```python
# Calculate the percentages of each gender
counts = df['gender'].value_counts()
percentages = counts / counts.sum() * 100
plt.figure(figsize=(8, 6))
plt.pie(percentages, labels=percentages.index, autopct=lambda pct: f'{pct:.1f}%', startangle=45)
```
```{tab-item} Average
As stated above, the most common question would be to see the average distance thrown by gender. Here we show the average along with the Standard Deviation in the data. The bar is relatively long showing that there is a good amount of variance in the data. 

![bar chart of avgerage distance by gender](../_static/dist_bar_sd.jpg)  
```python
# code snippet (see 'Average' tab above for more code)
sns.barplot(data=df, x='gender', y='distance', ci='sd')
```
```{tab-item} Histogram
In this histogram plot we have each gender plotted, female on top of male using a transparency (`alpha=0.7`). The transparency allows us to see both sets of bars, layered on top of one another, and that there is a 'normal distribution' for both genders. In this code, we explicitly set the boundaries of the bins so that we could easily know that the bin sizes were 10. Alternatively, we could have set the count of bins. However, setting the count of bins made it such that the female bin sizes were different because of the overall range being different. Setting the bin boundaries allows for the bars to line up nicely. 

The chart reveals that women are mostly likely to throw between 20-30 yards while men are most likely to throw between 40-50 yards. Also, women peak out at about 80 yards while men peak out around 110 with what appears to be an outlier(s) beyond 120 yards.  

![Histogram](../_static/dist_hist_mvf.jpg) 
```{admonition} See Code
:class: dropdown
``` python
def simple_hist(df):
    male_data = df[df['gender'] == 'Male']['distance']
    female_data = df[df['gender'] == 'Female']['distance']

    # Set up plot
    fig, ax = plt.subplots()

    # Define bin edges
    bins = range(0, 140, 10)

    # Plot histogram for males
    ax.hist(male_data, bins=bins, color='blue', alpha=0.7, label='Male')

    # Plot histogram for females
    ax.hist(female_data, bins=bins, color='pink', alpha=0.7, label='Female')
    ax.legend()
    plt.xlabel('Distance')
    plt.ylabel('Count')
    plt.title('Distance Histogram by Gender')
```

```{tab-item} Swarm
This plot provides a nice visual into the distribution of distance by gender. It gives more detail into how many people are at various distances. It reveals that men have a much broader spread of distances.
![Swarm Plot](../_static/dist_swarm.jpg) 
``` python
def swarm_plot(df):
    df2 = df[df['sport'] == 'None']
    sns.catplot(data=df2, x='gender', y='distance', kind='swarm')
    plt.xlabel('')
    plt.ylabel('Distance')
    plt.title('Swarm Plot of Distance by Gender')
```
````

## Data by Sport
Let's see if we can learn how the sport impacts the distance thrown. We already saw that a line plot was horrible. However, when examining the data by gender, we saw that a histogram provided some decent data, while a swarm plot was better. Attempts at these two plots showed that we needed to do even better. And, so we moved onto the better option, a box plot.
````{tab-set}
```{tab-item} Pie Chart
This pie chart shows how the sports compose both the male and female genres. We can see that more women do not affiliate with any sport at all, and that women are not a part of football.
![Sport Pie Chart by Gender](../_static/dist_pie_sport_both.png)  
```{admonition} See Code
:class: dropdown
```python
def plot_pie(ax, df, col_name, display_name):
    # Calculate the percentages of each category
    counts = df[col_name].value_counts()
    percentages = counts / counts.sum() * 100
   
    label_threshold = 2
    # Define the autopct formatting function
    def autopct_format(pct):
        return f'{pct:.1f}%' if pct >= label_threshold else ''

    # Create a list of labels based on the threshold
    labels = [name if percentages[name] >= label_threshold else '' for name in percentages.index]

    ax.pie(percentages, labels=labels, autopct=autopct_format, startangle=45)

    plt.axis('equal')
    ax.set_title('Percentage Makeup of ' + display_name)
    
    # Identify sports for the table that were not annotated
    not_annotated = [name for name in percentages.index if percentages[name] < label_threshold]

    # Create a table for not annotated sports
    if not_annotated:
        table_data = pd.DataFrame({display_name: not_annotated, 'Percentage': [f'{percentages[name]:.1f}%' for name in not_annotated]})
        table = ax.table(cellText=table_data.values, colLabels=table_data.columns, cellLoc='center', loc='bottom', bbox=[1, .75, .4, 0.25])
        table.auto_set_font_size(False)
        table.set_fontsize(10)
        table.scale(1, 1.5)
        
def plot_pie_by_side(df):
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))
    plot_pie(ax1, df[df['gender'] == 'Female'], 'sport', 'Sport (F)')
    plot_pie(ax2, df[df['gender'] == 'Male'], 'sport', 'Sport (M)')
```
```{tab-item} Swarm Plot
The swarm plot worked well for genders, let's try another one get get an understanding of Distance thrown by Sport. It is a little disappointing because the points are too uniform in their distribution and I don't come away feeling like I got any answers.  

![Sport Box Plot](../_static/dist_swarm_sport.png) 

```python
def swarm_sport_plot(df):
    # setting the figure size in Seaborn catplot requires used of height and aspect
    sns.catplot(data=df, x='sport', y='distance', kind='swarm', height=6, aspect=1.5)
    plt.xticks(rotation=-60)
    plt.xlabel('')
    plt.ylabel('Distance')
    plt.title('Swarm Plot of Distance by Sport')
```
```{tab-item} Distance Box Plot
Since I wanted to get some statistical insight into each sport, I decided to go with a boxplot. In this chart, sorted by average distance thrown, we can see that the sport Baseball has clear advantage over the rest, while No sport has a clear disadvantage. While Basketball appears to have a shorter average throwing distance than Hockey and Golf, there is a lot of variance to allow many basketball players to throw farther than most hockey players and golfers. When we look at the Age Box Plot showing Age Distribution by Sport (in the next tab) we can see that golfers had a much lower average age which likely gave them an advantage.   

![Sport Box Plot](../_static/dist_sport_boxplot.jpg)   

```{admonition} Note
Code for this Distance Box Plot can be seen in the next tab, Age Box Plot.

```{admonition} Box Plot Explanation
:class: dropdown
In a boxplot, the box represents the interquartile range (IQR) of the data, which is a measure of statistical dispersion. The box spans the range between the first quartile (Q1) and the third quartile (Q3) of the data. The line inside the box represents the median (Q2), which is the value that divides the data into two equal halves.

The length of the box gives an indication of the spread of the middle 50% of the data. A longer box indicates a larger range between the first quartile and the third quartile, suggesting greater variability in the data.

The bars extending from the box are called whiskers. The whiskers represent the range of the data, excluding any outliers. The length of the whiskers can vary depending on how outliers are defined and displayed in the plot. The whiskers can extend to a maximum of 1.5 times the IQR from the box.

Any data points outside the whiskers are considered outliers and are plotted as individual points. Outliers are typically displayed as dots or small markers on the plot and can provide insights into extreme or unusual observations in the data.

Some boxplots may also include additional elements, such as notches or confidence intervals, which provide additional information about the uncertainty or variability in the data.

Overall, boxplots provide a compact visualization of the distribution of a dataset, including measures of central tendency (median) and dispersion (IQR), as well as potential outliers. They are useful for comparing distributions, identifying skewness, detecting outliers, and gaining an overall understanding of the spread and shape of the data.
```
```{tab-item} Age Box Plot
In this plot, we see how the distribution of ages was not the same across each sport. This contributes to the distance of the throwers in a particular sport. We will first show that `age` correlates to `distance` below.  

![Age Box Plot](../_static/dist_age_by_sport.png)
```{admonition} See Code
:class: dropdown

```python
def boxes_for_sports(df):
    '''
    In this method, we get the mean distance for each sport so that we can sort the
    dataframe by the mean distance. 
    '''
    # we probably could have done something similar with a pivot table, but that would
    # have left out the statistical, distribution information
    # pivot_table = df.pivot_table(index='gender', columns='sport', values='distance', aggfunc='mean')
    
    sports = df['sport'].unique()
    plt.figure(figsize=(8,8))
    
    # Calculate the average distance for each sport
    # keep original index to make it easy to merge on sport
    average_distance = df.groupby('sport')['distance'].mean().reset_index()

    # add/merge the average_distance values back into the original dataset
    sorted_df = df.merge(average_distance, left_on='sport', right_on='sport')
    
    # Sort the DataFrame based on average distance in ascending order
    # Both dataframes had 'distance' so there is now 'distance_x' = original
    # and 'distance_y' which is the mean.
    sorted_df = sorted_df.sort_values('distance_y')

    # Create the boxplot using the new sorted DataFrame
    sns.boxplot(data=sorted_df, x='distance_x', y='sport')
    plt.title('Distribution by Sport')
    plt.ylabel('')
    plt.xlabel('Distance')

def boxes_for_sports_age(df):   
    fig, ax = plt.subplots(1, figsize=(8,8))
    sns.boxplot(ax=ax, data=df, x='age', y='sport')
    plt.title('Age Distribution by Sport')
    plt.ylabel('')
    plt.xlabel('Age')
```
```{tab-item} Area Plots
Below you'll see two plots. First is an Area Plot that shows the count of people in each sport. You'll see that there is a big hump around 20-30 yards because that is the distance that most people can throw. The primary "sport" contributing to that distance is "None", but that is the largest contributor overall. As the distance grows out farther, it become more difficult to differentiate between the sports because are simply too few people at those great distances.   

![Sport Area](../_static/dist_sport_area.png)  

While the above plot provides good information, it begs a question: What **percentage** does each sport contribute at each distance?  Creating a graph to answer that question took some creativity and some coding effort to _organize the data_. Essentially, we created a dataframe that represented the percentage of people representing a specific distance for each sport.  

![Sport Area by Percent](../_static/dist_sport_area_perc.png)
```{admonition} note
If you want to see the intermediate DataFrames and the code to create the above plots, well... I'm not sharing that exactly. **BUT**, you can see virtually the same thing in the section below, "Data by Age" in the *Area of Percent* tab. Check it out!
```
````

## Data by Age

````{tab-set}
```{tab-item} Pie Chart
The largest age groups happen to be: 38-47, then 28-37, followed by 18-27. This is a bias in the data and will skew the
results of the entire research. Given that we will soon see that younger people throw a bit farther on average, that
having our data skewed a bit older makes the results less accurate overall. The general population gets smaller as
the ages go up, and surely this distribution by age does not match what we expect.  

![Age Pie](../_static/dist_pie_age.png)   
```{admonition} See Code
:class: dropdown
See the code for the `plot_pie` method in the section above "Data By Sport -> Pie Chart".  
```python
def pie_by_age(df):
    # add an age bracket to a copy of the DF
    df2 = df.copy()
    bracket_names = [ str(n)+"-"+str(n+9) for n in range(18, 81, 10) ]
    bracket_names.append('88-99')
    age_bracket = [ bracket_names[-1] if age > 87 else bracket_names[(age-18)//10] for age in df['age'] ]
    df2['age_bracket'] = age_bracket
    df2 = df2.sort_values(by='age_bracket')
    fig, ax = plt.subplots()
    plot_pie(ax, df2, 'age_bracket', 'Age Bracket')
```
```{tab-item} Histogram
Here we see that the younger you are, the farther you can throw. The one exception is in the 88-99 age bracket. There we see that they are a bit better than they 78-87 year olds. Even though the average is slightly greater than the 68-77 year-olds, the range is much smaller. This is probably due to the low numbers we have the higher age group and is an anomoly in the data. 

![Age Box Plot](../_static/dist_age_box_plots.png)   

```python
def boxes_by_age(df):
    # add an age bracket to a copy of the DF
    df2 = df.copy()
    bracket_names = [ str(n)+"-"+str(n+9) for n in range(18, 81, 10) ]
    bracket_names.append('88-99')
    age_bracket = [ bracket_names[-1] if age > 87 else bracket_names[(age-18)//10] for age in df['age'] ]
    df2['age_bracket'] = age_bracket
    df2['age_bracket'] = age_bracket
    df2 = df2.sort_values(by='age_bracket')
    
    plt.figure(figsize=(8,8))
    sns.boxplot(data=df2, x='distance', y='age_bracket')
    plt.title('Distribution by Age')
    plt.ylabel('')
    plt.xlabel('Distance')
```
```{tab-item} Area of Percent
This plot is starting to show a little more creativity. Notice a few things:  

First, the y-label goes up to 1.0, which represent 100% of people at that distance. No matter what distance we look at, all the people there represent 100% of the people there. For example, even though at 120 yards there are only 2 people there, they make up 100% of the people there. At 110 yards, there is only one person who happens to be in the 18-27 year-old age-bracket, which is why the graph is entirely blue at 110 yards.   

Secondly, the older participants make up a very small percentage of the people overall and they are virually gone at 70 yards (with just a few outliers). At very short distances, the majority of people there are 58 and older. 

![Area of age percentage at each distance](../_static/dist_age_area.png)   
```{admonition} See Code and Data
:class: dropdown

In the code below you'll see that we create three different DataFrames:  
1) A new dataframe, `df2`, that has Distance "bins" and Age-Brackets for each person. (not shown) 
2) A `pivot table` created using `pd.pivot_table` API which is a fancy way to count the number of people in each bin for each age-bracket. This could also have been done using `df.groupby`.  
3) A DataFrame structured identically to the pivot table, only all the values are converted to percentages of the row.  

** DataFrame  `pivot_table` **  
![DataFrame df2](../_static/dist_age_df2.jpg)   

** DataFrame : Final Table as Percentages **  
![DataFrame df2](../_static/dist_age_pivot_table.jpg)  

```python
def create_perc_by_age_df(df):
    # add an distance bins and age bracket to a copy of the DF
    df2 = df.copy()
    bin_names = [ n for n in range(0, 140, 10)]
    df2['bin'] = [ int(d // 10) * 10 for d in df2['distance']]
    bracket_names = [ str(n)+"-"+str(n+9) for n in range(18, 81, 10) ]
    bracket_names.append('88-99')
    age_bracket = [ bracket_names[-1] if age > 87 else bracket_names[(age-18)//10] for age in df['age'] ]
    df2['age_bracket'] = age_bracket
    
    # Pivot to get totals of age at distance
    pivot_table = pd.pivot_table(df2, values='distance', index='bin', columns='age_bracket', aggfunc='count', fill_value=0)
    
    # create a datafame showing percent of count at bin belongs to age-group
    data_per_bin = { 'bin': pivot_table.index }
    totals = { index: row.sum() for index, row in pivot_table.iterrows() }
    for col in pivot_table.columns:
        data_per_bin[col] = [ r / totals[index*10] for index, r in enumerate(pivot_table[col])]
    
    return pd.DataFrame(data = data_per_bin)

def plot_perc_by_age_area(df):
    df2 = create_perc_by_age_df(df)
    ax = df2.plot.area(x='bin', figsize=(10, 5))
    ax.legend(loc='upper left', bbox_to_anchor=(1.02, 1))
    ax.set_xlabel('Distance')
    ax.set_ylabel('Percentage at Distance')
    ax.set_title("Each Age-Groups' Percentage at Distance")
````

# Machine learning

TODO: We've created a ML model that predicts distance based on the three features: gender, sport and age. (I think) the results show that the model is not very accurate at predicting.

(show accuracy)
(show code)
