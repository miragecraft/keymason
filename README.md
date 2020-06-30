# KeyMason
CSS based keyset renderer, create attractive keyset mockups and layouts using just HTML and CSS.

[See demo here](http://www.miragecraft.com/projects/keymason.html).

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

## Default Custom Properties

Default custom properties used to draw the keycaps.

  - `--u` is the key size, used for width, height and various offset values.
  - `--gutter` is the distance between keycaps.
  - `--accent` is the thickness of the key highlight.
  - `--b-top`, `--b-side`, `--b-bottom` are the values used for the 3D effect of the keys.
  - `--r-base` is the corner radius of the key base, and `--r-top` is the corner radius of the key top.

A set of default colors are included for development purposes.

```
:root {
  --u: 60px;
  --gutter: 3px;
  --accent: 2px;
  
  /* Cherry profile */
  --b-top:4px;
  --b-side:10px;
  --b-bottom:10px;
  --r-base: 2px;
  --r-top: 4px;

  /* default colors */
  --legend: #3e3e3e;
  --base: #CDCDCD;
  --lightest: #efe8e8;
  --lighter: #dadada;
  --dark: #bbbbbb; 
  --darker: #AAA9AA;
  --darkest: #9D9D9D;
  --shadow: #474747;
}
```

A `theme.css` file is included with some different preset of color themes.


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
  - adjust size using the following class names: `medium`, `small` (default is large size, you can still add `large` class, it just doesn't do anything)
  
## Special Keys

Several special keys are available:

### Space

Using `space` class to create a space key, it adds a gradient on top for that convex look.

### Flipped

You can flip a key by applying the `flipped` class to the `<k-cap>` element.

A flipped 7u spacebar: `<k-cap class="space flipped 7"></k-cap>`

A flipped 6.25u spacebar using `--w`: `<k-cap class="space flipped" style="--w:6.25"></k-cap>`

### Stepped
```
<k-cap class="stepped">
	<k-cap>
		<k-legend class="small">Caps<br>Lock</k-legend>
	</k-cap>
</k-cap>
```
Stepped key are declared by using class name `stepped` and nest two `<k-cap>` elements, defaults to 1.75u base (`--w:1.75`) and 1.25u step (`--step:1.25`).

Class names `right` and `center` are used to change the alignment of the step top. Left is the default, you can add `left` class for consistency sake but it's not necessary.

You can create a "deep" stepped key using the `deep` class.
```
<k-cap class="stepped deep" style="--w:3;--step:2"> <!-- deep stepped key with base size 3u and step size 2u -->
	<k-cap>
		<k-legend class="small">Caps<br>Lock</k-legend>
	</k-cap>
</k-cap>
```
### ISO Enter

ISO enter key can be created using the `iso-enter` class and the following element structure:
```
<k-cap class="iso-enter">
	<k-cap>
		<k-legend class="small center"><k-icon class="enter-tall"><i></i></k-icon></k-legend>
	</k-cap>
	<k-cap><k-corner></k-corner></k-cap>
</k-cap>
```
This key is created using two separate keys combined into one, a horizontal key (root `<k-cap>` element) and a vertical key (first nested `<k-cap>` element).

You can place the `<k-legend>` element in either one of them in order to align the legend to either the vertical segment of the key, or the horizontal segment of the key.
```
<k-cap class="iso-enter">
	<k-legend class="small center"><k-icon class="enter-tall"><i></i></k-icon></k-legend>
	<k-cap></k-cap>
	<k-cap><k-corner></k-corner></k-cap>
</k-cap>
```

### Big Enter (Big Ass Enter)

Big (ass) enter can be created using the `big-enter` class and the following element structure:
```
<k-cap class="big-enter">
	<k-cap>
		<k-legend class="small left"><k-icon class="enter"><i></i></k-icon>&nbsp;Enter</k-legend>
	</k-cap>
	<k-cap><k-corner></k-corner></k-cap>
</k-cap>
```
This key is created using two separate keys combined into one, a vertical key (root `<k-cap>` element) and a horizontal key (first nested `<k-cap>` element).

You can place the `<k-legend>` element in either one of them in order to align the legend to either the vertical segment of the key, or the horizontal segment of the key.
```
<k-cap class="big-enter">
	<k-legend class="small left"><k-icon class="enter"><i></i></k-icon>&nbsp;Enter</k-legend>
	<k-cap></k-cap>
	<k-cap><k-corner></k-corner></k-cap>
</k-cap>
```

### Big Enter Slim

This is the slim variant of the big ass enter, it shows up on some old keyboards, added just for completeness sake.

Add the `slim` class to `big-enter` to use, it simply changes the width of key.

## Special Elements

### Homing Device

`<k-homing>` element is used to display homing features, using class `bar`, `dot`, `dish` and `scoop`.
```
<k-cap>
	<k-legend class="top left">F</k-legend>
	<k-homing class="bar"></k-homing>
</k-cap>
```

### Key Window

`<k-window>` element is used to create a key window, defaults to unlit.
```
<k-cap>
	<k-legend class="small">F9</k-legend>
	<k-window></k-window>
</k-cap>
```
Custom property `--led` is used to light it up with color, some class names are provided with preset values: `red`, `green`, `blue` and `gold`.

## Icons

A basic SVG icon system is included, the syntax is `<k-icon class="tab"></k-icon>`.

The following icons are provided - `tab`, `win`, `menu`, `capslock`, `backspace`, `backspace-x`, `enter`, `enter-long`, `enter-tall`, `shift`, and `arrow`.

For the `arrow` icon, you can rotate it using `up`, `down`, and `right` class such as `<k-icon class="arrow up"></k-icon>`, default direction is left.

You can create your own icon easily by simply drawing black outline, save as an SVG file in the icons folder and then add it to the CSS. `--iw` is the icon width, and `--ih` is the height which is defined as a multiplier (default to 1 resulting in square shaped icon).

## Special features

### Selectable

Add the `seletable` class to an outer wrapper enable key highlighting on hover, can be used to build user interface.

### Blueprint

Add the `blueprint` class to to trigger a special blueprint display mode which uses legend color to draw outlines of the keys.

### Anchor

Add `anchor` class to any `<k-row>`, `<k-column>` and `<k-cap>` element will make it absolutely positioned.

What this means is that now you can move the key around without affecting the layout of subsequent keys, useful for some special layouts such as curved keys.

### Notes

The `<k-note>` element acts like `<k-cap>` in terms of positioning, but is style-less otherwise. This lets you add text such as row number (R1, R2...) using the very same `<k-legend>` element, while having all the positioning tools at your disposal.
