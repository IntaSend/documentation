---
description: >-
  This API is for the merchants to initiate card payments charge-back and
  refunds from a third-party system.
---

# Refunds

Before using this resource, please read carefully our article on how we handle [Chargebacks](https://intasend.com/chargebacks/) and the [Terms and Conditions](https://intasend.com/terms/) statements on the same.

These endpoints require [authentication](send-payments/api-authentication.md#obtain-authentication-token).

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/chargebacks/" method="post" summary="Create Chargeback" %}
{% swagger-description %}
Create a new chargeback request. IntaSend will be notified for processing.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Bearer <Token>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="invoice" type="number" %}
Invoice id of the transaction. This ID is normally returned in the complete card transaction as tracking_id or invoice_id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" %}
Amount to be refunded. Must be equal or less than the billed amount
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reason" type="string" %}
Reason for refund
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reason_details" type="string" %}
More details on the reason provided
{% endswagger-parameter %}

{% swagger-response status="200" description="A new chargeback entry details are returned" %}
```
{
    "id": 1,
    "transaction": 1,
    "invoice": 1,
    "amount": 200,
    "reason": "Delayed shipping",
    "status": "PENDING",
    "resolution": "",
    "staff_created": "false"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/chargebacks/" method="get" summary="List Chargeback" %}
{% swagger-description %}
List chargebacks made to the account
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Bearer <Token>
{% endswagger-parameter %}

{% swagger-response status="200" description="Returns array of results" %}
```
[{
    "id": 1,
    "transaction": 1,
    "invoice": 1,
    "amount": 200,
    "reason": "Delayed shipping",
    "reason_details": "System malfunction, could not send item faster", 
    "status": "PENDING",
    "resolution": "",
    "staff_created": "false"
}]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/chargebacks/:chargeback_id/" method="get" summary="Retrieve Chargeback" %}
{% swagger-description %}
Retrieve single chargeback record
{% endswagger-description %}

{% swagger-parameter in="path" name="chargeback_id" type="integer" %}
Record id to retrieve
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Bearer <Token>
{% endswagger-parameter %}

{% swagger-response status="200" description="Chargeback record" %}
```
{
    "id": 1,
    "transaction": 1,
    "invoice": 1,
    "amount": 200,
    "reason": "Delayed shipping",
    "reason_details": "System malfunction, could not send item faster",
    "status": "PENDING",
    "resolution": "",
    "staff_created": "false"
}
```
{% endswagger-response %}
{% endswagger %}
