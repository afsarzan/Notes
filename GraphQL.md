### GraphQL Nuances

## On server side
- require @apollo/server,body-parser, cors
- ```
    const server = new ApolloServer({
      typeDefs: `
        type TypeName {
          fields: FieldType!
        }
        type Query {
          methodName: [TypeName]
        }
    `,
      resolver:{
        Query: {
          getTodos: () => [] // return data here
        }
      }
    })
  ```
- 
## On client side
```
    const client = new ApolloClient({
      uri: "localhost",
      cache: new InMemoryCache()
    })
