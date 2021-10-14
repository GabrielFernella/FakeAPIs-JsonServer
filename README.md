### Running json-server

This example shows, how to run a local json-server for development purposes.

Edit `db.json` to alter the data, received from the endpoint.

This example does not use a global installation of json-server.

Find more details on the original repository of [json-server][json-server]

#### Usage

Clone the repository and start your own project.

```bash
$ git clone git@github.com:halfzebra/json-server-example.git my-project
$ cd my-project/
$ rm -rf .git
$ git init
```

Install the latest [Node.js](https://nodejs.org/en/), install dependencies and start the server.

```bash
$ npm i      # install deps
$ npm start  # start the server, using script
```

#### Use in JavaScript

You might use [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) to send a request to the endpoint.

```js
var request = new Request('http://localhost:3004/posts/', {
  headers: new Headers({
    'Content-Type': 'application/json'
  })
});

fetch(request)
  .then(function(res) {
    return res.json();
  })
  .then(function(data) {
    // Response data
  })
  .catch(function(err) {
    // Error
  });
```

[json-server]: <https://github.com/typicode/json-server>

# Dicas de como usar
- Para querys de relacionamento entre entidades
http://localhost:3004/participants/3fa85f64-5717-4562-b3fc-2c963f66afa2/adhesions


### Plural routes

```
GET    /posts
GET    /posts/1
POST   /posts
PUT    /posts/1
PATCH  /posts/1
DELETE /posts/1
```

### Singular routes

```
GET    /profile
POST   /profile
PUT    /profile
PATCH  /profile
```

### Filter

Use `.` to access deep properties

```
GET /posts?title=json-server&author=typicode
GET /posts?id=1&id=2
GET /comments?author.name=typicode
```

### Paginate

Use `_page` and optionally `_limit` to paginate returned data.

In the `Link` header you'll get `first`, `prev`, `next` and `last` links.


```
GET /posts?_page=7
GET /posts?_page=7&_limit=20
```

_10 items are returned by default_

### Sort

Add `_sort` and `_order` (ascending order by default)

```
GET /posts?_sort=views&_order=asc
GET /posts/1/comments?_sort=votes&_order=asc
```

For multiple fields, use the following format:

```
GET /posts?_sort=user,views&_order=desc,asc
```

### Slice

Add `_start` and `_end` or `_limit` (an `X-Total-Count` header is included in the response)

```
GET /posts?_start=20&_end=30
GET /posts/1/comments?_start=20&_end=30
GET /posts/1/comments?_start=20&_limit=10
```

_Works exactly as [Array.slice](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) (i.e. `_start` is inclusive and `_end` exclusive)_

### Operators

Add `_gte` or `_lte` for getting a range

```
GET /posts?views_gte=10&views_lte=20
```

Add `_ne` to exclude a value

```
GET /posts?id_ne=1
```

Add `_like` to filter (RegExp supported)

```
GET /posts?title_like=server
```

### Full-text search

Add `q`

```
GET /posts?q=internet
```

### Relationships

To include children resources, add `_embed`

```
GET /posts?_embed=comments
GET /posts/1?_embed=comments
```

To include parent resource, add `_expand`

```
GET /comments?_expand=post
GET /comments/1?_expand=post
```

To get or create nested resources (by default one level, [add custom routes](#add-custom-routes) for more)

```
GET  /posts/1/comments
POST /posts/1/comments
```

### Database

```
GET /db
```

### Homepage

Returns default index file or serves `./public` directory

```
GET /
```

## Extras

### Static file server

You can use JSON Server to serve your HTML, JS and CSS, simply create a `./public` directory
or use `--static` to set a different static files directory.

```bash
mkdir public
echo 'hello world' > public/index.html
json-server db.json
```

```bash
json-server db.json --static ./some-other-dir
```

### Alternative port

You can start JSON Server on other ports with the `--port` flag:

```bash
$ json-server --watch db.json --port 3004
```