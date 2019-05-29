# Server-Side JavaScript with Nodejs
Go to the profile of notshekhar

Node.js is a JavaScript framework for writing server-side applications. In its simplest form, it follows you to trigger small JavaScript programs from the command line without any browser involved.

For example: To run a JavaScript program in a file called `hello.js`
```javascript
console.log("Hello World")
```
And then use terminal with `node hello.js`

```
$ node hello.js
Hello World
```
## Node Package Manager
Node package manager (npm) comes with node and allows you to install node packages.

Node packages are like JavaScript Libraries and you can work in the same way as JavaScript Library.

So, yo get started first you need to create a node project using `npm init`
```
$ npm init
```
After answering the prompts you’ll see a file something like the following in a new `package.json` file
```json
{
  "name": "server.js",
  "version": "1.0.0",
  "description": "",
  "main": "0.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "notshekhar",
  "license": "ISC",
  "dependencies": {
    "express.js": "^1.0.0"
  }
}
```
here is the link to [documentation of package content](https://docs.npmjs.com/files/package.json)

Now let's say you are creating a node application which can use `fetch` package. `fetch` package can fetch data from an URL. To install a package, simply type `npm install packagename` in terminal
```
$ npm install fetch
```

## Express Basic
Express is a popular, simple web framework from node. It includes most of the things you want to do with the web server, like hosting files and getting query input from a user. I’m going to take a little time on this page to walk through some basic related to other kinds of server-side functionality you might need.

So, first thing you need to intall express package
```
$ npm install express
```
once it installed you are ready to get started

Include express package through `require()` function in your JavaScript file
```javascript
const express = require("express");
```
Now, create an express app
```js
let app = express();
```
The app is now a variable that holds an express instance and allows you to implement functionality on the instance. for example, you might listen to connections on a certain port. The callback is triggered when the server is called.
```js
let server = app.listen(3000);
```
You can also serve static files. for example, if you have an HTML file and you place it in a folder called `public` you can say.
```js
app.use(express.static("public"));
```
Now anytime you enter the URL to your server (if you are running it on your machine, this http://localhost:3000), the contents of the public folder will be hosted.

## Routes with express
Beyond hosting static files, one of the most useful things you can do with server-side programming is execute different blocks of code based on the user’s `route`

A route is a path on the server like `http://localhost:3000/path` with static this is only folder structure, but new possibilities open up when you programmatically handle a route.

For example, the folllowing code specifies a function to call whenever a users goes to `http://localhost:3000/path`
```js
app.get('/path', hello);
```
with the above code, you need to define `hello()` function
```js
function hello(request, response){
  response.send("Hello World!");
}
```
Notice how the callback `hello()` is defined with two parameters refers to HTTP request-response protocol. The user made a request and provides a response.

So, the above example just sending “Hello World!” in the response.

Through `send()` the HTML page will show `“Hello World!”` in screen (generated programmatically).

You can also look at the data associated with the user’s request. for example, if the request was made with a query string like.

`http://localhost:3000/someroute?name=”shekhar”` , the value shekhar can be accessed via the query property of request.
```js
app.get("/someroute", (request, response) => {
  let name = request.query.name;
  response.send("Hello "+ name + "!");
});
```
## RESTful routes
REST(Representational_state_transfer) is a common style of web architecture that is used by many API’s. for example, If you see Wordnik API looks something like `http://api.wordnik.com/v4/word.json/unicorn/definitions`

this is different then using URL query string like `http://localhost:3000/?word=unicorn` . Instead of a query string, the API pulls out commands (“definitions”) and parameters (“unicorn”) from the route itself. This translates to “Please send the definitions for the word unicorn”

You can implement this style in node using `app.get()` as above. The difference is the following

Variable (i.e values that are filled by the users) and notated with the colon (“:”).
Those variables are accessed via the params property of request rather than query
```js
app.get("/hello/:name/:age", hello);
```
A valid URL for the above might then be `http://localhost:3000/hello/shekhar/19`

You could handle the above using
```js
function hello(request, response){
  let name = request.params.name;
  let age = request.params.age;
  response.send("Hello "+ name + " " + age + " years old!");
}
```
