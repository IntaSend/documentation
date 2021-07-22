---
description: Implement collection using our RESTFul JSON API
---

# Collection API \(Advance\)

Use the collection API if you prefer to automatically trigger payment collection requests from your backend e.g Python, Java,  PHP,  and Go.

Use the [Website Integration](web-inline-sdk.md) option for **card payments** support. Note it is already 3D enabled.

### How to send Payment Collection Request

{% api-method method="post" host="https://sandbox.intasend.com" path="/api/v1/payment/collection/" %}
{% api-method-summary %}
M-Pesa request
{% endapi-method-summary %}

{% api-method-description %}
Send an M-Pesa STK push payment request
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="public\_key" type="string" required=true %}
Your account public key. Found under settings.
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
KES 
{% endapi-method-parameter %}

{% api-method-parameter name="method" type="string" required=true %}
M-PESA
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="number" required=true %}
Billing amount 
{% endapi-method-parameter %}

{% api-method-parameter name="api\_ref" type="string" required=false %}
Your transaction reference/tracking code
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}
Customer name
{% endapi-method-parameter %}

{% api-method-parameter name="phone\_number" type="string" required=true %}
Prefix with country code e.g 2547..
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=false %}
Required for card payments
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "invoice": {
        "id": 150,
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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



{% api-method method="post" host="https://sandbox.intasend.com" path="/api/v1/payment/status/" %}
{% api-method-summary %}
Check payment status
{% endapi-method-summary %}

{% api-method-description %}
Check payment status
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="public\_key" type="string" required=true %}
Account public key. Found under settings 
{% endapi-method-parameter %}

{% api-method-parameter name="invoice\_id" type="number" required=true %}
Invoice ID returned in the payment request
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Sample response returned
{% endapi-method-response-example-description %}

```
{
    "invoice": {
        "id": 10,
        "state": "PENDING",
        "provider": "CARD-PAYMENT",
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
            "id": 61,
            "phone_number": "",
            "email": "test@example.com",
            "first_name": "FELIX",
            "last_name": "CHERUIYOT",
            "country": "KE",
            "address": "Westlands",
            "city": "Nairobi",
            "state": "Nairobi",
            "zipcode": "2020",
            "provider": "CARD-PAYMENT",
            "created_at": "2020-08-06T16:24:06.247397+03:00",
            "updated_at": "2021-04-11T08:37:15.755013+03:00"
        },
        "payment_link": {
            "id": "faa26ef9-eb08-4353-b125-ec6a8f022815",
            "title": "Test Billing Page",
            "is_active": true,
            "redirect_url": null,
            "amount": null,
            "usage_limit": null,
            "qrcode_file": "https://intasend-staging.s3.amazonaws.com/qrcodes/...",
            "currency": "KES",
            "mobile_tarrif": "CUSTOMER-PAYS",
            "card_tarrif": "CUSTOMER-PAYS",
            "created_at": "2020-06-26T08:11:24.644509+03:00",
            "updated_at": "2020-10-05T16:45:59.757353+03:00"
        },
        "customer_comment": "",
        "created_at": "2021-04-11T08:37:15.810438+03:00",
        "updated_at": "2021-04-11T08:37:15.810475+03:00"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

