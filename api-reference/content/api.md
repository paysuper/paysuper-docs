---
title: Unlimint Game Services API Reference
language_tabs:
  - shell: cURL
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

# CORE RESOURCES

# Token

A token is an encrypted string that represents certain details of your customer (such as the customer ID, email and others), a game and purchase parameters.

## Create a payment token

> Code samples

```shell
curl -X POST \
  https://api.pay.super.com/api/v1/tokens \
  -H 'Content-Type: application/json' \
  -H 'X-API-SIGNATURE: YOUR_SECRET_KEY \
  -d '{
      "settings": {
          "project_id": "5dcd11bc218dc30001d7098f",
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
}'

```

### POST /api/v1/tokens

Create a payment token that encrypts details about your customer, the game and purchase parameters.

> Body parameters

```json
{
  "user": {
    "id": "string",
    "email": {
      "value": "string",
      "verified": true
    },
    "phone": {
      "value": "string",
      "verified": true
    },
    "name": {
      "value": "string"
    },
    "ip": {
      "value": "string"
    },
    "locale": {
      "value": "string"
    },
    "address": {
      "country": "string",
      "city": "string",
      "postal_code": "string",
      "state": "string"
    }
  },
  "settings": {
    "project_id": "string",
    "return_url": {
      "success": "string",
      "fail": "string"
    },
    "currency": "string",
    "amount": 0,
    "description": "string",
    "products_ids": [
      "string"
    ],
    "platform_id": "string",
    "type": "string",
    "is_buy_for_virtual_currency": true,
    "button_caption": "string",
    "metadata": {
      "parameter1": "value1"
    }
  }
}
```

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`user`|object|The customer data.|
|&ensp; `id` <span style="color: red;">*</span> |string|The unique identifier for the customer in the merchant project.|
|&ensp; `email`|object|The customer's email data.|
|&ensp; &ensp; `value`|string|The customer’s email address.|
|&ensp; &ensp; `verified`|boolean|Whether the email has been verified on the merchant side.|
|&ensp; `phone`|object|The customer's phone data.|
|&ensp; &ensp; `value`|string|The customer’s phone.|
|&ensp; &ensp; `verified`|boolean|Whether the phone has been verified on the merchant side.|
|&ensp; `name`|object|The customer's name data.|
|&ensp; &ensp; `value`|string|The customer’s name.|
|&ensp; `ip`|object|The customer's IP address data.|
|&ensp; &ensp; `value`|string|The customer’s IP address.|
|&ensp; `locale`|object|The customer's locale data.|
|&ensp; &ensp; `value`|string|The customer’s locale name. The Accept-Language format by RFC 7231.|
|&ensp; `address`|object|The customer's address data.|
|&ensp; &ensp; `country`|string|The customer's country. Two-letter country code in ISO 3166-1, in uppercase (for instance US).|
|&ensp; &ensp; `city`|string|The customer’s city.|
|&ensp; &ensp; `postal_code`|string|The customer's postal code.|
|&ensp; &ensp; `state`|string|The customer's state code in ISO 3166-2.|
|&ensp; `settings`|object|The project data.|
|&ensp; &ensp; `project_id` <span style="color: red;">*</span> |string|The unique identifier for the Project found in the merchant account in the Unlimint Game Services Dashboard.|
|&ensp; &ensp; `return_url`|object|The redirect URLs after the successful or failed payment.|
|&ensp; &ensp; &ensp; `success`|string|The redirect URL for a successful payment.|
|&ensp; &ensp; &ensp; `fail`|string|The redirect URL for a failed payment.|
|&ensp; &ensp; `currency`|string|The order currency. Three-letter Currency Code ISO 4217, in uppercase. It's required for a simple checkout payment.|
|&ensp; &ensp; `amount`|number|The order amount. It's required for a simple checkout payment.|
|&ensp; &ensp; `description`|string|An arbitrary order description.|
|&ensp; &ensp; `products_ids`|[string]|A list of unique identifiers for Project's products. It's required if a payment type equals to ‘product’ or ‘key’.|
|&ensp; &ensp; `platform_id`|string|The default platform's name for which the customer buys a key. This field is used only for the key type. Available values: steam, gog, uplay, origin, psn, xbox, nintendo, itch, egs.|
|&ensp; &ensp; `type` <span style="color: red;">*</span> |string|The order type. It depends on your sales option: Game Keys, Virtual Items, Virtual Currency, Simple Checkout. Available values: key, product, virtual_currency, simple.|
|&ensp; &ensp; `is_buy_for_virtual_currency`|boolean|Has a true value if an order must be processed using a virtual currency.|
|&ensp; &ensp; `button_caption`|string|The redirect button messages after the successful or failed payment. If it has an empty value the redirect message will be set at OK.|
|&ensp; &ensp; `metadata`|object|A string-value description that you can attach to the token object. It can be useful for storing additional information about your customer's payment.|

### Responses

> Example responses

> 200 Response

```json
{
  "token": "string",
  "payment_form_url": "string"
}
```

### 200 Returns the payment token string and the Unlimint Game Services-hosted URL for a payment form

||||
|---|---|---|
|`token`|string|The secure string which contains encrypted information about your customer and sales option data.|
|`payment_form_url`|string|The Unlimint Game Services-hosted URL of a payment form.|

### 400 Invalid request data

||||
|---|---|---|
|`code`|string|The error code.|
|`message`|string|The error short description.|
|`details`|string|The error details.|

### 404 Not found

||||
|---|---|---|
|`code`|string|The error code.|
|`message`|string|The error short description.|
|`details`|string|The error details.|

### 500 Internal Server Error

||||
|---|---|---|
|`code`|string|The error code.|
|`message`|string|The error short description.|
|`details`|string|The error details.|

# Transactions

## Get the transactions list

### GET /merchant/s2s/api/v1/order

Get the transactions list using filter parameters.

Use the basic HTTP authentication with the Base64 encoding of login and password joined by a single colon : , where `login` - the unique identifier for your Unlimint Game Services project, `password` - the Secret Key of that project. 

> Request Header:

> Authorization: Basic NWU1OGVjMGZiZTUzZWE0Yzk5NmNhMDVkOlZOaGMuazw4KXpaQVB7YT==

Request parameters to filter transactions:

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`id`|string|The unique identifier in Unlimint Game Services.|
|`project`|string[]|The project list to get its transactions. If this parameter is not set, the search is performed for all projects.|
|`status`|string[]|The transactions' statuses list. Available values: created, processed, canceled, rejected, refunded, chargeback, pending.|
|`account`|string|The unique identifier in the merchant project.|
|`project_date_from`|string|The period start date. Format: YYYY-MM-DDThh:ii:ss|
|`project_date_from`|string|The period end date. Format: YYYY-MM-DDThh:ii:ss|
|`invoice_id`|string|The unique identifier in the merchant project.|
|`limit`|integer|The number of objects returned in one page. Default value is 100.|
|`offset`|integer|The ranking number of the first item on the page.|

### Responses

> Example responses

> 200 Response

```json
{
  "count": 1,
  "items": [
    {
      "id": "5b25b60e-2561-468c-a326-cbb9e21d0fc5",
      "transaction": "376271699",
      "object": "order",
      "status": "processed",
      "description": "Payment by order # ffffffffffffffffffffffff",
      "canceled": false,
      "cancellation": null,
      "refunded": false,
      "receipt_email": "tets@example.com",
      "receipt_phone": "",
      "receipt_number": "",
      "receipt_url": "https://checkout.pay.super.com/pay/receipt/purchase/6aa62191-2f44-4c1d-814c-d47fbcf56e3a/5b25b60e-2561-468c-a326-cbb9e21d0fc5",
      "agreement_version": "",
      "agreement_accepted": false,
      "notify_sale": false,
      "notify_sale_email": "",
      "issuer": {
        "url": "https://checkout.pay.super.com/pay/order/5b25b60e-2561-468c-a326-cbb9e21d0fc5",
        "embedded": false,
        "reference": "",
        "reference_type": "",
        "utm_source": "",
        "utm_medium": "",
        "utm_campaign": "",
        "referrer_host": "checkout.pay.super.com"
      },
      "amount": 100,
      "currency": "RUB",
      "user": {
        "external_id": "test@example.com",
        "name": "",
        "email": "test@example.com",
        "email_verified": true,
        "phone": "",
        "phone_verified": false,
        "ip": "127.0.0.1",
        "locale": "ru-RU",
        "address": {
          "country": "UA",
          "city": "Alexandrovsk",
          "postal_code": "71610",
          "state": "23"
        },
        "metadata": null
      },
      "billing_address": null,
      "tax": {
        "type": "vat",
        "rate": 0,
        "amount": 0,
        "currency": "RUB"
      },
      "method": {
        "title": "Bank card",
        "external_id": "BANKCARD",
        "payment_system_id": "5be2d0b4b0b30d0007383gg7",
        "type": "BANKCARD",
        "saved": false,
        "card": {
          "first6": "400000",
          "last4": "0001",
          "masked": "400000...0001",
          "expiry_month": "06",
          "expiry_year": "2024",
          "brand": "MASTERCARD",
          "fingerprint": "$2a$04$vdhmWzMxN0tR/21jaGtkaOCvYVnk88P6ZGWbKLL9K5TqgsVgv8HGT",
          "secure3d": true
        },
        "wallet": null,
        "crypto_currency": null,
        "handler": "cardpay",
        "refund_allowed": true
      },
      "items": null,
      "refund": null,
      "metadata": {
        "invoiceId": "2697661"
      },
      "original_amount": 100,
      "country": "UA",
      "type": "simple",
      "platform_id": "",
      "receipt_id": "6aa62191-2f44-4c1d-814c-d47fbcf56e3a",
      "virtual_currency_amount": 0,
      "is_buy_for_virtual_currency": false,
      "charge_currency": "RUB",
      "charge_amount": 100,
      "vat_payer": "buyer",
      "is_production": true,
      "testing_case": "",
      "form_mode": "embed",
      "merchant_info": {
        "company_name": "Some Company LLC",
        "agreement_number": "0102-1234567"
      },
      "created_at": "2020-08-06T10:51:33.157Z",
      "canceled_at": "0001-01-01T00:00:00Z",
      "refunded_at": "0001-01-01T00:00:00Z"
    }
  ]
}
```

### 200 Returns the transactions list of projects

||||
|---|---|---|
|`count`|integer|The total number of found items.|
|`items`|object[] or null|The transactions list.|

### 400 Invalid request data

||||
|---|---|---|
|`code`|string|The error code.|
|`message`|string|The error short description.|
|`details`|string|The error details.|

### 500 Internal Server Error

||||
|---|---|---|
|`code`|string|The error code.|
|`message`|string|The error short description.|
|`details`|string|The error details.|

# ORDERS

# Order

You can create a payment order with details about your customer and sales option data.

### Statuses

|Name|Description|
|---|---|
|`created`|It’s an initial state of the requested order but it is not processed in a payment system yet. The `created` order can become one of the statuses: `processed`, `canceled`, `rejected`.|
|`processed`|The order is successfully processed in the payment system. The `processed` order can become `refunded` or `chargeback`.|
|`rejected`|The order is rejected by the payment system with any reasons.|
|`canceled`|The order is canceled by the customer.|
|`refunded`|The processed order is refunded by the merchant request.|
|`chargeback`|The processed order is refunded by the payment system with any reasons.|

> The Order object example:

```json
{
  "id": "726d9e07-1dc8-4159-8d52-f95941066bc8",
  "transaction": "2978077",
  "object": "order",
  "status": "created",
  "description": "A summary for the purchase",
  "created_at": "2019-07-10T14:27:54.691Z",
  "canceled": false,
  "canceled_at": "",
  "cancellation": null,
  "refunded": false,
  "refunded_at": "",
  "receipt_email": "user.email@example.com",
  "receipt_phone": "",
  "receipt_number": "",
  "receipt_url": "https://dashboard.pay.super.com/receipt/purchase/efefc5d3-c2e2-415",
  "agreement_version": "",
  "agreement_accepted": false,
  "notify_sale": false,
  "notify_sale_email": "",
  "issuer": {
      "url": "https://domain.com",
      "embedded": false,
      "reference": "",
      "reference_type": "",
      "utm_source": "",
      "utm_medium": "",
      "utm_campaign": "",
      "referrer_host": "domain.com"
  },
  "amount": 595,
  "currency": "RUB",
  "user": {
      "id": "5dcf8b24b5a6990001bac2b6",
      "object": "user",
      "external_id": "0000000000001",
      "name": "User Name",
      "email": "user.email@example.com",
      "email_verified": true,
      "phone": "9112223344",
      "phone_verified": true,
      "ip": "79.137.163.2",
      "locale": "ru-RU",
      "address": {
        "country": "RU",
        "city": "Moscow",
        "postal_code": "127221",
        "state": "MOW"
      },
      "metadata": {
        "user.param1": "user.val1",
        "user.param2": "user.val2",
        "user.param3": "user.val3"
      },
      "notify_new_region": false,
      "notify_new_region_email": ""
  },
  "billing_address": {
      "country": "DE"
  },
  "tax": {
      "type": "vat",
      "rate": 0.19,
      "amount": 95,
      "currency": "RUB"
  },
  "method": {
      "title": "Bank card",
      "external_id": "BANKCARD",
      "payment_system_id": "5be2d0b4b0b30d0007383ce5",
      "saved": false,
      "card": {
        "first6": "400000",
        "last4": "0002",
        "masked": "400000...0002",
        "expiry_month": "11",
        "expiry_year": "2023",
        "brand": "VISA",
        "fingerprint": "$2a$04$9VRouYlBC.qMYQrLpmlXOeGbL2WFZDGGq/KdTeeHSfWkosgJgrWw2",
        "secure3d": true
      },
      "wallet": null,
      "crypto_currency": null,
      "refund_allowed": true
  },
  "items": null,
  "refund": null,
  "metadata": {
      "param1": "val1",
      "param2": "val2",
      "param3": "val3"
  },
  "original_amount": 500,
  "country": "DE",
  "type": "simple",
  "platform_id": "",
  "receipt_id": "efefc5d3-c2e2-4157-8789-4bfb7c1eec34",
  "virtual_currency_amount": 0,
  "is_buy_for_virtual_currency": false
}
```

### The Order object:

|Attribute|Type|Description|
|---|---|---|
|`id`|string|The unique identifier for the order in Unlimint Game Services.|
|`transaction`|string|The unique identifier for the transaction in the issuer system (the bank, QIWI, PayPal, etc.)|
|`object`|string|The string representing the object’s type. Value: `order`.|
|`status`|string|The current status of the order.|
|`description`|string|An arbitrary string attached to the object. If this field was not sent, the Unlimint Game Services generates it automatically.|
|`created_at`|string|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) at which the order was created.|
|`canceled_at`|string|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) at which the order was cancelled.|
|`canceled`|boolean|Has the value `true` if the current order was canceled.|
|`cancellation`|object|The cancellation reason. Has the value `null` if the order is not canceled.|
|&ensp;&ensp;`code`|string|The cancellation reason code.|
|&ensp;&ensp;`reason`|string|The cancellation description.|
|`refunded`|boolean|Has the value `true` if the current order was refunded.|
|`refunded_at`|string|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) at which the order was refunded.|
|`receipt_email`|string|The customer's email for receipt information.|
|`receipt_phone`|string|The customer's phone for receipt information.|
|`receipt_number`|string|The unique identifier for a receipt. Has a non-empty value if the order has `refunded` status.|
|`receipt_url`|string|The URL in Unlimint Game Services service for online access to the receipt.|
|`agreement_version`|string|The EULA agreement accepted by payment.|
|`agreement_accepted`|boolean|Has the value `true` if the agreement was accepted.|
|`notify_sale`|boolean|Has the value `true` if the customer confirmed to be informed about sales or discounts.|
|`notify_sale_email`|string|The customer's email for sales or discounts.|
|`issuer`|object|Details about an issuer.|
|&ensp;&ensp;`url`|string|The referer URL.|
|&ensp;&ensp;`embedded`|boolean|Has the value `true` if the Unlimint Game Services form was embedded to collect payment.|
|&ensp;&ensp;`reference`|string|The unique identifier for the entity linked to the order, for instance `paylink ID`.|
|&ensp;&ensp;`reference_type`|string|The type of an entity linked to the order, for instance `paylink`.|
|&ensp;&ensp;`utm_source`|string|The UTM-tag of the advertising system, for example: Bing Ads, Google Adwords.|
|&ensp;&ensp;`utm_medium`|string|The UTM-tag of the traffic type, e.g.: cpc, cpm, email newsletter.|
|&ensp;&ensp;`utm_campaign`|string|The UTM-tag of the advertising campaign, for example: Online games, Simulation game.|
|&ensp;&ensp;`referrer_host`|string|The host of the referrer URL.|
|`amount`|float|The total amount for the order. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|`currency`|string|The currency for the order. Three-letter Currency Code ISO 4217, in uppercase.|
|`user`|object|Details about a customer.|
|&ensp;&ensp;`id`|string|The customer unique identifier on the Unlimint Game Services side.|
|&ensp;&ensp;`object`|string|The string representing the object’s type. Value: `user`.|
|&ensp;&ensp;`external_id`|string|The customer unique identifier in the merchant project.|
|&ensp;&ensp;`name`|string|The customer's name.|
|&ensp;&ensp;`email`|string|The customer's email.|
|&ensp;&ensp;`email_verified`|boolean|Whether the customer’s email address has been verified in the merchant project.|
|&ensp;&ensp;`phone`|string|The customer’s phone number.|
|&ensp;&ensp;`phone_verified`|boolean|Whether the customer’s phone number has been verified in the merchant project.|
|&ensp;&ensp;`ip`|string|The customer’s IP address.|
|&ensp;&ensp;`locale`|string|The customer’s locale name. Four-letter language code in ISO 639, for instance en-US.|
|&ensp;&ensp;`address`|object|Details about a customer's address.|
|&ensp;&ensp;&ensp;&ensp;`country`|string|The customer’s country. Two-letter country code in ISO 3166-1, in uppercase.|
|&ensp;&ensp;&ensp;&ensp;`city`|string|The customer’s city.|
|&ensp;&ensp;&ensp;&ensp;`postal_code`|string|The customer’s postal code.|
|&ensp;&ensp;&ensp;&ensp;`state`|string|The customer’s state code in ISO 3166-2.|
|&ensp;&ensp;`metadata`|object|A string-value description that you can attach to the customer object. It can be useful for storing additional information about your customer's payment.|
|&ensp;&ensp;`notify_new_region`|boolean|Has the value `true` if the customer confirmed to receive the Unlimint Game Services newsletter about the beginning of payment acceptance in new regions.|
|&ensp;&ensp;`notify_new_region_email`|string|The customer's email for a newsletter about the beginning of payment acceptance in new regions.|
|`billing_address`|object|Details about a customer's billing address. Has a non-empty value if the customer was asked to fill it on a payment form. For all countries has a `country` value and for the USA has `country`, `state` and `zip`.|
|&ensp;&ensp;`country`|string|The customer's country. Two-letter country code in ISO 3166-1, in uppercase.|
|`tax`|object|Details about a tax.|
|&ensp;&ensp;`type`|string|The tax type (Sales tax for USA, VAT for EU and Russia).|
|&ensp;&ensp;`rate`|float|The current customer's location taxes. A positive float with two decimal points.|
|&ensp;&ensp;`amount`|float|The tax amount. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|&ensp;&ensp;`currency`|string|The currency for the tax. Three-letter Currency Code ISO 4217, in uppercase.|
|`net_revenue`|object|Details about the amount and currency of the transaction in the currency of payment to the client.|
|&ensp;&ensp;`amount`|float|The net revenue amount. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|&ensp;&ensp;`currency`|string|The currency for net revenue. Three-letter Currency Code ISO 4217, in uppercase.|
|`fee`|object|Details about Unlimint Game Services commission for a transaction in the currency of payment to the client.|
|&ensp;&ensp;`amount`|float|The fee amount. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|&ensp;&ensp;`currency`|string|The currency for the fee. Three-letter Currency Code ISO 4217, in uppercase.|
|`method`|object|Details about a payment method.|
|&ensp;&ensp;`title`|string|The human readable method name.|
|&ensp;&ensp;`external_id`|string|The unique identifier for the payment method.|
|&ensp;&ensp;`payment_system_id`|string|The unique identifier for the payment system on the Unlimint Game Services side.|
|&ensp;&ensp;`type`|string|The payment method's group alias.|
|&ensp;&ensp;`saved`|boolean|Has a value `true` if the payment method was saved by the customer for future usage.|
|&ensp;&ensp;`card`|object|Details about a customer's card.|
|&ensp;&ensp;&ensp;&ensp;`first6`|string|The first 6 digits of the card. Available only for a card method.|
|&ensp;&ensp;&ensp;&ensp;`last4`|string|The last 4 digits of the card. Available only for a card method.|
|&ensp;&ensp;&ensp;&ensp;`masked`|string|The mask for a customer's card. Available only for a card method.|
|&ensp;&ensp;&ensp;&ensp;`expiry_month`|string|The validity month of the card. Available only for a card method.|
|&ensp;&ensp;&ensp;&ensp;`expiry_year`|string|The validity year of the card. Available only for a card method.|
|&ensp;&ensp;&ensp;&ensp;`brand`|string|The brand of the card issuer. Available only for a card method.|
|&ensp;&ensp;&ensp;&ensp;`fingerprint`|string|The internal fingerprint for given card. Available only for a card method.|
|&ensp;&ensp;&ensp;&ensp;`secure3d`|string|Has a value `true` if 3D-secure was used during payment. Available only for a card method.|
|&ensp;&ensp;`wallet`|object|The name of the wallet. Available only for an integrated wallet payment systems.|
|&ensp;&ensp;&ensp;&ensp;`brand`|string|The name of the wallet.|
|&ensp;&ensp;&ensp;&ensp;`account`|string|The customer identity in the wallet.|
|&ensp;&ensp;`crypto_currency`|object|The name of the crypto currency. Available only for a crypto currency.|
|&ensp;&ensp;&ensp;&ensp;`brand`|string|The name of the crypto currency.|
|&ensp;&ensp;&ensp;&ensp;`address`|string|The customer's address in the crypto currency.|
|&ensp;&ensp;`refund_allowed`|boolean|Has a value `true` if a refund is allowed.|
|&ensp;&ensp;`recurring_allowed`|boolean|Has a `true` value if the payment method allows a recurring.|
|`items`|object[]|An array of OrderItem objects associated with current Order.|
|&ensp;&ensp;`id`|string|The unique identifier for the object.|
|&ensp;&ensp;`sku`|string|The stock keeping unit.|
|&ensp;&ensp;`name`|string|A localized name of the object.|
|&ensp;&ensp;`description`|string|A localized description of the object.|
|&ensp;&ensp;`images`|string[]|Image urls associated with the object.|
|&ensp;&ensp;`metadata`|object|A string-value description that attached to an object on creating a product.|
|&ensp;&ensp;`code`|string|An activation code of the object. Can be ommited if the order is not processed or type of the order does not equal `key`.|
|&ensp;&ensp;`platform`|string|A platform for an activation code. Can be ommited if the order is not processed or type of the order does not equal `key`.|
|`refund`|object|Details about a refund.|
|&ensp;&ensp;`amount`|float|The refund amount. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|&ensp;&ensp;`currency`|string|The currency for the tax. Three-letter Currency Code ISO 4217, in uppercase.|
|&ensp;&ensp;`reason`|string|The refund reason.|
|&ensp;&ensp;`code`|string|The Unlimint Game Services internal identity for the refund reason.|
|&ensp;&ensp;`receipt_number`|string|The unique identifier for the refund receipt.|
|&ensp;&ensp;`receipt_url`|string|The URL in Unlimint Game Services service for online access to given refund receipt.|
|`metadata`|object|A string-value description that you can attach to the order object. It can be useful for storing additional information about your customer payment.|
|`original_amount`|float|The order amount excluding any taxes and commissions.|
|`country`|string|Two-letter country code in ISO 3166-1, in uppercase.|
|`type`|string|The order type. It depends on your sales option (Game Keys, Virtual Items, the simple checkout). For products created as Game Keys use the `key` type, as Virtual Items - the `product` type, for a simple checkout - the `simple` type. **Enum values:** key, products, simple.|
|`platform_id`|string|The default platform identifier for which customer buys the in-game key. This field used only for a payment type `key`. **Enum values:** steam, gog, uplay, origin, psn, xbox, nintendo, itch, egs.|
|`receipt_id`|string|The receipt unique identifier.|
|`virtual_currency_amount`|float|The virtual currancy amount for the order.|
|`is_buy_for_virtual_currency`|boolean|Has a value `true` if the order created for a virtual currency.|
|`charge_currency`|string|The currency of the order charge. It can differ from the order currency because it also depends on the customer's card currency.|
|`charge_amount`|float|The total amount of the order charge.|
|`vat_payer`|float|The responsible for VAT. Available values: `buyer` (VAT is added to the order charge), `seller` (VAT is included in the order charge), `nobody` (VAT exempt).|
|`is_production`|boolean|Has a `true` value for a production payment and false for a test payment that goes through a test sandbox.|
|`testing_case`|string|The webhook testing mode. Available values: `correct_payment`, `non_existing_user`, `existing_user`, `invalid_signature`.|
|`form_mode`|string|The opening mode of the payment form on the project side. Available values: `embed`, `iframe`, `standalone`. Default value: `embed`.|
|`merchant_info`|object|The merchant's company data.The merchant's company data.|
|&ensp;&ensp;`company_name`|string|The merchant's company name.|
|&ensp;&ensp;`agreement_number`|string|The merchant's license agreement number.|
|`recurring`|boolean|Exists recurring payments for the order.|
|`recurring_id`|string|Unique recurring identity.|

## Create a payment order

> Code samples

```shell
curl -X POST \
  https://checkout.pay.super.com/api/v1/order \
  -H 'Content-Type: application/json' \
  -H 'X-API-SIGNATURE: YOUR_SECRET_KEY \
  -d '{
    "project": "5db16ae811bf0d0001fdfbd1",
    "amount": 10,
    "currency": "USD",
    "type": "simple",
  "user": {
      "external_id": "58799f2c2564296bd2cb",
      "email": "user.email@example.com",
      "email_verified": true
    }
}'

```

### POST /api/v1/order

Create a payment order with a customer and order data

> Body parameters

```json
{
  "project": "string",
  "amount": 0,
  "currency": "string",
  "account": "string",
  "description": "string",
  "metadata": {
    "property1": "string",
    "property2": "string"
  },
  "url_success": "string",
  "url_fail": "string",
  "products": [
    "string"
  ],
  "token": "string",
  "user": {
    "external_id": "string",
    "name": "string",
    "email": "string",
    "email_verified": true,
    "phone": "string",
    "phone_verified": true,
    "ip": "string",
    "locale": "string",
    "address": {
      "country": "string",
      "city": "string",
      "postal_code": "string",
      "state": "string"
    }
  },
  "order": "string",
  "type": "string",
  "platform_id": "string"
}
```

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`project` <span style="color: red;">*</span> |string|The ID of the Project found in your merchant account in the Unlimint Game Services Dashboard.|
|`amount`|number|The order amount as a positive number. It is required for a simple checkout payment.|
|`currency`|string|The currency of the order. Three-letter Currency Code ISO 4217, in uppercase. If provided, the amount will be processed in this currency. It is required for a payment when the type equals to simple.|
|`account`|string|The customer account in the merchant project.|
|`description`|string|The arbitrary order description.|
|`metadata`|object|A string-value description that you can attach to the order object. It can be useful for storing additional information about your customer's payment.|
|`url_success`|string|The redirect URL for the successful payment. You need to enable the dynamic notify URLs option in the Project Settings to use this field.|
|`url_fail`|string|The redirect URL for the failed payment. You need to enable the dynamic notify URLs option in the Project Settings to use this field.|
|`products`|[string]|The list of unique identifiers of Products being in the Project. It is required if a payment type is equal to product or key.|
|`token`|string|An encrypted string that represents certain details of your customer (such as the customer ID, email and others), a game and purchase parameters. The token overrides the corresponding parameters (including required parameters) in an order object.|
|`user`|object|The customer data.|
|&ensp; `external_id`|string|The unique identifier for the customer in the merchant project.|
|&ensp; `name`|string|The customer's name.|
|&ensp; `email`|string|The customer's email address.|
|&ensp; `email_verified`|boolean|Whether the customer's email address has been verified on the merchant side.|
|&ensp; `phone`|string|The customer's phone number.|
|&ensp; `phone_verified`|boolean|Whether the customer's phone number has been verified on the merchant side.|
|&ensp; `ip`|string|The customer's IP address.|
|&ensp; `locale`|string|The customer's locale name. The language code in ISO 639-1 (for instance en-US).|
|&ensp; `address`|object|The customer's address data.|
|&ensp; &ensp; `country`|string|The customer's country. Two-letter country code in ISO 3166-1, in uppercase (for instance US).|
|&ensp; &ensp; `city`|string|The customer’s city.|
|&ensp; &ensp; `postal_code`|string|The customer's postal code.|
|&ensp; &ensp; `state`|string|The customer's state code in ISO 3166-2.|
|&ensp; `order`|string|The Unlimint Game Services unique identifier for the order.|
|&ensp; `type` <span style="color: red;">*</span> |string|The order type. It depends on your sales option (Game Keys, Virtual Items, Virtual Currency the simple checkout). For products created as Game Keys use the key type, as Virtual Items - the product type, as Virtual Currency - the virtual_currency type, for a simple checkout - the simple type. Enum values: key, product, virtual_currency, simple.|
|&ensp; `platform_id`|string|The default platform's name for which the customer buys a key. This field is used only for the key type. Enum values: steam, gog, uplay, origin, psn, xbox, nintendo, itch, egs.|

### Responses

> Example responses

> 200 Response

```json
{
  "id": "string",
  "payment_form_url": "string"
}
```

### 200 Returns the order ID and payment form URL

||||
|---|---|---|
|`id`|string|The unique identifier for the order.|
|`payment_form_url`|string|The URL of the Unlimint Game Services-hosted payment form.|

### 400 The error code and message with the error details

||||
|---|---|---|
|`code`|string|The error code.|
|`message`|string|The error short description.|
|`details`|string|The error details.|

### 500 Internal Server Error

||||
|---|---|---|
|`code`|string|The error code.|
|`message`|string|The error short description.|
|`details`|string|The error details.|