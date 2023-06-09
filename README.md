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
### Aggregation Pipeline
The aggregation pipeline is a powerful feature that allows us to perform complex queries and data manipulations on MongoDB collections. It provides a framework for specifying a sequence of data processing steps that are applied to documents in a collection, allowing us to perform operations such as filtering, sorting, grouping, and transforming data.  

The aggregation pipeline consists of one or more stages, with each stage representing a clear data processing step. Each stage takes input from the previous stage, processes the data, and outputs the results to the next stage. The output of the final stage is the result of the entire pipeline.  

**Some of the common stages used in the aggregation pipeline include:**  
- **$match:** filters documents based on certain conditions.
- **$group:** groups documents based on a specified key and performs aggregate functions on each group.  
- **$sort:** sorts documents based on specified criteria.
- **$project:** selects specific fields from the documents and optionally transforms them.
- **$limit:** limits the number of documents in the output.
- **$skip:** skips a specified number of documents in the input.
- **$unwind:** to flatten an array field in a document. When we use **$unwind**, it creates a new document for each element in the array and duplicates the values of the other fields in the original document for each of those documents.

Using the aggregation pipeline, we can perform complex queries and data manipulations on MongoDB collections with a single query. This can be more efficient and flexible than using multiple queries or manipulating data in code.  

A new schema to implement aggregation pipeline:
```javascript
const userSchema = new Schema({
  name: {
    type: String,
    required: [true, "A user must have a name"],
    trim: true,
  },
  email: {
    type: String,
    required: [true, "A user must have an email"],
    unique: true,
    lowercase: true,
    trim: true,
  },
  password: {
    type: String,
    required: [true, "A user must have a password"],
    minlength: 8,
    select: false,
  },
  age: {
    type: Number,
    required: [true, "A user must have an age field"],
    min: [18, "A user must be at least 18 years old"],
  },
  createdAt: {
    type: Date,
    default: Date.now,
  },
  active: {
    type: Boolean,
    default: true,
  },
  products: [
    {
      title: {
        type: String,
        required: [true, "A product must have a title"],
      },
      description: {
        type: String,
        required: [true, "A product must have content"],
      },
      soldAt: {
        type: Date,
        default: Date.now,
      },
      tags: [String],
    },
  ],
});
```
> *Aggregate Pipeline Function*
```javascript

/*
an aggregation pipeline to group posts by tag, count the
number of posts in each group, and sort the groups by count in descending order:
*/

exports.tagsAndCount = async (req, res) => {
  try {
    const pipeline = await User.aggregate([
      // Unwind the posts array to create a separate document for each post
      { $unwind: "$products" },

      // Group posts by tag and count the number of posts in each group
      {
        $group: {
          _id: "$products.title",
          count: { $sum: 1 },
        },
      },

      // Sort the groups by count in descending order
      { $sort: { count: -1 } },
    ]);

    res.status(200).json({
      status: "success",
      result: pipeline.length,
      data: pipeline,
    });
  } catch (error) {
    res.status(400).json({ status: "fail", message: error });
  }
};
```
```javascript
/*
aggregation pipeline that finds all active users, groups them by age range, and calculates the average age and the total 
number of users in each age group:
*/
exports.projectAnalyse = async (req, res) => {
  try {
    const userPipeline = await User.aggregate([
      // Match users with active status
      { $match: { active: true } },

      // Project a new field with the age range for each user
      {
        $project: {
          _id: 1,
          name: 1,
          email: 1,
          age: 1,
          ageRange: {
            $switch: {
              // https://www.mongodb.com/docs/manual/reference/operator/aggregation/switch/#mongodb-expression-exp.-switch
              branches: [
                { case: { $lte: ["$age", 25] }, then: "18-25" },
                { case: { $lte: ["$age", 35] }, then: "26-35" },
                { case: { $lte: ["$age", 50] }, then: "36-50" },
                { case: { $gt: ["$age", 50] }, then: "Over 50" },
              ],
              default: "Unknown",
            },
          },
        },
      },

      // Group users by age range, calculate the average age, the total number of users, and push the names into an array.
      {
        $group: {
          _id: "$ageRange",
          avgAge: { $avg: "$age" },
          totalUsers: { $sum: 1 },
          name: { $push: "$name" },
        },
      },

      // Sort the age groups by average age in descending order
      { $sort: { avgAge: -1 } },
    ]);

    res.status(200).json({ status: "success", data: userPipeline });
  } catch (error) {
    res.status(400).json({ status: "fail", message: error });
  }
};

```
> To find the top 5 active users with the highest number of products, and includes their names, email addresses, and the count of their products:
```javascript

exports.topFive = async (req, res) => {
  try {
    const topFive = await User.aggregate([
      // Match users with active status
      {
        $match: { active: true },
      },

      // Project necessary fields
      {
        $project: {
          name: 1,
          email: 1,
          numProducts: { $size: "$products" },
        },
      },

      // Sort users by the number of products in descending order
      { $sort: { numPosts: -1 } },

      // Limit the result to the top 5 users
      { $limit: 5 },
    ]);

    res.status(200).json({ status: "success", result: topFive.length, data: topFive });
  } catch (error) {
    res.status(400).json({ status: "fail", message: error });
  }
};
```

## Mongoose Middlewares
Middleware in Mongoose allows us to define functions that execute at specific points in the lifecycle of a Mongoose model or document.  

Middleware functions can be used for various purposes, such as performing validation, modifying data, logging, or executing additional logic before or after specific operations.  
- **Validation:** We can use pre-save middleware to perform data validation before saving a document to the database. This allows us to ensure that the data meets certain criteria or apply custom validation logic.
- **Data manipulation:** Middleware functions provide an opportunity to manipulate the data before saving or retrieving it. For example, we can hash passwords, format dates, or transform the data in any desired way.  
- **Logging:** Middleware functions can be used to log specific events or actions related to your documents or queries. This can help with debugging, auditing, or monitoring the application. 
- **Triggering actions:** We can use middleware to trigger actions or update related documents when a specific operation occurs. For example, we might want to update a counter or send a notification when a document is saved or removed.
- **Error handling:** Middleware can be used to handle errors or perform cleanup operations in case an error occurs during a specific operation. This helps us centralize error handling and keep our code clean and maintainable.
- **Complex operations:** Middleware allows us to break down complex operations into smaller, manageable pieces. We can execute different parts of the operation in separate middleware functions, making our code more organized and easier to understand.  

By using middleware, we can add reusable and customizable logic to our Mongoose models, making it easier to maintain and extend our application.  

> Mongoose middleware functions can be categorized into 4 types:  

**1) Document middleware:** These functions are executed for specific document instances. They include the following middleware types:  
- **pre** middleware: These functions are executed before a specific operation on a document, such as *save*, *validate*, or *remove*.
- **post** middleware: These functions are executed after a specific operation on a document, such as *save*, *validate*, or *remove*.  
> in model.js
```javascript
const mongoose = require('mongoose');

const Schema = mongoose.Schema;

const schema = new Schema({
  name: String,
  age: Number
});

schema.pre('create', function(next) {
  // This middleware function will be executed before saving a document
  console.log('Saving document...');
  next();
});

schema.post('create', function(doc, next) {
  // This middleware function will be executed after saving a document
  console.log('Document saved:', doc);
  next();
});

```
**2) Query middleware:** Query Middleware allows us to run functions before or after a certain query is executed.  

> We have a User model and we want to implement access control to limit certain users from accessing sensitive data. We can use query middleware to automatically modify the query based on the user's permissions.   

> in `model.js`
```javascript

const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: String,
  role: String
});

const User = mongoose.model('User', userSchema);

module.exports = User;


```
- Now, let's say we have a sensitive field called secretData in the User collection that should only be accessible to users with the role of "admin". We can use query middleware to check all queries to the User collection and modify them to include an additional condition for role-based access control.

```javascript

const User = require('./user'); // Importing the User model

// Query middleware for 'find' operation on User collection
User.schema.pre(/^find/, function() {
  // Get the current user's role from the context or wherever we store user information
  const currentUserRole = 'admin';

  // Modify the query to include the role-based access control condition
  if (currentUserRole !== 'admin') {
    this.find({ role:{ $ne: 'admin' }});
  }
});
```
**3) Aggregation Middleware:** Aggregation middleware in Mongoose allows us to define functions that are executed before or after an aggregation operation is performed on a model. Aggregation middleware provides hooks at different stages of the aggregation pipeline, allowing us to add custom logic and manipulate the aggregation results.  
- `Pre` aggregate: Executed before an aggregation operation starts.
- `Post` aggregate: Executed after an aggregation operation is completed.

```javascript
schema.pre('aggregate', function() {
  // This middleware function will be executed before an aggregation operation
  console.log('Executing aggregation...');
});

schema.post('aggregate', function(result) {
  // This middleware function will be executed after an aggregation operation
  console.log('Aggregation completed:', result);
});
```
