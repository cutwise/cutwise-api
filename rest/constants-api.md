
# Working with Constants

Constants API provides basic data to make subsequent requests.

```json
https://api.cutwise.com/v2/constants
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
      {
        "id": 9,
        "title": "Cushion"
      },
      {
        "id": 11,
        "title": "Oval"
      },
      {
        "id": 80,
        "title": "Marquise"
      },
      {
        "id": 22,
        "title": "Pear"
      },
      {
        "id": 83,
        "title": "Radiant"
      },
      {
        "id": 90,
        "title": "Emerald"
      },
      {
        "id": 92,
        "title": "Asscher"
      },
      {
        "id": 85,
        "title": "Heart"
      },
      {
        "id": 113,
        "title": "Other"
      }
    ],
    "color": [
      {
        "id": 15,
        "title": "D",
        "extTitle": "D",
        "position": 10
      },
      {
        "id": 16,
        "title": "E",
        "extTitle": "E",
        "position": 20
      },
      ...
    ],
    "fancyGrade": [
      {
        "id": 22,
        "title": "Black",
        "extTitle": "Bk",
        "position": 90,
        "children": []
      },
      {
        "id": 23,
        "title": "Gray",
        "extTitle": "Gr",
        "position": 100,
        "children": {
          "24": {
            "id": 24,
            "title": "White",
            "extTitle": "W",
            "position": 116
          },
          "56": {
            "id": 56,
            "title": "Yellow-Gray",
            "extTitle": "YGr",
            "position": 111
          },
          ...
        }
      },
      ...
    ],
    "clarity": [
      {
        "id": 1,
        "title": "FL",
        "extTitle": "FL",
        "position": 10
      },
      {
        "id": 2,
        "title": "IF",
        "extTitle": "IF",
        "position": 20
      },
      ...
    ],
    "cutQuality": [
      {
        "id": 10,
        "title": "Ideal",
        "extTitle": "ID",
        "position": 5
      },
      {
        "id": 1,
        "title": "Excellent",
        "extTitle": "EX",
        "position": 10
      },
      ...
    ],
    "polish": [
      {
        "id": 10,
        "title": "Ideal",
        "extTitle": "ID",
        "position": 5
      },
      {
        "id": 1,
        "title": "Excellent",
        "extTitle": "EX",
        "position": 10
      },
      ...
    ],
    "symmetry": [
      {
        "id": 10,
        "title": "Ideal",
        "extTitle": "ID",
        "position": 5
      },
      {
        "id": 1,
        "title": "Excellent",
        "extTitle": "EX",
        "position": 10
      },
      ...
    ],
    "laboratory": [
      {
        "id": 3,
        "title": "GIA"
      },
      {
        "id": 4,
        "title": "AGS"
      },
      ...
    ],
    "fluorescenceStrength": [
      {
        "id": 1,
        "title": "None",
        "extTitle": "NON",
        "position": 10
      },
      {
        "id": 2,
        "title": "Faint",
        "extTitle": "FNT",
        "position": 20
      },
      ...
    ],
    "fluorescenceColor": [
      {
        "id": 7,
        "title": "None",
        "extTitle": "N",
        "position": 0
      },
      {
        "id": 1,
        "title": "Blue",
        "extTitle": "B",
        "position": 10
      },
      ...
    ],
    "girdleThicknessGrade": [
      {
        "id": 1,
        "title": "Extremely Thin",
        "extTitle": "EXT THN",
        "position": 10
      },
      {
        "id": 2,
        "title": "Very Thin",
        "extTitle": "V THN",
        "position": 20
      },
      ...
    ],
    "culet": [
      {
        "id": 1,
        "title": "None",
        "extTitle": "N",
        "position": 10
      },
      {
        "id": 2,
        "title": "Very small",
        "extTitle": "V SML",
        "position": 20
      },
      ...
    ]
  },
  "metrics": {
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
