# Static Assets

\(since v. 0.0.2+\)

By default, static assets are served from a `public` directory. You can configure the directory by passing in a new path relative to the current working directory for the server:

```javascript
const { make } = require("funcatron")

const funcatron = make({
  static: "static_assets/"
})

// supply any other routes
funcatron([
  {
    method: "get",
    path: "/"  
    handler: ({req, res}) => res.end("Hello!")
  }
]).listen(8000)
```

Static assets are served _after_ checking the routes for a potential match, so you can always override certain requests and handle serving those static files on your own:

```javascript
const { make } = require("funcatron")

const funcatron = make({
  static: "static_assets/"
})

// supply any other routes
funcatron([
  {
    method: "get",
    path: "/index.html"  
    handler: ({req, res}) => { // server file ... or not. You choose. :) }
  }
]).listen(8000)
```



