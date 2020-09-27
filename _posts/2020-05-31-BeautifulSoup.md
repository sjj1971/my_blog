---
title: "BeautifulSoup - part1"
date: 2020-05-31 16:00:00
categories: programming
---

## Intro to Soup
```python
# initialization
from bs4 import BeautifulSoup as bs
import requests
import pymongo
conn="mongodb://localhost:27017"
client=pymongo.MongoClient(conn)
url = "https://newjersey.craigslist.org/search/sss?sort=rel&query=quitar'
```
```python
# create a Beautiful Soup object
response = request.get(url)
soup = bs(response.text, 'html.parser')
print(soup.prettify())
```
```python
#extract the title of the HTML document
soup.title
#extract the text of the title.
soup.title.text
#clean up the text
soup.title.text.strip()
```
```python
#extract text of the first paragraph
soup.body.p.text
soup.body.find('p')
#extract all paragraph elements in list format.
soup.body.find_all('p')
```
```python
#extract text of specific tag and class.
results = soup.find_all('li',class='result-row')
for result in results:
   try:
      title=result.find('a',class='result-title').text
      price=result.a.span.text
      link=result.a['href']
   except AttributeError as e:
      print(e)
```
```python
#extract text of specific tag and class.
db= client.craigslist_db
collection=db.items
results = soup.find_all('li',class='result-row')
for result in results:
   try:
      title=result.find('a',class='result-title').text
      price=result.a.span.text
      link=result.a['href']
      post = {
         'title':title,
         'price':price,
         'url':link
      }
      collection.insert_one(post)
   except AttributeError as e:
      print(e)
listings=db.items.find()
for listing in listings:
   print(listing)
```
###Web Scraping with BeautifulSoup : https://www.dataquest.io/blog/web-scraping-tutorial-python/
