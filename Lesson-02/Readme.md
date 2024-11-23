## Object Types

### n GraphQL, an Object Type is a complex type that represents a collection of fields. Object Types are used to define the structure of data that can be queried and mutated through a GraphQL API.

### Each Object Type has a unique name and a set of fields, where each field has a name and a type. The type of a field can be a scalar type (such as Int, String, or Boolean), another Object Type, or a list of another type.

### If you're familiar with Typescript and interfaces, this might help you.

### Here's an example of an Object Type that represents a "User" in a social media application:

```
type User {
  id: ID!
  name: String!
  email: String!
  friends: [User!]!
}
```

## The `!` sign means the field is mandatory.

### In this example, the "User" Object Type has four fields: "id", "name", "email", and "friends". The "id" field has a type of ID, which is a built-in scalar type in GraphQL that represents a unique identifier. The "name" and "email" fields have a type of String, and the "friends" field has a type of a list of "User" Objects.

### Here's another example of an Object Type that represents a "Book" in a library application:

```
type Book {
  id: ID!
  title: String!
  author: Author!
  genre: String!
  published: Int!
}
```

### Object Types can be used to define the structure of data that is returned from a query or mutation in a GraphQL API. For example, a query that returns a list of users might look like this:

```
query {
  users {
    id
    name
    email
    friends {
      id
      name
    }
  }
}
```

### In this query, the "users" field returns a list of "User" Objects, and the query specifies which fields to include in the response.

## Queries

### In GraphQL, a query is a request for specific data from the server. The query specifies the shape of the data that the client wants to receive, and the server responds with the requested data in the same shape.

### A query in GraphQL follows a similar structure to the shape of the data it expects to receive. It consists of a set of fields that correspond to the properties of the data the client wants to retrieve. Each field can also have arguments that modify the data returned.

### Here's an example of a simple query in GraphQL:

```
query {
  user(id: "1") {
    name
    email
    age
  }
}
```

### In this example, the query is requesting information about a user with the ID of "1". The fields specified in the query are "name", "email", and "age", which correspond to the properties of the user object.

### The response from the server would be in the same shape as the query, with the requested data returned in the corresponding fields like:

```
{
  "data": {
    "user": {
      "name": "John Doe",
      "email": "johndoe@example.com",
      "age": 25
    }
  }
}
```

### Here, the server has returned the requested data about the user in the "name", "email", and "age" fields. The data is contained in a "data" object to differentiate it from any errors or other metadata that may be included in the response.

## Mutations

### In GraphQL, mutations are used to modify or create data on the server. Like queries, mutations specify the shape of the data being sent to and received from the server. The main difference is that while queries only read data, mutations can both read and write data.

### Here's an example of a simple mutation in GraphQL:

```
mutation {
  createUser(name: "Jane Doe", email: "janedoe@example.com", age: 30) {
    id
    name
    email
    age
  }
}
```

### In this example, the mutation is creating a new user on the server with the name "Jane Doe", email "janedoe@example.com", and age 30. The fields specified in the mutation are "id", "name", "email", and "age", which correspond to the properties of the user object.

### The response from the server would be in the same shape as the mutation, with the newly created user data returned in the corresponding fields:

```
{
  "data": {
    "createUser": {
      "id": "123",
      "name": "Jane Doe",
      "email": "janedoe@example.com",
      "age": 30
    }
  }
}
```

### Mutations in GraphQL are designed to be composable, meaning that multiple mutations can be combined into a single request. This allows clients to perform complex operations with a single network round-trip.

## Resolvers

### In GraphQL, a resolver is a function responsible for fetching the data for a specific field defined in a GraphQL schema. Resolvers are the bridge between the schema and the data source. The resolver function receives four parameters: parent, args, context, and info.

- `parent`: The parent object for the current field. In nested queries, it refers to the parent field's value.

- `args`: The arguments passed to the current field. It is an object with key-value pairs of the argument names and their values.

- `context`: An object shared across all resolvers for a particular request. It contains information about the request such as the currently authenticated user, database connection, etc.

- `info`: Contains information about the query including the field name, alias, and the query document AST.

### Take a look at the resolver function:

```
const resolvers = {
  User: {
    posts: (parent, args, context, info) => {
      return getPostsByUserId(parent.id);
    },
  },
};
```

## Schemas

### In GraphQL, a schema is a blueprint that defines the structure of the data that can be queried in the API. It defines the available types, fields, and operations that can be performed on those types.

### GraphQL schemas are written in the GraphQL Schema Definition Language (SDL), which uses a simple syntax to define the types and fields available in the API. The schema is typically defined in the server-side code and then used to validate and execute incoming queries.

### Here's an example of a simple GraphQL schema definition:

```
type Book {
  id: ID!
  title: String!
  author: String!
  published: Int!
}

type Query {
  books: [Book!]!
  book(id: ID!): Book
}

type Mutation {
  addBook(title: String!, author: String!, published: Int!): Book!
  updateBook(id: ID!, title: String, author: String, published: Int): Book
  deleteBook(id: ID!): Book
}
```

### Note that each field has a type, which can be a built-in scalar type like String or Int, or a custom type like Book. The ! after a type indicates that the field is non-nullable, meaning it must always return a value (that is, it cannot be null).
