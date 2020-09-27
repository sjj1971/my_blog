---
title: "Pandas - part 1"
date: 2020-06-13 01:00:00
categories: programming
---
### Panda Cut (bin)
```python
# Create the bins in which Data will be held
# Bins are 0, 59.9, 69.9, 79.9, 89.9, 100.   
bins = [0, 59.9, 69.9, 79.9, 89.9, 100]
group_names = ["F", "D", "C", "B", "A"]
df["Test Score Summary"] = pd.cut(df["Test Score"], bins, labels=group_names, include_lowest=True)
```
