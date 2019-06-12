# API Calls

## Summary 
This is the API Calls section of our documentation.

#### Merchant 
| Name | Description|
| ------------- |-------------|
| **id**      | `"id"`: `"cmid_KixEkfTj"`<br><br>The associated merchant for the merchant that installed the app |
| **email**      | `"email"`: `"apps@carthook.com"`<br><br>The associated merchant for the merchant that installed the app      |
| **store_url** | `"store_url"`: `"roks-rocks.myshopify.com"`<br><br>The associated merchant for the merchant that installed the app|
| **currency** | `"currency"`: `"USD"`<br><br>The associated merchant for the merchant that installed the app |

<br> 

#### 1. GET /merchant 
**GET** `/merchant` - Get basic merchant data associated to the installed account

###### Response
**HTTP/1.1 200 OK**
``` 
{
  "data": {
    "id": "cmid_KixEkfTj",
    "email": "apps@carthook.com",
    "store_url": "roks-rocks.myshopify.com",
    "currency": "USD"
  }
}
```

<br><br>

#### Assets 
| Name | Description|
| ------------- |-------------|
| **id**<br><br><sub><sup>READ-ONLY</sup></sub>    | `"id"`: `"cas_P12jn3Qzexr"`<br><br>base64 encoded prefixed id. Prefix is based on the : as_ |
| **created_at** <br><br><sub><sup>READ-ONLY</sup></sub>| `"created_at"`: `1558356696`<br><br>The date and time ([Unix Timestamp](https://www.unixtimestamp.com/)) when the asset was created.|
| **updated_at** <br><br><sub><sup>READ-ONLY</sup></sub>| `"updated_at"`: `1558356696`<br><br>The date and time ([Unix Timestamp](https://www.unixtimestamp.com/)) when the asset was updated.|
| **display** <br><br><sub><sup>REQUIRED</sup></sub> | `"display"`: `"checkout"`<br><br>The page this asset is displayed on. <br><br> Valid values are: <br><br> • `landing` <br><br> • `checkout` <br><br> • `oto` <br><br> • `upsell` <br><br> • `downsell` <br><br> • `thank_you` <br><br> • `all`  |
| **priority** <br><br><sub><sup>OPTIONAL</sup></sub> | `"priority"`: `0 → [0…n]`<br><br>Default value: **depends on the priority of assets added before.** <br><br>The range is from [0…n]. Lower number means higher priority. E.g. priority 0 means that it gets loaded before priority 1 etc. |
| **placement** <br><br><sub><sup>OPTIONAL</sup></sub> | `"placement"`: `"header"`<br><br>Default value: `header`. <br><br> Valid values are: <br><br> • `header` <br><br> • `footer` |
| **type** <br><br><sub><sup>REQUIRED</sup></sub> | `"type"`: `"javascript"`<br><br>Default value: `javascript`. <br><br> Valid values are: <br><br> • `javascript` <br><br> • `css` |
| **url** <br><br><sub><sup>REQUIRED</sup></sub>| `"url"`: `"https://code.jquery.com/jquery-3.4.0.min.js"`<br><br>The URL of the remote script. <br><br> <sub>Please note that we cache the assets internally so they are available immediately on page load.</sub> |
<br>  

**WARNING** → The max file size of an asset can not exceed 1mb in size. Any assets greater than 1mb will be ignored. 

<br> 

#### Available resources
1. **GET** `/assets` - Get all global code assets
2. **POST** `/assets` - Create global code asset
3. **GET** `/assets/{asset_id}` - Get single global code asset by ID
4. **PUT** `/assets/{asset_id}` - Update  single global code asset by ID
5. **DELETE** `/assets/{asset_id}` - DELETE single global code asset by ID

<br> 

#### 1. GET /assets 
**GET** `/assets` - Get all global code assets

###### Response
**HTTP/1.1 200 OK**
``` 
{
   "data":[
      {
         "id":"cas_P12jn3Qzexr",
         "created_at": 1558356696,
         "updated_at": 1558356696,
         "display":"oto",
         "priority":0,
         "placement":"header",
         "type":"css",
         "url":"https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css"
      },
      {
         "id":"cas_P12jn3Qzeax",
         "created_at": 1558356696,
         "updated_at": 1558356696,
         "display":"checkout",
         "priority":0,
         "placement":"header",
         "type":"javascript",
         "url":"https://code.jquery.com/jquery-3.4.0.min.js"
      }
   ],
   "meta":{
      "pagination":{
         "count":3,
         "limit":25,
         "offset":0,
         "has_more":false
      }
   }
}
``` 

<br>

**GET** `/assets?type=css` - Get all assets filtered by type 

###### Response
**HTTP/1.1 200 OK** 
```
{
   "data":[
      {
         "id":"cas_P12jn3Qzexr",
         "created_at": 1558356696,
         "updated_at": 1558356696,
         "display":"oto",
         "priority":0,
         "placement":"header",
         "type":"css",
         "url":"https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css"
      }
   ],
   "meta":{
      "pagination":{
         "count":3,
         "limit":25,
         "offset":0,
         "has_more":false
      }
   }
}
```

<br>

**GET** `/assets/{asset_id}` - Get a single asset by ID
###### Response
**HTTP/1.1 200 OK**
```
{
  "data":
    [
      {
         "id": "cas_P12jn3Qzexr",
         "created_at": 1558356696,
         "updated_at": 1558356696,
         "display": "checkout",
         "placement": "header",
         "priority": 0,
         "type": "javascript",
         "url": "https://code.jquery.com/jquery-3.4.0.min.js"
      }
    ]
}
```
#### 2. POST /assets 
**POST** `/assets` - Create a single code asset

###### Payload
``` 
{
    "display": "checkout",
    "placement": "header",
    "priority": 0,
    "type": "javascript",
    "url": "https://code.jquery.com/jquery-3.4.0.min.js"
}
``` 

<br>

#### 3. PUT /assets/{asset_id}
**PUT** `/assets/{asset_id}` -  Update a single property of a specific asset by asset id

###### Payload
``` 
{
    "display": "checkout"
}
``` 

<br>

#### 4. DELETE /assets/{asset_id}
**DELETE** `/assets/{asset_id}` -  DELETE a single property of a specific asset by asset id

###### Payload
``` 
{}
``` 

<br>


#### Error examples

##### Creating an asset without the required field produces errors:
``` 
{
  "errors": {
    "url": [
      "can't be blank",
      "Source must be secure (HTTPS)"
    ]
  }
}
``` 


<br><br><br>


#### Webhooks 
| Name | Description|
| ------------- |-------------|
| **id**<br><br><sub><sup>READ-ONLY</sup></sub>    | `"id"`: `"cwe_P12jn3Qzexr"`<br><br>base64 encoded prefixed id. Prefix is based on the : cwe_ |
| **created_at** <br><br><sub><sup>READ-ONLY</sup></sub>| `"created_at"`: `"1558356696"`<br><br>The date and time ([Unix Timestamp](https://www.unixtimestamp.com/)) when the webhook was created.|
| **updated_at** <br><br><sub><sup>READ-ONLY</sup></sub>| `"updated_at"`: `"1558356696"`<br><br>The date and time ([Unix Timestamp](https://www.unixtimestamp.com/)) when the webhook was updated.|
| **url** <br><br><sub><sup>REQUIRED</sup></sub>| `"url"`: `"https://carthook.com/webhook_catch"`<br><br>URL to where the Webhook should send the POST request when the event occurs. |
| **format** <br><br><sub><sup>OPTIONAL</sup></sub> | `"format"`: `"json"`<br><br> Default value: `json` <br><br> Valid values are: <br><br> • `json`  |
| **topic** <br><br><sub><sup>REQUIRED</sup></sub> | `"topic"`: `"checkout/created"` <br><br> Event that triggers the Webhook. <br><br> Valid values are: <br><br> • `checkout/created`,`checkout/updated`,`checkout/delete` <br><br> • `app/uninstalled` |

<br>

##### Events and topics
| Event | Topic|
| ------------- |-------------|
| **Checkout**    | `checkout/created`,`checkout/updated`,`checkout/delete` |
| **App**    | `app/uninstalled` |

<br> 

#### Available resources
1. **GET** `/webhooks` - Get all webhooks
2. **POST** `/webhooks` - Create a webhook
3. **GET** `/webhooks/{webhook_id}` - Get a single webhook by ID
4. **PUT** `/webhooks/{webhook_id}` - Update a single webhook by ID
5. **DELETE** `/webhooks/{webhook_id}` - DELETE a single webhook by ID

<br> 

#### 1. GET /webhooks 
**GET** `/webhooks` - Get all webhooks

###### Response
**HTTP/1.1 200 OK**
``` 
{
   "data":[
      {
         "id":"cwe_P12jn3Qzexr",
         "created_at":1558356696,
         "updated_at":1558356696,
         "url":"https://carthook.com/checkout_create",
         "format":"json",
         "topic":"checkout/created"
      },
      {
         "id":"cwe_P12jn3Qzexr",
         "created_at":1558356696,
         "updated_at":1558356696,
         "url":"https://carthook.com/checkout_update",
         "format":"json",
         "topic":"checkout/updated"
      }
   ],
   "meta":{
      "pagination":{
         "count":2,
         "limit":10,
         "offset":0,
         "has_more":false
      }
   }
}
``` 

<br>

**GET** `/webhooks/{webhook_id}` - Get a single webhook by ID
###### Response
**HTTP/1.1 200 OK**
```
{
  "data": {
    "id": "cwe_P12jn3Qzexr",
    "created_at": 1558356696,
    "updated_at": 1558356696,
    "address": "https://carthook.com/checkout_created",
    "format": "json",
    "topic": "checkout/created"
  }
}
```
#### 2. POST /webhooks 
**POST** `/webhooks` - Creates a single webhook

###### Payload
``` 
{
  "topic": "checkout/created",
  "url": "https://carthook.com/checkout_created",
  "format": "json"
}
``` 

**Errors**
- Throw 422 error if missing address field or address field is empty.
- Throw 422 error if address field does not contain a valid web address.
- Throw 422 error if missing events field or address field is empty.

<br>

#### 3. PUT /webhooks/{webhook_id}
**PUT** `/webhooks/{webhook_id}` -  Update a single property of a specific webhook by webhook id

###### Payload
``` 
{
  "topic": "checkout/created",
  "url": "https://carthook.com/checkout_created",
  "format": "json"
}
``` 

**Errors**
- Throw 403 error if not owner of this webhook.
- Throw 404 error if webhook id does not exist
- Throw 422 error if missing address field.
- Throw 422 error if address field does not contain a valid web address.
- Throw 422 error if missing events field.

<br>

#### 4. DELETE /webhooks/{webhook_id}
**DELETE** `/webhooks/{webhook_id}` -  Deletes a single webhook by ID

###### Payload
``` 
{}
``` 


