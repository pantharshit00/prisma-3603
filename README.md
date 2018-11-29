### Introduction

Reproduction for https://github.com/prisma/prisma/issues/3603

To reproduce:- 

1. `docker-compose up -d`
2. `export PRISMA_MANAGEMENT_API_SECRET=my-prisma-api-secret`
3. `prisma deploy`
4. subscribe to this subscription
```graphql
subscription {
  user {
    node{
      id
      firstName
      lastName
      email
      createdAt
      updatedAt
      archivedAt
    }
    mutation
    updatedFields
    previousValues {
      id
      firstName
      lastName
      email
      createdAt
      updatedAt
      archivedAt
    }
  }
}
```
5. Run this mutation
```graphql
mutation {
  updateUser(data: { lastName: "TestLastName" }, where: { email: "user@example.com" }) {
    id
    firstName
    lastName
    email
    createdAt
    updatedAt
    archivedAt
  }
}
```
