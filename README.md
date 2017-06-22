# node-express-ejs-cheat-sheet

### Index
* [How do I get an express server up and running?](#express)
* [How do I get EJS up and running?](#ejs)
* [How do I set up LokiJS?](#lokijs)
* [How do I set up router files?](#router)

<h2 id="express">How do I get an express server up and running?</h2>
* Create a directory & cd into directory
* run `touch server.js` & `npm init -y`
* run `npm install --save express cors body-parser`
* Open directory in your text editor
* In server.js, type `expserv` and hit the `tab` button
* Fill in any of the urls that you would like to use or just delete all of the `app.get`, `app.post`, `app.patch`, and `app.delete`
* To run the server, run the command `nodemon server.js`

<h2 id="ejs">How do I get EJS up and running?</h2>
* Run `npm install --save ejs`
* Create a folder in the main directory called `views`
* Create a file inside of the `views` folder called `index.ejs` and put some boilerplate of your choice in there to make sure that it will work
* Set your views folder and your view engine using the following code:
```
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');
```
* Create a test route in server.js that renders the `index.ejs` file:
```
  app.get('/', function(req, res) {
    res.render('index');
  })
```

<h2 id="lokijs">How do I set up LokiJS?</h2>
* Run `npm install --save lokijs`
* Create a folder called `db` in the main directory.
* Create a file within the `db` folder called `config.js`.
* Import Loki and create an instantiation of it:
```
var Loki = require('lokijs');
var db = new Loki('loki.json');
```
* Create a variable for each `collection` and add the addCollection method:
```
var posts = db.addCollection('posts');
```
* Add any dummy data with the `insert` method
* Export the collections at the end of the file after all of the dummy data: `
```
  module.exports = {
    posts: posts
  }
```
* Require the collection in whichever route file you are going to use:

```
  var posts = require('../db/config').posts;
```
* Access/manage the collection with the `find`, `insert`, `findAndUpdate`, and `findAndRemove`

<h2 id="router">How do I set up router files?</h2>
* Create `routes` folder in the main directory.
* Create a file for the resource that you want to CRUD. Example: `posts.js`
* Include these at the top of your file:
```
  var express = require('express');
  var router = express.Router();
```
* Create routes with prefix `router`, not `app`. If you want to send JSON back to the user, then use `res.send(someJSON)`. However, if you want to render an EJS page, then use `res.render('someFileName')`. Example:
```
  router.get('/', function (req, res) {
    res.render('index');
  });
```
* Export `router`. Example:
```
  module.exports = router;
```
* In `server.js`, require/import the routes files and assign them to their respective URLs. Example:
```
  var postsRoutes = require('./routes/posts');

  app.use('/posts', postsRoutes);
```
