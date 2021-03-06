# Configuration Validator

Built as the pluggable validator for [webpack-validator](https://github.com/kentcdodds/webpack-validator)
but could be used to validate any configuration object.

[![version](https://img.shields.io/npm/v/configuration-validator.svg?style=flat-square)](http://npm.im/configuration-validator)
[![downloads](https://img.shields.io/npm/dm/configuration-validator.svg?style=flat-square)](http://npm-stat.com/charts.html?package=configuration-validator)
[![MIT License](https://img.shields.io/npm/l/configuration-validator.svg?style=flat-square)](http://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

## Usage

```javascript
var configValidator = require('configuration-validator')

// call the function with your config and validators
configValidator('Name of config', config, arrayOfValidators)
```

## Validators

A validator is an object that describes to configuration-validator what it should run on and
defines a function to run to do the validation. Here's an example of a simple validator that
checks for the value to be a boolean:

```javascript
{
  key: 'foo.bar', // can be any depth. Uses lodash's `get` method
  description: 'Some descriptive message', // used in verbose mode (in development)
  validate: function validateFooBar(value, context) {
    // value is the value of `foo.bar` for the given object
    // context is an object with the following properties:
    //   - `key` - `foo.bar` in this case
    //   - `parent` - the parent object in which this value is found
    //   - `config` - the entire object being validated

    if (typeof value !== 'boolean') {
      // if it's not a boolean, then we fail the validation. In this case
      // we return a message that is an error or a warning
      return 'must be a boolean' // just shorthand for: {error: 'must be a boolean'}
      // or you can do:
      // return {warning: 'must be a boolean'} // output is yellow
      // return {error: 'must be a boolean'} // output is red
    }
  },
}

```

## LICENSE

MIT

