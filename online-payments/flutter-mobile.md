---
description: How to integrate IntaSend with Flutter for IOS and Android applications
---

# Flutter (Mobile)

## How to accept online payments with IntaSend on your mobile app

#### How to install IntaSend Flutter package

Check [https://pub.dev/packages/intasend\_flutter/install](https://pub.dev/packages/intasend\_flutter/install) the official package for installation instructions. Be sure to install and use the latest.

#### How to use

Flutter plugins enable you to set up a [checkout](express-checkout.md) screen and render it on a webview. You'll require your public key. Consider using [webhooks](../webhooks/how-to-setup.md) to update your backend when the user pays, and probably send a push notification or update the user interface on payment success.

```
import 'package:intasend_flutter/models/checkout.dart';
import 'package:intasend_flutter/intasend_flutter.dart';

// How to initiate the checkout widget
Checkout checkout = Checkout(
    publicKey: "<PUBLIC-KEY>",
    amount: 10.01,
    email: "joe@doe.com",
    currency: "USD",
    firstName: "Joe",
    lastName: "Doe");

// Add test to true in sandbox environment. Use false to go live
IntasendFlutter.initCheckout(
    test: true, checkout: checkout, context: context);
```

#### Code example

Check out [https://pub.dev/packages/intasend\_flutter/example](https://pub.dev/packages/intasend\_flutter/example) for a complete code example on initiating checkout view on button press.
