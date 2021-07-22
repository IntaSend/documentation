---
description: How to directly fund an account
---

# Fund Account

To fund your account uses the same approach as in [Collection API](../payment-collection/collection-api.md). This API does not require OAuth 2.0 authentication. You'll need your [account Public Key](https://payment.intasend.com/account/settings/) when making the request.

The following are code examples on how to fund any account using M-Pesa.

#### How to Deposit - Code examples

{% tabs %}
{% tab title="Python" %}
```python
import requests

url = "https://sandbox.intasend.com/api/v1/payment/collection/"

payload = "{\n    \"currency\": \"KES\",\n    \"method\": \"M-PESA\",\n    \"amount\": 10,\n    \"api_ref\": \"Test-ref\",\n    \"name\": \"test-name\",\n    \"phone_number\": 254723890353,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))

```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://sandbox.intasend.com/api/v1/payment/collection/",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS =>"{\n    \"currency\": \"KES\",\n    \"method\": \"M-PESA\",\n    \"amount\": 10,\n    \"api_ref\": \"Test-ref\",\n    \"name\": \"test-name\",\n    \"phone_number\": 254723890353,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}",
  CURLOPT_HTTPHEADER => array(
    "Content-Type: application/json"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://sandbox.intasend.com/api/v1/payment/collection/"
  method := "POST"

  payload := strings.NewReader("{\n    \"currency\": \"KES\",\n    \"method\": \"M-PESA\",\n    \"amount\": 10,\n    \"api_ref\": \"Test-ref\",\n    \"name\": \"test-name\",\n    \"phone_number\": 254723890353,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}")

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
  }
  req.Header.Add("Content-Type", "application/json")
  
  res, err := client.Do(req)
  defer res.Body.Close()
  body, err := ioutil.ReadAll(res.Body)

  fmt.Println(string(body))
}
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "uri"
require "net/http"

url = URI("https://sandbox.intasend.com/api/v1/payment/collection/")

https = Net::HTTP.new(url.host, url.port);
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Content-Type"] = "application/json"
request.body = "{\n    \"currency\": \"KES\",\n    \"method\": \"M-PESA\",\n    \"amount\": 10,\n    \"api_ref\": \"Test-ref\",\n    \"name\": \"test-name\",\n    \"phone_number\": 254723890353,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}"

response = https.request(request)
puts response.read_body

```
{% endtab %}

{% tab title="Java" %}
```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n    \"currency\": \"KES\",\n    \"method\": \"M-PESA\",\n    \"amount\": 10,\n    \"api_ref\": \"Test-ref\",\n    \"name\": \"test-name\",\n    \"phone_number\": 254723890353,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}");
Request request = new Request.Builder()
  .url("https://sandbox.intasend.com/api/v1/payment/collection/")
  .method("POST", body)
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var axios = require('axios');
var data = JSON.stringify({"currency":"KES","method":"M-PESA","amount":10,"api_ref":"Test-ref","name":"test-name","phone_number":254723890353,"public_key":"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f"});

var config = {
  method: 'post',
  url: 'https://sandbox.intasend.com/api/v1/payment/collection/',
  headers: { 
    'Content-Type': 'application/json'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});

```
{% endtab %}
{% endtabs %}

#### Sample response

```text
{
    "invoice": {
        "id": 157,
        "state": "PENDING",
        "provider": "M-PESA",
        "value": "10.00",
        "account": "254723890353",
        "api_ref": "Test-ref",
        "failed_reason": null,
        "created_at": "2020-06-26T19:23:17.935396+03:00",
        "updated_at": "2020-06-26T19:23:17.935421+03:00"
    }
}
```

#### How to check status - code examples

{% tabs %}
{% tab title="Python" %}
```python
import requests

url = "https://sandbox.intasend.com/api/v1/payment/status/"

payload = "{\n    \"invoice_id\": 157,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://sandbox.intasend.com/api/v1/payment/status/",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS =>"{\n    \"invoice_id\": 157,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}",
  CURLOPT_HTTPHEADER => array(
    "Content-Type: application/json"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://sandbox.intasend.com/api/v1/payment/status/"
  method := "POST"

  payload := strings.NewReader("{\n    \"invoice_id\": 157,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}")

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
  }
  req.Header.Add("Content-Type", "application/json")
  
  res, err := client.Do(req)
  defer res.Body.Close()
  body, err := ioutil.ReadAll(res.Body)

  fmt.Println(string(body))
}
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "uri"
require "net/http"

url = URI("https://sandbox.intasend.com/api/v1/payment/status/")

https = Net::HTTP.new(url.host, url.port);
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Content-Type"] = "application/json"
request.body = "{\n    \"invoice_id\": 157,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}"

response = https.request(request)
puts response.read_body

```
{% endtab %}

{% tab title="Java" %}
```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n    \"invoice_id\": 157,\n    \"public_key\": \"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f\"\n}");
Request request = new Request.Builder()
  .url("https://sandbox.intasend.com/api/v1/payment/status/")
  .method("POST", body)
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var axios = require('axios');
var data = JSON.stringify({"invoice_id":157,"public_key":"TPPublicKey_91ffc81a-8ac4-419e-8008-7091caa8d73f"});

var config = {
  method: 'post',
  url: 'https://sandbox.intasend.com/api/v1/payment/status/',
  headers: { 
    'Content-Type': 'application/json'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});

```
{% endtab %}
{% endtabs %}



