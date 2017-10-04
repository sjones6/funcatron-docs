# Configuration

Let's say you need to supply a custom error handler or 404 handler, you'll want to pass a number of configuration options.

Use the `make` method to supply this configuration. Any supplied option overrides the default:

```javascript
// make-funcatron.js

const { make } = require("funcatron")

module.exports = make({

    // Path to server static resources; pass `false` to disable any static file serving
    static: "public",

    // Enable HTTPS; pass an object that will be passed into https.createServer to enable HTTPS.
    // See Node documentation for these values: https://nodejs.org/api/https.html#https_https_createserver_options_requestlistener
    https: false,

    // Handle 404
    lost: ({req, res}) => res.end("You're lost"),

    // Handle any errors caught by funcatron while processing a request.
    // Remember that you will also need to handle the serving a response
    // otherwise the request will hang and eventually time out.
    err: ({req, res, err}) => res.end("You've hit an error!")
})
```

Once you have funcatron configured, you can use it like so:

```javascript
const makeFuncatron = require("./make-funcatron")

// Pass in the routes needed
const server = makeFuncatron([
  {
    method: "get",
    path: "/home",
    handler: ({req, res}) => res.end("Welcome home!")
  }
])

module.exports = server
```



