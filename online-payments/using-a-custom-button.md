---
description: Customize the customer payment experience using a custom button.
---

# Using a custom button

The [standard button](payment-button.md) approach is the simplest way to start collecting payment on your website. Sometimes you might want to parse more items and this might not be possible through the data-\* attribute. IntaSend **inline web sdk** has a `.run()` method where you can pass extra parameters and initialize the payment popup.

## 1. Install Inline Web SDK

Include IntaSend plugin before closing your `</head>` tag.

```
<script src="https://unpkg.com/intasend-inlinejs-sdk@3.0.4/build/intasend-inline.js"></script>
```

## 2. Add your custom button

Note, unlike the standard button, the custom button does not require you to provide `data-*` attributes and **IntaSend class identifier**. For the sake of demonstration, we are using an ID attribute that we'll use to trigger the `onclick` event in the next code block.

```
<button id="customBtn">Pay USD 10</button>
```

## 3. Initialize IntaSend instance

Add your publishable public key and set the enviroonment.

```
let customBtnObj = new window.IntaSend({
    publicAPIKey: "<--REPLACE-WITH-YOUR-PUBLISHABLE-KEY-->",
    live: false // set to true when going live
})
```

## 4. Show payment screen on button click

Finally start payment process using the `.run({...})` method. Set the required payment options as per your need. [Here is a full list of options](payment-data-parameters.md) you can pass to the `.run({...})` method.

```
document.getElementById("customBtn").onclick = () => {
    customBtnObj.run({
        amount: 10,
        currency: "USD",
        email: "john@doe.com",
        first_name: "John",
        last_name: "Doe",
        country: "US"
    })
    .on("COMPLETE", (results) => console.log("Do something on success", results))
    .on("FAILED", (results) => console.log("Do something on failure", results))
    .on("IN-PROGRESS", (results) => console.log("Payment in progress status"))
}
```

Finally, capture payment results and do something on success and failure.
