# Feature Importance 

**Feature importance** is a concept in machine learning (ML) that helps us understand and quantify the impact of different **features** on the predictions made by a model. It allows us to identify which features are more influential in contributing to the model's performance and predictions. 

There are several techniques to measure feature importance. This unit will go over a few of these techniques.
#### Coefficient Magnitudes (Linear Models)
In linear regression and other linear models, the magnitude of the coefficients assigned to each feature gives an indication of its importance. Larger absolute coefficients imply stronger impact on the output variable.

````{tab-set}

```{tab-item} Code
```python
# Split the data into training and testing sets
train_f, test_f, train_l, test_l = train_test_split(features, labels, test_size=0.2)

# Initialize the Linear Regression model
model = LinearRegression()

# Fit the model to the training data
model.fit(train_f, train_l)

# Get the coefficients and feature names
coefficients = model.coef_
feature_names = data.feature_names

# Print the coefficients and feature names
feature_coef = zip(feature_names, coefficients)
for f, c in feature_coef:
    print(f + ": " + c);

```
```{tab-item} Comments
The following is how to interpret coefficient magnitudes for feature importance:

**Coefficient Magnitude:** The magnitude of the coefficient reflects the strength and direction of its influence on the target variable. A larger coefficient magnitude (positive or negative) indicates that the feature has a greater influence.

1. A positive coefficient suggests that an increase in the value of the feature will result in an increase in the model's output. This signifies that the feature has a positive linear connection with the target variable.

2. A negative coefficient indicates that an increase in the value of the feature will result in a decrease in the model's output. This shows a negative linear relationship between the feature and the label.

**Magnitude Comparison:** By comparing the magnitudes of coefficients across different features, you can rank features based on their relative importance. Features with larger absolute coefficients are generally considered more important in influencing the model's predictions.
```
````
#### Permutation Importance
This is a technique used to measure the importance of features in a model by evaluating how much the model's performance drops when the values of a specific feature are randomly shuffled. The idea is that important features contribute significantly to the model's prediction, so shuffling their values would lead to drop in performance.
````{tab-set}
```{tab-item} Goal
1. Train a model and record its performance on the original set
2. Randomly shuffle the values of a single feature in the set
3. Calculate the performance again using the shuffled data
4. Compare the drop in performance to the original performance. **A larger drop indicates that the shuffled feature is important.**
```
```{tab-item} Code
```python
print("loading...")
```
````






