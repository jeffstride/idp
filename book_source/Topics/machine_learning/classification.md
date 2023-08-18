# Classification
This page will do create a Machine Learning Classification model. We create and use contrived data where
and then attempt to predict whether someone is in the NBA or not.  

## Summary
In this study, we create the data which means that we absolutely know things about the
data. The ML model is used to reverse engineer the characteristics that we built in. Since
we know the _truth_ of the data, we can explore the _value_ of the ML model--its predictions and
statistics.  

For example, we know that **gender** makes a _genuine_ difference in the accuracy of the predictions. When we ask
our code to give us statistics (e.g. Accuracy, Feature Importance) we can interpret these
numbers with full understanding of "the truth" to know that **gender** is an important feature.  

In normal research, we do not know _the truth_ of the data. All we have are the results of the
ML model. We need to be able to accurately and fairly interpret the model so that value is added.  

In our studies here, students should learn:
* How to create and analyze a Classification model  
* Accuracy can be misleading in a multitude of ways  
* Calculating accuracy is not the stopping point of the research  
* That graphing a model's predictions reveals important information & insight  
* Feature Importance reflects how much a feature is used in making a model's decisions, but that does not mean the feature is, in practice, (un)important in a Fair & Ethical ML model.  
* With limited data, a model's accuracy may be _"wrong"_   
* Using a randomized test set won't always reveal that the model is overly complex or convoluted.  

## Data Overview
In this hypothetical example, we know the **height** and **gender** of about 2000 people who are between the ages of 22-32. We
also know whether they play in the NBA (or WNBA). Let's see if a `DecisionTreeClassifier` can accurately predict whether they
play in the NBA or not based soley on their gender and height.  Note that for simplicity, we will only consider male/female,
and we will often say just NBA when we also mean to include WNBA.  

We will break up our study into two primary sections. Each section uses completely contrived and made-up data. This
allows us to understand the model's results. In both cases, **height** impacts the results (playing for NBA), but
the specifics of how it impacts the results is different in each study.  

In our first dataset, the threashold for automatically being in the NBA is
81+ inches tall for a male, while a woman must be only 75+ inches tall.  

The two data types are:  
1) Predictable Data :  a person is in the NBA based entirely on their height.  
2) Ranomized Data : the taller a person is, the more likely they are in the NBA.

**Example Data**  
````{tab-set}
```{tab-item} Predictable
TODO: show right image here
![Predictable Data](../../_static/fi_nba_data.png)
```
```{tab-item} Randomized

![Randomized Data](../../_static/fi_nba_data.png)
```
````
## The code
There are several parameterized methods used to create the data, models and graphs. Seeing the code can help the
student understand the results as well as to reproduce similar studies.  

```{admonition} imports
:class: seealso dropdown
```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
from sklearn.tree import plot_tree
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import random
```

```{admonition} See Code
:class: seealso dropdown
```python
def in_nba(height, male, basis):
    '''
    Chances of being in NBA increase when one is taller than some cutoff.
    Normal and short people have a 'basis' chance.
    '''
    # pick the cutoffs based on the gender of the person
    cutoffs = [ [85, 82, 80], [76, 74, 72]][0 if male else 1]
    if height>cutoffs[0]:
        basis *= 60
    elif height>cutoffs[1]:
        basis *= 20
    elif height>cutoffs[2]:
        basis *= 10

    return random.random() < basis

def in_nba_by_height(height, male, ignored):
    return (male and height>=81) or (not male and height>=75)

def get_nba_data(size, basis, nba_method=in_nba):
    # This uses Numpy to create a normal distribution around some mean with 
    # some standard deviation. https://youtu.be/rzFX5NWojp0 
    # use Numpy concatenate to make a single list of values rounded to 1 decimal place
    men_height = np.random.normal(71, 5, size)
    women_height = np.random.normal(64, 5, size)
    height = np.concatenate([men_height, women_height])
    height = np.round(height, decimals=1)
    # Create a list of size having 'Male' as every value
    # use 'extend' to 'concatenate' another list to the end
    # if we used 'append' then only 1 element, a list, would get added
    genders = ['Male']*size
    genders.extend(['Female']*size)
    # Create the True/False values for being in the NBA based on height & gender
    nba = [ nba_method(h, g=='Male', basis) for h, g in zip(height, genders) ]
    df_sorted = pd.DataFrame(data={'gender':genders, 'height':height, 'nba':nba})
    # shuffle the dataframe rows so that we don't have all males at the top
    df_height = df_sorted.sample(frac=1).reset_index(drop=True)
    return df_height

def run_nba(randomized=False, size=1000, basis=0.005, keep_gender=True, max_depth=3):
    nba_method = in_nba if randomized else in_nba_by_height
    df_height = get_nba_data(size, basis, nba_method)

    labels = df_height['nba']
    # translate the 'gender' column, a string, to a boolean 'male' column
    df_height['male'] = df_height['gender'] == 'Male'
    # get our feature columns; honor our keep_gender argument
    features = df_height[['male', 'height'] if keep_gender else ['height']]

    model_nba = model_acc(features, labels, max_depth=max_depth)

    return model_nba, features, df_height

def plot_nba_predictions(model, actual=None, keep_gender=True):
    plt.clf()
    # create features to predict
    height = [ t for t in range(59, 88) ]
    genders = [False] * len(height)
    gender_m = [True] * len(height)
    genders.extend(gender_m)
    height.extend(height)
    features = pd.DataFrame(data={'male':genders, 'height':height})
    model_features = features if keep_gender else pd.DataFrame(data={'height':height})
    features['nba'] = model.predict(model_features)
    
    sns.scatterplot(x=features['height'], y=features['male'] , hue=features['nba'], 
                    legend='full', s=150)
    if actual is not None:
        colors = ['red', 'green']
        sns.scatterplot(x=df['height'], y = df['male'], hue=df['nba'], palette=colors, 
                        legend=False, s=10)

    plt.title('DecisionTreeClassifier\nPredicted NBA from Height & Gender')
    plt.yticks([0, 1])
    plt.ylim(-.5, 1.5)
    plt.ylabel('Is Male')

def plot_confusion_matrix(df, features, model, gender=0):
    # Update the title depending on whether features has 'male' as a column. 
    gender_for_title = ('Male' if gender==1 else 'Female')
    
    if 'male' in features.columns:
        gender_for_title += '\nGender Included in Prediction'
        feature_list = ['male', 'height']
    else:
        gender_for_title += '\nGender Ignored in Prediction'
        feature_list = ['height']
    
    # filter to a gender
    df_filtered = df[df['male'] == gender]
    features = df_filtered[feature_list]
    actual = df_filtered['nba']
    
    # get our predictions
    predicted = model.predict(features)
    # Calculate confusion matrix
    confusion = confusion_matrix(actual, predicted)
    
    # Calculate the rates of accuracy for each quadrant
    # get the counts
    tn, fp, fn, tp = confusion.ravel()
    # FNR (Equal opportunity): #fn / (actual positives)
    actual_positives = df_filtered['nba'].sum()
    fnr = np.NaN if actual_positives == 0 else fn / actual_positives
    # FPR (Predictive Equality): #fp / (actual negatives)
    actual_negatives = (len(df_filtered)-df_filtered['nba'].sum())
    fpr = np.NaN if actual_negatives == 0 else fp / actual_negatives
    print(f'Equal Opportunity (FNR): {fnr:.0%}')
    print(f'Predictive Equality (FPR): {fpr:.0%}')

    # Create a table for visualization
    data = {'Predicted True': [tp, fp],
            'Predicted False': [fn, tn]}

    table_df = pd.DataFrame(data, index=['Actual True', 'Actual False'])

    # Plot the table using Seaborn's heatmap
    plt.figure(figsize=(8, 4))
    sns.heatmap(table_df, annot=True, fmt="d", cmap="Blues") 
    ax = plt.gca()
    ax.annotate(f'Equal Opportunity (FNR): {fnr:.0%}', (1.0, .40), xytext=(25, 0), 
                textcoords='offset points', weight='bold')
    ax.annotate(f'Predictive Equality (FPR): {fpr:.0%}', (0.1, 1.30), xytext=(0, 0), 
                textcoords='offset points', weight='bold')
    plt.title('Counts for ' + gender_for_title)
```
## Data 1: Predictable Data Study
In this contrived dataset, we say that whether a person is in the NBA is completely determined
by their height. We use the `in_nba_by_height` method (in the **Code** dropdown above). We see
that the accuracy is very, very high--nearly 100%! This kind of makes sense because we've
generated the data in a way to be predictable.    

Belonging to the NBA in this _Predictable Data Study_ is very simple: if you're tall enough
for your gender, you're in! When we look at the _Feature Importance_ we see that **height** has
an importance of 60% while **gender** is ~40%. 

**Model Predictions Drawn**  
In this graph we see both how the actual data is distributed and how the predictions are made.
The predictions are shown with the larger, blue and organge dots. On top of predictions are
smaller, red and green dots that represent that actual data. It shows that the model does
a great job! The picture says a lot and you should find it useful in concluding that
the model is sound.  

![Simple Data Predictions](../../_static/fi_nba_not_random.png)  

So what? Where do we go from here?  

Let's present a few questions:  
* How important is **gender** in the predictions?  
* What does the 40% mean?  

We will explore this by removing **gender** from the set of features available to the
model when making its predictions. 

```{admonition} Make your prediction
:class: important
Take a minute to think and make some predictions about what will happen when we
remove **gender** from the feature set. 
```

```{admonition} An Aside
:class: note
When the percentage of actual women in WNBA drops to less than 1% (say, 2/500 women), then the _Feature Importance_
drops to just ~6%. **What does that say about Feature Importance?**  

Read on and hopefully it will all make sense.
```
### Gender Removed
Here are the results when **gender** is removed. I find the results fascinating! First off, the
accuracy of the model is 99.5%!! Where you expecting that?  

How in the world does the model predict with 99.5% accuracy when we ingore **gender** which has
a _Feature Importance_ of 40%?  

What we see in the graph is that the model doesn't predict NBA until one is 80 inches tall. In this
particular dataset, one woman happened to be that tall while 12 others in the WNBA were not that tall.  
![No Gender Model Results](../../_static/class_no_gender.png)    


#### Discussion   
We are left to reflect about the meaning of Accuracy when it completely clobbers
a segment of the population. Without knowing the error rates, the Accuracy number
alone loses significance.  

We must also question what the _Feature Importance_ really means. In this scenario
we can predict with nearly 100% accuracy who is in the NBA even when excluding a
feature with 40% importance.   

In this study, the count of people at various heights is random, and the training set randomly selected.
This leads to getting different numbers each time we run the code. The greatest variance was
in the _Feature Importance_ of **gender**. The accuracy was always very close to 100%.  

So, is gender an important feature to have in the model? The answer depends on whether you want
to be _Fair_ or not. If all you care about is overall accuracy, you could ignore **gender** which
simplifies your model. But, then, you're not fair! Let's examine Fairness more.

#### Fairness
First, you should know that fairness is covered in 
[Lesson 28](https://cse163.github.io/book/module-10-beyond-163/lesson-28-fairness/index.html). 
What is especially important is to know the definitions of fairness and how we can discuss
fairness scientifically once we define it.

Let's say that in our new model we choose to ignore **gender** because we've seen how
overall Accuracy is still very high. What happens?

We see that the model's predictions for men is still very good and it basically ignores
that women are shorter on average. This means that we have bad Fairness as measured by
Equal Opportunit: there are too many False Negatives and not enough (or any) True-Positives.

In other words, the True-Positive rate
(the ability to correctly identify WNBA players) for women is near 0%.
This is also called PPV (Positive Predictive Value) [Video Reference](https://youtu.be/QqgJHryKOSU)  

To be Fair, you want FNR and FPR to be relatively close across all the groups. If you look
a these two graphs, you'll see that FNR for Females is 92% while Males is at 0%!! This leads
us to conclude that the model is **NOT FAIR** when we exclude **gender** from the features.  

````{tab-set}
```{tab-item} Female
![Female Fairness](../../_static/class_female_fairness.png)
```
```{tab-item} Male
![Male Fairness](../../_static/class_male_fairness.png)  
```
````

#### Summary
_Feature Importance_ can be drawn as a pie chart. Each feature is given a percentage amount
that reflects how much that feature is used in the Decision Tree.  

_Feature Importance_ does **NOT** necessarily reflect how accurate the model will be.  

Plotting the model's predictions provides a lot of information.  

Calculating _Fairness_ values is important when evaluating a model.  

## Data 2: TODO: Randomized Data Study 
In this sub-study, we will create data that is more random. Surely not everyone who is very
tall is in the NBA; they are simply more likely to be in the NBA. 


**Model Predictions**  
![Simple Data Predictions](../../_static/fi_nba_not_random.png)

> **OUTPUT**  
> Accuracy: 99.83%  
> Feature: male, Importance: 5.60%  
> Feature: height, Importance: 94.40%  

This output is generated from the `model_acc` code in the prior tab. It is a bit
surprising to think that height is the utmost importance in the decision making.
We know from how we generated the data that females have a much lower height
threshold before their chances increase. We know that `gender` has an impact. Yet,
our **Feature Importance** says that gender has 0% importance.   

> **OUTPUT**  
> Feature: male, Importance: 0.00%  
> Feature: height, Importance: 100.00%


This graphic shows that our tree is relatively simple. It shows that it always looks at height,
and it predicts in the NBA in only 1 small case.
![NBA Model](../../_static/fi_model_nba.png)

