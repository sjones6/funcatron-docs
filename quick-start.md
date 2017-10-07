# Quick Start

Install via npm or yarn:

`npm install funcatron --save` or `yarn add funcatron`.

Then, wire up a server by passing in an array of route definitions:

```javascript
const funcatron = require('funcatron')

const http = funcatron([{
    path: "/hello",
    method: "get",
    handler: ({req, res}) => res.end("Hello world!")
}])

http.listen(8000)
```

If you're ready to rock-and-roll, the last thing I'd check-out is [how middleware works](/route-middleware.md) in funcatron.