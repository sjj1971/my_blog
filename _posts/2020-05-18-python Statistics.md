---
title: "Statistics with python Note - part1"
date: 2020-05-18 15:00:00
categories: programming
---

## Quartile calculations, temperatures is series or list.
```python
quartiles = temperatures.quantile([.25,.5,.75])
lowerq = quartiles[0.25]
upperq = quartiles[0.75]
iqr = upperq-lowerq
lower_bound = lowerq - (1.5*iqr)
upper_bound = upperq + (1.5*iqr)
plt.boxplot(temperatures)
```
## Sampling
```python
sample = pd_dataframe.samle(N)
```
```python
# normal continuous random variables, loc=position of mean, 
sample=stats.norm.rvs(loc=loc, size=200, random_state=42)
```
## SEM with errorbar (The SEM is a measure of precision for an estimated population mean.)
```python
sample_data = pd_dataframe.sample(N)
sample_set = [pd_dataframe.sample(N) for x in range(10)]
means = [sample_column.mean() for sample in sample_set]
standard_errors = [sem(sample_column) for sample in sample_set]
x_axis=np.aragne(0,len(sample_set),1)+1
fig, ax = plt.subplots()
ax.errorbar(x_axis, means, standard_errors, fmt="o")
```
## Correlation and linear regression
```python
import scipy.stats as st
import numpy as np
# Pearson Correlation
correlation=st.pearsonr(x_values, y_values)
#linear regression
(slope, intercept, rvalue, pvalue, stderr) = st.linregress(x_values, y_values)
regress_values = x_values * slope + intercept
line_eq = f"y={slope}*x+{intercept}"
plt.scatter(x_values, y_values)
plt.plot(x_values, regress_values, "r-")
plt.annotate(line_eq, (x,y), fontsize=15, color="red")
```
## 1sample T-test
```python
# assmuption : data is normally distributed, independent and randomly sampled.
stats.ttest_1samp(sample, data.mean())
#compare sample data, if pvalue is greater than 0.05, sample and data is not different in mean.
```
## ANOVA test (one-way ANOVA, NULL: 2 or more has same population mean)
```python
# ANOVA is to check whether any of the group element is significantly different than the rest.
stats.f_oneway(group1, group2, group3, group4, group5)
```
## Chi square (Null: categorical data has the given frequencies)
```python
# degree of freadom = #groups - 1, q is confidence level(1 - pvalue)
critical_value = st.chi2.ppf(q=0.95, df=degreeoffreedom)
st.chisquare(observed, expected)
# if the result is greater than critical value, result are statistically significant.
# It means, the observed values are statistically different from expected values.
```
### Reference
*args **kwargs : https://book.pythontips.com/en/latest/args_and_kwargs.html

