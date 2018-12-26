
# Working with Constants

## Overview

The Constants API provides structured JSON-objects with Cutwise dictionaries and Cutwise scoring definitions.

## Requesting Constants

Cutwise Constants data can be fetched by simple unauthorized HTTP GET request:

```http
GET https://api.cutwise.com/v2/constants
```

It returns JSON object like this:

```json
{
  "ver": "4.1.0",
  "dict": {
    "cutShape": [
      {
        "id": 2,
        "title": "Round"
      },
      {
        "id": 4,
        "title": "Princess"
      },
      ...
    ],
    "color": [
      {
        "id": 15,
        "title": "D",
        "short": "D",
        "position": 10
      },
      {
        "id": 16,
        "title": "E",
        "short": "E",
        "position": 20
      },
      ...
    ],
    "clarity": [
      {
        "id": 1,
        "title": "FL",
        "short": "FL",
        "position": 10
      },
      {
        "id": 2,
        "title": "IF",
        "short": "IF",
        "position": 20
      },
      ...
    ],
    "cutQuality": [
      {
        "id": 1,
        "title": "Excellent",
        "short": "EX",
        "position": 10
      },
      {
        "id": 2,
        "title": "Very Good",
        "short": "VG",
        "position": 20
      },
      ...
    ],
    "polish": [
      {
        "id": 1,
        "title": "Excellent",
        "short": "EX",
        "position": 10
      },
      {
        "id": 2,
        "title": "Very Good",
        "short": "VG",
        "position": 20
      },
      ...
    ],
    "symmetry": [
      {
        "id": 1,
        "title": "Excellent",
        "short": "EX",
        "position": 10
      },
      {
        "id": 2,
        "title": "Very Good",
        "short": "VG",
        "position": 20
      },
      ...
    ],
    "fluorIntensity": [
      {
        "id": 1,
        "title": "None",
        "short": "NON",
        "position": 10
      },
      {
        "id": 2,
        "title": "Faint",
        "short": "FNT",
        "position": 20
      },
      ...
    ],
    "fluorColor": [
      {
        "id": 7,
        "title": "None",
        "short": "N",
        "position": 0
      },
      {
        "id": 1,
        "title": "Blue",
        "short": "B",
        "position": 10
      },
      ...
    ],
    "fancyGrade": [
      {
        "id": 8,
        "title": "Faint",
        "short": "Faint",
        "abbreviation": "FT",
        "position": 10
      },
      {
        "id": 9,
        "title": "Very Light",
        "short": "V.Light",
        "abbreviation": "VL",
        "position": 20
      },
      ...
    ],
    "colorHue": [
      {
        "id": 11,
        "title": "Yellow",
        "short": "Y",
        "position": 10,
        "children": [
          {
            "id": 30,
            "title": "Green-Yellow",
            "short": "GY",
            "position": 8
          },
          ...
        ]
      },
      {
        "id": 20,
        "title": "Red",
        "short": "R",
        "position": 40,
        "children": []
      },
      ...
    ],
    "colorModifier": [
      {
        "id": 1,
        "title": "Brownish",
        "short": "br",
        "position": 10
      },
      {
        "id": 3,
        "title": "Brown",
        "short": "Br",
        "position": 20
      },
      ...
    ]
  },
  "scoring": {
    "fluorescence": {
      "ver": "5.4.2018-06-29-770653064"
    },
    "fire": {
      "grades": [0.3, 0.5, 0.7, 0.85, 1, 1.3],
      "ver": "fire-2018-01-26-6525426815546393815"
    },
    "brightness": {
      "grades": [0.5, 0.7, 0.85, 0.95, 1.03, 1.3],
      "ver": "5.4.2018-06-29-3890169345"
    },
    "symmetry": {
      "grades": [2, 4, 6, 7, 8, 9],
      "ver": "1.3.0"
    },
    "integral": {
      "grades": [0.51, 0.69, 0.83, 0.93, 1.02, 1.27],
      "ver": "1.1.0"
    }
  }
}
```

## Fields description

Let's assume root Constants API result object called `res`.

- `res.ver` - current Cutwise Platform API version (followed by [Semantic Versioning 2.0](https://semver.org/));
- `res.dict` - list of Cutwise Dictionaries, see descriptions below;
- `res.dict.cutShape` - list of top-level Cut Shapes. To fetch relative shapes please use CutShape API (`GET https://api.cutwise.com/v2/cutshapes` for list, `GET https://api.cutwise.com/v2/cutshapes/87` for detailed info);
- `res.dict.color` - colour grades flat list for colorless diamonds;
- `res.dict.clarity` - clarity grades flat list;
- `res.dict.cutQuality` - cut quality grades flat list;
- `res.dict.polish` - polish grades flat list;
- `res.dict.symmetry` - symmetry grades flat list;
- `res.dict.fluorIntensity` - fluorescence intensity grades flat list;
- `res.dict.fluorColor` - fluorescence colours flat list;
- `res.dict.fancyGrade` - color grades for fancy-coloured diamonds;
- `res.dict.colorHue` - tree view of colour structure of fancy-coloured diamonds;
- `res.dict.colorModifier` - colour modifier flat list;
- `res.scoring` - Cutwise Optical Scores technical constants (see [Cutwise Scores Scale doc](scoring-scale.md) for details);

## Constants Caching

Constants data is recommended be cached on client side.
The most simple cache invalidation condition is on Cutwise Platfrom version change (even patch-segment by semver).
Current Cutwise Platform Version returns with each API request in response HTTP Header `X-App-Version`.

## Roadmap

- Support [If-Modified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since) header for cache invalidation.
