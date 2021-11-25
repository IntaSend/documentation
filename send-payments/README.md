---
description: Guide on how to send payments using IntaSend Payment Gateway.
---

# Send Payments

## How to use Send Payments API

Send Payments API enables you to send money from your IntaSend API to another IntaSend account or an external wallet such M-Pesa B2C, M-Pesa B2B, and bank.

First and foremost, all requests in send money API require [authentication](api-authentication.md). You can obtain your authentication keys from your IntaSend dashboard. We also have a [sandbox (developers test environment)](../sandbox-and-live-environments.md#sandbox-development-environment) where you can test your integration before going live.

This API also serves as a disbursement API. When specifying transactions, we add them in an array, meaning multiple transactions can be triggered in a single request. The API has been tested with up to 5000 transactions in a single request to M-Pesa B2B and M-Pesa B2C, taking up to 15 minutes to complete the full payment cycle (initiation, results, and reporting reconcilation). The smaller batches take a shorter time < 3 seconds at most. In case you need to do more than 5000 transactions per request, please let us know so that we can advise well and archive optimum success rates.

### M-Pesa API Integration

IntaSend's send money API support both the M-Pesa B2B and B2C for [business payments](https://intasend.com/business-payments/). Unlike the IntaSend P2P requests, for M-Pesa requests, we have to wait for a success message from Safaricom. This will inform us well if the transaction is a success or not. In turn, we parse the same status back to you through the callback URL that you provided during the request. You can use the status retrieved to update your account. For every request, we also generate a tracking id that you can use to [query the status](payment-status.md#get-send-money-status) of the transactions at any time.

### How to fund your account

You must fund your account to be able to disburse payments from it. For the test environment, this can be done through the available [test cards](../sandbox-and-live-environments.md#sandbox-development-environment). If you already have funds in your wallet from sales and it has been cleared and ready to use, you are good to go.&#x20;

The following options are used to load funds to your IntaSend wallet.

1. Initate M-Pesa STK push from your account dashboard
2. Make a direct deposit from your card to the IntaSend account.
3. Direct bank deposit to our collection account. Please contact support for assistance on bank deposits.

Once this one is done, you'll see the funds reflected in your account and available. You are now ready to start sending money to multiple beneficiaries with the API.&#x20;
