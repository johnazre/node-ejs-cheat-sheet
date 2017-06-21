# node-express-ejs-cheat-sheet

## How do I get an express server up and running?
* Create a directory & cd into directory
* run `touch server.js` & `npm init -y`
* run `npm install --save express cors body-parser`
* Open directory in your text editor
* In server.js, type `expserv` and hit the `tab` button
* Fill in any of the urls that you would like to use or just delete all of the `app.get`, `app.post`, `app.patch`, and `app.delete`
* To run the server, run the command `nodemon server.js`

## How do I get EJS up and running?
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

## How do I set up LokiJS?
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
