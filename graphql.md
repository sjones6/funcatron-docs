# GraphQL 

Using GraphQL with Funcatron can be done easily by pulling in the `express-graphql` package.

First, install the necessary modules:

```
yarn add express-graphql graphql
```

```javascript
const { e2f, funcatron } = require('funcatron')
const graphqlHTTP = require('express-graphql')
const TestSchema = require('./TestSchema')

// Initialize the GraphQL handler with your schema (see below)
const graphQL = graphqlHTTP({
    schema: TestSchema,
    graphiql: true
})

funcatron([
    {
        path: "/graphql",
        handler: e2f(graphQL)
    }
]).listen(8000)
```

Here's a very basic test schema:

```javascript
// TestSchema.js
const {
    graphql,
    GraphQLSchema,
    GraphQLObjectType,
    GraphQLString
} = require('graphql')
  
module.exports = new GraphQLSchema({
    query: new GraphQLObjectType({
        name: 'TestQuery',
        fields: {
            hello: {
                type: GraphQLString,
                resolve() {
                    return 'world';
                }
            }
        }
    })
})
```

That's it! You should be able to hit `localhost:8000/graphql` and see the GraphiQL interface.