## Cutwise Widget for RapNet

The Cutwise Widget lets you embed a Cutwise video on your website on RapNet stock.
Cutwise Widget for RapNet is an iFrame element with strict size: `480px` in width and `640px` in height.

Cutwise Widget for RapNet URL has the following format:
`https://widget.cutwise.com/rapnet/{CUTWISE_ID}` .

Iframe attributes `sandbox="allow-same-origin allow-scripts allow-presentation"` and `allowfullscreen` is required for proper work of Cutwise WIdget features in all browsers.

## Embedding example

```html
<iframe
    width="480"
    height="640"
    frameborder="0"
    sandbox="allow-same-origin allow-scripts allow-presentation"
    src="https://widget.cutwise.com/rapnet/337"
    allowfullscreen
></iframe>
```

## Requirements

IFrame size (width × height) should not be smaller than 480px × 640px. Full widget view should be visible without iframe scroll.

List of fully supported browsers:

- todo
- todo
- todo
- todo

The remaining browsers either have limited functionality or only the first frame of the video will be shown.
