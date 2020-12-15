# Vuetify Cheat Sheet
This is written for Vuetify 2.3.21

# Basics
## Installing
```
npm install -g vue-cli / yarn global add vue-cli
vue create project-name
cd project-name
vue add vuetify
```
For Electron app:
```
vue add electron-builder
```
## Commands
```
yarn serve
yarn build
```
Electron:
```
yarn electron:serve
yarn electron:build
```
# Features
## Accessibility
https://vuetifyjs.com/en/features/accessibility/
## Bidirectionality
https://vuetifyjs.com/en/features/bidirectionality/

```js
// src/plugins/vuetify.js

import Vue from 'vue'
import Vuetify from 'vuetify/lib'

Vue.use(Vuetify)

export default new Vuetify({
  rtl: true,
})
```
Changing direction from component: 
```js
this.$vuetify.rtl = true
```
## Breakpoints
https://vuetifyjs.com/en/features/breakpoints/

Material design breakpoints:
```
xs < 600px
sm 600px > < 960px
md 960px > < 1264px*
lg 1264px > < 1904px*
xl > 1904px*
```
Getting current breakpoint via API:

```
this.$vuetify.breakpoint.name
```

Making popup fullscreen on mobile:

```html
<template>
  <v-dialog :fullscreen="$vuetify.breakpoint.mobile">
    ...
  </v-dialog>
</template>
``` 

### Breakpoint service object

```ts
{
  // Breakpoints
  xs: boolean
  sm: boolean
  md: boolean
  lg: boolean
  xl: boolean

  // Conditionals
  xsOnly: boolean
  smOnly: boolean
  smAndDown: boolean
  smAndUp: boolean
  mdOnly: boolean
  mdAndDown: boolean
  mdAndUp: boolean
  lgOnly: boolean
  lgAndDown: boolean
  lgAndUp: boolean
  xlOnly: boolean

  // true if screen width < mobileBreakpoint
  mobile: boolean
  mobileBreakpoint: number

  // Current breakpoint name (e.g. 'md')
  name: string

  // Dimensions
  height: number
  width: number

  // Thresholds
  // Configurable through options
  {
    xs: number
    sm: number
    md: number
    lg: number
  }

  // Scrollbar
  scrollBarWidth: number
}
```

### Conditionals

```html
<template>
  <v-sheet
    :min-height="$vuetify.breakpoint.xs ? 300 : '20vh'"
    :rounded="$vuetify.breakpoint.xsOnly"
  >
    ...
  </v-sheet>
</template>
```

### Setting the mobile breakpoint
```js
// src/plugins/vuetify.js

export default new Vuetify({
  breakpoint: {
    mobileBreakpoint: 'sm' // This is equivalent to a value of 960
  },
})
```

### Setting mobile breakpoint for specific component
```html
<template>
  <v-banner mobile-breakpoint="1024">
    ...
  </v-banner>
</template>
```

### Changing SCSS grid variables
```scss
$grid-breakpoints: (
  'xs': 0,
  'sm': 340px,
  'md': 540px,
  'lg': 800px - 24px,
  'xl': 1280px - 24px
);
```

## Global configuration
`Vuetify.config` to get an object containing configuration options

### Silent mode 

Suppresses all Vuetify logs and warnings:
```js
// src/plugins/vuetify.js
import Vuetify from 'vuetify/lib'
Vuetify.config.silent = true
```

## Icons
https://vuetifyjs.com/en/features/icons/ — more about installing here. But you can choose the package you want during the Vuetify installation (via `vue add vuetify`)

### Choosing a font:

[Icon preset values](https://github.com/vuetifyjs/vuetify/tree/master/packages/vuetify/src/services/icons/presets)
```js
export default new Vuetify({
  icons: {
    iconfont: 'mdiSvg', // 'mdi' || 'mdiSvg' || 'md' || 'fa' || 'fa4' || 'faSvg'
  },
})
```

### Using custom icons:
#### Global configuring
```js
export default new Vuetify({
  icons: {
    iconfont: 'fa',
    values: {
      cancel: 'fas fa-ban',
      menu: 'fas fa-ellipsis-v',
    },
  },
})
```

#### Using in templates
```html
<v-icon v-html="'$vuetify.icons.menu'"></v-icon>
```

## Internationalization
https://vuetifyjs.com/en/features/internationalization/

## Layouts
https://vuetifyjs.com/en/features/layouts/

Basic layout:
```html
<v-app>
  <v-main>
    <v-container>
      Hello World
    </v-container>
  </v-main>
</v-app>
```

## Presets
https://vuetifyjs.com/en/features/presets/

## SASS variables
https://vuetifyjs.com/en/features/sass-variables/

### With Vuetify installed via Vue CLI
Create a folder called sass, scss or styles in your src directory with a file named variables.scss or variables.sass. The vuetify-loader will automatically bootstrap your variables into Vue CLI’s compilation process, overwriting the framework defaults.

### Example variables file
```scss
// src/sass/variables.scss

// Globals
$body-font-family: 'Work Sans', serif;
$border-radius-root: 6px;
$font-size-root: 14px;

// Variables must come before the import
$btn-letter-spacing: 0;
$btn-font-weight: 400;
$list-item-title-font-size: 0.929rem;
$list-item-dense-title-font-size: 0.929rem;
$list-item-dense-title-font-weight: initial;
$fab-icon-sizes: (
  'small': 20
);
$btn-sizes: (
  'default': 41,
  'large': 54
);

$headings: (
  'h1': (
    'size': 3.3125rem,
    'line-height': 1.15em
  ),
  'h2': (
    'size': 2.25rem,
    'line-height': 1.5em
  )
);
```

## Programmatic scrolling
https://vuetifyjs.com/en/features/scrolling/

### Usage
Target: Number, Selector or DOMElement

Options: Easing, Duration, Offset
```
@click="$vuetify.goTo(target, options)"
```

## Theme
https://vuetifyjs.com/en/features/theme/

### Light and Dark
```js
export default new Vuetify({
  theme: { dark: true },
})
```

### Standard colors
```js
{
  primary: '#1976D2',
  secondary: '#424242',
  accent: '#82B1FF',
  error: '#FF5252',
  info: '#2196F3',
  success: '#4CAF50',
  warning: '#FFC107',
}
```

How to change:

```js
const vuetify = new Vuetify({
  theme: {
    themes: {
      light: {
        primary: '#3f51b5',
        secondary: '#b0bec5',
        accent: '#8c9eff',
        error: '#b71c1c',
      },
    },
  },
})
```

Via API:
```js
// Light theme
this.$vuetify.theme.themes.light.primary = '#4caf50'

// Dark theme
this.$vuetify.theme.themes.dark.primary = '#4caf50'
```

How to prevent inheriting dark theme from the component
```html
<v-card dark>
  <p>From component</p>
  <v-theme-provider root>
    <p>From root</p>
  </v-theme-provider>
</v-card>
```

## Treeshaking
https://vuetifyjs.com/en/features/treeshaking/

# Styles and animations

## CSS Reset
https://vuetifyjs.com/en/styles/css-reset/

## Border radius
https://vuetifyjs.com/en/styles/border-radius/

Basic template: `.rounded-{0 || sm || md || lg || xl || pill || circle}`

Round by side or corner: `.rounded-{t || r || b || l || tl || tr || br || bl}-{0 || sm || md || lg || xl || pill || circle}`

SASS Variables:
```scss
$rounded: (
  0: 0,
  'sm': $border-radius-root / 2,
  null: $border-radius-root,
  'lg': $border-radius-root * 2,
  'xl': $border-radius-root * 6,
  'pill': 9999px,
  'circle': 50%
);

// How to change
$rounded: (
  'sm': $border-radius-root / 3,
  'lg': $border-radius-root * 2
);
```

## Colors
https://vuetifyjs.com/en/styles/colors/

Each color from the spec gets converted to a background and text variant for styling within your application through a class, e.g. `<div class="red">` or `<span class="red--text">`. These class colors are defined [here](https://github.com/vuetifyjs/vuetify/blob/master/packages/vuetify/src/styles/settings/_colors.scss).

Class template for text is `text--{lighten|darken}-{n}`
```html
<div class="purple darken-2"> <!-- Background -->
  <span class="purple--text text--lighten-5">Lorem ipsum</span> <!-- Text -->
</div>
```

### How to use optional color pack
```js
import colors from 'vuetify/lib/util/colors'

Vue.use(Vuetify)

export default new Vuetify({
  theme: {
    themes: {
      light: {
        primary: colors.red.darken1, // #E53935
        secondary: colors.red.lighten4, // #FFCDD2
        accent: colors.indigo.base, // #3F51B5
      },
    },
  },
})
```

[Material Colors Pack](https://vuetifyjs.com/en/styles/colors/#material-colors)

## Content

https://vuetifyjs.com/en/styles/content/

Vuetify has custom styling for multiple standard elements:

```html
<blockquote></blockquote>
<p></p>
<code></code>
<kbd></kbd>
<var></var>
```

## Display helpers
https://vuetifyjs.com/en/styles/display/

Specify the elements display property. These classes can be applied to all breakpoints from xs to xl. When using a base class,.d-{value}, it is inferred to be .d-${value}-xs.

`.d-{value}` for `xs`

`.d-{breakpoint}-{value}` for `sm`, `md`, `lg` and `xl`

The value property is one of:

+ `none`
+ `inline`
+ `inline-block`
+ `block`
+ `table`
+ `table-cell`
+ `table-row`
+ `flex`
+ `inline-flex`

### Examples
+ `.d-flex` — visible on all
+ `.d-flex .d-sm-none` — visible only on xs
+ `.d-none .d-sm-flex .d-md-none` — visible only on sm

### Hide elements
`.hidden-{breakpoint}-{condition}`

Conditions: `only`, `and-down`, `and-up`

### Display in print

`.d-print-none`, `.d-print-block` etc.

### Accessibility
Use the `d-sr` utility classes to conditionally hide content on all devices except screen readers.

`.d-sr-only` visually hides elements but will still announce to screen readers.

`.d-sr-only-focusable` visually hides an element until it is focused. This is useful when implementing skip links.

## Elevation

https://vuetifyjs.com/en/styles/elevation/

Sets `z-index` and `box-shadow`. Can be a prop. `elevation-{n}` where `n` is an integer between 0-24

### Dynamic elevation

```html
<template>
  <div class="text--primary">
    <!-- Using the elevation prop -->
    <v-hover>
      <template v-slot:default="{ hover }">
        <v-card
          :elevation="hover ? 24 : 6"
          class="mx-auto pa-6"
        >
          Prop based elevation
        </v-card>
      </template>
    </v-hover>

    <div class="my-6"></div>

    <!-- Using a dynamic class -->
    <v-hover>
      <template v-slot:default="{ hover }">
        <div
          :class="`elevation-${hover ? 24 : 6}`"
          class="mx-auto pa-6 transition-swing"
        >
          Class based elevation
        </div>
      </template>
    </v-hover>
  </div>
</template>
```

## Flex

https://vuetifyjs.com/en/styles/flex/

Display: `.d-{breakpoint?}-{flex || inline-flex}`

Flex direction: `.flex-{breakpoint?}-{row || row-reverse || column || column-reverse}`.

Justify: `.justify-{breakpoint?}-{start || end || center || space-between || space-around}`.

Align: `.align-{breakpoint?}-{start || end || center || baseline || stretch}`.

Align-self: `.align-self-{breakpoint?}-{start || end || center || baseline || auto || stretch}`.

Flex wrap: `.flex-{breakpoint?}-{nowrap || wrap || wrap-reverse}`.

Flex order: `.order-{breakpoint?}-{first || 0-12 || last}`.

Align content: `.align-content-{breakpoint?}-{start || end || center || space-between || space-around || stretch}`

Flex grow and shrink: `flex-{breakpoint?}-grow-{0 || 1}`, `flex-{breakpoint?}-shrink-{0 || 1}`

## Float

https://vuetifyjs.com/en/styles/float/

Template: `.float-{breakpoint?}-{left || right || none}`

## Spacing

https://vuetifyjs.com/en/styles/spacing/

Template `{property}{direction}-{breakpoint?}-{size}`

Property: `m` if margin, `p` is padding.

Direction: `t || b || l || r` for one side `s || e` for L || R in LTR/RTL mode, `x || y` for both left/right or top/bottom directions, `a` for all directions.

Size: `0` for 0, `1-16` = number * 4px, `n1-16` = number * (-4px), `auto` for auto.

## Text and typography

https://vuetifyjs.com/en/styles/text-and-typography/

Template: `.text-{breakpoint?}-{h1 || h2 || h3 || h4 || h5 || h6 || subtitle-1 || subtitle-2 || body-1 || body-2 || button || caption || overline}`

Font weight: `.font-weight-{black || bold || medium || regular || light || thin}`

Italic: `.font-italic`

Justify: `.text-{breakpoint?}-{left || center || right}`

Decoration: `.text-decoration-{none || line-through || overline || underline}`

Opacity: `.text--{primary || secondary || disabled}`

Transform: `.text-{lowercase || uppercase || capitalize}`

Wrapping: `.text-no-wrap`, `.text-break`

Ellipsis: `.text-truncate`

RTL: `text-{start || end}`

## Transitions

https://vuetifyjs.com/en/styles/transitions/

API:

+ v-fab-transition
+ v-fade-transition
+ v-expand-transition
+ v-scale-transition
+ v-scroll-x-transition
+ v-scroll-x-reverse-transition
+ v-scroll-y-transition
+ v-scroll-y-reverse-transition
+ v-slide-x-transition
+ v-slide-x-reverse-transition
+ v-slide-y-transition
+ v-slide-y-reverse-transition

Example:

```html
<v-menu transition="fade-transition">
  <template v-slot:activator="{ on, attrs }">
    <v-btn
      dark
      color="primary"
      v-bind="attrs"
      v-on="on"
    >
      Fade Transition
    </v-btn>
  </template>
  <v-list>
    <v-list-item
      v-for="n in 5"
      :key="n"
    >
      <v-list-item-title v-text="'Item ' + n"></v-list-item-title>
    </v-list-item>
  </v-list>
</v-menu>
```
