---
description: How to integrate IntaSend payment in your JavaScript web framework.
---

# React/Vue/Yarn/NPM

## 1. Install SDK

IntaSend inlinejs-sdk is available using `yarn` or `npm`

```text
yarn add intasend-inlinejs-sdk
```

## 2. Import IntaSend in your code

```text
const IntaSend = require("intasend-inlinejs-sdk")
```

## 3. Initialize

You'll need your `publicAPIKey` and ensure the `live` flag is well set depending on your environment.

```text
const intaSendInstance = new IntaSend({
    publicAPIKey: "<YOUR-API-KEY>",
    live: true //or false for sandbox environment
})
    
```

## 4. Load payment screen

The `.run()` method will load the payment popup. Feel free to set the payment setting e.g the amount and currency based on your need. Here is a [reference](payment-data-parameters.md) of more options you can add.

```text
// Load payment popup with the run() function
intaSendInstance.run({amount: 10, currency: "USD"})
```

## 5. Capture results

Finally, do something on payment complete or failure.

```text
intaSendInstance
.on("COMPLETE", (results) => alert("COMPLETE"))
.on("FAILED", (results) => alert("FAILED"))
```

