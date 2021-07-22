---
description: Working with accounts (wallets) and sub-accounts
---

# Wallets and Balance API

Wallets API enables you to extend IntaSend's capability and automate your payment workflows. This API requires [authentication](../api-prerequisite/api-authentication.md).

Here are some of the use-cases you can build using our wallets API:

* Mobile banking and micro-lending applications
* Ecommerce vendors payments and collection systems
* Charges tracking and reconciliation solution
* A crowdfunding solution where each campaign is tied to a single wallet for easy reconciliation and reports.
* Wallet solution for gaming and e-sports

There are so many other use-cases that our API can support. Please feel free to [contact us](../resources/api-support.md) in case you need any clarification.

{% api-method method="get" host="https://sandbox.intasend.com" path="/api/v1/wallets/" %}
{% api-method-summary %}
List available wallets
{% endapi-method-summary %}

{% api-method-description %}
Get a list of available wallets in the account. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer &lt;ACCESS-TOKEN&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Sample successful response
{% endapi-method-response-example-description %}

```
[{
    'id': 9,
    'currency': 'KES',
    'wallet_type': 'SETTLEMENT',
    'current_balance': '1004602.43',
    'available_balance': '865016.45',
    'updated_at': '2021-05-29T22:20:18.631286+03:00'
}, {
    'id': 328,
    'currency': 'GBP',
    'wallet_type': 'WORKING',
    'current_balance': '0.00',
    'available_balance': '0.00',
    'updated_at': '2021-05-31T21:51:05.577470+03:00'
}]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://sandbox.intasend.com" path="/api/v1/wallets/:id/" %}
{% api-method-summary %}
Get wallet details
{% endapi-method-summary %}

{% api-method-description %}
Get wallet detailed information such as balance using its ID
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer &lt;ACCESS-TOKEN&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Sample successful response.
{% endapi-method-response-example-description %}

```
{
    'id': 201,
    'currency': 'GBP',
    'wallet_type': 'SETTLEMENT',
    'current_balance': '3281.00',
    'available_balance': '3281.00',
    'updated_at': '2021-05-23T09:25:50.665390+03:00'
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="​ https://sandbox.intasend.com" path="/api/v1/wallets/" %}
{% api-method-summary %}
Create a wallet
{% endapi-method-summary %}

{% api-method-description %}
Create a new wallet/sub-account
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer &lt;ACCESS-TOKEN&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="wallet\_type" type="string" required=true %}
Available option: WORKING
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
Available Options: KES, USD, GBP, EUR
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Sample successful response
{% endapi-method-response-example-description %}

```
{
    'id': 328,
    'currency': 'GBP',
    'wallet_type': 'WORKING',
    'current_balance': '0.00',
    'available_balance': '0.00',
    'updated_at': '2021-05-31T21:51:05.577470+03:00'
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://sandbox.intasend.com" path="/api/v1/payment/collection/" %}
{% api-method-summary %}
Fund Wallet \(M-Pesa\)
{% endapi-method-summary %}

{% api-method-description %}
Fund wallet directly with M-Pesa STK Push \(collections API\).  Note that this API request is similar to the collection API. The only difference is that here you have to specify the destination `wallet_id`.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer &lt;ACCESS-TOKEN&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="public\_key" type="string" required=true %}
Your public key
{% endapi-method-parameter %}

{% api-method-parameter name="method" type="string" required=true %}
Available option: M-PESA
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
Available option: KES
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="number" required=true %}
Amount to pay
{% endapi-method-parameter %}

{% api-method-parameter name="phone\_number" type="string" required=true %}
Start with country prefix e.g 2547xxx
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="api\_ref" type="string" required=false %}
For own application tracking purposes
{% endapi-method-parameter %}

{% api-method-parameter name="wallet\_id" type="integer" required=true %}
Destination wallet id
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Sample payload on successful request.
{% endapi-method-response-example-description %}

```
{
    'id': '77750cb8-ad67-46f7-b687-ce09831785bc',
    'invoice': {
        'id': 1762,
        'state': 'PENDING',
        'provider': 'M-PESA',
        'charges': '0.00',
        'net_amount': 10.0,
        'currency': 'KES',
        'value': '10.00',
        'account': '254723890353',
        'api_ref': 'API Request',
        'host': None,
        'failed_reason': None,
        'failed_code': None,
        'failed_code_link': 'https://intasend.com/troubleshooting',
        'created_at': '2021-05-31T22:15:34.611185+03:00',
        'updated_at': '2021-05-31T22:15:34.611279+03:00'
    },
    'device_fingerprint': None,
    'ip_address': '127.0.0.1',
    'customer': {
        'id': 55,
        'phone_number': '254723890353',
        'email': 'felix@intasend.com',
        'first_name': None,
        'last_name': None,
        'country': None,
        'address': None,
        'city': None,
        'state': None,
        'zipcode': None,
        'provider': 'M-PESA',
        'created_at': '2020-08-03T12:14:25.191171+03:00',
        'updated_at': '2021-05-31T22:15:34.602101+03:00'
    },
    'payment_link': None,
    'customer_comment': None,
    'created_at': '2021-05-31T22:15:34.619332+03:00',
    'updated_at': '2021-05-31T22:15:34.619359+03:00'
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://sandbox.intasend.com" path="/api/v1/wallets/<:source\_id>/intra\_transfer/" %}
{% api-method-summary %}
Intra-Wallet Transfers
{% endapi-method-summary %}

{% api-method-description %}
Move money between wallets/sub-accounts you own. This request can be used for reconciliation purposes across different sub-accounts. For instance, implementing a charge on a working wallet that is tied to a supplier or a branch and moving it to your settlement account, and maintain a detailed narrative as shown above. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer &lt;ACCESS-TOKEN&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="narrative" type="string" required=false %}
Reason for transfer
{% endapi-method-parameter %}

{% api-method-parameter name="wallet\_id" type="integer" required=true %}
Destination wallet id
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="number" required=true %}
Amount to transfer
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Sample successful request payload.
{% endapi-method-response-example-description %}

```
{
    'origin': {
        'id': 201,
        'currency': 'GBP',
        'wallet_type': 'SETTLEMENT',
        'current_balance': '3279.00',
        'available_balance': '3279.00',
        'updated_at': '2021-05-31T22:31:41.297514+03:00'
    },
    'destination': {
        'id': 328,
        'currency': 'GBP',
        'wallet_type': 'WORKING',
        'current_balance': '2.00',
        'available_balance': '2.00',
        'updated_at': '2021-05-31T22:31:41.317929+03:00'
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

