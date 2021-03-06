[![Build Status](https://travis-ci.org/npm/npm-registry-mock.png?branch=master)](https://travis-ci.org/npm/npm-registry-mock)
[![Dependency Status](https://gemnasium.com/npm/npm-registry-mock.png)](https://gemnasium.com/npm/npm-registry-mock)

#npm-registry-mock


##Usage

Currently mocked packages are:

`underscore` at 1.3.1, 1.3.3 and 1.5.1 while version 1.5.1 is the latest in this mocked registry.

`request` at 0.9.0, 0.9.5 and 2.27.0 while version 2.27.0 is the latest in this mocked registry.

`test-package-with-one-dep` at 0.0.0, version 0.0.0 is the latest in this mocked registry. It has a mocked dependency: `test-package@0.0.0`

Installing underscore 1.3.1:

```javascript
var mr = require("npm-registry-mock")

mr(1331, function (s) {
  npm.load({registry: "http://localhost:1331"}, function () {
    npm.commands.install("/tmp", "underscore@1.3.1", function (err) {
      // assert npm behaves right...
      s.close() // shutdown server
    })
  })
})
```

Defining custom mock routes:

```javascript
var mr = require("npm-registry-mock")

var customMocks = {
  "get": {
    "/mypackage": [500, {"ente" : true}]
  }
}

mr({port: 1331, mocks: customMocks}, function (s) {
  npm.load({registry: "http://localhost:1331"}, function () {
    npm.commands.install("/tmp", "mypackage", function (err) {
      // assert npm behaves right with an 500 error as response...
      s.close() // shutdown server
    })
  })
})
```

##Todo

 - add more use-cases
