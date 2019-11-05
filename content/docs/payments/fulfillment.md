---
title: After the payment
bookToc: true
---

# After the payment
***

When your customers successfully complete payments they are redirected to the success URL page that you passed in a request parameter. Typically, this is a page on your website that informs your customer that their payment was successful.

To fulfil the customer’s purchase you can make it in several ways:

[**Fulfilling purchases manually with the PaySuper Dashboard**](/docs/payments/fulfillment/#fulfilling-purchases-with-the-dashboard)

[**Fulfilling purchases automatically with webhooks**](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks)

[**Email receipts**](/docs/payments/fulfillment/#payment-or-refund-receipts)

## Fulfilling purchases with the PaySuper Dashboard

Every customers' payment is recorded as a new entry in the payments log shown on the [Transactions page](https://paysupermgmt.tst.protocol.one/transactions).

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

After the payments, PaySuper can send you webhook events to your server. You can create a handler for the webhook events like a successful payment, refund payment and so on.

Using the handler you can obtain information from the webhook's `object` parameter in the payload about the customer and payment. With this comprehensive data, you can execute your server-side code and fulfil the payment.

{{< hint warning >}}
[Configure Webhooks](/docs/payments/webhooks/) for your Project in PaySuper Dashboard and handle them on your server.
{{< /hint >}}

For instance, this is the base object representing the webhook event `payment.success`:

{{< highlight json >}}
{
   "id": "b303ec344deca48af01f3412d51af2198207f5bfff549bbdfffac46d971fc725",
   "type": "notification",
   "event": "payment.success",
   "created_at": "2019-10-01T15:10:51Z",
   "object": {
      "id": "f29ab03a-c5f0-40db-a798-9deba14a9099",
      "transaction": "302212411",
      "object": "order",
      "status": "created",
      "amount": 100,
      "currency": "USD",
      "type": "simple",
      "user": {
         "id": "U3oFCwIOwRnQzfKZn58fnkzx3xnPGYdP",
         "object": "user",
         "email": "user.email@example.com",
         "email_verified": true,
         ...
      },
      "method": {
         "title": "VISA/MasterCard",
         "card": {
            "masked": "414943...2348",
            "expiry_month": "10",
            "expiry_year": "2021",
            "brand": "VISA",
            ...
         },
      },
      ...
   }
}
{{< /highlight >}}

## Email receipts

**Payment or refund receipts**

PaySuper automatically sends email receipts to your customers whenever they make a successful payment or refunded purchase. 

It's required for user to fill in an email field on the Checkout form. Besides, you can pass a customer's email address when making the [API Tokens](/docs/api/#tag/Token) or [API Order](/docs/api/#tag/Payment-Order) requests for payment initiation.

**Key-product receipts**

For a [key-activated product](/docs/payments/#products-checkout) purchase, your customer gets an email with the receipt and an extra email with a purchased product key.

If your customer has purchased several game keys for different DRM platforms, he gets an email per DRM platform with a game key and instructions on how to activate the key on the target DRM store.

***

## Next steps

{{< hint info >}}
[**Testing the Checkout**](/docs/payments/testing/)

Verify that your integration with PaySuper Checkout works correctly. Our offered test cards can be used to create payments that produce defined responses for you to test your integration code.
{{< /hint >}}

{{< hint info >}}
[**Going live checklist**](/docs/payments/live/)

You can inspect this checklist before going live to ensure you've implemented all the significant setup steps.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}