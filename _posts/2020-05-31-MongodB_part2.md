---
title: "MongoDB - part2"
date: 2020-05-31 15:00:00
categories: programming
---

## PyMongo
```python
# initialization
import pymongo
conn="mongodb://localhost:27017"
client=pymongo.MongoClient(conn)
```
```python
# define 'classDB" database and collection 'classroom'
db= client.classDB
classroom = db.classroom.find()
```
```python
#insert a document into the classroom collection
db.classroom.insert_one({})
db.classroom.insert_many([{},...])
#update a document
db.classroom.update_one({},{'$set':{}})
db.classroom.update_one({},{'$push':{}})
```
```python
#delete a field from a document
db.classroom.update_one({},{'$unset':{'row':""}})
#delete a document
db.classroom.delete_one({})
```
