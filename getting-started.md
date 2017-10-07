## Getting Started

At its core, an Node web server is nothing more than a callback that receives a request and response object every time a request is received:

```javascript
const { createServer } = require('http')

const http = createServer((req, res) => res.end("Hello world!"))

http.listen(8000)
```

Stripped of all fluff, Funcatron is merely the server callback that pipes the request and response through a series of functions until a response is served back to the client.

## Basic Example

First, let's re-create the above example in funcatron

```javascript
const funcatron = require('funcatron')

const http = funcatron([{
   handler: ({req, res}) => res.end("Hello world!")
}])

http.listen(8000)
```

Now, this isn't a very interesting application since it returns the same response no matter what is requested.

So, let's add a few more routes:

```javascript
const http = funcatron([
   {
      path: "/",
      method: "get",
      handler: ({req, res}) => res.end("Hello world!")
   },
   {
      path: "/login",
      method: "post",
      handler: ({req, res}) => res.end("Welcome! You're logged in!")
   },
   {
      handler: ({req, res}) => {
         res.statusCode = 400
         res.end("Not found")
      }
   }
])

http.listen(8000)
```

That's a little better, but it's going to get really cumbersome for any serious application with more than a handful of routes. [Routing in Functatron](/routing.md)