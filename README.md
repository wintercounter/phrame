# Phrame
Modular, configurable SASS framework mostly to be used with CSS modules.

# What **Phrame** offers:
- 0kb footprint
- Multilevel configuration system
- Config references
- Color/Scheme management
- Exposed breakpoint rules
- Easing library
- Helper mixins
- Modules
- No bloat
- Use on existing codebases

# Basic setup

```bash
npm install phrame2 --save
```

Now use it:

```scss
// Load the environment (has not output)
@import '~phrame2/core';

// Just a simple reset (optional)
@import '~phrame2/module/reset';

// Some basic styles (optional)
@import '~phrame2/module/basic';

// Expose breakpoints (optional)
@import '~phrame2/module/expose';
```

> **Phrame** related stuff (mixins, functions, etc.) are prefixed with an `_` so **Phrame** won't conflict your codebase.

---

# Config system

The config system uses Sass Maps as a multi dimensional array - since Sass is only able to handle a
single level (looking at you map-get).

With building **Phrame** my primary goal was to build a flexible tool to handle multiple
sites from one codebase. For this to work we needed a system where it's simple to override the common stuff
and makes easy to switch color schemes for example. To achieve this we've built a flow where you can overwrite
the default configuration.

## Flow

To use such behavior you need to import your own instance of **Phrame** into your codebase.

`Load Phrame Env -> Config Overrides -> Output`

Here's a basic structure with the ability to override config values:

```

├── components
│   └── MyAwsomeCmp
│        └── MyAwsomeCmp.js
│        └── MyAwsomeCmp.scss
│
└── scss
    ├── core.scss
    └── config.scss

```

With these contents (and flow backwords to the root):

`MyAwsomeCmp.js`
```js
import styles from './MyAwesomeCmp.scss'
```

`MyAwsomeCmp.scss`
```scss
// Always import this `core` instead of Phrame directly
@import '../../scss/core';

body {
    background-color: _color('body.bg');
    font-size: _config('size.large');

    @include _on('mobile') {
        background-color: _color('body.bg-on-mobile');
        font-size: _config('size.sub-sizes.small');
    }
}
```

`core.scss`
```scss
@import '~phrame2/core';
@import './config';
```

`config.scss`
```scss
// $_ is just a temporary assignment
// because this is how functions work in Sass
$_: _config('size', (
    'small': 3.0em,
    'big': 8.0em,
    'large': 1.4em,
    'sub-sizes': (
        'small': 1.0em,
        'big': 2.0em,
        'large': 3.4em
    )
));
```

# Config Management
In case you're building a multi-(site/color) solution, or just need to make
the environment configurable, you may end up having multiple configuration files.

**Phrame** comes with multiple solutions to easier manage these options/values.

## `@function _config(key[, value])`

- `key`: The key of the config property (size.small)
- `value` (optional):

> **Good to know:** key is optional too. Returns full config object. Good for debugging purposes.

> **Good to know:** this is just a shorthand function, `_config-set` and `_config-get` is available too.

### Usage