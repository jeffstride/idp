# Feature Importance 

**Feature importance** is a concept in machine learning (ML) that helps us understand and quantify the impact of different input variables (features) on the predictions made by a model. It allows us to identify which features are more influential in contributing to the model's performance and predictions. 

There are several techniques to measure feature importance. This unit will go over a few of these techniques.
#### Coefficient Magnitudes (Linear Models)
In linear regression and other linear models, the magnitude of the coefficients assigned to each feature gives an indication of its importance. Larger absolute coefficients imply stronger impact on the output variable.

````{tab-set}

```{tab-item} Code
```python
# Split the data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Initialize the Linear Regression model
model = LinearRegression()

# Fit the model to the training data
model.fit(X_train, y_train)

# Get the coefficients and feature names
coefficients = model.coef_
feature_names = data.feature_names

# Print the coefficients and feature names
for feature, coef in zip(feature_names, coefficients):
    print(f"{feature}: {coef:.4f}")

# Plot the coefficient magnitudes
plt.figure(figsize=(10, 6))
plt.barh(range(len(feature_names)), coefficients)
plt.yticks(range(len(feature_names)), feature_names)
plt.xlabel('Coefficient Magnitude')
plt.ylabel('Feature')
plt.title('Coefficient Magnitudes for Feature Importance')
plt.show()
```
```{tab-item} Comments
Here's how you can interpret coefficient magnitudes for feature importance:

Magnitude of Coefficient: The magnitude of the coefficient for a particular feature indicates the strength and direction of its impact on the target variable. A larger coefficient magnitude (positive or negative) implies a greater influence of that feature on the target variable.

Positive Coefficient: A positive coefficient indicates that an increase in the feature's value will lead to an increase in the predicted output. In the context of linear regression, this means that the feature has a positive linear relationship with the target variable.

Negative Coefficient: A negative coefficient implies that an increase in the feature's value will lead to a decrease in the predicted output. In the context of linear regression, this suggests a negative linear relationship between the feature and the target variable.

Magnitude Comparison: By comparing the magnitudes of coefficients across different features, you can rank features based on their relative importance. Features with larger absolute coefficients are generally considered more important in influencing the model's predictions.
```
````

#### Decision Trees 


#### Permutation Importance


#### Correlation Analysis


