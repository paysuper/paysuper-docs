---
title: Customizing Checkout
bookToc: true
---

# Customizing Checkout
***

Learn about the different ways you can customize your Checkout.

## Localization

The Checkout Form is localized to 2 languages with 10 more translations coming soon.

You can choose the complete set of supported languages for the project and products descriptions on the Project Settings page in your PaySuper Dashboard.

## Prefilling customer data

Boost your payment conversion rate with a payment form pre-filled with your customer's name and email. To have the payment form prefilled, you can generate a token to encrypt all required information about your customer's intent to pay.

## Saving payment methods for future

PaySuper can securely store your customer's billing address and the payment method data to prefill the Checkout Form with. The customer has to agree for this to happen.

## Customizing theme

{{< highlight javascript >}}
const paySuper = new PaySuper({
    viewScheme: 'light'
});
{{< /highlight >}}

Available options: **`dark`** (default), **`light`**.

## Customizing the colors

{{< highlight javascript >}}
const paySuper = new PaySuper({
    viewSchemeConfig: { 
        // headerTextColor overrides the default value of the viewSchemeConfig object
        headerTextColor: '#333333'
    }
});
{{< /highlight >}}

[Available parameters of **`viewSchemeConfig`**](https://github.com/paysuper/paysuper-js-sdk/blob/192153-quickstart/docs/CUSTOMIZATION.md#available-parameters-of-viewschemeconfig)

***

## Next steps

{{< hint info >}}
[**After the payment**](/docs/payments/live/)

After a successful payment, you have to fulfil the customer’s purchase. You can use [webhooks](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks) or the [Transactions](/docs/payments/fulfillment/#fulfilling-purchases-with-the-dashboard) to accomplish the purchase.
{{< /hint >}}

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