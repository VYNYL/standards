# APIs


## Endpoint Design

### [Resources](http://restful-api-design.readthedocs.io/en/latest/resources.html)

Definition:

>The key abstraction of information in REST is a resource. Any information that can be named can be a resource: a document or image, a temporal service (e.g. "today's weather in Los Angeles"), a collection of other resources, a non-virtual object (e.g. a person), and so on. In other words, any concept that might be the target of an author's hypertext reference must fit within the definition of a resource. A resource is a conceptual mapping to a set of entities, not the entity that corresponds to the mapping at any particular point in time.

In other words, a resource can be an endpoint such as `/users/:id` which can receive one of several actions (HTTP verbs).  Those actions are HTTP verbs.  Predominantly in our usage, resources will be entities (objects) or collections (arrays).  Common actions on a single entity resource are:

* `GET /users/:id`: retrieve the entity
* `PUT /users/:id`: replace the entity
* `PATCH /users/:id`: partially update the entity
* `DELETE /users/:id`: destroy the entity

Notice that we are using the plural form of the entity, `user`, to describe the endpoint.  This allows for consistency and allows
the easy addition of relations to the endpoint:


#### Collections

Collections are homogeneous groupings (arrays) of resources (entities).  Common actions on a collection are:

* `GET /users`: retrieve the collection
* `POST /users`: add a new entity to the collection (you need to send a body with the request)
* `PUT /users`: replace the entire collection.  Requires a new collection to be sent in the body

If you need to "include" relationships for entities in a collection, use the `include` parameter in the request uri:
`GET /users?include=posts`.  Be careful that you do not run a query for each include since that will result in a horrible [N+1](https://secure.phabricator.com/book/phabcontrib/article/n_plus_one/) mess.  Most ORMs have the ability to include relationship entities. Eloquent has the `with()` method as well as properties that will load a relation only once: `$user->posts` will load the `posts` for the `user` only once but `$user->posts()` will load them every time. 


#### Relationships (Sub Resources)

Relationships are connections between entities.  For example, `GET /users/:id/posts` would return a list of all the posts for a user.  Common actions on a relationship are:

* `GET /users/:id/posts`: retrieve the posts for a user
* `POST /users`: add a new entity to the collection (you need to send a body with the request)
* `PUT /users`: replace the entire collection.  Requires a new collection to be sent in the body


Do **NOT** format relationship endpoints in this manner `GET /posts/get-by-user/:id`.  Technically it would do the same thing as the above endpoint but this format is difficult to understand as well as redundant since the `GET` is implied from the HTTP Method.  If you started down this path, before long you would see developers creating endpoints such as `GET /posts/user-get-by/:id` as well as other dubious schemes.  That leads to an API that is incomprehensible.  Don't do it.

Do **NOT** access a single entity through a relationship: `GET /users/:id/posts/:id`.  Instead, go directly to the endpoint
for that entity: `GET /posts/:id`.



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
http://restful-api-design.readthedocs.io/en/latest/resources.html#representations
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


## Concerns for public APIs

### Auto-incrementing ids

public vs private api
UUIDs

## [Content Representations](http://restful-api-design.readthedocs.io/en/latest/resources.html#representations)


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
* [Restful Api Design Site](http://restful-api-design.readthedocs.io/en/latest/intro.html)
* [Nobody Understand REST](http://blog.steveklabnik.com/posts/2011-07-03-nobody-understands-rest-or-http)



## Glossary


* *Transformer*:
