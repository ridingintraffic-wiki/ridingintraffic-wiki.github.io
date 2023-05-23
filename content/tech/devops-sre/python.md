---
title: "python snippets"
date: 2023-05-23
categories: [ devops-sre ]
---
## sometimes you just need to remember how to do a thing in python

### base64 uaer auth in requests  
use the base64 for the first header and then reuse the bearer token that you get back.
``` 
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

