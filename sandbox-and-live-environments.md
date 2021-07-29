---
description: >-
  The following are details on how to develop and test the APIs before going
  live.
---

# Testing

IntaSend provides both staging and live environments.

All requests and callback URLs to this environment must be made through a secure network protocol \(HTTPS\). 

{% hint style="info" %}
Get started with our developers environment - so sign-up is required. Start experimenting right away - [https://sandbox.intasend.com/](https://sandbox.intasend.com/)
{% endhint %}

### Sandbox / Development Environment

Sign up for the **sandbox environment** for your development and testing.

**Sign up URL:** [https://sandbox.intasend.com/account/signup/](https://sandbox.intasend.com/account/signup/) ``

**API base URL:** [https://sandbox.intasend.com/api/](https://sandbox.intasend.com/api/)

### **Live environment** for your production.

**Sign up URL:** [https://payment.intasend.com/account/signup/](https://payment.intasend.com/account/signup/) ``

**API base URL:** [https://payment.intasend.com/api/](https://payment.intasend.com/account/signup/)

### Test details for sandbox environment

#### Test card numbers

| Card | Date | CVC |
| :--- | :--- | :--- |
| 4000 0000 0000 0002 | Any future date | Any 3 digits |
| 4242 4242 4242 4242 | Any future date | Any 3 digits |
| 4000 0000 0000 0101 | Any future date | Any 3 digits |
| 4000 0027 6000 3184 | Any future date | Any 3 digits |
| 5555 5555 5555 4444 | Any future date | Any 3 digits |
| 5200 8282 8282 8210 | Any future date | Any 4 digits |
| 4000 0566 5566 5556 | Any future date | Any 3 digits |
| 5200 8282 8282 8210 | Any future date | Any 3 digits |
| 4000 0027 6000 3184 | Any future date | Any 3 digits |
| 4456 5300 0000 1005 | Any future date | Any 3 digits |
| 5200 0000 0000 3001 | Any future date | Any 3 digits |

#### Test M-Pesa

Send money test number **254708374149**.

You can use your own number for the M-Pesa deposit/STK push. We are using the M-Pesa developers platform which does a reversal of all test amounts within 48 hours.

