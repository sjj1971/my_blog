---
title: "SQLAlchemy Note"
date: 2020-05-12 15:00:00
categories: programming
---
## How to use SQLalchemy to query sql database
```python
from sqlalchemy import create_engine
database_path = "../Resources/Census_Data.sqlite"
engine = create_engine(f"sqlite:///{database_path}")
data = engine.execute("select * from Census_Data").fetchall()
```
## How to use SQLalchemy to query postgres database in pandas
```python
from sqlalchemy import create_engine
database_url = "postgresql://username:password@localhost:5432/EmployeeSQL"
engine = create_engine(database_url)
connection = engine.connect()
employees_df = pd.read_sql("select * from employees, connection)
```

## How to make SQL Data Base using SQLalchemy (defin Class and Table)
#### 1. Load SQLalchemy package
```python
# Imports the method used for connecting to DBs
from sqlalchemy import create_engine

# Imports the methods needed to abstract classes into tables
from sqlalchemy.ext.declarative import declarative_base

# Allow us to declare column types
from sqlalchemy import Column, Integer, String, Float

# Sets an object to utilize the default declarative base in SQL Alchemy
Base = declarative_base()
```
#### 2. Create Classes which will serve as the anchor points for our tables.
```python
# Here, "BaseballPlayer" is class name and "player" is table name. 
class BaseballPlayer(Base):
    __tablename__ = "player"
    player_id = Column(String, primary_key=True)
    birth_year = Column(Integer)
    birth_month = Column(Integer)
    birth_day = Column(Integer)
    birth_country = Column(String)
    birth_state = Column(String)
 
# Create a Specific Instance of the classes
player1 = BaseballPlayer("birth_year" = "...", ...)
 ```

#### 3. Create Database Connection & create sql file
```python
data_path = "../Resources/database.sqlite"
engine = create_engine('sqlite:///{data_path}')
conn = engine.connect()

# Create metadata layer that abstracts our SQL database
Base.metadata.create_all(engine)
# When clear out the db : Base.metadata.drop_all(engine)
```

#### 4. Create a session object to connect to DB
```python
from sqlalchemy.orm import Session
session = Session(bind=engine)
```

#### 5. Add record to the DB
```python
# add record
session.add(Baseballplayer(birth_year = "...", birth_month = "...", ...)
# check if there is any update to commit and commit
session.new
session.commit
```

#### 6. Query the table
```python
session.query(Dog.column).all()
#We can using iteration
data = session.query(Dog)
for i in data:
    print(i)
```

## Several method for query using SQLalchemy
```python
session.query(Class_name).filter(Class_name.columns == "XXX"){.count(), .all(), sum()}
# If want to update data
data = session.query(Class_name).filter_by(column_name = "XXX:).first()
data.column_name2 = XXX
```
```python
# check metadata of the table
Base.metadata.tables
```
## Reference : 
1. Introduction to SQLAlchemy : https://www.youtube.com/watch?v=woKYyhLCcnU
2. Essential SQLAlchemy Book : http://shop.oreilly.com/product/0636920035800.do
3. SQLAlchemy: https://pynash.org/2013/02/15/using-sqlalchemy-func-and-group/

