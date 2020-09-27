---
title: "Python API - part1"
date: 2020-06-10 14:00:00
categories: programming
---
```python
import requests
import json
url = "https://api.spacexdata.com/v2/launchpads"
print(requests.get(url))
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
