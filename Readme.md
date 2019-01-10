# destyle.css

[![npm][npm-image]][npm-url] [![license][license-image]][license-url]

Opinionated [reset stylesheet](https://cssreset.com/what-is-a-css-reset/) that provides a clean slate for styling your html.

## What it does

- Ensures consistency across browsers (thanks normalize.css)
- Resets spacing (margin & padding)
- Resets font-size and line-height
- Prevents the necessity of reseting user agent styles
- Prevents style inspector bloat by only targeting what is necessary
- Contributes to the separation of presentation and semantics
- Works well with all kind of styling approaches, atomic libraries like [tachyons](https://tachyons.io/), component based styling like css-in-js in [React](https://reactjs.org), good 'ol css, ...

## Why?

[Eric Meyer's reset](https://meyerweb.com/eric/tools/css/reset/) resets properties on elements that do not need it, are unused or even deprecated, this creates bloat in the browser's style inspector which makes developing and debugging less efficient. [Normalize.css](https://github.com/necolas/normalize.css) makes elements look consistent across browsers and it does it well, but it does not remove the user agent's assumptions about how things look. Destyle.css targets both reseting & normalization.

## Installation

```shell
$ npm install --save destyle.css
```

Download: https://raw.githubusercontent.com/nicolas-cusan/destyle.css/master/destyle.css

## Usage

Include `destyle.css` in the `head` of your HTML file before your main stylesheet.

### Recommended

Add your base font and color styles to the `body` element in your stylesheet, all other elements will inherit the style from the body.

```css
/* app.css */

body {
  color: #333;
  font: 16px/1.4 'Helvetica Neue', sans-serif;
}
```

It is discouraged to define styles for raw html tags apart from `body` and `html`, use classes (or any other selectors / system) for styling.

If you need to create styles for tags generated by a CMS or markdown wrap them in a class (e.g. `.type`).

```css
.type h1 {
  \* styles *\
}

.type h2 {
  \* styles *\
}
```

```html
<div class="type">{{ generatedMarkup }}</div>
```

## Example

An `h1` might need to be bold & large in some context (at the top of a text page) but might be small and inconspicuous in others (on a settings page in an app).

Creating two different styles for `h1` is made easy as only the styles you need to get the desired visual results have to be applied without the need to overwrite default styles while maintaining semantics.

```css
/* No reseting of the user agent styles necessary,
 * just take care of making things look how you want to. */

/* Bold, large title */
.main-title {
  font-size: 3em;
  margin-bottom: 20px;
  font-weight: bold;
}

/* Just some padding and gray color, otheriwse looks like normal text */
.secondary-title {
  color: gray;
  padding: 10px;
}
```

```html
<!-- article.html -->
<h1 class="main-title">Large title</h1>

<!-- profile.html -->
<h1 class="secondary-title">Small title</h1>

<!-- Looks the same as `h1.secondary-title` -->
<p class="secondary-title">Other small title</p>
```

How to create the styles is up to the author, it can be by creating classes, compose style using functional classes, styling inside a react component, etc. In any case the author always gets a clean slate for styling each element and it is up to him/her to reuse the styles or start from scratch for every instance.

## Rules & Caveats

- The box model is reset to `border-box` using the `*` selector
- `button` and `input` are also reset (as much as possible)
- `code`, `pre`, `kbd`, `samp` maintain a monospaced font-family
- `hr` is set to be a solid 1px line that inherits its color from its parent's text color
- Inline elements that carry style (`b`, `i`, `strong`, etc.) are not reset.
- `textarea` maintains its natural height.
- `select` is reset using `appearance: none` which is not cross-browser, be advised when styling custom selects. You can find a good guide [here](https://www.filamentgroup.com/lab/select-css.html)
- HTML5 Inputs like `range` and `color` are not reset.

## Credits

This project is heavily inspired by [normalize.css](https://github.com/necolas/normalize.css) and the original [reset](https://meyerweb.com/eric/tools/css/reset/) by Eric Meyer. The source of the test page is from [html5-test-page](https://github.com/cbracco/html5-test-page/pulls).

[license-image]: https://img.shields.io/npm/l/destyle.css.svg?style=flat-square
[license-url]: LICENSE
[npm-image]: https://img.shields.io/npm/v/destyle.css.svg?style=flat-square
[npm-url]: https://www.npmjs.com/package/destyle.css
