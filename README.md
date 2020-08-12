## Overview

This document describes the official Cutwise Platform REST API. If you have any problems or requests, please feel free to contact [Cutwise Support](mailto:support@cutwise.com).

Common APIs:
- [Cutwise API Authentification](rest/auth.md)
- [Constants API](rest/constants-api.md)

Diamonds API V3 uses dictionaries for managing diamond values:
- [Diamonds API V3](rest/diamonds-api-v3.md)

Diamonds API V4 uses string values for diamond data:
- [Diamonds API V4](rest/diamonds-api-v4.md)
- [Certifications API V4](rest/certifications-api-v4.md)

Mode info:
- [API Error Handling](rest/error-handling.md)
- [Cutwise Optical Performance Scores](rest/scoring-scale.md)
- [Examples](examples.md)

## HTTP redirects

API v3 and v4 use HTTP redirection where appropriate. Clients should assume that any request may result in a redirection. Receiving an HTTP redirection is not an error and clients should follow that redirect. Redirect responses will have a Location header field which contains the URI of the resource to which the client should repeat the requests.

|Status Code|Description|
|-|-|
|301|Permanent redirection. Indicates that the resource requested has been definitively moved to the URL given by the `Location` headers.|
|302|Temporary redirection. Indicates that the resource requested has been temporarily moved to the URL given by the `Location` header.|

Other redirection status codes may be used in accordance with the HTTP 1.1 spec.

## HTTP verbs

Where possible, API v3 strives to use appropriate HTTP verbs for each action.

|Verb|Description|
|-|-|
|GET|Used for retrieving resources (single or collection).|
|POST|Used for creating resources.|
|PATCH|Used for updating resources with partial JSON data. For instance, an `Diamond` resource has `color` and `clarity` attributes. A PATCH request may accept one or more of the attributes to update the resource.|
|PUT|Synonym for `PATCH`, so some fields can be ommited and they wouldn't be updated.|
|DELETE|Used for deleting resources.|

## Timezones

Please explicitly provide an ISO 8601 timestamp with timezone information
For API calls that allow for a timestamp to be specified, we use that exact timestamp. An example of this is the Commits API.

These timestamps look something like 2014-02-27T15:05:06+01:00.

## External Links

- [Cutwise.com](https://cutwise.com)
- [Pricing](https://cutwise.com/pricing/)
- [About](https://octonus-teams.com/wiki/display/CUDO/About+Cutwise+Team)
- [Service Privacy agreement](https://cutwise.com/privacy)
