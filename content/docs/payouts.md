---
title: Receiving Payouts
bookToc: true
---

# Receiving Payouts
***

Your customers' successful payments are stored on your PaySuper account balance and can be received to your bank account using [Payouts](https://dashboard.pay.super.com/payouts).

{{< figure src="/images/payouts-table.png">}}

- **Amount available for withdraw** - the amount of the merchant balance as the difference between the total amount of all received royalty reports and all paid or pending payouts.
- **Period** - the payout period. By default, the Royalty report automatically generates based on the successfully received payments during the last 7 days. [Learn more](/docs/payouts/#confirming-a-royalty-report) 
- **Report date** - the date of the Royalty report confirmation. By default, your Royalty report will be automatically confirmed.
- **Payout ID** - the unique identifier for the payout.
- **Payment date** - the date when the payout amount transferred to the merchant bank account.
- **Amount** - the payout amount.
- **Status** - the current status of the payout. [Learn more](/docs/payouts/#payout-statuses)

## Setting up your bank account to receive payouts

When you are ready to start selling you will need to fill in all your company details in [Company Onboarding](https://dashboard.pay.super.com/company).

Bank account details for payouts are required when filling in Company Onboarding.

{{< hint warning >}}
Note that the currency of the bank account must be the same as the Account Currency for payouts filled in the Banking info.
{{< /hint >}}

{{< figure src="/images/banking-info.png">}}

{{< hint info >}}
Accounts can receive payouts in the following settlement currencies: **USD**, **EUR**, **RUB**, **GBP**.
{{< /hint >}}

## Confirming a Royalty report

PaySuper automatically generates a [Royalty report](https://dashboard.pay.super.com/reports) based on the successfully received payments during the last 7 days. This report contains detailed information like fees, VAT, license share and so on. The PaySuper Royalty reports have a credible legal basis for receiving an invoice for a payout and making a payment to your bank account.

{{< figure src="/images/royalty-report.png">}}

Once in 7 days, you will be notified in the Dashboard and by email about a new Royalty report. 

If you confirm this report for 5 days you can proceed with the payout process on the [Payouts](https://dashboard.pay.super.com/payouts) page. In another case, in 5 days your Royalty report will be automatically confirmed.

If you reject the Royalty report then PaySuper will process the disputed report within 5 days and resend for your confirmation.

## Minimum payout amount

To create a payout your PaySuper account balance must be more than a minimum payout amount.

Currency|Minimum payout
---|---
USD|100.00 USD
EUR|100.00 EUR
RUB|10000.00 RUB
GBP|100.00 GBP

## Payout costs

Please notice there is a fixed service price **$25.00** for every payout transaction for all payment methods.

## Payout statuses

Status|Description
:---|:---
PENDING|The payout has been sent to the merchant bank account.
PAID|The merchant received the payout amount in a bank account.
SKIP|The payout amount exceeded the minimum payout threshold limit. This amount will be included in the next payout.
CANCELED|The payout has been rejected by the bank.
FAILED|The payout has been rejected by the bank.

## Payout failures

There are some reasons when a payout is rejected by your bank. Thus your funds remain in the PaySuper account. PaySuper provides you an error message about the failure reason in the Dashboard and by email.

**Failure codes with a description:**

---

**Account Closed** — The merchant bank account is closed.

---

**Account Frozen** — The merchant bank account is frozen.

---

**Account Restricted** — The merchant account has restrictions receiving payments. For instance, account has the limit of payments per time unit or has another type.

---

**Destination bank invalid** — The destination bank has incorrect info.

---

**Could not process** — The bank couldn't make the transfer, but no further information is available.

---

**Declined** — The bank has refused to carry out the transfer. In that case, the merchant needs to contact the bank for details.

---

**Insufficient funds** — Not enough funds on the merchant account to transfer.

---

**Invalid account number** — The recipient's account number or transit number is incorrect. This error is the same if the account number is absent from the bank.

---

**Incorrect account holder name** — The recipient's name is incorrect.

---

**Invalid currency** — The destination bank cannot process an incoming payment in the specified currency or the currency of the account differs from the currency of payment.

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