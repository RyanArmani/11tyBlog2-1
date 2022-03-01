# 🕛 Twelvety

[See the demo site](https://twelvety.netlify.app)

Twelvety is a pre-configured Eleventy starter project built to be fast. It includes:

## Docker Introduction
Docker is an extraordinarily popular open source containerization platform among developers. Docker enables developers to develop, ship, and run applications through its implementation of containers. Containers are a piece of software that packages up any code and its dependencies, enabling applications to run on various computing environments regardless of differences between system requirements from one computer to another. This popular method of running and delivering apps opens a world of possibilities, with a common use being businesses rolling out updates to existing software, and reverting back to older stages of a software if any errors arise.

## Starting with Docker
Docker utilizes a special file called a Dockerfile. a Dockerfile is a file that automatically runs a set amount of code within an application to assemble an image (an image is a set of code that creates a container within docker). One such example of a Dockerfile is included below, which is used to run the NewsAPI app from our class' project. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vcjtivtzet4d3or69bwr.png)An example of a fully functional application, the NewsAPI, is included below as well to demonstrate the full capabilities of docker. This includes a series of links to news articles 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bi0bu1pf2jqsnkvym7fh.png) One can utilize a query to find specific key terms 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/18v62me8an1gqux2qegs.png) 



## Create a docker file
To create a docker file for your own web app, you will need to clone a copy of your git repository (repo). One way to acquire the link to your repo is by navigating to your repo on github.com. Using my own repo as an example, navigate to the `Code` tab
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b56b1wd5lqrusw3dn7ve.png), and select the `https` icon. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qbdxuh8dcraoi34pm3af.png)You will see a link to your repo. Copy this link, as we will be utilizing it in the docker environment. Navigate to "play with docker" (https://www.docker.com/play-with-docker), and scroll down until you find the "Lab Environment" tab. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sy4j3rrh8qipg8agaq01.png)Select "Get Started, and sign into Docker if prompted. Once signed in, select the "Start" button. You are now ready to set up your web app!

Inside the docker playground, on the left hand side of the screen, click the "+ Add New Instance" option. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1cc0m1sybis0bbi3ga77.png)In a moment, you should see a terminal-like sandbox environment appear in docker playground. We can input commands here! For our purposes, we will clone our git repo. Use the command `git clone <your-repo-link-here>`. For my web app, I used the command `git clone https://github.com/IST402GroupB/ip-project.git`. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t6vzwfjau2v316xywdi9.png)We will now create a temporary file within our web app. Type in the command touch dockerfile. This command creates an image of a file within docker named dockerfile, which is a file that can be edited within the Docker Editor provided, and can be viewed by the `ls -la` command. 

Write components like this:

```html
<main class="home">
  <h1 class="home__title">Twelvety</h1>
</main>

{% stylesheet 'scss' %}
  @import "mixins";

  .home {
    @include container;

    &__title {
      color: red;
    }
  }
{% endstylesheet %}

{% javascript %}
  console.log("Super fast 💨");
{% endjavascript %}
```

## Deploy to netlify

To quickly deploy your own instance of Twelvety to netlify, just click the button below and follow the instructions.

[![Deploy to netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/gregives/twelvety)

**What will happen when I click this button?** Netlify will clone the Twelvety git repository to your GitHub account (it will ask your permission to do this), add the new repository to your netlify account and deploy it!

## Run Locally

Click the <kbd>Use this template</kbd> button at the top of this repository to make your own Twelvety repository in your GitHub account. Clone or download your new Twelvety repository onto your computer.

You'll need [Node.js](https://nodejs.org) and npm (included with Node.js). To install the required packages, run

```sh
npm install
```

### Commands

- Run `npm run serve` to run a development server and live-reload
- Run `npm run build` to build for production
- Run `npm run clean` to clean the output folder and Twelvety cache

The brains of Twelvety live in the `utils` folder: if you just want to make a website, then you don't need to touch anything inside `utils`. However, if you want to change any of the shortcodes, have a look around!

## Features

Twelvety sets up transforms, shortcodes and some sensible Eleventy options. Click the features below to learn how they work.

<details>
<summary><strong><code>stylesheet</code> paired shortcode</strong></summary>
<br>

Use the `stylesheet` paired shortcode to include your Sass. You can import Sass files from your `styles` directory (defined in `.twelvety.js`) and from `node_modules`. The Sass will be rendered using [dart-sass](https://github.com/sass/dart-sass#javascript-api), passed into [PostCSS](https://github.com/postcss/postcss) (with [PostCSS Preset Env](https://github.com/csstools/postcss-preset-env) and [Autoprefixer](https://github.com/postcss/autoprefixer) for compatibility) and either minified using [clean-css](https://github.com/jakubpawlowicz/clean-css) or beautified by [JS Beautifier](https://github.com/beautify-web/js-beautify) (in production and development respectively).

```html
{% stylesheet 'scss' %}
  @import "normalize.css/normalize";
  @import "mixins";

  .home {
    @include container;

    color: $color--red;
  }
{% endstylesheet %}
```

The second parameter of the `stylesheet` paired shortcode is the language; currently, this does nothing and is included solely to align with Shopify's definition of the shortcode. If you want to use Sass **indented syntax**, you can change the `indentedSass` Twelvety option, found in `.twelvety.js`.

The `stylesheet` paired shortcode also has a third parameter, which by default is set to `page.url`, the URL of the current page being rendered. This means that only the required CSS is included in each page. You can make your own 'chunk' of CSS using this parameter, for example, a CSS file common to all pages of your website.

___

</details>

<details>
<summary><strong><code>styles</code> shortcode</strong></summary>
<br>

The `styles` shortcode collects together all Sass written in `stylesheet` paired shortcodes for the given chunk and outputs the rendered CSS. The 'chunk' defaults to `page.url`, the URL of the current page being rendered.

```html
<!-- Inline all styles on current page -->
<style>
  {% styles page.url %}
</style>

<!-- Capture styles on current page -->
{% capture css %}
  {% styles page.url %}
{% endcapture %}
<!-- And output asset using `asset` shortcode -->
<link rel="stylesheet" href="{% asset css, 'css' %}" />
```

Note that the `styles` shortcode must be placed below any `stylesheet` paired shortcodes in the template; see the `append` paired shortcode and transform for more information.

___

</details>

<details>
<summary><strong><code>javascript</code> paired shortcode</strong></summary>
<br>

Include your JavaScript using the `javascript` paired shortcode. Twelvety uses [Browserify](http://browserify.org) so that you can `require('modules')` and [Babel](https://babeljs.io) so you can use the latest JavaScript. Your JavaScript will then be minified using [Uglify](https://github.com/mishoo/UglifyJS) in production or beautified by [JS Beautifier](https://github.com/beautify-web/js-beautify) in development.

```html
{% javascript %}
  const axios = require("axios");

  axios.get("/api/endpoint")
    .then((response) => {
      console.log("Yay, it worked!");
    })
    .catch((error) => {
      console.log("Uh oh, something went wrong");
    });
{% endjavascript %}
```

The `javascript` paired shortcode has a second parameter, which by default is set to `page.url`, the URL of the current page being rendered. This means that only the required JavaScript is included in each page. You can make your own 'chunk' of JavaScript using this parameter, for example, a JavaScript file for all vendor code.

The output of each `javascript` paired shortcode will be wrapped in an [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) so that your variables do not pollute global scope. If you want to define something on `window`, use `window.something =`.

___

</details>

<details>
<summary><strong><code>script</code> shortcode</strong></summary>
<br>

The `script` shortcode collects together all the JavaScript for the given chunk and outputs the JavaScript (after transpilation and minification). The 'chunk' defaults to `page.url`, the URL of the current page being rendered.

```html
<!-- Inline all JavaScript on current page -->
<script>
  {% script page.url %}
</script>

<!-- Capture JavaScript on current page -->
{% capture js -%}
  {% script page.url %}
{%- endcapture -%}
<!-- And output asset using `asset` shortcode -->
<script src="{% asset js, 'js' %}" defer></script>
```

Note that the `script` shortcode must be placed below any `javascript` paired shortcodes in the template; usually this is not a problem as JavaScript is often included immediately preceding `</body>`. If you want the JavaScript somewhere else, see the `append` paired shortcode and transform.

___

</details>

<details>
<summary><strong><code>asset</code> shortcode</strong></summary>
<br>

The `asset` shortcode outputs a content-hashed asset with the given content and extension. The content may be either a `String` or `Buffer`. Assets will be saved to the `assets` directory inside the `output` directory (both defined within `.twelvety.js`).

```html
<!-- Capture some content -->
{% capture css %}
h1 {
  color: red;
}
{% endcapture %}

<!-- Save content to content-hashed file with .css extension -->
<link rel="stylesheet" href="{% asset css, 'css' %}" />

<!-- Output of shortcode -->
<link rel="stylesheet" href="/_assets/58f4b924.css" />
```

You can import the `asset` shortcode function in JavaScript: this is how the `picture` shortcode saves your responsive images into the `assets` directory.

___

</details>

<details>
<summary><strong><code>picture</code> shortcode</strong></summary>
<br>

The `picture` shortcode takes `src` and `alt` parameters and outputs a responsive picture element with AVIF* and WebP support. Your images must be stored within the `images` directory, defined within `.twelvety.js`. Twelvety will save the outputted images to the `assets` directory inside the `output` directory (both defined within `.twelvety.js`). The `picture` shortcode also takes two other parameters: `sizes` which defaults to `90vw, (min-width: 1280px) 1152px`, based upon the breakpoint sizes; and `loading` which defaults to `lazy`, can also be `eager`.

*AVIF is disabled by default due to long build times. You can enable it in `.twelvety.js`.

```html
<!-- Picture shortcode with src, alt, sizes and loading -->
{% picture 'car.jpg', 'Panning photo of grey coupe on road', '90vw', 'eager' %}

<!-- Absolute paths also work -->
{% picture '/src/_assets/images/car.jpg', 'Panning photo of grey coupe on road', '90vw', 'eager' %}

<!-- Output of shortcode -->
<picture style="background-color:rgb(38%,28%,26%);padding-bottom:50%">
  <source srcset="/_assets/2263c1d0.avif 320w,/_assets/519fcdec.avif 640w,/_assets/b59349f7.avif 960w,/_assets/e8dae22f.avif 1280w,/_assets/4ba755ff.avif 1600w,/_assets/87c06dd1.avif 1920w" sizes="90vw" type="image/avif">
  <source srcset="/_assets/0e7cdd2f.webp 320w,/_assets/ba4e43dd.webp 640w,/_assets/bc541ea5.webp 960w,/_assets/6d620165.webp 1280w,/_assets/756857ea.webp 1600w,/_assets/483e9c95.webp 1920w" sizes="90vw" type="image/webp">
  <source srcset="/_assets/6a3b0321.jpeg 320w,/_assets/2bf90b83.jpeg 640w,/_assets/4a810813.jpeg 960w,/_assets/601b629c.jpeg 1280w,/_assets/c39ac58c.jpeg 1600w,/_assets/25a2b530.jpeg 1920w" sizes="90vw" type="image/jpeg">
  <img src="/_assets/25a2b530.jpeg" alt="Panning photo of grey coupe on road" width="2400" height="1200" loading="lazy">
</picture>
```

The `picture` shortcode uses native lazy-loading but it would be easy to add support for `lazysizes` or a similar library if you wished. The `picture` shortcode calculates the average colour of the image to show while the image loads, using `padding-bottom` to avoid layout shift.

The `picture` shortcode is automatically used for every image in Markdown. To disable this, you'll need to edit the instance of markdown-it (see Markdown feature).

```md
<!-- Automatically uses picture shortcode -->
![Panning photo of grey coupe on road](car.jpg)
```

**The images outputted by the `picture` shortcode are cached.** If you want to clear the cache, delete `.twelvety.cache` (just a JSON file) or run `npm run clean` to delete the cache and the output directory. If you delete the output directory but `.twelvety.cache`, things will break.

___

</details>

<details>
<summary><strong><code>append</code> paired shortcode and transform</strong></summary>
<br>

Okay folks, here it is: the one _gotcha_ with Twelvety. In order for the `styles` shortcode to work, it must come after all `stylesheet` paired shortcodes, which would usually be in the `body`. However, we want our CSS to be linked or inlined in the `head`. This is where the `append` paired shortcode and transform come in, to move the output of the `styles` shortcode back into the `head` where we want it.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Everything in append paired shortcode will be moved here -->
  </head>
  <body>
    <!-- Stylesheet paired shortcodes can go here -->
    ...
    <!-- Append paired shortcode with styles inside -->
    {% append 'head' %}
      <style>
        {% styles page.url %}
      </style>
    {% endappend %}
  </body>
</html>
```

The `append` paired shortcode will actually be replaced with a `template`. The `append` transform then uses [jsdom](https://github.com/jsdom/jsdom) to append the contents of the `template` to the given selector (in this case, `head`).

The same problem exists for the `script` shortcode, however, this is not such a problem because it's very common to include JavaScript from the bottom of `body` anyway.

___

</details>

<details>
<summary><strong><code>markdown</code> paired shortcode and configuration</strong></summary>
<br>

Twelvety sets its own instance of markdown-it. The configuration options are:

```js
{
  html: true,
  breaks: true,
  typographer: true
}
```

Twelvety also modifies the `image` rule of the renderer: instead of outputting an `img` element, Twelvety uses the responsive `picture` shortcode to render each image. If you want to disable this, remove the following lines in `utils/markdown.js`.

```js
md.renderer.rules.image = function (tokens, index) {
  const token = tokens[index];
  const src = token.attrs[token.attrIndex("src")][1];
  const alt = token.content;
  return pictureShortcode(src, alt);
};
```

Twelvety also adds a `markdown` paired shortcode which uses the markdown-it configuration.

```html
{% markdown %}
# `markdown` paired shortcode

Lets you use **Markdown** like _this_.
{% endmarkdown %}
```

This is also really useful for including Markdown files into a template.

```html
{% markdown %}
  {%- include 'content.md' -%}
{% endmarkdown %}
```

Be careful of the [common pitfall of indented code blocks](https://www.11ty.dev/docs/languages/markdown/#there-are-extra-and-in-my-output) when using the `markdown` paired shortcode. If indented code blocks are becoming a nuisance, you can disable them in `utils/markdown.js` whilst retaining fenced code blocks.

```diff
   // Uncomment the following line to disable indented code blocks
-  // .disable("code")
+  .disable("code")
```

___

</details>

<details>
<summary><strong><code>critical</code> transform</strong></summary>
<br>

Instead of using a transform, Twelvety now uses [eleventy-critical-css](https://github.com/gregives/eleventy-critical-css) to extract and inline critical-path CSS on every page.

___

</details>

<details>
<summary><strong><code>format</code> transform</strong></summary>
<br>

The `format` transform beautifies HTML in development using [JS Beautifier](https://github.com/beautify-web/js-beautify) and minifies HTML in production using [HTMLMinifier](https://github.com/kangax/html-minifier). Any inline CSS and JavaScript will also be beautified or minified.

___

</details>

## Visual Studio Code

If you're using Visual Studio Code I recommend this [Liquid extension](https://github.com/panoply/vscode-liquid) so that your Sass and JavaScript will be highlighted correctly.
