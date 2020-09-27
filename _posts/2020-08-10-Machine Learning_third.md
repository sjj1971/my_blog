---
title: "Machine Learning - part3"
date: 2020-08-10 12:00:00
categories: programming
---
### Logistic Regression (yes or no) with activation function
```python
from sklearn.datasets import make_blobs
X,y = make_blobs(center=2, random_state=42, cluster_std=1)
plt.scatter(X[:,0],X[:,1],c=y)
```
```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y)
from sklearn.linear_model import LogisticRegression
classifier = LogisticRegression()
classifier.fit(X_train, y_train)
classifier.score(X_train, y_train)
classifier.score(X_test, y_test)
new_data = np.array([[-2,6]]) //generate a new data
predictions = classifier.predict(new_data)
predictions = classifier.predict(X_test)
```
```python
# read data set
voice=pd.read_csv(os.path.join('..','Resource','voice.csv')
X=voice.drop("label",axis=1)
y=voice["label"]
for num_iter in [50, 100, 200, 500, 1000]:
    for pen in ['none','l2']:
        print(num_iter, pen)
        X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=1)
        classifier = LogisticRegression(penalty=pen, max_iter=num_iter)
        classifier.fit(X_train, y_train)
        print(f"Training Data Score: {classifier.score(X_train, y_train)}")
        print(f"Testing Data Score: {classifier.score(X_test, y_test)}")
        // find good iteration and penalty options
predictions = classifier.predict(X_test)
print(f"First 10 Predictions:   {predictions[:10]}")
print(f"First 10 Actual labels: {y_test[:10].tolist()}")
```
### Decision Tree Classifier
```python
from sklearn import tree
clf = tree.DecisionTreeClassifier()
clf.fit(X_train, y_train)
```
### Random Forests
```python
from sklearn.ensemble import RandomForestClassifier
rf = RandomForestClassifier(n_estimators=50, max_depth=2)
rf.fit(trainingData, trainingScores)
importances=rf.feature_importances_
importances
sorted(zip(rf.feature_importances_, iris.feature_names),reverse=True)
```
### KNeighborsClassifier
```python
from sklearn.neighbors import KNeighborsClassifier
//Loop through different k values to see which has the highest accuracy
//Note: We only use odd numbers because we don't want any ties
train_scores = []
test_scores = []
for k in range(1, 20, 2):
    knn = KNeighborsClassifier(n_neighbors=k)
    knn.fit(X_train, y_train)
    train_score = knn.score(X_train, y_train)
    test_score = knn.score(X_test, y_test)
    train_scores.append(train_score)
    test_scores.append(test_score)
    print(f"k: {k}, Train/Test Score: {train_score:.3f}/{test_score:.3f}")
plt.plot(range(1, 20, 2), train_scores, marker='o')
plt.plot(range(1, 20, 2), test_scores, marker="x")
plt.xlabel("k neighbors")
plt.ylabel("Testing accuracy Score")
plt.show()
```
```python
# Note that k: 9 provides the best accuracy where the classifier starts to stablize
knn = KNeighborsClassifier(n_neighbors=9)
knn.fit(X_train, y_train)
print('k=9 Test Acc: %.3f' % knn.score(X_test, y_test))
```
https://scikit-learn.org/stable/auto_examples/neighbors/plot_nca_classification.html
### Support Vector Machine (kernel : linear, nonlinear, polynomial, RBF(radial basis function), sigmoid,
```python
from sklearn.svm import SVC
model = SVC(kernel='linear)
model = SVC(kernel='poly',C=2.2, degree=10)
model.fit(X,y)
```
```python
// plot the decision boundaries
x_min = X[:,0].min()
x_max = X[:,0].max()
y_min = X[:,1].min()
y_max = X[:,1].max()
XX, YY = np.mgrid[x_min:x_max, y_min:y_max]
Z=model.decision_function(np.c_[XX.ravel(), YY.ravel()])
Z=Z.reshape(XX.shape)
plt.contour(XX, YY, Z, colors=['k', 'k', 'k'],
            linestyles=['--', '-', '--'], levels=[-.5, 0, .5])
plt.scatter(X[:, 0], X[:, 1], c=y, cmap='bwr', edgecolor='k', s=100)
plt.show()
```
```python
from sklearn.metrics import classification_report
predictions = model.predict(X_test)
print(classification_report(y_test,predictions,target_names = ["negative", "positive"])
```
https://scikit-learn.org/stable/modules/svm.html
### LinearDiscriminant
```python
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
clf = LinearDiscriminantAnalysis()
clf.fit(trainingData, trainingScores)
```
### GaussianNB
```python
from sklearn.naive_bayes import GaussianNB
clf = GaussianNB()
clf.fit(trainingData, trainingScores)
```
### Grid Search
```python
from sklearn.model_selection import GridSearchCV
param_grid = {'C':[1,5,10,50],'gamma':[0.0001,0.0005,0.001,0.005]}
grid = GridSearchCV(model,param_grid,verbose=3)
grid.fit(X_train,y_train)
print(grid.best_params_)
print(grid.best_score_)
predictions = grid.predict(X_test)
from sklearn.metrics import classification_report
print(classifictaion_report(y_test, predictions, target_names = ['blue','red']))
```
https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html
