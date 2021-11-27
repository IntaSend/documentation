---
description: >-
  Single API to send money from your IntaSend account to your mobile money
  account i.e M-PESA, send to PayBill and TillNumber (M-Pesa B2B API), and
  IntaSend P2P.
---

# Send Money

## How to send money with the API&#x20;

Currently, you can send money to the following providers directly from your IntaSend [wallet](../wallet-as-a-service/).

| Transfer Type                          | Provider API Code |
| -------------------------------------- | ----------------- |
| IntaSend to IntaSend transfer          | INTASEND          |
| M-Pesa send money (B2C)                | MPESA-B2C         |
| M-Pesa send to Till and Paybills (B2B) | MPESA-B2B         |

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/send-money/initiate/" method="post" summary="Step 1 - Initiate send money" %}
{% swagger-description %}
This endpoint allows you to initiate send money requests. This method only initiates the send money process. You'll need to approve the transaction using your 

**approval private key**

. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Bearer <TOKEN> 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="device_id" type="number" %}
Create device under API section on the dashboard, add a public key, and obtain its id.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="provider" type="string" %}
Options are: MPESA-B2C, INTASEND, MPESA-B2B
{% endswagger-parameter %}

{% swagger-parameter in="body" name="callback_url" type="string" %}
URL to send payment notification
{% endswagger-parameter %}

{% swagger-parameter in="body" name="transactions" type="array" %}
List of transactions
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" %}
KES
{% endswagger-parameter %}

{% swagger-response status="200" description="Payment successfully received" %}
```
{
    "tracking_id": "c1acf08c-5cc1-4b3e-b4a8-e43bc068aa56",
    "status": "Preview and approve",
    "nonce": "1aiw02",
    "device_id": 1,
    "transactions": [
        {
            "status": "Pending",
            "request_reference_id": "f6a5a8dc-e190-4707-8ea2-102919709a72",
            "name": null,
            "account": 254723890353,
            "amount": 10,
            "narrative": null
        },
        {
            "status": "Pending",
            "request_reference_id": "cd763f35-44b3-4e89-a27a-252d507105f6",
            "name": null,
            "phone_number": 254708374149,
            "amount": 500,
            "narrative": null
        }
    ],
    "charge_estimate": 50.0,
    "total_amount_estimate": 560.0,
    "created_at": "2020-07-31T14:00:56.563163+03:00",
    "updated_at": "2020-07-31T14:00:56.632188+03:00"
}
```
{% endswagger-response %}
{% endswagger %}

Transaction list items

| Parameter     | Type    | Required    | Description                                                                                                   |
| ------------- | ------- | ----------- | ------------------------------------------------------------------------------------------------------------- |
| name          | string  | Yes         | Beneficiary name                                                                                              |
| account       | integer | Yes         | Beneficiary phone number. Must be in the format `2547xxxxxxxxx` - note the country prefix `254` without a `+` |
| amount        | integer | Yes         | Amount to send                                                                                                |
| account\_type | string  | Conditional | Required only for M-Pesa B2B. Acceptable fields are: **`Paybill`** or **`TillNumber`**                        |

NB - Obtain tracking\_id for the purpose of [checking status](payment-status.md).

#### Code examples

{% tabs %}
{% tab title="Python" %}
```python
import requests

url = "http://sandbox.intasend.com/api/v1/send-money/initiate/"

payload = {'provider': 'MPESA-B2C', 'currency': 'KES', 'callback_url': 'https://example.com', 'transactions': [{'name': 'test-name', 'account': 254723890353, 'amount': 10}], 'device_id': 1}
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
  CURLOPT_URL => "http://sandbox.intasend.com/api/v1/send-money/initiate/",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS =>"{\"transactions\": [{\"account\": \"254723890353\", \"amount\": \"5\"}, {\"account\": \"254723890323\", \"amount\": \"5000\"}], \"currency\": \"KES\", \"callback_url\": \"http://127.0.0.1:8000/false-api/\", \"device_id\": \"1\"}",
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

  url := "http://sandbox.intasend.com/api/v1/send-money/initiate/"
  method := "POST"

  payload := strings.NewReader("{\"transactions\": [{\"account\": \"254723890353\", \"amount\": \"5\"}, {\"account\": \"254723890323\", \"amount\": \"5000\"}], \"currency\": \"KES\", \"callback_url\": \"http://127.0.0.1:8000/false-api/\", \"device_id\": \"1\"}")

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

url = URI("http://sandbox.intasend.com/api/v1/send-money/initiate/")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Authorization"] = "Bearer LfqRDqvfvwv77BhxuDsdXN04NyUx97"
request["Content-Type"] = "application/json"
request.body = "{\"transactions\": [{\"account\": \"254723890353\", \"amount\": \"5\"}, {\"account\": \"254723890323\", \"amount\": \"5000\"}], \"currency\": \"KES\", \"callback_url\": \"http://127.0.0.1:8000/false-api/\", \"device_id\": \"1\"}"

response = http.request(request)
puts response.read_body

```
{% endtab %}

{% tab title="Java" %}
```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\"transactions\": [{\"phone_number\": \"254723890353\",\"amount\": \"5\"},{\"phone_number\": \"254723890323\",\"amount\": \"5000\"}],\"currency\": \"KES\",\"device_id\": \"1\",\"callback_url\": \"http://127.0.0.1:8000/false-api/\"}");
Request request = new Request.Builder()
  .url("http://sandbox.intasend.com/api/v1/send-money/initiate/")
  .method("POST", body)
  .addHeader("Authorization", "Bearer LfqRDqvfvwv77BhxuDsdXN04NyUx97")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```
{% endtab %}
{% endtabs %}

#### Sample response

{% tabs %}
{% tab title="Successful request" %}
```
{
    "tracking_id": "c1acf08c-5cc1-4b3e-b4a8-e43bc068aa56",
    "status": "Preview and approve",
    "nonce": "1aiw02",
    "device_id": 1,
    "transactions": [
        {
            "status": "Pending",
            "request_reference_id": "f6a5a8dc-e190-4707-8ea2-102919709a72",
            "name": null,
            "account": 254723890353,
            "amount": 10,
            "narrative": null
        },
        {
            "status": "Pending",
            "request_reference_id": "cd763f35-44b3-4e89-a27a-252d507105f6",
            "name": null,
            "phone_number": 254708374149,
            "amount": 500,
            "narrative": null
        }
    ],
    "charge_estimate": 50.0,
    "total_amount_estimate": 560.0,
    "created_at": "2020-07-31T14:00:56.563163+03:00",
    "updated_at": "2020-07-31T14:00:56.632188+03:00"
}
```
{% endtab %}

{% tab title="Failed request" %}
```
# Returned with http status 400, 403, 401 depending on error type
# Reason for failure will be indicated under "details".
Sample response:

{'details': 'Device id not found'}
```
{% endtab %}
{% endtabs %}

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/send-money/approve/" method="post" summary="Step 2 - Approve send money" %}
{% swagger-description %}
Every transaction must be approved using the approval secret key. Only after approval, the transaction will be processed. Learn more about how to sign and approve a transaction using a digital key please check Extra Authentication - https://developers.intasend.com/apis/extra-payment-authentication.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer <TOKEN>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="payload" type="string" %}
Send back the response returned in step 1 by signing and  replacing the nonce
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

The original i.e returned response in step 1 (initiation step) looks like in the code block below. Pay attention to the `nonce` token which is a unique generated id for this transaction. You are required to sign this token and attach it back to the payload. Send back the payload with the signed nonce to the approval API.&#x20;

Note: You are required to sign the nonce with the **Private Key** of the device used to initiate the payment. Note this is under the device\_id parameter. On the IntaSend side, we'll verify the signature with the **Public Key** uploaded for use on the device.

Here are more details on [how to sign the nonce](extra-payment-authentication.md).&#x20;

```
{
    "tracking_id": "c1acf08c-5cc1-4b3e-b4a8-e43bc068aa56",
    "status": "Preview and approve",
    "nonce": "1aiw02",
    "device_id": 1,
    "transactions": [
        {
            "status": "Pending",
            "request_reference_id": "f6a5a8dc-e190-4707-8ea2-102919709a72",
            "name": null,
            "account": 254723890353,
            "amount": 10000,
            "narrative": null
        }
        ...
    ],
    "charge_estimate": 140.0,
    "total_amount_estimate": 20140.0,
    ...
}
```

Sample signed payload

```
{
    "tracking_id": "c1acf08c-5cc1-4b3e-b4a8-e43bc068aa56",
    "status": "Preview and approve",
    "nonce": "<SIGNED-NONCE-HEX>",
    "transactions": [
        {
            "status": "Pending",
            "request_reference_id": "f6a5a8dc-e190-4707-8ea2-102919709a72",
            "name": null,
            "account": 254723890353,
            "amount": 10000,
            "narrative": null
        }
    ],
    "charge_estimate": 140.0,
    "total_amount_estimate": 20140.0,
    ...
}
```
