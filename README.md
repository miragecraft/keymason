# KeyMason
CSS based keyset renderer, create attractive keyset mockups and layouts using just HTML and CSS.

Requires CSS support for:
- Flexbox
- Grid
- Custom Properties
- Calc()
- Mask (for icons)

Due to the bleeding edge CSS features utilized it is not a goal of this project to have widespread browser compatibility, therefore the development target is the latest Chrome and Firefox browser. Chrome has sharper results when performing CSS transforms so is recommended for best visual quality.

For local development and usage (using the `File:\\\` protocol) the latest Firefox and Chrome both block SVG masks due to CORS policy. To get around this restriction for Firefox you will need to set the `privacy.file_unique_origin` flag to false in `about:config`, and for Chrome you will need to launch it with the command line switch of `--allow-file-access-from-files`, you can set up a shortcut with this switch, and set the `Target` value to be (as an example) `"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --allow-file-access-from-files`.

**Features**
- Row and column based layout system
- X and Y offset
- Space (convex) key
- Flipped key
- Special keys
  - Stepped
  - Big/Slim Ass Enter
  - ISO Enter
- Rotation & rotation origin offset
- Homing dot, bar, scoop and dish
- Window and light
- Basic SVG icons
- Outline based highlighting for potential use as an editor interface

**Limitations**
- Susceptible to pixel rounding errors when zooming.

# How to use

KeyMason makes extensive use of inline styles in order to assign value to custom properties.

All custom properties for length are based on keycap size, so value of "1" means 1 keycap long.

## General Layout

General layout is done using `<k-row>`, `<k-column>` and `<k-cap>`, for each of those elements, you can adjust the following custom properties:
  - `--x` and `--y` for X and Y offset respectively
  - `--r`, `--rx` and `--ry` for rotation (degree) and rotation origin offset x and y starting from top left

## Keycap

Keycap is constructed of the following:
```
<k-cap>
  <k-legend class="top left">Q</k-legend> <!-- repeat as necessary -->
</k-cap
```

For the `<k-cap>` element you can:
  - adjust size using the `--w` and `--h` custom properties for width and height
  - Also contains the following shortcuts using class name:
  ```
  [class~="1.25"] {--w:1.25}
  [class~="1.5"] {--w:1.5}
  [class~="1.75"] {--w:1.75}
  [class~="2"] {--w:2}
  [class~="2.25"] {--w:2.25}
  [class~="2.75"] {--w:2.75}
  [class~="3"] {--w:3}
  [class~="4"] {--w:4}
  [class~="5.5"] {--w:5.5}
  [class~="6.25"] {--w:6.25}
  [class~="7"] {--w:7}
  .tall {--h:2}
  ```

For the `<k-legend>` element you can:
  - adjust position using the following class names: `top`, `bottom`, `left`, `right`, `center`, `front`.
  - adjust size using the following class names: `medium`, `small` (default is big size, you can still add `big` class, it just doesn't do anything)
  
## Special Keys

Several special keys are available:

### Flipped

You can flip a key by applying the `flipped` class to the `<k-cap>` element.

A flipped 7u spacebar: `<k-cap class="flipped 7"></k-cap>`
A flipped 6.25u spacebar using `--w`: `<k-cap class="flipped" style="--w:6.25"></k-cap>`

### Stepped
```
<k-cap class="stepped" style="--w:1.75">
		<k-cap>
			<k-legend class="small">Caps<br>Lock</k-legend>
		</k-cap>
</k-cap>
```
Stepped key are declared by using class name `stepped` and nest two `<k-cap>` elements.

You must declare a width for stepped key (either using shortcut classname or `--w` custom property) because there exists several variants.

The nested `<k-cap>` has a default width based on outer `<k-cap>` width, based on the normal capslock key, you can override this by applying your own `--w` value, such as 1u:
```
<k-cap class="stepped" style="--w:1.75">
		<k-cap style="--w:1">
			<k-legend class="small">Caps<br>Lock</k-legend>
		</k-cap>
</k-cap>
```
### Big-Enter (Big Ass Enter)

`<to be continued...>`
