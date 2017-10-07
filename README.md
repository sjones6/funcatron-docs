# Funcatron

Funcatron is a functional framework for composing Node applications.

```javascript
const funcatron = require('funcatron')
const http = funcatron([{
    path: "/hello",
    method: "get",
    handler: ({req, res}) => res.end("Hello world! Yours sincerely, Funcatron")
}]).listen(8000)
```

## Another Node framework, really?

There are lots of great frameworks for writing Node applications, but none of them focus on functional programming.

(If that statement is inaccurate, please open an [issue](https://github.com/sjones6/funcatron/issues) and I'll mention them here and how they differ.)

## How does this compare to Express or Sails?

Both Funcatron and Express are middleware style, minimal frameworks, although the API is totally different and Funcatron's focus on functional programming is certainly different.

Sails is a full-featured and relatively-opinionated framework. It has opinions about framework architecture (MVC) and comes with things like an ORM. With Funcatron, it has no opinions about those things and you can plug in your own ORM if necessary.

## Core Values

* Functional programming (obviously)
* Testable - applications should be easy to test
* Elegant - composing asynchronous pipelines to handle requests should easy and elegant

## Get Started

Take a look at the [quick start](/quick-start.md) or [dive into the larger tutorial](/getting-started.md).

