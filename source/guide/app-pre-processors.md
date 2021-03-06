title: App Pre-Processors
---
The boilerplate created with Quasar CLI has pre-configured CSS extraction for most popular CSS pre-processors including LESS, SASS, Stylus, and PostCSS. To use a pre-processor, all you need to do is installing the appropriate webpack loader for it. For example, to use SASS:

``` bash
$ npm install sass-loader node-sass --save-dev
```
Note you also need to install node-sass because sass-loader depends on it as a peer dependency.

## Using Pre-Processors inside Components

Once installed, you can use the pre-processors inside your `*.vue` components using the lang attribute on `<style>` tags:

``` html
<style lang="scss">
/* write SASS! */
</style>
```

### A note on SASS syntax

* lang="scss" corresponds to the CSS-superset syntax (with curly braces and semicolones).
* lang="sass" corresponds to the indentation-based syntax.

## PostCSS

Styles in `*.vue` files (and all other style files) are piped through PostCSS by default, so you don't need to use a specific loader for it.

For `*.vue` files you can simply add PostCSS plugins you want to use in `build/webpack.base.conf.js` under the vue block, and for the other files under postcss block:

``` js
module.exports = {
  // ...
  vue: {
    postcss: [/* your plugins */]
  },
  // ...
  postcss: []
}
```

By default, PostCSS is configured to use Autoprefixer.

Also, see [vue-loader's related documentation](http://vue-loader.vuejs.org/en/features/postcss.html) for more details.

## Standalone CSS Files

To ensure consistent extraction and processing it is recommended that you import global, standalone style files from your root component, for example:

``` html
<style src="./styles/global.less" lang="less"></style>
```

Note you should probably only do this for the styles written by yourself for your application. For existing libraries e.g. Bootstrap or Semantic UI, you can place them inside `src/statics/` and reference them directly in index.html. This avoids extra build time and also is better for browser caching. (See [Handling Static Assets](/guide/app-handling-static-assets.html)).
