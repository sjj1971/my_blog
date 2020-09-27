---
title: "Chrome Driver - part1"
date: 2020-05-31 23:00:00
categories: programming
---

## Import splinter
```python
# initialization
from splinter import Browser
from bs4 import BeautifulSoup as bs
executable_path = {'executable_path':'chromedriver.exe'}
browser = Browser('chrome',**executable_path, headless=False)
url = "http://quotes.toscrape.com/"
browser.visit(url)
```
```python
# create a Beautiful Soup object
for x in range(1, 6):
    html = browser.html
    soup = BeautifulSoup(html, 'html.parser')
    quotes = soup.find_all('span', class_='text')
    for quote in quotes:
        print('page:', x, '-------------')
        print(quote.text)
    browser.links.find_by_partial_text('Next')
```
## Scraping with Pandas
```python
import pandas as pd
url = 'https://en.wikipedia.org/wiki/List_of_capitals_in_the_United_States'
tables = pd.read_html(url)
tables #tables is list of panda frame
df = tables[0]
```
```python
# DataFrames as HTML
html_table = df.to_html() #generating HTML tables from DataFrames
html_table.replace('\n','')
df.to_html('table.html') #or saving the table directly to a file
```
