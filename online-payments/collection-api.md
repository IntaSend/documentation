---
description: >-
  How to trigger M-Pesa STK push without showing the IntaSend's payment popup or
  express check-out page.
---

# Direct M-Pesa STK-Push

Use the collection API if you prefer to automatically trigger M-Pesa STK payment requests from your backend using Python, Java,  PHP,  and Go.

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/payment/collection/" method="post" summary="Send M-Pesa STK-Push request" %}
{% swagger-description %}
Send an M-Pesa STK push payment request
{% endswagger-description %}

{% swagger-parameter in="body" name="public_key" type="string" %}
Your account public key. Found under settings.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" %}
KES 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
M-PESA
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="number" %}
Billing amount 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="api_ref" type="string" %}
Your transaction reference/tracking code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" %}
Customer name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone_number" type="string" %}
Prefix with country code e.g 2547..
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Customer email
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "invoice": {
        "id": "XMSLWOS",
        "invoice_id": "XMSLWOS",
        "state": "PENDING",
        "provider": "M-PESA",
        "value": "10.00",
        "account": "customer@example.com",
        "api_ref": null,
        "failed_reason": null,
        "created_at": "2020-06-26T13:24:47.040822+03:00",
        "updated_at": "2020-06-26T13:24:47.040849+03:00"
    }
}
```
{% endswagger-response %}
{% endswagger %}



{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/payment/status/" method="post" summary="Check payment status" %}
{% swagger-description %}
Check payment status
{% endswagger-description %}

{% swagger-parameter in="body" name="public_key" type="string" %}
Account public key. Found under settings 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="invoice_id" type="string" %}
Invoice ID returned in the payment request
{% endswagger-parameter %}

{% swagger-response status="200" description="Sample response returned" %}
```
{
    "invoice": {
        "id": "XMSLWOS",
        "invoice_id": "XMSLWOS",
        "state": "PENDING",
        "provider": "M-PESA",
        "charges": "0.00",
        "net_amount": 10.36,
        "currency": "KES",
        "value": "10.36",
        "account": "test@example.com",
        "api_ref": "ISL_faa26ef9-eb08-4353-b125-ec6a8f022815",
        "host": "https://sandbox.intasend.com",
        "failed_reason": null,
        "created_at": "2021-04-11T08:37:15.781977+03:00",
        "updated_at": "2021-04-11T08:37:15.782011+03:00"
    },
    "meta": {
        "id": "5aec8e0b-8d96-429b-98b7-5361198160bd",
        "customer": {
            "id": "ZOEW022",
            "phone_number": "",
            "email": "test@example.com",
            "first_name": "FELIX",
            "last_name": "CHERUIYOT",
            "country": "KE",
            "address": "Westlands",
            "city": "Nairobi",
            "state": "Nairobi",
            "zipcode": "2020",
            "provider": "M-PESA",
            "created_at": "2020-08-06T16:24:06.247397+03:00",
            "updated_at": "2021-04-11T08:37:15.755013+03:00"
        },
        "customer_comment": "",
        "created_at": "2021-04-11T08:37:15.810438+03:00",
        "updated_at": "2021-04-11T08:37:15.810475+03:00"
    }
}
```
{% endswagger-response %}
{% endswagger %}
