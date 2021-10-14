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