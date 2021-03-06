---
title: mysql example scorpio common interface httpUtils httpUtil (snippet)
date: 2020-03-03
tags: ["python"]
---
Python mysql example 'scorpio common interface httpUtils httpUtil'

Functions in program: 
* `def do_request(items: RequestItems):`
* `def __ignore_urllib3_warning():`
* `def __verify_cas():`

Modules used in program: 
* `import requests`

## python scorpio common interface httpUtils httpUtil

Python mysql example: scorpio common interface httpUtils httpUtil

```python
import requests
from config.env_interface import *
from common.interface.httpUtils.httpMethod import HttpMethod
from common.interface.jsonCompare.compare import *


class RequestItems(object):
    def __init__(self, url: str, method: HttpMethod, data=None, request_json=None, **kwargs):
        self.url = url
        self.method = method
        self.data = data
        self.json = request_json  # type: dict
        self.kwargs = kwargs

    def __str__(self):
        return "RequestItems: [url:%s, method:%s, data:%s, json:%s, kwargs:%s]" % \
               (self.url, self.method, self.data, json_format(self.json), self.kwargs)


class ResponseItems(object):
    def __init__(self, response: requests.Response):
        self.url = response.url
        self.status = response.status_code
        self.log = BaseLog(ResponseItems.__name__).log
        try:
            self.json = response.json()
        except json.decoder.JSONDecodeError as e:
            self.log.error("json.decoder.JSONDecodeError: %s" % e)
            self.json = response.text

    def __str__(self):
        return "ResponseItems: [url:%s, status:%d, json:%s]" % \
               (self.url, self.status, json_format(self.json))


def __verify_cas():
    session = requests.session()
    session.get(CUR_ENV[CAS], verify=False)
    return session


def __ignore_urllib3_warning():
    import urllib3
    urllib3.disable_warnings()


def do_request(items: RequestItems):
    # 忽略 warning
    if http_variable[IGNORE_WARN]:
        __ignore_urllib3_warning()

    session = requests.session()

    # cas 认证
    if env_variable[CAS]:
        session = __verify_cas()

    try:
        methods = {
            HttpMethod.GET:
                session.get(items.url, **items.kwargs),
            HttpMethod.POST:
                session.post(items.url, items.data, items.json, **items.kwargs),
            HttpMethod.PUT:
                session.put(items.url, items.data, **items.kwargs),
            HttpMethod.DELETE:
                session.delete(items.url, **items.kwargs)
        }
        response = methods[items.method]
        res_items = ResponseItems(response)
    finally:
        session.close()
    return res_items


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
