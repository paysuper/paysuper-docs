---
title: PaySuper API Reference
language_tabs:
  - shell: cURL
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

# Order

You can create a payment order with details about your customer and sales option data.

### Statuses

|Name|Description|
|---|---|
|`created`|It’s an initial state of the requested order but it is not processed in a payment system yet. The `created` order can become one of the statuses: `processed`, `canceled`, `rejected`.|
|`processed`|The order is successfully processed in the payment system. The `processed` order can become `refunded` or `chargeback`.|
|`rejected`|The order is rejected by a payment system with any reasons.|
|`canceled`|The order is canceled by a user.|
|`refunded`|The processed order is refunded by a merchant request.|
|`chargeback`|The processed order is refunded by a payment system with any reasons.|

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
      "phone": "0639597531",
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
|`id`|string|The unique identifier for the object.|
|`transaction`|string|The unique identifier for the transaction in the payment system.|
|`object`|string|The string representing the object’s type. Value: `order`.|
|`status`|string|The current status of the order.|
|`description`|string|An arbitrary string attached to the object. If this field was not sent, the PaySuper generates it automatically.|
|`created_at`|string|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) at which the order was created.|
|`canceled_at`|string|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) at which the order was cancelled.|
|`canceled`|boolean|Has the value `true` if the current order was canceled.|
|`cancellation`|object|The cancellation reason. Has the value `null` if the order is not canceled.|
|`· code`|string|The cancellation reason code.|
|`· reason`|string|The cancellation description.|
|`refunded`|boolean|Has the value `true` if the current order was refunded.|
|`refunded_at`|string|The date and time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) at which the order was refunded.|
|`receipt_email`|string|The customer's email for receipt information.|
|`receipt_phone`|string|The customer's phone for receipt information.|
|`receipt_number`|string|The unique identifier for a receipt. Has a non-empty value if the order has `refunded` status.|
|`receipt_url`|string|The URL in PaySuper service for online access to the receipt.|
|`agreement_version`|string|The EULA agreement accepted by payment.|
|`agreement_accepted`|boolean|Has the value `true` if the agreement was accepted.|
|`notify_sale`|boolean|Has the value `true` if a user confirmed to be informed about feature sales or discounts.|
|`notify_sale_email`|string|The customer's email for sales or discounts.|
|`issuer`|object|Details about an issuer.|
|`· url`|string|The referer URL.|
|`· embedded`|boolean|Has the value `true` if the PaySuper form was embedded to collect payment.|
|`· reference`|string|The unique identifier of an entity linked to the order, for instance `paylink ID`.|
|`· reference_type`|string|The type of an entity linked to the order, for instance `paylink`.|
|`· utm_source`|string|The UTM-tag of the advertising system, for example: Bing Ads, Google Adwords.|
|`· utm_medium`|string|The UTM-tag of the traffic type, e.g.: cpc, cpm, email newsletter.|
|`· utm_campaign`|string|The UTM-tag of the advertising campaign, for example: Online games, Simulation game.|
|`· referrer_host`|string|The host of the referrer URL.|
|`amount`|float|The total amount for the order. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|`currency`|string|The currency for the order. Three-letter Currency Code ISO 4217, in uppercase.|
|`user`|object|Details about a customer.|
|`· id`|string|The user unique identifier on the PaySuper side.|
|`· object`|string|The string representing the object’s type. Value: `user`.|
|`· external_id`|string|The user unique identifier in the merchant project.|
|`· name`|string|The user's name.|
|`· email`|string|The user's email.|
|`· email_verified`|boolean|Whether the user’s email address has been verified in the merchant project.|
|`· phone`|string|The user’s phone number.|
|`· phone_verified`|boolean|Whether the user’s phone number has been verified in the merchant project.|
|`· ip`|string|	The user’s IP address.|
|`· locale`|string|The user’s locale name. Four-letter language code by ISO 639, for instance en-US.|
|`· address`|object|Details about a user's address.|
|`·· country`|string|The user’s country. Two-letter language code by ISO 3166-1, in uppercase.|
|`·· city`|string|The user’s city.|
|`·· postal_code`|string|The user’s postal code.|
|`·· state`|string|The user’s state code by ISO 3166-2.|
|`· metadata`|object|A string-value description that you can attach to the user object. It can be useful for storing additional information about your customer's payment.|
|`· notify_new_region`|boolean|Has the value `true` if a user confirmed to receive the PaySuper newsletter about the beginning of payment acceptance in new regions.|
|`· notify_new_region_email`|string|The customer's email for a newsletter about the beginning of payment acceptance in new regions.|
|`billing_address`||Details about a user's billing addres. Has a non-empty value if the user was asked to fill it on a payment form. For all countries has a `country` value and for the USA has `country`, `state` and `zip`.|
|`· country`|string|The user's country. Two-letter language code by ISO 3166-1, in uppercase.|
|`tax`|object|Details about a tax.|
|`· type`|string|The tax type (Sales tax for USA, VAT for EU and Russia).|
|`· rate`|float|The current user's location taxes. A positive float with two decimal points.|
|`· amount`|float|The tax amount. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|`· currency`|string|The currency for the tax. Three-letter Currency Code ISO 4217, in uppercase.|
|`method`||Details about a payment method.|
|`· title`|string|The human readable method name.|
|`· external_id`|string|The unique identifier of the payment method.|
|`· payment_system_id`|string|The unique identifier of payment system on the PaySuper side.|
|`· saved`|boolean|Has a value `true` if a payment method was saved by a user for a future usage.|
|`· card`|object|Details about a user's card.|
|`·· first6`|string|The first 6 digits of the card. Available only for a card method.|
|`·· last4`|string|The last 4 digits of the card. Available only for a card method.|
|`·· masked`|string|The mask for a user's card. Available only for a card method.|
|`·· expiry_month`|string|The validity month of the card. Available only for a card method.|
|`·· expiry_year`|string|The validity year of the card. Available only for a card method.|
|`·· brand`|string|The brand of the card issuer. Available only for a card method.|
|`·· fingerprint`|string|The internal fingerprint for given card. Available only for a card method.|
|`·· secure3d`|string|Has a value `true` if 3D-secure was used during payment. Available only for a card method.|
|`· wallet`|object|The name of the wallet. Available only for an integrated wallet payment systems.|
|`·· brand`|string|The name of the wallet.|
|`·· account`|string|The customer identity in the wallet.|
|`· crypto_currency`|object|The name of the crypto currency. Available only for a crypto currency.|
|`·· brand`|string|The name of the crypto currency.|
|`·· address`|string|The customer's address in the crypto currency.|
|`· refund_allowed`|boolean|Has a value `true` if a refund is allowed.|
|`items`|object[]|An array of OrderItem objects associated with current Order.|
|`· id`|string|The unique identifier of the object.|
|`· sku`|string|The stock keeping unit.|
|`· name`|string|A localized name of the object.|
|`· description`|string|A localized description of the object.|
|`· images`|string[]|Image urls associated with the object.|
|`· metadata`|object|A string-value description that attached to an object on creating a product.|
|`· code`|string|An activation code of the object. Can be ommited if the order is not processed or type of the order does not equal `key`.|
|`· platform`|string|A platform for an activation code. Can be ommited if the order is not processed or type of the order does not equal `key`.|
|`refund`|object|Details about a refund.|
|`· amount`|float|The refund amount. A positive float with two decimal points (e.g., 1.00 to charge $1.00).|
|`· currency`|string|The currency for the tax. Three-letter Currency Code ISO 4217, in uppercase.|
|`· reason`|string|The refund reason.|
|`· code`|string|The PaySuper internal identity for the refund reason.|
|`· receipt_number`|string|The unique identifier of the refund receipt.|
|`· receipt_url`|string|The URL in PaySuper service for online access to given refund receipt.|
|`metadata`|object|A string-value description that you can attach to the order object. It can be useful for storing additional information about your customer payment.|
|`original_amount`|float|The order amount excluding any taxes and commissions.|
|`country`|string|Two-letter language code by ISO 3166-1, in uppercase.|
|`type`|string|The order type. It depends on your sales option (Game Keys, Virtual Items, the simple checkout). For products created as Game Keys use the `key` type, as Virtual Items - the `product` type, for a simple checkout - the `simple` type. **Enum values:** key, products, simple.|
|`platform_id`|string|The default platform identifier for which customer buys the in-game key. This field used only for a payment type `key`. **Enum values:** steam, gog, uplay, origin, psn, xbox, nintendo, itch, egs.|
|`receipt_id`|string|The receipt unique identifier.|
|`virtual_currency_amount`|float|The virtual currancy amount for the order.|
|`is_buy_for_virtual_currency`|boolean|Has a value `true` if the order created for a virtual currency.|

## Create a payment order

> Code samples

```shell
curl -X POST \
  https://api.pay.super.com/api/v1/order \
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

Create a payment order with details about your customer and sales option data.

> Body parameter

```json
{
  "account": "string",
  "amount": 0,
  "currency": "string",
  "description": "string",
  "order_id": "string",
  "project": "string",
  "url_fail": "string",
  "url_success": "string",
  "type": "key",
  "products": [
    "string"
  ],
  "platform_id": "steam",
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
    },
    "metadata": {}
  }
}
```

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`body`  <br><p style="color: red;">required</p> ||Parameters to create a payment order.  |
|`· account` | string |The user unique account in the Project.  |
|`· amount` | number |The order amount as a positive number. It is required for a simple checkout payment.  |
|`· currency` | string |The currency of the order. Three-letter Currency Code ISO 4217, in uppercase.  If provided, the amount will be processed in this currency.  It is required for a simple checkout payment.  |
|`· description` | string |The arbitrary order description.  |
|`· order_id` | string |The unique order identifier on the merchant side. This field is not required, but we recommend sending this field always.  |
|`· project`  <br><p style="color: red;">required</p> | string |The ID of the Project found in your merchant account in the PaySuper Dashboard.  |
|`· url_fail` | string |The redirect URL for the failed payment.  Enable the dynamic notify URLs option in the Project Settings to use this field.  |
|`· url_success` | string |The redirect URL for the successful payment.  Enable the dynamic notify URLs option in the Project Settings to use this field.  |
|`· type`  <br><p style="color: red;">required</p> | string |The order type. It depends on your sales option (Game Keys, Virtual Items, the simple checkout). For products created as Game Keys use the `key` type,  as Virtual Items - the `product` type, for a simple checkout - the `simple` type. <br>**Enum values:** <br>key<br>product<br>simple |
|`· products` | [string] |The list of unique identifiers of Products being in the Project. It is required if a payment type is equal to 'product' or 'key'.  |
|`· platform_id` | string |The default platform identifier for which customer buys the in-game key. This field used only for a payment type 'key'. <br>**Enum values:** <br>steam<br>gog<br>uplay<br>origin<br>psn<br>xbox<br>nintendo<br>itch<br>egs |
|`· token` | string |An encrypted string that represents certain details of your customer (such as the user ID, email and others), a game and purchase parameters. The token overrides the corresponding parameters in an order object even the required parameters.  |
|`· user` ||   |
|`·· external_id` | string |The user unique identifier in the merchant project.  |
|`·· name` | string |The user's name.  |
|`·· email` | string |The user's email address.  |
|`·· email_verified` | boolean |Whether the user's email address has been verified on the merchant side.  |
|`·· phone` | string |The user's phone number.  |
|`·· phone_verified` | boolean |Whether the user’s phone number has been verified on the merchant side.  |
|`·· ip` | string |The user's IP address.  |
|`·· locale` | string |The user's locale name. Two-letter language code by ISO 639-1, in lowercase.  |
|`·· address` ||   |
|`··· country` | string |The user's country. Two-letter language code by ISO 3166-1, in lowercase.  |
|`··· city` | string |The user's city.  |
|`··· postal_code` | string |The user's postal code.  |
|`··· state` | string |The user's state code by ISO 3166-2.  |
|`·· metadata` | object |A string-value description that you can attach to the user object. It can be useful for storing additional information about your customer's payment.  |

### Responses

> Example responses

> 200 Response

```json
{
  "id": "string",
  "payment_form_url": "string"
}
```

### 200 An object with the unique identifier of the order and a PaySuper-hosted URL of a payment form.

||||
|---|---|---|
|`· id` |string|The unique identifier for the order.  |
|`· payment_form_url` |string|The PaySuper-hosted URL of payment form.  |

### 400 An error message object with a reason.

||||
|---|---|---|
|`· message` |string|A description of the error.  |
|`· code` |string|A status code of the error.  |

### 401 An error message object with an unauthorized reason.

||||
|---|---|---|
|`· message` |string|A description of the error.  |
|`· code` |string|A status code of the error.  |

### 500 An error message object with a reason on the PaySuper server side.

||||
|---|---|---|
|`· message` |string|A description of the error.  |
|`· code` |string|A status code of the error.  |

# Token

A token is an encrypted string that represents certain details of your customer (such as the user ID, email and others), a game and purchase parameters.

## Create a token

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

Create a token that encrypts certain details of your customer, a game and purchase parameters.

> Body parameter

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
    },
    "metadata": {}
  },
  "settings": {
    "project_id": "string",
    "return_url": {
      "success": "string",
      "fail": "string"
    },
    "currency": "string",
    "amount": 0,
    "products_ids": [
      "string"
    ],
    "description": "string",
    "type": "simple",
    "metadata": {}
  }
}
```

|PARAMETER|TYPE|DESCRIPTION|
|---|---|---|
|`body`  <br><p style="color: red;">required</p> ||Parameters to create a token.  |
|`· user`  <br><p style="color: red;">required</p> ||   |
|`·· id`  <br><p style="color: red;">required</p> | string |The user unique identifier in the merchant project.  |
|`·· email` | object |The user’s email address.  |
|`··· value`  <br><p style="color: red;">required</p> | string |The parameter value.  |
|`··· verified` | boolean |Whether the value has been verified on the merchant side.  |
|`·· phone` | object |   |
|`··· value`  <br><p style="color: red;">required</p> | string |The parameter value.  |
|`··· verified` | boolean |Whether the value has been verified on the merchant side.  |
|`·· name` | object |The user’s name.  |
|`··· value`  <br><p style="color: red;">required</p> | string |The parameter value.  |
|`·· ip` | object |The user’s IP address.  |
|`··· value`  <br><p style="color: red;">required</p> | string |The parameter value.  |
|`·· locale` | object |The user’s locale name. Two-letter language code by ISO 639-1, in lowercase.  |
|`··· value`  <br><p style="color: red;">required</p> | string |The parameter value.  |
|`·· address` ||   |
|`··· country` | string |The user's country. Two-letter language code by ISO 3166-1, in lowercase.  |
|`··· city` | string |The user's city.  |
|`··· postal_code` | string |The user's postal code.  |
|`··· state` | string |The user's state code by ISO 3166-2.  |
|`·· metadata` | object |A string-value description that you can attach to the user object. It can be useful for storing additional information about your customer's payment.  |
|`· settings`  <br><p style="color: red;">required</p> ||   |
|`·· project_id`  <br><p style="color: red;">required</p> | string |The ID of the Project found in your merchant account in the PaySuper Dashboard.  |
|`·· return_url` ||   |
|`··· success` | string |The redirect URL for the successful payment.  |
|`··· fail` | string |The redirect URL for the failed payment.  |
|`·· currency` | string |The currency of the order. Three-letter Currency Code ISO 4217, in uppercase.  If provided, the amount will be processed in this currency.  It is required for a simple checkout payment.  |
|`·· amount` | number |The order amount as a positive number. It is required for a simple checkout payment.  |
|`·· products_ids` | [string] |The list of unique identifiers of Products being in the Project. It is required if a payment type is equal to 'product' or 'key'.  |
|`·· description` | string |The arbitrary order description.  |
|`·· type`  <br><p style="color: red;">required</p> | string |The order type. It depends on your sales option (Game Keys, Virtual Items, the simple checkout). For products created as Game Keys use the 'key' type,  as Virtual Items - the 'product' type, for a simple checkout - the 'simple' type. <br>**Enum values:** <br>simple<br>product<br>key |
|`·· metadata` | object |A string-value description that you can attach to the user object. It can be useful for storing additional information about your customer's payment.  |

### Responses

> Example responses

> 200 Response

```json
{
  "token": "string",
  "payment_form_url": "string"
}
```

### 200 An object with a token string and a PaySuper-hosted URL of a payment form.

||||
|---|---|---|
|`· token`  <br><p style="color: red;">required</p> |string|A secure string which contains encrypted information about your customer and sales option data.  |
|`· payment_form_url` |string|The PaySuper-hosted URL of payment form.  |

### 400 An error message object with a reason.

||||
|---|---|---|
|`· message` |string|A description of the error.  |
|`· code` |string|A status code of the error.  |

### 500 An error message object with a reason on the PaySuper server side.

||||
|---|---|---|
|`· message` |string|A description of the error.  |
|`· code` |string|A status code of the error.  |

