This fork is intended to work with Webpack 4 and Babel 7, it's open for issues and help is welcome, for now:

Added :
- markdown-it-container
- markdown-it-source-map
- Corrected the source for mardown-it-katex
- update dependencies to work with Babel V7
- created a dist folder using Webpack 4 and Babel 7

The following items have been removed as I think that Konishi won't need such features for its
markdown previews.

Remove:
- markdown-it-icons
- markdown-it-footnote
- markdown-it-abbr
- markdown-it-ins
- markdown-it-toc-and-anchor

TODO:
- It need loader for emoji (markdown-it-emoji)

Next plugin to add:
- markdown-it-plugin-echarts
- markdown-it-plugin-mermaid
- markdown-it-plugin-flowchart



# vue-markdown

[![npm](https://img.shields.io/npm/v/vue-markdown.svg?style=flat)](https://www.npmjs.com/package/vue-markdown)
[![npm](https://img.shields.io/npm/l/vue-markdown.svg?style=flat)](https://www.npmjs.com/package/vue-markdown)
[![npm](https://img.shields.io/npm/dt/vue-markdown.svg?style=flat)](https://www.npmjs.com/package/vue-markdown)

> If you want vue-markdown for `vue1.X.X`, please checkout [vue-markdown1.X.X](https://github.com/miaolz123/vue-markdown/tree/v1).

A Powerful and Highspeed Markdown Parser for Vue.

Quick start: `<vue-markdown>i am a ~~tast~~ **test**.</vue-markdown>`

Supported Markdown Syntax:

* [x] Source map in html (data-source-line="")
* [x] automatic table of contents
* [x] table & class customize
* [x] *SyntaxHighlighter
* [x] custom container
* [x] definition list
* [x] strikethrough
* [x] GFM task list
* [x] abbreviation
* [x] superscript
* [x] subscript
* [x] footnote
* [x] insert
* [x] *katex
* [x] emoji
* [x] icon
* [x] mark

`*SyntaxHighlighter` work with [Prism](https://prismjs.com) recommend

`*katex` need add [katex css](https://unpkg.com/katex/dist/katex.min.css).

# Example

[simple](https://github.com/miaolz123/vue-markdown/blob/master/example/simple)

[webpack-simple](https://github.com/miaolz123/vue-markdown/blob/master/example/webpack-simple)

[Live Demo](https://miaolz123.github.io/vue-markdown/)

# Installation

### Browser globals

> The **dist** folder contains `vue-markdown.js` with the component exported in the `window.VueMarkdown` object.

```html
<body>
  <vue-markdown>i am a ~~tast~~ **test**.</vue-markdown>
</body>
<script src="path/to/vue.js"></script>
<script src="path/to/vue-markdown.js"></script>
<script>
    Vue.use(VueMarkdown);
    var vm = new Vue({
        el: "body"
    });
</script>
```

### NPM

```shell
$ npm install --save vue-markdown-konishi
```

or Yarn

```shell
$ yarn add vue-markdown-konishi --save
```

## CommonJS

```js
var VueMarkdown = require('vue-markdown-konishi);

new Vue({
  components: {
    'vue-markdown': VueMarkdown
  }
})
```

## ES6 (Vue-CLI users)

After installing via Yarn or NPM, use the following snippet in the script portion of the Vue component which you wish to render the Markdown.

```js
import VueMarkdown from 'vue-markdown-konishi'

new Vue({
  components: {
    VueMarkdown
  }
})
```

# Slots

```html
<vue-markdown>this is the default slot</vue-markdown>
```

After setting up the middleware in your vue component above, using the embedded markdown is as easy as writing it between the `vue-markdown` tags.

VueMarkdown has a default slot which is used to write the `markdown` source.

TIP: The default slot only renders **once** at the beginning, and it will overwrite the prop of `source`!

# Props

| Prop | Type | Default | Describe |
| ---- | ---- | ------- | ------- |
| watches | Array | `["source", "show", "toc"]` | HTML refresh automatically when the prop in this array changed |
| source | String | `null` | the markdown source code |
| show | Boolean | `true` | enable render to the default slot automatically |
| html | Boolean | `true` | enable HTML syntax in source |
| xhtml-out | Boolean | `true` | `<br></br>` => `<br />` |
| breaks | Boolean | `true` | `\n` => `<br>` |
| linkify | Boolean | `true` | autoconvert URL-like text to link |
| emoji | Boolean | `true` | `:)` => `😃` |
| markdownItIcons | Boolean |  `true`| add Font Awesome icon
| sourceMap | Boolean | `true`| add line number in html data attribute
| typographer | Boolean | `true` | enable some language-neutral replacement and quotes beautification |
| lang-prefix | String | `language-` | CSS language prefix for fenced blocks |
| quotes | String | `“”‘’` | use `“”‘’` for Chinese, `„“‚‘` for German, `«»„“` for Russian |
| table-class | String | `table` | customize html class of the `<table>` |
| task-lists | Boolean | `true` | enable GFM task list |
| toc | Boolean | `false` | enable automatic table of contents |
| toc-id | String | `undefined` | the HTML id to render TOC |
| toc-class | String | `table` | customize html class of the `<ul>` wrapping the TOC |
| toc-first-level | Number | `2` | use `2` if you want to skip `<h1>` from the TOC |
| toc-last-level | Number | `'toc-first-level' + 1` | use `5` if you want to skip `<h6>` from the TOC |
| toc-anchor-link | Boolean | `true` | enable the automatic anchor link in the headings |
| toc-anchor-class | String | `toc-anchor` | customize the anchor class name |
| toc-anchor-link-symbol | String | `#` | customize the anchor link symbol |
| toc-anchor-link-space | Boolean | `true` | enable inserting a space between the anchor link and heading |
| toc-anchor-link-class | String | `toc-anchor-link` | customize the anchor link symbol class name |
| anchorAttributes | Object | `{}` | anchor tag attributes such as `target: '_blank'` or `rel: 'nofollow'` |
| prerender | Function (String) String | `null` | filter function before markdown parse |
| postrender | Function (String) String | `null` | filter function after markdown parse |

# Events

| Name | Param[Type] | Describe |
| ---- | --------- | -------- |
| rendered | outHtml[String] | dispatch when render finish |
| toc-rendered | tocHtml[String] | dispatch when TOC render finish, never dispatch if the toc[prop] is `false` |

# Container
Example:
```
::: danger
*here be dragons*
:::
```
Will give:
```html
<div class="danger" data-source-line="31">
<p><em>here be dragons</em></p>
</div>
```

Possible containers:
- warning
- info
- danger
- success
- to-left
- to-right
- centered
- justify

# Icons
```
A :fa-car: runs
```
A :fa-car: runs
# Thanks

- [markdown-it](https://github.com/markdown-it/markdown-it)
- [transtone](https://github.com/transtone)
- [**brandonferens**](https://github.com/brandonferens)

# Contributions

- [miaolz123](https://github.com/miaolz123)
- [brandonferens](https://github.com/brandonferens)
- [brianbancroft](https://github.com/brianbancroft)
- [nikolasp](https://github.com/nikolasp)
- [mbackonja](https://github.com/mbackonja)
- [Endi1](https://github.com/Endi1)
- [printscreen](https://github.com/printscreen)
- [killix](https://github.com/killix)
- [LeFnord](https://github.com/lefnord)
- [FlorianWendelborn](https://github.com/FlorianWendelborn)

# License

Copyright (c) 2016 [miaolz123](https://github.com/miaolz123) by [MIT](https://opensource.org/licenses/MIT)
