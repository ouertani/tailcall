# Graphql datasource

```graphql @config
schema {
  query: Query
}

input StringHashFilter {
  eq: String
  in: [String]
}

input PostFilter {
  name: StringHashFilter
  rec: PostFilter
}

type Post {
  name: String!
  shortName: String
}

type Query {
  posts(filter: PostFilter): Post @expr(body: {name: "A", shortName: "B"})
}
```

```yml @test
- method: POST
  url: http://localhost:8080/graphql
  body:
    query: "query { posts { name  shortName } }"
```
