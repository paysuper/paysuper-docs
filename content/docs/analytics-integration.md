---
title: Analytics Integration
bookToc: true
---

# Analytics Integration
***

It's assumed that you have already integrated [PaySuper Checkout via SDK](/docs/payments/sdk-integration) and have set up your Google Analytics account.

## Integrate

{{< hint warning >}}
We've set up a Google Analytics data collection in a test mode inside PaySuper. After the Beta testing, we'll release the analytics integration to use with a customer's tracking ID.
{{< /hint >}}

## Google Analytics

You can track the following events:

Category|Action|Description
---|---|---
userAction|clickCloseCross|Close the form by clicking on the cross (for the modal window mode).
general|formClosed|The Checkout Form is closed (for the modal window mode).
general|hasSavedBankCards|The Checkout Form contains user's saved cards on start.
general|noSavedBankCards|The Checkout Form does not contain user's saved cards on start.
userAction|clickSaveUserCountry|Clicking the **Save** button after selecting a country on the country selection screen for a payment.
userAction|clickCloseButton|Clicking the **Close** button at the bottom of the Checkout Form.
userAction|clickOkButton|Clicking the **OK** button at the bottom of the Checkout Form.
userAction|clickPayButton|Clicking the **Pay** button at the bottom of the Checkout Form.
general|submitPaymentForm|Starting the payment proccess after a successful card validation.
userAction|setUserCountry|The selected country has been changed (in any way).
userAction|clickRememberCard|Clicking the checkbox **Remember**.
userAction|selectSavedCard|A user has selected a saved card.
userAction|removeSavedCard|A user has started deleting a saved card.
userAction|cancelRemovingSavedCard|A user has cancelled deleting a saved card.
general|submitSavedCardRemove|A request to delete a saved card has been submitted (after the 5 second timeout).
userAction|clickSupportLink|Clicking the **Support** link.
userAction|clickUserAgreementLink|Clicking the **User Agreement** link.
userAction|clickToggleCart|Clicking the **Collapse/Expand a cart** toggle (for the mobile view mode).
userAction|clickProjectLink|Clicking the **Project** link.
userAction|clickTermsOfUseLink|Clicking the **Terms of use** link.
userAction|clickPaySuperLink|Clicking the **PasySuper** link.
userAction|clickIconSupportLink|Clicking the **Support** icon on the top of the Checkout Form next to the Languages selector.
userAction|clickOpenReceiptButton|Clicking the **Open the receipt page** button.
userAction|selectPlatform|A user has selected the game platform.
userAction|useSavedBankCards|A user has switched to the saved cards.
userAction|useManualBankCardsInput|A user has switched to the manual input of a bank card data.
general|showActionProcessing|The loading screen is being shown.
general|showActionResult|A screen with a successful or failed result is being shown.
general|orderPrimaryInitError|An error on the Checkout Form initialisation (i.e. a failure to create the order).
general|orderAlreadyProcessed|The Checkout Form has failed to load because the order had already been processed.
userAction|setPaymentMethod|A payment method has been selected (a bank card, QIWI etc.).
general|purchaseFailed|The payment process has failed.
general|checkPaymentAccount|Started verifying the bank card number.
general|customLocale|The Checkout Form has started with a defined locale (set via a token).
userAction|setLocale|A user has changed a locale.
ecommerce|begin_checkout|Submitting [e-commerce data](https://developers.google.com/analytics/devguides/collection/gtagjs/enhanced-ecommerce) after the Checkout Form start.
ecommerce|purchase|Submitting [e-commerce data](https://developers.google.com/analytics/devguides/collection/gtagjs/enhanced-ecommerce) after a successul purchase.

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
