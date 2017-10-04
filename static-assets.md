# Static Assets

\(since v. 0.0.2+\)

By default, static assets are served from a `public` directory. You can configure the directory by passing in a new path relative to the current working directory for the server:

```javascript
const { make } = require('funcatron')

const funcatron = make({
  static: 'static_assets/'
})

// supply any other routes
funcatron([
  {
    method: 'get',  
    handler: ({req, res}) => res.end('Hello!')
  }
]).listen(8000)
```



