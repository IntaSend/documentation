---
description: Payment results are returned by the events emitter.
---

# Payment results

IntaSend SDK event returns results with details like api\_ref, charges incurred, etc.

```bash
new window.IntaSend({
    publicAPIKey: "<REPLACE-WITH-YOUR-PUBLISHABLE-KEY>",
    live: false //set to true when going live
})
.on("COMPLETE", (results) => console.log(results))
.on("FAILED", (failed_results) => console.log(failed_results))
```

Below is a sample result returned for your reference. 

```javascript
{
    "tracking_id": "NLSK100",
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

