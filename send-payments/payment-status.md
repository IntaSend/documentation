---
description: How to obtain send money payment status.
---

# Send Money Status

## Handling send money status

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/send-money/status/" method="post" summary="Get send money status" %}
{% swagger-description %}
This endpoint allows you to check payment status.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Bearer <TOKEN>
{% endswagger-parameter %}

{% swagger-parameter in="query" name="tracking_id" type="string" %}
Transaction tracking_id returned from send money request
{% endswagger-parameter %}

{% swagger-response status="200" description="Payment status" %}
```
{
    "tracking_id": "6138a6b7-51f6-42e2-86d0-8ca31c286dd8",
    "status": "Processing payment",
    "transactions": [
        {
            "status": "Pending",
            "request_reference_id": "9da1df21-b14b-44e3-99fd-573fd939f4dd",
            "mno_reference": "",
            "name": null,
            "phone_number": 254723890323,
            "amount": 5000,
            "narrative": null
        },
        {
            "status": "Unsuccessful",
            "request_reference_id": "ef99a2b4-4cbc-4869-8983-5b7fe5ae0415",
            "mno_reference": "OFQ31HC99P",
            "name": null,
            "phone_number": 254723890353,
            "amount": 5,
            "narrative": null
        }
    ],
    "actual_charges": 0,
    "paid_amount": 0,
    "failed_amount": 5,
    "created_at": "2020-06-26T17:37:07.323436+03:00",
    "updated_at": "2020-06-26T17:37:17.933968+03:00"
}
```
{% endswagger-response %}
{% endswagger %}

### Status codes description

#### Files status codes meaning

| Code  | Description                                                  |
| ----- | ------------------------------------------------------------ |
| BP101 | New batch or request, reading in progress                    |
| BF102 | Batch/request failed                                         |
| BP103 | Batch/request waiting approval                               |
| BP104 | Queued to check for float balance                            |
| BF105 | Failed checking float balance                                |
| BP106 | Float/balance check in progress                              |
| BF107 | Failed advance float check issue                             |
| BP108 | Advance internal validations in progress                     |
| BP109 | Payment to beneficiary in progress                           |
| BP110 | Sending payments to beneficiary in progress                  |
| BC100 | Completed sending all transactions. Results ready for review |
| BE111 | Batch/request ended or cancelled early.                      |

#### Code examples

{% tabs %}
{% tab title="Python" %}
```python
import requests

url = "https://sandbox.intasend.com/api/v1/send-money/status/"

payload = "{\"tracking_id\": \"6138a6b7-51f6-42e2-86d0-8ca31c286dd8\"}"
headers = {
  'Authorization': 'Bearer LfqRDqvfvwv77BhxuDsdXN04NyUx97',
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
  CURLOPT_URL => "https://sandbox.intasend.com/api/v1/send-money/status/",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS =>"{\"tracking_id\": \"6138a6b7-51f6-42e2-86d0-8ca31c286dd8\"}",
  CURLOPT_HTTPHEADER => array(
    "Authorization: Bearer LfqRDqvfvwv77BhxuDsdXN04NyUx97",
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

  url := "https://sandbox.intasend.com/api/v1/send-money/status/"
  method := "POST"

  payload := strings.NewReader("{\"tracking_id\": \"6138a6b7-51f6-42e2-86d0-8ca31c286dd8\"}")

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
  }
  req.Header.Add("Authorization", "Bearer LfqRDqvfvwv77BhxuDsdXN04NyUx97")
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

url = URI("https://sandbox.intasend.com/api/v1/send-money/status/")

https = Net::HTTP.new(url.host, url.port);
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = "Bearer LfqRDqvfvwv77BhxuDsdXN04NyUx97"
request["Content-Type"] = "application/json"
request.body = "{\"tracking_id\": \"6138a6b7-51f6-42e2-86d0-8ca31c286dd8\"}"

response = https.request(request)
puts response.read_body

```
{% endtab %}
{% endtabs %}

