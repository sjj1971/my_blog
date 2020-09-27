---
title: "Python API - part2"
date: 2020-06-10 15:30:00
categories: programming
---
### NYT API
```python
import requests
import json
url = "https://api.nytimes.com/svc/search/v2/articlesearch.json?"
query="granola"
query_url = url + "api-key=" + api_key + "&q=" + query
# when query with begin&end_date and query multiple page
# query_url = f"{url}api-key={api_key}&q={query}&begin_date={begin_date}&end_date={end_date}"
# query_url = f"{query_url}&page={str(page)}"
articles = requests.get(query_url).json()
```
### Open Weather API
```python
import json
import requests
from config import api_key
url = "http://api.openweathermap.org/data/2.5/weather?"
query_url = f"{url}appid={api_key}&units={units}&q="
query_url=
city = "Portland"
query_url = url + "appid=" + api_key + "&q=" + city
weather_response=requests.get(query_url)
weather_json = weather_response.json()

response = requests.get(url).json()
print(json.dumps(response, indent=4, sort_keys=True))
#check datatype of response and keys if dictionary
```
```python
# build url address
base_url = "http://numbersapi.com/"
url = base_url + "/" + input_data.lower() + "?json"
```
```python
# using API keys (with OMDBapi case)
import requests
import json
from config import api_key #config.py is a file including api_key
url = base_url + "?t=" + search_keyword + "&apikey=" + api_key
# pretty print
from pprint import pprint
pprint(requests.get(url).json())
```
### google place API
