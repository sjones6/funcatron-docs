# Routing

In order to make routes more maintainable, use the spread operator:

```javascript
const authRoutes = require('./auth-routes')

funcatron([
    {
        path: "/",
        method: "get",
        handler: ({req, res}) => res.end("Hello world!")
    },
    ...authRoutes,
    {
        handler: ({req, res}) => {
            res.statusCode = 404
            res.end("Not found")
        }
    }
])
```

```javascript
// auth-routes.js
module.exports = [
    {
        path: "/auth/login",
        method: "post",
        handler: ({req, res}) => res.end("you're logged in!")
    }, 
    {
        path: "/auth/logout",
        method: "get",
        handler: ({req, res}) => res.end("you're logged out!")
    }
]
```

Now, let's say that you want to guard your API routes to only allow authorized users. For that, you would use route groups.

## Route Groups

Route groups allow you to apply a path prefix and a middleware method to all routes within the group.

```javascript
const { group } = require('funcatron')
const checkAuth = require("./middleware/check-auth")

const makeAPIRoutes = group({

    // route prefix
    path: "/api,

    // This middleware handler will be applied to all requests in the route group
    handler: ({req, res, next}) => {
      if(checkAuth(req)) {
        next()
      } else {
        res.statusCode = 403
        res.end("Forbidden")
      }
    }
})

module.exports = makeAPIRoutes([
  {
     path: "profile", // matches "GET: /api/profile"
     method: "get",
     handler: ({req, res}) => res.end("Your profile")
  },
  {
     path: "profile", // matches "POST: /api/profile"
     method: "post",
     handler({req, res}) => res.end("Profile updated")
  }
])
```



