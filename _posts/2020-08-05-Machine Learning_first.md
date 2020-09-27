---
title: "Machine Learning - part1"
date: 2020-08-05 15:00:00
categories: programming
---
### making data samples
```python
from sklearn.datasets import make_regression
X,y = make_regression(n_samples=20, n_features=1, random_state=0, noise=4, bias=100.0)
plt.scatter(X,y)
```
```python
from sklearn.datasets import make_s_curve
data, color = make_s_curver(100,random_state=0)
plt.scatter(data[:,0],color)
```
### Assign data to X and y
```python
X= data_frame.column1.values.reshape(-1,1)
y = data_frame.column2.values.reshape(-1,1)
```
### Testing and Training Data
```pythonX
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y, random_state=42)
```
### analyze linear regression (y = x* model_coef_ + model.intercept_)
```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X_train,y_train)
print('Weight Coefficients:', model.coef_)
print('y-axis intercept:', model.intercept_)
predictions = model.predict(X_test)
mse=mean_squared_error(y_test,predictions)
r2=r2_score(y_test,predictions)
model.score(X_test, y_test)
```
### plot the residual for training and testing data
```python
plt.scatter(model.predict(X_train), model.predict(X_train)-y_train, c="blue", label="Training Data")
plt.scatter(model.predict(X_test), model.predict(X_test)-y_test, c="red", label="Test Data")
plt.legend()
plt.hlines(y=0, xmin=y.min(), xmax=y.max())
plt.title("Residual Plot")
```
### Multiple Linear Regression (Y_i = Bias_0 + Weight_1* Feature_1 + Weight_2 * Feature_2 + ... + Weight_p * Feature_p)
```python
from sklearn.datasets import make_regression
n_features = 3
X,y = make_regression(n_samples = 30, n_features = n_features, n_informative = n_features, random_state = 42, noise=0.5, bias = 100.0)
```
```python
foam=pd.read_csv("path")
X=foam[["col1","col2"]]
y=foam["col3"].values.reshape(-1,1)
```
