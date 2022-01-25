---
description: API end-points for working with wallets and sub-accounts
---

# Wallets API

## How to integrate wallets API

These APIs will help you to create and manage **WORKING** wallets. By default, all IntaSend accounts have **SETTLEMENT** accounts which act as main accounts. **WORKING** wallets are basically sub-accounts that you can use to isolate your customers'/merchants' funds. Each customer can have their own wallets within IntaSend that you will manage on their behalf.

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/wallets/" method="get" summary="List available wallets" %}
{% swagger-description %}
Get a list of available wallets in the account. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer <ACCESS-TOKEN>
{% endswagger-parameter %}

{% swagger-response status="200" description="Sample successful response" %}
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
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/wallets/:id/" method="get" summary="Get wallet details" %}
{% swagger-description %}
Get wallet detailed information such as balance using its ID
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer <ACCESS-TOKEN>
{% endswagger-parameter %}

{% swagger-response status="200" description="Sample successful response." %}
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
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/wallets/:id/transactions/" baseUrl="https://sandbox.intasend.com" summary="Get wallet transactions" %}
{% swagger-description %}
Retrieve a list of all transactions made in the specified wallet.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Bearer <ACCESS-TOKEN>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Transactions list" %}
```javascript
[{
    "invoice": "",
    "value": "10.00",
    "running_balance": "20.00",
    "narrative": "Intra Txn. wallet 9",
    "created_at": "2020-08-03T15:08:40.263322+03:00",
    "updated_at": "2020-08-03T15:08:40.263349+03:00"
}, {
    "invoice": "",
    "value": "10.00",
    "running_balance": "10.00",
    "narrative": "Intra Txn. wallet 9",
    "created_at": "2020-08-03T15:08:32.283968+03:00",
    "updated_at": "2020-08-03T15:08:32.283992+03:00"
}]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="​ https://sandbox.intasend.com" path="/api/v1/wallets/" method="post" summary="Create a wallet" %}
{% swagger-description %}
Create a new wallet/sub-account
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Bearer <ACCESS-TOKEN>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="wallet_type" type="string" required="true" %}
Available option: WORKING
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="true" %}
Available Options: KES, USD, GBP, EUR
{% endswagger-parameter %}

{% swagger-parameter in="body" name="label" required="true" %}
New wallet identifier label e.g charges, owner name etc for easy querying on the dashboard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="can_disburse" type="Boolean" %}
If set to true, the wallet can be used to send money/withdraw to mobile money wallet with the API
{% endswagger-parameter %}

{% swagger-response status="200" description="Sample successful response" %}
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
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/payment/collection/" method="post" summary="Fund Wallet (M-Pesa)" %}
{% swagger-description %}
Fund wallet directly with M-Pesa STK Push (collections API).  Note that this API request is similar to the collection API. The only difference is that here you have to specify the destination 

`wallet_id`

.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer <ACCESS-TOKEN>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="public_key" type="string" %}
Your public key
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
Available option: M-PESA
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" %}
Available option: KES
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="number" %}
Amount to pay
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone_number" type="string" %}
Start with country prefix e.g 2547xxx
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="api_ref" type="string" %}
For own application tracking purposes
{% endswagger-parameter %}

{% swagger-parameter in="body" name="wallet_id" type="integer" %}
Destination wallet id
{% endswagger-parameter %}

{% swagger-response status="200" description="Sample payload on successful request." %}
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
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://sandbox.intasend.com" path="/api/v1/wallets/<:source_id>/intra_transfer/" method="post" summary="Intra-Wallet Transfers" %}
{% swagger-description %}
Move money between wallets/sub-accounts you own. This request can be used for reconciliation purposes across different sub-accounts. For instance, implementing a charge on a working wallet tied to a supplier or a branch, move it to your settlement account, and maintain a detailed narrative as shown above. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer <ACCESS-TOKEN>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="narrative" type="string" %}
Reason for transfer
{% endswagger-parameter %}

{% swagger-parameter in="body" name="wallet_id" type="integer" %}
Destination wallet id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="number" %}
Amount to transfer
{% endswagger-parameter %}

{% swagger-response status="200" description="Sample successful request payload." %}
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
{% endswagger-response %}
{% endswagger %}
