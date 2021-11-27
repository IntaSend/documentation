---
description: >-
  You'll be required to authenticate your requests when using transfer and
  accounts APIs. The following guidelines provide details on how to generate an
  authentication token.
---

# Authentication

## How to Generate API Token

1. Log in with your account username and password. Ensure this request is made through HTTPS (secure HTTP protocol).
2. For **sandbox (no sign-up is required)** go to [https://sandbox.intasend.com/account/api-keys/](https://sandbox.intasend.com/account/api-keys/) and for **production** use [https://payment.intasend.com/account/api-keys/](https://payment.intasend.com/account/api-keys/)
3. Click Generate API Token button to create your token. You must copy this token and store it in a safe place. This is what you'll be using for authentication.

{% hint style="info" %}
Get test API key here [https://sandbox.intasend.com/](https://sandbox.intasend.com) (No sign-up needed).
{% endhint %}

![](<../.gitbook/assets/image (10).png>)

**Note:** For transfer APIs, you'll need an extra authentication mechanism in addition to your API Token. Please check it out below.

{% content-ref url="extra-payment-authentication.md" %}
[extra-payment-authentication.md](extra-payment-authentication.md)
{% endcontent-ref %}
