---
title: API Reference
---

# Introduction

The PaySuper API is organized around REST. Our API is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP verbs, which can be understood by off-the-shelf HTTP clients.
JSON will be returned in all responses from the API, including errors.

All API requests must be made over **HTTPS**.

# Authentication

Authentication to the API occurs via Signature-based authentication. You must authenticate for all requests that contain a user data.

Add a Header **X-API-SIGNATURE** with the Project's Secret key found on the Project webhooks page.

<aside class="notice">
Your API keys carry many privileges, so be sure to keep them secret.
</aside>

# Errors

PaySuper uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing, a charge failed, etc.), and codes in the 5xx range indicate an error with PaySupers's servers.

**HTTP status codes summary:**

**200 OK** - Everything worked as expected.

**201 Created** - Resource has been successfully created

**202 Accepted** - Request has been accepted, but requires asynchronous work to be fully performed

**400 Bad Request** - Request failed due to a combination of errors

**401 Unauthorized** - No valid API credentials provided.

**402 Payment Required** - Your request was in Live Mode while your account is not activated for Live requests yet.

**403 Forbidden** - You are not authorized to access the requested item.

**404 Not Found** - The requested item doesn't exist.

**406 Unacceptable** - Your request format was not supported. Use JSON.

**409 Conflict** - The data you submitted is in conflict with existing data.

**422 Unprocessable Entity** - Often missing a required parameter.

**429 Too Many Requests** - You sent us too many API requests in a row. Please retry later.

**500, 502, 503, 504 Server errors** - Something went wrong on PaySupers's end.

# Versioning

PaySuper is developed incrementally. We use [semantic versioning](https://semver.org/) and approach to release new versions of the specification.

The content of each release is the result of the work of the project team located on GitHub. 
All changes and additions to each version of this specification are publicly discussed by the PaySuper working group.

While making requests in PaySuper using HTTPS, the version is passed as a special HTTP header, which makes it easier to choose the correct implementation of objects on the receiving and transmitting side. 
The version passed is specified as major and minor of the version using semantic versioning. 

For the transmission version must use the header `'x-paysuper-api-version': '1.0'`.

# Compression

The amount of data transferred with notifications can be huge, and endpoints are required to support data compression to reduce the amount and speed of data transfer over the network.

Endpoints that send HTTP 1.1 messages are required to send gzip-compressed data by specifying the appropriate value in the HTTP [Accept-Encoding header](https://tools.ietf.org/html/rfc7231#section-5.3.4).

Receiving hosts are required to support gzip and respond to requests by passing an HTTP [Content-Encoding header](https://tools.ietf.org/html/rfc7231#section-3.1.2.2).

# Pagination

<aside class="warning">
Implemention of the pagination is in progress.
</aside>

> Example request

```shell
$ curl https://api.pay.super.com/payouts?limit=3 \
   -u tkHCYYOUVrYyY5rBFZxNzgtt:
```

> Example response

```json
{
  "object": "list",
  "has_more": true,
  "has_before": false,
  "total_count": 240,
  "data": [
    {
      "id": "po_1ED765CmSJsu7cy1iQZUkPKz",
      "object": "payout",
      "type": "bank_account",  
      "status": "in_transit",
      "created_at": "2018-07-10T14:27:54.691Z",
      "arrival_date": "2018-07-10T14:27:54.691Z",
      "amount": "2.00",
      "currency": "USD",
      "payout_url": "https://pay.super.com/receipts/long-id-string-for-receipt",
      "automatic": true,
      "description": "PAYSUPER PAYOUT",
      "destination": "ba_1ED765CmSJsu7cy1ZufOeBtW",
      "failure_balance_transaction": null,
      "failure_code": null,
      "failure_message": null,
      "live": false,
      "metadata": {}
    },
    {...},
    {...}
  ]
}
```

All top-level PaySuper API resources have support for bulk fetches "list" API methods. For instance, you can list users, list orders.
Like Stripe, PaySuper uses cursor-based pagination using the parameter `starting_after`. Pass `starting_after` parameter 
at the previous page last object id value to determine where to start in the list.

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`limit`|integer|A limit on the number of objects to be returned. Must be included between 1 and 100.|
|`starting_after`|string|A cursor for use in pagination. `starting_after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with `obj_foo`, your subsequent call can include `starting_after=obj_foo` in order to fetch the next page of the list.|
|`ending_before`|string|A cursor for use in pagination. `ending_before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with `obj_bar`, your subsequent call can include `ending_before=obj_bar` in order to fetch the previous page of the list.|

### Response

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`object`|string|The string representing the object’s type. Value: `list`.|
|`data`|array|An array containing the actual response elements, paginated by any request parameters.|
|`has_more`|boolean|Whether or not there are more elements available after this page. If `false`, this page is the end of the list.|
|`has_before`|boolean|Whether or not there are more elements available before this page. If `false`, this page is the beginning of the list.|
|`total_count`|boolean|The total count of all recipients that match your filters, as if there was no pagination.|

# WEBHOOKS

The PaySuper system can send you notifications for a set of events during the flow, such as creating new accounts or transaction flow, making payouts, and so on.

These notifications are sent as webhooks to the corresponding URL configured on your Project Webhook page.

In most cases, webhooks are triggered by user actions on your website or by back-end related events like a successful payment, a refund payment and other.

> The Webhook object examples:
>
>For instance, this is the base object representing the webhook event `payment.success`:

```json
{
  "id": "5d23426ab8b1eea163304202653796fa801081e739d506615ddac583019045f3",
  "type": "notification",
  "event": "payment.success",
  "live": false,
  "created_at": "2019-11-16T05:41:05Z",
  "delivery_try": 0,
  "object": {
    "id": "726d9e07-1dc8-4159-8d52-f95941066bc8",
    "transaction": "2978077",
    "object": "order",
    "status": "created",
    "description": "A summary for the purchase",
    "created_at": "2019-07-10T14:27:54.691Z",
    "canceled_at": "",
    "canceled": false,
    "cancellation": null,
    "refunded": false,
    "refunded_at": "",
    "receipt_email": "user.email@example.com",
    "receipt_phone": "",
    "receipt_number": "",
    "receipt_url": "https://dashboard.pay.super.com/receipt/purchase/efefc5d3-c2e2-4157-8789-4bfb7c1eec34/726d9e07-1dc8-4159-8d52-f95941066bc8",
    "agreement_version": "",
    "agreement_accepted": false,
    "notify_sale": false,
    "notify_sale_email": "",
    "issuer": {
      "url": "https://domain.com",
      "embedded": false,
      "reference": "",
      "reference_type": "",
      "utm_source": "",
      "utm_medium": "",
      "utm_campaign": "",
      "referrer_host": "domain.com"
    },
    "amount": 595,
    "currency": "RUB",
    "user": {
      "id": "5dcf8b24b5a6990001bac2b6",
      "external_id": "0000000000001",
      "name": "User Name",
      "email": "user.email@example.com",
      "email_verified": true,
      "phone": "9112223344",
      "phone_verified": true,
      "ip": "79.137.163.2",
      "locale": "ru-RU",
      "address": {
        "country": "RU",
        "city": "Moscow",
        "postal_code": "127221",
        "state": "MOW"
      },
      "metadata": {
        "user.param1": "user.val1",
        "user.param2": "user.val2",
        "user.param3": "user.val3"
      }
    },
    "billing_address": {
      "country": "DE"
    },
    "tax": {
      "type": "vat",
      "rate": 0.19,
      "amount": 95,
      "currency": "RUB"
    },
    "method": {
      "title": "Bank card",
      "external_id": "BANKCARD",
      "payment_system_id": "5be2d0b4b0b30d0007383ce5",
      "type": "CARD",
      "saved": false,
      "card": {
        "first6": "400000",
        "last4": "0002",
        "masked": "400000...0002",
        "expiry_month": "11",
        "expiry_year": "2023",
        "brand": "VISA",
        "fingerprint": "$2a$04$9VRouYlBC.qMYQrLpmlXOeGbL2WFZDGGq/KdTeeHSfWkosgJgrWw2",
        "secure3d": true
      },
      "wallet": null,
      "crypto_currency": null,
      "refund_allowed": true,
      "recurring_allowed": true
    },
    "items": null,
    "refund": null,
    "metadata": {
      "param1": "val1",
      "param2": "val2",
      "param3": "val3"
    },
    "original_amount": 500,
    "country": "DE",
    "type": "simple",
    "platform_id": "",
    "receipt_id": "efefc5d3-c2e2-4157-8789-4bfb7c1eec34",
    "virtual_currency_amount": 0,
    "is_buy_for_virtual_currency": false,
    "charge_currency": "EUR",
    "charge_amount": 59.99,
    "vat_payer": "buyer",
    "is_production": true,
    "testing_case": false,
    "form_mode": "embed",
    "merchant_info": {
      "company_name": "Company name",
      "agreement_number": "4bfb7c1eec34efefc5d3"
    },
    "net_revenue" : {
        "amount": 10.12,
        "currency": "EUR"
    },
    "fee" : {
        "amount": 1.78,
        "currency": "EUR"
    },
    "recurring": false,
    "recurring_id": ""
  }
}
```

>This example is the base object representing the webhook event `user.validate`:

```json
{
  "id": "79bfd757-bb5a-4754-9d5c-5c7e131e7cf3",
  "type": "notification",
  "event": "user.validate",
  "live": false,
  "created_at": "2020-04-06T21:14:18Z",
  "expires_at": "",
  "delivery_try": 1,
  "object": {
    "id": "5e8b9baa8fba167a4a284572",
    "object": "user",
    "external_id": "bcbb8259-b65e-44bc-ba1d-2a150cc04338",
    "name": "User Name",
    "email": "user.email@example.com",
    "email_verified": true,
    "phone": "9112223344",
    "phone_verified": true,
    "ip": "79.137.163.2",
    "locale": "ru-RU",
    "address": {
        "country": "RU",
        "city": "Moscow",
        "postal_code": "127221",
        "state": "MOW"
    },
    "metadata": {
      "user.param1": "user.val1",
      "user.param2": "user.val2"
    },
    "notify_new_region": false,
    "notify_new_region_email": ""
  }
}
```

### Setting up a webhook

**1.** Add the URL of the server that will receive the webhook requests in the *Functional URL section* on the Project Webhooks page.

**2.** Select the Webhooks mode:

**Default** is the asynchronous mode that provides webhook notifications only about a payment.

**a.** A customer initiates a payment request on your site via the PaySuper payment form.

**b.** If the payment is finished with a successful or failed result PaySuper sends a payment notification to your server.

**Pre-approval** is the mode that provides a synchronous notification for user validation and asynchronous notification about a payment.

**a.** A customer initiates a payment request on your site via the PaySuper payment form.

**b.** PaySuper sends the user validation request with the customer data to check the details of the user on the project side.

**c.** When the project server responds with success or failure, PaySuper continues or cancel the payment respectively for this customer.

**d.** If the payment is finished with a successful or failed result PaySuper sends a payment notification to your server.

**3.** [Verify the webhook request](#verifying-a-webhook).

**4.** Respond with HTTP code 200 without a message body to acknowledge the receipt a webhook notification.

### Webhook event types

|TYPE|PAYLOAD|DESCRIPTION|
|---|---|---|
|`payment.success`|Order|Sent when a customer successfully completes a payment.|
|`payment.chargeback`|Order|Sent when a payment must be cancelled for a chargeback.|
|`payment.refund`|Order|Sent when a payment must be cancelled for refund for any reasons.|
|`payment.cancel`|Order|Sent when a payment must be cancelled for cancel for any reasons.|
|`user.validate`|User|Sent when a customer initiates a payment. It's applied for the pre-approval webhooks mode.|

### The Webhook object

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`id`|string| The unique identifier for the object.|
|`type`|string| The string representing the webhook's type. Value: `notification`.|
|`event`|string| The string representing the event's type.|
|`live`|boolean| Has a value `true` if notification originated from a live environment.|
|`created_at`|DateTime|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) when the event has been created.|
|`expires_at`|DateTime|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) when the event stops trying to deliver.|
|`delivery_try`|integer|The current delivery try for the event.|
|`object`|[Order](#order)| The object representing the payload of the event with a given type. Objects of the same type share the same value.|

## Verifying a webhook

PaySuper signs webhook events that it sends to your endpoint allowing you to validate that they were not sent by a third-party and prevent any unauthorised actions.

The PaySuper API uses a Secret key to check the notification request.

<aside class="notice">
Your Secret keys carry many privileges, so be sure to keep them secure! Do not share your Secret API keys in any publicly accessible areas such as GitHub, client-side code, and so forth.
</aside>

> All API requests must be made over HTTPS. Calls made over a plain HTTP will fail.

```http
POST /your_endpoint HTTP/1.1
Host: your.host
Accept: application/json
Content-Type: application/json
Authorization: Signature sh9b1r69bjqie88n5uizqcrerhee50dypsp195mh
```

**To check a digital signature:**

**1.** Concatenate the request's JSON body with your Project's Secret key found on the Project webhooks page.

**2.** Apply SHA-256 hashing to the resulting string. 

**3.** Compare the digital signature with [Authorization](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization) HTTP Header value in the received notification.