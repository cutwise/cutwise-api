# Plotting Package API v1

## Overview

API major purpose is retrieving multilight plotting data packages.

## Package Entry Description

Here is the example of the single object fetched from Cutwise Plotting Package API:

```json
{
	"id": 337,
	"sku": "MSSRBC13",
	"files": [{
			"lighting": "Darkfield ML",
			"wireframe": false,
			"url": "http://files-cdn.cutwise.com/img1.jpg"
		},
		{
			"lighting": "Darkfield ML",
			"wireframe": true,
			"url": "http://files-cdn.cutwise.com/img2.jpg"
		},
		{
			"lighting": "Chex1 Full ML",
			"wireframe": false,
			"url": "http://files-cdn.cutwise.com/img3.jpg"
		},
		{
			"lighting": "Chex1 Full ML",
			"wireframe": true,
			"url": "http://files-cdn.cutwise.com/img4.jpg"
		},
		{
			"lighting": "ASET White ML",
			"wireframe": false,
			"url": "http://files-cdn.cutwise.com/img5.jpg"
		},
		{
			"lighting": "ASET White ML",
			"wireframe": true,
			"url": "http://files-cdn.cutwise.com/img6.jpg"
		},
		{
			"lighting": "ML Composite",
			"wireframe": true,
			"url": "http://files-cdn.cutwise.com/img7.jpg"
		}
	],
	"date": "2014-11-27T21:11:00+00:00"
}
```

Fields description (`Constants` is a reference to Dictionaries from [Constants API](constants-api.md):

|Field|Format|Description|
|-|-|-|
|id|int|Cutwise ProductID|
|sku|string|Diamond SKU, provided by Client|
|files|array|Package files for external plotting|
|date|string (ISO 8601)|Date and time of object creation on Cutwise Platform|

## Authorization

All HTTP requests to Plotting Package API should be authorized by OAuth HTTP Bearer Tokens (see [Cutwise Authorization](auth.md)).
Request example:

```http
GET /plotting/v1/packages HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer YzU5NDczNTMwMDY2YWY1ZjM5YmViNGJlMTU2ZmI2YjZmNjJjYjE0Y2Y5MmVhNmEyNzIxY2IxMzk1N2EzNWYyMw
```

## Entries List Request

List can be fetched with following HTTP request:

```http
GET /plotting/v1/packages HTTP/1.1
Host: api.cutwise.com
Authorization: Bearer {CUTWISE_ACCESS_TOKEN}
```

Response returns in JSON array format, containing list of Diamond object (see Diamond Object Description section):

```json
[
  {
    "id": 31893,
    "sku": "RBC_Melee-6",
    "files": [ ... ],
    "date": "2014-11-27T21:11:00+00:00"
  },
  {
    "id": 31892,
    "sku": "RBC_Melee-9",
    "files": [ ... ],
    "date": "2014-11-27T21:13:00+00:00"
  },
  
  ...

]
```

Initial sorting is made by creation date.

If no diamonds matching filters then HTTP 204 response code will be return with no content.

### Filtration

List filtered can be done by fields `id`, `sku`, `date`.

Filtration example:

```http
GET /plotting/v1/packages?f[id][]=1&f[id][]=2&f[sku][]=EJ50&f[sku][]=EJ51&f[dateFrom]=20050809T183142+0330&f[dateTo]=20150809T183142+0330 HTTP/1.1
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
