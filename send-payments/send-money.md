---
description: >-
  Send money from your IntaSend account to your mobile money account i.e M-PESA
  and IntaSend P2P.
---

# Send Money

{% api-method method="post" host="https://sandbox.intasend.com" path="/api/v1/send-money/initiate/" %}
{% api-method-summary %}
Step 1 - Initiate send money
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to initiate send money requests. This method only initiates the send money process. You'll need to approve the transaction using your **approval private key**. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Bearer &lt;TOKEN&gt; 
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="device\_id" type="number" required=true %}
Create device under API section on the dashboard, add a public key, and obtain its id.
{% endapi-method-parameter %}

{% api-method-parameter name="provider" type="string" required=true %}
Options are: MPESA-B2C, INTASEND
{% endapi-method-parameter %}

{% api-method-parameter name="callback\_url" type="string" required=false %}
URL to send payment notification
{% endapi-method-parameter %}

{% api-method-parameter name="transactions" type="array" required=true %}
List of transactions
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
KES
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Payment successfully received
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Transaction list items

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| name | string | Yes | Beneficiary name |
| account | integer | Yes | Beneficiary phone number. Must be in the format `2547xxxxxxxxx` - note the country prefix `254` without a `+` |
| amount | integer | Yes | Amount to send |

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
```text
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

{% api-method method="post" host="https://sandbox.intasend.com" path="/api/v1/send-money/approve/" %}
{% api-method-summary %}
Step 2 - Approve send money
{% endapi-method-summary %}

{% api-method-description %}
Every transaction must be approved using the approval secret key. Only after approval, the transaction will be processed. Learn more about how to sign and approve a transaction using a digital key please check Extra Authentication - https://developers.intasend.com/apis/extra-payment-authentication.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer &lt;TOKEN&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="payload" type="string" required=true %}
Send back the response returned in step 1 by signing and  replacing the nonce
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

The original i.e returned response in step 1 \(initiation step\) looks like in the code block below. Pay attention to the `nonce` token which is a unique generated id for this transaction. You are required to sign this token and attach it back to the payload. Send back the payload with the signed nonce to the approval API. 

Note: You are required to sign the nonce with the **Private Key** of the device used to initiate the payment. Note this is under the device\_id parameter. On the IntaSend side, we'll verify the signature with the **Public Key** uploaded for use on the device.

Here are more details on [how to sign the nonce](extra-payment-authentication.md). 

```text
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

```text
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

