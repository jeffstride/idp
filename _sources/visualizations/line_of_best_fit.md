# Curve of Best Fit
In this section, we will show how you can identify a Curve of Best Fit for a set of data points.
You can choose the form of the equation of the line; it can be a line, parabola, polynomial of order 4 or more,
or some custom equation like Sigmoid.  

We will review three different ways to get the equation of a fitted curve.  
1. `scipy.stats.linregress`: a statistical method that identifies a line's coefficients as well some statistical information.  
2. `numpy.polyfit`: a Numpy method that identifies the coefficients of any n-ordered polynomial.  
3. `scipy.stats.curve_fit`: a statistical method that identifies the coefficients of **_any_ function** as well as some statistical information about the fit.  

In identifying a Curve of Best Fit, it is good to know _how good_ the curve is at representing
the data points. You should quanitify that it is better worse than a parabola. We can do some of this with 
the Mean Squared Error.  

Often we want to know how much of a correlation there is between the x & y data points. Afterall, 
we may have just asked Seaborn to plot a regression line and the line presented is the best line that fits the
data, but is the data linearly related at all? This is a different, but also important question! This is
answered by looking at the `Coefficient of Determination`.  

```{admonition} $R^2$ or Coefficient of Determination  
:class: dropdown tip
R-squared ($R^2$) is a statistical measure that provides an indication of how well the line of best fit (the regression line) fits the data points. It quantifies the proportion of the variance in the dependent variable (y) that can be explained by the independent variable (x) in a linear regression model.

The R-squared value ranges from 0 to 1. A value of 1 indicates that the regression line perfectly predicts the dependent variable, meaning all the data points lie exactly on the line. A value of 0 indicates that the regression line does not explain any of the variance in the dependent variable, and the points are scattered randomly.

In general, a higher R-squared value indicates a better fit of the line to the data. For example, an R-squared value of 0.8 means that 80% of the variability in the dependent variable is accounted for by the independent variable(s) in the model.
```

Here is a table that shows some of the most frequent API we used in this section. 

|API|Notes|  
|---|-----|
|[plt.plot](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)|This does a simple line plot on the current axis. It does not offer 'ax=ax' argument.|  
|[plt.scatter](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html)|This does a simple scatter plot on the current axis. It does not offer 'ax=ax' argument.|  
|[np.linspace](https://seaborn.pydata.org/generated/seaborn.regplot.html)| This creates a numpy array of values linearly spaced between [start, end] with a specific number of points. It is helpful in generating `x_data` during plotting.|   
|[np.polyfit](https://numpy.org/doc/stable/reference/generated/numpy.polyfit.html)|This identifies the coefficients of any n-ordered polynomial.|   
|[linregress](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.linregress.html)|a statistical method that identifies a line's coefficients as well some statistical information.|  
|[curve_fit](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html#scipy.optimize.curve_fit) |A statistical method that identifies the coefficients of **_any_ function** as well as some statistical information about the fit.|  
|[mean_squared_error](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_squared_error.html)|Calculates the Mean Squared Error (MSE) from two sets of y_data points.|  

```{admonition} code imports
:class: dropdown note

```python
import random
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from scipy.optimize import curve_fit
from scipy.stats import linregress
from scipy import stats
from sklearn.metrics import mean_squared_error

sns.set()

# This if for Jupyter Notebook only
%matplotlib inline
```

## Seaborn Regression
In many research projects, it is beneficial to find a curved line that best fits the data.
Students will often do a scatter plot of the data points and have Seaborn do a regression plot
which shows a line of best fit with a shaded area around the line representing
a 95% confidence interval. None of that is horrible. It is convenient to have a line of best fit, 
if there is one. And, `regplot` will draw one for you by default.  

````{tab-set}
```{tab-item} Simple regplot
![regplot](../_static/bestfit_simple_reg.png)  
```
```{tab-item} Code
```python
true_slope = 3/4
true_intercept = -4
x_data = [ x for x in range(3, 50, 2) ]
y_data = [ x*true_slope + random.randint(-5, 5) + true_intercept for x in x_data]

# Use the grid in the plot and set the line style to black & dashed
plt.grid(True, linestyle='--', linewidth=0.5, color='black')
sns.regplot(x=x_data, y=y_data)
```
```{tab-item} Comments
This is about as simple as it gets. We generated `x_data` with a simple comprehension. We could
have also used `np.linspace()`. We similarly created the `y_data` and added some noise with
`random.randint(-5, 5)`. By default, `regplot` will add a regression line and a confidence
interval. The confidence interval is 95% and students often misunderstand what it means. 

It does **NOT** mean that there is a 95% confidence that the points in the scatter plot will
fall within the shaded interval. Clearly, that is not the case!  

It means, insteatd, that there is a 95% confidence that the average of the scatter plot data falls within that range.
I know what you're thinking: the average of the data is clear and concrete--there is no need to estimate it. 
That is true. The average is easy to 
calculate with a finite set of points that **are** the _true population_ data. 
`regplot` estimates what the _true population_ might look like assuming that your data is just a sample. It then calculates
the confidence interval based on the assumption that the errors (residuals) in the regression model 
follow a normal distribution. It is 95% sure that the _true average_ falls in that range.  

Note that in your research, you may want to extend the curve of best fit out further. You can see
how to do this in the next plot below.  

Here are some helpful links:  
<a href="https://seaborn.pydata.org/tutorial/regression.html" target="_blank">Seaborn Tutorial</a>    
<a href="http://seaborn.pydata.org/generated/seaborn.regplot.html" target="_blank">Seaborn regplot API</a>    

```{admonition} Lastly
:class: important
It is common to hide the shaded confidence interval by setting the named parameter, `ci` to `None`, as follows:
```python
sns.regplot(x_data, y_data, ci=None)
```

````


## SciPy Linregress
````{tab-set}
```{tab-item} Annotated Regression
This plot shows a scatter plot of data drawn with `plt.scatter`. It then finds the line of best fit using
`linregress`. It plots it out, extending an extra 20 values on the x-axis, and it provides data on the
graph itself. It shows what the slope and y-intercept are (m & b), gives the $R^2$ value, and lastly
it presents the Mean Squared Error.  
![regplot](../_static/bestfit_linregress.png)
```
```{tab-item} Code
```python
# use the same x_data & y_data in example above.
# To find details about the line, we need to use linregress.
slope, intercept, r_value, p_value, std_err = linregress(x_data, y_data)

# generate 100 x_fit points and go out 20 past x_data limits to show "prediction"
x_fit = np.linspace(min(x_data), max(x_data)+20, 100)
y_fit = intercept + slope * x_fit

# create a 'vector' (list of values) for the line of best fit.
# We use the scalar values (1 value) from linregress and the original x_data points.
# We need the same number of y values as are in y_data.
y_predicted = intercept + slope * np.array(x_data)

# Calculate the MSE 
mse = mean_squared_error(y_data, y_predicted)

# plot our data points with line of best fit with info on the graph
plt.figure(figsize=(10, 5))
plt.scatter(x_data, y_data, label='Actual')
plt.plot(x_fit, y_fit, color='red', label='Fitted')
plt.grid(True, linestyle='--', linewidth=0.5, color='black')
plt.legend()
plt.title('Best Linear Fit', fontsize=16)
plt.xlabel('X')
plt.ylabel('Y')
plt.text(42, 20, f'm = {slope:.2f}\nb = {intercept:.2f}\nR2 = {r_value**2:.2f}\nMSE = {mse:.2f}', 
         ha='left', va='top', fontsize=14)
```
```{tab-item} Comments
Comments go here.
```
````

## Numpy Polyfit  
Here we use `np.polyfit` to find the best fit for a line and a parabola. Put another way,
the coefficients of a polynomial of degree 1 and 2.  
````{tab-set}
```{tab-item} Best Fit Plot
The graph shows many things: scatter plot of data, line of best fit, parabola of best fit,
a legend, coefficients of the parabola of best fit, and MSE of both the parabola and line. Whew!  
It shows that the parabola is a much better fit for the points.  
![regplot](../_static/bestfit_polyfit.png)
```
```{tab-item} Code
```python
def add_inset_text(fig, position, actual, coeffs):
    # print values in an inset positioned in figure percentages [x, y, width, height]
    ax_inset = fig.add_axes(position)
    ax_inset.set_xlabel('')
    ax_inset.set_ylabel('')
    ax_inset.set_xticks([])
    ax_inset.set_yticks([])
    ax_inset.grid(False)
    text = 'Coeff Actual vs Pred'
    ax_inset.text(0.05, 0.90, text, ha='left', va='top', fontsize=14)
    text = ''
    for a, c in zip(actual, coeffs):
        text += f'{a:.2f} vs {c:.2f}\n'
    ax_inset.text(0.18, .70, text, ha='left', va='top', fontsize=12)
    return ax_inset
    
    
def best_parabola_fit():

    def generate_points(a, b, c, noise):
        x_data = [ x for x in range(3, 50, 2) ]
        y_data = [ parabola(x, a, b, c) + random.randint(-noise, noise) for x in x_data]
        return x_data, y_data
    
    # establish our True parabola coefficients
    actual = (0.45, 2.5, -7)
    noise = 150
    x_data, y_data = generate_points(*actual, noise)
    
    # plot it all
    fig, ax = plt.subplots(figsize=(10,5))

    # Use the grid in the plot and set the line style to black & dashed
    plt.grid(True, linestyle='--', linewidth=0.5, color='black')
    
    # Eliminate the confidence interval shading of the parapola and color the line red
    sns.regplot(x=x_data, y=y_data, ax=ax, order=2, ci=None, line_kws={'color':'red'})
    
    # Determine if a linear line is a better fit using MSE
    # find the coefficients of the parbola that best fits the points generated
    # The coefficients are ordered from high order to lower order
    coeffs_2 = np.polyfit(x_data, y_data, 2)
    y_predicted_2 = [ coeffs_2[0]*x**2 + coeffs_2[1]*x + coeffs_2[2] for x in x_data]
    mse_degree_2 = mean_squared_error(y_data, y_predicted_2)
    
    #  get coefficients for the line
    coeffs_1 = np.polyfit(x_data, y_data, 1)
    # Use vector math instead of a comprehension this time (because we can)
    y_predicted_1 = coeffs_1[1] + coeffs_1[0] * np.array(x_data)
    mse_degree_1 = mean_squared_error(y_data, y_predicted_1)
    print('MSE Degree2:', mse_degree_2, ' MSE Degree1:', mse_degree_1)
    
    # add MSE to our inset text box
    ax_inset = add_inset_text(fig, [0.15, 0.50, 0.35, 0.28], actual, coeffs_2)
    ax_inset.text(0.6, 0.90, 'MSE:', ha='left', va='top', fontsize=14)
    text = f'Line:{mse_degree_1:.0f}\nPara:{mse_degree_2:.0f}'
    ax_inset.text(0.65, .70, text, ha='left', va='top', fontsize=12)
    
    # since plt.plot() does not offer ax=ax argument, and without it we plot on the inset,
    # use ax.plot() to get the line to show up on the right axis.
    ax.plot(x_data, y_predicted_1, color="green")
    ax.set_title('Best Parabola & Line Fit', fontsize=16)
    
    # Need to set the legend on the axis to get things to show up correctly,
    # even when setting label=''values' during plots, we need to set the label strings here.
    ax.legend(['Parabola Fit', 'Line Fit', 'Actual'], loc='lower right')

```
```{tab-item} Comments
Comments go here.
```
````

## Curve Fit
````{tab-set}
```{tab-item} Sinusoidal
![regplot](../_static/bestfit_curve_two.png)
```
```{tab-item} Best Fit
![regplot](../_static/bestfit_curve_fit.png)
```
```{tab-item} Code
```python
def function():
    pass
```
```{tab-item} Comments
Comments go here.
```
````

# ML regressions
https://realpython.com/linear-regression-in-python/
https://datagy.io/mean-squared-error-python/
`model = LinearRegression()`
Students will often pursue a Machine Learning model to do predictions which it is great at doing. 
ML models are intended to do predictions.
