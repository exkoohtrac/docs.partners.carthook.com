# Webhooks

## Summary 
This is the Webhooks section of our documentation.

## API Push Calls
1. Checkouts 
    1. `/checkouts/created` - Sent via webhook subscription when cart is created
    2. `/checkouts/completed` - Sent via webhook subscription when cart is closed
    3. `/checkouts/updated` - Sent via webhook subscription when cart is updated
        1. email input (available regardless of subscribe checkbox)
        2. sms input (only if consent provided)
        3. When users move through the upsell/downsell flow and they accept an offer (or reject), send a /checkouts/updated WebHook. This ensures that consumers like cart abandoned apps don't send out an abandoned email too fast. <br>
            <sub>Example: A shopper lands on a checkout page. He has 10 minutes of inactivity on each upsell/downsell before we close the order down automatically, and that timer refreshes every time he reaches a new page (i.e. next upsell). We need to send an checkouts/updated with the new page that he's currently on so that consumers (i.e. cart abandoned apps) do not assume a cart has been abandoned.</sub>
2. App
    1. `app/uninstalled` - Sent via webhook subscription when a merchant uninstalls the app

<br>

#### PUSH `/checkouts/created`
Upon the creation of a shopper’s checkout for a specific merchant, push the checkout data to all apps

1. that have been installed by the merchant and 
2. that have webhooks subscribing to /checkouts/created

This event will fire as soon as a shopper adds a product to their “cart” from either the landing page or checkout page of a CartHook funnel.

```
{
  "id": "cev_P12jn3Qzexr",
  "webhook_id": "cwe_Sai45cWed",
  "cid": "cid_xxxxxx",
  "merchant_id": "cmid_PxVEpmJar8xr9Qe86ZvD",
  "store_url": "store.myshopify.com",
  "funnel_id": "cfu_Sa9473Cf21",
  "currency": "USD",
  "subtotal_price": 247.5,
  "total_price": 275.97,
  "cart_url": "<CARTHOOK_CHECKOUT_CART_URL>",
  "funnel_step": "checkout_page",
  "line_items": [
    {
      "product_id": "39117609670",
      "variant_id": "39607609670",
      "discounted_price": 48.8,
      "price": 49,
      "quantity": 5,
      "sku": "SKU-XL-RED",
      "tax_amount": 4.39,
      "tax_rate": 0.09,
      "taxable": true,
      "title": "Average Oceanic Rock"
    },
    {
      "product_id": "39117609670",
      "variant_id": "39607609670",
      "discounted_price": 2.5,
      "price": 2.5,
      "quantity": 1,
      "sku": "SKU-XL-RED",
      "tax_amount": 0.23,
      "tax_rate": 0.09,
      "taxable": true,
      "title": "Average Oceanic Rock"
    }
  ]
}
```

<br>


#### PUSH `/checkouts/updated`
Sent via webhook subscription when cart is updated by:
1. email input (available regardless of subscribe checkbox)
2. sms input (only if consent provided)
3. When users move through the upsell/downsell flow and they accept an offer (or reject), send a /checkouts/updated WebHook. This ensures that consumers like cart abandoned apps don't send out an abandoned email too fast. <br>
<sub>Example: A shopper lands on a checkout page. He has 10 minutes of inactivity on each upsell/downsell before we close the order down automatically, and that timer refreshes every time he reaches a new page (i.e. next upsell). We need to send an checkouts/updated with the new page that he's currently on so that consumers (i.e. cart abandoned apps) do not assume a cart has been abandoned.</sub>

```
{
  "id": "cev_P12jn3Qzexr",
  "webhook_id": "cwe_Sai45cWed",
  "cid": "cid_xxxxxx",
  "merchant_id": "cmid_PxVEpmJar8xr9Qe86ZvD",
  "store_url": "store.myshopify.com",
  "funnel_id": "cfu_Sa9473Cf21",
  "currency": "USD",
  "subtotal_price": 247.5,
  "total_price": 275.97,
  "cart_url": "<CARTHOOK_CHECKOUT_CART_URL>",
  "funnel_step": "checkout_page",
  "customer": {
    "email": "customer+email@carthook.com",
    "first_name": "First",
    "last_name": "Last",
    "buyer_accepts_marketing": true
  },
  "selected_shipping_rates": [
    {
      "title": "Priority Mail",
      "price": 7.29,
      "code": "Priority",
      "source": "usps",
      "carrier_identifier": null,
      "requested_fulfillment_service_id": null
    }
  ],
  "coupons": [
    {
      "coupon_code": "1DOLLAROFF",
      "coupon_type": "amount_off",
      "coupon_source": "shopify",
      "amount": 1,
      "title": "Some Coupon"
    }
  ],
  "shipping_address": {
    "first_name": "First",
    "last_name": "Last",
    "company": "Company",
    "address1": "Address 1",
    "address2": "Address 2",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": "12345678"
  },
  "billing_address": {
    "first_name": "First",
    "last_name": "Last",
    "company": "Company",
    "address1": "Address 1",
    "address2": "Address 2",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": "12345678"
  },
  "line_items": [
    {
      "product_id": "39117609670",
      "variant_id": "39607609670",
      "discounted_price": 48.8,
      "price": 49,
      "quantity": 5,
      "sku": "SKU-XL-RED",
      "tax_amount": 4.39,
      "tax_rate": 0.09,
      "taxable": true,
      "title": "Average Oceanic Rock"
    },
    {
      "product_id": "39117609670",
      "variant_id": "39607609670",
      "discounted_price": 2.5,
      "price": 2.5,
      "quantity": 1,
      "sku": "SKU-XL-RED",
      "tax_amount": 0.23,
      "tax_rate": 0.09,
      "taxable": true,
      "title": "Average Oceanic Rock"
    }
  ]
}
```

<br>


#### PUSH `/checkouts/completed`
Close the order and send a `/checkouts/completed` webhook notification when:
 1. a shopper finishes the flow and reaches the Thank you page
 2. a shopper abandons an upsell and our abandoned worker dispatches this order into Shopify

```
{
  "id": "cev_P12jn3Qzexr",
  "webhook_id": "cwe_Sai45cWed"
  "cid": "cid_xxxxxx",
  "merchant_id": "cmid_PxVEpmJar8xr9Qe86ZvD",
  "store_url": "store.myshopify.com",
  "funnel_id": "cfu_Sa9473Cf21",
  "customer": {
    "email": "customer+email@carthook.com",
    "first_name": "First",
    "last_name": "Last",
    "buyer_accepts_marketing": true
  },
  "carthook_order_id": "PcA4raUZdta1vTsJdcLb",
  "currency": "USD",
  "subtotal_price": 247.5,
  "total_price": 275.97,
  "total_coupons_amount": 1,
  "order_number": "CH-1234",
  "order_id": "4214124124124124121241",
  "payment_gateway": "stripe",
  "shipping_address": {
    "first_name": "First",
    "last_name": "Last",
    "company": "Company",
    "address1": "Address 1",
    "address2": "Address 2",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": "12345678"
  },
  "billing_address": {
    "first_name": "First",
    "last_name": "Last",
    "company": "Company",
    "address1": "Address 1",
    "address2": "Address 2",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": "12345678"
  },
  "line_items": [
    {
      "product_id": "39117609670",
      "variant_id": "39607609670",
      "discounted_price": 48.8,
      "price": 49,
      "quantity": 5,
      "sku": "SKU-XL-RED",
      "tax_amount": 4.39,
      "tax_rate": 0.09,
      "taxable": true,
      "title": "Average Oceanic Rock"
    },
    {
      "product_id": "39117609670",
      "variant_id": "39607609670",
      "discounted_price": 2.5,
      "price": 2.5,
      "quantity": 1,
      "sku": "SKU-XL-RED",
      "tax_amount": 0.23,
      "tax_rate": 0.09,
      "taxable": true,
      "title": "Average Oceanic Rock"
    }
  ],
  "selected_shipping_rates": [
    {
      "title": "Priority Mail",
      "price": 7.29,
      "code": "Priority",
      "source": "usps",
      "carrier_identifier": null,
      "requested_fulfillment_service_id": null
    }
  ],
  "coupons": [
    {
      "coupon_code": "1DOLLAROFF",
      "coupon_type": "amount_off",
      "coupon_source": "shopify",
      "amount": 1,
      "title": "Some Coupon"
    }
  ]
}
```


<br>


#### PUSH `/app/uninstalled`
Send out an `app/uninstalled` topic whenever a merchant uninstalls the app from their store.

- `id` is the id of the event that can retry n-times based on your APIs response (always starts with cev_)
- `webhook_id` is the same ID of the webhook at the time of subscription to the webhook
- `merchant_id` is the ID of a merchant that is accessible from the /merchant endpoint at any time

```
{ 
    "id":"cev_941942192",
    "webhook_id": "cwe_91249124",
    "merchant_id": "cmid_KixEkfTj"
}
```
