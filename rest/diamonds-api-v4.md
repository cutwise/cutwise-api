# Diamond API v4

## Overview

Diamonds API v4 major purpose is managing Vendor's owned diamonds, published on Cutwise Platform.

## Diamond Object Description

Here is the example Diamond object fetched from Cutwise Diamonds API:

```json
{
  "id": 337,
  "sku": "MSSRBC13",
  "price": null,
  "isColored": false,
  "isLabGrown": false,
  "cutShape": "Round",
  "carat": 0.73,
  "clarity": "VS2",
  "color": "G",
  "cutQuality": "Excellent",
  "polish": "Excellent",
  "symmetry": "Excellent",
  "fluorIntensity": "FNT",
  "fluorColor": "B",
  "fancyGrade":null,
  "colorHue":null,
  "colorModifier":null,
  "culetSize":"N",
  "girdle":"Thin-Medium",
  "date":"2014-11-27T21:11:00+00:00",
  "visibility":"full",
  "certifications": [
    {
      "id": 330,
      "laboratory": "GIA",
      "number": "33188",
      "url": "https://www.gia.edu/report-check?reportno=2136273512",
      "file": "https://d1d7qk4j7uzdqw.cloudfront.net/StoneCertificates/333/2136273512.pdf"
    }
  ],
  "scores": {
    "integral": {
      "val": 0.95,
      "rg": 1.02,
      "d": 0.05,
      "ver": "1.1.0"
    },
    "spread": {
      "ct": -0.19,
      "pc": -14.2,
      "d": 0.1,
      "ver": "1.0.0"
    },
    "fire": {
      "val": 0.73,
      "rg": 1.02,
      "d": 0.05,
      "ver": "fire-2018-01-26-6525426815546393815"
    },
    "brilliance": {
      "val": 1.03,
      "rg": 1.03,
      "d": 0.02,
      "faceup": 1.01,
      "avg": 0.98,
      "ver": "5.4.2018-06-29-3890169345"
    },
    "fluor": {
      "n": 1,
      "f": 0,
      "m": 0,
      "s": 0,
      "vs": 0,
      "ver": "5.4.2018-06-29-770653064"
    },
    "symmetry": {
      "val": 8.55,
      "pav": 8.71,
      "crown": 8.39,
      "d": 0.05,
      "ver": "1.3.0"
    }
  },
  "_links": [{
    "rel": "page.report",
    "href": "https:\/\/cutwise.com\/diamond\/337"
  }]
}
```

Fields description:

|Field|Format|Description|
|-|-|-|  
|id|int|Cutwise ProductID|
|sku|string|Diamond SKU, provided by Client|
|price|float\|int\|null|Diamond price, `null` if not set|
|isColored|bool|Is diamond graded as fancy coloured|
|isLabGrown|bool|Is diamond lab-grown|
|carat|float\|int|Diamond carat weight|
|cutShape|string|Diamond cut shape|
|clarity|string|Diamond clarity grade|
|color|string|Colorless diamond color grade|
|cutQuality|string|Diamond cut quality grade|
|polish|string|Diamond Polish grade|
|symmetry|string|Diamond symmetry grade|
|fluorIntensity|string|Diamond fluorescence intensity (strength) grade|
|fluorColor|string|Fluorescence Colour|
|colorHue|string|Fancy coloured colour hue (GIA) grade|
|colorModifier|string|Fancy coloured diamond colour modifier|
|culetSize|string|Diamond culet size grade|
|girdle|string|Diamond girdle grade|
|date|string (ISO 8601)|Date and time of object creation on Cutwise Platform|
|visibility|string("noaccess"|"widget"|"search"|"full")|Diamond visibility in Cutwise web interface. [Learn more](https://octonus-teams.com/wiki/display/CUDO/Cutwise+Stock+Management+Documentation)|
|certifications|Certification[]|Certifications array list. [Learn more](certifications-api-v4.md)|
|scores|object|Cutwise Optical Performance Scores. [Learn more](scoring-scale.md)|
|_links|object|HATEOAS Links to Cutwise Platform representations|

Accepted values for diamond fields are described on the [Accepted Values page](diamonds-api-v4-values.md).

## Authorization

All HTTP requests to Diamonds API should be authorized by OAuth HTTP Bearer Tokens (see [Cutwise Authorization](auth.md)).
Request example:

```http
GET /v4/diamond/1234 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

## Diamonds List Request

Diamonds list allways additionally filters by owning to user requested Cutwise Access Token.

List can be fetched with following HTTP request:

```http
GET /v4/diamond HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Response returns in JSON array format, containing list of Diamond object (see Diamond Object Description section):

```json
[
  {
    "id": 31893,
    "sku": "RBC_Melee-6",
    "price": null,
    "isColored": false,
    "isLabGrown": false,
    "carat": 0.03,
    ...
  },
  {
    "id": 31892,
    "sku": "RBC_Melee-9",
    "price": null,
    "isColored": false,
    "isLabGrown": false,
    "carat": 0.03,
    ...
  },
  {
    "id": 31891,
    "sku": "RBC_Melee-8",
    "price": null,
    "isColored": false,
    "isLabGrown": false,
    "carat": 0.03,

    ...
  }
]
```

Initial sorting is made by creation date.

If no diamonds matching filters then HTTP 204 response code will be return with no content.

### Filtration

List filtered can be done by fields `id`, `sku`, `isColored`, `date`.

Filtration example:

```http
GET /v4/diamond?f[id][]=1&f[id][]=2&f[sku][]=EJ50&f[sku][]=EJ51&f[dateFrom]=20050809T183142+0330&f[dateTo]=20150809T183142+0330 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

### Pagination

List pagination follows limit-offset pattern.

Default limit is 25. Default offset is 0.

```http
GET /v4/diamond?limit=50&offset=50 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Total count of matching filters objects is returned in HTTP Response Header `X-Total-Count`.

## Fetching Single Diamond

Single diamond can be fetched by Cutwise ProductID (field `id` from diamond object).
To fetch diamond with ProductId=1234 make the following request:

```http
GET /v4/diamond/1234 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

## Single Diamond Creation

On diamond creation Diamond object should be sent, except following fields:

- `id`: will be created automatically by Cutwise Platform;
- `date`: will be set automatically by Cutwise Platform;
- `certifications`: to add new certification to diamond you must use [Certifications API](certifications-api-v4.md);
- `scores`: will be ready after scoring processing (may take up to 1 hour);
- `_links`: virtual field;

Object should be sent in POST request payload encoded in JSON object.

```http
POST /v4/diamond HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Payload:

```json
{
  "sku": "RBC_Melee-6",
  "price": null,
  "isColored": false,
  "cutShape": 2,
  "carat": 0.03
}
```

Diamond will be owned by user who requested provided Access Token

On success diamond object will be returned.

Accepted values are described on the [Accepted Values page](diamonds-api-v4-values.md).

## Bulk Diamonds Creation

Requirements is the same as for single diamond, but object should in following structure:

```http
POST /v4/diamond/bulk HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Payload:

```json
{
  "entries": [{
    "sku": "RBC_Melee-6",
    "price": null,
    "isColored": false,
    "cutShape": 2,
    "carat": 0.03
  },
  {
    "sku": "RBC_Melee-7",
    "price": null,
    "isColored": false,
    "cutShape": 4,
    "carat": 0.025
  }]
}
```

On success list of diamond objects will be returned.

Up to 500 entries can be sent in single request.

## Single Diamond Modifying

The same as a Creation request, but PUT or PATCH HTTP method should be used.

Some fields can be ommited, it will not be changed in entity.

To remove value provide `null`.

```http
PATCH /v4/diamond/{PRODUCT_ID} HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Payload:

```json
{
  "carat": 0.031,
  "cutQuality": null
}
```

On success diamond object will be returned.

## Bulk Diamond Modifying

The same as a Bulk Creation request, but PUT or PATCH HTTP method should be used and each object should contain `id` fields.

```http
PATCH /v4/diamond/bulk HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Payload:

```json
{
  "entries": [{
    "id": {PRODUCT_ID_1},
    "carat": 0.032
  },
  {
    "id": {PRODUCT_ID_2},
    "carat": 0.55
  }]
}
```

On success list of diamond objects will be returned.

Up to 500 entries can be sent in single request.

## Single Diamond Deletion

```http
DELETE /v4/diamond/{PRODUCT_ID} HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

## Bulk Diamond Deletion

```http
DELETE /v4/diamond/bulk HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Payload:

```json
{
  "entries": [{
    "id": {PRODUCT_ID_1},
  },
  {
    "id": {PRODUCT_ID_2},
  }]
}
```
