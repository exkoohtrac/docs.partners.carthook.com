# Getting Started 

## API Base URL 

#### Production
- https://api.carthook.com/  

#### Sandbox
- https://api.sandbox.carthook.com

## Versioning
https://api.carthook.com/{version_number}/

#### Active version:
- `v1` -> https://api.carthook.com/v1/


## API Authentication
CartHook uses [OAuth 2.0's authorization code](https://tools.ietf.org/html/rfc6749#section-4.1) grant flow to issue access tokens on behalf of users. 

1. The merchant makes a request to install the app from the Apps section within the CartHook admin or by redirecting a user to the admin Apps section from an external URL.
    1. **Note:** An external admin can redirect to our install page url
2. The app redirects to CartHook's App Authorization page to load the OAuth grant screen and requests the required scopes.
3. CartHook displays a prompt to receive Authorization and prompts the merchant to login if required.
4. The merchant consents to the scopes and is redirected to the "**oAuth callback URL**" specified in the app details page of a single app. That will be set as the `redirect_uri` query param in the redirect URL. 
5. The app makes an access token request to CartHook including the `client_id`, `client_secret`, and `code`.
6. CartHook returns the access token and requested scopes.
7. The app uses the **Permanent Acess Token** to make requests to the CartHook API.
8. CartHook returns the requested data.

<br>

| Name | Description|
| ------------- |-------------|
| **client_id** | You can find your `client_id` in the details section for a single app of your CartHook partners dashboard. Every app has a unique Client ID|
| **redirect_uri** | This is the redirect URI you specified while creating or updating the app. A Merchant will be redirected to your whitelisted URI after app authorization|
| **response_type** | This is the expected response type. Currently, only `code` is supported. |
| **scope** | The scopes you need granted privileges to. You can find all available scopes a bit lower in these docs. Please note that scopes must be separated with spaces(or %20 if you want to URL encode the scopes). |

###### Full URL Example
- https://admin.sandbox.carthook.com/settings/apps/install?client_id=<YOUR_CLIENT_ID>&redirect_uri=<YOUR_CALLBACK_URL>&response_type=code&scope=<DESIRED_SCOPES>  
    - Example: https://admin.sandbox.carthook.com/settings/apps/install?client_id=53ce1831deacc3766d37db12713a4bbf&redirect_uri=https://acme.com/callback&response_type=code&scope=read_assets write_assets

## API SCOPES
Authenticated access scopes control access to resources in the REST Admin API. Authenticated access is intended for interacting with a store on behalf of the merchant to perform actions such as creating/managing assets or webhooks.

- `read_merchant_data`
    - Access to the basic merchant data, such as connected store URL
- `read_webhooks`, `write_webhooks`
    - Access to the Webhooks endpoints
- `read_assets`, `write_assets`
    - Access to the Assets endpoints

## Requesting the permanent access token
Requesting access token
When the merchants get redirected to your redirect_uri a code parameter will be present in the URL. You can use that code to request the permanent access token.

**POST** `/oauth/token`
###### Payload
```
{
    "grant_type": "authorization_code",
    "client_id": "53ce1831deacc3766d37db12713a4bbf",
    "client_secret": "cmnIaqJ7i8NcROeh4EkuHO9izxjC4ICQ28Zo8vvR",
    "code": "def50200de4ca3e8d16873642c684a4fac8895010ee85e9263356a4c41769bc6a651d63d67d510e0c2df68aa65cb722c6298f4d2bb9014a0eb44bb4e64f810bbf3cdd7d2f3ba72cc989abca09c6780e38a7be4121a83855336dd04fd17f55b0b7ecb7ce0e9b1ea2a4616baed8e15c4c4e32df303654d3ef451b778dd7bf9879d597080e430203994b8ed0100cef14840dcd14af91c1902a0f3b61c243acbab1e1ac487d6f0c76ee0ad41d929f910f015bd121572776ebfac091242a3b1d91e91985ac98c5b91fb770210843c17e284d2c8fa1f7d46872c6177db78803e4f529fd63af8efd3a6b0f1e9b798f5f626a90ceaa04ed843f03d37cb549901e38b1c636b1fe863c1fbb286e6696a20dd92ba206a0cb16e5665f2496146f35eb080bb9866af504c38009a81f4b38e05ebab6ace4865ea91d4d2d47de1368195751fdc4c4612ed5f2cd5abc18ba80e3571a122ef844232867d2e44ba5d453da38d717c02410aabe4c6fd0d2904547342ef11e9623ae14bf46b73996c630ea90095b75d3dad1093aa1c3d1944568c573fbe84844945364ae09cad28bcc7a15e53587ec9063c2380de283ce92d",
    "redirect_uri": "https://partners.carthooklocal.com/callback"
}
```
###### Example Response
````
{
    "token_type": "Bearer",
    "expires_in": 631152000,
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjQ2YWQzMjYzNDlhMDlkMzU2NmEyNWFkZWIxNzA4MzczNGIyNjQyNmM5YzZkNWI0MWRjMWZiOTZhMWViNDk2MTYyMWUwODQ2ZWU5NWZlNzhiIn0.eyJhdWQiOiI4MjlmMDk1MDM2NTliOTVkMGI3ZTQ3MDg0ODVkMGYyNyIsImp0aSI6IjQ2YWQzMjYzNDlhMDlkMzU2NmEyNWFkZWIxNzA4MzczNGIyNjQyNmM5YzZkNWI0MWRjMWZiOTZhMWViNDk2MTYyMWUwODQ2ZWU5NWZlNzhiIiwiaWF0IjoxNTYwMzQwOTg2LCJuYmYiOjE1NjAzNDA5ODYsImV4cCI6MjE5MTQ5Mjk4Niwic3ViIjoibWlkX1VMbEdSdXNWIiwic2NvcGVzIjpbIndyaXRlX3dlYmhvb2tzIiwicmVhZF93ZWJob29rcyIsIndyaXRlX2Fzc2V0cyIsInJlYWRfYXNzZXRzIl19.EZS47EbmX9NvIq9f2AR-gC5bsdtLObHy6tHBoSRSmO-V8lxXwL97zfI_VU9S0Ui-OjNtAfu95T0rkHiTdPLrMT4-657tMpcLhjGzPwIUF80BXUF6lNaPlYi9ne5XJvUEW8jAdDfrVe2b1_osFCvzPARw0DypZofpSH0wds2TsYqDoVcuNcTFq3QHFweiojNJgWeF8rc73ye_ql-O7d1EHfGDjyWPhtj1XZKUEAtLEZzG17b-SO7ocLUagMnLLh1D_v9wcf9oE5lZ4luQohahJARBceUTWexYLxSLhyO08EnNdD5O5GSbBy05Kc4ZZJgVLRQaDSqCZmu75OLlvx_u23xrTy4bb4krL2WazbnE2CypYgJ_XUou7TgKQIvDkLiIKAH5Iv21xvc7-Yey9rZKDjZrLunfuoqGEaQaC-rhhEUSHLuXH0UnEVjEgSYPoviO81OYuoFxGPFnzLZ7eV6dJb85HtQQUSmXix0kqakjPmFubTLGZlRuATCHHxE9Af33auk4610ZXmDL5yk_Vx5aZu8Zkk3m2NgOLJu2-fcILmkK3-6jXq0gaFTTlttAhqs-u6XfCPdHlAq6bJzWaY8pY5AvNfAUftcIV6TxCNvQ-rahHgrz-YUWmxUb3dnbkstnC7OqCZTgcOlPFIQOI0S1fPzbROcrb0gVf2itresGjLE",
    "refresh_token": "def502003ee3d818bdb864ecdf46806a5618491215815621b0fb0ee96a33b01a9466d7fb191dbc134d411ab43b8f5ca732f13025ecaf22256a674df3da1456180025180936f6e6b82f75e88ae8937093dc36cd067e714a74489aba1f45fd3c02545cbf0fa9c1d7ef4d67f761ac0598684c2c0752dd555abe69c8eab42ae7743c3dc1cbb87b4783507dcd2d02a43bc00558b7c7b4171fd6e388f53067b2a2852a6e777660a9ae2e51f590f5b225943b0b0615e17b44c3cf4444da8f78c7964b59b464dc3bd1855e551b2839ac80245299d3bb9d23ecfb5e6b85cd3e335273ed8747e048ec9d1b73b5de5c00289911a3f3f5f6be3e255819934d9a422254ba5d93876c030ab5e2fc56c1f47396eb0b06abef6b1dfa8e9b19e1534fd769cf08dfef565d1bdf748592362c8ecd4dff333a92ab6fe7f61a0552c0029eedcacf4ea7003ffdadcefd29d067181bfde776fc078b68d8b86f02383f20d47b889cdf38e9e31f7825b1bc29fb66afac7aa2f24d3efa64efd2b7135faa76100895ef128a679b84c99b6d3231ef0e8f7601d43efafcab66307681e314194d8c826ddbade38a27b60ebb4b4eea8dd4cb1a702ad0b17bef06ceb6288ad1180ae6ec041d6ea55f418d7517cc3246e34a0e81"
}
````

<br>

## API call Authentication
 
 The app can make requests by sending the OAuth token as a header parameter.  
 Authorization: `Bearer {access_token}` where `{access_token}` is replaced by the app developer with the permanent token.

