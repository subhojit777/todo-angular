# todo-angular
Todo app using Nodejs + AngularJs

Requirements
-------------
- [Nodejs and npm](http://nodejs.org/)

Installation and usage
------------------------
- Clone the repository `git@github.com:subhojit777/todo-angular.git`
- Install the application `npm install`
- Start the server `node server.js`
- View in browser at `http://localhost:8080/api/todo`

Services used
--------------
- [Modulus.io](https://modulus.io/) for database.

Code has been taken from this tutorial [https://scotch.io/tutorials/creating-a-single-page-todo-app-with-node-and-angular](https://scotch.io/tutorials/creating-a-single-page-todo-app-with-node-and-angular). But I have not copied the exact code.
This [GitHub](https://github.com/scotch-io/node-todo) code was not working for me.

Problems faced
---------------
- ExpressJs routing problem.
	- In GitHub the routing code was like this:
	```javascript
	app.get('*', function(req, res) {
		res.sendfile('./public/index.html');
	});
	```
	This means for every request it will load `index.html`
	- I changed it to this:
	```javascript
	app.get('/api/todo', function(req, res) {
		res.sendfile('./public/index.html');
	});

	app.get('/js/controllers/:name', function(req, res) {
		res.sendfile(__dirname + '/js/controllers/' + req.params.name);
	});

	app.get('/js/services/:name', function(req, res) {
		res.sendfile(__dirname + '/js/services/' + req.params.name);
	});

	app.get('/js/:name', function(req, res) {
		res.sendfile(__dirname + '/js/' + req.params.name);
	});
	```
- Error while loading AngularJs module.
	- In GitHub the AngularJs code loading was in this code:
	```html
	<script src="js/controllers/main.js"></script> <!-- load up our controller -->
	<script src="js/services/todos.js"></script> <!-- load our todo service -->
	<script src="js/core.js"></script> <!-- load our main application -->
	```
	Since we are accessing the app from this URL `http://localhost:8080/api/todo`,
	therefore it was unable to load the resource files.
	- I changed it to this:
	```html
	<script src="../js/core.js"></script> <!-- load our main application -->
	<script src="../js/controllers/main.js"></script> <!-- load up our controller -->
	<script src="../js/services/todos.js"></script> <!-- load our todo service -->
	```
	I figured out this problem by seeing the browser console.

Things I understood while creating this application
----------------------------------------------------
- The backend and APIs are provided by Nodejs and its modules.
- AngularJs service provides service and controllers to control the HTML DOM.

Things I need to understand more in detail
-------------------------------------------
- Purpose of service and controllers in AngularJs
- Packages used in this application

Things I need to know
---------------------
- Best practices for creating AngularJs app.
- Coding standards.
- Currently we use `http://localhost:8080/api/todo` to access the app, the URL
is not clean. How do we change it something nice like `http://todo-app.me`. We
use [virtual hosts](http://httpd.apache.org/docs/2.2/vhosts/examples.html) in
Apache to do this.
