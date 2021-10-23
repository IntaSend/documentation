---
description: Chargeback events example
---

# Chargeback events

Chargeback event payload will be sent to you in real-time every time when the **`status`** field changes. Please ensure you have validated the challenge provided.

#### Payload example

```
{
  "chargeback_id": "VYBBVY4",
  "transaction": {
    "invoice": {
      "invoice_id": "VQ3X4OY",
      "state": "COMPLETE",
      "provider": "CARD-PAYMENT",
      "charges": "3.63",
      "net_amount": "100.00",
      "currency": "KES",
      "value": "103.63",
      "account": "cynthia@talklift.com",
      "api_ref": "ISL_faa26ef9-eb08-4353-b125-ec6a8f022815",
      "host": "https://sandbox.intasend.com",
      "failed_reason": null,
      "failed_code": null,
      "failed_code_link": "https://intasend.com/troubleshooting",
      "created_at": "2021-08-17T09:27:36.742159+03:00",
      "updated_at": "2021-08-17T09:28:26.654541+03:00"
    },
    "value": "103.63",
    "running_balance": "1898301.65",
    "narrative": "ISL_faa26ef9-eb08-4353-b125-ec6a8f022815",
    "created_at": "2021-08-17T09:28:26.271766+03:00",
    "updated_at": "2021-08-18T12:20:20.852267+03:00"
  },
  "invoice": {
    "invoice_id": "VQ3X4OY",
    "state": "COMPLETE",
    "provider": "CARD-PAYMENT",
    "charges": "3.63",
    "net_amount": "100.00",
    "currency": "KES",
    "value": "103.63",
    "account": "cynthia@talklift.com",
    "api_ref": "ISL_faa26ef9-eb08-4353-b125-ec6a8f022815",
    "host": "https://sandbox.intasend.com",
    "failed_reason": null,
    "failed_code": null,
    "failed_code_link": "https://intasend.com/troubleshooting",
    "created_at": "2021-08-17T09:27:36.742159+03:00",
    "updated_at": "2021-08-17T09:28:26.654541+03:00"
  },
  "amount": "103.63",
  "reason": "Unavailable service",
  "status": "PENDING",
  "resolution": null,
  "staff_created": false,
  "created_at": "2021-08-18T12:20:20.858491+03:00",
  "updated_at": "2021-08-18T12:20:20.858509+03:00",
  "challenge": "testnet"
}
```

#### Status field reference

| Value     | Description                                                                      |
| --------- | -------------------------------------------------------------------------------- |
| PENDING   | Chargeback has just been recorded                                                |
| CANCELLED | The Chargeback request has been canceled                                         |
| DISPUTED  | A dispute has been recorded against the chargeback                               |
| OVERDUE   | The chargeback has been marked as delayed. Urgent action is needed to settle it. |
| COMPLETED | The chargeback issue has been resolved and closed successfully.                  |
