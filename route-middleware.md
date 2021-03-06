# Middleware

A req/res pair generated by the HTTP server will generally flow through a series of middleware functions which may transform the req/res, branch the flow depending on certain conditions, or terminate the request early \(e.g., in the case of authentication middleware that guards certain routes\).

## Stack

Funcatron makes it easy to compose sets of middleware functions that can be composed together freely using the `stack` method. You can think of `stack` like a sequential but asynchronous-capable `pipe`.

A stack is a sequence of functions that can run asynchronously. Stacks can be nested to form larger stacks.

Here's a really simple stack:

```javascript
const { stack } = require("funcatron")

module.exports = stack(
    ({req, res, next}) => {
        console.log("First")
        next()                          // no need to explicitly pass req/res through
    },
    ({req, res, next}) => {
        console.log("Second")
        next({req, res})                // but you can if you wish :)
    }
)
```

You can also nest stacks:

```javascript
const { stack } = require("funcatron")

module.exports = stack(
    ({req, res, next}) => {
        console.log("First")
        next()                          
    },

    // Nested stack
    stack(
        ({req, res, next}) => {
            console.log("Second")
            next({req, res}) // but you can if you wish :)
        },
        ({req, res, next}) => {
            console.log("Third")
            next({req, res}) // but you can if you wish :)
        },
    ),

    // proceed
    ({req, res, next}) => {
        console.log("Fourth")
        next({req, res})                
    }
)
```

This code isn't the cleanest, but you get the gist. You can also export stacks in order to make stacks easy to compose from discrete parts.

The real power of a stack is that if you don't call `next`, the rest of the stack is never run. This allows you to reject requests that fail validations.

## Example: Form Validation Using Nested Stacks

Let's create a stack that parses the body of a request into JSON and ensures it exists before allowing the request through:

```javascript
// verify-body.js
const { stack } = require("funcatron")
const jsonParser = require("body-parser").json() // https://github.com/expressjs/body-parser

module.exports = stack(
    ({req, res, next}) => jsonParser(req, res, next), // parse body
    ({req, res, next}) => {                           // only allow request that have bodies through.
        if (!req.body) {
            res.statusCode = 400
            res.end("Body required")
        } else {
            next()
        }
    }
)
```

## Nested Stacks

Now we've got a stack that parses and verifies the body exists; now let's create a higher-order function that injects a validation method into a new stack.

```javascript
// validate-body.js
const { stack } = require("funcatron")
const verifyBody = require("./verify-body")

module.exports = validate => stack(
    verifyBody,
    validate
)
```

The return from this higher-order function is a nested stack that will run all the middleware methods in order, ending with the `validate` method that is passed in.

Using this higher-order function, we can create all sorts of validations. Let's create one to validate a user registration:

```javascript
// validate-user-registration.js
const validateBody = require("./validate-body")

const validateUser = validateBody(
    ({req, res, next}) => {
       if (!req.body.email && !req.body.name) {
           res.statusCode = 400
           res.end("Name and email required")
       } else {
           next()
       }
    }
)

module.exports = validateUser
```

Our middleware stack now parses the JSON body into a useful format and ensures that body exists; then it applies a validation for a user registration. The final thing to do is wire up a route that runs the middleware and actually persists the user, which could be stubbed out like so:

```javascript
// user-registration-route.js
const { stack } = require("funcatron")
const validateRegistration = require("./validate-user-registration")
const createUser = require("./create-user") // some method that persists to DB

module.exports = {
   path: "/register",
   method: "post",
   handler: stack(
       validateRegistration, 
        ({req, res}) => createUser(req.body, err => {
            return (!err) ? res.end("Success!") : res.end("Whoops! Failure")
        })
   )
}
```

Eventually, you'd need to pass this into the routes array passed into the `funcatron` method.

## Eager Stacks

Stacks are lazy-evaluated at time of request in order to provide nesting capabilities. However, for the extreme performance-minded, you can take advantage of the `eagerStack`:

Let's create an eagerStack that handles updates to a user profile:
```javascript
const { eagerStack } = require('funcatron')
const jsonParser = require("body-parser").json()
const updateUser = require("./update-user") // some method that persists to DB

module.exports = {
   path: "/profile",
   method: "post",
   handler: eagerStack(
        ({req, res, next}) => {
            jsonParser(req, res, () => next({req, res}))
        },
        ({req, res, next}) => {                           // only allow request that have bodies through.
            if (!req.body) {
                res.statusCode = 400
                res.end("Form input required required")
            } else {
                next({req, res})
            }
        },
        ({req, res}) => updateUser(req.body, err => {
            return (!err) ? res.end("Success!") : res.end("Whoops! Failure")
        })
   )
}
```

Limitations of `eagerStack`:

* It cannot be nested (although you can nest regular `stacks` within `eagerStacks`)
* Have to return the request/response in `next`, like so `next({req, res})`
