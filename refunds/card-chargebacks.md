---
description: >-
  This API is for the merchants to initiate card payments charge-back and
  refunds from a third-party system.
---

# Card Chargebacks

Before using this resource, please read carefully our article on how we handle [Chargebacks](https://intasend.com/chargebacks/) and the [Terms and Conditions](https://intasend.com/terms/) statements on the same.

These endpoints require [authentication](../api-prerequisite/api-authentication.md#obtain-authentication-token).

{% api-method method="post" host="https://sandbox.intasend.com" path="/api/v1/chargebacks/" %}
{% api-method-summary %}
Create Chargeback
{% endapi-method-summary %}

{% api-method-description %}
Create a new chargeback request. IntaSend will be notified for processing.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Bearer &lt;Token&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="invoice" type="number" required=true %}
Invoice id of the transaction. This ID is normally returned in the complete card transaction as tracking\_id or invoice\_id
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="string" required=true %}
Amount to be refunded. Must be equal or less than the billed amount
{% endapi-method-parameter %}

{% api-method-parameter name="reason" type="string" required=true %}
Reason for refund
{% endapi-method-parameter %}

{% api-method-parameter name="reason\_details" type="string" required=false %}
More details on the reason provided
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
A new chargeback entry details are returned
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://sandbox.intasend.com" path="/api/v1/chargebacks/" %}
{% api-method-summary %}
List Chargeback
{% endapi-method-summary %}

{% api-method-description %}
List chargebacks made to the account
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Bearer &lt;Token&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Returns array of results
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://sandbox.intasend.com" path="/api/v1/chargebacks/:chargeback\_id/" %}
{% api-method-summary %}
Retrieve Chargeback
{% endapi-method-summary %}

{% api-method-description %}
Retrieve single chargeback record
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="chargeback\_id" type="integer" required=true %}
Record id to retrieve
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=false %}
Bearer &lt;Token&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Chargeback record
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

