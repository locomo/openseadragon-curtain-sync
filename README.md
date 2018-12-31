# Curtain & Snyc Modes for OpenSeadragon

This library is an extension for [OpenSeadragon](https://openseadragon.github.io/#) that enables side-by-side, syncronized image viewing. This extension will add the "curtain" and "sync" view modes to any OpenSeadragon viewer.

**Curtain mode** overlays images on top of each other and reveals more or less of each image based on your cursor position.

**Sync mode** shows images side-by-side but keeps each image in sync as the user zooms or pans.

## Demo
Demo coming soon!

*All images copyright of The Leiden Collection, New York*

## Install
1. [Download and install OpenSeadragon](https://openseadragon.github.io/#download).
2. Include `openseadragon-curtain-sync.min.js` on your page.

## Getting Started
This library includes only the javascript for extending OpenSeadragon. It does not include any of the UI elements for interacting with the CurtainSyncViewer. You may use any of the [default configuration options](https://openseadragon.github.io/docs/OpenSeadragon.html#.Options), but must include the new `images` option which is specific to this plugin.

**First**, initialize the viewer (note: this example uses IIIF for image tiling).

```js
var viewer = new CurtainSyncViewer({

  // default options
  container: document.querySelector('#viewer'),

  // images used by the viewer (2 or more).
  // "key" (string) - a unique string used to target this image.
  // "shown" (boolean) - whether the image is on/off when page is loaded.
  images: [
    {
      key: 'my-key-1',
      tileSource: 'https://url-to-iiif-manifest.json',
      shown: true
    },
    {
      key: 'my-key-2',
      tileSource: 'https://url-to-iiif-manifest.json',
    }
  ],

});
```

**Second**, implement the UI for interacting with the new view modes. Below is a simple example using jQuery. For a more detailed example, see the demo.

```js
// show an alternate image
$('#myButton').on('click', function(e){
  viewer.setImageShown('my-key-2', true);
});

// switch view mode ("curtain" or "sync")
$('#myButton').on('click', function(e){
  viewer.setMode('curtain');
});
```

## Methods
`getImageShown(key)`

Returns `true` or `false` for a given image key.

`setImageShown(key, shown)`

Shows or hides an image key based on the `shown` arguement.

`getMode(key)`

Returns the current viewer mode ("curtain" or "sync").

`setMode(key)`

Sets the mode for the viewer (`key` = "curtain" or "sync"). If no key is provided, it will default to "sync" mode.
