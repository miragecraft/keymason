# KeyMason
CSS based keyset renderer, create attractive keyset mockups and layouts using just HTML and CSS.

Requires CSS support for:
- Flexbox
- Grid
- Custom Properties
- Calc()
- Mask (for icons)

Tested on Chrome and Firefox, for local development the latest Firefox blocks SVG masks due to CORS policy, you will need to set the `privacy.file_unique_origin` flag to false in `about:config`, or make use of an extension such as [CORS Everywhere](https://addons.mozilla.org/en-CA/firefox/addon/cors-everywhere/).

Due to the bleeding edge CSS features utilized it is not a goal of this project to have widespread browser compatibility, therefore the development target is the latest Chrome and Firefox browser. Chrome has sharper results when performing CSS transforms so is recommended for best visual quality.

Features
- Row and column based layout system
- X and Y offset
- Space (convex) key
- Flipped key
- Special keys
  - Stepped (adjustible step size)
  - Big (Ass) Enter + Slim (Ass) Enter
  - ISO Enter
- Rotation & rotation origin
- Homing dot, bar, scoop and dish
- Window and light
- Basic SVG icons
- Outline based highlighting for potential use as an editor interface

Limitations
- Susceptible to pixel rounding errors when zooming.
