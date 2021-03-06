# INITIALIZATION

```python
import python_http_client

host = "https://api.sendgrid.com"
api_key = os.environ.get('SENDGRID_API_KEY')
request_headers = {
    "Authorization": 'Bearer {0}'.format(api_key)
}
version = 3
client = python_http_client.Client(
    host=host,
    request_headers=request_headers,
    version=version
)
```

# Table of Contents

* [CLIENT](#client)
* [RESPONSE](#response)

<a name="response"></a>
# RESPONSE

Response object holds the response or data from a return statement from a client API call. It has three main properties, status_code, headers and body, which can be retrieved via a simple call:

```python
print(response.status_code)
print(response.headers)
print(response.body)
```

<a name="client"></a>
# CLIENT
Client object that allows quick access a REST-like API. All methods return a Response object that can be treated with as explained in Response.

## GET
HTTP request to retrieve information from a source.

```python
response = client.api_keys.get()
```

```python
response = client.api_keys._(api_key_id).get()
```

## POST
HTTP request to send data to a source.

```python
data = {
    "name": "My API Key",
    "scopes": [
        "mail.send",
        "alerts.create",
        "alerts.read"
    ]
}
response = client.api_keys.post(request_body=data)
# print(response) as shown above
```

## PATCH
HTTP request to update partial resources in a source.

```python
data = {
    "name": "A New Hope"
}
response = client.api_keys._(api_key_id).patch(request_body=data)
# print(response) as shown above
```

## PUT
HTTP request used to replace a collection or element in a source.

```python
data = {
	"name": "The Empire Strikes Back",
	"scopes": [
		"user.profile.read",
		"user.profile.update"
	]
}
response = client.api_keys.put(request_body=data)
# print(response) as shown above
```

## DELETE
HTTP request to delete elements in a source.

```python
response = client.api_keys._(api_keys_id).delete()
# print(response) as shown above
```

## LOGGING
Logging namespace `python_http_client.client` is available on API Client.

Example to stdout:

```
>>> import logging
>>> import sys
>>> logger = logging.getLogger('python_http_client.client')
>>> logger.setLevel(logging.DEBUG)
>>> handler = logging.StreamHandler(sys.stdout)
>>> handler.setLevel(logging.DEBUG)
>>> formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
>>> handler.setFormatter(formatter)
>>> logger.addHandler(handler)
>>> client.templates.get()
2019-03-08 17:21:25,329 - python_http_client.client - DEBUG - GET Request: https://api.sendgrid.com/v3/templates
2019-03-08 17:21:25,329 - python_http_client.client - DEBUG - HEADERS: {'Authorization': 'Bearer redacted_token', 'Accept': 'application/json', 'User-agent': 'sendgrid/5.6.0;python'}
2019-03-08 17:21:25,696 - python_http_client.client - DEBUG - GET Response: 200 {"templates":[]}
```
