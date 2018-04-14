
News Aggregator
===============================
-----------
## Description

This is a project from the Udacity Front-End Web Developer nanodegree.  This project focused on optimizing an existing web site, and using debugging skills. There are many known bugs in the existing site that need to be fixed in order to make the site run faster and smoother. This repo represents my submission to the project.

-----------
## How to Load the website

You can load the website in two ways:
1. From this GitHub pages - open the [website](https://bschwarz.github.io/news-aggregator/dist/).
2. Download the [repo](https://github.com/bschwarz/news-aggregator) locally - You can either download a zip file from the repo or you can clone the repo onto your local machine. Once downloaded onto your local machine, you can do one of two things to view:
-- Open the *dist/index.html* file that is in the root directory of the repo, with a browser (i.e. Chrome, Firefox).
-- Host the files through a local web server, and use your browser to navigate to the local web server. For example, if you have python installed, you can run this command within the *dist/* of the repo directory to serve the files: 

      ```
      python -m SimpleHTTPServer 8080 # assuming port 8080 is not used already.
      ```

   Then you can navigate your browser to *localhost:8080/*

-------------

## Optimizations
### Page Rendering and Painting
-	The original app created a story details widget for each story when clicked. So, I changed that so that there was only one widget, which got updated with the active story when clicked. This reduced the number of DOM elements significantly, and excess layers.
-	Layers (via ```will-change```) were being created for individual elements of the story details widget. I removed the CSS for any children of the story details, and only kept it for the main story details element. This reduced the number of layers.
-	Wrapped the ```loadStoryBatch``` function with a ```requestAnimationFrame```, to make sure the visuals were being painted at the correct time.
-	re-factored the ```colorizeAndScaleStories``` function to optimize it, by separating the reading and writing into separate batches, reduced calculations, and reduced the number of stories being work on at one time (only visible items).
-	Removed the loop in ```onStoryData```, since the element can be queried directly, without the looping.
-	Used CSS transform, instead of javascript for the story details animation.

### Page Loading
-   Minified CSS with ```htmlmin``` to reduce file size
-   Minified JS with ```uglify-js``` to reduce file size
-   Inlined CSS to avoid another round trip with ```inline-source```
-   Inlined javascript files ```namespace.js```, ```app.js``` and ```data.js``` to avoid another round trip with ```inline-source```

### Page Speed Insights Results:

[Page Speed Insight analysis](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fbschwarz.github.io%2Fnews-aggregator%2Fdist%2F&tab=mobile) 

### Chrome DevTools Audit (Lighthouse)
Received a performance score of 89 (good)

### General Observations
From Chrome DevTools Performance tab, you can visually see a huge difference between the old and new for both page loading, scrolling and story detail animation. FPS generally average almost double improvement.

<table>
	 <caption align="center"><b>Optimization Summary<b></caption>
  <tr>
    <th colspan="2">Page Speed Mobile</th>
    <th colspan="2">Page Speed Desktop</th>
    <th colspan="2">Chrome Perf Audit</th>
  </tr>
  <tr>
    <td>Original</td>
    <td>Optimized</td>
    <td>Original</td>
    <td>Optimized</td>
    <td>Original</td>
    <td>Optimized</td>
  </tr>
  <tr>
    <td>65</td>
    <td>78</td>
    <td>85</td>
    <td>88</td>
    <td>62</td>
    <td>89</td>
  </tr>
</table>

-------
## Build Automation
Used Gulp to automate the building and common tasks of the website. Includes the following:
- minification of javascript using ```uglify```
- minification of HTML and CSS using ```htmlmin```
- inlining CSS using ```inline source```
- Javascript linting using ```jshint```
- CSS linting using ```csslint```
- moves all assets under the ```dist/``` directory

Gulp dependencies are in the ```package.json``` file

You need to install [nodejs/npm](https://www.npmjs.com/get-npm) and [gulp](https://gulpjs.com/) first.

To generate distribution, run the following in the root directory of the repo

Install Dependencies
```
npm install
```

Generate Distribution
```
gulp main
```
You can run individual tasks by replacing ```main``` with either ```html```, ```csslint```,```js``` or ```img```
The resulting files for distribution will be in the ```dist/``` directory

-------
## Resources
+ [Google Page Speed Insights](https://developers.google.com/speed/pagespeed/insights/) - tool to measure web page performance
+ [convert](https://www.imagemagick.org/script/convert.php) - CLI tool to resize and optimize images
+ [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks)
+ [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/)
+ [gulp](https://gulpjs.com/) - build/task tool to automate common tasks (i.e. minifications, inlining)
+ [gulp-htmlmin](https://github.com/jonschlinkert/gulp-htmlmin) - tool to minimize the HTML and CSS
+ [gulp-uglify](https://www.npmjs.com/package/gulp-uglify) - tool to minimize the Javascript files
+ [gulp-inline-source](https://www.npmjs.com/package/gulp-inline-source) - Tools to inline CSS into the HTML page from gulp
+ [gulp-csslint](https://www.npmjs.com/package/gulp-csslint) - tool to check syntax of CSS from Gulp
+ [gulp-jshint](https://www.npmjs.com/package/gulp-jshint) - tool to check syntax of javascript files from Gulp


-------
## License

This project is licensed under the terms of the MIT license. (See LICENSE.md)

Copyright (c) 2018 Brett Schwarz