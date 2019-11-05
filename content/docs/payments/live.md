---
title: Going Live
bookToc: true
---

# PaySuper Checkout integration checklist
***

When you’re done with PaySuper Checkout integration and are thinking about going live, we suggest you refer to the points below to check that you've covered all the significant steps.

## Complete the Company onboarding

`Dashboard`

When you are ready to start selling you will need to fill in all your company details in [Company Onboarding](https://paysupermgmt.tst.protocol.one/company) and sign the documents in the License Agreement.

> Before confirming your application we manually check each new account to ensure that our platform is attended only by companies who are related to the gaming industry. This allows us to focus on the relevant features and quality for our users.

## Filling in the info about your Project

`Dashboard`

Choose the complete set of supported languages for the project and products descriptions on the Project Settings page in your PaySuper Dashboard. Fill in localised project and products descriptions. It will be mentioned in a payment form and different customer correspondence.

## Prefilling customer data

`Token`

Use a [token](/docs/payments/token/) to prefill the Checkout Form with all required information about your customer on the payment initialization.

## Redirecting after a payment

`PaySuper JS SDK` `PaySuper API`

Check your redirect URLs for a successful or failed payment are available.

## Customizing PaySuper Form

`PaySuper JS SDK`

Add your branding colors to the Checkout Form [view scheme](https://github.com/paysuper/paysuper-js-sdk/blob/192153-quickstart/docs/CUSTOMIZATION.md#available-parameters-of-viewschemeconfig).

## Fulfiling purchases

`Webhooks`

You can manually fulfil a purchase. Instead, create a handler for the [webhook](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks) events and execute your server-side code to fulfil the payment.

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

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}