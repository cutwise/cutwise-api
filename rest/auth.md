# Cutwise Authorization

## Overview

Cutwise Authorization made with OAuth2.0-compliant server. See [RFC 6749 "The OAuth 2.0 Authorization Framework"](https://tools.ietf.org/html/rfc6749).
For the security reasons Cutwise strictly recommends to follow one of the OAuth 2.0 process flows with enforced HTTPS (TLS 1.2) transport.

## Password Grant

See [Password Grant](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/) (oauth.com).

See [RFC 6749, section 1.3.3](https://tools.ietf.org/html/rfc6749#section-1.3.3) (oauth.com).

```http
GET https://cutwise.com/api/oauth/v2/token?grant_type=password&username={CUTWISE_LOGIN}&password={CUTWISE_PASSWORD}&client_id={CUTWISE_CLIENT_ID}&client_secret={CUTWISE_CLIENT_SECRET}
```

- `CUTWISE_LOGIN` - Cutwise user login, requests will be authentificated as provided user;
- `CUTWISE_PASSWORD` - Cutwise user password;
- `CUTWISE_CLIENT_ID` - Client Application ID;
- `CUTWISE_CLIENT_SECRET` - Client Application Secret.

Result returns in following JSON structure:

```json
{
  "access_token": "NDZmOTU2OGQyNDMzOTIyNDNjNDRhMWVlZWE0NmI1YzM3YTVmZmIxYzUyMmE0ODU3YjYyMmJlZWMzM2JjYjg5Zg",
  "expires_in": 604800,
  "token_type": "bearer",
  "scope": "user",
  "refresh_token": "MTJkNDAxNzcwYmQyYzQzNGFiMDczZmUxYjMyN2YzOGUzYTRkYzMyZGQ1ZWNlNmI1YTI4MjBjNTY4YjUzMmIyOA"
}
```

Access Token (`access_token`) can be used in Bearer Authorization, Refresh Token (`refresh_token`) can be used for prolongation of authorization.

## Refresh Token

Access Token can be refreshed by Refresh Token with following request:

```http
GET http://cutwise.local/api/oauth/v2/token?grant_type=refresh_token&refresh_token={REFRESH_TOKEN}&client_id={CUTWISE_CLIENT_ID}&client_secret={CUTWISE_CLIENT_SECRET}
```

- `REFRESH_TOKEN` - Refresh Token, retrieved in fetching Access Token request or from another refresh token request;
- `CUTWISE_CLIENT_ID` - Client Application ID;
- `CUTWISE_CLIENT_SECRET` - Client Application Secret.

Refresh Token can be used only once.

## Make API Request with Cutwise Access Token

To make API request authorized Authorization HTTP header with Cutwise Access Token (retrieved in previous steps) should be added.
See header format in [RFC 6750, section 2.1](https://tools.ietf.org/html/rfc6750#section-2.1).

Example:
```http
GET /v3/diamond/123 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer YzU5NDczNTMwMDY2YWY1ZjM5YmViNGJlMTU2ZmI2YjZmNjJjYjE0Y2Y5MmVhNmEyNzIxY2IxMzk1N2EzNWYyMw
```

## Handling Errors

In case when Cutwise API returns 401 (Unauthorized) HTTP response code, access token with sufficient rights should be provided with request. Client should fetch Access Token from Cutwise OAuth server and provide in as Bearer Authorization header.
If Cutwise API returns 403 (Access Denied) HTTP response code, then provided Cutwise Access Token has no rights to access or modify requested REST resource.