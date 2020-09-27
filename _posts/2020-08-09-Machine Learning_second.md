---
title: "Machine Learning - part2"
date: 2020-08-09 10:00:00
categories: programming
---
### Data Cleaning and Preprocessing
```python
import warnings
warnings.simplefilter('ignore')
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
```
```python
# read data set
brain=pd.read_csv(path)
X=brain[["gender","age","size"]]
y=brain["weight"].values.reshape(-1,1)
print(X.shape, y.shape)
```
```python
# handling categorical data Integer, One-hot, or Binary Encoding
# Binary Encoded Data (categorical data ==> vector)
data=X.copy()
data_binary_encoded = pd.get_dummies(data, columns=["gender"]) //for one column
data_binary_encoded = pd.get_dummies(data) //for multiple columns
```
```python
from sklearn.model_selection import train_test_split
X=pd.get_dummies(brain[["size","gender","age"]])
y=brain["weight"].values.reshape(-1,1)
X_train, X_test, y_train, y_test = train_test_split(X,y, random_state=42)
# scaling and normalization
from sklearn.preprocessing import StandardScaler
X_scaler=StandardScaler().fit(X_train)
y_scaler=StandardScaler().fit(y_train)
X_train_scaled=X_scaler.transform(X_train)
X_test_scaled=X_scaler.transform(X_test)
y_train_scaled=y_scaler.transform(y_train)
y_test_scaled=y_scaler.transform(y_test)
```
```python
# fit the model and plt the result
from sklearn.linear_model import LinearRegression
model=LinearRegression
model.fit(X_train_scaled,y_train_scaled)
plt.scatter(model.predict(X_train_scaled), model.predict(X_train_scaled) - y_train_scaled, c="blue", label="Training Data")
plt.scatter(model.predict(X_test_scaled), model.predict(X_test_scaled) - y_test_scaled, c="orange", label="Testing Data")
plt.legend()
plt.hlines(y=0, xmin=y_test_scaled.min(), xmax=y_test_scaled.max())
plt.title("Residual Plot")
plt.show()
```
```python
from sklearn.metrics import mean_squared_error
predictions=model.predict(X_test_scaled)
MSE=mean_squared_error(y_test_scaled,predictions)
r2=model.score(X_test_scaled,y_test_scaled)
print(f"MSE: {MSE}, R2: {r2}")
```
### Label Encoding
```python
from sklearn.preprocessing import LabelEncoder
label_encoder=LabelEncoder()
data=X.copy()
label_encoder.fit(data["gender"])
label_encoder.classes_ //array['Female','Male'],dtype=object)
label_encoder.transform(data.gender)
```
### MinMaxScaler
```python
from sklearn.preprocessing import MinMaxScaler
X_minmax = MinMaxScaler().fit(X_train)
y_minmax=MinMaxScaler().fit(y_train)

X_train_minmax = X_minmax.transform(X_train)
y_train_minmax = y_minmax.transform(y_train)
X_test_minmax = X_minmax.transform(X_test)
y_test_minmax = y_minmax.transform(y_test)
```
### plotting original and scaled
```python
fig1 = plt.figure(figsize=(12, 6))
axes1 = fig1.add_subplot(1, 2, 1)
axes2 = fig1.add_subplot(1, 2, 2)

axes1.set_title("Original Data")
axes2.set_title("Min Max Scaled Data")

maxx = X_train["size"].max()
maxy = y_train.max()
axes1.set_xlim(-maxx + 1, maxx + 1)
axes1.set_ylim(-maxy + 1, maxy + 1)

axes2.set_xlim(-1, 1)
axes2.set_ylim(-1, 1)

def set_axes(ax):
    ax.spines['left'].set_position('center')
    ax.spines['right'].set_color('none')
    ax.spines['bottom'].set_position('center')
    ax.spines['top'].set_color('none')
    ax.xaxis.set_ticks_position('bottom')
    ax.yaxis.set_ticks_position('left')
    
set_axes(axes1)
set_axes(axes2)

axes1.scatter(X_train["size"], y_train)
axes2.scatter(X_train_minmax[:,0], y_train_minmax[:])
```
### LASSO model
```python
from sklearn.linear_model import Lasso
lasso=Lasso(alpha=0.1).fit(X_train_scaled,y_train_scaled)
predictions=lasso.predict(X_test_scaled)
r2=lasso.score(X_test_scaled,y_test_scaled)
```
### Ridge model
```python
from sklearn.linear_model import Ridge
ridge=Ridge(alpha=0.1).fit(X_train_scaled,y_train_scaled)
predictions=ridge.predict(X_test_scaled)
r2=ridge.score(X_test_scaled,y_test_scaled)
```
### ElasticNet model
```python
from sklearn.linear_model import ElasticNet
elasticnet=ElasticNet(alpha=0.1).fit(X_train_scaled,y_train_scaled)
predictions=elasticnet.predict(X_test_scaled)
r2=elasticnet.score(X_test_scaled,y_test_scaled)
```
