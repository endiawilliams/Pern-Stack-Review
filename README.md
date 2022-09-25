![Node Logo](https://cdn-media-1.freecodecamp.org/images/1*DF0g7bNW5e2z9XS9N2lAiw.jpeg)

# Intro to Node

### Lesson Objectives
- Describe Node and Node Package Manager
- Set up a basic Node project
- Create, export, and import Node modules
- Use NPM to install and save node packages
- Describe what data is found in package.json

## The Client-Server Relationship
- What's the front-end (client side)?
  - Browser
  - User Interface (UI)
    - HTML, CSS, Javascript
- What's the back-end (server-side)?
  - data transactions/business logic
    - Create - sign up for a facebook account
    - Read - display all of your facebook friends
    - Update - change your facebook password
    - Delete - delete your facebook account
  - Why do we need a back-end?
    - efficiency and security
    - lighten up front end load
    - manage data securely

## What is Node?
Node is a platform that uses JavaScript for creating network and web applications.

But wait! Isn't Javascript a front-end language written for browsers? Yes! This is the beauty of Node. It gives us a server-side environment that can handle logic and code written in Javascript. In other words, it allows JavaScript to be run outside of the browser on a web server. 

This change in environment matters. We can't use `alert()` or `prompt()` anymore and if you've really gotten into JS nerdery, you'll notice our global scope no longer has the window or document objects. We'll see that there are functions and patterns unique to Node (for example, the require function in Node, which is not available in the browser).

## Setting up a Node Project
1. Create a new folder for your first node project.
  
  ```mkdir my-first-node-proj```
  
  Open the folder in your text editor.

2. Initialize Node inside the project folder.

  (check the command line prompt to make sure you're actually inside the project folder)

  ```npm init```

You will be prompted to enter values for a number of fields to set up the node project. You can just press enter to accept the default value, or enter specific values if you'd like.

To skip this step in the future (and accept all default values at once), type `npm init -y`.

Take a look at the `package.json` file that was just created. This is where the values we just set up via npm init are stored. This is like a settings file. You can edit these values by changing them in this file (make sure to save!).

3. Make your entry point.

Unless you specified a different file name in setup (check the value for "main" in `package.json`), Node will look for a file called index.js as the entry point for running your project. Node expects this file (or another file specified in `package.json`) to hold the code to be executed - this is the heart of your program. Create this file now.

```touch index.js```

Open the file in your editor. Let's write some code in here and run it to see Node in action! Write the following line to your `index.js`:

```console.log("Hello world!")```

4. Run your program!

To run a file in node via the command line, type `node [file name here]`.

`node index.js`

Congratulations, you've created and run your first Node program! Let's learn more about how Node is used in the wild (and eventually, in the web-development context).

# Modules in Node

## Creating, Exporting, and Importing Modules

Node's module system allows code written in one file to be exported, and then imported into other files. By importing a module (i.e. a specified section of code), we can then use that code as if it actually were written in the file we imported it to. 

Let's try an example!

### 1. Create your module.

Inside the `my-first-node-project` folder, create a javascript file called `myModule.js`.

In Node, `module.exports` is an object that will hold the code to be exported. We can use dot-notation to add the code we want to export to this object.

Add the following code to your `myModule.js` file:

```js
module.exports.beBasic = function() {
	return "That's so fetch.";
}
```

Now, our module.exports object has a key-value pair where the key is `beBasic` and the value is a function.

### 2. Import your module in `index.js`.

This is where the `require` function, specific to Node, comes into play. This function takes one argument: the path to the file that contains the module you are exporting.

In the `index.js` file, write the following code:

```js
const myModule = require('./myModule.js');

console.log(myModule.beBasic());
```

Run `index.js` via the command line:

`node index.js`

Voila! You've successfully created and imported a module!

Let's add some more code to our module. In `myModule.js`, add the following code:

```js
module.exports.beBasic = function() {
	console.log("That's so fetch.");
}

const count = function() {
	for (var i = 0; i <= 10; i++) {
		console.log(i);
	}
}
```

Now call this new count function from `index.js`:

```js
const myModule = require('./myModule.js');

myModule.beBasic();
myModule.count();
```

Try running this code in the command line:

```node index.js```

What happened? Why didn't this work?

_The exported module will only contain the code that is encapsulated in the_ ```module.exports``` _object!_

How do we get our `count` function to run? Make this happen.

Functions aren't the only things we can export! Try adding some other types of data to your module.

### Further Reading

To view a practical example of importing and exporting modules, read
[this article](http://www.sitepoint.com/understanding-module-exports-exports-node-js/). You'll see that we can export multiple functions by assigning `module.exports` to an object. This is a pattern that we'll see frequently in Node.

## Using Built-In Modules

It's great to have the flexibility to create our own modules, but Node supplies us with some simple built-in modules (aka "core modules") that are ready for us to import and use!

### Example: fs module

We will use the `fs` core module (it stands for "file system") to read a text file. 

Create a `story.txt` text file inside your project directory and write a short story inside it.

Core modules just need to be imported using the `require` function.

Write the following code to your entry point file:

```js
const fs = require('fs');

fs.readFile('story.txt', 'utf8', function(err, data){
	if(err) {
		console.log("There was a problem reading the file.");
	} else {
		console.log(data);
	}
});
```

Run `index.js` to read your story in the terminal!

For more on the `fs` module, see [w3schools](https://www.w3schools.com/nodejs/ref_fs.asp).

Try adding to your story using `fs.write()`.

### Exercise: HTTP core module

In this excercise, you will make a Hello World app from scratch by using the the HTTP core module to spin up an [HTTP server](https://www.quora.com/What-is-an-HTTP-Server-and-what-does-it-do).

![HTTP Request and Response Diagram](https://qph.fs.quoracdn.net/main-qimg-7cf2f16f34b9cdd2652abcf17f85555d)

1. Create a `hello-node` directory.
2. Initialize Node in this directory.
3. Create your entry point file.
4. Import the `http` module into your entry file. (Hint: use the `require` function)
5. Create an http server that listens to `port 8000` and writes `Hello, World!` to the client. (Hint: look up the core http module on [w3schools](https://www.w3schools.com/nodejs/nodejs_http.asp))
6. Run the server using the command `node index.js`.
7. Check to see that your program is working by visiting `localhost:8000` in your browser.

#### Finished Code

<details>
  <summary>index.js</summary>
  	<br>
	const http = require('http')
	<br><br>
	http.createServer(function(req, res){
	<br>
	&nbsp;&nbsp;res.write('Hello, World!')
	<br>
	&nbsp;&nbsp;res.end()
	<br>
	}).listen(8000)
</details>

# Node Package Manager

There are three types of Node modules:
1. Core Modules (like ```fs```)
2. Local Modules (that you create)
3. Third Party Modules

Core modules are great for gaining quick access to commonly-needed functionality in your program, and local modules allow you the flexibility to build out whatever tools you might possibly need, but third party modules, which fall somewhere in between, are perhaps the most exciting modules of them all!

### Node Packages

Because developers are awesome, there are hundreds of thousands of already-written modules out there, ready for use! Each of these modules are encapsulated in a ***Node Package*** and made available via ***Node Package Manger*** or ***NPM***, for short. A node package is a folder that contains one or more modules, a ```package.json``` file, and any meta-info needed to make the modules work correctionly and play well with your node program.

### NPM

NPM is the largest open-source software registry in the world. It includes a website, a registry of Node Packages, and a command line interface that allows us to easily incorporate packages into our programs.

Check out this [NPM Intro Video](https://www.youtube.com/watch?v=x03fjb2VlGY)

The NPM CLI makes incorporating a node package into your program fairly easy, but you can refer to [this playlist](https://www.youtube.com/watch?v=pa4dc480Apo&list=PLQso55XhxkgBMeiYmFEHzz1axDUBjTLC6) if you ever get lost. It includes a whole series of videos that demonstrate the fundamentals of using NPM.

The NPM CLI installed automatically on your machine when you installed Node. Verify this now by checking the version in your terminal:
```npm -v```

### First Node Package: Nodemon

[Nodemon](https://www.npmjs.com/package/nodemon) is a package that makes developing node apps easier. It restarts the application everytime you save changes to your code.

We will use Nodemon quite a bit, so instead of installing it on each node app we build, we will install it globally. This will make it accessible to all of our node apps.

In the command line, type the following code:
```npm install -g nodemon```

Since we're installing it globally (that's where the ```-g``` flag comes in), it doesn't matter what directory we're in.

Let's see nodemon in action! Try running your ```my-first-node-app``` using nodemon. Simply ```cd``` into the directory, then run ```nodemon```. Nodemon knows to run the file that corresponds to ```main:``` in your ```package.json```.

Now open up ```my-first-node-app``` in sublime. Add the following code to ```index.js```:

```js
var i = 0

var myTimer = setInterval(count, 1000)

function count() {
	console.log(i)
	i++
}
```

Make sure to save the file and check out what's happening in your terminal!

Now change the ```count``` function to print ```i*2``` instead of just ```i``` and save. 

You can always restart nodemon by typing ```rs```.

To quit nodemon (and any program running in the terminal), press CTRL+C.

***Congratulations***, you've just installed and used your first third party node module!

We installed nodemon globally, but most node packages will only be useful for specific projects. In this case, when you run ```npm install [package name]``` you want to make sure you're inside the directory of the project you want to use the package in, and leave off the ```-g``` flag.

## Using a Third Party Module

#### Introducing Moment: A Date/Time Format Module

Moment is a date formatting module. Believe it or not, representing dates and time in Javascript is tricky. Just look at the output of using the Date class natively.

```js
console.log(new Date())
// Prints: Fri Apr 05 2019 09:58:38 GMT-0700 (Pacific Daylight Time)
```

Instead of the mess of text that comes out when you create a regular date with JavaScript using the date class, we can pretty-print the date in a human readable way.

#### Install Moment

1. Go to your terminal 

2. Make sure you're in the top level of your `my-first-node-app` folder

3. Type the command `npm install moment`

4. When the command is finished, go back to your text editor

5. Make sure there is a folder called `node_modules` in the top level of your `my-first-node-app` folder

#### Use Moment in a Node App

* Open `index.js` in your text editor

* Require the moment library at the top of `index.js` and assign it to a variable called `moment`

* Take a look at [Moment's Docs](http://momentjs.com/). There are a lot of things you can do with this module!

* Let's use the moment module to print a date! Add the following code to your `index.js` file:

```js
console.log(moment().format("MMM Do YYYY"))
```

* What does this print? You should have seen whatever today's date was in the format: 3-letter month, numerical day plus ordinal, and 4-digit year. For example: 

```
Apr 15th, 2020
```

* Next challenge: Use moment to pretty-print your birthday. Use the fully spelled out month, day of the week, escaped text for words such as `the` and `of`, and 4-digit year. For example:

```
Wednesday the 11th of September in the year 1985
```

* BONUS: Use moment's `.fromNow()` function to print just how many years ago that birthday was!

<details>
    <summary>Solution Code</summary>
<br>
var moment = require('moment')
<br><br>
// Prints today's date
<br>
console.log(moment().format("MMM Do YYYY"))
<br><br>
// Prints my birthday
<br>
console.log(moment('09-11-1985', 'MM DD YYYY').format("dddd [the] Do [of] MMMM [in the year] YYYY"))
<br><br>
// Prints how long ago my birthday was
<br>
console.log('Oh boy, that was', moment('09-11-1985', 'MM DD YYYY').fromNow(), 'years ago!')
</details>

#### Git Ignore File

Before we get too much further, **WAIT**! 

Take a look at the `node_modules` folder that got generated when you used the `npm install` command. How big is this folder? How many files are in it? What's going on?

In general, we keep track of the version of the module that we are using in a file called `package.json`. This means we can just redownload the modules based on the version number on any new computer we want to put our code on - be that a fellow developer's computer or a production server. A package.json file might look something like this:

```js
{
  "name": "node-introl",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "moment": "^2.24.0"
  }
}
```

> Notice there is a "dependencies" section which lists our 3rd party dependencies. Right now we just have one, but others we install will go here, along with their version numbers in alphabetical order.

So, because we can just re-install the appropriate packages, we actually don't *need* to have the `node_modules` folder to be tracked by git at all! In fact, the node_modules folder can get so huge and unweildy that it's greatly preferred that you **DO NOT** push them up to github nor track them with version control! In fact, this can also cause serious errors during deployment!

**How can we avoid this?!**

We can specify directions to git about which files it should ignore by creating a file called `.gitignore`. Yes, the `.` at the front is necessary!

A `.gitignore` file will contain a list of files and folders that git should NOT be tracking. Go ahead and make a `.gitignore` file now and put `node_modules` into it as the first line.

```
# .gitignore
node_modules/
```

Congrats - now when you add git tracking to this folder, it will not track the node_modules folder and will not push it to github! 

Other common things to ignore for git are things like `.env` files which contain localized settings and possibly sensitive data like secret keys, salts, or API keys. Thus leading to this pro-tip:

> Life Pro Tip: .gitignore should be one of the first files you create in a project! Create it before you do a single check-in. Always. Don't be the developer who oopsed and put an API key in public. 

# Introduction to Express

## Objectives
* Describe what Express is and how it works with Node.
* Create Express routes that utilize parameters and form middleware
* Contrast and implement different HTTP verbs through Express routes
* Implement and explain the components of a basic Express app

## Express

_Express is a light-weight, web application framework for writing RESTful APIs in Node.js._

We'll get to the _RESTFUL API_ part soon, but for now, think of Express as a Node Package that gives us some extra tools for creating a web application using Node.

Let's create our first Node/Express app!

## Our first Express App

### 1. Create a new directory for your project.
```bash
mkdir hello-express
```

### 2. Initialize Node
```bash
cd hello-express
npm init
```

### 3. Install Express
```bash
npm install express
```

***Pause!*** Open your project file tree in your text editor and notice the new files/folders that appear.

#### node_modules
Each time you use npm to install a new package, this folder will populate with the package you installed, _along with all the dependencies of that package_. That's why you'll see several files that look like they have nothing to do with the package you were trying to install. They are helper packages for the one you're going to use! More on this folder [here](https://docs.npmjs.com/files/folders).

#### package-lock.json
This file keeps track of your npm install history. As we just learned, when we use npm to install a package, there may be several other dependencies installing behind the scenes. Think of package-lock.json as the commit history for this activity. More on this file [here](https://docs.npmjs.com/files/package-lock.json).

_No need to mess with any of these automatically generated files! NPM takes care of the modifications/additions for you each time you install/uninstall a package._

### package.json:
Revisit the package.json file. Notice that express and the version number now shows up in the dependencies field. All third party modules will be listed here automatically when you use npm to install them (but the dependencies of _those_ files will not be listed here).

### 4. Create your entry point file.
```bash
touch index.js
```

### 5. Import the Express module

***index.js***
```js
var express = require('express');
```

### 6. Create an instance of an express app

***index.js***
```js
var express = require('express');
var app = express();
```

### 7. Create a Home Route

***index.js***
```js
var express = require('express');
var app = express();

app.get('/', function(req, res) {
	res.send('Hello, World!');
});

app.listen(8000);
```

We'll learn more about this code in the next part of the lesson. For now, just copy it down.

### 8. Run nodemon
```bash
nodemon
```

Now visit localhost:8000 in your browser. ***Congratulations!*** You've just built your first express app!

<hr> 

# Routes

A **route** is a combination of a ***URL pattern*** and an ***HTTP Verb***.

### URL Pattern
The URL Patterns refer to everything that comes after the base URL (the slash and anything that follows). For example, let's look at a simple website - go to http://www.lemon-fol.io . You're looking at the home route. Now click on "projects" in the nav bar, or add /projects to the end of the URL in the URL bar. In this scenario, everything _before_ /projects is the base URL. The base URL alone took you to the home route ("/") which served the home page. The URL pattern "/projects" served different files.

Let's look at a more complex example. Go to reddit.com and search for "cute puppies". Notice what appears in the URL bar: 
<em>https://www.reddit.com/search?q=cute%20puppies</em>

Let's break this down:
* Base URL (consists of the protocol (https) and the domain (www.reddit.com)):
<em>https://www.reddit.com</em>
* URL Pattern (think of as directories of the web app):
<em>/search</em>
* Query String (a key=value way of sending data with the request):
<em>?q=cute%20puppies</em>

In this situation, the URL pattern would look something like "/search". When the request arrived in our route handler function, we would have access to the query string key-value pairs as part of the `request` object. More on this a bit later...

URL Patterns will become clearer as we get into some examples.

## HTTP Verb

There are 4 main HTTP verbs:
* GET
* POST
* PUT
* DELETE

These verbs represent a _method_ for the request. In other words, they tell the server what the nature of the request from the client is.

| HTTP Verb     | CRUD          | Example  |
| ------------- |:-------------:| -----------------:|
| GET           | READ          | Look at someone's profile on LinkedIn |
| POST          | CREATE        | Post on LinkedIn |
| PUT           | UPDATE        | Change your bio on LinkedIn |
| DELETE        | DELETE        | Delete a photo from LinkedIn |


## Backtrack: hello-express

Let's circle back to our home route in our `hello-express` project and break the code down a little more to see how routes look in express.

Here we have imported the express module, and created an instance of an express application called _app_. This code comes straight from the express [docs](https://expressjs.com/en/guide/routing.html).

```js
const express require('express');
const app = express();
```

Next, we created a home route. Here, the HTTP verb is ***get***, which we indicate using the express method, `get()`. This method takes two parameters, (1) a URL Pattern and (2), a callback function that tells the app what to do when this route is reached.
```js
app.get('/', function(req, res) {
  res.send('Hello, World!');
});
```

The URL pattern '/' simply denotes the base URL or root of the app. This is almost always the directory where you initialized npm and git but can be different when you deploy it to a platform service.

The last line of code in our program, `app.listen(8000)` tells our app to listen to port 8000. This is the actual "place" in the network layers of our operating system where the request will come in. After this starts, the full base URL of our app will be http://localhost:8000.

***The combination of the URL Pattern '/' and the HTTP verb 'get' ensures that this route will be reached when a GET request made by the client from the base URL.***

If you'd like, you could pull out the callback function to get even more visual clarity on what is happening here. (Run nodemon to convince yourself that this does not change any functionality of the program.)

```js
function hello(req, res) {
  res.send('Hello, World!');
}

app.get('/', hello);
```

By design, the express `get()` function will pass two arguments into the callback function: (1) the request object and (2) the response object. That is why we define a callback function with two parameters.

## The Request and Response Objects

Our callback functions for our routes (which are sometimes referred to as **Controllers**) receive two very special objects from Express. They are provided to our function very much like the `e` object holding all the event data is passed into our event listeners, or like each item in an array is passed into our `forEach()` callback.

### request
The Request object, frequently abbreviated to `req`, contains all the data we would ever need about the actual request that came in. What are they requesting? What browser are they using? Bunches of other stuff. But mostly we will using three keys inside of it:

* `req.body` - this is where any submitted form data will be stored for us.
* `req.params` - this is where special route variables are stored for us.
* `req.query` - this is where the query string data is stored.

As you can see, most of the time, if we are accessing the `req` object, its because we need to get at some data being sent to us from the user.

### response
The Response object, or `res` for short, is what we use to send something back to the user's browser, or more formally, send a response to the request. There are a number of functions we can use:

* `res.send()` - sends back a simple string. Not really used in production. This is kind of like the `console.log()` for network requests. Good for testing if the route is working.
* `res.sendFile()` - more sophisticated in that it can send an entire file back but file is static.
* `res.render()` - used to render data into templates with the selected template engine. More on this later.
* `res.json()` - used to send object data back as JSON. Very common when writing a backend API. Much more on this later.

You'll get more comfortable with all of this as we do more examples.

## 2nd Express App: Fun With Routes

### Set up the project

#### 1. Create a new directory called route-fun
```bash
mkdir route-fun
```
#### 2. Initialize Node
```bash
cd route-fun
npm init
```
#### 3. Install Express
```bash
npm install express
```
#### 4. Create entry point
```bash
touch index.js
```
#### 5. Create an instance of express
***index.js***
```js
const express = require('express');
const app = express();
```
#### 6. Establish the base URL
***index.js***
```js
const express = require('express');
const app = express();

app.listen(8000);
```

#### 7. Write a home route

```js
const express = require('express');
const app = express();

app.get('/', function(req, res) {
  res.send("You've reached the home route!");
});

app.listen(8000);
```

Run nodemon and visit localhost:8000 to make sure everything is working.

### More Route Styles

#### Paths

Now let's try adding another route that has the URL pattern of a string after the root slash:
```js
app.get('/', function(req, res) {
  res.send('You've reached the home route!');
});

app.get('/about', function(req, res) {
  res.send('This is a practice app to learn about express routes.');
});
```

Visit `localhost:8000/about` to view the response from this route. We have made a "directory" in our app that will deliver the results of a different function whenever someone hits our site's `/about` URL.

This is one of the primary ways in which we organize our site. Every part of our site **should** be bookmarkable in a browser - which means that each section needs a distinct URL. This is how we make our web server respond to different URLs.

#### Parameters

We can also pass variables in as part of a URL. By putting a colon before a string in our route, we can create routes with different variables, or **parameters**. These parameters are automatically pulled out for us by Express and can be accessed via the `req.params` object.

```js
app.get('/', function(req, res) {
  res.send("You've reached the home route!");
});

app.get('/about', function(req, res) {
  res.send('This is a practice app to learn about express routes.');
});

app.get('/:input', function(req, res) {
  res.send("Our parameter is " + req.params.input + ".");
});
```

We can name them whatever we like. The string we use after the colon will be the name of the key added to the `req.params` object which will contain whatever the user typed in there after the root slash.

We can combine parameters and paths.
```js

app.get("/greet/:name", function(req, res) {
  res.send("Hello " + req.params.name + "!");
});
```

And we can have more than one parameter:
```js

app.get("/greet/:name/:lastname", function(req, res) {
  res.send("Hello " + req.params.name + " " + req.params.lastname);
});

app.get("/multiply/:x/:y", function(req, res) {
  res.send("The answer is: " + (req.params.x * req.params.y));
});

app.get("/add/:x/:y", function(req, res) {
  res.send("The answer is: " + (req.params.x + req.params.y));
});
```

Wait, what happened with that last route?? URL parameters come in as strings, so Javascript just concatonated them instead of treating them as integers and adding them. We can fix that:

```js

app.get("/add/:x/:y", function(req, res) {
  res.send("The answer is: " + (parseInt(req.params.x) + parseInt(req.params.y)));
});
```

Say we want to add any number of integers together. We could use wildcard route, denoted by an asterisk!

First let's take a look at how the asterisk works:

```js
app.get("/add/*", function(req, res) {
  res.send(req.params);
});
```

Now let's split up the wildcard parameter and sum using _reduce_:
```js
app.get("/add/*", function(req, res) {
  const myParams = req.params[0].split("/");
  const result = myParams.reduce(function(total, num) {
    return total + parseInt(num)
  }, 0);
  res.send("The answer is  " + result);
});
```

### Query Strings

One last thing we can do in our routes is pass in a special set of key-value pairs as the last part of the URL. They are called query strings because they are typically only included with GET requests which are conventionally used to query data from some source. The query string gives us a way to pass in additional parameters to the query.

In the following URL:

`https://www.domain.com/some/data?key1=value&key2=value2`

The query string starts at the question mark (?) and goes through the end of the URL. The syntax is `key=value`. If you need more than one pair, they can be separated with ampersands (&) as you see above.

Let's add a new route where we can play with this. After all the other routes but before the line that starts the server listening, add a new route:

```js
app.get("/querystring", function(req, res) {
  let printout = '';
  for (let key in req.query) {
    printout += key + ": " + req.query[key] + "<br />";
  }
  res.send("Here's what they sent: <br /><br />" + printout);
});
```

As you can see, we don't need to do anything special to our URL pattern. Any route that we make can accept a query string. All we need to do is look inside of `req.query`. This one will loop over the `req.query` object to see if it has anything and will print whatever keys it finds. We can test it by hitting our server in a browser window: `http://localhost:8000/querystring?name=Steve&food=tacos`. Try replacing those key-value pairs or adding some more.

## Conclusion

In this example, we focused on the URL patterns. The HTTP verbs will come into play more when we start working with true CRUD functionality. For now, everything is a GET request.

# Getting started with Sequelize

## Objectives
* Identify an ORM
* Weigh pros and cons between ORMs and raw SQL queries
* Use the Sequelize CLI to create and migrate models
* Utilize Sequelize to create, find, and delete database records
* Explain the purpose of promises and their use in Sequelize

We learned the basics about relational databases (PostgreSQL) and used SQL to query from databases. Now, we're going to incorporate a relational databse into an Express application. But first, some terminology.

## Key terms + definitions

#### ORM

An ORM (Object Relational Mapper) is a piece/layer of software that creates a map between our database into javascript objects that represent our data. This means we can just use JavaScript to create and work with our data instead of writing raw SQL queries.

You can read some more about the benefits of using an ORM [here](http://stackoverflow.com/questions/1279613/what-is-an-orm-and-where-can-i-learn-more-about-it)

**Exercise:** What are 3 pros of an ORM? What are 3 cons?

#### Sequelize

From the Sequelize docs "To put it in a nutshell, it's an ORM (Object-Relational-Mapper). The library is written entirely in JavaScript and can be used in the Node.JS environment." In other words, Sequelize is an ORM that works with relational databases and Node.js. It allows us to do many things including:

- Represent models and their data.
- Represent associations between these models.
- Validate data before they gets persisted to the database.
- Perform database operations in an object-oriented fashion.

#### Model

A model is a javascript object that maps to a data relation (table). You can think of a model as the blueprint for what each row of data is going to contain. Each instance of your model represents one row of data. The ORM allows you perform CRUD on instances of your models which will then map to the equivalent changes in your database.

#### Migration

Migrations (also known as 'schema evolution' or 'mutations') are a way of changing your database schema from one version into another. A migration lays out a plan to change your _model_. When the migration is _run_, it changes your model _and_ uses your ORM to map those changes into your database so your database is alterred accordingly.

# Setup

## Setup part 1 - getting the sequelize-cli tool (you only have to do this once)

We need install a generator so we can use sequelize. Much like our other terminal apps, we will only install this once.

```
npm install -g sequelize-cli
```


### Setup part 2 - starting a new node project

Let's build our first app using Sequelize! First we need to create a node app and include our dependencies. **All in terminal**:

Create a new folder and add an index.js and .gitignore and initialize the repository

```
mkdir userapp
cd userapp
npm init
touch index.js
echo "node_modules" >> .gitignore
```

Add/save dependencies (sequelize needs pg for Postgres)

```
npm install express ejs pg sequelize
```

Create a database and initialize a sequelize project

```
createdb userapp
sequelize init
```

#### For your historical reference...

**WARNING (2017) Edited (2018):**
At one point, sequelize-cli, sequelize, and pg modules were not playing nicely with each other. Luckily, this issue (for version Sequelize 4) has been resolved and we can resume using the current versions of both. In the future, be mindful that many modules you use are maintained by individual third parties and issues like this may come up! 

If you used to use Sequelize 3, keep in mind that Sequelize 4 has breaking changes! If you need to upgrade your app, refer to these [docs](http://docs.sequelizejs.com/manual/tutorial/upgrade-to-v4.html#breaking-changes), which guide you in the update process.

### Setup part 3 - config.json, models and migrations:

In sublime we should now see a bunch of new folders. We now have config, migrations and models. This was created for us when we ran `sequelize init`.

Let's start in the config folder and open up the config.json file. This file contains information about the database we are using as well as how to connect.

We have three settings, one for development (what we will use now), test (for testing our code), and production (when we deploy our app on AWS/Heroku).

Let's change the config.json so it looks like this.

**config/config.json**

```js
{
  "development": {
    "username": "< your postgres username here >",
    "password": "< your postgres user's password >",
    "database": "userapp",
    "host": "127.0.0.1",
    "dialect": "postgres"
  },
  "test": {
    "username": "< your postgres username here >",
    "password": "< your postgres user's password >",
    "database": "userapp_test",
    "host": "127.0.0.1",
    "dialect": "postgres"
  },
  "production": {
    "username": "< your postgres username here >",
    "password": "< your postgres user's password >",
    "database": "userapp_production",
    "host": "127.0.0.1",
    "dialect": "postgres"
  }
}
```

> Note: Remove the angle brackets from the username and password sections

The only thing we are actually changing for database setup, is the **database name**. If you have a username and password for your Postgres server, you'd include those as well.

When we deploy to Heroku (a hosting service for full stack apps), they will provide us a long url that contains password and login that will be secure when deployed. More on this later.

Once this is complete, let's move to the models folder.

## Creating a model and a matching migration

In order to create a model, we start with `sequelize model:create` and then specify the name of the model using the `--name` flag. Make sure your models are **always** singular (table name in plural, model name in singular). After passing in the `--name` flag followed by the name of your model, you can then add an `--attributes` flag and pass in data about your model. Generating the model also generates a corresponding migration. You only need to do this once for your model.

```bash
sequelize model:create --name user --attributes firstName:string,lastName:string,age:integer,email:string
```

> Make sure you do **not** have any spaces between each of the attributes and their data types. Convention matters!

If you want to make changes to your model after generating it - all you have to do is make a change and save it before running the migrate command.

This will generate the following migration

**migrations/\*-create-user.js**

```js
'use strict';
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('users', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      firstName: {
        type: Sequelize.STRING
      },
      lasName: {
        type: Sequelize.STRING
      },
      age: {
        type: Sequelize.INTEGER
      },
      email: {
        type: Sequelize.STRING
      },
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE
      },
      updatedAt: {
        allowNull: false,
        type: Sequelize.DATE
      }
    });
  },
  down: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('users');
  }
};
```

And a corresponding model:

**models/user.js**
```js
'use strict';
const {
  Model
} = require('sequelize');
module.exports = (sequelize, DataTypes) => {
  class user extends Model {
    /**
     * Helper method for defining associations.
     * This method is not a part of Sequelize lifecycle.
     * The `models/index` file will call this method automatically.
     */
    static associate(models) {
      // define association here
    }
  };
  user.init({
    firstName: DataTypes.STRING,
    lasName: DataTypes.STRING,
    age: DataTypes.INTEGER,
    email: DataTypes.STRING
  }, {
    sequelize,
    modelName: 'user',
  });
  return user;
};
```

## What is this "associate" thing in my model?

In this function, we specify any relations/associations (one to one, one to many or many to many) between our models (hasMany or belongsTo). We'll discuss this more, but always remember, the association goes in the model and the foreign keys go in the migration.

## Running the migration

To run the migration, use the following command.

```
sequelize db:migrate
```

> If you get an error after running the command above, look at your config.json file and search for typos, making sure the database name, your postgres username, and password are all spelled correctly.

If you need to undo the last migration, this command will undo the last migration that was applied to the database.

```
sequelize db:migrate:undo
```

## Using your Models inside an app

Just like using express, body-parser, and the other modules, your models must be required
in order to access them in your app.

```js
var db = require("./models");
db.user.create({
  firstName: 'Brian',
  lastName: 'Hague',
  age: 99
}).then(function(data) {
  // you can now access the newly created task via the variable data
});
```

### CRUD with Sequelize (Using our User model)

#### Create

```js
db.user.create({
  firstName: 'Brian',
  lastName: 'Hague',
  age: 99
}).then(function(data) {
  // you can now access the newly created task via the variable data
});
```

#### Read One

```js
db.user.findOne({
  where: {id: 2}
}).then(function(user) {
  // user will be an instance of User and stores the content of the table entry with id 2. if such an entry is not defined you will get null
});
```

#### Find or Create

The method `findOrCreate` can be used to check if a certain element is already existing in the database. If that is the case the method will result in a respective instance. If the element does not yet exist, it will be created with the provided attributes (a combination of `where` and `defaults`).

In current versions of Sequelize, the library has better support for JavaScript promises and uses them to return results from the database asynchronously. Promised are a part of the language that we're introducing today but will go over in more depth during the React unit. Here is an example of `findOrCreate` in action:

```js
db.user.findOrCreate({
  where: {
    firstName: 'Brian',
    lastName: 'Smith'
  },
  defaults: { age: 88 }
}).then(function([user, created]) {
  console.log(user); // returns info about the user
});
```

We are using the standard `.then()` promise function to run some code once our database returns what we queried for - it's called a promise because our initial request to the database will take some time and so the function "promises" to return a result one war or another. We can get that response inside that promise callback function, where we wrap our two variables in a literal array and pass it as a paramter to the callback function. This will achieve the same effect of providing both the data and the boolean to your promise handler function. 

This will probably be the preferred way of doing this in future versions of Sequelize since the `.spread()` function is actually a feature of another node module called Bluebird. If Sequelize can move away from requiring a 3rd party library, they probably will want to do that so favor the `.then()` way of using it moving forward.

#### Find All

findAll returns more than one instance, which is useful if you need more than one record. find only returns one record.

```js
db.user.findAll().then(function(users) {
  console.log(users);
  // users will be an array of all User instances
});
```

#### Update

```js
db.user.update({
  lastName: 'Taco'
}, {
  where: {
    firstName: 'Brian'
  }
}).then(function(user) {
  // do something when done updating
});
```

#### Delete (destroy)

```js
db.user.destroy({
  where: { firstName: 'Brian' }
}).then(function() {
  // do something when done deleting
});
```

### Promises
After a sequelize statement, we can interact with the return of that object using `.then` and in `findOrCreate` we can use `.spread`.

Finding a user

```js
db.user.findOne({where: {id: 1}});
```

This will execute a statement to find a user, but it will not let us interact with it. Because of the asynchronous nature of a call, we need to use a Promise (a type of callback) to get that data.

```js
db.user.findByPk(1).then(function(foundUser) {
  console.log(foundUser);
  //res.send("myTemplate", {user: foundUser);
});
```

In a `findOrCreate`, a callback will return back an array, instead of a single object. There is a type of callback called `.spread` which will allow us to break apart that array and use similar to a traditional callback.

```js
db.user.findOrCreate({
  where: { firstName: 'Brian' }
}).spread(function(user, created) {
  console.log(user); // returns info about the user
});
```

But as mentioned above, it looks like this syntax will be replaced with more standard promise syntax moving forward. THis would be the new way to use the `findOrCreate` promise:

```js
db.user.findOrCreate({
  where: { firstName: 'Brian' }
}).then(function([user, created]) {
  console.log(user); // returns info about the user
});
```

## Sequelize Promises

The main callback handlers to be used are as follows.

* `.then` - default promise called when a query is completed.
* `.spread` - used to spread an array of values to parameters. This is only used for `findOrCreate` on old versions of Sequelize. This method isn't used in the official documentation but you might it floating around stack overflow posts as little as 1 year old.
* `.catch` - triggered if something goes wrong (an error).
* `.finally` - triggered after all other callbacks. Can be used for cleanup.

The important thing to remember is that all queries take time and are asynchronous, so you MUST use promises to execute code that needs to happen after the query is completed. You will usually use `then`, except possibly for `findOrCreate` (but only if you need to support old versions.)

## Useful Sequelize Documentation Links
* Models
  * [Data types](http://docs.sequelizejs.com/en/latest/docs/models-definition/#data-types)
  * [Validations](http://docs.sequelizejs.com/en/latest/docs/models-definition/#validations)
  * Note that Sequelize **expects the model to be singular**, and uses a pluralizer module to determine what the pluralized model should be. If you're unsure what the pluralizer will output, use this handy app to see what the pluralized model will be. [http://plural-test.herokuapp.com/](Plural Test)
* Querying
  * [Query usage (comparable to SELECT, INSERT, COUNT, MAX, etc.)](http://docs.sequelizejs.com/en/latest/docs/models-usage/)
  * [Destroying records (comparable to DELETE)](http://docs.sequelizejs.com/en/latest/docs/instances/#destroying-deleting-persistent-instances)
  * [Attribute selection](http://docs.sequelizejs.com/en/latest/docs/querying/#attributes)
  * [Querying Basics and Operators (comparable to AND/OR/LIKE/IN)](http://docs.sequelizejs.com/en/latest/docs/querying/#basics)
  * [Pagination and Limiting (comparable to OFFSET, LIMIT)](http://docs.sequelizejs.com/en/latest/docs/querying/#pagination-limiting)
  * [Ordering (comparable to ORDER BY)](http://docs.sequelizejs.com/en/latest/docs/querying/#ordering)
* Configuration and Commands
  * [Sequelize CLI and Migrations](http://docs.sequelizejs.com/en/latest/docs/migrations/#the-cli)

# Frontend Setup in Express

## Setup
#### 0. 
Do a basic express app setup. If you need step by step instructions, look at one of our previous lessons. You should install the npm packages `express` and `ejs`
- Add a home route that renders an `index.ejs` file with some boilerplate HTML.

#### 1. 
Set up your static files and folder structure.
- Create public folder in top level folder
- Put the following line of code in your `index.js`

```javascript
app.use(express.static(__dirname + '/public/'));
```

- Inside the public folder, create folders `css`, `js`, `images`.

#### 2. 
Create some frontend files and place them in the appropriate file. You'll need a `style.css` file, a `main.js` file, and pick a random image from the internet or your computer to copy into the `images` folder.

#### 3. 
Link the CSS file
- in the head of `index.ejs` file, add the line:
```html
<link rel="stylesheet" href="css/style.css">
```
- add a style rule to the CSS file to test the connection. Something like this:
```css
body {
    background: goldenrod;
}
```

> If you don't see the background colour change in your browser, check the `href` attribute of the link tag, then make sure the CSS file was saved, then make sure the `express.static()` line from step 1 is copied exactly. You got this!

#### 4. 
Link the JS file and display the image in an `<img />` element added to `index.ejs`.
- Take 5 min. and use what you know so far to try and figure it out and don't forget to use the docs or other resources. We'll take this up as a class afterward.

# What is React Really??
Our learning objective in this lesson is to understand the design pattern behind React. After this lesson you will understand the how to build ui in three different ways: Static, Vanilla Js Dynamic Generation, and lastly React.

## Static Built UI

Let's build out some UI statically. For this practice we will be using [Codepen](https://codepen.io) as a playground.

```html
<div class="hero">
  <h1>Batman</h1>
  <p>I'm Batman!</p>
</div>

<div class="hero">
  <h1>Superman</h1>
  <p>Up, Up and Away!</p>
</div>
```

```css
.hero {
  display: inline-block;
  margin: 10px;
  border: 1px solid #eee;
  box-shadow: 0 2px 2px #ccc;
  width: 200px;
  padding: 20px;
}
```

This works if we have just some simple static information we need to display on the page, but what about dynamic data? What if we need this structure to repeat over and over with different values? 

## Dynamically Built UI

One option is through Js. Let's build this out dynamically with just JS before we tackle this with React. 

Let's remove the html elements and we will use JS to build out our UI.

### State

First we will start out with a **state** object that will hold our heroes. **State** is a term we use to hold values that represent information about our UI.

```jsx
const state = {
  heroes: [
    {
      name: 'Batman',
      catchphrase: "I'm Batman"
    },
    {
      name: 'Superman',
      catchphrase: "Up, Up and Away!"
    }
  ]
};

```
### Render 

Now that we have some data to work with we can start to build out our UI. For this we will be creating a render function to use the state we created.

```jsx
const render = () => {
  const ui = state.heroes.map(hero => {
    return `<h1>${hero.name}</h1>`
  }).join(" ")
  document.body.insertAdjacentHTML('beforeEnd', ui)
};
```

*NOTE: Dont't forget to invoke your render function!*

This function creates our UI by maping through the data and for every object in the array it will return a joined array of the object name values as headers. It will then take those names and append them to the dom. 

### Components

Now this works, but if our UI starts to get bigger and more complex (which it usually does) we will need break out our template into its own function. This is the underlying concept to **Components**.

For this example we will build out what we call a presentational component (more on this later) that will simply build out the tempate html and return it to our mapping.

```jsx
const heroComponent = props => {
  return `<div class="hero">
              <h1>${props.name}</h1>
              <p>${props.catchphrase}</p>
        </div>`
};
```

Our function (aka component) is recieving props. This is simply the data we are passing into the function for our component. The component then builds a string of the UI and returns it. Let's now replace the header in our render method with the heroComponent function passing in the hero data.

```jsx
const render = () => {
  const ui = state.heroes.map(hero => {
    return personComponent(hero)
  }).join(" ")
  document.body.insertAdjacentHTML('beforeEnd', ui)
};
```

Now this works! We can clearly see our content rendering on the Dom. This is at the simpliest of breakdowns what react is all about. 

## The React Way

React is a javascript library that allows us easily build single page applications and break our UI up into small reusable components. Let's convert our application into a React application. For now remove all of your js code since we will be replacing it with React Code.

*For codepen we will bring in our react library by hitting settings and typing `react` and `react-dom` from the quick add search bar. Make sure you set `babel` as your JavaScript Preprocessor*

### React Functional Component

First thing that we will do is create a react component. 

```jsx
const Hero = () => {
  return (
    <div class="hero">
      <h1>Batman</h1>
      <p>I'm Batman!</p>
    </div>
  )
};
```

Take note of the capital Hero. In react we define components with a capital letter becasue they are constructor functions.

But wait.. There's HTML in my JS! And it's not a string! 

This is because we are actually using what is called JSX with allows us to write HTML style syntax that will be converted by React for us. We will be diving deeper into JSX in the next lesson. For now know that it is a way for us to write HTML style syntax in our JS.

Let's get this Component on our Dom! 

At the bottom of our js add the following..

```jsx
ReactDOM.render(<Hero/>, document.querySelector('#app'));
```

WHOA! There's that render again! This line is allowing react to add the Person component to the dom via selecting a div with id of app. We dont have this yet so let's add it to the html.


```html
<div id="app"></div>
```
And just like that our Hero Component is in our view.

But wait.. 
Why does Hero look like an HTML element? 
JSX hard at work again. For now let's get familiar with the syntax and in the next lecture we will dive deeper into how it works behind the scenes.

### Props for Dynamic Components

For now our component does not really do anything besides render out some html. With props we can pass information into our component to change its content.

Let's add props into our Person Component.
```jsx
const Hero = props => {
  return (
    <div class="hero">
      <h1>{props.name}</h1>
      <p>{props.catchphrase}</p>
    </div>
  )
}
```

Esentially props is an object that is passed into our function that looks like this: 

```js
props = {
    name: 'Batman'
    description: "I'm Batman!"
}

Hero(props)
```

So how do we pass this information in Hero if Hero looks like HTML? The same as how we add properties to normal HTML elements. (That's why JSX is so cool!)

```js 
ReactDOM.render(<Hero name="Batman" description="I'm Batman!"/>, document.querySelector('#app'))
```

And with that we can see our properties on the DOM!

### Dynamically Generating Multiple Components

As of right now we are only appending a single component to the page. But we need to be able to ultimately append as many as we want with whatever data we want. To do this we will create a new component that will handle the logic of dynamically showing our data. 

We will first create a functional component that will simply return two Hero Components with different sets of information. Here we can see our component changing based on the props we pass it.

```js 
const App = () => {
  return (
    <div class="container">
      <Hero name="Batman" catchphrase="I'm Batman!'"/>
      <Hero name="Superman" catchphrase="Up, Up and Away!"/>
     </div>
  )
}
```
*NOTE: Every JSX return must always return a single element. So if you have several make sure to wrap them in an element for return. IE container is the only element being returned, but container can have an unlimited amount of elements within.*

So if we can manually enter as many as we want... Can we procedurally create as many as we want? Absolutely! 

Let's bring back the state object within our App component so we can start dynamically creating our content.

```jsx
const App = () => {
  const state = {
  heroes: [
    {
      name: 'Batman',
      catchphrase: "I'm Batman"
    },
    {
      name: 'Superman',
      catchphrase: "Up, Up and Away!"
    }
  ]
}
  
  return (
    <div class="container">
      <Hero name="Batman" catchphrase="I'm Batman!'"/>
      <Hero name="Superman" catchphrase="Up, Up and Away!"/>
     </div>
  )
}
```
*REMINDER: State is literally the current ui state of our components. What heroes should we render? All the heroes within our current App state.*

Our last step is to handle the logic of looping through our state of heroes and creating a component for every index.


```jsx
const App = () => {
  const state = {
  heroes: [
    {
      name: 'Batman',
      catchphrase: "I'm Batman"
    },
    {
      name: 'Superman',
      catchphrase: "Up, Up and Away!"
    }
  ]
}
  
  const displayHeroes = heroes => {
    return heroes.map(data => {
      return <Hero name={data.name} catchphrase={data.catchphrase}/>
    })
  }
  
  return (
    <div class="container">
      {displayHeroes(state.heroes)}
     </div>
  )
}
```

For that we will create a function inside of App called displayHeroes that will take in the current state and return an array of JSX elements. What is great about JSX is that is will loop through that array for us and append to the App component.

And just like that.. We have used some of the very base foundations of React.

# Intro to React.js

![react-logo](./images/react-white-logo.png)

## Learning Objectives

* Explain what a frontend framework is and why they can be helpful in writing more complex applications.
* Explain what ReactJS is and where it fits in our applications' stack.
* Explain the component model of web development.
* Create and return React components in the browser.

## Framing

### What is a Frontend Framework? 

- A framework is software providing generic functionality and structure that serves as foundation to build and deploy applications.
- Express is a framework that runs on the server, receiving incoming request from the client, preforming some work that you have defined, and returning some response to the client.  Front-end frameworks run in the client's browser, receive input from interactions with the page, perform some work that you have defined, and make any updates necessary.
- Frameworks can help standardize code, give you additional functionality and performance, and can help get your code off the ground faster.  
- There are [many](https://2019.stateofjs.com/overview/) front end frameworks and each go about solving problems of how state is managed, updated, and represented by a view but there are many commonalities.
- There is a lot of debate over whether frontend frameworks count as frameworks at all -- some people say that they are just libraries and should be referred to as such.

### What is ReactJS?

React is a JavaScript library used to craft modern day UI and views for the front-end in web applications.

> **Selling Point:** By modeling small compatible components that focus on just rendering a view, we can move business logic out of the DOM, and therefore improve our app's performance, maintainability, modularity and readability.

#### Some History

The first thing most people hear about React is "Facebook uses it."
* First used by Facebook in 2011.
* Then Instagram in 2012.
* Went open source in May 2013.

**BEHOLD! The OLD FACEBOOK!** 

*2008*

<img src='https://lh3.googleusercontent.com/d4ypmybEZT8SAOj1efmy9CCkKwNG3Dd-Mv0__FoIsWgK0iWuYWBS4NPHOf71ANpKcx2ElOndGeiDInxm8p-sOMqNXBkPy3y-HsH45lGscqJepxFOYkU1_6BbAw' alt='2008 facebook' width='600px'>

*2011*

<img src='https://lh4.googleusercontent.com/lNCcVZlrC08vdkMrMZ8XCGjD5a3w8yUybFm2YN7VJJzOttmEl99lR_bXcW21hw7AVtKDRvQajA4AsqJHVHqzhHnkNsVmMRXMvi9uuoV3iIU5gIJjSSkUee8fpg' alt='2011 facebook' width='600px'>

*2020*

<img src="https://cdn.vox-cdn.com/uploads/chorus_asset/file/19819048/News_Feed.jpg" alt="2020 facebook" width="600px"> 

React was born out of Facebook's frustration with the traditional MVC model and how..
  * Re-rendering something meant re-rendering everything (or just a lot).
  * That had negative implications on processing power and ultimately user experience, which at times became glitchy and laggy.


### React from horse's mouth

If you want to get a taste of what React is all about, [here's an introduction from React.js Conf 2015](https://www.youtube.com/watch?v=KVZ-P-ZI6W4&feature=youtu.be&t=510). Recommend starting around the 8:35 mark and watching until 16:30.

### React in MVC

React can be thought of as the "Views" layer.

React will work with any back-end language, but for React project and in our in-class examples we will be using Mongoose and Express for the models and controllers.

<details>
  <summary><strong>What is the role of a "view" in a front-end Javascript application?</strong></summary>
  The visual template the user sees, often populated with data from our models.
</details>

## Components

One comment made about React when it was first open sourced was "Rethinking established best practices" which kind of became the React motto.  In React, we want to move away from template pages, away from separating code based purely on file type, and more towards a **component-based** separation of concerns.  [Templates vs Components](https://wanderoak.co/fixed-templates-vs-components/)

![Templates Page](images/templates-page.png)
![Components Page](images/components-page.png)
> [WanderOak - Fixed Templates vs. Components](https://wanderoak.co/fixed-templates-vs-components/)

When taking a look at Facebook, you could think of each status post as a mini-component in React. And a list of those updates, is a component that contains several of those mini-components. You could take that one step further and think of the Facebook app, as one giant component with several components within it. (Things like the list of status updates, the friends list, the header, etc...)

Imagine you worked at Facebook when they wanted to shift from using likes to reactions. Using traditional JavaScript, HTML, and CSS the shift would make you have to change your code in a bunch of places. Component based architecture allows us to maintain our code more easily.

### Let's together identify the components 

![Wireframe](images/wireframe.png)
![Wireframe with components](images/wireframe_deconstructed.png)
> [MakeTea - Building Robust Apps with React](http://maketea.co.uk/2014/03/05/building-robust-web-apps-with-react-part-1.html)

Notice the structure of how the various components are nested. 
```
- TubeTracker
    - Network
        - Line
    - Predictions
        - DepartureBoard
            - Trains
```

TubeTracker contains the application
Network displays each line on the network
Line displays the stations on a line
Predictions controls the state of the departure board
DepartureBoard displays the current station and platforms
Trains displays the trains due to arrive at a platform

### [F.I.R.S.T. Components](https://addyosmani.com/first/)

A React component is built to expect an input and render a UI with it. More importantly, a well-structured component only receives data specific to its purpose.

This is because React follows a more **functional** approach to programming. For React components under this approach, **the same input will always produce the same output**.

Best practice is that React components follow the **F.I.R.S.T.** guidelines

#### Focused

Components should do one thing and do it well.

#### Independent

Components should increase cohesion and reduce coupling. Behavior in one component should not impact the behavior of another. In other words, components should not rely on one another.

> But they should compliment one another.

#### Reusable

Components should be written in a way that reduces the duplication of code.

#### Small

Ideally, components should be short and condensed.

#### Testable

Because the same input will always produce the same output, components are easily unit testable.

> If you're interested, [Jest](https://facebook.github.io/jest/docs/tutorial-react.html) is a popular testing library for React.

----------------------------

## Code Along: Initial Setup

In order to create a new project and to get our development environment setup, we are going to use the Terminal command `create-react-app`. It will create a new folder in your current directory for the in-class application.

`create-react-app` is an NPM package also built by Facebook that writes our build dependencies for us so that we can do less configuration. It allows us to use React, JSX, and ES6. It also allows us to import our CSS, it autoprefixes our CSS so that we don't have to worry about cross browser compatibility, it gives us a dev server to run, and it enables hot reloading which updates the code in our browser without us refreshing the page.

It uses Webpack which is a build tool that enables many of the features listed above. It also includes Babel which transpiles our JavaScript from ES6 to be compatible with older browsers. It also includes Autoprefixer for CSS compatibility, ESLint for linting, and Jest for testing.

You can also set up all this yourself, but for now `create-react-app` allows us to worry more about our code and less about configuration.

```bash
$ npx create-react-app my-app
$ cd my-app
$ npm start
```

> We're using `npx` instead of `npm` here and you might be wondering why. `create-react-app` is updated often and using `npx` ensures that we take advantage of the most recent version. This also allows us to run `create-react-app` without installing anything to our machines!

> Here you will begin setting up a blog app that you will continue working on during this lesson's exercises. For demonstration purposes, We will be creating a simple "hello world" app.

After running `$ npm start`, we can view the app at `http://localhost:3000`

`create-react-app` provides us with all the necessary tools and configuration necessary to start writing React. `npm start` refers to an included script that starts up the development server.

Along with installing the necessary dependencies, it creates an initial app skeleton that looks like this...

```bash
├──README.md
├──  favicon.ico
├──  index.html
├──  node_modules
├──  package.json
└──  src
    ├──  App.css
    ├──  App.js
    ├──  index.css
    ├──  index.js
    └──  logo.svg
```

Most of the important files, which are primarily the ones where we will be working today, are in the `/src` directory.

Take some time and look at what's been generated. Specifically look in `App.js` and `index.js`


### We Do: Hello World - A Very Basic Component

The basic unit you'll be working with in ReactJS is a **component**.

* Components can be thought of as functional elements that take in data and as a result, produce a dynamic UI.

Throughout class we have separated HTML, CSS and Javascript.
* With components, the lines between those three become a bit blurry.
* Instead, we organize our web apps according to small, reusable components that define their own content, presentation and behavior.  

What does a component look like? Let's start with a simple "Hello World" example...

To start, in our `/src/App.js` file, let's remove the contents and in its place add this component definition...

```js
// bring in React from React
import React from 'react'

// define our Hello functional component
function Hello() {
// what should the component return
  return (
  // Make sure to return some UI
    <h1>Hello World!</h1>
  );
}

export default Hello
```

Let's break down the things we see here...

##### `function Hello`
This is the component we're creating. In this example, we are creating a "Hello" functional component.

##### `extends Component`
This is the React library class we inherit from to create our component definition.

##### `return`
Every component has, at minimum, a return. It generates a **Virtual DOM** node that will be added to the actual DOM.
* Looks just like a regular ol' DOM node, but it's not yet attached to the DOM. In this example the return is handling this functionality.

##### `export default Hello`
This exposes the Hello class to other files which import from the App.js file. The `default` keyword means that any import that's name doesn't match a named export will automatically revert to this. Only one default is allowed per file.

### Quick Recap

![](https://media2.giphy.com/media/ekvi8AacTWOuw5hHLS/giphy.gif)

## JSX

> Hey you got your html in my javascript!
>
> You got your javascript in my html!
>
> (https://youtu.be/O7oD_oX-Gio?t=5s)

Let's talk about the value that the render method returns. It looks an awful lot like an HTML heading, but it's not. We often write out React components in JSX.

JSX is [a language that compiles to Javascipt](http://blog.yld.io/2015/06/10/getting-started-with-react-and-node-js/#.V8eDk5MrJPN) that allows us to write code that strongly resembles HTML. It is eventually compiled to lightweight JavaScript objects.

Your Hello function:

* Currently returns JSX, not HTML.
The JSX creates a heading with 'Hello World!'.
* Your component reads this and renders a "Hello World!" heading.

> React can be written without JSX. If you want to learn more, [check out this blog post](http://jamesknelson.com/learn-raw-react-no-jsx-flux-es6-webpack/).  

Here is an example of React code without JSX-

![Templates Page](images/react-without-jsx.png)


## Virtual DOM 

You may have noticed that our `src/index.js` code mentions ReactDOM. ReactDOM doesn't refer to the same DOM we know. Instead, it refers to a Virtual DOM. The Virtual DOM is a key piece of how React works.

The Virtual DOM is a Javascript representation of the actual DOM. The virtual DOM is a staging area for changes that will eventually be implemented.

* Because of that, React can keep track of changes in the actual DOM by comparing different instances of the Virtual DOM.
* React then isolates the changes between old and new instances of the Virtual DOM and then only updates the actual DOM with the necessary changes.
* By only making the "necessary changes," as opposed to re-rendering an entire view altogether, we save up on processing power.
* This is not unlike Git, with which you compare the difference -- or `diff` -- between two commits.

![Virtual DOM Diagram](https://docs.google.com/drawings/d/11ugBTwDkqn6p2n5Fkps1p3Elp8ZToIRzXzvM4LJMYaU/pub?w=543&h=229)

> If you're interested in learning more about the Virtual DOM, [check this video out](https://www.youtube.com/watch?v=-DX3vJiqxm4).

So we've created the template for our component. Now, let's use `/src/index.js` to load in our new component and render it on the DOM...

```js
import React from 'react'
import ReactDOM from 'react-dom'
import Hello from './App.js'

ReactDOM.render(
  <Hello />,
  document.getElementById('root')
)
```
> In place of `ReactDOM.render` some tutorials will use React.renderComponent, which has been phased out. The change is outlined [here](http://bit.ly/1E81Whs).

`ReactDOM.render` takes the Virtual DOM node created by `extends Component` and adds it to the actual DOM. It takes two arguments...

  1. The component.
  2. The DOM element we want to append it to.

> **NOTE:** Whenever you use a self-closing tag in JSX, you **MUST** end it with a `/` like `<Hello />` in the above example.

---

### Review Questions
- How does JSX make your life as a developer easier?
- What are some of the advantages of having a virtual DOM?



## Hello World: A Little Dynamic

Our `Hello` component isn't too helpful. Let's make it more interesting.
* Rather than simply display "Hello world", let's display a greeting to the user.
* So the question is, how do we feed a name to our `Hello` component without hardcoding it into our render method?

First, we pass in data wherever we are rendering our component, in this case in `src/index.js`...

```js
import React from 'react'
import ReactDOM from 'react-dom'
import Hello from './App.js'

ReactDOM.render(
  <Hello name={"Nick"} />,
  document.getElementById('root')
)
```

Then in our component definition, we have a reference to that data via as a property on the `props` object...

```js
function Hello(props) {
  return (
      <h1>Hello {props.name}</h1>
  );
}
```

In the above example, we replaced "world" with `{props.name}`.

### What are `.props`?

Properties! Every component has `.props`
* Properties are immutable. That is, they cannot be changed while your program is running.
* We define properties in development and pass them in as attributes to the JSX element in our `.render` method.

First we can pass multiple properties to our component when its rendered in `src/index.js`..

```js
import React from 'react';
import ReactDOM from 'react-dom'
import Hello from './App.js'

ReactDOM.render(
  <Hello name={"Nick"} age={24} />,
  document.getElementById('root')
)
```

Then in our component definition we have access to both values...

```js
function Hello(props) {
  return (
    <div>
      <h1>Hello {props.name}</h1>
      <p>You are {props.age} years old</p>
    </div>
  );
}
```

> **NOTE:** The return statement in `render` can only return one DOM element. You can, however, place multiple elements within a parent DOM element, like we do in the above example with `<div>`.

---

## You Do: A Blog Post 

Let's have some practice creating a React component from scratch. How about a blog post?
* Create a `post` object literal in `src/index.js` above `ReactDOM.render()` that has the below properties.
  1. `title`
  2. `author`
  3. `body`
  4. `comments` (array of strings)
* Render these properties using a Post component.
* The composition of your Post is up to you.

If you finish early, try experimenting with CSS (Make Sure you use `className` instead of `class` in `JSX`!)


<details><summary>Solution</summary>

*Post.js*

```
import React from 'react';

function Post(props) {
	return(
        <div>
            <h1>{props.title}</h1>
            <p>By {props.author}</p>
            <div>
                <p>{props.body}</p>
            </div>
            <h3>Comments:</h3>    
            <p>{props.comments[0]}</p>
        </div>
    )
}

export default Post;
```

*index.js*

```
import Post from './Post';

const post = {
    title: "Avengers",
    author: "Nick Fury",
    body: "I secretly recruited a group of superheroes to save our world.",
    comments: [
      "I love Avengers.",
      "Forget Avengers, we want the Witcher.",
		"At least let aliens destroy D&D for what they did to GOT!"
    ]
}

ReactDOM.render(
    <Post 
        title={post.title} 
        author={post.author}
        body={post.body} 
        comments={post.comments}/>, 
    document.getElementById('root')
);
```

</details>


---


#### Q: What problems did you encounter when trying to add multiple comments to your Post?

It would be a pain to have to explicitly define every comment inside of `<Post />`, especially if each comment itself had multiple properties.
* This problem is a tell tale sign that our separation of concerns is being stretched, and it's time to break things into a new component.

We can nest a Comment component within a Post component.
* We create these comments the same way we did with posts
* Then we can reference a comment using `<Comment />` inside of Post's return method.

Let's create a new file for our Comment component, `src/Comment.js`...

```js
import React from 'react';

const Comment = (props) => {
    return(
        <div>
            <p>{props.message}</p>
        </div>
    )
}

export default Comment;
```

Then in `src/Post.js`, we need to load in our `Comment` component and render it inside of our `Post` component...

```js
import React from 'react';
// Load in Comment component
import Comment from './Comment.js'


function Post(props) {
	return (
	  <div>
	    <h1>{props.title}</h1>
	    <p>By {props.author}</p>
	    <div>
	      <p>{props.body}</p>
	    </div>
	    <h3>Comments:</h3>
	    // Render Comment component, passing in data
	    <Comment message={props.comments[0]} />
	  </div>
	);
}

export default Post;
```

> **Note**: We could put all of our code in one file, but it's considered a good practice to break components out into different files to help practice separation of concerns. The only downside is we have to be extra conscious of remembering to **export / import** each component to where it's rendered.

The above code works, but we'd have to hard-code all of our `Comments`.  This is not very dry and our code will not dynamically change.  The best way to handle this is to set a variable equal to all of the `<Comments />` for this post.  We can do this using `.map` in `Post` function.

We can use `.map` in `Post` function to avoid having to hard-code all of our `Comments`

```js
import React from 'react';
import Comment from './Comment';

function Post(props) {
    let comments = props.comments.map((comment, index) => (
        <Comment message={comment} key={index}/>
    ))

    return(
        <div>
            <h1>{props.title}</h1>
            <p>By {props.author}</p>
            <div>
                <p>{props.body}</p>
            </div>
            <h3>Comments:</h3>    
            {comments}
        </div>
    )
}

export default Post;
```

---

## Closing

* Why do we use components in React?
* What is the Virtual DOM?
* What is JSX?
* What features does `create-react-app` give us?

# State and Data-flow

## Learning Objectives

* Review passing data to a React component via `props`.
* Define and use nested components.
* Identify `state` in a React app.
* Modify the `state` of a React component through events.
* Distinguish container and presentational components.

## Framing

In this lesson we will be looking at how data is managed within a React application. In particular, we will compare and contrast a component's `props` and `state`. They are similar, but have a couple key distinctions:

* `props` are passed into a component, but `state` is local or native to the component
* While we cannot change `props` (immutable) from within a component, we can change a component's `state` (mutable).

## State

The limitation of props is that they are immutable; we can't change the data from within the component. The data that we can change within a component is called **[state](https://facebook.github.io/react/docs/state-and-lifecycle.html)**. 

We haven't talked about state much, but you have worked with it before. Think back to your game project. How did you track the score of the game, the current turn, whether or not the game had ended or not. These are all examples of state.

* **Trivia**: what is the current score, what card is currently displayed to the user, is the user's input correct or incorrect?
* **Simon**: what order of buttons did the user push, what is the order of buttons they were supposed to push, what round or level are they on?
* **Blackjack**: what is the score of the player's hand? The dealer's? How do we award money to a winning hand?

We can figure out the `state` of a turn-based game because there is a clear idea of a beginning and end and states that reflect progress from one turn to the next turn: what flash card is the user on, what buttons do they need to push, how the cards are distributed among the two players.


*Q: So we know an application can have different states. But how do we transition in between them?*

Events! (or user actions)


### F.I.R.S.T. Principles and State

The aim of the F.I.R.S.T. principles is to create a sane approach to breaking down not just a user interface, but also an application's data. Following the F.I.R.S.T principles should lead you to manageable, focused components that work with a specific set of data: the **props** we pass to those components and the **state** of the component itself.

*Each component is concerned only with the data relevant to its purpose*.

For your first project, you had to do that manually. Manually write event listeners that would update state stored in global scope and then update your UI by manually updating individual DOM nodes.

You can think of React as an event-driven state machine, in other words, a react app churns out new states as a result of user interactions. 

A React application receives input through user interactions (event listeners) and outputs a UI that reflects a brand new state (new cards, fewer or more chips, etc).


 *Q: What do we mean by a React component's "state"?*

The object properties of a component (`state`) that change as the application runs, as opposed to `props`, which are immutable.


### State and Rendering

Before moving on to build our application, it's worth mentioning another aspect of `state`: when it changes our components re-render.

![react component image](./images/react-component-state-update.png)

Our UI updates when state changes. The user takes some action, like submitting information via a form, and the component holding that form has a `state` that is updated with the value of the user's input.

### Props vs State

Just a recap, both **props** and **state** are plain JS objects that hold information, but when updated re-renders the component. However they are different in one important way, `props` get passed to the component whereas `state` is managed within a component.

## Let's build something together.

Together we are going to grow our blog application with state and props! Yay!

Start by cloning this repo, then follow these instructions:

```bash
cd react-state-remote/blog-app
npm install
npm start
```
You should be greeted with a Hello message. 

Now let's install a handy tool.
1. Chrome: [React Dev Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
2. Firefox: [React Dev Tools](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)

At the moment we will see our `Hello` component inside of google chrome's development tools under the React tab. (We can even see our props/state!)

Now let's create two new component files inside the `src` folder.

Your structure should look like this:

```
blog-app
├──  favicon.ico
├──  public
├──  node_modules
├──  package.json
└──  src
    ├──  Comment.js
    ├──  Post.js
    ├──  App.css
    ├──  App.js
    ├──  index.css
    ├──  index.js
    └──  logo.svg

```

Let's throw some info into those files! 

**src/Post.js**

```js
import React from 'react';
import Comment from './Comment';

function Post(props) {
    let comments = props.comments.map((comment, index) => (
        <Comment message={comment} key={index}/>
    ))

    return(
        <div>
            <h1>{props.title}</h1>
            <p>By {props.author}</p>
            <div>
                <p>{props.body}</p>
            </div>
            <h3>Comments:</h3>    
            {comments}
        </div>
    )
}

export default Post;
```

Let's break down the above code. We created a Post component that takes in the props: title, author, body, and an array of comments. For each comment inside of *this.props.comments* it will create a Comment component. Since this file requires the Comment component let's update that next. 

**src/Comment.js**

```js
import React from 'react';

const Comment = (props) => {
    return(
        <div>
            <p>{props.message}</p>
        </div>
    )
}

export default Comment;
```

Awesome! Now update `index.js` to render out the Post component.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import Post from './Post';
import * as serviceWorker from './serviceWorker';

const post = {
    title: "A Day In the Life of a React Developer",
    author: "Disgruntled Dev",
    body: "Components... components everywhere.",
    comments: [
      "Some shady internet comment.",
      "A rare comment with actual feedback."
    ]
}

ReactDOM.render(
    <Post 
        title={post.title} 
        author={post.author}
        body={post.body} 
        comments={post.comments}/>, 
    document.getElementById('root')
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

As you can see we are rendering a Post component with the props that we defined earlier.

You should see this now: 

![example react one](./images/blog-app1.png)

So far we have used props to pass information from one component to another. But, what if we wanted data to change within a component? Props are immutable and as such can't be changed while the app is running. Time for `state`!

Unfortunately, introducing `state` means exposing the limitations of our functional components and learning about a new syntax for defining components called "Class-based components".

However easy *functional components* are to read, debug or test but they do not have state or lifecycle methods. Class-based components do. Both of these new concepts (state, and lifecycle methods) are important in React development, which is why we need to learn how to write a class component.

### Functional vs Class Component

#### Syntax
One of the obvious differences between these types of components is the syntax.

Functional components, as the name implies, are just like a regular js function with access to a `props` argument.

```
import React from 'react';

function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

Class components, again as the name implies, are written in JS class syntax and inherits properties and a lot of functionality from `React.Component`.

```
import React from 'react';

class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

Notice the use of `this` to call the property name. Why do we have to use the `this` keyword here?

#### State

Functional components are **stateless** that means they don't have access to state. 

Class components are **stateful**, state can be accessed and updated.

> Technically, this has changed post React 16.8 release. We now have something called "hooks" for changing the state in a functional component. But for simplicity sake we will say that state cannot be changed in functional component.

#### Lifecycle Methods

Another feature that cannot be used in functional components are "lifecycle methods". Lifecycle methods run at specific times in the rendering, mounting, and unmounting phases of a component's life. Functional components don't have access to these methods for the same reason that they don't have access to state: all lifecycle methods are inherited from `React.Component` through the extend syntax.

So,if you need lifecycle methods you need a class component.

> This has also changed post React 16.8 hooks update.

### Code Along: Adding a state object

We're going to add "Karma" to our comments in order to show the user which comments are positive and which are negative by changing their colour.

We need a class-based component to add and access state. Let's first change the syntax of our functional `Comment` component to the Class-based alternative.

```js
import React, {Component} from 'react'

class Comment extends Component {

}

export default Comment
```

Since this is a class, instead of adding a `return` (which is not possible), we will use `render()` to return JSX when this component is invoked.

```js
import React, {Component} from 'react'

class Comment extends Component {
  render () {
    return (
      <div>
	<p>{this.props.message}</p>
      </div>
    )
  }
}

export default Comment
```

> `this` keyword is used to access `message` property sent from `Post`

Let's set state inside of our comments. And we will use the `karma` state to set class name in `div`

```js
import React, {Component} from 'react'

class Comment extends Component {
  state = {
    karma: 'good'
  };

  render () {
    return (
      <div className={this.state.karma}>
        <p>{this.props.message}</p>
      </div>
    )
  }
}

export default Comment
```

As you can see `state` is an object with key-value pair.

Inside our React Developer Tools we will now see that by default we have set the state of karma to 'good' for all comments. We also used this state to declare a classname attached to our comment component. Now that we have a set state we can now create a method built into our component to update the state.

We will be creating a `changeKarma` method to update our `state` and a button that will call trigger that update by calling the new method. Simply put, the function checks the state and toggles it depending on the current value. While we're at it, let's add some gifs.

```js
import React, {Component} from 'react'

class Comment extends Component {
  state = {
    karma: 'good'
  };

  changeKarma = () => {
    if (this.state.karma === 'good'){
      this.setState({
        karma: 'bad'
      })
    } else {
      this.setState({
        karma: 'good'
      })
    }
  }

  render () {
    let goodKarmaSrc = "https://media.giphy.com/media/1zJFtdNUhblPRT1yQy/giphy.gif";
    let badKarmaSrc = "https://media.giphy.com/media/AxVvk4TmDfmoMtSmmQ/giphy.gif";
    
    return (
      <div className={this.state.karma}>
        <img src={this.state.karma === 'bad' ? badKarmaSrc : goodKarmaSrc }/>
        <p>{this.props.message}</p>
        <button className={"button"} onClick={this.changeKarma}>Change Karma</button>
      </div>
    )
  }
}

export default Comment
```

> Notice the use of ternary operator to change the gif in the `img` tag

So onClick the button will run the method changeKarma. 

Even though our `className` is changing on click of the button, nothing really is happens on the screen. So let's add a bit of styling in `index.css` to see some changes.

```
.good,
.bad {
  padding: 20px;
}

.good img {
  border: 5px solid green;
  width: 200px;
}

.bad img {
  border: 5px solid red;
  width: 200px;
}
```


Amazing!  Now when we click on our button the class attached to the component is switched without having to refresh the page. 


## Check for Understanding

* What is the difference between `state` and `props`?
* What do we use `props` for?
* What do we use `state` for?

We've done a fair amount of framing so far, so let's practice with another application: React Counters!


## Closing 

If asked, could you explain the differences between props and state? If not, reread this lesson and build out another Counters app, repitition is the key to understanding React. We've now covered the differences between the two as well as how you can use state to control data inside a component and how to update state to display new data to a user.

Defining components and working with props and state (data) constitutes the majority of the work of building a React application.

## Bonus

### Style in React

When it comes to adding styles to React, there is a bit of debate over what's the best practice. Facebook's official docs and recommendations are to write stylesheets that treat your CSS rule declarations as properties on one big Javascript object that can be passed into components via inline styles.

From the [Docs](https://facebook.github.io/react/tips/inline-styles.html)...

>  "In React, inline styles are not specified as a string. Instead they are specified with an object whose key is the camelCased version of the style name, and whose value is the style's value, usually a string"

However, this kind of rethinking the wheel feels like a step backwards for a lot of designers and developers who cringe at the notion of inline styles. For them, they choose to build React apps through a more traditional flow of adding ids and classes and then targeting elements via external stylesheets.

Also, via Webpack and other custom loaders, it is possible to use many third-party libraries or processors such as SASS, LESS, and Post-CSS.

Interesting to note, this problem has not been universally solved, and thus the debate will most likely continue to rage on until somebody figures it out. Therefore, its often left to a team decision when choosing the best option for the application.

Interested in learning more? Check out some excellent blog posts on the subject from the front-end community:
- https://medium.com/@jviereck/modularise-css-the-react-way-1e817b317b04#.61qgjgdu3
- http://jamesknelson.com/why-you-shouldnt-style-with-javascript/
- http://stackoverflow.com/questions/26882177/react-js-inline-style-best-practices
- https://css-tricks.com/the-debate-around-do-we-even-need-css-anymore/

### [Example of Object Literal Styles with React](https://github.com/ga-wdi-exercises/react-omdb/commit/830697fc68dcdccafcae9f73e711103de8d93fc9)

> **Reminder**: `class` is a protected keyword in React, in order to add a class attribute to an element use the keyword `className`

To add the finishing touches to our application, let's take a stab at styling our app with inline-styles and advance our markup with some help from Bootstrap...
- Load in Bootstrap CDN in `index.html`
- Modify UI to include Bootstrap classes
- Create a `styles` directory and make a file for your CSS rule definitions - this will be written in Javascript!
- Load in that file in any component and then use that to apply inline styling

### Resources

* [Imperative vs. Declarative Javascript](http://www.tysoncadenhead.com/blog/the-state-of-javascript-a-shift-from-imperative-to-declarative#.VxgGxZMrKfQ)
* [Styling in React](http://survivejs.com/webpack_react/styling_react/)
* [ReactJS Fundamentals Course](http://courses.reactjsprogram.com/courses/reactjsfundamentals)

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Intro to React Router

For this lesson, students should:

- Understand components
- Understand state and props

The first part is a demonstration of how Router works. 
## Learning Objectives

- Learn about routing with react-router
  <!-- - Using data from APIs and JSON files -->
  <!-- - Create a Stock Trading app -->

## Preparation

First, we'll create a new app to learn how React Router works.

1. Create a new react app: `npx create-react-app learn-react-router`
2. `cd learn-react-router`
3. `npm install react-router-dom`

## What is React Router?

React Router is a module that makes it easy to build single page apps (SPAs) that appear to have more than one page - mimicking an experience users are familiar with elsewhere on the internet. Links in a React app work differently than anchor tags in server-rendered applications. Essentially we will display elements that look and behave like links but really just swap components on the page without making a full page reload.

The main components of the router are:

1. `BrowserRouter`: The module that stores all the routes for the app as well as route history, current location and url.
2. `Switch`: Creates a switch case to replace the component area depending on the route.
3. `Route`: Used to define each individual route by relating each path to a specific component.
4. `Link`: Used to render anchor tag lookalikes that tell the `Switch` which `Route` to load.

Since `BrowserRouter` is the parent component, we'll configure it in `index.js`. It would look like this:

```
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router
} from "react-router-dom"

import App from './App';

ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById('root')
);
```

Update `index.js` to include this code.

Next, let's add some routes. Open `App.js` and let's add let's import the routing components we'll need first.

```
import {
    Route,
    Link,
    Switch
} from 'react-router-dom'
```

- `Route` is used to connect URL paths to components.
- `Link` is used to create links to `Route` paths.
- `Switch` will find the _first_ route to match a given path. Once found, it will stop looking, just like a Javascript switch or if  statement.

Now we need some routes. But first, let's create a new component that we can attach to a route:

### About.js

```
import React, { Component } from 'react';

class About extends Component {
    render () {
        return (
            <div>
                All about routing! Read it here folks!
            </div>
        )
    }
}

export default About;
```

Before we jump into connecting the two let's look at the syntax for creating a Link to a route.

```jsx
<Link to='/about'>About</Link>
```

### App.js

```diff
import React, { Component } from 'react';
import './styles/App.css';
import {
    Route,
    Link,
    Switch
} from 'react-router-dom'

+ import About from './About';

class App extends Component {
    render() {
        return (
+           <header>
+               <h1>Learn Routing</h1>
+               <nav>
+                   {/* Create our nav bar links using the Link element from react router */}
+                   <ul>
+                       <li><Link to="/about">About</Link></li>
+                   </ul>
+               </nav>

                
+               <div className="main">
+                   {/* Create the routes. This will not appear on the page. */}
+ 		    <Switch>
+                       <Route path="/about" component={ About } />
+                   </Switch>
+               </div>
+           </header>
        );
    }
}

export default App;

```

Done. We've successfully added a link to a route in our app. Try visiting the route in the browser!

### You Do: Practice (15 min)
Create two new components representing other pages of the app - `Contact` and a `Homepage`. The content and layout of the components is up to you but feel free to keep them simple, like we did with the `About` page.

When your two new components are created, add `Route`s for each within the `Switch` statement. Again, follow the example laid out by the `Route` for the `About` page.

Finally, add two new `Link`s for the pages in the `<nav>` and test to make sure you can swap pages by clicking each link in the browser. 

[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Building a PERN App

The PERN stands for Postgres, Express, React and Node and is an acronym used to
describe applications built with that stack of technologies. React and it's
surrounding ecosystem (like Redux and React-Router) are just for the front-end
of the application. If we want to persist data to a database or have any other
back-end logic we need to (1) provide a separate back-end and (2) get the
front-end and back-end to communicate somehow.

In this lesson, we'll discuss two options for building full stack applications
using React on the front-end with Express, Postgres and Node on the back-end.

## Objectives

By the end of this, developers should be able to:

* Describe the difference between single-server and multi-server configurations
  for an application built in the PERN stack
* Install and use `cors` to allow for Cross-Origin Resource Sharing between our
  front-end application and back-end API
* Build and deploy our front-end application
* Describe the process of connecting our front-end and back-end
* Set up our front-end development server to proxy requests to our back-end
  server
* Set up our back-end API to serve static `build` assets in production

## Introduction (10 min / 0:15)

To integrate React with a back-end framework (such as Express) we will need to
make a few decisions about the desired architecture of our application (how we
want to structure everything). The first primary decision to make is where we
want our front-end application to be served from. There are two primary options:

### Multi-Server Configuration

Our front-end application and back-end API will be completely separate, hosted
on separate servers even! They will each have their own Git repositories and
will be deployed independently to different servers. Our front-end will retrieve
data from our back-end (across separate domains) using AJAX.

#### Pros

* Separation of Concerns: Our application is more modular and our front-end and
  back-end developers can work on their parts of the application independent
  of each other.
* Specialized Configuration: Since our front-end and API will be hosted on
  separate servers, we can optimize server configuration for each one
  independently, allowing them to scale independently of each other and
  preventing them from competing for resources on the same server.

#### Cons

* Since requests will be sent across separate domains, we will have to configure
  CORS (Cross-Origin Resource Sharing) for the browser to allow our front-end to
  retrieve data from our back-end

### Single-Server Configuration

Our front-end application will be housed in the same repository as our back-end
code. They will be deployed together to a single server where our back-end will
be responsible for serving up our front-end application in addition to our API
data.

#### Pros

* Single Deployment: Since our front-end will be served up by our API, we only
  need to manage one deployment.
* Unified Codebase: Since our front-end and back-end will be housed in the same
  Git repo, we will always have a more full picture of the application than if
  they were in separate repos.
* No CORS: Since our front-end application will be making requests back to the
  same domain that served it up (its 'origin'), we do not need to configure
  CORS.

#### Cons

* We will have to modify our server to serve up both json data for the API
  endpoints and the assets of our front-end which could require additional
  configuration and cause the two to compete over server resources.

Today, we will focus on setting up and deploying our application on separate
servers. This is more common and more straightforward.

## Getting Started (20 min / 0:35)

Today, we will be building the GameLib.biz app. GameLib.biz is a place for users to track their video game library and which games they've completed. 
We will also be using a Sequelize / Express back-end to allow for users to save their games.

### Back-End Setup

1. First, clone down [the
   back-end](https://git.generalassemb.ly/seir-921/gamelib-api-sql),
   install dependencies, create a `gamelib` database, and open in VS Code.

2. Run the migration and seed files to build the game table and populate is 
   with game data.

```bash
sequelize db:migrate
sequelize db:seed:all
```

3. Start the server

```bash
npm start
```

> If you inspect `package.json`, you will see that this is an alias for `nodemon server.js` in the "scripts" object

4. Navigate to `localhost:4000/api/v1/games` to see the response from our server. You should see a message that says: "Incomplete games#index controller function". 

5. In `controllers/games.js` all CRUD functionality has been stubbed out but is currently incomplete. Complete the `index` function with the following:

```js
const index = (req, res) => {
    db.game.findAll().then((foundGames) => {
        if(!foundGames) return res.json({
            message: 'No Games found in database.'
        })
      
        res.json({ games: foundGames })
    })
    .catch(err => console.log("Error at games#index", err))
}
```

> The code we added will return a JSON response to the client that we can use to save or display the data as necessary.

6. Navigate to `localhost:4000/api/v1/games` to see the response from our server now. You should see an array of 10 game objects from our database in JSON format. If you don't, debug before moving on.

7. Complete the `show` function so that it too sends back a single JSON game object when a request is made to `localhost:4000/api/v1/games/<ValidGameIdHere>`. 

8. To implement the `create` method we first need to modify `server.js` to parse any JSON included with a POST or PUT request and save it within `req.body` for our access in the associated controller function. Uncomment line 9 of `server.js` to enable express's built-in body parsing capabilities. 

9. Modify the `create` function in `controllers/games.js` to the following:

```js
const create = (req, res) => {
    db.Game.create(req.body, (err, savedGame) => {
        if (err) console.log('Error in games#create:', err)

        // Validations and error handling here

        res.status(200).json({ game: savedGame })
    })
}
```

> Any function that modifies data in the database really should be protected with validations and comprehensive error handling. We don't have the time to add it now but here in the controller is one place where we can make sure the user is saving the data we need.

10. Spend 15 minutes completing the `update` and `destroy` methods (using similar techniques that we used with the `index`, `show`, and `create` routes). Test all of the routes with your favourite HTTP Request tool (like Postman or `curl`). 

### Front-End Setup

1. In a ***separate terminal window/tab***, clone down [the React GameLib
   app](https://git.generalassemb.ly/SF-SEI/gamelib-client)
2. Install dependencies, and open in VS Code.
3. Start the development server:

```bash
npm start
```

> If you inspect `package.json`, you will see that this is an alias for `react-scripts start`

3. Navigate to `localhost:3000` to ensure the app is up and running. Take 5 minutes to familiarize yourself with the starter code.

4. We want our users to see a list of games served from the database (keep it running in another window or tab of your terminal app). Let's start by adding a Route in `config/routes.js`.

```js
import React from 'react'
import { Switch, Route } from 'react-router-dom'

import Home from '../pages/Home'
import GameList from '../pages/GameList'

export default (
  <Switch>
    <Route exact path='/' component={ Home } />
    <Route path='/games' component={ GameList } />
  </Switch>
)
```

> We import `GameList` even though it doesn't exist and you may see an error  we'll fix that right now.

5. Create `/src/pages/GameList.js` and get a boilerplate class-based component in place.

6. The `GameList` component is going to be our first to make a request to the backend through our helper functions. Build out the component with the following code:

```js
import React, { Component } from 'react'
import GameModel from '../models/game'

import { Link } from 'react-router-dom'
import GameCard from '../components/GameCard'

class GameList extends Component {
  state = {
    games: []
  }

  componentDidMount() {
    this.fetchData()
  }

  fetchData = () => {
    GameModel.all().then(data => {
      this.setState({ games: data.games })
    })
  }

  render() {
    return (
      <div>
        <h1>All Games</h1>
      </div>
    );
  }
}

export default GameList;
```

7. In `/models/game.js` add the method we invoke in the `GameList` component.

```js
  static all = () => {
    // the fetch API will not parse JSON in the response automatically so we handle it in the first .then()
    return fetch(`${url}/games`).then(res => res.json())
  }
```

> What is the `static` keyword here for?

8. We won't see a list of games in state quite yet. What we will see is a CrossCORS error in the browser's console. Let's take a break to discuss that.

## Two-Server Architecture (30 min / 1:15)

Currently we are using this type of architecture. Our back-end is running on
`localhost:4000` while our front-end is running on `localhost:3000`. One way to
say this is that these applications have different "origins". One issue with
this is that our browser is not going to like requests from our front-end
(served by `localhost:3000`) to our back-end on `localhost:4000`. In the
application, navigate to the Game List view and check the console. You
should see:

```
XMLHttpRequest cannot load http://localhost:4000/api/v1/games. No 'Access-
Control-Allow-Origin' header is present on the requested resource. Origin
'http://localhost:3000' is therefore not allowed access.
```

This is Chrome telling us that since our back end is running on a separate port
("origin") than our front end, our front end is not allowed to retrieve data
from it. To fix this, we need to configure CORS (Cross-Origin Resource Sharing)
on our back-end.

### Installing `cors` in Express

1. Stop your Express server, and install `cors` via npm:

```bash
npm install cors
```

2. In `index.js`, require the `cors` module and integrate with Express:

```js
const cors = require('cors')
```

```js
app.use(cors())
```

3. Restart your Express server:

```bash
npm start
```

Now when you navigate to `localhost:3000/games`, you should see an array of games 
being retrieved from our API and stored in `GameList`'s state.

> Note: The default `cors` configuration (above) will allow requests from
> **any** origin (which may or may not be ideal). To more precisely control
> access to our API, we would need to do little more configuration. Check out
> the [cors documentation](https://www.npmjs.com/package/cors) for more
> information on this process.

### Complete the GameList Component

1. Let's display each game on the GameList page. Refactor your `render` function to the following:

```js
  render() {
    let gameList = this.state.games.map((game, index) => {
      return <h1 key={index}>{ game.title }</h1>
    })

    return (
      <div>
        <h1>All Games</h1>
        { this.state.games ? gameList : 'Loading...' }
      </div>
    );
  }
```

> We're **conditionally rendering** the game titles once we know the data from our API is safely in state. This will show a "Loading..." message until the array of games in state has some value and is no longer empty. Once that is true, we render the titles for each game.

### Single Game Page

1. A list of game titles is fine but our users will want to do more than see some text. Let's refactor those `<h1>` elements to render individual `GameCard` components. The GameCard component should display the title, publisher, and the coverArtUrl but how it is laid out is up to you. 

2. With a working GameCard component rendering to the GameList page, we can now start to build a single detail page for each game. Let's make each GameCard component a clickable link. In the render function of `GameList.js`:

```js
let gameList = this.state.games.map((game, index) => {
  return (
    <Link to={`/games/${ game._id }`} key={index}>
      <GameCard  {...game} />
    </Link>
  )
})
```

For every `<Link>` component, we need to add a `<Route />`. React Router can handle dynamic URLs and does so in a way we are already familiar with by allowing path names to look like `/games/:id` in the Route component. Add this to `routes.js`:

```js
import GameShow from '../pages/GameShow'
...
<Route path='/games/:id' component={ GameShow } />
```

3. The GameShow component will be up to you to build out. Here are the requirements:

```
- it must use a static method from the GameModel 
- it must fetch a single game from the database using the ID
- it must conditionally render a GameCard component and pass it all required props
```

> Hint: Look for the game's ID in the props passed to each component rendered through a <Route />. You can find the id in the `match` props.

4. Our last step together will be to build out the functionality for a user to create a new game. We'll type this out together, but here is the final code for this component. In a new file, `/pages/NewGame.js`, add:

```js
import React, { Component } from 'react';
import GameModel from '../models/game'

class NewGame extends Component {
  state = {
    title: '',
    publisher: '',
    coverArtUrl: '',
    completed: false  
  }

  handleSubmit = (event) => {
    event.preventDefault();

    GameModel.create(this.state)
      .then(data => {
        this.props.history.push('/games')
      })
  }

  handleChange = (event) => {
    if (event.target.type !== "text") {
      this.setState({ completed: !this.state.completed })
    }

    this.setState({
      [event.target.name]: event.target.value
    })
  }

  render() {
    return (
      <div>
        <h2>New Game</h2>
        <form onSubmit={this.handleSubmit}>
          <div className="form-input">
            <label htmlFor="title">Title</label>
            <input 
              type="text" 
              name="title" 
              onChange={this.handleChange}
              value={this.state.title} />
          </div>
          <div className="form-input">
            <label htmlFor="publisher">Publisher</label>
            <input 
              type="text" 
              name="publisher" 
              onChange={this.handleChange}
              value={this.state.publisher} />
          </div>
          <div className="form-input">
            <label htmlFor="coverArtUrl">Image URL</label>
            <input 
              type="text" 
              name="coverArtUrl" 
              onChange={this.handleChange}
              value={this.state.coverArtUrl} />
          </div>
          <div className="form-input">
            <label htmlFor="completed">Completed</label>
            <input 
              type="checkbox" 
              id="completed" 
              checked={this.state.completed} 
              onChange={this.handleChange} />
          </div>

          <input type="submit" value="Save!"/>
        </form>
      </div>
    );
  }
}

export default NewGame;
```

As we've seen before, here our component renders a form for our user to interact with. This form has **controlled inputs**, in other words, input elements where the value is tied directly to state and only modified through changing state. A separate `onSubmit()` method is called when the form's submit button is pressed. We stop the default submit behaviour from happening and instead make the request through our model file. Let's write the fetch statement that will send our form data to the API as JSON.

And in `/models/game.js` add:

```js
class GameModel {
  ...
  static create = (gameData) => {
    return fetch(`${url}/games`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(gameData)
    })
      .then(res => res.json())
  }
}
```

### Complete Functionality

Time permitting, work through the following features until your GameLib app allows a user full CRUD functionality.
- on the GameList page, a user should be able to press a button to delete a game from the DB and be immediately shown an updated list of games.
- on the GameCard component, a user should be able to toggle an edit form, provide new values for the game, and save their changes.
- find an image of a badge online and display it on the GameList page for each game the user has completed

## Closing / Questions (10 min / 2:30)

### Microservice Solution

This is the setup that we implemented together in class.

* [Back-End](https://git.generalassemb.ly/seir-921/gamelib-api-sql/tree/solution)
* [Front-End](https://git.generalassemb.ly/SF-SEI/gamelib-client/tree/921-solution/src)
