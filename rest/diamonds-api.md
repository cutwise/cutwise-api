# Diamond API v3

## Overview

Diamonds API v3 major purpose is managing Vendor's owned diamonds, published on Cutwise Platform.

## Diamond Object Description

Here is the example Diamond object fetched from Cutwise Diamonds API:

```json
{
  "id": 337,
  "sku": "MSSRBC13",
  "price": null,
  "isColored": false,
  "isPublished": true,
  "cutShape": 2,
  "carat": 0.73,
  "clarity": 6,
  "color": 18,
  "cutQuality": 1,
  "polish": 1,
  "symmetry": 1,
  "fluorIntensity": 1,
  "fluorColor": null,
  "fancyGrade": null,
  "colorHue": null,
  "colorModifier": null,
  "date": "2014-11-27T21:11:00+00:00",
  "scores": {
    "integral": {
      "val": 0.95,
      "rg": 1.02,
      "d": 0.05,
      "ver": "1.1.0"
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
  "_links": [
    {
      "rel": "page.report",
      "href": "https:\/\/cutwise.com\/diamond\/337"
    }
  ]
}
```

Fields description (`Constants` is a reference to Dictionaries from [Constants API](constants-api.md):

|Field|Format|Constants|Description|
|-|-|-|-|
|id|int|—|Cutwise ProductID|
|sku|string|—|Diamond SKU, provided by Client|
|price|float\|int\|null|—|Diamond price, `null` if not set|
|isColored|bool|—|Is diamond graded as fancy coloured|
|isPublished|bool|—|Is diamond in Published status on Cutwise Platform|
|carat|float\|int|—|Diamond carat weight|
|cutShape|int|`dict.cutShape`|Diamond cut shape|
|clarity|int|`dict.clarity`|Diamond clarity grade|
|color|int|`dict.color`|Colorless diamond color grade|
|cutQuality|int|`dict.cutQuality`|Diamond cut quality grade|
|polish|int|`dict.polish`|Diamond Polish grade|
|symmetry|int|`dict.symmetry`|Diamond symmetry grade|
|fluorIntensity|int|`dict.fluorIntensity`|Diamond fluorescence intensity (strength) grade|
|fluorColor|int|`dict.fluorColor`|Fluorescence Colour|
|colorHue|int|`dict.colorHue`|Fancy coloured colour hue (GIA) grade|
|colorModifier|int|`dict.colorModifier`|Fancy coloured diamond colour modifier|
|date|string (ISO 8601)|—|Date and time of object creation on Cutwise Platform|
|scores|object|—|Cutwise Optical Performance Scores. [Learn more](scoring-scale.md)|
|_links|object|—|HATEOAS Links to Cutwise Platform representations|

## Authorization

All HTTP requests to Diamonds API should be authorized by OAuth HTTP Bearer Tokens (see [Cutwise Authorization](auth.md)).
Request example:

```http
GET /v3/diamond/1234 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer YzU5NDczNTMwMDY2YWY1ZjM5YmViNGJlMTU2ZmI2YjZmNjJjYjE0Y2Y5MmVhNmEyNzIxY2IxMzk1N2EzNWYyMw
```

## Diamonds List Request

Diamonds list allways additionally filters by owning to user requested Cutwise Access Token.

List can be fetched with following HTTP request:

```http
GET /v3/diamond HTTP/1.1
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
    "isPublished": true,
    "cutShape": 2,
    "carat": 0.03,
    ...
  },
  {
    "id": 31892,
    "sku": "RBC_Melee-9",
    "price": null,
    "isColored": false,
    "isPublished": true,
    "cutShape": 2,
    "carat": 0.03,
    ...
  },
  {
    "id": 31891,
    "sku": "RBC_Melee-8",
    "price": null,
    "isColored": false,
    "isPublished": true,
    "cutShape": 2,
    "carat": 0.03,

    ...
  }
]
```

Initial sorting is made by creation date.

If no diamonds matching filters then HTTP 204 response code will be return with no content.

### Filtering

List filtered can be done by fields `id`, `sku`, `isColored`, `isPublished`, `date`.

Filtering example:

```http
GET /v3/diamond?f[id][]=1&f[id][]=2&f[sku][]=EJ50&f[sku][]=EJ51&f[dateFrom]=20050809T183142+0330&f[dateTo]=20150809T183142+0330 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

### Pagination

List pagination follows limit-offset pattern.

Default limit is 25. Default offset is 0.

```http
GET /v3/diamond?limit=50&offset=50 HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Total count of matching filters objects is returned in HTTP Response Header `X-Total-Count`.

### Response Example

TODO

### Error Handling

TODO

## Fetching Single Diamond

TODO

## Modifying Single Diamond

TODO

## Modifying Diamonds List

TODO
 max collection update is 500

## Deleting Single Diamond

TODO

## Deleting Diamonds List

TODO
 max collection update is 500

## Example

TODO
