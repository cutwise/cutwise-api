# Certification API v4

## Overview

TODO

## Certification Object Description

Here is the example Certification object fetched from Cutwise Certification API:

```json
{
  "id": 330,
  "laboratory": "GIA",
  "number": "33188",
  "url": "http://www.gia.edu/cs/Satellite?pagename=GST%2FDispatcher&childpagename=GIA%2FPage%2FReportCheck&c=Page&cid=1355954554547&reportno=33188",
  "file": "https://cutwise-test.s3.amazonaws.com/StoneCertificates/337/uploded_file.pdf"
}
```

Fields description:

|Field|FormatDescription|
|-|-|-|-|  
|id|int|Cutwise CertificationID|
|laboratory|string|Certification Laboratory|
|number|string|Certification Number|
|url|string|Certification URL on the laboratory website|
|file|string|Certification URL of uploaded file|

## Authorization

All HTTP requests to Certification API should be authorized by OAuth HTTP Bearer Tokens (see [Cutwise Authorization](auth.md)).
Request example:

```http
GET /v4/certification/{CERTIFICATION_ID} HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

## Single Certification Creation

On certification creation Certification object should be sent, except following fields:

- `url`: will be created automatically by Cutwise Platform;

Object should be sent as "multipart/form-data" request.

```http
POST /v4/certification HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
Content-Type: multipart/form-data
```

Payload:

```json
{
  TODO
}
```

Certification will be owned by user who requested provided Access Token

On success certification object will be returned.

## Deletion

```http
DELETE /v4/certification/{CERTIFICATION_ID} HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```
