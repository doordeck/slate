# Encoding

## Versioning

All Doordeck endpoints use JSON as their primary encoding scheme and respond to clients sending an 
```Accept: application/json header```, when a newer endpoints are available, clients should specify 
```Accept: application/vnd.doordeck.api-v2+json``` (replacing v2 with v3, etc).

## Certificate & Asymmetric Keys

Where certificates or keys are specified, these are in a BASE64 encoded 
[DER](https://en.wikipedia.org/wiki/X.690#DER_encoding) format - DER is a binary encoding using ASN.1 and is commonly 
understood by most cryptographic libraries. 

BASE64 encoded DER strings are very similar to PEM encoded values and can be converted by adding the appropriate 
[PEM](https://en.wikipedia.org/wiki/Privacy-Enhanced_Mail) header and footer and by adding a newline character every 64 
characters, e.g. 

```
-----BEGIN PUBLIC KEY-----
BASE64 DER PUBLIC KEY
-----END PUBLIC KEY-----
```
