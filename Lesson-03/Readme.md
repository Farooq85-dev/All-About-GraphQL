## TLDR and Comparison with Equivalent REST Concepts

- `Object Types`: In GraphQL, Object Types are used to define the data that can be queried from an API, similar to how the response data model is defined in REST APIs. However, unlike REST, where data models are often defined in different formats (for example, JSON or XML), GraphQL Object Types are defined using a single language-agnostic syntax.

- `Queries`: In GraphQL, queries are used to fetch data from an API, similar to HTTP GET requests in REST APIs. However, unlike REST APIs, where multiple requests may be required to fetch nested data, GraphQL queries can be used to fetch nested data in a single request.

- `Mutations`: In GraphQL, mutations are used to modify data in an API, similar to HTTP POST, PUT, and DELETE requests in REST APIs. However, unlike REST APIs, where different endpoints may be required to perform different modifications, GraphQL mutations are performed through a single endpoint.

- `Resolvers`: In GraphQL, resolvers are used to specify how to fetch data for a particular field in a query or mutation. Resolvers are similar to controller methods in REST APIs, which are used to fetch data from a database and return it as a response.

- `Schemas`: In GraphQL, a schema is used to define the data that can be queried or mutated from an API. It specifies the types of data that can be requested, how they can be queried, and what mutations are allowed. In REST APIs, schemas are often defined using OpenAPI or Swagger, which specify the endpoints, request and response types, and other metadata for an API.

### Overall, GraphQL and REST APIs differ in how they handle data fetching and modification.

### REST APIs rely on multiple endpoints and HTTP methods to fetch and modify data, whereas GraphQL uses a single endpoint and queries/mutations to accomplish the same.

### GraphQL's use of a single schema to define the data model of an API makes it easier to understand and maintain compared to REST APIs, which often require multiple documentation formats to describe the same data model.
