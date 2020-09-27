---
title: "Big Data - part1"
date: 2020-08-11 09:00:00
categories: programming
---
### Map Reduce
```python
from mrjob.job import MRJob
class Bacon_count(MRJob):
   def mapper(self, _, line):
       for word in line.split():
           if word.lower() == "bacon":
               yield "bacon",1
   def reducer (self, key, values):
       yield key, sum(values)
if __name__ == "__main__":
    Bacon_count.run()
    
// running code : python app.py input.txt
```
```python
// find number of hot days in Austin for 2017
from mrjob.job import MRJob
class Hot_days(MRJob):
    def mapper(self, key, line):
       (station, name, state, date, snow, tmax, tmin) = line.split(",")
       if tmax and int(tmax) >= 100:
           yield name, 1
    def reducer(self, name, hot):
       yield name, sum(hot)
if __name__ == "__main__":
    Hot_days.run()
```
https://mrjob.readthedocs.io/en/latest/guides/writing-mrjobs.html
