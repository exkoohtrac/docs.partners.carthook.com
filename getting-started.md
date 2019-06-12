# Getting Started 

## API Base URL 
- https://api.carthook.com/  

## Versioning
https://api.carthook.com/{version_number}/

#### Active version:
- `v1` -> https://api.carthook.com/v1/


# API Authentication
CartHook uses [OAuth 2.0's authorization code](https://tools.ietf.org/html/rfc6749#section-4.1) grant flow to issue access tokens on behalf of users. 

TODO - document oauth flow steps

# API call Authentication
 
 The app can make requests by sending the OAuth token as a header parameter.  
 Authorization: `Bearer {access_token}` where `{access_token}` is replaced by the app developer with the permanent token.

