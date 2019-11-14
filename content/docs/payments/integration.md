---
title: Server-side payment initialization
bookToc: true
---

# Payment initialization on the server-side
***

The server-side payment initialization makes it possible to integrate a Checkout Form into your website or game client using PaySuper API. It’s easy to get a Checkout Form URL using an Order API request and render a payment form in a browser.

You can use PaySuper JS SDK for the [client-side payment initialization](/docs/payments/sdk-integration/) to integrate a Checkout Form into your website only on the client-side.

***

## **Step 1.** Create a Checkout order on your server

Send the [POST /api/v1/order](/docs/api/#tag/Payment-Order) to receive an Order ID. Learn more about the [full list of parameters](/docs/api/#tag/Payment-Order/paths/~1api~1v1~1order/post) that can be used for instance the redirect URLs for successful and failed payments.

### **Simple Checkout**

To initiate simple checkout payments it's enough to create a payment order with your [Project ID](/docs/payments/quick-start/#step-2-set-up-a-project) and an acceptable amount and currency.

Use this sample code to create an Order ID with the required parameters for a simple checkout:

{{< tabs "order-simple-checkout" >}}

{{< tab "Runkit" >}}
Run the script and view the response data:

{{< runkit "simple-checkout-order" >}}
Y29uc3QgYXhpb3MgPSByZXF1aXJlKCdheGlvcycpOwoKY29uc3QgcmVzcG9uc2UgPSBhd2FpdCBheGlvcy5wb3N0KAogJ2h0dHBzOi8vcDFwYXlhcGkudHN0LnByb3RvY29sLm9uZS9hcGkvdjEvb3JkZXInLAogewogICAicHJvamVjdCI6ICI1ZGIxNmFlODExYmYwZDAwMDFmZGZiZDEiLAogICAiYW1vdW50IjogMTAsCiAgICAiY3VycmVuY3kiOiAiVVNEIiwKICAgICJ0eXBlIjogInNpbXBsZSIKIH0sCiAgewogICAgaGVhZGVyczogewogICAgICAgICdDb250ZW50LVR5cGUnOiAnYXBwbGljYXRpb24vanNvbicKICAgIH0KICB9Cik=
{{< /runkit >}}
{{< /tab >}}

{{< tab "cURL" >}}
Or try it with cURL to interact with the API over HTTP from your console:

{{< highlight bash >}}
curl -X POST -H 'Content-Type: application/json' -d '{
    "project": "YOUR_PROJECT_ID",
    "amount": 10,
    "currency": "USD",
    "type": "simple"
}' 'https://p1payapi.tst.protocol.one/api/v1/order'
{{< /highlight >}}
{{< /tab >}}

{{< /tabs >}}

{{< hint warning >}}
Remember to use your IDs for the project and products. You can find your IDs in your merchant account on [the PaySuper Projects](https://paysupermgmt.tst.protocol.one/projects/). Open your Project settings page, select the Product tab and click on the Product name. Copy the Project and Product IDs from the page URL.
{{< /hint >}}

### **Products Checkout**

If you're selling products such as [key-activated products, virtual items or in-game currency](/docs/payments/quick-start/#step-3-additional-sales-options), you can use this sample code with a defined product parameter:

{{< tabs "order-products-checkout" >}}

{{< tab "Game Key" >}}

Run the script and view the response data:

{{< runkit "key-checkout-order" >}}
Y29uc3QgYXhpb3MgPSByZXF1aXJlKCdheGlvcycpOwoKY29uc3QgcmVzcG9uc2UgPSBhd2FpdCBheGlvcy5wb3N0KAogJ2h0dHBzOi8vcDFwYXlhcGkudHN0LnByb3RvY29sLm9uZS9hcGkvdjEvb3JkZXInLAogewogICAicHJvamVjdCI6ICI1ZGIxNmFlODExYmYwZDAwMDFmZGZiZDEiLAogICAicHJvZHVjdHMiOiBbIjVkYjE2ZDUzMTFiZjBkMDAwMWZkZmJkMiJdLAogICAidHlwZSI6ICJrZXkiCiB9LAogIHsKICAgIGhlYWRlcnM6IHsKICAgICAgICAnQ29udGVudC1UeXBlJzogJ2FwcGxpY2F0aW9uL2pzb24nCiAgICB9CiAgfQop
{{< /runkit >}}

Or try it with cURL to interact with the API over HTTP from your console:

{{< highlight bash >}}
curl -X POST -H 'Content-Type: application/json' -d '{
    "project": "YOUR_PROJECT_ID",
    "products": ["YOUR_GAME_KEY_ID"],
    "type": "key"
}' 'https://p1payapi.tst.protocol.one/api/v1/order'
{{< /highlight >}}

{{< /tab >}}

{{< tab "Virtual Item" >}}

Run the script and view the response data:

{{< runkit "products-checkout-order" >}}
Y29uc3QgYXhpb3MgPSByZXF1aXJlKCdheGlvcycpOwoKY29uc3QgcmVzcG9uc2UgPSBhd2FpdCBheGlvcy5wb3N0KAogICdodHRwczovL3AxcGF5YXBpLnRzdC5wcm90b2NvbC5vbmUvYXBpL3YxL29yZGVyJywKewogICAgInByb2plY3QiOiAiNWRiMTZhZTgxMWJmMGQwMDAxZmRmYmQxIiwKICAgICJwcm9kdWN0cyI6IFsiNWRiOTVhYzA5NDcyNjMwMDAxZDM5YzBkIiwgIjVkYjk1YWRmOTQ3MjYzMDAwMWQzOWMwZSJdLAogICAgInR5cGUiOiAicHJvZHVjdCIKfSwKICB7CiAgICBoZWFkZXJzOiB7CiAgICAgICAgJ0NvbnRlbnQtVHlwZSc6ICdhcHBsaWNhdGlvbi9qc29uJwogICAgfQogIH0KKQ==
{{< /runkit >}}

Or try it with cURL to interact with the API over HTTP from your console:

{{< highlight bash >}}
curl -X POST -H 'Content-Type: application/json' -d '{
    "project": "YOUR_PROJECT_ID",
    "products": ["YOUR_VIRTUAL_ITEM_ID_1", "YOUR_VIRTUAL_ITEM_ID_2"],
    "type": "product"
}' 'https://p1payapi.tst.protocol.one/api/v1/order'
{{< /highlight >}}

{{< /tab >}}

{{< tab "Virtual Currency" >}}


{{< /tab >}}

{{< /tabs >}}

## **Step 2.** Display a Checkout Form

{{< tabs "server_form" >}}

{{< tab "New browser window" >}}

Retrieve the response parameter `payment_form_url` from the previous step. It is the URL of a PaySuper-hosted payment form.

When your customer is ready to start a payment you can redirect the user to the URL in a new browser window.

{{< /tab >}}

{{< tab "Iframe" >}}

Retrieve the response parameter `payment_form_url` from the previous step. It is the URL of a PaySuper-hosted payment form.

Embed the Checkout Form as an inline iframe by URL:

{{< highlight html >}}
<iframe src="{payment_form_url}"></iframe>
{{< /highlight >}}

{{< /tab >}}

{{< tab "Standalone web-page" >}}

Retrieve the response parameter with `id` from the previous step. It is the ID of the created order.

Use this code sample to open the Checkout Form as a standalone web-page with [PaySuper JS SDK](/docs/payments/sdk-integration/#step-1-embed-the-checkout-form) and replace `YOUR_ORDER_ID` in the `formUrl` with `id` value:

{{< highlight html >}}
<script>
function buyItems() {
    const paySuper = new PaySuper({
        formUrl: 'https://order.pay.super.com/?order_id=YOUR_ORDER_ID'
    });

    paySuper.renderPage();
}
</script>

<button onclick="buyItems()">BUY</button>
{{< /highlight >}}

{{< /tab >}}

{{< /tabs >}}

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