# Securing Your API Endpoints - A Practical Authentication Guide
NOTE TO READER:  presenter moved really quickly, but his slides are excellent.  These are in the same folder; read those instead

## Overview
1. Identity vs Authentication vs Authorization
1. Compare/Contrast security techniques

```
GET /foo/42
Authorization: alice
```
1. Identity: user data (Alice)
1. Authentication: Which user is this request for?
1. Authorization: is this requested permitted?


## Webserver - Simple Methods
1. Built in to webserver:
    - Client Certs
    - basic auth
    - digest auth

### Client Certs
- "Reverse TLS" - proves client identity to server
- no usernames or passwords
- ideal for internal apps, **not** public facing
- on IIS, only "simple" with Active Directory

### HTTP Basic Auth
```
GET /foo
Authorization basic asldkajsdalkdjasldjalsdkjaskljdaksdj
```
- String is `base64` encoded.  Passwords are being sent over the wire **in plain text**.
- TLS is effectively what you are relying on

- Drawbacks
    - Couples API calls to primary account password
    - Can leverage compromised information on other domains (i.e. reused passwords)

### HTTP digest auth
- Strenghts
    - easily integrates w/other standards-based systems
- Drawbacks
    - MD5 hash algo **has been cracked**
    - prevents the use of storing passwords with strong encryption
    - effectively unused at this point

## Webserver - Custom methods

1. API keys
    - use something *other than primary account credentials* as proof of identity
    - unique, random, **site-assigned**
        - this prevents escalation of attach
    - Great for server-based clients
    - less great for JS clients
        - there's no way to pre-load a key
        - things placed in `localStorage` are vulnearble via `XSS` attacks     
    - API keys as "bearer tokens"
        - pass the key in plain text with each request
        - anyone that has the key, gets access; **requires TLS**
        - can pass as querystring or header collection
            - generally more secure in header key, i.e.
            ```
            get /foo
            X-API-KEY: abc123
            ```
        - trade-offs when storing bearer tokens
            - you can have secure storage of API keys OR the ability to show users a list of their keys.  **NOT BOTH**.
    
    - API keys as cryptographic keys: HMAC
        - credentials not sent over the wire
        - server knows message wasn't changed in transit

        - drawbacks
            - complexity.  Client and server must compute hash EXACTLY THE SAME
            - i.e. AWS header canonicalization process
    
1. JWTs
    - Open, industry standard method for securely representing _claims_ between two parties

1. Oauth (1.0a)
    - **A Protocol**
    - uses signed requests
    - best with web-based clients
    - complex to implement
    - 2 legged: client <-> server
    - Delegated authorization (3-legged)
        - resource owner
        - resource provider
        - client

1. Oauth 2.0
    - **A Framework**
    - no HMAC signature == simpler to implement
    - better support for enterprise and web-based clients
    - less interoperable than Oauth 1.0a, as more details are up to the implementation.
    - Criticism: Eran Hammer, OAuth2 and the road to hell

1. OpenID Connect
    - Open Standard, built **on top of** OAuth2.0
        - ID Tokens - gives authentication data to client
        - unlike OAuth, provides audience restrictions

## Enterprisey stuff
1. SAML
    - Commonly used in enterprise SSO

## What should you use?
1. Client Certs
    - intranet logins against active directory
1. basic auth:
    - server to server

1. Digest Auth:
    - never
1. API keys as bearer tokens
    - rapidly standing up a new API
    - scenario where simplicity is more important than security
1. API keys as signature keys
    - you need exra security
