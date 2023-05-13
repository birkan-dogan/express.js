# Node.js

Node.js is a server-side JavaScript runtime environment that allows developers to build scalable and high-performance web applications using JavaScript. Unlike client-side JavaScript, which is executed by a browser's JavaScript engine, Node.js runs on the server-side, allowing developers to use JavaScript for both front-end and back-end development. We have JavaScript outside of the browser in a kind of standalone environment which just node.js.  

Node.js provides a range of built-in modules that make it easy to handle tasks such as file system access, network communication, and data processing. It also has a large and active community of developers who contribute to a wide variety of open-source modules and tools that can be easily integrated into Node.js applications.  

One of the key advantages of Node.js is its ability to handle large volumes of data and requests efficiently, making it well-suited for building real-time applications such as chat applications, online gaming platforms, and streaming services. Node.js also provides a non-blocking I/O model, which allows for asynchronous processing of requests, resulting in faster response times and better performance.  

Node.js is really built around concept of modules where all kind of additional functionality are stored in a module.

## NPM (Node Package Manager)
NPM is a package manager for Node.js. It allows developers to easily install and manage third-party libraries, modules, and tools that can be used in their Node.js projects.  
```bash
npm init
```
`npm init` will basically initialize a new Node.js project and create a package.json file in your project directory. The package.json file is used to manage your project's dependencies, scripts, metadata, and other configuration details.  
 NPM provides access to a wide range of open-source packages that can be installed and used in Node.js projects. Here are some examples of the types of packages you can install with npm:  
- Frameworks: npm provides access to a wide range of frameworks for building web applications, APIs, and more. For example, we can install the Express.js framework for building web servers or the Vue.js framework for building user interfaces.  
- Libraries: npm provides access to a wide range of libraries for handling various tasks in Node.js projects. For example, we can install the Moment.js library for handling dates and times or the Lodash library for working with arrays and objects.  
- Tools: npm provides access to a wide range of tools for improving our development workflow. For example, we can install the Nodemon tool for automatically restarting our Node.js server when changes are made or the ESLint tool for enforcing code quality standards.  
- Utilities: npm provides access to a wide range of utility packages for performing various tasks in Node.js projects. For example, we can install the Debug package for adding debugging information to our code or the Axios package for making HTTP requests.

In general, npm provides access to a vast ecosystem of packages that can help us build, test, and deploy our Node.js projects more efficiently and effectively. Whether we're building a web application, a command-line tool, or anything in between, there's likely a package on npm that can help us get the job done.  

**package versioning and updating** "packageName":"majorVersion.newFeatures.fixingSomeBugs"

## Express.js
 Express.js is a popular Node.js web application framework that provides a simple, powerful set of features for building web applications and APIs. Here are some of its key features:
- **Routing:** Express.js provides a simple and flexible routing system for defining endpoints and handling HTTP requests. We can define routes for specific HTTP methods (e.g. GET, POST, PUT, DELETE), and handle requests using functions known as middleware. 
- **Middleware:** Express.js middleware are functions that can be chained together to handle requests in a specific order. Middleware functions can perform various tasks, such as authentication, logging, parsing request bodies, and more.
- **Templating:** Express.js provides support for various template engines, such as EJS and Pug, which allow us to render dynamic HTML pages based on data from your application.
- **Error handling:** Express.js provides a robust error handling system that allows us to handle errors and exceptions in a consistent and flexible way.
- **Static file serving:** Express.js makes it easy to serve static files, such as images, CSS, and JavaScript files, from our web server.
- **Security:** Express.js includes built-in security features, such as HTTP headers for preventing cross-site scripting (XSS) and cross-site request forgery (CSRF) attacks.
- **Third-party integration:** Express.js makes it easy to integrate with other third-party packages and services, such as databases, caching systems, and more.  
- Also, Express.js makes it easier to organize our application into the **MVC architecture**.  

### Installation
```bash
npm i express
```
> We can have all the Express.js configuration in app.js file
```javascript
// Import Express.js
const express = require("express");
const app = express();  // now, app variable has bunch of methods
```
> to start our server
```javascript
const port = 8000;
app.listen(port, ()=>{
    console.log('Server listening on port 8000!');
});
```
> Next, we'll need to define a route that will handle incoming HTTP requests to our server. We can do this using the **app.get()** method, which will create a route that handles GET requests to a specified URL.
```javascript
app.get('/', (req, res)=> {
  res.status(200).send('Hello, world!');
});
```
```javascript
// response in json format
app.get("/", (req, res)=>{
    res.status(200).json({message:"message from the server", app:"appName"})
});
```

- When we use methods like res.send(), res.json(), or res.sendFile() in Express.js, the framework automatically sets certain headers in the response object, based on the content being sent. For example, when we use res.send() to send a string, the Content-Type header is set to text/html, unless we specify a different content type. Similarly, when we use res.json() to send a JSON object, the Content-Type header is set to application/json.  
- Here are some of the default headers that Express.js sets automatically, based on the content being sent: Content-Type, Content-Length, Cache-Control, Last-Modified  

### Middleware
In an Express.js application, a middleware is a function that sits in between the incoming request and the final route handler, and can perform some processing or modification on the request and/or response objects.  

Middleware functions are executed sequentially in the order they are defined, and can perform tasks such as logging, authentication, data parsing, error handling, and more.  

Express.js provides built-in middleware functions as well as the ability to define custom middleware functions. Here are some of the built-in middleware functions provided by Express.js:  
- **express.json():** This middleware function parses incoming JSON requests and makes the parsed data available in req.body
- **express.urlencoded()**: This middleware function parses incoming URL-encoded requests and makes the parsed data available in req.body.
- **express.static()**: This middleware function serves static files from a directory on the server.
- **morgan()**: This middleware function logs incoming requests and their associated responses.
- **cookieParser()**: This middleware function parses cookies in incoming requests and makes them available in req.cookies.
> We can also define our own middleware functions using the app.use() method. Here's an example:
```javascript
// we define a middleware function that simply logs a message to the console
app.use((req, res, next) => {
  console.log('Middleware function called');
  next(); 
  // next() function to pass control to the next middleware function or route handler.
});
```
### Middleware and the request-response cycle
Express app receives a request when someone hits a server, it will then create a request and response objects.  

Middleware manipulates the request or the response object, or any other code that we like.  

```javascript
app.use((req, res, next)=>{
   req.requestedTime = new Date().toISOString();
   next();
})
```

**We always send back something to finish the request/response cycle.**  
> Using third-party middleware
```bash
npm i morgan
```
```javascript
const morgan = require("morgan");
app.use(morgan("dev"));
```

### MongoDB Connection and Mongoose
**Mongoose** allows developers to define data models and schema structures for MongoDB collections in a way that makes working with data more organized and efficient.  
Here are some of the key features and benefits of Mongoose:

- **Schema-based modeling:** Mongoose provides a way to define data models and schema structures for MongoDB collections, which makes it easier to validate and manage data, as well as to enforce consistency and integrity across our application.
> **Take the schema and create a model out of it and perform each of the CRUD operation**

- **Validation:** Mongoose allows us to define custom validation rules for our data models, so we can ensure that data is consistent and correct before it is saved to the database.

- **Querying:** Mongoose provides a rich set of query APIs that allow us to perform complex queries on MongoDB databases, including filtering, sorting, limiting, and pagination.  

- **Middleware:** Mongoose provides middleware support, which allows us to define hooks that get executed before or after certain events occur, such as saving, updating, or removing documents from the database.

- **Virtuals:** Mongoose provides support for virtual properties, which are properties that are not persisted to the database, but are computed on the fly based on other properties.

- **Population:** Mongoose provides a way to reference documents from other collections, and to retrieve them automatically when querying a parent document.

```bash
npm i mongoose
```
```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<database>?retryWrites=true&w=majority', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  useCreateIndex: true,
}).then((con) => console.log("DB connection successful!")).catch((error)=>console.log(error));

// connect() method returns a promise, so we should handle it.
```
### Create a simple mongoose-schema and create documents in mongodb
> **in model.js**
```javascript
const mongoose = require('mongoose');

const Schema = mongoose.Schema;

const ProductSchema = new Schema({
  name: {
    type: String,
    required: [true, "A tour must have a name"],
    unique: true,
    trim: true,
    // trim only works for strings
  },
  description: {
    type: String,
    required: [true, "A tour must have a duration"],
  },
  price: {
    type: Number,
    required: true,
  },
  date: {
    type: Date,
    default: Date.now,
  },
  image: {
    type: [String],
    required: true,
  }
});

// create a model from the schema
const Product = mongoose.model('Product', ProductSchema);

module.exports = Product;

```
> **in controller.js**, create documents by using this model and after that, we should declare an endpoint for this function.
```javascript
exports.createProduct = async (req, res) => {
  try {
    const newProduct = await Product.create(req.body);
    // create() method returns a promise

    res.status(201).json({
      status: "success",
      data: {
        newProduct
      },
    });
  } catch (error) {
    res.status(400).json({ status: "fail", message: error });
  }
};
```
> endpoint for POST request **in router.js**
```javascript
const express = require("express");

const { createProduct } = require("../controller/productController");

const router = express.Router();

router.route("/").post(createProduct);

module.exports = router;
// and we can use the router in app.js file
``` 
### Reading documents that comes from mongodb by using mongoose
```javascript
// get all documents 

exports.getAllProducts = async (req, res) => {
  try {
    const products = await Product.find();
    // .find() method returns all the documents and promise

    res.status(200).json({
      status: "success",
      data: {
        products
      },
    });
  } catch (error) {
    res.status(404).json({
      status: "fail",
      message: error,
    });
  }
};
```

```javascript
// get specific document

exports.getProduct = async (req, res) => {
  try {
    const product = await Product.findById(req.params.id);
    // .findById() method is mongoose feature
    res.status(200).json({
      status: "success",
      data: {
        product,
      },
    });
  } catch (error) {
    res.status(404).json({
      status: "fail",
      message: error,
    });
  }
};
```

> We have access this function by using the special endpoint
```javascript
router.route("/:id").get(getProduct);
```
### Update product based on the parameter in the url.
```javascript

exports.updateProduct = async (req, res) => {
  try {
    const product = await Product.findByIdAndUpdate(req.params.id, req.body, { new: true, runValidators: true });

    res.status(200).json({
      status: "success",
      data: { product },
    });
  } catch (error) {
    res.status(400).json({ status: "fail", message: error });
  }
};
```
- **{ new: true }**: This parameter tells Mongoose to return the updated document after the update operation is complete. If we omit this parameter, the method will return the old document before it was updated.
- **{ runValidators: true }**: This parameter tells Mongoose to run the validators specified in your schema when performing the update operation. This includes things like checking for required fields and validating data types.

```javascript
// also, we can use the same endpoint, but different http method
router.route("/:id").get(getProduct).patch(updateProduct); 
```

### Delete product based on the parameter in the url.
```javascript
exports.deleteProduct = async (req, res) => {
  try {
    await Product.findByIdAndDelete(req.params.id);

    res.status(204).json({
      status: "success",
      data: null,
    });
  } catch (error) {
    res.status(400).json({ status: "fail", message: error });
  }
};
```
> endpoint for that:
```javascript
router.route("/:id").get(getProduct).patch(updateProduct).delete(deleteProduct);
```

