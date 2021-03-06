# Ember Uploader [![Build Status](https://travis-ci.org/benefitcloud/ember-uploader.png?branch=develop)](https://travis-ci.org/benefitcloud/ember-uploader)

Ember.js file uploader

## Getting Started

Download the [production version][min] or the [development version][max].

[min]: https://raw.github.com/benefitcloud/ember-uploader/master/dist/ember-uploader.min.js
[max]: https://raw.github.com/benefitcloud/ember-uploader/master/dist/ember-uploader.js

or using bower `bower install ember-uploader --save`

#### Basic Setup
Create new component and extend `Ember.FileField` provided by ember-uploader. If you're using `Ember.FileField`, it will automatically give you an input field, and will set `files` property when you choose a file.

```js
App.FileUploadComponent = Ember.FileField.extend({
  url: '',
  filesChange: (function() {
    var uploadUrl = this.get('url');
    var files = this.get('files');

    var uploader = Ember.Uploader.create({
      url: uploadUrl
    });

    if (!Ember.isEmpty(files)) {
      uploader.upload(files[0]);
    }
  }).observes('files')
});
```

Call the component, pass it the url, and thats it!
```hbs
{{file-upload url="/upload"}}
```

#### Ajax request type
By default request will be sent as `POST`. To override that, set `type` when creating the object

```js
var uploader = Ember.Uploader.create({
  url: '/upload',
  type: 'PUT'
});
```

#### Change Namespace

```js
var uploader = Uploader.create({
  paramNamespace: 'post'
});

// will be sent as -> post[file]=...
```

#### Change Parameters
By default parameter will be `file`

```js
var upload = Uploader.create({
  paramName: 'upload'
});

// will be sent as -> upload=...
```

#### Progress

```js
uploader.on('progress', function(e) {
  // Handle progress changes
  // Use `e.percent` to get percentage
});
```

#### Finished Uploading

```js
uploader.on('didUpload', function(e) {
  // Handle finished upload
});
```

#### Response
Retured value from uploader will be a promise

```js
var promise = uploader.upload(file);

promise.then(function(data) {
  // Handle success
}, function(error) {
  // Handle failure
});
```

#### Multiple files
```js
App.FileUploadComponent = Ember.FileField.extend({
  multiple: true,
  url: '',

  filesChange: (function() {
    var uploadUrl = this.get('url');
    var files = this.get('files');

    var uploader = Ember.Uploader.create({ url: uploadUrl });

    if (!Ember.isEmpty(files)) {
      uploader.upload(files);
    }
  }).observes('files')
});
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality.

Ember Uploader uses [node.js](http://nodejs.org) and [Grunt.js](http://gruntjs.com/) for builds and tests while using [bower](http://bower.io/) for dependency management. You will need to have these tools installed if you would like to build Ember Uploader.

To get started with development simply do a `npm install` inside the cloned repository to install all dependencies needed for running [Grunt.js](http://gruntjs.com/). You will also need to run `bower install` to install the runtime dependencies. Afterwards you can do a simple `grunt` to execute the default task which will  build the library.

Lint and test your code using: `grunt test`.

_Also, please don't edit files in the "dist" subdirectory as they are generated via Grunt. You'll find source code in the "packages/ember-uploader/lib" subdirectory; tests are located in "packages/ember-uploader/tests"!_

## Thank you
The Ember team, its contributors and community for being awesome. Also thank you to [Erik Bryn](http://twitter.com/ebryn) and the contributors behind [ember-model](http://github.com/ebryn/ember-model) as well as [TJ Holowaychuk](http://twitter.com/tjholowaychuk) for [component/upload](http://github.com/component/upload).

## License
Copyright (c) 2014 Joshua Borton
Licensed under the MIT license.
