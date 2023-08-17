*****************Mutation And Query***********************************

mutation CreateRepository($inputRepo: CreateRepositoryInput!) {
  createRepository(input: $inputRepo) {
    repository {
      id
      name
      owner {
        login
      }
    }
  }
}

mutation AddProject($input: CreateProjectInput!) {
  createProject(input: $input) {
    clientMutationId
    project {
      id
      createdAt
      url
    }
  }
}

query MyFirstQuery($name: String!, $owner: String!) {
  CoreRepo: repository(name: $name, owner: $owner) {
    ...RepositoryCommonField
    databaseId
    descriptionHTML
    pushedAt
    licenseInfo {
      id
    }
  }
  WpfRepo: repository(name: "wpf", owner: "dotnet") {
    ...RepositoryCommonField
    databaseId
    descriptionHTML
    pushedAt
    licenseInfo {
      id
    }
  }
}

query OwnerQuery {
  viewer {
    login
    id
  }
}

fragment RepositoryCommonField on Repository {
  id
  url
  createdAt
  description
}

*********************************************************

*******************Variables*****************************
{
  "name": "core",
  "owner": "dotnet",
  "input": {
    "ownerId": "MDQ6VXNlcjE0MzExNjY2",
    "name": "My First GraphQL Project",
    "body": "I'm trying to create my first graphql project.",
    "clientMutationId": "1234567"
  },
  "inputRepo": {
    "name": "RepositoryCreatedByGraphQL",
    "ownerId": "MDQ6VXNlcjE0MzExNjY2",
    "visibility": "PUBLIC"
  }
}

*********************************************************