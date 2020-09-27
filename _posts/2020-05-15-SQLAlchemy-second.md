---
title: "SQLAlchemy Note - part2"
date: 2020-05-15 15:00:00
categories: programming
---
## Reflection using SQLalchemy
```python
# reflection is to reflect the database tables to Base class
import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine
engine = create_engine("sqlite:///../Resources/dow.sqlite")
# Declare a Base using `automap_base()`
Base = automap_base()
# Use the Base class to reflect the database tables
Base.prepare(engine, reflect=True)
# check class using base
Base.classes.keys()
# Assign the dow class to a variable called `Dow`
Dow = Base.classes.dow
# Create a session
session = Session(engine)
# Display the row's columns and data in dictionary format
first_row = session.query(Dow).first()
first_row.__dict__
# Use the session to query Dow table and display the first 5 trade volumes
for row in session.query(Dow.column_1, Dow.column_2).limit(15).all():
    print(row)
```

## Inspector
```python
# Import SQLAlchemy `automap` and other dependencies
import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine, inspect
# Create the connection engine
engine = create_engine("sqlite:///../Resources/dow.sqlite")
# Create the inspector and connect it to the engine
inspector = inspect(engine)
# Collect the names of tables within the database
inspector.get_table_names()
# Using the inspector to print the column names within the 'dow' table and its types
columns = inspector.get_columns('dow')
for column in columns:
    print(column["name"], column["type"])
```

## Additional method to use aggregation function query using SQLAlchemy
```python
# The format of instruction for aggregation using SQLAlchemy is similar to one of SQL.
from sqlalchemy import func
session.query(Dow.id, func.avg(Dow.column_1).filter(column == value).group_by(Dow.id).all()
```
```python
# using label
from sqlalchemy import func
from sqlalchemy.sql import label
results = session.query(User.group,
          label('members', func.count(User.id)),
          label('total_balance', func.sum(User.balance))).group_by(User.group).all()
for result in results:
    print(f"{result.group}, {result.members}, {result.total_balance}")
```
