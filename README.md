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
