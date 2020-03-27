---
title: Customizing Checkout
bookToc: true
---

# Customizing Checkout
***

Learn about the different ways you can customize your Checkout.

- [Localization](#localization)
- [Prefilling customer data](#prefilling-customer-data)
- [Displaying VAT in a payment form](#displaying-vat-in-a-payment-form)
- [Saving payment methods for future](#saving-payment-methods-for-future)
- [Customizing theme](#customizing-theme)
- [Customizing the colors](#customizing-the-colors)
- [Analytics Integration](#analytics-integration)

***

## Localization

`Dashboard`

The Checkout Form is localized for [24 languages](/docs/payments/localization).

You can choose the complete set of supported languages for the project and products descriptions on the Project Settings page in your PaySuper Dashboard.

## Prefilling customer data

`Token`

Boost your payment conversion rate with a payment form pre-filled with your customer's name and email. To have the payment form prefilled, you can generate a token to encrypt all required information about your customer's intent to pay.

## Displaying VAT in a payment form

`Dashboard`

[Get to know about VAT for e-services of foreign companies.](/docs/vat)

You can configure your Project Settings to display the total price and VAT in a payment form and receipt.

To show the total price with VAT already included, choose "VAT included in price" on the Project Settings page in your PaySuper Dashboard. 
By default, PaySuper displays a calculated VAT and product price separately in a payment form.

{{< figure src="/images/vat-settings.png">}}

As the example below shows, if the in-game purchase is $10 and you apply "VAT included in price" then the total price will be equal to the same $10 in a payment form. 
By default, your customers see the total price with added taxes, for example, if the in-game purchase is $10 with VAT 20% then the total price is $12.

{{< figure src="/images/vat-included.gif">}}

## Saving payment methods for future

PaySuper can securely store your customer's billing address and the payment method data to prefill the Checkout Form with. The customer has to agree for this to happen.

## Customizing theme

`PaySuper JS SDK`

{{< highlight javascript >}}
const paySuper = new PaySuper({
    viewScheme: 'light'
});
{{< /highlight >}}

Available options: **`dark`** (default), **`light`**.

{{< figure src="/images/themes-form.gif">}}

## Customizing the colors

`PaySuper JS SDK`

{{< highlight javascript >}}
const paySuper = new PaySuper({
    viewSchemeConfig: { 
        // headerTextColor overrides the default value of the viewSchemeConfig object
        headerTextColor: '#333333'
    }
});
{{< /highlight >}}

[Available parameters of **`viewSchemeConfig`**](https://github.com/paysuper/paysuper-js-sdk/blob/master/docs/CUSTOMIZATION.md#available-parameters-of-viewschemeconfig)

{{< figure src="/images/colors-form.gif">}}

## Analytics Integration

`PaySuper JS SDK`

Nowadays we set up a Google Analytics data collection in a test mode inside PaySuper. After the Beta testing, we'll release the [analytics integration](/docs/analytics-integration) to use with a customer's tracking ID.

***

## Next steps

{{< hint info >}}
[**After the payment**](/docs/payments/fulfillment/)

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