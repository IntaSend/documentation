---
description: How to integrate IntaSend payment in your JavaScript web framework.
---

# React and Vue Examples

## How to add IntaSend to any Javascript project

### 1. Install SDK

IntaSend inlinejs-sdk is available using `yarn` or `npm`

```
yarn add intasend-inlinejs-sdk
```

### 2. Import IntaSend in your code

```
const IntaSend = require("intasend-inlinejs-sdk")
```

### 3. Initialize

You'll need your `publicAPIKey` and ensure the `live` flag is well set depending on your environment.

```
const intaSendInstance = new IntaSend({
    publicAPIKey: "<YOUR-API-KEY>",
    live: true //or false for sandbox environment
})
    
```

### 4. Load payment screen

The` .run()` the method will load the payment popup. Feel free to set the payment setting e.g the amount and currency based on your need. Here is a [reference](../payment-data-parameters.md) of options you can add.

```
// Load payment popup with the run() function
intaSendInstance.run({amount: 10, currency: "USD"})
```

### 5. Capture results

Finally, do something on payment complete or failure.

```
intaSendInstance
.on("COMPLETE", (results) => alert("COMPLETE"))
.on("FAILED", (results) => alert("FAILED"))
```
