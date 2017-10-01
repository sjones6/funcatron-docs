# Routing

Let's

```javascript
funcatron([
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
            res.statusCode = 404
            res.end("Not found")
        }
    }
])
```



