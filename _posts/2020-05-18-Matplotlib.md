---
title: "Matplotlib Note - part1"
date: 2020-05-18 14:00:00
categories: programming
---
# Mathplot Figure

```python
import numpy as np
import matplotlib.pyplot as plt
plt.figure(figsize=(20,3))
plt.plot(x_axis_list, y_axis_list, color="r", linewidth=0.4, marker="-", label="label")
plt.xlabel("X Axis")
plt.ylabel("Y Axis")
# Draw a horizontal line with 0.25 transparency. linestyles : {'solid', 'dashed', 'dashdot', 'dotted'}, optional
plt.hlines(y, xmin, xmax, alpha=0.25, color="red", linestyles="line", label='horizontal')
#set x and y limits
plt.xlim(0,10)
plt.ylim(-1,1)
#set a grid on the plot
plt.grid()
plt.legend(loc="lower right", rotation=90)
plt.title("Title")
plt.savefix("../Images/plot.png")
plt.show()
```
## Tick
```python
tick_locations=[value for value in x_axis]
plt.xticks(tick_locations, [l_0,..., l_n], rotation="vertical")
```
## Bar chart
```python
plt.bar(x_axis, y_axis, color="r", alpha = 0.5, align="center")
```
## Pie chart, explode=separate sections from others,
```python
plt.pie(value_list, explode=(,,,,), labels=[,,,,], colors=['r',,,,], autopct"%1.1f%%", shadow=True, startangle=90))
plt.axis("equal")
```
## Scatter plot, s:size of each point
```python
plt.scatter(x_axis, data, marker='o', facecolors='red', edgecolors='black', s=x_axis, alpha=0.75)
```
## Pandas plot
```python
pd_dataframe.plot(kind=" ", figsize=(20,3))
```

## Plot histogram on list or series
```python
plt.hist(list_date[])
```
## group chart
```python
%matplotlib notebook
import matplotlib.pyplot as plt
import pandas ad pd
```
```python
a, = plt.plot()
b, = plt.plot()
plt.legend(handles=[a,b], loc='best')
plt.show()
```
```python
a_df.plot(,,,label="")
b_bf.plot(,,,label="")
plt.legend()
plt.show()
```
```python
fig1, ax1 = plt.subplots()
ax1.set_title()
ax1.set_ylabel()
ax1.boxplot(list or series)
plt.show()
```
###reference
observablehq.com - Gallery : https://observablehq.com/@d3/gallery
