---
title: Payment initialization with token
bookToc: true
---

# Payment initialization with token
***

A token is an encrypted string that represents certain details of your customer (such as the user ID, email and others), a game and purchase parameters.

You can create a token before your customer intents to pay and use it in the future payments. For instance, you can create the token after a user has signed up or has logged in to your website or a game client. When your customer wants to pay for something you redirect them to the PaySuper-hosted Checkout Form to instantly complete a purchase.

## Token-based features

* **Instantly redirect to a Checkout Form**: Once you have created a token that stores the necessary customer data, you don't need to request that data again from the customer. Instead you can display the PaySuper Checkout Form so the customer can conveniently confirm the purchase. This is useful when you can identify a customer in your system.

* **The pre-filled information in a Checkout Form**: The Checkout Form is pre-filled with the applicable information about your customer that it can get from the token.

***

You can follow these steps to create a Checkout Form:

## **Step 1.** Create a token on your server

Send the [POST /api/v1/tokens](/docs/api/#tag/Token) to receive an encrypted string. Learn more about the [full list of parameters](/docs/api/#tag/Token/paths/~1api~1v1~1tokens/post).

{{< hint warning >}}
Remember to add a Header `X-API-SIGNATURE` with the Project's Secret key found on the Project webhooks page.

Your Secret keys carry many privileges, so be sure to keep them secure! Do not share your Secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.
{{< /hint >}}

{{< tabs "token-simple-checkout" >}}

{{< tab "Runkit" >}}
Run the script and view the response data:

{{< runkit "simple-checkout-token">}}
Y29uc3QgYXhpb3MgPSByZXF1aXJlKCdheGlvcycpOwoKY29uc3QgcmVzcG9uc2UgPSBhd2FpdCBheGlvcy5wb3N0KAogICdodHRwczovL2FwaS5wYXkuc3VwZXIuY29tL2FwaS92MS90b2tlbnMnLAp7CiAgICJzZXR0aW5ncyI6IHsKICAgICAgInByb2plY3RfaWQiOiAiNWRjZDExYmMyMThkYzMwMDAxZDcwOThmIiwKICAgICAgImFtb3VudCI6IDEwLAogICAgICAiY3VycmVuY3kiOiAiVVNEIiwKICAgICAgInR5cGUiOiAic2ltcGxlIgogICB9LAogICAidXNlciI6IHsKICAgICAgImlkIjogIjU4Nzk5ZjJjMjU2NDI5NmJkMmNiIiwKICAgICAgImFkZHJlc3MiOiB7CiAgICAgICAgICJjaXR5IjogIkFsbWVyZSIsCiAgICAgICAgICJjb3VudHJ5IjogIk5MIiwKICAgICAgICAgInBvc3RhbF9jb2RlIjogIjEzMjYgUEEiLAogICAgICAgICAic3RhdGUiOiAiRmxldm9sYW5kIgogICAgICB9LAogICAgICAiZW1haWwiOiB7CiAgICAgICAgICJ2YWx1ZSI6ICJ1c2VyLmVtYWlsQGV4YW1wbGUuY29tIiwKICAgICAgICAgInZlcmlmaWVkIjogdHJ1ZQogICAgICB9CiAgIH0KfSwKICB7CiAgICBoZWFkZXJzOiB7CiAgICAgICAgJ0NvbnRlbnQtVHlwZSc6ICdhcHBsaWNhdGlvbi9qc29uJywKICAgICAgICAnWC1BUEktU0lHTkFUVVJFJzogJ0g4WWUmaChzcko8Sm5fWicKICAgIH0KICB9Cik=
{{< /runkit >}}
{{< /tab >}}

{{< tab "cURL" >}}
Or try it with cURL to interact with the API over HTTP from your console:

{{< highlight bash >}}
curl -X POST -H 'X-API-SIGNATURE: YOUR_SECRET_KEY' -d '{
 "settings": {
    "project_id": "YOUR_PROJECT_ID",
    "amount": 10,
    "currency": "USD",
    "type": "simple"
 },
 "user": {
   "id": "58799f2c2564296bd2cb",
   "address": {
      "city": "Almere",
      "country": "NL",
      "postal_code": "1326 PA",
      "state": "Flevoland"
   },
   "email": {
      "value": "user.email@example.com",
      "verified": true
   }
 }
}' 'https://p1payapi.tst.protocol.one/api/v1/tokens'
{{< /highlight >}}
{{< /tab >}}

{{< /tabs >}}

## **Step 2.** Create a Checkout Form with a token

### **Open a Checkout Form by URL**

{{< tabs "token_form" >}}

{{< tab "New browser window" >}}

Retrieve the response parameter `payment_form_url` from the previous step. It is the URL of PaySuper-hosted payment form.

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

{{< hint info >}}
Note that the parameters used in the `POST /api/v1/tokens` request override the corresponding parameters in an order object.
{{< /hint >}}

### **Client-side payment initialization**

To integrate a Checkout Form you can follow the [client-side payment initialization](/docs/payments/sdk-integration/) but instead pass a token parameter when creating a PaySuper object.

If your token contains [user and order parameters](/docs/api/#tag/Token) then you can create a Checkout Form instance with just a single parameter:

{{< highlight javascript >}}
const paySuper = new PaySuper({
   token: '5cd5620f06ae110001509185'
});
{{< /highlight >}}

### **Server-side payment initialization**

To integrate a Checkout Form you can follow the [server-side payment initialization](/docs/payments/integration/) with the `token` parameter.

If your token contains the [user and order parameters](/docs/api/#tag/Token) then you can request a Checkout Form URL with just a single parameter:

{{< tabs "token-product-checkout" >}}

{{< tab "Runkit" >}}
Run the script and view the response data:

{{< runkit "token-products-checkout-order">}}
Y29uc3QgYXhpb3MgPSByZXF1aXJlKCdheGlvcycpOwoKY29uc3QgcmVzcG9uc2UgPSBhd2FpdCBheGlvcy5wb3N0KAogICdodHRwczovL2FwaS5wYXkuc3VwZXIuY29tL2FwaS92MS9vcmRlcicsCnsKICAgInRva2VuIjogIll0WmNVdWpMdmlNS3kxektNUkNMdGdydFdJQkplWFU1Igp9LAogIHsKICAgIGhlYWRlcnM6IHsKICAgICAgICAnQ29udGVudC1UeXBlJzogJ2FwcGxpY2F0aW9uL2pzb24nCiAgICB9CiAgfQop
{{< /runkit >}}
{{< /tab >}}

{{< tab "cURL" >}}
Or try it with cURL to interact with the API over HTTP from your console:

{{< highlight bash >}}
curl -X POST -H 'Content-Type: application/json' -d '{
    "token": "YOUR_TOKEN"
}' 'https://p1payapi.tst.protocol.one/api/v1/order'
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