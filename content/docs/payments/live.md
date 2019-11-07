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

## Fill in the info about your Project

`Dashboard`

Choose the complete set of supported languages for the project and product descriptions on the Projects page in your PaySuper Dashboard. Fill in localised project and products descriptions. These will be listed on the payment form and customer receipt emails.

## Prefill the customer data

`Token`

You can use a [token](/docs/payments/token/) to prefill the Checkout Form with all required information about your customer for the payment.

## Fill in Redirect URLs

`Dashboard`

Check your Redirect URLs found in the Payment form menu under Project in the PaySuper Dashboard. You can set what would your customers see after a successful or a failed payment.

{{< figure src="/images/redirect-urls.png">}}

## Customize the PaySuper Form

`PaySuper JS SDK`

You can add your branding colors to the Checkout Form [view scheme](https://github.com/paysuper/paysuper-js-sdk/blob/master/docs/CUSTOMIZATION.md#available-parameters-of-viewschemeconfig).

## Fulfill the purchases

`Webhooks`

You can manually fulfil a purchase by looking into [Transaction Search](/docs/payments/fulfillment/#fulfilling-purchases-with-the-dashboard) in your PaySuper Admin. Or you can create a handler for the [webhook](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks) events and execute your server-side code to fulfill payments.

***

## Next steps

{{< hint info >}}
[**Testing the Checkout**](/docs/payments/testing/)

Verify that your integration with PaySuper Checkout works correctly. Our offered test cards can be used to create payments that produce defined responses for you to test your integration code.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}
