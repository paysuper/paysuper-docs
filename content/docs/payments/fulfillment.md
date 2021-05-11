---
title: After the payment
bookToc: true
---

# After the payment
***

When your customers successfully complete payments they are redirected to the success URL page that you passed in a request parameter. Typically, this is a page on your website that informs your customer that their payment was successful.

To fulfil the customer’s purchase you can make it in several ways:

[**Fulfilling purchases manually with the Unlimint Game Services Dashboard**](/docs/payments/fulfillment/#fulfilling-purchases-with-the-paysuper-dashboard)

[**Fulfilling purchases automatically with webhooks**](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks)

[**Email receipts**](/docs/payments/fulfillment/#email-receipts)

## Fulfilling purchases with the Unlimint Game Services Dashboard

Every customers' payment is recorded as a new entry in the payments log shown on the [Transactions page](https://dashboard.pay.super.com/transactions).

All your customers' transactions are organised by Products, Dates and other payment parameters.

{{< figure src="/images/transactions.png">}}

### The transaction details

To manually fulfil the customer's purchase you can click a specified record to dive into transaction card to see additional details.

### Manually refund a purchase

Also, you can manually request a refund a processed transaction from the Transactions page or a transaction card.

### Filter transactions and download

If it's necessary to use the transactions data in an external analytics tool just export the list of transactions per period in an appropriate format pdf, xls or csv.

{{< figure src="/images/transaction-card.png">}}

## Fulfilling purchases with webhooks

After the payments, Unlimint Game Services can send you webhook events to your server. You can create a handler for the webhook events like a successful payment, refund payment and so on.

Using the handler you can obtain information from the webhook's `object` parameter in the payload about the customer and payment. With this comprehensive data, you can execute your server-side code and fulfil the payment.

{{< hint warning >}}
[Configure Webhooks](/api/#webhooks) for your Project in Unlimint Game Services Dashboard and handle them on your server.

After webhooks enabled, [follow this instruction to test your notifications](/docs/payments/testing/#webhooks).
{{< /hint >}}

For instance, this is the base object representing the webhook event `payment.success`:

{{< highlight json >}}
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
    "canceled_at": "2019-07-10T15:17:12.341Z",
    "canceled": true,
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
    "issuer": null,
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
      ...
    },
    "type": "simple",
    "platform_id": "",
    "receipt_id": "efefc5d3-c2e2-4157-8789-4bfb7c1eec34",
    ...
  }
}
{{< /highlight >}}

## Email receipts

**Payment or refund receipts**

Unlimint Game Services automatically sends email receipts to your customers whenever they make a successful payment or refunded purchase. 

It's required for user to fill in an email field on the Checkout form. Besides, you can pass a customer's email address when making the [API Tokens](/api/#create-a-token) or [API Order](/api/#create-a-payment-order) requests for payment initiation.

**Key-product receipts**

For a [key-activated product](/docs/payments/#products-checkout) purchase, your customer gets an email with the receipt and an extra email with a purchased product key.

If your customer has purchased several game keys for different DRM platforms, he gets an email per DRM platform with a game key and instructions on how to activate the key on the target DRM store.

***

## Next steps

{{< hint info >}}
[**Testing the Checkout**](/docs/payments/testing/)

Verify that your integration with Unlimint Game Services Checkout works correctly. Our offered test cards can be used to create payments that produce defined responses for you to test your integration code.
{{< /hint >}}

{{< hint info >}}
[**Going live checklist**](/docs/payments/live/)

You can inspect this checklist before going live to ensure you've implemented all the significant setup steps.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}