---
title: Quick start
bookToc: true
---

# Payments Flow
***

## User Flow

{{< figure src="/images/user-flow.png">}}

## Integration Flow

{{< figure src="/images/integration-flow.png">}}

# Quick start
***

## **Step 1.** Register a PaySuper Company account

{{< expand "Registration and onboarding" " " >}}

1. [Sign up](https://paysupermgmt.tst.protocol.one).
2. Verify your email address with the delivered confirmation email.
3. Follow the steps of a brief [Welcome Onboarding](https://paysupermgmt.tst.protocol.one/profile).
4. You are required to fill in the Banking info in the [Company Onboarding](https://paysupermgmt.tst.protocol.one/company) to be able create a project.

{{< hint info >}}
When you are ready to start selling you will need to fill in all your company details in [Company Onboarding](https://paysupermgmt.tst.protocol.one/company) and sign the documents in the License Agreement.

Before confirming your application we manually check each new account to ensure that our platform is attended only by companies who are related to the gaming industry. This allows us to focus on the relevant features and quality for our users.
{{< /hint >}}

{{< /expand >}}

## **Step 2.** Set up a Project

A single project is enough to start selling. 

{{< expand "Create a project" " " >}}

**To create a Project:**

1. Open the [**Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Click the **Create Project** button.
3. Enter a **Project Name**.
4. Click **Create** to redirect to the Project Settings page.
5. Fill in the unique name and localised project descriptions. It will be mentioned in a payment form and different customer correspondence.
7. Click **Save**.

{{< /expand >}}

Now you can initiate a simple checkout payment. It's enough to create a payment order with your Project ID and an acceptable amount and currency.

## **Step 3.** Additional sales options

If you want to sell products (as Game keys, Virtual items, Virtual currency) then easily add the necessary sales information about your products to the project.

{{< expand "Add a Game key to the project" " " >}}

**To add a Game key:**

1. Open your Project from the [**Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Select the Sales options in the left sidebar and open the Game keys tab.
3. Create a package to sell your game keys for associated DRM platforms. You can choose several platforms at once.
4. Upload a pack of game keys for each DRM platform you selected.
5. **Enable** the package and click **Save**.

{{< /expand >}}

{{< expand "Add a Virtual item to the project" " " >}}

**To add a Virtual item:**

1. Open your Project from the [**Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Select the Sales options in the left sidebar and open the Virtual items tab.
3. Add a new item with localised text descriptions, SKU, prices and currencies.
4. **Enable** and click **Save**.

{{< /expand >}}

{{< expand "Add a Virtual currency to the project" " " >}}

**To add a Virtual currency:**

1. Open your Project from the [**Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Select the Sales options in the left sidebar and open the Virtual currency tab.
3. Fill in the unique name and localised project descriptions.
4. **Enable** and click **Save**.

{{< /expand >}}

## **Step 4.** Set up a Checkout Form

Use Checkout to collect [one-time payments](/docs/payments/#simple-checkout) or to sell [products defined in the Project](/docs/payments/#products-checkout).

### [Payment initialization with token](/docs/payments/token/)

You can encrypt details of your customer (such as the user ID, email and others), a game and purchase parameters. When your customer wants to pay for something you redirect them to the PaySuper-hosted Checkout Form to instantly complete a purchase.

### [Server-side payment initialization](/docs/payments/integration/)

You can also integrate on a server-side without PaySuper SJ SDK for other reasons. Checkout Form can be embedded as an iframe or new window.

### [Client-side payment initialization](/docs/payments/sdk-integration/)

The client-side payment initialization lets you accept online payments using only frontend code PaySuper JS SDK. The Checkout Form can be embedded as an iframe or modal window.

## **Step 4.** After the payment

You can use webhooks or the Transaction log to accomplish the purchase. More details about handling the purchase fulfilment with PaySuper Checkout are available at [After the payment](/docs/payments/fulfillment/).

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
[**Customizing the Checkout**](/docs/payments/customization/)

Learn about the different ways you can customize your Checkout.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}