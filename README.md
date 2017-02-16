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

@include _on(small, up) {

}

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

When building **Phrame** the first goal was to build a flexible tool to handle multiple
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

And you have these contents:

`MyAwsomeCmp.js`

```
import styles from './MyAwesomeCmp.scss'
```

`MyAwsomeCmp.scss`

```
@import '../../scss/core';

.body {
    background-color: _color();
}
```

`MyAwsomeCmp.scss`

```
@import '../../scss/core';
```



