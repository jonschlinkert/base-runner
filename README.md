# base-runner [![NPM version](https://img.shields.io/npm/v/base-runner.svg?style=flat)](https://www.npmjs.com/package/base-runner) [![NPM downloads](https://img.shields.io/npm/dm/base-runner.svg?style=flat)](https://npmjs.org/package/base-runner) [![Build Status](https://img.shields.io/travis/node-base/base-runner.svg?style=flat)](https://travis-ci.org/node-base/base-runner)

> Orchestrate multiple instances of base-methods at once.

## Install

Install with [npm](https://www.npmjs.com/):

```sh
$ npm install base-runner --save
```

## Usage

```js
var runner = require('base-runner');
var Base = require('base');

runner(Base, config, argv, function(err, app, runnerContext) {
  // `err`: error object
  // `app`: instance of `base` 
  // `runnerContext`: object with `argv`, `env` and `config` properties
});
```

## API

### [runner](index.js#L36)

Create a `runner` with the given `constructor`, [liftoff](https://github.com/js-cli/js-liftoff) `config` object, `argv` object and `callback` function.

**Params**

* `Ctor` **{Function}**: Constructor to use, must inherit [base](https://github.com/node-base/base).
* `config` **{Object}**: The config object to pass to [liftoff](https://github.com/js-cli/js-liftoff).
* `argv` **{Object}**: Argv object, optionally pre-parsed.
* `cb` **{Function}**: Callback function, which exposes `err`, `app` (base application instance) and `runnerContext`
* `returns` **{Object}**

**Example**

```js
var Base = require('base');
var argv = require('minimist')(process.argv.slice(2));
var config = {
  name: 'foo',
  cwd: process.cwd(),
  extensions: {'.js': null}
};

runner(Base, config, argv, function(err, app, runnerContext) {
  if (err) throw err;
  // do stuff with `app` and `runnerContext`
  process.exit();
});
```

## Events

The following constructor events are emitted:

* [preInit](#preInit)
* [init](#init)
* [postInit](#postInit)

### preInit

Exposes `runnerContext` as the only paramter.

```js
Base.on('preInit', function(runnerContext) {
});
```

### init

Exposes `runnerContext` and `app` (the application instance) as paramters.

```js
Base.on('init', function(runnerContext, app) {
});
```

### postInit

Exposes `runnerContext` and `app` (the application instance) as paramters.

```js
Base.on('postInit', function(runnerContext, app) {
});
```

### finished

Exposes `runnerContext` and `app` (the application instance) as paramters.

```js
Base.on('finished', function(runnerContext, app) {
});
```

## Related projects

You might also be interested in these projects:

* [base-generators](https://www.npmjs.com/package/base-generators): Adds project-generator support to your `base` application. | [homepage](https://github.com/node-base/base-generators)
* [base-options](https://www.npmjs.com/package/base-options): Adds a few options methods to base-methods, like `option`, `enable` and `disable`. See the readme… [more](https://www.npmjs.com/package/base-options) | [homepage](https://github.com/jonschlinkert/base-options)
* [base-plugins](https://www.npmjs.com/package/base-plugins): Upgrade's plugin support in base applications to allow plugins to be called any time after… [more](https://www.npmjs.com/package/base-plugins) | [homepage](https://github.com/node-base/base-plugins)
* [base-store](https://www.npmjs.com/package/base-store): Plugin for getting and persisting config values with your base-methods application. Adds a 'store' object… [more](https://www.npmjs.com/package/base-store) | [homepage](https://github.com/node-base/base-store)
* [base-tasks](https://www.npmjs.com/package/base-tasks): base-methods plugin that provides a very thin wrapper around [https://github.com/jonschlinkert/composer](https://github.com/jonschlinkert/composer) for adding task methods to… [more](https://www.npmjs.com/package/base-tasks) | [homepage](https://github.com/jonschlinkert/base-tasks)
* [base](https://www.npmjs.com/package/base): base is the foundation for creating modular, unit testable and highly pluggable node.js applications, starting… [more](https://www.npmjs.com/package/base) | [homepage](https://github.com/node-base/base)

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/base-runner/issues/new).

## Building docs

Generate readme and API documentation with [verb](https://github.com/verbose/verb):

```sh
$ npm install verb && npm run docs
```

Or, if [verb](https://github.com/verbose/verb) is installed globally:

```sh
$ verb
```

## Running tests

Install dev dependencies:

```sh
$ npm install -d && npm test
```

## Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2016, [Jon Schlinkert](https://github.com/jonschlinkert).
Released under the [MIT license](https://github.com/node-base/base-runner/blob/master/LICENSE).

***

_This file was generated by [verb](https://github.com/verbose/verb), v0.9.0, on April 22, 2016._