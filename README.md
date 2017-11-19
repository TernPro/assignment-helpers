## GraphQL Helpers

Consume these functions however you want. Their return values can be POSTed to
the endpoint as the request body.

If we use `getProject` as an example, a successful result would look like this:

```json
{
  "data": {
    "project": {
      "...properties": "...values",
      "tasks": [
        {
          "...properties": "...values"
        },
        {
          "...properties": "...values"
        },
        {
          "...properties": "...values"
        }
      ],
      "collection": {
        "...properties": "...values"
      }
    }
  }
}
```

A failed request can have many errors and will look like this:

```json
{
  "errors": ["...errors"]
}
```

### Queries

#### getCollection

Retrieve a collection by id. All fields of the collection as well as child
projects, and their child tasks will be provided.

#### getCollections

Retrieve all the collections. All fields of the collection as well as child
projects, and their child tasks will be provided. In our case, there is only 1
collection that all projects will be created under.

#### getProject

Retrieve a project by id. All fields of the project as well as the parent
collection and child tasks will be provided.

#### getProjects

Retrieve all projects in a collection by the collection's id. All fields of the
project as well as the parent collection and child tasks will be provided.

#### getTask

Retrieve a task by id. All fields of the task as well as the parent project, and
its parent collection.

#### getTasks

Retrieve all tasks in a project by the project's id. All fields of the task as
well as the parent project, and its parent collection.

### Mutations

#### createProject

This is the only mutation exposed by the endpoint. Your `args` parameter should
follow the structure below.

```
name          {String}  the name of the project
description   {String}  the description of the project
collectionId  {String}  the id of collection the project is in
tasks         {Array}   the tasks in the project
  name        {String}  the name of the task
  description {String}  the description of the task
  type        {String}  which type of task this is, "CONTENT" || "TODO"
  dueDate     {String}  the date this task is due
```
