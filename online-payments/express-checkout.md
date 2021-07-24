---
description: How to create check-out page using IntaSend 's check-out API
---

# Express check-out

To create a checkout page, simply send a post request to `/api/v1/checkout/` with the [payment data parameter](payment-data-parameters.md)s as payload.

{% hint style="info" %}
Here is a quick example of how to create a link using JavaScript. Note this can be done from any backend e.g PHP, Python, and Java
{% endhint %}

## 1. Install Axios

We'll use axios to send HTTP post requests. Feel free to use any other tool that works well for you.

```text
<script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.21.1/axios.min.js"></script>
```

## 2. Create a check-out link request

Send a POST request to the API environment that you'd wish to create the link. Learn more on test and live environment [here](../sandbox-and-live-environments.md).

A successful request will return an `url` which in this case will be our check-out URL. Share this `url` with the customer for them to complete payment.

```text
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

Trigger the above function using on-click event. Here is a sample button for your reference.

```text
<button onclick="generateLink()">Pay now</button>
```

