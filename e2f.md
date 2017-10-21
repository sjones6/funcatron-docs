# Using Express Middleware

The Express community is huge, and has built lots of great middleware.

Funcatron has a help function called `e2f` (for Express to Funcatron) to help take advantage of that community:

```javascript
const { e2f, stack } = require('funcatron')
const bodyParser = require('body-parser')

// your routes array
module.exports = [
    {
        path: '/',
        method: 'get',
        handler: stack(
            e2f(bodyParser.json()),
            ({req, res}) => res.end('Hello!')
        )
    }
]
```

## Caveat

Note that Funcatron uses the plain `Request`/`Response` objects constructed by Node and does not add any sugar that Express does (for instance, the `res.json` method). Therefore, if a middleware function relies upon those methods, it will probably error out.