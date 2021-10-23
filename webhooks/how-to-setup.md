---
description: How to setup your webhook destination URL.
---

# How to set up a webhook

## What are webhooks?

_**Webhooks**_ are automated messages sent from apps when something happens. They have a message—or payload—and are sent to a unique URL.

IntaSend supports webhooks where we send collection, send money, and chargeback events whenever the object's state changes.

Webhook events can be used to validate payments transactions, log collections, and chargeback actions in real-time.

## Add your destination URL

From the IntaSend dashboard, select Webhooks and set up your endpoint URL, and provide a challenge. Use the provided challenge to validate requests from IntaSend. We store this in an encrypted manner. To ensure maximum security between IntaSend and your backend, please ensure the provided endpoint uses HTTPS  protocol.

![](<../.gitbook/assets/image (24).png>)

### Managing requests and failure

To ensure the service works well and efficiently, we recommend that the provided endpoint be up around the clock. The webhook will deactivate if IntaSend fails to send more than 20 subsequent requests to the endpoint. You can only re-activate by contact customer support. Please ensure that your endpoint is back up and running before contacting customer support.

