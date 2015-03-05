The optimized portfolio site is at http://vincegiorno.github.io/

The directory structure in this repository is a little complicated, because the index.html and associated directories/files have to be in the root to display properly, but they are all minimized. So the source files are in the src directory. The minimization was done using Gulp, so gulpfile.js, package.json and the node_modules directory are also in the root.

Optimization was achieved in several ways. To speed the initial loading time, I
<ul><li>used a @media attribute on the print.css link</li>
<li>replaced the webfonts call with @font-face CSS rules</li>
<li>made the analytics script async</li>
<li>resized pizzeria.jpg to 100px wide for the small front-page image (all annotated in src/index.html)</li>
<li>compressed all files, including image files, using Gulp plugins.</li></ul>


The optimizations for the pizzeria page, documented in the main.js file in the src/views/js directory, were
<ul><li>main pizzeria.jpg image resized to 360px wide (affects load time)</li>
<li>number of sliding pizzas reduced from 200 to 48 (8 rows x 6 columns) which is enough to keep the visible functionality on widescreen and mobile portrait displays (affects load time and scrolling fps)</li>
<li><em>getElementById</em> and <em>getElementsByClassName</em> were used in place of <em>querySelector</em> and <em>querySelectorAll</em>, respectively (affects load time, time to change pizza sizes and scrolling fps</li>
<li>calculations and assignments that only needed to be done once were moved outside of loops where they were being re-evaluated on each iteration. These include:
<ul><li><em>dx</em> and <em>newwidth</em> calculations in the <b>changePizzaSizes</b> function, where the value of <em>document.getElementsByClassName("randomPizzaContainer")</em> is also stored as a variable rather than re-evaluated for each step (affects time to change pizza sizes)</li>
<li><em>document.getElementById("randomPizzas")</em> is also evaluated and stored in a variable outside of the <em>for</em> loop that appends the random pizzas when the page loads (affects load time)</li>
<li>(<em>document.body.scrollTop</em> / 125) calculation moved outside the <em>for</em> loop in the <b>updatePositions</b> function (affects scrolling fps)</li></ul></ul>
