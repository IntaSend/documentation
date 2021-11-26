---
description: Capture real-time events and send them to your backend for further processing.
---

# WebHooks

## What is a webhook and how does it work?

Webhooks are user-defined callbacks that receive messages based on events triggered in the system.

Webhooks enable real-time updates of third-party systems as they are triggered and sent out immediately based on events. You can set up webhooks endpoints/URLs on your IntaSend dashboard to receive real-time POST notifications on the following changes:

* Changes on payment collections i.e new transactions and state changes
* Refund activities i.e new refunds, and changes in status
* Send money states - get events on a new transaction, and change in status of every transaction.

With webhook, you are able to update your application or CRM in real-time and without having to do a pull request to query for statuses. We'll send it to the URL that you received.

### Webhooks requirements

For webhooks to work well, you must:

* A valid URL/endpoint that accepts POST request
* They endpoint must use a secure transport protocol i.e HTTPS
* Consider implementing a queue mechanism on your end especially if your site received a lot of traffic. This is important to optimize your system to capture all messages from IntaSend and process other resource-intensive tasks like sending emails, reconciliations, etc.

IntaSend will try and send all the events that you have subscribed to. In case we are not able to deliver, our system will try to send the same request five more times with exponential delays. This means we will send the first request after 5 minutes, then the second retry after 20 minutes, and keep increasing the delay until we reach the maximum retries threshold.
