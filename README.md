## Website Performance Optimization portfolio project
This is a project from a Udacity class to learn web site performance optimization.

## My Notes
Final PageSpeed Insights Score on index.html: Mobile: 95/100 Desktop: 97/100
Final Time to resize pizzas: 0.6430000066757202ms


I used the following resources to learn how to optimize HTML and JS:
Udacity's Website Performance Optimization class:
https://www.udacity.com/course/viewer#!/c-ud884-nd

Google's Optimizing Performance site:
https://developers.google.com/web/fundamentals/performance/

Stack Overflow, how to turn on the FPS counter in Chrome:
http://stackoverflow.com/questions/22038065/show-fps-meter-chrome-33

I made a separate commit for each change I made, so you can see them all in my commit history.

In order to improve the page load time of index.html I made the following changes:

Initial PageSpeed Insights score: Mobile 76/100 Desktop 89/100
1. Replaced the image profilepic.jpg with an optimized one from PageSpeed Insights.
New Score: Mobile: 76/100 Desktop: 90/100

2. Add the async attribute to the analytics.js script tag:
New Mobile Score: 77/100

3. Add media="print" attribute to the print.css link tag.
This decreased the critical load by one file, but did not increase my score.

4. Removed the Google font from index.html:
Before: DCL: 106ms, onload: 158ms
After: DCL: 36ms, onload: 90ms
The Google font added like 70ms to DCL!
New Score: Mobile: 87/100 Desktop: 94/100

5. Moved all CSS from style.css into index.html:
New Score: Mobile: 95/100 Desktop: 97/100
This is a controversial change, but for the sake of this exercise it did make a large increase on the score.
In some cases this may be a bad idea because now we have to load CSS again for other pages.
However, if the site is largely contained in one page this would be a good idea,
or if it is most important to load the first page quickly, and subsequent pages can be slower, this might be a good strategy.

6. Minified index.html reducing it by 918 bytes.
This did not increase my score, but it decreased the bytes to load by 918.

JavaScript Optimization:
I found a great disparity between the FPS, and load times on my two computers. My powerful desktop is able to load everything very fast no matter what. My laptop struggles even when the page is optimized.
I also found some of the numbers to differ radically between page loads.

Before starting:
Time to generate pizzas on load: 108.73300000093877ms
Time to generate pizzas on load: 168.74200000893325ms
Time to resize pizzas: 860.759999952279ms

1. Change repeat DOM selection in function changePizzaSizes(size) to a single call saved into a variable to avoid repeated DOM queries.
Little or no affect on load, but the time to resize pizzas was cut down a lot:
Time to resize pizzas: 632.876000017859ms

2. Change repeat DOM document.body.scrollTop selection in function updatePositions() for loop
from a repeat lookup to saving it before the loop and using the saved copy.
This has  large affect on Average time to generate last 10 frames:
BEFORE:
Average time to generate last 10 frames: 61.18579999929352ms
main.js:495 Average time to generate last 10 frames: 69.29589999999735ms
main.js:495 Average time to generate last 10 frames: 75.29450000038196ms
main.js:495 Average time to generate last 10 frames: 69.48929999925895ms
main.js:495 Average time to generate last 10 frames: 69.73529999922903ms
main.js:495 Average time to generate last 10 frames: 69.33739999985846ms

AFTER:
Average time to generate last 10 frames: 1.8269000000145752ms
main.js:495 Average time to generate last 10 frames: 1.4917000004061265ms
main.js:495 Average time to generate last 10 frames: 1.6325999997206964ms
main.js:495 Average time to generate last 10 frames: 1.173299998845323ms
main.js:495 Average time to generate last 10 frames: 1.3949000000138767ms

This was on my laptop. On my desktop the frames look like the provided image, loading in under 0.4ms

After the above two changes here are the times on my Desktop Computer:
Time to generate pizzas on load: 14.544000005116686ms
main.js:467 Time to resize pizzas: 133.7399999902118ms
main.js:495 Average time to generate last 10 frames: 1.2279999995371327ms
main.js:495 Average time to generate last 10 frames: 0.4456000024219975ms
main.js:495 Average time to generate last 10 frames: 0.5517000070540234ms
main.js:495 Average time to generate last 10 frames: 0.5674000101862475ms
main.js:495 Average time to generate last 10 frames: 0.4885999922407791ms
main.js:495 Average time to generate last 10 frames: 0.4192999971564859ms

3. Move var pizzasDiv outside of for loop.
Time to generate pizzas on load: 14.77899999008514ms
6main.js:467 Time to resize pizzas: 98.40600000461563ms
main.js:495 Average time to generate last 10 frames: 0.7552999944891781ms
main.js:495 Average time to generate last 10 frames: 0.46269999584183097ms
main.js:495 Average time to generate last 10 frames: 0.48130000359378755ms

4. Save document.querySelector("#movingPizzas1") to variable outside of for loop.
Time to generate pizzas on load: 15.42199999676086ms
4main.js:467 Time to resize pizzas: 95.78199998941272ms
main.js:495 Average time to generate last 10 frames: 0.6781000032788143ms
main.js:495 Average time to generate last 10 frames: 0.4438999923877418ms
main.js:495 Average time to generate last 10 frames: 0.44349999516271055ms
main.js:495 Average time to generate last 10 frames: 0.4288999974960461ms

5. Move pizza old and new size determination outside of for loop.
Time to generate pizzas on load: 11.522999993758276ms
6main.js:469 Time to resize pizzas: 0.6430000066757202ms
main.js:497 Average time to generate last 10 frames: 0.9732999984407797ms
main.js:497 Average time to generate last 10 frames: 0.4771000036271289ms
main.js:497 Average time to generate last 10 frames: 0.5089999991469085ms
main.js:497 Average time to generate last 10 frames: 0.4659000027459115ms
main.js:497 Average time to generate last 10 frames: 0.5137000058311969ms
main.js:497 Average time to generate last 10 frames: 0.516500003868714ms
THIS TOOK ABOUT 95ms OFF OF THE RESIZE PIZZA TIME!

## Original Insructions:

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository, inspect the code,

### Getting started

####Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

####Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js. 

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

### Sample Portfolios

Feeling uninspired by the portfolio? Here's a list of cool portfolios I found after a few minutes of Googling.

* <a href="http://www.reddit.com/r/webdev/comments/280qkr/would_anybody_like_to_post_their_portfolio_site/">A great discussion about portfolios on reddit</a>
* <a href="http://ianlunn.co.uk/">http://ianlunn.co.uk/</a>
* <a href="http://www.adhamdannaway.com/portfolio">http://www.adhamdannaway.com/portfolio</a>
* <a href="http://www.timboelaars.nl/">http://www.timboelaars.nl/</a>
* <a href="http://futoryan.prosite.com/">http://futoryan.prosite.com/</a>
* <a href="http://playonpixels.prosite.com/21591/projects">http://playonpixels.prosite.com/21591/projects</a>
* <a href="http://colintrenter.prosite.com/">http://colintrenter.prosite.com/</a>
* <a href="http://calebmorris.prosite.com/">http://calebmorris.prosite.com/</a>
* <a href="http://www.cullywright.com/">http://www.cullywright.com/</a>
* <a href="http://yourjustlucky.com/">http://yourjustlucky.com/</a>
* <a href="http://nicoledominguez.com/portfolio/">http://nicoledominguez.com/portfolio/</a>
* <a href="http://www.roxannecook.com/">http://www.roxannecook.com/</a>
* <a href="http://www.84colors.com/portfolio.html">http://www.84colors.com/portfolio.html</a>
