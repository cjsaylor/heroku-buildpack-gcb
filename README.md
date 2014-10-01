## Heroku buildpack: Node.js with grunt support
============================================

Supported Grunt versions: 0.3 and 0.4.
See the Grunt [migration guide](https://github.com/gruntjs/grunt/wiki/Upgrading-from-0.3-to-0.4) if you are upgrading from 0.3.

This is a fork of [Heroku's official Node.js buildpack](https://github.com/heroku/heroku-buildpack-nodejs) with support for [Grunt](http://gruntjs.com/), [Compass](http://compass-style.org/), and [Bower](http://bower.io/). This buildpack could be modified for specific needs of projects that I am working on, so please fork for stability.

This buildpack also assumes you are using [Heroku buildpack multi](https://github.com/ddollar/heroku-buildpack-multi).

Compass will install, and if available, grunt and bower will run installations.

Usage
-----

Create a new app with this buildpack:

    heroku create myapp --buildpack heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git

Or add this buildpack to your current app:

    heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git
    
Or change the buildpack for a specific app:

    heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git --app APP_NAME

Create your Node.js app and add a Gruntfile named `gruntfile.js` with a `heroku` task:

    grunt.registerTask('heroku', 'clean less mincss');

Create a `.buildpacks` file and add the following (or add to it):

    https://github.com/heroku/heroku-buildpack-nodejs.git
    https://github.com/cjsaylor/heroku-buildpack-grunt-compass-bower.git


Don't forget to add grunt to your dependencies in `package.json`. If your grunt tasks depend on other pre-defined tasks make sure to add these dependencies as well:

    "devDependencies": {
        ...
        "grunt": "*",
        "grunt-contrib": "*",
    }

Push to heroku

    git push heroku master
    ...
    -----> Heroku receiving push
    -----> Fetching custom buildpack... done
    -----> Node.js app detected
    -----> Resolving engine versions
           Using Node.js version: 0.8.2
           Using npm version: 1.1.41
    -----> Fetching Node.js binaries
    -----> Vendoring node into slug
    -----> Installing dependencies with npm
           ...
           Dependencies installed
    -----> Building runtime environment
    -----> Found gruntfile, running grunt heroku task
    Running "heroku" task
    ...
    -----> Discovering process types

Further Information
-------------------

[Heroku: Buildpacks](https://devcenter.heroku.com/articles/buildpacks)

[Heroku: Getting Started with Node.js](https://devcenter.heroku.com/articles/nodejs)

[Buildpacks: Heroku for Everything](http://blog.heroku.com/archives/2012/7/17/buildpacks/)

[Grunt: a task-based command line build tool for JavaScript projects](http://gruntjs.com/)
