---
title: Checkout Overview
bookToc: true
---

# PaySuper Checkout

PaySuper Checkout creates a secure PaySuper-hosted form that lets you collect payments with just a few lines of code. The PaySuper Form loads near instantly and is designed to boost your paying conversion rate.

***

{{< load-photoswipe >}}

{{< figure src="/images/products-dark-form.png">}}

## PaySuper Checkout features:

- **Payment methods:** VISA, Master Card, AMEX, JCB, China UnionPay, Bitcoin payments, Alipay, QIWI, Bank Wire Transfers.
- **Payment types:** Simple Checkout, Products, Game Keys.
- **Authentication:** Dynamic 3D Secure.
- **Localization:** Localized for 2 languages with 10 more translations coming soon.
- **Email receipts:** Automatic email receipts right to your customers' inbox.
- **Automated calculations:** Automatically calculates the VAT due on your orders.
- **Conversion-optimized:** The payment form loads instantly with a single-page layout.

***

## See how PaySuper Checkout form looks and feels

{{< columns >}}
### Try PaySuper Checkout now
Choose one of the test cards below to checkout in a test mode:

Default card: **`4000 0000 0000 0002`**

3D Secure: **`4000 0000 0000 0077`**

Enter arbitrary cardholder name, expiry date and CVV2/CVC2/CAV2 (Secure code) with these PANs.

{{< button href="https://paysupermgmt.tst.protocol.one/form-demo" >}}Test Payment{{< /button >}}

<--->

### See the demo project
Try out [the payment sample](ССЫЛКА НА ПРИМЕР ФОРМЫ, та же что выше) or see [the code on GitHub](ПРИМЕР КОДА и КАК ЕГО ЗАПУСКАТЬ).
{{< /columns >}}

***

## Getting Started
PaySuper Checkout form currently supports one-time payments for products, game keys and a simple checkout option.

 **` type {String}; Available options: 'product', 'simple', 'key' `**

- **[Product Checkout](/docs/payments/product)**

Product checkout works well for games or in-game items.

- **[Simple Checkout](/docs/payments/simple)**

Simple Checkout is designed for payment orders with dynamical pricing, for example, stores that use its e-commerce engine for product management. Likewise, this option works well with non-product payments such as donations or virtual currency. In this mode, you specify the currency and the price, while the payment amount due for the end-user is calculated accordingly to the exchange rate if it differs from the specified order currency.

- **[Keys Checkout](/docs/payments/keys)**

Keys Checkout is best suited to sale game keys for DRM platforms such as Steam, GOG, Uplay, Origin, Xbox, Switch, PSN. In fact, this feature allows you to sell any key-activated products (such as DLCs and expansion packs) that the target DRM platforms support. 
***

## Questions?

{{< columns >}}
#### [Sales](https://docs.google.com/forms/d/e/1FAIpQLScQPU83wKPkJeui_WvxGDoXWLDL4vyD8GsWNqf9-ccwDg3dEw/viewform)
Our sales people are nice and friendly. Leave your contact details, and we'll be back to you in no time. 

<--->

#### [Support](https://docs.google.com/forms/d/e/1FAIpQLScQPU83wKPkJeui_WvxGDoXWLDL4vyD8GsWNqf9-ccwDg3dEw/viewform)
We are always happy to help with a code, improve a guide or consider a feature.

<--->

#### [GitHub](https://github.com/paysuper)
The PaySuper Checkout form, the JS SDK and even the server are available as a source code on our GitHub. You're welcome to explore the code and help us make PaySuper even better.

{{< /columns >}}
