---
title: Understanding Declines and Failed Payments
bookToc: true
---

# Understanding Declines and Failed Payments
***

During a payment process, a failure result can happen because of the typical reasons. For example, the customer may not have enough money on a bank card, or PaySuper Checkout may suspect a fraud attempt. If so, the payment status will be cancelled and a PaySuper Checkout notification event will contain an explanatory description.

But some reasons for the failed payments are unclear and uninformative. Moreover, for many alternative payment methods (APM) it’s hard to investigate the payment decline reasons. In PaySuper we continuously work to reduce the decline rates both for cards and APM. For instance, one of the most interesting issues is the decline by Card Issuer bank. In this case, we are working with each bank with a high decline rate to find workaround to solve the problem. As well as using local gateways to process a card payment only with high potency local gateways and banks.

We highlight the common possible reasons for the failed payments:

* [Payment declined by card issuers or APM](/docs/payments/declines/#payment-declined-by-card-issuers-or-apm)
* [Payment blocked due to suspected fraud](/docs/payments/declines/#payment-blocked-due-to-suspected-fraud)

In most cases, each type of failure is variously handled. To help you better understand what happened, the reason for a payment’s failure is provided within the payment’s details opened from the [Transactions](https://paysupermgmt.tst.protocol.one/transactions) page.

## Payment declined by card issuers or APM

Usually, the issuer of your customer’s card have automated systems or risk models which determine whether or not to authorize it when a charge is submitted. Black and white lists, your customer’s spending habits, account balance and a card information like the expiration date, cardholder and CVC are taken into account. You can find the decline reason for your customer’s card issuer in the transaction details from the [Transactions](https://paysupermgmt.tst.protocol.one/transactions) page or in the [webhook](/docs/payments/webhooks/) event `payment.canceled`.

Unfortunately, most of the declines are reported as “generic”. So it’s not always possible to know exactly why a payment was declined. Especially for a payment that was processed with APM. For privacy and security, card issuers can only discuss the specifics of the declined payment with their cardholders but not with the merchant or PaySuper team. If you are sure that card information is correct, it’s perfect to have your customer contact his card issuer to get more information about the decline.

## Restriction on geographic location

Some customers find that their cards have restrictions on the type of purchases they make. For example, purchases from certain countries or outside of their own can be disallowed. The decline rates is increased if your customer do a payment in a country differs from his card issued country.

## Reducing the card issuer declines

One of the approaches to reduce card issuer declines is to handle responses about incorrect card information (e.g., incorrect cardholder name or expiration date). Thus, PaySuper Checkout provides a set of error handlers that allows users to correct their data and proceed with the payment process.

PaySuper Checkout collects additional customers’ data such as CVC/CVV and postal code that is strongly decreasing a card issuers’ suspicions of fraudulent activity. Moreover, using 3D Secure for payments authentication and a user’s billing address may decrease decline rates in many countries.

## Payment blocked due to suspected fraud

PaySuper uses the self-developed fraud prevention system with cascade checks across our own and partners’ systems. Being the PCI DSS certified provider we can share data with other certified fraud protection systems to check any high-risk classified your customers’ payments. A blocked payment couldn’t be processed successfully and would be declined on an initial stage.

Fraud prevention system based both on black and white lists of customers details, score-based analysis and manages not only the payment admission reasons but also a level and need to use of 3D Secure for card payments.

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}