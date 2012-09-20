Automatically run mocha specs either *client-side* via grunt/mocha/PhantomJS, or with a straight-up node.js mocha runner.

# grunt-mocha

This plugin builds on the work from following projects:

   * [Grunt](https://github.com/cowboy/grunt)
   * [PhantomJS](http://phantomjs.org/)
   * [grunt-simple-mocha](https://github.com/yaymukund/grunt-simple-mocha)
   * (package/README format heavily borrowed from [grunt-jasmine-task](hhttps://github.com/creynders/grunt-jasmine-task) and builtin QUnit task)

## Getting Started

**Important note**

If you are not using AMD, include `mocha-helper.js` from `tasks/mocha` after you include `mocha.js` and run `mocha.setup`. The helper will override `mocha.setup` if it detects PhantomJS.

See the example folder for a vanilla example.

Example setup with AMD (advanced): https://gist.github.com/2655876

### Grunt and this plugin

First, make sure you have grunt installed globally, `npm install grunt -g`

Install this grunt plugin next to your project's [grunt.js gruntfile](https://github.com/cowboy/grunt/blob/master/docs/getting_started.md) with: `npm install grunt-mocha`

Then add this line to your project's `grunt.js` gruntfile at the bottom:

```javascript
grunt.loadNpmTasks('grunt-mocha');
```

Also add this to the ```grunt.initConfig``` object in the same file:

```javascript
mocha: {
  index: ['specs/index.html']
},
```

The plugin will automatically detect if the list of files contains html files, and will run the tests with phantomJS if any are found. Replace ```specs/index.html``` with the location of your mocha spec running html file.

Otherwise the task will run the tests in straight-up node.js mocha runner. Example configuration:

```javascript
js: ['js/**/*.js', 'test/unit/**/*.js'],
unit: {
    src: [ 'js/**/*.js', 'test/unit/**/*.js' ],
    // or you can specifically define a multi-task to be run as unit test
    type: 'unit',
    // you can pass any of the usual options from grunt-simple-mocha
    options: {
        reporter: 'nyan'
    }
}
```

Now you can run the mocha task with `grunt mocha`, but it won't work. That's because you need...

### PhantomJS

This task is for running Mocha tests in a headless browser, PhantomJS. [See the FAQ on how to install PhantomJS](https://github.com/cowboy/grunt/blob/master/docs/faq.md#why-does-grunt-complain-that-phantomjs-isnt-installed).

### Mocha

Use [Mocha](http://visionmedia.github.com/mocha/)

If you are not using AMD, include `mocha-helper.js` from `tasks/mocha` after you include `mocha.js` and run `mocha.setup`. The helper will override `mocha.setup` if it detects PhantomJS.

See the example folder for a vanilla example.

Example setup with AMD (advanced): https://gist.github.com/2655876

### Maybe Growl?

Growl support is optional. I'm not sure what the Windows situation is with growl.

### Hacks

The PhantomJS -> Grunt superdimensional conduit uses `alert`. If you have disabled or aliased alert in your app, this won't work. I have conveniently set a global `PHANTOMJS` on `window` so you can conditionally override alert in your app.

## License
Copyright (c) 2012 Kelly Miyashiro
Licensed under the MIT license.