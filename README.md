# Oui_grid

## In process!

A sass powered css responsive grid builder [flexbox](//caniuse.com/#feat=flexbox) and [calc()](//caniuse.com/#search=calc).
Click these features for support informations via [caniuse.com](//caniuse.com/).

* [Features](#features)
* [Settings](#settings)
* [Mixins](#mixins)
    * [bpt](#bpt)
    * [item](#item)
* [Addons](#addons)

## Features

* Unlimited columns width;
* unlimited breakpoints;
* responsive gutters;
* gutters as margin and/or padding;
* and more…

## Usage

Import `oui_grid.scss` in your main `.scss` file.

```
@import "_oui_grid";
```

## Settings

See `src/settings/_variables.scss`.

### $layout

```scss
$layout: (
    s: (
        content-max-width : 480px,
        vertical-spacing  : 12px,
        horizontal-spacing: 8px
    ),
    m: (                           // Each key is used as a breakpoint.
        device-min-width  : 640px, // Media-query min-width (also generates the max-width of the previous breakpoint).
        content-max-width : 800px, // Max-width to optionally apply to containers
        vertical-spacing  : 16px,  // Top and bottom gutters
        horizontal-spacing: 12px   // Right and left gutters
    ),
    …
);
```

## Mixins

See `src/mixins/_mixins.scss`.

### item

```scss
@include item($media, $flow, $width, $gutter, $position, $padding);
```

#### arguments

- `$media` (`null`): media-query min-width and/or max-width as `$layout` map keys.

    ```scss
    @include item("s") { … }; // or…
    @include item("m" "l") { … }; // or…
    @include item(false "l") { … };
    ```

- `flow` (`null`): …

    ```scss
    @include item("s" "l", "grid") { … };
    ```

- `$width` (`null`): fraction of factor of the container width.
You can also use `true` to apply a width of 100% and a max-width of the `$max-content-width` responsive value.
    ```scss
    @include item("s" "l", "grid", 1/2) { … }; // or…
    @include item("s" "l", "grid", .5) { … };
    ```

- `$gutter` (`null`): value or list of two or four values.
  - `true` or `false` will enable or disable the responsive gutter;
  - `nested` will be read as a factor of `-1` of the responsive gutter (see the next list item);
  - a unitless value will be read as a factor of the responsive gutter;
  - a usual margin value followed by its unit will be used as it.

    ```scss
    @include item("s" "l", "grid", 1/2, true) { … }; // or…
    @include item("s" "l", "grid", 1/2, 2 -1) { … }; // or…
    @include item("s" "l", "grid", 1/2, 1px 2px 3px 4px) { … };
    ```

- `$position` (`null`): a positive (to push) or a negative (to pull) fraction of the container width.

    ```scss
    @include item("s" "l", "grid", 1/2, true, 1/2) { … }; // or…
    @include item("s" "l", "grid", 1/2, true, -1/2) { … };
    ```

- `$padding` (`null`): see `margin`.

    ```scss
    @include item("s" "l", "grid", 1/2, true, 1/2, true) { … }; // or…
    @include item("s" "l", "grid", 1/2, true, 1/2, 1 -1) { … }; // or…
    @include item("s" "l", "grid", 1/2, true, 1/2, 1px 2px 3px 4px) { … };
    ```

## Addons

* [children mixin](//github.com/NicolasGraph/oui_grid/tree/dev/addons/oui_grid_children)

## Author

[Nicolas Morand](//twitter.com/NicolasGraph)

## Licence

This project is distributed under the [MIT licence](//opensource.org/licenses/MIT).

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
