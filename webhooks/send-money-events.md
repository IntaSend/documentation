---
description: Send money events fields and example
---

# Send money events

Send money event payload will be sent to you in real-time every time when the **`status`** field changes. Please ensure you have validated the challenge provided.

#### Payload example

```
{
  "tracking_id": "7e96bc5c-191c-40bd-94f2-be4a0226c69c",
  "status": "Preview and approve",
  "transactions": [
    {
      "status": "Pending",
      "request_reference_id": "66aa1c24-a698-409f-9372-3ea55dc32af8",
      "provider": "MPESA-B2C",
      "name": "John Doe",
      "account": 254708374149,
      "amount": "100.00",
      "narrative": "Webhook test"
    }
  ],
  "actual_charges": 0,
  "paid_amount": 0,
  "failed_amount": 0,
  "created_at": "2021-08-18T12:23:55.378709+03:00",
  "updated_at": "2021-08-18T12:23:55.502828+03:00",
  "challenge": "testnet"
}
```

Status field reference

| Status               | Description                                                                                      |
| -------------------- | ------------------------------------------------------------------------------------------------ |
| Preview and Approve  | Batch pending approval state                                                                     |
| Confirming balance   | Confirming account balance                                                                       |
| Processing (FLT)     | Preparing processing on IntaSend side                                                            |
| Failed Processing    | Failed to process the transactions - end early                                                   |
| Processing (FLTRSLT) | Continuer processing on IntaSend side                                                            |
| Sending payment      | Sending payment requests to providers e.g M-Pesa                                                 |
| Processing payment   | Post send payment checks and updates                                                             |
| Completed            | Completed processing the batch - check individual transactions for status i.e failed or complete |
