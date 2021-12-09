---
description: List of options you can provide to improve the user check out experience.
---

# Payment data parameters

## List of payments payload fields

The following options can be parsed to the payment button during integration using the `data-*` attribute e.g `data-email="user@example.com"`. If any of this data is available, it is highly recommended that you provide them so that we can shorten the payment form and provide a better user experience. Customers will not be prompted to provide this information once if already been added.

This schema is also useful for [custom button integration](using-a-custom-button.md).

| Parameter      | Description                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| currency       | Recommended: Options are USD, KES, GBP, EUR                                                                                      |
| amount         | Optional. If not defined customers will have the option to specify how much they want to pay                                     |
| phone\_number  | Optional. Customers will be prompted if required e.g M-Pesa payment                                                              |
| email          | Optional. Customers will be prompted if required e.g card payments                                                               |
| api\_ref       | Recommended - Tracking reference for own use.                                                                                    |
| comment        | Optional customer comment if any                                                                                                 |
| first\_name    | Optional customer first name                                                                                                     |
| last\_name     | Optional customer last name                                                                                                      |
| country        | Optional country code e.g US, BR, KE, etc                                                                                        |
| address        | Optional user billing address                                                                                                    |
| city           | Optional user billing city                                                                                                       |
| state          | Optional user billing state                                                                                                      |
| zipcode        | Optional user billing zipcode                                                                                                    |
| method         | Optional - if specified only the method will be used. Options are M-PESA, CARD-PAYMENT. Leave blank to show all payment methods. |
| card\_tarrif   | options are **BUSINESS-PAYS** and **CUSTOMER-PAYS** . Specify who pays the card charges. Set to BUSINESS-PAYS by default         |
| mobile\_tarrif | options are **BUSINESS-PAYS** and **CUSTOMER-PAYS** . Specify who pays the mobile charges. Set to BUSINESS-PAYS by default       |
| redirect\_url  | Optional URL where we should redirect the user on payment success                                                                |
