---
title: Client-side payment initialization
bookToc: true
---

# Payment initialization on the client-side
***

{{< columns >}}

The client-side payment initialization makes it possible to integrate a Checkout Form into your website using only frontend code.

It’s easy to embed [PaySuper JS SDK](https://github.com/paysuper/paysuper-js-sdk) with just a few lines of Javascript code to start a payment process and display a purchase status finally without any server-side code.

<--->

**HOW IT WORKS**

Try out [the payment sample](https://checkout.pay.super.com/demo/shop) or see [the code on GitHub](https://github.com/paysuper/paysuper-examples).
{{< /columns >}}

{{< hint warning >}}
Notice that a pure client-side payment initialization is possible yet a special care must be taken. Your project identity could be used from any web-site to initiate payments without any additional checks or verifications from the PaySuper side. At the moment we're working on an option to disable that kind of payment orders in the Project settings.
{{< /hint >}}

If your sales use cases are not filled, use the [server-side payment initialization](/docs/payments/integration/) with PaySuper API instead.

***

## **Step 1.** Embed the Checkout Form

To get started, include the following script tag on your website - always load it directly from `https://cdn.pay.super.com`:

{{< highlight html >}}
<script src="https://cdn.pay.super.com/paysdk/latest/paysuper.js"></script>
{{< /highlight >}}

## **Step 2.** Provide parameters

### **Simple Checkout**

To create a Checkout Form for one-time payments it's enough to have a [Project ID](/docs/payments/quick-start/#step-2-set-up-a-project) and an acceptable price and currency.

Use this sample code to create a PaySuper object with the required parameters for a simple checkout:

{{< highlight javascript >}}
const paySuper = new PaySuper({
    project: '5cd5624a06ae110001509186',
    amount: 10,
    currency: 'USD'
});
{{< /highlight >}}

### **Products Checkout**

If you're selling such products such as [key-activated products, virtual items or in-game currency](/docs/payments/quick-start/#step-3-additional-sales-options), you can use this sample code with a defined product parameter:

{{< tabs "client-products-checkout" >}}
{{< tab "Game Key" >}}

{{< highlight javascript >}}
const paySuper = new PaySuper({
    project: '5dcd11bc218dc30001d7098f',
    products: ['5dcdb885218dc30001d73c27'],
    type: 'key'
});
{{< /highlight >}}

{{< /tab >}}

{{< tab "Virtual Item" >}}

{{< highlight javascript >}}
const paySuper = new PaySuper({
    project: '5dcd11bc218dc30001d7098f',
    products: ['5dcdb73d218dc30001d73c25', '5dcdb841218dc30001d73c26'],
    type: 'product'
});
{{< /highlight >}}

{{< /tab >}}

{{< tab "Virtual Currency" >}}

{{< highlight javascript >}}
const paySuper = new PaySuper({
    project: '5dcd11bc218dc30001d7098f',
    products: ['5e292ba2769774c7377b739e'],
    type: 'product'
});
{{< /highlight >}}

{{< /tab >}}

{{< /tabs >}}

[Full list of PaySuper parameters](https://github.com/paysuper/paysuper-js-sdk/tree/master#parameters)

{{< hint warning >}}
Remember to use your IDs for the project and products. You can find your IDs in your merchant account on [the PaySuper Projects](https://dashboard.pay.super.com/projects). Open your Project settings page, select the Product tab and click on the Product name. Copy the Project and Product IDs from the page URL.
{{< /hint >}}

## **Step 3.** Display the Checkout Form

This example offers a sample code that displays a PaySuper Checkout Form with a `BUY` button.

{{< tabs "client_form" >}}

{{< tab "Embed as a modal window" >}}

{{< highlight html >}}
<script>
function buyItems() {
    const paySuper = new PaySuper({
        project: '5cd5624a06ae110001509186',
        amount: 10,
        currency: 'USD'
    });

    paySuper.renderModal();
}
</script>

<button onclick="buyItems()">BUY</button>
{{< /highlight >}}

{{< /tab >}}

{{< tab "Embed as an iframe" >}}

{{< highlight html >}}
<script>
function buyItems() {
    const paySuper = new PaySuper({
        project: '5cd5624a06ae110001509186',
        amount: 10,
        currency: 'USD'
    });

    paySuper.renderPage();
}
</script>

<button onclick="buyItems()">BUY</button>
{{< /highlight >}}

{{< /tab >}}

{{< /tabs >}}

## **Step 4.** Handle the purchase events

{{< highlight javascript >}}
paySuper.on('paymentCompleted', function() {
      // You can show a message that the payment is completed
})
{{< /highlight >}}

[Full events list in the expected order of execution](https://github.com/paysuper/paysuper-js-sdk/tree/master#events)

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
[**Customizing the Checkout**](/docs/payments/customization/)

Learn about the different ways you can customize your Checkout.
{{< /hint >}}

***

{{< questions >}}{{< questions-text >}}{{< /questions-text >}}{{< /questions >}}