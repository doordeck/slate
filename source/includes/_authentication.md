# Authentication

Doordeck uses tokens to permit access to the API. Doordeck expects for the token to be included in all API requests to 
the server in a header that looks like the following:

`Authorization: Bearer TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with your authentication token.
</aside>

Authentication tokens are JSON Web Tokens (JWT) loosely using the OpenID format, they can be examined to determine their
expiry date, the user's ID. JSON web tokens are split into three sections separated by a `.`, the header, payload and
signature - each section can be BASE64URL decoded to read further.

Doordeck understands the following OpenID fields in the auth token payload:

Field | Mandatory | Datatype | Description
----- | --------- | -------- | -----------
sub | Yes | String <= 1024 bytes | Unique identifier for the user
iss | Yes | URI | URI of application responsible for issuing this token
exp | Yes | Epoch Timestamp | Timestamp in seconds at when this token will be considered invalid
iat | Yes | Epoch Timestamp | Timestamp in seconds when this token was issued and the data within loaded
auth_time | No | Epoch Timestamp | Timestamp in seconds when the user last authenticated
aud | Yes | URI or list of URIs | Must include https://api.doordeck.com
sid | No | String | Session identifier 
email | No | String | User's email address
email_verified | No (Defaults to false) | Boolean | Flag to specify if the user's email has been verified
telephone | No | [E.164](https://www.twilio.com/docs/glossary/what-e164) | User's phone number
telephone_verified | No (Defaults to false) | Boolean | Flag to specify if the user's phone number has been verified
locale | No | [BCP  47](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Locale.html) | User's locale (e.g. en-US)
zoneinfo | No | [Timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) | Timezone of user, e.g. Europe/London
name | No | String | User's full name
family_name | No | String | User's family name
middle_name | No | String | User's middle name
given_name | No | String | User's given name
picture | No | URI | User's profile picture

Authentication tokens can be issued directly by Doordeck using the [login](#login) endpoint or by third-party 
application developers using pre-registered asymmetric authentication keys.
