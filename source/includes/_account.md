# Authentication

> To authorize, use this code:

```shell
curl 'https://api.doordeck.com/auth/token/'
  -X POST
  -H 'content-type: application/json'
  --data-binary '{"email":"EMAIL","password":"PASSWORD"}'
```

> Make sure to replace `USERNAME` and `PASSWORD` with your credentials.

> The above command returns JSON structured like this:

```json
{
  "privateKey":"base 64 encoded private key",
  "publicKey":"base 64 encoded public key",
  "authToken":"JSON Web Token for authentication",
  "refreshToken":"JSON Web Token for refreshing authentication credentials"
}
```

Doordeck uses tokens to permit access to the API. Doordeck expects for the token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your authentication token (the <code>authToken</code> from the login response).
</aside>

Authentication tokens are JSON web tokens, they can be examined to determine their expiry date, the user's ID. JSON web tokens are split into three sections separated by a `.`, the header, payload and signature - each section can be base64 decoded to read further.

```shell
echo 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE0NzMxNjMwNzUsImlhdCI6MTQ3MzA3NjY3NSwic3ViIjoiNWE1ZjZlODAtM2M1MS0xMWU2LTllNTctY2Y0MGJlMzAxM2ZiIiwic2Vzc2lvbiI6ImZiMmEwMDYwLTczNWYtMTFlNi1iNDg3LTZmMTZmZGE1MzkxNyIsInJlZnJlc2giOmZhbHNlLCJlbWFpbCI6Im1pY2hhZWxAZG9vcmRlY2suY29tIn0.REDCATED' | cut -d. -f2 | base64 -D
```

> The above command returns JSON structured like this:

```json
{
  "exp":1473163075,
  "iat":1473076675,
  "sub":"5a5f6e80-3c51-11e6-9e57-cf40be3013fb",
  "session":"fb2a0060-735f-11e6-b487-6f16fda53917",
  "refresh":false,
  "email":"michael@doordeck.com"
}
```

# Account

## Login

```shell
curl 'https://api.doordeck.com/auth/token/'
  -X POST
  -H 'content-type: application/json'
  --data-binary '{"email":"EMAIL","password":"PASSWORD"}'
```

> Make sure to replace `USERNAME` and `PASSWORD` with your credentials.

> The above command returns JSON structured like this:

```json
{
  "privateKey":"base 64 encoded private key",
  "publicKey":"base 64 encoded public key",
  "authToken":"JSON Web Token for authentication",
  "refreshToken":"JSON Web Token for refreshing authentication credentials"
}
```

This endpoint lets user's attempt to login.

### HTTP Request

`POST https://api.doordeck.com/auth/token`

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
email | true | User's email address
password | true | User's password

### Response

Parameter | Description
--------- | -----------
privateKey | PKCS8 encoded private key wrapped in base 64 encoding to be JSON friendly
publicKey | Base 64 encoded public key
authToken | JSON web token to be used for normal requests
refreshToken | JSON web token to be used for getting new authentication tokens

## Registration (v1)

```shell
curl "https://api.doordeck.com/auth/register"
  -X POST
  -H 'content-type: application/json'
  --data-binary '{"email":"EMAIL","password":"PASSWORD"}'
```

> The above command returns JSON structured like this:

```json
{
  "privateKey":"base 64 encoded private key",
  "publicKey":"base 64 encoded public key",
  "authToken":"JSON Web Token for authentication",
  "refreshToken":"JSON Web Token for refreshing authentication credentials"
}
```

This endpoint allows users to register for a Doordeck account.

### HTTP Request

`POST https://api.doordeck.com/auth/register`

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
email | true | Email address to register.
password | true | Password for access to account.
displayName | false | User's display name (e.g. their fullname)

<aside class="success">
A validation email will be disptahced to the user's email address upon successful registration.
</aside>

## Registration (v2)

```shell
curl "https://api.doordeck.com/auth/register"
  -X POST
  -H "Accept: application/vnd.doordeck.api-v2+json"
  -H 'content-type: application/json'
  --data-binary '{"email":"EMAIL","password":"PASSWORD"}'
```

> The above command returns JSON structured like this:

```json
{
  "privateKey":"base 64 encoded private key",
  "publicKey":"base 64 encoded public key",
  "authToken":"JSON Web Token for authentication",
  "refreshToken":"JSON Web Token for refreshing authentication credentials"
}
```

This endpoint allows users to register for a Doordeck account; it's handling of accounts with a pending invite is 
different from v1 in that the call will fail with a 409 conflict error if there is a pending invite (unless force is set
 to true).

### HTTP Request

`POST https://api.doordeck.com/auth/register`

This call must be made with the ```Accept``` header set to ```application/vnd.doordeck.api-v2+json```

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
email | true | Email address to register.
password | true | Password for access to account.
displayName | false | User's display name (e.g. their fullname)

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
force | false | Boolean flag to indicate if a pending invite should be discarded and a new account created

<aside class="success">
A validation email will be disptahced to the user's email address upon successful registration.
</aside>

## Refresh Token

```shell
curl -X POST "https://api.doordeck.com/auth/token/refresh"
  -H "Authorization: Bearer REFRESH_TOKEN"
```

> The above command returns JSON structured like this:

```json
  {
    "authToken":"JSON Web Token for authentication",
    "refreshToken":"(Optional) JSON Web Token for refreshing authentication credentials"
  }
```

This endpoint refreshes a users' authentication token using their refresh token. Refresh tokens cannot be used for standard requests and have a very long life compared with an authentication token.

### HTTP Request

`POST https://api.doordeck.com/auth/token/refresh`

<aside class="notice">
A refresh token should be used in place of an authentication token for this request.
</aside>

<aside class="notice">
The <code>refreshToken</code> field is optionally returned, if a new refresh token should be stored, otherwise it will not be present.
</aside>

## Logout

```shell
curl "https://api.doordeck.com/token/destroy"
  -H "Authorization: Bearer TOKEN"
```

This endpoint destroys a session associated with an authentication token and any associated refresh token.

### HTTP Request
`POST https://api.doordeck.com/token/destroy`

## Verify Email

```shell
curl "https://api.doordeck.com/account/email/verify?code=CODE"
  -X PUT
```

> Replace `CODE` with the verification code from the email.

This endpoint is used to verify a user's email address.

### HTTP Request
`PUT https://api.doordeck.com/account/email/verify`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
code | true | Verification code from email.

## Reverify Email

```shell
curl "https://api.doordeck.com/account/email/reverify"
  -X POST
  -H "Authorization: Bearer TOKEN"
```

This endpoint will generate a new email to the logged user with a new verification code to validate their email address.

### HTTP Request
`POST https://api.doordeck.com/account/email/reverify`

## Change Password

```shell
curl "https://api.doordeck.com/account/password"
  -H "Authorization: Bearer TOKEN"
  -X POST
  -H 'content-type: application/json'
  --data-binary '{"oldPassword":"OLD_PASSWORD","newPassword":"NEW_PASSWORD"}'
```

> Replace `OLD_PASSWORD` with the users' current password and `NEW_PASSWORD` with their desired password.

This endpoint is used to allow a user to change their password.

### HTTP Request
`POST https://api.doordeck.com/account/password`

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
oldPassword | true | User's old password.
newPassword | true | User's desired new password.

## Get User Details

```shell
curl "https://api.doordeck.com/account"
  -H "Authorization: Bearer TOKEN"
```

> The above command returns JSON structured like this:

```json
  {
    "publicKey": "User's public key",
    "email": "User's email address",
    "displayName": "User's display name",
    "emailVerified": true or false
  }
```

This endpoint returns information about the currently logged in user

### HTTP Request
`GET https://api.doordeck.com/account`

## Update User Details

```shell
curl "https://api.doordeck.com/account"
  -H "Authorization: Bearer TOKEN"
  -X POST
  -H 'content-type: application/json'
  --data-binary '{"displayName":"NEW_DISPLAY_NAME"}'
```

> Replace `NEW_DISPLAY_NAME` with the new display name to use

This endpoint updates a user's details, currently this is limited to display name.

### HTTP Request
`POST https://api.doordeck.com/account`

### Request Parameters

Parameter | Required | Description
--------- | ------- | -----------
displayName | true | User's desired display name
