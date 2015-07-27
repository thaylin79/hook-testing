#The New York Times Paid Post Scaffolding

## Why not use an existing scaffolding project (Yeoman, etc..)?
Paid Posts are treated as articles in the NYTimes.com ecosystem.  As a result, there are at least three major proprietary requirements for deployment and management:

* Managed by our internal CMS "Scoop"
* Rendered by our internal web framework "NYT5"
* Hosted in the NYTimes.com server ecosystem

All of the decisions in scaffolding are designed to allow maximum flexibility for development within the above constraints.

## Getting started
Scaffolding is a discrete starting point for a new Paid Post.  No installer is required. 

The simplest way to start a project is to clone, remove .git and git init:

    git clone https://githubfdasfds.com/nytpi/scaffolding.git <your projectname>
    cd <your projectname>
    rm -rf .git
    git init
    git remote add origin <your repo>
    git add .
    git commit -m"Initial Commit"
    git push origin master
    npm install
fsafdsafdsafd
gffds


This same effect can also be accomplished through a variety of other means.

## Working with the Scaffolding
> Below is an overview of how to develop Paid Posts from this scaffolding.  Please reach out early an often to NYTimes developers with any questions, concerns or if you would like any explanations to why things are the way they are.

### Building 
Paid Posts are built using Grunt.  To get started, go to your project folder and run

    grunt watch

You can see which files are watched in Gruntfile.js.  It's set up by default to watch for any relevant js and html changes, but you may need to add other paths/files if you choose to use files/directories outside of our conventions.

Feel free to add any other libraries you'd like to use to the build process, such as js/css precompilers, templating engines, etc...

### Previewing
Grunt builds a local development version of the Paid Post into the index.html file in the rood of the folder structure, so simply aim your browser at the directory and you should see what you will get.

### Updating HTML
All html updates need to happen in the /htmlComponents/body.html file and should exist between <main> tags:

    <main> ... your code goes here ...</main>
    
If you are running grunt watch, each update will be built into index.html on save.

Template preprocessors can be used here.  For example, you could create a main.hbs file that gets built by grunt into the main.html file early in the build process.

### Working with JS
Scaffolding concatinates all code into a require block in order to insulate it from the javascript at play in the greater NYT5 application.  

Look at the concat section of Gruntfile.js to see how it concatinates.  Fee free to update this files/folders to make sure your code is put together like this:

    /js/src/head.js 
    ... all of your js files 
    /js/src/tail.js.  

Open up head.js and notice that all this happens within a require context.  Feel free to add any libraries or other depenencies into this require context.

> Note: Please only use require to include libraries and make sure your code is concatinated into the app-build file.  This will greatly aid us during the deployment process.

### Working with CSS
Scaffolding ships with a simple css file in the /styles/ directory.  Note that the css file is versioned and that version is controlled in the top of Gruntfile.js.  If you want to precompile css, make sure to set your precompiler's filename to the name of the current file.

## Delivery
Paid Posts should be delivered to us via a public repo (aka, github.com).  

### Assets
All assets except videos should be included in the repo.  

Videos are to be zipped up and posted somewhere we can download them.  Please ensure the link remains live up to the launch date of the project. 

If video compression is part of your deal, all videos should be compressed into three sizes:
* Web mp4 720p (for laptop/desktops not Firefox)
* Web webm 720p (for Firefox)
* Mobile mp4 360p 

VHS Video elements included in code must include a name and type. This is for tracking purposes and SHOULD NOT be ignored.
Example:
```
"name": "PaidPost | Toyota | mothers-of-invention | Impact",
"type": "PaidPost"...
```
Or just insert replacement variables to not only worry about the video name
```
"name": "PaidPost | ---client--- | ---projectname--- | Impact",
"type": "PaidPost",
```
For reference see [htmlComponents/body.html](htmlComponents/body.html). 

Compression is as much art as science.  Care should be taken to find the smallest filesize that does not result in video or audio deterioration.  When in doubt, send samples to us for approval.

## An Explanation of the Breakpoint system:
If you inspect one of our pages, you'll notice that the <HTML> tag has an unusual number of classes  assigned to it. Among them are classes with names like "viewport-medium-10", and "viewport-small".

These are created by a piece of JavaScript monitors the page width, and adds additional classes for each successive breakpoint class the viewport is wider than. For example:
A viewport with a width of 720px result in this:
<html class="viewport-small viewport-small-10 viewport-small-20 viewport-medium">
while a viewport with a width of only 320px would result in:
<html class="viewport-small">
This is done so that we can code responsively, mobile-first by having more specific selectors for each of our breakpoints. for example,
.myDiv{
  height:10px;
  width:200px;
}
 
would display a 200px-wide div. If we we want .myDiv to be larger on wider screens, we would add:
.viewport-medium .myDiv{
  height:10px;
  width:500px;
}
Because only devices with viewports 720px and above have the class .viewport-medium, .myDiv will only take this style on those devices. Here's a complete list of our breakpoints:

```
var breakpoints = [
        {key: 'viewport-small' , val: 315},
        {key: 'viewport-small-10' , val: 450},
        {key: 'viewport-small-20' , val: 600},
        {key: 'viewport-medium' , val: 720},
        {key: 'viewport-medium-10', val: 765}, //This is the minimum width at which the "ribbon" of suggested NYT stories appears across the top of the page.
        {key: 'viewport-medium-20', val: 855},
        {key: 'viewport-medium-30', val: 960},
        {key: 'viewport-medium-31', val: 975},
        {key: 'viewport-medium-40', val: 1005},
        {key: 'viewport-medium-50', val: 1020},
        {key: 'viewport-medium-60', val: 1050},
        {key: 'viewport-large' , val: 1080},
        {key: 'viewport-large-10' , val: 1125},
        {key: 'viewport-large-11' , val: 1155},
        {key: 'viewport-large-20' , val: 1200},
        {key: 'viewport-large-21' , val: 1215},
        {key: 'viewport-large-30' , val: 1245},
        {key: 'viewport-large-40' , val: 1280},
        {key: 'viewport-large-41' , val: 1335},
        {key: 'viewport-large-50' , val: 1375},
        {key: 'viewport-large-51' , val: 1410},
        {key: 'viewport-large-60' , val: 1607},
        {key: 'viewport-large-70' , val: 1650},
        {key: 'viewport-large-80' , val: 2030}
    ];

```

## Thanks!  
Ad Platform Innovations
