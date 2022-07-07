# gridSpriter
A mixin to help using svg sprites.
# Installation
```bash
yarn add grid-spriter
```
# Usage
Setup your sprite in your scss
```scss
// Import the mixin from node_module (your path may vary)
@import './node_modules/grid-spriter/src/grid-spriter';

// Select the icons you want to import and define classes using a map
$classes: (1: 'isOk', 3: 'isWarn', 7: 'isError');

// Create the classes using the mixin. Icons as mask-image won't be available in older browsers but the color of the icon can be configured
.has-status-icon-mask {
  // generic.svg is a 7*4 grid
  @include GridSpriter('../images/icons/generic.svg', 7, 4, $classes);
}

// Create the classes using the mixin. Icons as background-image has better compatibility
.has-status-icon-background {
  // generic.svg is a 7*4 grid
  @include GridSpriter('../images/icons/generic.svg', 7, 4, $classes, 'background');
}

// Setup pseudo-elements
.has-status-icon-mask.aft::after {
  display: inline-block;
  width: 2rem;
  height: 2rem;
  background-color: #F00;
  content: '';
}
```
Then apply the right classes in the HTML
```html
<!-- Icon as a background image -->
<div class="has-status-icon" data-icon="isOK"></div>

<!-- Icon as a before pseudo-element -->
<div class="has-status-icon bfr" data-icon="isWarn"></div>

<!-- Icon as a before pseudo-element -->
<div class="has-status-icon aft" data-icon="isError"></div>
```
