# Static Assets

\(since v. 0.0.2+\)

Funcatron provides a helper for serving static assets while still providing you complete control.

```javascript
const { 
    funcatron,
    static
} = require('funcatron')

const serveStatic = static("public")  // directory name for static assets relative to the server process root
funcatron([
    ...serveStatic,
    ...otherRoutes
]).listen(8000)
```



