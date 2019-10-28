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
4. You are required to fill in the Banking info in [Company Onboarding](https://paysupermgmt.tst.protocol.one/company) to be able create a Project.

{{< hint info >}}
When you are ready to start selling you will need to fill in all your company details in [Company Onboarding](https://paysupermgmt.tst.protocol.one/company) and sign the documents in the License Agreement.

Before confirming your application we manually check each new account to ensure that our platform is attended only by companies who are related to the gaming industry. This allows us to focus on the relevant features and quality for our users.
{{< /hint >}}

{{< /expand >}}

## **Step 2.** Set up a Project

A single Project is enough to start selling. 

{{< expand "Create a project" " " >}}

**To create a Project:**

1. Open [**the Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Click the **Create Project** button.
3. Enter a **Project Name**. 
4. Click **Create** to redirect to the Project Settings page.
5. Fill the required information in an appropriate localization:

    * **Full description**
    * **Short description**
    * **Secret key**: Generate a secret key to set up a correct integration with PaySuper platform.
    * **Currency**: by default is equal to **USD**.
6. Optional information:

    * **Localization**: you can choose the complete set of supported languages for the Project and Product descriptions
    * **Logotype**

7. Click **Save**.

{{< /expand >}}

You can provide all the necessary sales information about your Products in the Project settings in the dashboard to be able to sell Game keys, Virtual items or Virtual currency.

{{< expand "Add a Game key to a Project" " " >}}

**To add a Game key:**

1. Open [**the Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Open the Project settings page.
3. 

{{< /expand >}}

{{< expand "Add a Virtual item to a Project" " " >}}

**To add a Virtual item:**

1. Open [**the Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Open the Project settings page.
3. 

{{< /expand >}}

{{< expand "Add a Virtual currency to the project" " " >}}

**To add a Virtual currency:**

1. Open [**the Projects list page**](https://paysupermgmt.tst.protocol.one/projects/)
2. Open the Project settings page.
3. 

{{< /expand >}}

## **Step 3.** Set up a PaySuper Checkout Form

Use Checkout to collect [one-time payments](/docs/payments/#simple-checkout) or to sell [products defined in the Project](/docs/payments/#typed-checkout).

### [Integration on client-side](/docs/payments/sdk-integration/)

The client-only integration lets you accept online payments using only frontend code PaySuper JS SDK. The Checkout Form can be embedded as an [iframe](ССЫЛКА на метод renderPage) or [modal window](ССЫЛКА на метод renderModal).

### [Integration on client and server-side](/docs/payments/integration/)

You can also integrate on a server-side without PaySuper SJ SDK for other reasons. Checkout Form can be embedded as an [iframe](ССЫЛКА) or [new window](ССЫЛКА).

## **Step 4.** After the payment

You can use [webhooks](ССЫЛКА) or the [Transaction log](ССЫЛКА) to accomplish the purchase. More details about handling the purchase fulfilment with PaySuper Checkout are available at [After the payment](/docs/payments/fulfillment/).

***

## Next steps

{{< hint info >}}
[**Testing the Checkout**](/docs/payments/testing/)

Verify that your integration with PaySuper Checkout works correctly. Our offered test cards can be used to create payments that produce defined responses for you to test your integration code.
{{< /hint >}}

{{< hint info >}}
[**Customizing Checkout**](/docs/payments/customization/)

Learn about the different ways you can customize your PaySuper Checkout.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}
