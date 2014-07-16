# critical [![Build Status](https://travis-ci.org/addyosmani/critical.svg?branch=master)](https://travis-ci.org/addyosmani/critical)

![](http://i.imgur.com/lAzmBD2.png)

Critical extracts & inlines critical-path (above-the-fold) CSS from HTML

## Install

```sh
$ npm install --save critical
```

## Usage

Include:

```js
var critical = require('critical');
```

### Generate and inline critical-path CSS

```js
critical.generateInline({
    base: 'dist/', // Your base directory
    src: 'index.html', // HTML source
    htmlTarget: 'index-critical.html', // Target for final HTML output
    styleTarget: 'styles/main.css', // Target for generated critical-path CSS (which we inline)
    width: 320, // Viewport width
    height: 480, // Viewport height
    minify: true // Minify critical-path CSS when inlining
});
```

### Generate critical-path CSS

Basic usage:

```js
critical.generate({
    base: 'test/',
    src: 'index.html',
    dest: 'styles/main.css',
    width: 320,
    height: 480
});
```

Generate and minify critical-path CSS:

```js
critical.generate({
    base: 'test/',
    src: 'index.html',
    dest: 'styles/styles.min.css',
    minify: true,
    width: 320,
    height: 480
});
```

Generate and return output via a callback:

```js
critical.generate({
    base: 'test/',
    src: 'index.html',
    width: 320,
    height: 480
}, function (err, output) {
    // You now have critical-path CSS
    // Works with and without dest specified
});
```

### Inline `<style>` / critical CSS from generation

Basic usage:

```js
critical.inline({
    base: 'test/',
    src: 'index-critical.html',
    dest: 'inlined.html'
});
```

Minify and inline stylesheets:

```js
critical.inline({
    base: 'test/',
    src: 'index-critical.html',
    dest: 'inlined-minified.html',
    minify: true
});
```

Inline and return output via a callback:

```js
critical.inline({
    base: 'test/',
    src: 'index-critical.html'
}, function (err, output){
    // You now have HTML with inlined critical-path CSS
    // Works with and without dest specified
});
```

### Options

| Name          | Type          | Description   |
| ------------- | ------------- | ------------- |
| base          | `string`      | Base directory in which the source and destination are to be written |
| src           | `string`      | Location of the HTML source to be operated against |
| dest          | `string`      | Location of where to save the output of an operation |
| width         | `integer`     | (Generation only) Width of the target viewport |
| height        | `integer`     | (Generation only) Height of the target viewport |
| minify        | `boolean`     | Enable minification of CSS output |
| styleTarget   | `string`      | (`generateInline` only) Destination for critical-path styles |
| htmlTarget    | `string`      | (`generateInline` only) Destination for (critical-path CSS) style-inlined HTML |


## Why?

### Why is critical-path CSS important?

> CSS is required to construct the render tree for your pages and JavaScript
will often block on CSS during initial construction of the page.
You should ensure that any non-essential CSS is marked as non-critical
(e.g. print and other media queries), and that the amount of critical CSS
and the time to deliver it is as small as possible.

### Why should critical-path CSS be inlined?

> For best performance, you may want to consider inlining the critical CSS
directly into the HTML document. This eliminates additional roundtrips
in the critical path and if done correctly can be used to deliver a
“one roundtrip” critical path length where only the HTML is a blocking resource.


## FAQ

### Are there any sample projects available using Critical?

Why, yes!. Take a look at [this](https://github.com/addyosmani/critical-path-css-demo) Gulp project
which demonstrates using Critical to generate and inline critical-path CSS. It also includes a mini-tutorial
that walks through how to use it in a simple webapp.

### When should I just use Penthouse directly?

I recommend using [Penthouse](https://github.com/pocketjoso/penthouse) directly if your app has a large number of styles
or stylesheets being dynamically injected into the DOM. Critical is best used
when your page uses a fixed set of stylesheets as we can automatically scrape
this for you, avoiding the overhead of passing known styles yourself manually to Penthouse.

### What other alternatives to Critical are available?

FilamentGroup maintain a [criticalCSS](https://github.com/filamentgroup/criticalCSS) node module, which
similar to [Penthouse](https://github.com/pocketjoso/penthouse) will find and output the critical-path CSS for
your pages.

### Is Critical stable and suitable for production use?

Many of the current tools around critical-path CSS are in an experimental stage and are constantly striving
to improve. The same could be said of Critical. It hasn't been extensively tested on a ton of sites and it's
very possible something may well break. That said, we welcome you to try it out on your project and report
bugs if you find them.

## Can I contribute?

Of course. We appreciate all of our [contributors](https://github.com/addyosmani/critical/graphs/contributors) and
welcome contributions to improve the project further. If you're uncertain whether an addition should be made, feel
free to open up an issue and we can discuss it.
