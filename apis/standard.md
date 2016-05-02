# APIs


## Endpoint Design

### HTTP Methods (aka HTTP verbs)

While HTTP verbs do not match directly to CRUD operations, for the sake of developer sanity we will outline a loose mapping to CRUD as well as other operations.

#### `GET`

Used to retrieve an individual entity or a collection.  `GET` is an idempotent operation.   

Examples:

* `GET /users`  retrieve users collection (i.e. all users).  This response will contain an array of objects (entities)
* `GET /users/:id` retrieve an individual user.  This response will be an object.
* `GET /users/:id/posts` retrieve an individual user.  This response will contain an array of objects (entities)


#### `POST`

HTML forms only support `GET` & `POST` which has led to widespread abuse of the `POST` verb.

For our usage, unless there is an extremely good reason beyond developer preference, `POST` will be used for creation of new entities.

Examples:

* `POST /users` with a payload of `{name: 'foobar'}` will create a new user.

#### `PUT`

Used for replacing or creating a specific entity.  `PUT` is an idempotent operation.

Examples:

* `PUT /users/:id` with a payload of `{name: 'barfoo'}` will replace that specific user.
* `PUT /users/:id/posts/:id`, with no payload, will create a relationship between the post and user.  

#### `PATCH`


Used for updating a specific entity.  Although not required by the [spec](https://tools.ietf.org/html/rfc5789), our `PATCH`
implementations will be idempotent.  

On the backend, Laravel treats the replacement of an entity and the changing of a single value on that entity the same.

Examples:

* `PATCH /users/:id` with a payload of `{name: 'barfoo'}` will update the user's name.


#### `DELETE`

Used to destroy a specific entity.  `DELETE` is an idempotent operation.

Examples:

* `DELETE /users/:id` will delete the specific user.
* `DELETE /users/:id/posts/:id` will remove the relationship between the post and user.



### Sub-Resource Endpoint Design


/routes/:id/runs/:id

If you need to get to the `run`, go to `/runs/:id`


### Auto-incrementing ids

public vs private api
UUIDs

## Transformation Layers

Transformers allow for the API to be decoupled from the backend code implementation.  They also enable the combining of multiple entities and

### Private to Public

### Public to Private


### Links (HATEOAS or Hypermdedia Linking)

## Relationships

## Authentication

## Versioning

## Pagination

## Documentation

## Testing

### Seeds

## Status Codes

## Custom Endpoints

## Content-types

`application/json` is our default content type unless there is a pressing & substantial project need beyond developer preference.


## Resources

* Postman
* *How to build APIs You Don't Hate*
* [Rest Cookbook](http://restcookbook.com/)



## Glossary


* *Transformer*:
