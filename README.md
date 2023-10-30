# GridSpriter
A mixin to help using svg sprites.

# Installation
```shell
yarn add grid-spriter
```

# Constructor
```scss
@include GridSpriter($name, $col, $row, $params);
```

| Parameter | Type   | Is required | Default | Description                               |
|-----------|--------|-------------|---------|-------------------------------------------|
| $name     | string |      ✔      |         | The name of your sprite set               |
| $col      | number |      ✔      |         | The number of columns in your sprite grid |
| $row      | number |      ✔      |         | The number of rows in your sprite grid    |
| $params   | map    |             | ()      | A map of optional parameters.             |

## Optional parameters
| Parameter | Type   | Default                     | Description                                              |
|--------|--------|-----------------------------|----------------------------------------------------------|
| path   | string | '/assets/images/sprites/'   | The base path to your sprite image                       |
| format | string | 'svg'                       | The extension of your sprite image                       |
| def    | map    | null                        | A map with icon indexes as keys and icon names as values |
| modes  | list   | ['is', 'prepend', 'append'] | The modes for which to generate class definitions        |
| type   | string | 'mask'                      | The type of images to use                                |

# Output
```scss
// Generated classes will look like this
// .#{$mode}-#{$name}-#{$id}-icon[-mask][::before|::after] {}

// For example if you used the mixin like so
$twitchParams: (
  def: (1: 'follow'), 
  modes: ['is', 'append']
);

@include GridSpriter('twitch', 3, 2, $twitchParams);

// The resulting classes would look like this
.is-twitch-follow-icon-mask {}
.append-twitch-follow-icon-mask::after {}
```

# Usage
Any element or pseudo-element containing a sprite image must have a set `width` and `height`.
Any pseudo-element containing a sprite image must have a set `content`. An empty string will do.
Any element or pseudo-element containing a sprite image as a mask must have a set `background` or `background-color`.

The default path for images is `/assets/images/sprites/`, the default format is `svg`.
In our example, the image must be located at `/assets/images/sprites/twitch.svg`. 

```scss
@import 'grid-spriter';

$twitchParams: (
  def: (0: 'follow', 1: 'sub'),
  modes: ['is', 'prepend']
);

@include GridSpriter('twitch', 3, 2, $twitchParams);

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
