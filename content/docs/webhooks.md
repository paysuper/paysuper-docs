---
title: Webhooks
bookToc: true
---

# Webhooks
***

The PaySuper system can send you notifications for a set of events during the flow, such as creating new accounts or transaction flow, making payouts, and so on.

These notifications are sent as webhooks to the corresponding URL configured on your Project Webhook page.

In most cases, webhooks are triggered by user actions on your website or back-end related events like a successful payment, refund payment and other.

## Setting up a webhook

**1.** Add the URL of the server that will receive the webhook requests in the Functional URL section on the Project Webhooks page.

**2.** [Verify the webhook request](/docs/payments/webhooks/#verifying-a-webhook).

**3.** Respond with HTTP code 200 without a message body to acknowledge the receipt a webhook. 

## Webhook event types

Type|Payload|Description
---|---|---
`payment.success`|Order|Sent when a customer successfully completes a payment.
`payment.chargeback`|Order|Sent when a payment must be cancelled for a chargeback.
`payment.refund`|Order|Sent when a payment must be cancelled for refund for any reasons.
`payment.cancel`|Order|Sent when a payment must be cancelled for cancel for any reasons.

## The Webhook object

Attribute|Type|Description
---|---|---
`id`|string| Unique identifier for the object.
`type`|string| String representing the webhook's type.
`event`|string| String representing the event's type.
`live`|boolean| Equals to `true` if notification originated from the live environment.
`created_at`|DateTime|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) when an event has been created.
`expires_at`|DateTime|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) when the event stops trying to deliver.
`delivery_try`|integer|The current delivery try for this event.
`object`|object| The object representing payload of event with a given type. Objects of the same type share the same value.

## The Webhook object example

For instance, this is the base object representing the webhook event `payment.success`:

{{< highlight json >}}
{
   "id": "b303ec344deca48af01f3412d51af2198207f5bfff549bbdfffac46d971fc725",
   "type": "notification",
   "event": "payment.success",
   "live": true,
   "created_at": "2019-10-31T16:01:41Z",
   "expires_at": "",
   "delivery_try": 0,
   "object": {
      "id": "f29ab03a-c5f0-40db-a798-9deba14a9099",
      "transaction": "302212411",
      "object": "order",
      "status": "created",
      "description": "Payment by order # 5dbb050f662d2d0001704b03",
      "created_at": {
         "seconds": 1572537615,
         "nanos": 242000000
      },
      "canceled_at": {
         "seconds": -62135596800
      },
      "canceled": false,
      "cancellation_reason": "",
      "refunded": false,
      "refunded_at": {
         "seconds": -62135596800
      },
      "receipt_email": "michael.kirpa@gmail.com",
      "receipt_phone": "",
      "receipt_number": "",
      "receipt_url": "",
      "agreement_version": "",
      "agreement_accepted": false,
      "notify_sale": false,
      "notify_sale_email": "",
      "issuer": {
         "url": "",
         "embedded": false
      },
      "amount": 0.12,
      "currency": "USD",
      "user": {
         "id": "U3oFCwIOwRnQzfKZn58fnkzx3xnPGYdP",
         "object": "user",
         "external_id": "",
         "name": "",
         "email": "michael.kirpa@gmail.com",
         "email_verified": false,
         "phone": "",
         "phone_verified": false,
         "ip": "80.91.180.90",
         "locale": "ru",
         "address": {
            "country": "UA",
            "city": "Dublin",
            "postal_code": "D02",
            "state": "L"
         },
         "metadata": null,
         "notify_new_region": false,
         "notify_new_region_email": ""
      },
      "billing_address": {
         "country": "AO"
      },
      "tax": {
         "type": "vat",
         "currency": "USD"
      },
      "method": {
         "title": "VISA/MasterCard",
         "external_id": "BANKCARD",
         "params": {
            "currency": "USD",
            "terminal_id": "52195",
            "secret": "167CjmMJY2fl",
            "secret_callback": "wBR54pLIfo19"
         },
         "payment_system_id": "5be2d0b4b0b30d0007383ce5",
         "saved": false,
         "card": {
            "first6": "414943",
            "last4": "2348",
            "masked": "414943...2348",
            "expiry_month": "10",
            "expiry_year": "2021",
            "brand": "VISA",
            "fingerprint": "$2a$04$O5T96ZeHx27HbLw0eXNUjO1sj4y0nnPKLsXy5Kw49iLC/EXCFfUzq",
            "secure3d": true
         },
         "wallet": null,
         "crypto_currency": null
      },
      "items": null,
      "refund": null,
      "metadata": null,
      "country": "AO",
      "type": "simple",
      "platform_id": ""
   }
}
{{< /highlight >}}

## Verifying a webhook

PaySuper signs the webhook events it sends to your endpoint, allowing you to validate that they were not sent by a third-party and prevent hacker attacks.

The PaySuper API uses a Secret key to check a notification request. 

{{< hint warning >}}
Your Secret keys carry many privileges, so be sure to keep them secure! Do not share your Secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.
{{< /hint >}}

**To check a digital signature:**

**1.** Concatenate the request's JSON body with your Project's Secret key found on the Project webhooks page.

**2.** Apply SHA-256 hashing to the resulting string. 

**3.** Compare the digital signature with [Authorization](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization) HTTP Header value in the received notification:

> All API requests must be made over HTTPS. Calls made over a plain HTTP will fail. API requests without the authentication will also fail.

{{< highlight http >}}
POST /your_endpoint HTTP/1.1
Host: your.host
Accept: application/json
Content-Type: application/json
Authorization: Signature sh9b1r69bjqie88n5uizqcrerhee50dypsp195mh
{{< /highlight >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}