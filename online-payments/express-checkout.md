---
description: How to create check-out page using IntaSend 's checkout API
---

# Checkout API

## How to use REST API to create a sharable payment URL

To create a checkout page, a payment checkout URL that can be shared to the client to complete payment on email or social media, simply send a post request to `/api/v1/checkout/` with the [payment data parameter](payment-data-parameters.md)s as payload.

### Code examples

Send **POST** request to generate a **checkout URL**, then redirect the user to the checkout link to securely complete payment.

{% tabs %}
{% tab title="Curl" %}
```
curl --location --request POST 'https://sandbox.intasend.com/api/v1/checkout/' \
--header 'Content-Type: application/json' \
--header 'Cookie: csrftoken=RJXYBwzJ3IeqxgrNZ0iRFblmo9dOO6Sr6PiCjkrwrmu5LUYDTuNJanEbVwWveodC' \
--data-raw '{
    "public_key": "<YOUR-PUBLISHABLE-API-KEY>",
    "amount": 10,
    "currency": "USD",
    "email": "john@doe.com",
    "first_name": "John",
    "last_name": "Doe",
    "country": "US",
    "redirect_url": "https://example.com"
}'
```
{% endtab %}

{% tab title="Go" %}
```
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://sandbox.intasend.com/api/v1/checkout/"
  method := "POST"

  payload := strings.NewReader(`{
    "public_key": "<YOUR-PUBLISHABLE-API-KEY>",
    "amount": 10,
    "currency": "USD",
    "email": "john@doe.com",
    "first_name": "John",
    "last_name": "Doe",
    "country": "US",
    "redirect_url": "https://example.com"
}`)

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("Content-Type", "application/json")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endtab %}

{% tab title="JavaScript" %}
```
var axios = require('axios');
var data = JSON.stringify({"public_key":"<YOUR-PUBLISHABLE-API-KEY>","amount":10,"currency":"USD","email":"john@doe.com","first_name":"John","last_name":"Doe","country":"US",
    "redirect_url": "https://example.com"});

var config = {
  method: 'post',
  url: 'https://sandbox.intasend.com/api/v1/checkout/',
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

{% tab title="PHP" %}
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://sandbox.intasend.com/api/v1/checkout/',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "public_key": "<YOUR-PUBLISHABLE-API-KEY>",
    "amount": 10,
    "currency": "USD",
    "email": "john@doe.com",
    "first_name": "John",
    "last_name": "Doe",
    "country": "US",
    "redirect_url": "https://example.com"
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
{% endtab %}

{% tab title="Python" %}
```
import requests

url = "https://sandbox.intasend.com/api/v1/checkout/"

payload={
  "public_key":"<YOUR-PUBLISHABLE-API-KEY>",
  "amount": 10,
  "currency": "USD",
  "email": "john@doe.com",
  "first_name": "John",
  "last_name": "Doe",
  "country": "US",
  "redirect_url": "https://example.com"
}
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```
{% endtab %}
{% endtabs %}

### Response

The checkout request returns a JSON response with a **`url`** field. Redirect the user to the **`url`** to securely complete payment.

```
{
    "id": "666f4283-ffb2-4633-8c30-5338a50be37d",
    "url": "https://sandbox.intasend.com/checkout/666f4283-ffb2-4633-8c30-5338a50be37d/express/",
    "signature": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzY29wZSI6ImV4cHJl....",
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": null,
    "email": "john@doe.com",
    "country": "US",
    "address": null,
    "city": null,
    "state": null,
    "zipcode": null,
    "api_ref": null,
    "amount": "10.00",
    "currency": "USD",
    "mobile_tarrif": "BUSINESS-PAYS",
    "card_tarrif": "BUSINESS-PAYS",
    "created_at": "2021-08-05T10:53:08.761765+03:00",
    "updated_at": "2021-08-05T10:53:08.761794+03:00"
}
```

### Code Example using Axios (JavaScript)

{% hint style="info" %}
Here is a quick example of how to create a link using JavaScript. Note this can be done from any backend e.g PHP, Python, and Java
{% endhint %}

### 1. Install Axios

We'll use Axios to send HTTP post requests. Feel free to use any other tool that works well for you.

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.21.1/axios.min.js"></script>
```

### 2. Create a check-out link request

Send a POST request to the API environment that you'd wish to create the link. Learn more on test and live environment [here](../sandbox-and-live-environments.md).

A successful request will return an `url` which in this case will be our check-out URL. Share this `url` with the customer for them to complete payment.

```
function generateLink() {
    // Use https://payment.intasend.com/api/v1/checkout/ for live payments
    let url = "https://sandbox.intasend.com/api/v1/checkout/"
    let payload = {
        public_key: "REPLACE-WITH-YOUR-PUBLISHABLE-KEY",
        amount: 10,
        currency: "KES",
        email: "john@doe.com",
        first_name: "John",
        last_name: "Doe",
        country: "US"
    }
    axios.post(url, payload).then((resp) => {
        if (resp.data.url) {
            window.open(resp.data.url, '_blank').focus();
        }
    }).catch((err) => alert("Problem experienced while initializing your request: " + err))
}
```

Trigger the above function using an on-click event. Here is a sample button for your reference.

```
<button onclick="generateLink()">Pay now</button>
```
