---
title: Going Live
bookToc: true
---

# Unlimint Game Services Checkout integration checklist
***

When you’re done with Unlimint Game Services Checkout integration and are thinking about going live, we suggest you refer to the points below to check that you've covered all the significant steps.

## Complete the Company onboarding

`Dashboard`

{{< hint warning >}}
Royalty reports and Payouts disabled before the documents in the License Agreement will be signed by both our sides.
{{< /hint >}}

**1.** Click the *Activate Live Mode button* on Dashboard at the Top menu or Side menu.

{{< figure src="/images/live-mode.png">}}

**2.** Fill in all your company details including the Banking info in [Company Onboarding](https://dashboard.pay.super.com/company).

>Note that the currency of the bank account must be the same as the Account Currency for [payouts](/docs/payouts/) filled in the Banking info.

{{< figure src="/images/fill-company-info.png">}}

**3.** Sign the documents in the License Agreement.

> Before confirming your application we manually check each new account to ensure that our platform is attended only by companies who are related to the gaming industry. This allows us to focus on the relevant features and quality for our users.

**4.** Now, you can enable processing real money within each project after the License Agreement signed:

- Open your project's *Sales options*.
- Enable processing real money for this project by clicking the *Going live toggle switch*.

{{< figure src="/images/project-sales-options.png">}}

## Fill in the info about your Project

`Dashboard`

Choose the complete set of supported languages for the project and products descriptions on the Project Settings page in your Unlimint Game Services Dashboard. Fill in localised project and products descriptions. These will be listed on the payment form and customer receipt emails.

## Prefill the customer data

`Token`

You can use a [token](/docs/payments/token/) to prefill the Checkout Form with all required information about your customer on the payment initialization.

## Fill in the redirect URLs

`Dashboard`

Check your redirect URLs for a successful or failed payment are added in the Project Setting for the Payment Form.

{{< figure src="/images/redirect-urls.png">}}

## Customize the Checkout Form

`Unlimint Game Services JS SDK`

You can add your branding colors to the Checkout Form [view scheme](https://github.com/paysuper/paysuper-js-sdk/blob/master/docs/CUSTOMIZATION.md#available-parameters-of-viewschemeconfig).

## Fulfill the purchases

`Webhooks`

You can manually fulfil a purchase. Instead, create a handler for the [webhook](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks) events and execute your server-side code to fulfil the payment.

***

## Next steps

{{< hint info >}}
[**After the payment**](/docs/payments/fulfillment/)

After a successful payment, you have to fulfil the customer’s purchase. You can use [webhooks](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks) or the [Transactions](/docs/payments/fulfillment/#fulfilling-purchases-with-the-dashboard) to accomplish the purchase.
{{< /hint >}}

{{< hint info >}}
[**Testing the Checkout**](/docs/payments/testing/)

Verify that your integration with Unlimint Game Services Checkout works correctly. Our offered test cards can be used to create payments that produce defined responses for you to test your integration code.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}