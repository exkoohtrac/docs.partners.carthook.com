# API Calls

## Summary 
CartHook exposes a public `CH` window variable, with an `.event()` callback function. You can use that `.event()`  callback function to subscribe to specific page events. This is used to track specific user events, but NOT purchase events.

<br>

#### Basic Event structure

```
CH.event(callbackSuccess, callbackError);
```

###### Example
```
CH.event(function(EVENT, data) {
    console.log(EVENT, data);
}, function(EVENT, error) {
    console.log(EVENT, error);
});
```
<br>

The available **EVENT**(s) are based on the page type and are as followed: 

<br>

### Checkout page events:
- `INITIATED_PAGE`
- `INPUT_EMAIL` 
- `FETCHED_SHIPPING`
- `FETCHED_TAXES` 
- `FETCHED_COUPON_CODE` 

<br> <br>

#### Page initiated event
Event: `INITIATED_PAGE`
```
{
  "cart_data": {
    "coupon": null,
    "currency": "USD",
    "subtotal_price": 8,
    "total_price": 8,
    "total_coupons_amount": 0,
    "token": null,
    "line_items": [
      {
        "id": "9993963462",
        "variant_id": "39607598598",
        "grams": "0.00",
        "line_price": "8.00",
        "price": "8.00",
        "quantity": 1,
        "sku": "",
        "taxable": true,
        "title": "Big Honk'n Rock",
        "body_html": "<p>Wow. What to say?w</p>",
        "handle": "big-honkn-rock",
        "image": "https://cdn.shopify.com/s/files/1/1853/8535/products/weird_rock.jpg?v=1489713431",
        "variant_title": "l",
        "vendor": "Rok's Rocks"
      }
    ]
}
```

<br> <br>

#### Input email event
Event: `INPUT_EMAIL`
```
{
  "email": "tech@carthook.com",
  "cart_data": {
    "coupon": null,
    "currency": "USD",
    "subtotal_price": 8,
    "total_price": 8,
    "total_coupons_amount": 0,
    "token": null,
    "line_items": [
      {
        "id": "9993963462",
        "variant_id": "39607598598",
        "grams": "0.00",
        "line_price": "8.00",
        "price": "8.00",
        "quantity": 1,
        "sku": "",
        "taxable": true,
        "title": "Big Honk'n Rock",
        "body_html": "<p>Wow. What to say?w</p>",
        "handle": "big-honkn-rock",
        "image": "https://cdn.shopify.com/s/files/1/1853/8535/products/weird_rock.jpg?v=1489713431",
        "variant_title": "l",
        "vendor": "Rok's Rocks"
      }
    ]
}
```

<br> <br>

#### Fetched shipping event
Event: `FETCHED_SHIPPING`
```
{
  "customer": {
    "buyer_accepts_marketing": true,
    "email": "tech@carthook.com"
  },
  "billing_address": {
    "first_name": "John",
    "last_name": "Doe",
    "company": "CartHook",
    "address1": "834 Fieldcrest Road",
    "address2": "",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": ""
  },
  "shipping_address": {
    "first_name": "John",
    "last_name": "Doe",
    "company": "CartHook",
    "address1": "834 Fieldcrest Road",
    "address2": "",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": ""
  }
}
```

<br> <br>

#### Fetched taxes event
Event: `FETCHED_TAXES`
```
{
  "customer": {
    "buyer_accepts_marketing": true,
    "email": "tech@carthook.com"
  },
  "shipping_address": {
    "first_name": "John",
    "last_name": "Doe",
    "company": "CartHook",
    "address1": "834 Fieldcrest Road",
    "address2": "",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": ""
  },
  "tax_rate": {
    "0": {
      "variant_id": 39607598598,
      "rate": 0.08875
    },
    "1": {
      "variant_id": 39607598598,
      "rate": 0.08875
    },
    "2": {
      "variant_id": 39607598662,
      "rate": 0.08875
    }
  }
}
```


<br> <br>

#### Fetched coupon event
Event: `FETCHED_COUPON_CODE`
```
{
  "cart_data": {
    "coupon": {
      "id": 12,
      "description": "ilovestuff",
      "coupon_code": "ilovestuff",
      "coupon_type": "percent_off",
      "amount": "10.00",
      "max_redemptions": "0",
      "used_redemptions": "19",
      "ends_on": null,
      "deleted_at": null,
      "total_minus": 0.8
    },
    "currency": "USD",
    "subtotal_price": 8,
    "total_price": 8,
    "total_coupons_amount": 0.8,
    "token": null,
    "line_items": [
      {
        "id": "9993963462",
        "variant_id": "39607598598",
        "discounted_price": 7.2,
        "grams": "0.00",
        "line_price": "8.00",
        "price": "8.00",
        "quantity": 1,
        "sku": "",
        "taxable": true,
        "title": "Big Honk'n Rock",
        "body_html": "<p>Wow. What to say?w</p>",
        "handle": "big-honkn-rock",
        "image": "https://cdn.shopify.com/s/files/1/1853/8535/products/weird_rock.jpg?v=1489713431",
        "variant_title": "l",
        "vendor": "Rok's Rocks"
      }
    ]
  },
  "customer": {
    "buyer_accepts_marketing": true,
    "email": "tech@carthook.com"
  }, // The customer fields are available but might be empty("") if coupon is applied before the user inputs the shipping address
  "shipping_address": {
    "first_name": "John",
    "last_name": "Doe",
    "company": "CartHook",
    "address1": "834 Fieldcrest Road",
    "address2": "",
    "city": "New York",
    "province": "New York",
    "zip": "10001",
    "country": "United States",
    "phone": ""
  }, // The shipping address fields are available but might be empty("") if coupon is applied before the user inputs the shipping address
  "selected_shipping_rate": {
    "name": "Flat Shipping Rate",
    "price": "0.00",
    "source": "carthook_flat",
    "carrier_identifier": null,
    "requested_fulfillment_service_id": null,
    "code": "CARTHOOK_FLAT"
  } // This can also be null if coupon is applied BEFORE the addres is inserted
}
```


### OTO (One Time Offer) page events:
- `INITIATED_PAGE`

<br> <br>

#### Page initiated event
Event: `INITIATED_PAGE`
```
{
  "product": {
    "body_html": "<p>Wow. What to say?w</p>",
    "id": "9993963462",
    "selected_quantity": 1,
    "selected_variant_id": "39607598598",
    "title": "Big Honk'n Rock",
    "vendor": "Rok's Rocks",
    "price": "10.00",
    "currency": "USD"
  },
  "order": {
    "customer": {
      "email": "tech@carthook.com",
      "first_name": "John",
      "last_name": "Doe"
    },
    "encoded_order_id": "ymRDGvoySmFgd5Nf5OAM",
    "subtotal_price": "8.00",
    "total_price": "7.84",
    "order_number": null,
    "order_id": null,
    "payment_gateway": "stripe",
    "shipping_address": {
      "first_name": "John",
      "last_name": "Doe",
      "company": "CartHook",
      "address1": "834 Fieldcrest Road",
      "address2": "",
      "city": "New York",
      "province": "New York",
      "zip": "10001",
      "country": "",
      "phone": ""
    }
  },
  "line_items":[ // This is exactly the same as "product"
    {
        "body_html": "<p>Wow. What to say?w</p>",
        "id": "9993963462",
        "selected_quantity": 1,
        "selected_variant_id": "39607598598",
        "title": "Big Honk'n Rock",
        "vendor": "Rok's Rocks",
        "price": "10.00",
        "currency": "USD"
      }
  ],
  "position": 1 // The position of the upsell downsell based on the order of upsells downsells. I.e. first upsell would be position 1, first downsell would be position 2
}
{
  "product": {
    "body_html": "<p>Wow. What to say?w</p>",
    "id": "9993963462",
    "selected_quantity": 1,
    "selected_variant_id": "39607598598",
    "title": "Big Honk'n Rock",
    "vendor": "Rok's Rocks",
    "price": "10.00",
    "currency": "USD"
  },
  "order": {
    "customer": {
      "email": "tech@carthook.com",
      "first_name": "John",
      "last_name": "Doe"
    },
    "encoded_order_id": "ymRDGvoySmFgd5Nf5OAM",
    "subtotal_price": "8.00",
    "total_price": "7.84",
    "order_number": null,
    "order_id": null,
    "payment_gateway": "stripe",
    "shipping_address": {
      "first_name": "John",
      "last_name": "Doe",
      "company": "CartHook",
      "address1": "834 Fieldcrest Road",
      "address2": "",
      "city": "New York",
      "province": "New York",
      "zip": "10001",
      "country": "",
      "phone": ""
    }
  },
  "line_items":[ // This is exactly the same as "product"
    {
        "body_html": "<p>Wow. What to say?w</p>",
        "id": "9993963462",
        "selected_quantity": 1,
        "selected_variant_id": "39607598598",
        "title": "Big Honk'n Rock",
        "vendor": "Rok's Rocks",
        "price": "10.00",
        "currency": "USD"
      }
  ],
  "position": 1 // The position of the upsell downsell based on the order of upsells downsells. I.e. first upsell would be position 1, first downsell would be position 2
}
```

<br> <br>

#### Page initiated event
Event: `INITIATED_PAGE`
```
{
  "cart_data": {
    "coupon": {
      "coupon_type": "percent_off",
      "total_minus": "0.80",
      "coupon_code": "ilovestuff"
    },
    "currency": "USD",
    "subtotal_price": 16,
    "total_price": 16,
    "total_coupons_amount": "0.80",
    "token": null,
    "line_items": [
      {
        "id": "10",
        "variant_id": "39607598598",
        "discounted_price": "7.2",
        "price": "8.00",
        "quantity": "1",
        "sku": "",
        "tax_amount": "0.64",
        "tax_rate": "0.08875",
        "taxable": true,
        "title": "Big Honk'n Rock",
        "body_html": "<p>Wow. What to say?w</p>",
        "handle": "big-honkn-rock",
        "image": "https://cdn.shopify.com/s/files/1/1853/8535/products/weird_rock.jpg?v=1489713431",
        "variant_title": "l"
      },
      {
        "id": "10",
        "variant_id": "39607598598",
        "discounted_price": null,
        "price": "8.00",
        "quantity": "1",
        "sku": "",
        "tax_amount": "0.71",
        "tax_rate": "0.08875",
        "taxable": true,
        "title": "Big Honk'n Rock",
        "body_html": "<p>Wow. What to say?w</p>",
        "handle": "big-honkn-rock",
        "image": "https://cdn.shopify.com/s/files/1/1853/8535/products/weird_rock.jpg?v=1489713431",
        "variant_title": "l"
      }
    ]
  },
  "order": {
    "customer": {
      "email": "tech@carthook.com",
      "first_name": "John",
      "last_name": "Doe"
    },
    "encoded_order_id": "ymRDGvoySmFgd5Nf5OAM",
    "subtotal_price": "16.00",
    "total_price": "16.55",
    "order_number": "1147",
    "order_id": "5520500550",
    "payment_gateway": "stripe",
    "shipping_address": {
      "first_name": "John",
      "last_name": "Doe",
      "company": "CartHook",
      "address1": "834 Fieldcrest Road",
      "address2": "",
      "city": "New York",
      "province": "New York",
      "zip": "10001",
      "country": "",
      "phone": ""
    }
  }
```
<br><br>

### Example implementation
```
CH.event(function(EVENT, data) {
    if (EVENT == 'INITATED_PAGE') {
        console.log("Page was just initiated!");
    }
}, function(EVENT, error) {
    console.log('Uh oh! There was an error: ', error);
});
```
