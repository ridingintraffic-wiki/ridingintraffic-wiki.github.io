---
title: "python tricks"
date: 2023-04-27
categories: [ devops-sre ]
---

## Accessing Dictionaries
Getting dictionaries back from a http endpoint usually results in a mess of objects.   Dealing with this in python can be a challenge of `ValueError` exceptions.   so what is the easiest  way to handle this?    a nested get.   if the object looks like  
```
message={"detail":{"operation":"create"}}
```
then you can access it like this 
```
>>> message.get('detail', {}).get('operation')
create
```
then if you access something that doesn't exist   you will get a nice `None` back 
```
>>> print(message.get('detail', {}).get('notoperation'))
None
```
hurray safe handling hey

## base64 user auth in requests  
use the base64 for the first header and then reuse the bearer token that you get back.
``` 
import requests
import json
from requests.auth import HTTPBasicAuth

    headers = {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    }
    
    base_url = 'https://www.something.com'
    token_url = "/tauth/1.0/token/"
    url=base_url + token_url
    response = requests.post(url, headers=headers, auth=HTTPBasicAuth(USER, PASSWORD))
    data = response.json()
    
    #reusing that bearer token from the repsonse
    headers = {
        'Authorization': f"Bearer {data['token']}",
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    }
    url="/something/"
    response=requests.get( url, headers=headers)
    data = response.json()

```
