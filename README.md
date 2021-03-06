# PostCSS Nested [![Build Status][ci-img]][ci]

<img align="right" width="135" height="95"
     title="Philosopher’s stone, logo of PostCSS"
     src="http://postcss.github.io/postcss/logo-leftp.svg">

[PostCSS] plugin to unwrap nested rules like how Sass does it.

```css
.phone {
    &_title {
        width: 500px;
        @media (max-width: 500px) {
            width: auto;
        }
        body.is_dark & {
            color: white;
        }
    }
    img {
        display: block;
    }
}
```

will be processed to:

```css
.phone_title {
    width: 500px;
}
@media (max-width: 500px) {
    .phone_title {
        width: auto;
    }
}
body.is_dark .phone_title {
    color: white;
}
.phone img {
    display: block;
}
```

Use [postcss-current-selector] **after** this plugin if you want to use current selector in properties or variables values.

Use [postcss-nested-ancestors] **before** this plugin if you want to reference any ancestor element directly in your selectors with `^&`.

See also [postcss-nesting], which implements [Tab Atkin's proposed syntax](https://tabatkins.github.io/specs/css-nesting/) (requires the `&` and introduces `@nest`).

There is also [postcss-nested-props] for nested properties like `font-size`.

<a href="https://evilmartians.com/?utm_source=postcss-nested">
<img src="https://evilmartians.com/badges/sponsored-by-evil-martians.svg" alt="Sponsored by Evil Martians" width="236" height="54">
</a>

[postcss-current-selector]: https://github.com/komlev/postcss-current-selector
[postcss-nested-ancestors]: https://github.com/toomuchdesign/postcss-nested-ancestors
[postcss-nested-props]:     https://github.com/jedmao/postcss-nested-props
[postcss-nesting]:          https://github.com/jonathantneal/postcss-nesting
[PostCSS]:                  https://github.com/postcss/postcss
[ci-img]:                   https://travis-ci.org/postcss/postcss-nested.svg
[ci]:                       https://travis-ci.org/postcss/postcss-nested

## Usage

```js
postcss([ require('postcss-nested') ])
```

See [PostCSS] docs for examples for your environment.

## Options

### `bubble`

By default, plugin will unwrap only `@media`, `@supports` and `@document`
at-rules. You can add your custom at-rules to this list by `bubble` option:

```js
postcss([ require('postcss-nested')({ bubble: ['phone'] }) ]
```
