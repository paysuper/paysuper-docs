---
title: Testing Checkout
bookToc: true
---

# Testing the Payment Process
***

The Payment Form integration should be tested in the Sandbox before [going live](/docs/payments/live/).

The Sandbox provides full functionality but it only emulates processing, no actual bank transactions are made.

When using PaySuper JS SDK ensure that:

* [Handlers for the events](/docs/payments/sdk-integration/#step-4-handle-the-purchase-events) are displayed properly.
* The PaySuper object is created with all [required parameters](/docs/payments/sdk-integration/#step-2-provide-parameters) or a [token](/docs/payments/token/).

If you're using the PaySuper API in your server-side code then ensure that:

* All [API errors](/api/#errors) are handled accurately.
* [Webhooks](/api/#webhooks) contains properly URL configured in the Functional URL section on the Project webhooks page.

## Test card numbers 

To test a bank card payment in the Sandbox enter arbitrary expiry date (the format is MM/YY), a Secure code (CVC/CVV, the format is 3 digits) and a cardholder name (the format is first name last name).

{{< hint warning >}}
You can also specify incorrect details (card number, expiration date, or CVV) to generate an error.
{{< /hint >}}

You will be redirected to the Sandbox page to select the desired results for success or failure. After you click the result button the current page will be closed and you will be redirected to the Checkout Form to view the purchase status.

> Note, that when Merchant chooses to fail the authentication, then the payment is always declined, no matter what PAN has been used.

Use any of the following test card numbers:

> Note that the `Authorized` cards must only be used to test the antifraud system reaction with a compulsory transfer payment to preauthorization.

### 3-D Secure test cards

3-D Secure is emulated with a page that doesn’t require any passwords and shows two buttons instead. One button is for a successful authentication, another is for a failed authentication.

{{< columns >}}
{{< card "Confirmed" "green" "mastercard" >}}4000 0000 0000 0002{{< /card >}}
<--->
{{< card "Declined" "red" "visa" >}}5555 5555 5555 4444{{< /card >}}
<--->
{{< card "Authorized" "grey" "visa" >}}4000 0000 0000 0044{{< /card >}}
{{< /columns >}}

### Non 3-D Secure test cards

{{< columns >}}
{{< card "Confirmed" "green" "visa" >}}4000 0000 0000 0077{{< /card >}}
<--->
{{< card "Declined" "red" "mastercard" >}}5555 5555 5555 4477{{< /card >}}
<--->
{{< card "Authorized" "grey" "visa" >}}4000 0000 0000 0051{{< /card >}}
{{< /columns >}}

## Currencies

You can choose a fixed set of currencies which will be actual for all products in your project on the Project settings page.

The full list of currencies that are supported for testing:

{{< columns >}}
Code|Country and Currency
---|---
USD|United States Dollar
EUR|Euro Member Countries
GBP|United Kingdom Pound
RUB|Russia Ruble
BRL|Brazil Real
JPY|Japan Yen
IDR|Indonesia Rupiah
MYR|Malaysia Ringgit
PHP|Philippines Peso
SGD|Singapore Dollar
THB|Thailand Baht
VND|Viet Nam Dong
KRW|Korea (South) Won
TRY|Turkey Lira
MXN|Mexico Peso
CAD|Canada Dollar
AUD|Australia Dollar	
NZD|New Zealand Dollar
NOK|Norway Krone
PLN|Poland Zloty
CHF|Switzerland Franc
CNY|China Yuan Renminbi
INR|India Rupee

<--->

Code|Country and Currency
---|---
CLP|Chile Peso
PEN|Peru Sol
COP|Colombia Peso
ZAR|South Africa Rand
HKD|Hong Kong Dollar
TWD|Taiwan New Dollar
SAR|Saudi Arabia Riyal
AED|UAE Dirham
ARS|Argentine Peso
ILS|New Israeli Sheqel
KZT|Kazakhstan Tenge
QAR|Qatar Riyal
CRC|Costa Rica Colon
HRK|Croatia Kuna
CZK|Czech Republic Koruna
RSD|Serbia Dinar
RON|Romania Leu
EGP|Egypt Pound
DKK|Denmark Krone
HUF|Hungary Forint
BHD|Bahraini Dinar
SEK|Sweden Krona

{{< /columns >}}

## Webhooks

{{< columns >}}
PaySuper can send you webhook events to your server to notify on the payment status. You can make a successful payment with a test card number and verify the resulting event data and to ensure that your webhook's endpoint is working and is configured properly.

<--->
**GETTING STARTED**

[Configure Webhooks](/api/#webhooks) for your Project in PaySuper Dashboard and handle them on your server.

{{< /columns >}}

**Testing the webhook notifications:**

Before going live, check that your server responds with status code 200 and empty body to webhook notifications to acknowledge about success (or any status code from 400 for failure) for all types of the order:

1. Go to Project Webhooks page.
2. Under Webhook Settings section choose the tab with the order's type: Simple checkout, Virtual currency, Virtual items, Game keys.
3. Enter the payment order data from your project: customer ID, transaction ID, virtual item ID (if any). You can test success and failure responses using a valid data or non-existing values.
4. Click Test and view the temporary logs below with the PaySuper notification and your server response.

***

## Next steps

{{< hint info >}}
[**After the payment**](/docs/payments/fulfillment/)

After a successful payment, you have to fulfil the customer’s purchase. You can use [webhooks](/docs/payments/fulfillment/#fulfilling-purchases-with-webhooks) or the [Transactions](/docs/payments/fulfillment/#fulfilling-purchases-with-the-dashboard) to accomplish the purchase.
{{< /hint >}}

{{< hint info >}}
[**Customizing the Checkout**](/docs/payments/customization/)

Learn about the different ways you can customize your Checkout.
{{< /hint >}}

{{< hint info >}}
[**Going live checklist**](/docs/payments/live/)

You can inspect this checklist before going live to ensure you've implemented all the significant setup steps.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}