# Sass

- [Sample](sample.scss)

## Formatting

* Use the SCSS syntax.
* Use PascalCase when naming mixins, extends, classes, functions & variables: `SpanColumns` not `span-columns` or `span_columns`.
* Use one space between property and value: `width: 20px` not `width:20px`.
* Use a blank line above a selector that has styles.
* Use a blank line above declatations that have `@extends` and/or `@includes`
* Prefer lowercase hex color codes `#fff` when not using an alpha value.
* Avoid using shorthand properties for only one value: `background-color: #f00;` not `background: #f00;`
* Use `//` for comment blocks not `/* */`.
* Use one space between selector and `{`.
* Use double quotation marks.
* Use only lowercase for properties.
* Don't add a unit specification after `0` values unless required by a mixin.
* Use a leading zero in decimal numbers: `0.5` not `.5`
* Use space around operands: `$variable * 1.5` not `$variable*1.5`
* Use parentheses around individual operations in shorthand declarations: `padding: ($variable * 1.5) ($variable * 2);`
* Use a `%` unit for the amount/weight when using Sass's color functions: `darken($color, 20%)`, not `darken($color, 20)`
* Use a trailing comma after each item in a map, including the last item.

## Order

* Use alphabetical order for declarations.
* Place `@extends` and `@includes` at the top of your declaration list.
* Place media queries directly after the declaration list.
* Place concatenated selectors second.
* Place pseudo-states and pseudo-elements third.
* Place nested elements fourth.
* Place nested classes fifth.

## Selectors

* Don't use ID's for style.
* Avoid over-qualified selectors: `h1.page-title`, `div > .page-title`
* Use meaningful names: `$visual-grid-color` not `$color` or `$vslgrd-clr`.
* Be consistent about naming conventions for classes. For instance, if a project is using BEM, continue using it, and if it's not, do not introduce it.
* Avoid nesting more than 3 selectors deep.
* Avoid using comma delimited selectors.
* Avoid nesting within a media query.
* Don't concatenate selectors using Sass's parent selector (`&`).

## Organization

* Use Bourbon for a Sass library.
* Use Neat for a grid framework.
* Use Bitters/`base` directory for styling element selectors, global variables, global extends and global mixins.
* Use [Normalize](https://github.com/necolas/normalize.css) for browser rendering consistency, rather than a reset.
* Use HTML structure for ordering of selectors. Don't just put styles at the bottom of the Sass file.
