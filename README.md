# KeyMason
CSS based keyset renderer, create attractive keyset mockups and layouts using just HTML and CSS.

Requires CSS support for:
- Flexbox
- Grid
- Custom Properties
- Calc()
- Mask (for icons)

Due to the bleeding edge CSS features utilized it is not a goal of this project to have widespread browser compatibility, therefore the development target is the latest Chrome and Firefox browser. Chrome has sharper results when performing CSS transforms so is recommended for best visual quality.

For local development and usage (using the `File:\\\` protocol) the latest Firefox and Chrome both block SVG masks due to CORS policy. To get around this restriction for Firefox you will need to set the `privacy.file_unique_origin` flag to false in `about:config`, and for Chrome you will need to launch it with the command line switch of `--allow-file-access-from-files`, you can set up a shortcut with this switch, and set the "Target" value to be (as an example) `"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --allow-file-access-from-files`.

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
