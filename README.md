# Funcatron

Funcatron is a functional framework for building Node applications.

## Introduction

At its core, an Node web server is nothing more than this:

```javascript
const { createServer } = require('http')

const http = createServer((req, res) => res.end("Hello world!"))

http.listen(8000)
```

In other words, the HTTP server listens for request coming in to a certain port, generates a `req`/`res` object pair, and passes them into a callback.

Stripped of all fluff, Funcatron is nothing other than the callback that is passed into the `createServer` method and enough scaffolding to make composing the functions that handle HTTP requests easy.

## Installation

Install via npm or yarn:

`npm install funcatron --save`

or

`yarn add funcatron`

## Basic Example

First, let's re-create the above example in funcatron

```javascript
const { funcatron } = require('funcatron')

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

That's a little better, but it's going to get really cumbersome for any serious application.

