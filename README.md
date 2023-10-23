# GridSpriter
A mixin to help using svg sprites.
# Installation
```shell
yarn add grid-spriter
```
# Constructor
```scss
@include GridSpriter($src, $set, $col, $row, $def, $modes, $type)
```
| Parameter | Type   | Is required | Default                     | Description                                                                                                                                                                              |
|-----------|--------|-------------|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| $src      | string |      ✔      |                             | The path to your sprite image                                                                                                                                                            |
| $set      | string |      ✔      |                             | The name of your sprite set                                                                                                                                                              |
| $col      | number |      ✔      |                             | The number of columns in your sprite grid                                                                                                                                                |
| $row      | number |      ✔      |                             | The number of rows in your sprite grid                                                                                                                                                   |
| $def      | map    |             | null                        | A map with icon indexes as keys and icon names as values. Used to generate class name. Icon name will default to index value if map is null.                                             |
| $modes    | list   |             | ['is', 'prepend', 'append'] | The modes for which to generate class definitions. `is` will generate images as background, `prepend` as `::before` pseudo-elements and `append` as `::after` pseudo-elements.           |
| $type     | string |             | 'mask'                      | The type of images to use. `mask` or `background`. Mask images are easier to recolor but will most likely require an autoprefixer while background images provide perfect compatibility. |
# Output
```scss
// Generated classes will look like this
// .#{$mode}-#{$set}-#{$id}-icon[-mask][::before|::after] {}

// For example if you used the mixin like so
@include GridSpriter('/images/icons/twitch.svg', 'twitch', 3, 2, (1: 'follow'), ['is', 'append']);

// The resulting classes would look like this
.is-twitch-follow-icon-mask {}
.append-twitch-follow-icon-mask::after {}
```
# Usage
Any element or pseudo-element containing a sprite image must have a set `width` and `height`.
Any pseudo-element containing a sprite image must have a set `content`. An empty string will do.
Any element or pseudo-element containing a sprite image as a mask must have a set `background` or `background-color`.
```scss
@import 'grid-spriter';

$classes: (0: 'follow', 1: 'sub');

@include GridSpriter('/assets/sprite/twitch.svg', 'twitch', 3, 2, $classes, ['is', 'append']);

// Twitch follow icon as background image
// The class can be anything as long as its target element also has a GridSpriter generated class
.is-twitch-follow-icon { 
  width: 64px;
  height: 64px;
}

// Twitch sub icon as a before pseudo-element with mask image
.prepend-twitch-sub-icon-mask::before {
  content: '';
  display: inline-block;
  width: 64px;
  height: 64px;
  background-color: #6441A5;
}
```
```html
<!-- twitch follow icon as background image -->
<div class="is-twitch-follow-icon"></div>

<!-- twitch follow icon as mask image -->
<div class="is-twitch-follow-icon-mask"></div>

<!-- twitch follow icon as a before pseudo-element with background image -->
<div class="prepend-twitch-follow-icon"></div>
```
