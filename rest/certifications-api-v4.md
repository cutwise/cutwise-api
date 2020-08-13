# Certification API v4

## Overview

Certification API v4 major purpose is managing certifications of diamonds, published on Cutwise Platform.

## Certification Object Description

Here is the example Certification object fetched from Cutwise Certification API:

```json
{
  "id": 330,
  "laboratory": "GIA",
  "number": "33188",
  "url": "https://www.gia.edu/report-check?reportno=2136273512",
  "file": "https://d1d7qk4j7uzdqw.cloudfront.net/StoneCertificates/333/2136273512.pdf"
}
```

Fields description:

|Field|Format|Description|
|-|-|-|
|id|int|Cutwise CertificationID|
|laboratory|string|Certification Laboratory|
|number|string|Certification Number|
|url|string|Certification check URL on the laboratory website|
|file|string|Certification URL of uploaded file|

Supported laboratories:
- GIA
- AGS
- HRD
- IGI
- IIDGR
- GCAL

Only pdf files are supported. Maximum file size of the report should not exceed 10 MB.

## Authorization

All HTTP requests to Certification API should be authorized by OAuth HTTP Bearer Tokens (see [Cutwise Authorization](auth.md)).

## Single Certification Creation

Certification creation request parameters:

|Field|Format|Description|
|-|-|-|
|product|int (required)|Product to link with|
|laboratory|string (required)|Certification Laboratory|
|number|string|Certification Number|
|file|string|Certification File as binary content|

Object should be sent as "multipart/form-data" request.
Request example:

```http
POST /v4/certification HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
Content-Type: multipart/form-data; boundary=WebAppBoundary
--WebAppBoundary
Content-Disposition: form-data; name="file"; filename="file.pdf"
/path/to/file.pdf
--WebAppBoundary
Content-Disposition: form-data; name="product"
337
--WebAppBoundary
Content-Disposition: form-data; name="laboratory"
GIA
--WebAppBoundary
Content-Disposition: form-data; name="number"
33188
--WebAppBoundary--
```

Certification will be owned by user who requested provided Access Token

On success certification object will be returned.

## Deletion

```http
DELETE /v4/certification/{CERTIFICATION_ID} HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```
