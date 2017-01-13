# Oui_grid

A quite light (17ko) sass powered css responsive and "semantic" grid builder using [flexbox](//caniuse.com/#feat=flexbox) and [calc()](//caniuse.com/#search=calc).
Click these features for support informations via [caniuse.com](//caniuse.com/).

## Contents

* [Features](#features)
* [Usage](#usage)
* [Settings](#settings)
* [Usage](#usage)
* [Mixin](#mixin)
* [Example / demo](#example--demo)
* [Add-ons](#add-ons)
* [Credits](#credits)

## Features

* Unlimited columns width;
* unlimited custom breakpoints;
* responsive gutters;
* gutters as margin and/or padding;
* add-ons;
* etc.

## Usage

Import `oui_grid.scss` in your main `.scss` file.

```scss
@import "_oui_grid";
```

## Settings

You can customize the following values on the top of `_oui_grid.scss`.

```scss
$settings: (
    "s": (                           // Each $settings key is used as a custom breakpoint.
        "content-max-width" : 480px, // Max-width to optionally apply to containers.
        "vertical-spacing"  : 12px,  // Top and bottom gutters.
        "horizontal-spacing": 8px    // Right and left gutters.
    ),
    "m": (
        "device-min-width"  : 640px, // Media-query min-width (useless for the first breakpoint).
        "content-max-width" : 800px,
        "vertical-spacing"  : 16px,
        "horizontal-spacing": 12px
    ),
    …
);
```

While oui_grid is able to play with responsive gutters, no extra CSS will be generated if two breakpoints have the same spacing values.

## Mixin

### this

```scss
@include this($media, $flow, $width, $gutter, $position, $padding);
```

#### arguments

- `$media` (`null`): media-query min-width and/or max-width as `$layout` map keys.

  ```scss
  @include this("s") { … }; // or…
  @include this("s" "l") { … }; // or…
  @include this(false "l") { … };
  ```

- `flow` (`null`): CSS `flex-flow` value.

  ```scss
  @include this("s" "l", row wrap) { … }; // or…
  @include this($flow: row wrap) { … };
  ```

- `$width` (`null`): fraction of factor of the container width.
You can also use `max-width` to apply a width of 100% and a responsive `max-width` according to the `$max-content-width` value.
  ```scss
  @include this("s" "l", "row wrap", 1/2) { … }; // or…
  @include this("s" "l", "row wrap", .5) { … }; // or…
  @include this($width: 1/2) { … };
  ```

- `$gutter` (`null`): value or list of two or four values.
  - `true` or `false` will enable or disable the responsive gutter;
  - `nested` will be read as a factor of `-1` of the responsive gutter (see the next list item);
  - a unitless value will be read as a factor of the responsive gutter;
  - a usual margin value followed by its unit will be used as it.
  - `(silent: …)` can be used to alterate the width of an item, by soustracting the applied gutter; without affecting any margin rule to it (see [Example / demo](#example--demo)).

  ```scss
  @include this("s" "l", "row wrap", 1/2, true) { … }; // or…
  @include this("s" "l", "row wrap", 1/2, 2 -1) { … }; // or…
  @include this("s" "l", "row wrap", 1/2, 1px 2px 3px 4px) { … }; // or…
  @include this($gutter: false true) { … };
  ```

- `$position` (`null`): a positive (to push) or a negative (to pull) fraction of the container width.

  ```scss
  @include this("s" "l", "row wrap", 1/2, true, 1/2) { … }; // or…
  @include this("s" "l", "row wrap", 1/2, true, -1/2) { … }; // or…
  @include this($position: "center") { … };
  ```

- `$padding` (`null`): see `gutter`.

  ```scss
  @include this("s" "l", "row wrap", 1/2, true, 1/2, true) { … }; // or…
  @include this("s" "l", "row wrap", 1/2, true, 1/2, 1 -1) { … }; // or…
  @include this("s" "l", "row wrap", 1/2, true, 1/2, 1px 2px 3px 4px) { … }; // or…
  @include this($padding: false true) { … };
  ```

## Example / demo

```html
<ul class="catalog">
    <li class="catalog_product catalog_product--first"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product"></li>
    <li class="catalog_product catalog_product--last"></li>
</ul>
```

```scss
.catalog {
    // @include this($media, $flow, $width, $gutter, $position, $padding);
    @include this(false, row wrap, "max-width", true, "center", true);
    list-style: none;
    background: #eee;

    &_product {
        @include this("s" "l", false, 1/2, true, false, true);
        @include this("l", false, 1/4, true, false, true);
        background: #ddd;

        &--first {
            @include this("s" "l", false, 1, (silent: true));
            @include this("l", false, 1/2, (silent: true));
        }

        &--last {
            @include this($position: "push");
        }
    }
```

See and play on [Sassmeister](http://www.sassmeister.com/gist/0a4b4870f20b95404d8d463fa7500693).

## Add-ons

* [children mixin](//github.com/NicolasGraph/oui_grid/tree/dev/addons/children): apply `this` mixin with multiple widths to children elements;
* [CSS grid](//github.com/NicolasGraph/oui_grid/tree/dev/addons/css): Old style CSS grid to use oui_grid through classes or placeholders

## Credits

### Author

[Nicolas Morand](//twitter.com/NicolasGraph)

### Licence

This project is distributed under the [MIT licence](//opensource.org/licenses/MIT).

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
