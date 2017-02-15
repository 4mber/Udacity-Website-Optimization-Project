## Website Performance Optimization Portfolio Project!

### Getting started:
1. Here's the demo!
1. To inspect the site on your phone, you can run a local server:

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely:

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights!

### OPTIMIZATIONS: index.html
- Inlined critical CSS to `<head>`, then moved nonessential CSS to 'styles.css' and linked to that separately at the bottom of `<body>`. Nonessential CSS moved to `styles.css`:
  + `b, strong { font-weight: bold; }`
  + `body { background: #fff; font-weight: 400; }`
  + `html { -ms-text-size-adjust: 100%; -webkit-text-size-adjust: none; -webkit-tap-highlight-color: rgba(0,0,0,0); }`
  + `a:hover, a:active { color: #c00; outline: 0; }`
  + `pre, code { font-family: monospace, monospace; font-size: 1em; }`
  + `img { border: 0; }`
  + `.content li { list-style-type: none; }`
  + styles for button,input,select,textarea, & ol
  + styles  for `a:focus, a:active, and a:hover`
  + media query for smartphones on landscape mode
  + all styles from 'print.css'
- Resized `pizzeria.jpg` into one thumbnail sized image, and one 720px image (for use in `pizza.html`), then optimized both with ImageOptim.
- Saved 3 main article images to be sourced from `img` that were previously linked to from an outside source, optimized images using ImageOptim, and changed html to reflect new sources. Then, removed inline style from `<img src="views/images/pizzeria.jpg">`, and added it to `<style>` in `<head>` applied to all 4 line item images.
- Changed all image types to `.jpg`.
- Optimized all images using ImageOptim (saved up to 89.4% per image).
- Removed render blocking Google Web Fonts, as it didn't seem to be adding much, and took 193.87ms to load.
- Added `async` attribute to both Google Analytics scripts in `<head>` and moved them to the bottom of `<body>` to keep them from parser blocking.
- Removed unnecessary `<a>` tag around profile pic that linked to nothing.
- Minified all HTML, JS and CSS files.


### OPTIMIZATIONS: views/js/main.js

- In the function `updatePositions()`:
  + Reworked according to {https://www.html5rocks.com/en/tutorials/speed/animations/}.
  + Decoupled scroll event from animation, and only used `requestAnimationFrame` when visual updates are necessary.
  + Moved `phase` out of for-loop and into its own array so that it only calculates the necessary 5 times (instead of the original 200).
  + Moved `document.body.scrollTop;` outside of for loop and into its own variable, `cachedScrolling`.
  + Replaced `.querySelectorAll()` with more efficient `.getElementsByClassName()`.
  + Replaced `style.left` with `transform: translateX()` to keep from triggering a layout.
- In the `pizzaElementGenerator` variable, changed `style.width` to more efficient `.classList.add("col-md-6”)`.
- In the function `changePizzaSizes()`:
  + Changed slider value to a percentage of width.
  + Replaced `.querySelectorAll()` with more efficient `.getElementsByClassName()`.
  + Improved for-loop.
- In the `DOMContentLoaded` event listener:
  + Used `cloneNode` to duplicate pizzas and append them after DOM has loaded to limit the number of pizzas created in the background to those that are actually visible.
  + Changed `className` to more efficient `classList.add` method.
- Moved var `pizzasDiv` outside of for loop.
- Inlined `styles.css` to bottom of `<body>` of `pizza.html`, and minified `pizza.html`
