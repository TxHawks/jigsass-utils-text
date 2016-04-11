# JigSass Utils Text
[![NPM version][npm-image]][npm-url]  [![Dependency Status][daviddm-image]][daviddm-url]   

 > Text composition related utility classes

The JigSass Utils Text module provides utility classes controlling text alignment, text decoration,
vertical alignment and white-space.

Class names follow the [Emmet](http://docs.emmet.io/cheat-sheet/) abbreviation
syntax, with colons (':') replaced by two dashes (`--`) to follow BEM naming
conventions.

## Available classes

#### Text Alignment

  - `.u-ta--start`: text-align: (left|right) (left in `LTR`, right in `RTL`)
    - `[dir=ltr] .u-ta--start`: text-align: left
    - `[dir=rtl] .u-ta--start`: text-align: right
  - `.u-ta--l`: text-align: left
  - `.u-ta--c`: text-align: center
  - `.u-ta--end`: text-align: (right|left) (right in `LTR`, left in `RTL`)
    - `[dir=ltr] .u-ta--end`: text-align: right
    - `[dir=rtl] .u-ta--end`: text-align: left
  - `.u-tr--r`: text-align: right
  - `.u-ta--j`: text-align: justify


#### Text Decoration

  - `.u-td--n`: text-decoration: none
  - `.u-td--u`: text-decoration: underline
  - `.u-td--o`: text-decoration: overline
  - `.u-td--l`: text-decoration: line-through


  - `.u-td--n:hover`: text-decoration: none when hovered
  - `.u-td--u:hover`: text-decoration: underline when hovered
  - `.u-td--o:hover`: text-decoration: overline when hovered
  - `.u-td--l:hover`: text-decoration: line-through when hovered


  - `.u-td--n:focus`: text-decoration: none when focused
  - `.u-td--u:focus`: text-decoration: underline when focused
  - `.u-td--o:focus`: text-decoration: overline when focused
  - `.u-td--l:focus`: text-decoration: line-through when focused


  - `.u-td--n:active`: text-decoration: none when active
  - `.u-td--u:active`: text-decoration: underline when active
  - `.u-td--o:active`: text-decoration: overline when active
  - `.u-td--l:active`: text-decoration: line-through when active


#### Vertical Alignment

  - `.u-va--sup`: vertical-align: super
  - `.u-va--t`: vertical-align: top
  - `.u-va--tt`: vertical-align: text-top
  - `.u-va--m`: vertical-align: middle
  - `.u-va--bl`: vertical-align: baseline
  - `.u-va--b`: vertical-align: bottom
  - `.u-va--tb`: vertical-align: text-bottom
  - `.u-va--sub`: vertical-align: sub


#### White Space

  - `.u-whs--n`: white-space: normal
  - `.u-whs--p`: white-space: pre
  - `.u-whs--nw`: white-space: nowrap
  - `.u-whs--pw`: white-space: pre-wrap
  - `.u-whs--pl`: white-space: pre-line


## Installation

Using npm:

```sh
npm i -S jigsass-utils-text
```

## Usage
Import JigSass Utils Text into your main scss file near its very end, together with all
other utilities (utilities should always be the last to be imported).

```scss
@import 'path/to/jigsass-utils-text/scss/index';
```

Like all other JigSass Utils, JigSass Text does not automatically generate any CSS
when imported. You would need to explicitly indicate that each individual text
class should actually be generated in each component or object it is used in
(clarification: This will include style declarations inside `.foo` and .`bar`):

```scss
// _c.foo.scss
.foo {
  @include jigsass-util(u-va, $modifier: m); // <-- vertical-align: middle

  ...
}
```

```scss
// _c.bar.scss
.bar {
  @include jigsass-util(u-va, $modifier: b);  // <-- vertical-align: bottom
  @include jigsass-util(u-va, $modifier: t, $from: large); // <-- vertical-align: top from large bp and on.

  ...
}
```

Doing so helps us a great deal with portability, as no matter where we import component or object
partials, the correct utility classes will be generated. Think of it as a poor man's dependency
management.

Developer communication is also assisted by including "dependencies" wherever they are required,
as anyone going through a partial, can easily understand how it should be marked up with just a
glance.

As far as bloat goes, just don't worry about it - the actual styles will only be generated once,
at the location in the cascade where the Jigsass Text partial was imported into the main file.


JigSass Text classes are responsive-enabled, using [JigSass MQ](https://txhawks.github.io/jigsass-tools-mq/)
and the breakpoints defined in the [$jigsass-breakpoints](https://txhawks.github.io/jigsass-tools-mq/#variable-jigsass-breakpoints) variable.

Based on the breakpoint arguments passed to `jigsass-util` when including a JigSass Text class,
responsive modifiers are generated according to the following logic:

```scss
.u-va--<modifier>[-[-from-<breakpoint-name>][-until-<breakpoint-name>][-misc-<breakpoint-name>]]
```

So, assuming the `medium`, `large` and `landscape` breakpoints are defined in `$jigsass-breakpoints`
as `600px`, `1024px` and `(orientation: landscape)` respectively,

```scss
@include jigsass-util(u-va, $modifier: bl);
```
will generate the `.u-va--bl` class, which is not limited to any media-query.

```scss
@include jigsass-util(u-va, $modifier: tt, $until: medium);
```

will generate the `.u-va--tt--until-medium` class, which will be in effect at
`(max-width: 37.49em)` and will override styles in the default class until that point.

```scss
@include jigsass-util(u-va, $modifier: t, $from: large, $misc: landscape);
```

will generate the `.u-va--t--from-large-when-landscape` class, which will go into
effect at `(min-width: 64em) and (orientation: landscape)` and will override styles in the default
class under these  conditions.


## Documentation

The full documentation was generated using mdcss, and is available at 
[https://txhawks.github.io/jigsass-utils-text/](https://txhawks.github.io/jigsass-utils-text/)

## Contributing

It is a best practice for JigSass modules to *not* automatically generate css on `@import`, but 
rather have the user explicitly enable the generation of specific styles from the module.

Contributions in the form of pull-requests, issues, bug reports, etc. are welcome.
Please feel free to fork, hack or modify JigSass Text in any way you see fit.

#### Writing documentation

Good documentation is crucial for usability, scalability and maintainability. When 
contributing, please do make sure that both its Sass functionality (functions, mixins, 
variables and placeholder selectors), as well as the CSS it generates (selectors, 
concepts, usage exmples, etc.) are well documented.

Jigsass Text uses Jonathan Neal's [mdcss](//github.com/jonathantneal/mdcss).

When styles and documentation comments are not automatically generated by your module on `@import`,
please use the `sgSrc/sg.scss` file to enable their generation.

In addition, any file in `sgSrc/assets` will be available for use in the style guide.



## File structure
```bash
┬ ./
│
├─┬ scss/ 
│ └─ index.scss # The module's importable file.
│
├─┬ sgSrc/      # Style guide sources
│ │
│ ├── sg.scc    # It is a best practice for JigSass 
│ │             # modules to not automatically generate 
│ │             # css and documentation on `@import.` 
│ │             # Please use this file to enable css
│ │             # and documentation comments) generation.
│ │
│ └── assets/   # Files in `sgSrc/assets` will be 
│               # available for use in the style guide
│
└─┬ docs/      # Documention
  │
  └── styleguide/ # Generated documentation 
                  # of the module's CSS
```

**License:** MIT



[npm-image]: https://badge.fury.io/js/jigsass-utils-text.svg
[npm-url]: https://npmjs.org/package/jigsass-utils-text

[daviddm-image]: https://david-dm.org/TxHawks/jigsass-utils-text.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/TxHawks/jigsass-utils-text
