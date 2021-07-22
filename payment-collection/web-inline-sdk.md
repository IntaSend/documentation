---
description: The easiest way to add payment widgets with IntaSend. Recommended for websites
---

# Website Integration

Web Inline SDK tool is the easiest way for businesses to integrate IntaSend payments on websites and mobile web. 

Here is a step-by-step procedure.

### 1. Install IntaSend Inline Javascript SDK plugin

Install the script before closing the `</body>` tag.

```javascript
<script src="https://unpkg.com/intasend-inlinejs-sdk@2.0.8/build/intasend-inline.js"></script>
<script>
    window.IntaSend.setup({
        publicAPIKey: "<YOUR-ACCOUNT-PUBLIC-KEY>",
        // Optional URL to redirect your clients after payment
        redirectURL: "http://example.com", 
        // Set live to false for sandbox environment
        live: true
    })
</script>
```

Obtain your account public key from [https://payment.intasend.com/account/login/?next=/account/settings/](https://payment.intasend.com/account/login/?next=/account/settings/) for live keys and [https://sandbox.intasend.com/account/login/?next=/account/settings/](https://payment.intasend.com/account/login/?next=/account/settings/) for the test keys. Your public key starts with the prefix `ISPublicKey_`

**Use `live:false`  during development to use the sandbox environment**.

### 2. Add your Payment Button

Note the button class `tp_button` is used by IntaSend to identify and trigger payment requests when it is clicked. Check the [payment options](web-inline-sdk.md#payment-options) below for more details.

```markup
<button class="tp_button" data-api_ref="payment-link" data-phone-number="254xxxxxxxx"
        data-email="user@example.com" data-amount="100" data-currency="KES">Pay Now</button>
```

Here is a code example of the setup

```markup
<!DOCTYPE html>
<html>

<head>
</head>

<body>
    <button class="tp_button" data-api_ref="payment-link" data-phone_number="254xxxxxxxx"
        data-email="user@example.com" data-amount="100" data-currency="KES">
        Pay Now
    </button>

    <script src="https://unpkg.com/intasend-inlinejs-sdk@2.0.8/build/intasend-inline.js"></script>
    <script>
        window.IntaSend.setup({
            publicAPIKey: "<YOUR-ACCOUNT-PUBLIC-KEY>",
            // Optional URL to redirect your clients
            redirectURL: "http://yoursite.com/thankyou/", 
            // Set live to false for sandbox environment
            live: true 
        })
    </script>
</body>

</html>
```

> Use either USD, GBP,  or EUR for currency field to support only card payments and foreign currency only transactions. To collect both card and MPesa payments, set the currency value to KES.

#### Initializing with options

You can also initialize/call the payment parameters during setup instead of defining them in the HTML button as shown below.

```javascript
<script>
    let is_obj = window.IntaSend.setup({
        publicAPIKey: "<YOUR-ACCOUNT-PUBLIC-KEY>",
        redirectURL: "http://yoursite.com/thankyou/"
    })
    
    // Note this items can also be included in the button using
    // data-* attribute.
    is_obj.run({
        amount: 200,
        phone_number: "254xxxxxxxxx",
        email: "customer@business.com",
        currency: "KES"
    })
</script>
```

#### Payment Options

| Parameter | Description |
| :--- | :--- |
| publicAPIKey | Required. |
| redirectURL | Optional link to redirect users after payment |
| element | Expects a CSS class. Defaults to `tp_button` |
| currency | Recommended: Options are USD, KES, GBP, EUR |
| amount | Optional. If not defined users will have the option to specify how much they want to pay |
| phone\_number | Optional. Users will be prompted if required e.g M-Pesa payment |
| email | Optional. Users will be prompted if required e.g card payments |
| api\_ref | Optional tracking reference for own use. |
| comment | Optional user comment if any |
| first\_name | Optional user first name |
| last\_name | Optional user last name |
| country | Optional country code e.g US, BR, KE etc |
| address | Optional user billing address |
| city | Optional user billing city |
| state | Optional user billing state |
| zipcode | Optional user billing zipcode |
| card\_tarrif | options are **BUSINESS-PAYS** and **CUSTOMER-PAYS** . Determine pays the card charges. Set to BUSINESS-PAYS by default |
| mobile\_tarrif | options are **BUSINESS-PAYS** and **CUSTOMER-PAYS** . Determine pays the card charges. Set to BUSINESS-PAYS by default |

### Get transaction status \(Events Hook\)

Use events to track the status of the transaction and update the relevant part of your website. Event code is in Javascript and for simple setup, it can be added inside `<script>` tag code.

1. Using Javascript, define your event handler

```javascript
function bindEvent(element, eventName, eventHandler) {
    if (element.addEventListener) {
        element.addEventListener(eventName, eventHandler, false);
    } else if (element.attachEvent) {
        element.attachEvent('on' + eventName, eventHandler);
    }
}
```

2. Wait for the event update

```javascript
bindEvent(window, 'message', function (e) {
    if (e.data.message) {
        if (e.data.message.identitier == 'intasend-status-update-cdrtl') {
            if (e.data.message.state === "COMPLETE") {
                // Do something on pay success
                // Make sure redirectURL is ommited in 
                // your setup function for this to work well
            }
        }
    }
})
```

**Note:** `e.data.message.state` outputs the following values: **COMPLETE, PENDING, FAILED, IN-PROGRESS**.

You can `console.log(e.data.message)` in that line to view every item the message object contains. Below is a sample data of the \``e.data.message`\` . Note from meta fields you can retrieve the invoice details e.g customer information and any other information that is available for the transaction.

```javascript
{
    "tracking_id": 10,
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
        }
        "customer_comment": "",
        "created_at": "2021-04-11T08:37:15.810438+03:00",
        "updated_at": "2021-04-11T08:37:15.810475+03:00"
    },
    "identitier": "intasend-status-update-cdrtl"
}
```

