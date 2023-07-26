# Python `requests` Module-Notes

## Introduction
The `requests` module is a powerful and user-friendly library in Python for making HTTP requests. It simplifies the process of sending HTTP requests to web servers and handling responses. The library is widely used for consuming APIs, scraping data from websites, and interacting with web services.

## Installation
To use `requests` it must first be installed with pip

```bash
pip install request
```

## Making a GET Request
The most common type of HTTP request is the GET request, which retrieves data from the server. Here's how to make a simple GET request using `requests`

```python
import requests

response = requests.get('https://api.example.com/data')
if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print('Error:', response.status_code)
```

## Sending Data With a POST Request
When you need to send data you can use a POST request -- for example, to send JSON data to a server.

```python
import requests

data = {'username': 'john_doe', 'email': 'john@example.com'}
response = requests.post('https://api.example.com/users', json=data)

if response.status_code == 201:
    print('User created successfully!')
else:
    print('Error:', response.status_code)

```

## Error Handling
It's essential to handle potential errors and exceptions when making HTTP requests. Use the `raise_for_status()` method or `try...except` blocks to handle exceptions

```python
import requests

try:
    response = requests.get('https://api.example.com/nonexistent')
    response.raise_for_status()  # Raises an exception for unsuccessful responses
    data = response.json()
    print(data)
except requests.exceptions.RequestException as e:
    print('Error:', e)

```

## Query Parameters
You can pass query paramters in the URL for filtering or paginating data.

```python
import requests

params = {'page': 2, 'per_page': 10}
response = requests.get('https://api.example.com/users', params=params)

if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print('Error:', response.status_code)
```

## Adding Headers
Headers can be added to customize your requests, such as setting the user agent.

```python
import requests

headers = {'Authorization': 'Bearer YOUR_ACCESS_TOKEN'}
response = requests.get('https://api.example.com/protected', headers=headers)

if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print('Error:', response.status_code)
```

## Handling Sessions
Using sessions allows certain parameters to persist across requests, such as headers or cookies.

```python
import requests

session = requests.Session()
session.headers.update({'User-Agent': 'MyApp/1.0'})

response = session.get('https://api.example.com/')
if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print('Error:', response.status_code)
```