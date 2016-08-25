# Angular Unit Tests

## Examples 

### ES5

See John Papa's [AngularJS Testing Examples](https://github.com/johnpapa/ng-patterns-testing).  You can download the 
codebase and try out tests.  If you want to start a new codebase that utilizes this testing strategy, you can use 
[Angular Hot Towel](https://github.com/johnpapa/generator-hottowel) to scaffold a new project for you.  Keep in mind that 
you probably not need the `src/server` folder nor the separate `src/client` folder in the generated codebase

In the `src/client/app` folder in the example codebase, you will find several component folders. 

In those component folders, you will find `spec.js` files for tests of controllers, route definitions, and services.  


### ES2015 

For examples in an ES2015 code base, refer to the [NG6](https://github.com/AngularClass/NG6-starter) codebase.  

In the `client/app/components/` folders, you will find examples of tests.  


## Resources

Refer to the [Angular Style Guide](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#testing) for general 
information on testing in Angular.

There is also a [Pluralsight Course on Angular Testing](https://www.pluralsight.com/courses/play-by-play-angular-testing-papa-bell).

## Libraries 

* [Mocha](http://mochajs.org/) for unit tests 
* [Chai](http://chaijs.com/) for assertions.
* [Sinon](http://sinonjs.org/) for spies, stubs, and mocks.
* [PhantomJS](http://phantomjs.org/) provides the web stack for testing. 
* [Karma](http://karma-runner.github.io/1.0/index.html) is the test runner.
