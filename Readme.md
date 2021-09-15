# Node JS Runtime - with Express JS and Mongo DB

Node JS is a JavaScript runtime built on google's v8 javascript engine which allows user to run JavaScript outside the browser without having the restrictions seen in browser

> Node JS = ( v8 ( JavaScript ) )

### Adv of Node JS -

> 1.  Accessing the file system
> 2.  Better Network Capabilities
> 3.  Single threaded event driven non-blocking I/O model
> 4.  Perfect for building fast and sclable data intensive apps
> 5.  JavaScript across the entire stack, faster and more efficient development
> 6.  NPM - huge library of open source packages
> 7.  Huge dev community

### Use of Node JS -

> 1.  Building API with database
> 2.  Data Streaming supported Apps
> 3.  Real time chat application
> 4.  Server-side web application

### Don't use Node JS for -

> 1.  Apps with heavy server side processing (CPU Intensive)

### Running Node in CLI mode

> node <br>
> Enter the commands or script to run in the CLI

### Exiting the Node in CLI mode

> .exit

### Synchronous Reading and Writing Files

> const fs = require("fs"); <br>
> const textIn = fs.readFileSync("./txt/input.txt", "utf-8");

> const textOut = '`This is an example of writing file to existing file: ${testIn}. \n Created on ${Date.now()}`'; <br>
> fs.writeFileSync("./txt/Output.txt", textOut);

### Synchronous vs Asynchronous (Blocking vs Non-Blocking Code)

> Sync functions can block the task until the result is obtained from the running process. This is called as blocking code. <br> This problem can be avoided by using the non-blocking code using the async functions that run in the background and carry on with the rest of the process.

### Node JS Thread

> For each application only one thread is available. This means when ever the code runs, it can be executed on a single thread only, irrespective of the number of users or applicatioons accessing the thread. Only one thread is available to all. So, when a single user blocks the thread with a sync function, the other application or users can not use the thread for execution. Thus the callbacks based async functions are used. The function can process in the background and the result is returned via a callback function and this allows the other users to use the avtive thread for various other operatinos. <br>Not all callbacks are async.

The problem -> Callback Hell

> Nested callbacks can lead to congestion and this can be overcome by using <br> 1. async and await <br> 2. Promises

### Asynchronous Reading and Writing Files

> fs.readFile('`./txt/${data1}.txt`', "utf-8", (err, data2) => { <br>
> console.log("async reading: ", data2);<br>
> });

> fs.writeFile('./txt/final.txt','`${data2} \n ${data3}`','utf-8',(err)=>{})

### Creating a Simple web Server

> const http = require("http"); <br>const server = http.createServer((req, res) => { <br>
> res.end("Hello from the server!"); <br>
> }); <br> server.listen(8000, "127.0.0.1", () => { <br>
> console.log("Listening to the incoming request..."); <br>
> });

### Routing in Node

> const url = require("url"); <br>const pathName = req.url; <br> if (pathName === "/" || pathName === "/overview") { <br> res.end("This is overview"); <br>
> } else if (pathName === "/product") { <br>
> res.end("This is product"); <br>
> } else { <br>
> res.writeHead(404, {<br> "Content-type": "text/html",<br> "my-own-header": "test header"<br> });<br> res.end("< h6> Page Not found</ h6>"); <br>
> }

### Building a simple web API

> const data = fs.readFileSync('`${__dirname}/dev-data/data.json`', "utf-8"); <br>
> const productData = JSON.parse(data); <br>
>
> else if (pathName === "/api") { <br> res.writeHead(200, {
> "Content-type": "application/json", }); <br> res.end(data); <br> }

### Parsing variables from URLs

> const path = req.url; <br>
> console.log(url.parse(path, true)); <br>
> const { query, pathname } = url.parse(path, true);

### Type of Package and Installs

> npm install express

this indicates a dependency required on production build

> npm install express --save-dev

this indicates a dev dependency required during the build cycle. Some dependency can be installed globally for use in multiple projects.

> npm install express --global

### How the web works

> Web works with the request-response model or the client-server architecture. <br> https://www.google.com/maps/ - https/http refers to protocol, www.google.com refers to the domain name, and /maps refers to the resource requested.
> <br>
> Client browser does a DNS lookup for the domain name and the path may look as below.
> <br> https://216.58.211.206:443/ <br> port 443 - HTTPS request and <br> port - 80 HTTP request
> <br> The request has some fundamental requirement like HTTP method + request target + HTTP version, HTTP request headers, Request Body (optional).
> <br> Similarly, the response has some fundamental requirement like HTTP version + status code + status message, HTTP response headers, Response Body

### Node architecture - v8 engine and libuv

> libuv is an open source library with focus on async I/O, event loop and thread pool support (for heavy lifting processing). <br>
>
> Process, threads and thread pool
> Single thread - sequence of instruction
>
> <ol> <li>Initialize the program </li>
> <li>Execute top level code</li><li>Require modules</li><li>Register Callbacks</li><li>Start Event Loop</li></ol>
> In case of heavy lifting or CPU intensive operations, Node used Thread pool that provides an additional of 4 threads. This can be extended upto 128 thread on demand. The event loop can offload tasks to thread pool. <br>ex- file operations, cryptography, compression, DNS look-up, etc.

### The Node JS Event Loop

> Event loops works with the callback queues. <br> Start<ol><li>Expired tiemr callbacks - setTimeout(), etc</li><li>I/O polling and callbacks - file read write, networking etc</li><li>setImmediate callbacks </li><li>Close callbacks - web socket shutdown, etc</li></ol> Node then checks if any pending I/O tasks or timer are available, if yes the loop again, if not, exit the program. <br> There are two other special queues. <ol><li>PROCESS.NEXTTICK() queue</li><LI>Other microtasks queue</LI></ol>

### Event Loop in action

> const fs = require("fs");<br>
> setTimeout(() => console.log("timer 1 finished"), 0);<br>
> setImmediate(() => console.log("Immediate 1 finished"));<br>
> fs.readFile("/test-file.txt", () => { <br>
> console.log("I/O finished \n-----------------------------"); <br>
> setTimeout(() => console.log("timer 2 finished"), 0); <br>
> setTimeout(() => console.log("timer 3 finished"), 3000); <br>
> setImmediate(() => console.log("Immediate 2 finished")); <br>
> process.nextTick(() => console.log("Process.nextTick()")); <br>
> }); <br>
> console.log("Hello from the top level code");

This will result in the below Output: -

> Hello from the top level code<br>
> timer 1 finished <br>
> Immediate 1 finished<br>
> I/O finished<br>
> Process.nextTick() <br>
> Immediate 2 finished<br>
> timer 2 finished<br>
> timer 3 finished

Setting the thread pool size to use lesser than 4 default threads

> process.env.UV_THREADPOOL_SIZE = 2;

### Event and Event-Driven Architecture in a Nutshell

> Event emitter - emits named event (request hitting the server, timer expiring, file finished reading) <br> Event Listeners - picks up the emitted events (set up by devs) <br> Attached callback functions - event listeners reacts to event by calling the attached callbacks.

EventEmitter in Action

> const EventEmitter = require("events"); <br> const myEmitter = new EventEmitter(); <br> myEmitter.on("newSale", () => console.log("there was a new sale")); <br> myEmitter.emit("newSale", 9);

Streams

> Streams are used for processing the data piece by piece (read or write) without completing the whole read/write operation at once and thus keeing the memory free. Streams are perfect for handling huge amount of data. More efficient in Data processing in terms of memory (no need to keep all the data in memory) and Time (no need to wait until all data is available) <br>Type of Stream: -<ol><li>Readable Stream - streams from which we can read (consume) data<ul><li>Example - http requests, fs read streams</li><li>Important Events - data, end</li><li>Important functions - pipe(), read()</li></ul></li><li>Writable Stream - Streams to which we can write data <ul><li>Example - http response, fs write streams</li><li>Important Events - drain, finish</li><li>Important functions - write(), end()</li></ul></li><li>Duplex Stream - Streams that are both readable and writable <ul><li>Example - net web socket</li></ul></li><li>Transform Stream - Duplex streams that transform data as it is written or read<ul><li>Example - zlib Gzip creation</li></ul></li></ol>

Stream in Action: -

> const readable = fs.createReadStream("test-file.txt"); <br>
> readable.on("data", (chunk) => { res.write(chunk); }); <br>
> readable.on("end", () => { res.end(); }); <br>
> readable.on("error", (err) => { res.statusCode = 500; res.end("Error"); });

Optimising using pipes

> server.on("request", (req, res) => {<br>const readable = fs.createReadStream("test-file.txt"); <br>
> readable.pipe(res); }); <br>
> // readabelSource.pipe(writableDestinations)

### Asynchronous JS - Promises and await

Consuming Promises

> axios<br>.get('https://github.com/') <br> .then( (res)=>{ console.log(res.body.message) } )<br>.catch( (err)=>{ console.log(err.message) } );

Consuming Promises with await

> const asyncGet = async () = > {<br> try { <br> const data = await axios.get('https://github.com/')<br> } catch(err) {<br> console.log(err) } <br>} <br> asyncGet();

await multiple promise

> const asyncGet = async () = > {<br> try { <br> const pro1 =axios.get('https://github.com/')<br> const pro2 =axios.get('https://github.com/')<br> const pro3 =axios.get('https://github.com/')<br> const all = await Promise.all( [pro1, pro2, pro3] ); <br>} catch(err) {<br> console.log(err) } <br>} <br> asyncGet();

# Express JS

### What is Express JS?

> Express is minimal node js framework.<br> Express contains a very robust set of features like: complex routing, easier handling of requests and responses, middleware, server-side rendering, etc.

### Express and basic routing

> const express = require('express'); <br>
> const app = express();<br>
> app.get('/', (req, res) => { <br>
> res.status(200).json({ message: 'hello from the server', app: 'Natours' });<br>
> });<br>
> const port = 3000;<br>
> app.listen(port, () => {<br>
> console.log('listening on port ', `${port}`);<br>
> });

### API and Restful API Design

> API (Application Programming Interface) is a piece of software that can be used by another piece of software, in order to allow applications to talk to each other (data or methods). <br> Rest Architecture - Representational State Transfer <ol><li>Separate API into logical resources - any information that can be named can be a resource. Ex: - users, review, etc.</li><li>Expose structured resource-based URLs - /users, /tours, etc </li><li>Use HTTP methods - GET, PUT, POST, PATCH, DELETE</li><li>Send data as JSON (usually)</li><li>Be stateless - all the state should be handled at the client, meaning each request must contain all the information necessary to process the request. The server should not have to remember the previous requests</li></ol>

### Parameters from request URLs

> app.get('/api/v1/tours/:id, (req, res)=>{<br> console.log( req.params);<br>}); <br>Here :id refers to parameter in the request URL who's value is required to be sent from the client side.

Adding optional Parameters

> app.get('/api/v1/tours/:id?, (req, res)=>{<br> console.log( req.params);<br>}); <br>Here :id? refers to an optional parameter in the request URL who's value may not be sent as part of the request URL.

### Refactoring the Routes

> app.get('/', (req, res) => { <br>
> res.status(200).json({ message: 'hello from the server', app: 'Natours' }); <br>
> });

This can be written as below: -

> const defaultRoute = (req, res) => { <br>
> res.status(200).json({ message: 'hello from the server', app: 'Natours' }); <br>
> } <br><br> app.get( '/', defaultRoute );

Chaining the Routes

> app.route( '/api/v1/tours' ).get( getTours ).post( updateTours );

### Express Development: The Request - Response Cycle

> Incoming Request --> Middleware --> Response
> <br><ol><li>Incoming Request - req obj and res obj</li><li>Middleware<ol><li>next() - parsing the body</li><li>next() - Logging</li><li>next() - Setting Headers</li><li>res.send() - router</li></ol></li><li>Response</li></ol>

Creating a middleware

> app.use((req, res, next) => { <br>
> req.reqTime = new Date().toISOString(); <br>
> next(); <br>
> }); <br><br>app.get('/', (req, res) => {
> res.status(200).json({requestedAt: req.reqTime,}); <br>
> }); <br>The middleware are executed in order of the creation. Thus, if the middleware is defined after the route, that middleware will not be used by the request or currrently called route.

Param Middleware

> const router = express.Router(); <br> <br> router.param( 'id' , ( req, res, next, val ) =>{<br> console.log( '`Tour id is: ${val}`' );<br> next();<br> }); <br><br> router.route( '/:id' )<br>.get( getAllTours )<br>.post( createNewTour );

Serving Static Files

> app.use( express.static ( '`${__dirname}/public`' ) );

### Connecting to MongoDB using Express

Connecting to local or hosted database

> const mongoose = require('mongoose'); <br> const DB = process.env.DATABASE_URI; <br> mongoose <br>
> .connect(DB, { <br> useUnifiedTopology: true,<br> useNewUrlParser: true, <br> useCreateIndex: true, <br> useFindAndModify: false <br>}) <br>
> .then(conn => console.log(conn.connections))<br>.catch(err => console.log(err));

### Creating a Document Model - Schema in Express for MongoDB Collection

> const tourSchema = new mongoose.Schema({ <br>
> name: { <br>
> type: String, <br>
> required: [true, 'A tour must have a name'], <br>
> unique: true <br>
> }, <br>
> rating: { type: Number, default: 4.5 }, <br>
> price: { type: Number, required: [true, 'A tour must have a price'] } <br>
> }); <br><br>
> const Tour = mongoose.model('Tour', tourSchema);

### Creating a Document in MongoDB Collection using Express

> const newTour = new Tour({ <br> name: 'The Park Camper', <br> price: 497 <br> });
> <br><br>newTour <br>
> .save() <br>
> .then(doc => { <br>
> console.log(doc); <br>
> }) <br>
> .catch(err => { <br>
> console.log(err); <br>
> });

### Backend Architecture - MVC, Logic Types and more

> MVC components <ul><li>Model - Business Logic</li><li>View - Presentation Logic</li><li>Controller - Application Logic </li></ul>

Application Vs Business Logic

> Application <ul><li>Managing requests and responses</li><li>Bridge between model and view logic</li></ul>
> Business <ul><li>How the business works, or the business needs</li><li>Example: - <ul><li>Creating a new Collection in the database</li><li>Checking if user password is correct</li><li>Validating users input data</li><li>Ensure authenticated access</li></ul></li></ul>
> Offload as much as logic as possible into the models and keep the controllers are simple and lean as possible.

### Filtering the results - Using query parameters

> // destructuring the query params to create a query object
> <br>const queryObj = { ...req.query }; <br> const excludedFields = ['page', 'sort', 'limit', 'fields']; <br> excludedFields.forEach(el => delete queryObj[el]); <br><br>let queryStr = JSON.stringify(queryObj); <br> queryStr = queryStr.replace(/\b(gte|gt|lte|lt)\b/g, match => { <br> return `$${match}`; <br> }); <br><br> const query = Tour.find(JSON.parse(queryStr)); <br> const tours = await query;

### Sorting the results - Using query parameters

> let query = Tour.find(JSON.parse(queryStr)); <br><br>// Ascending Sorting - 127.0.0.1:3000/api/v1/tours?difficulty=easy&duration[gte]=5&<strong>sort=price</strong> <br> if (req.query.sort) { <br> query = query.sort(req.query.sort); <br> }<br><br>// Descending Sorting - 127.0.0.1:3000/api/v1/tours?difficulty=easy&duration[gte]=5&<strong>sort=-price</strong> <br> if (req.query.sort) { <br> query = query.sort(req.query.sort); <br> } <br> const tours = await query;

Multiple fields in sorting

> // 127.0.0.1:3000/api/v1/tours?difficulty=easy&duration[gte]=5&sort=-price,-ratingsAverage <br><br> if (req.query.sort) { <br> const sortBy = req.query.sort.split(',').join(' '); <br> query = query.sort(sortBy); <br>} <br> const tours = await query;

### Field Limiting - Using query parameters

> Field limiting also known as projecting <br>// 127.0.0.1:3000/api/v1/tours?fields=name,duration,difficulty <br><br>
> if (req.query.fields) { <br> const field = req.query.fields.split(',').join(' '); <br> // Example - query = query.select('name duration price'); <br> query = query.select(field); <br> } <br> const tours = await query;

Field limiting at schema level

> createdAt: { type: Date, default: Date.now(), <strong>select: false </strong>},

### Pagination - Using query parameters

> // page=2$limit=10 <br> // query = query.skip(10).limit(10) <br><br> const page = req.query.page \* 1 || 10; <br> const limit = req.query.limit _ 1 || 100; <br> const skip = (page - 1) _ limit; <br> query = query.skip(skip).limit(limit); <br> const tours = await query;

### Aggregation Pipeline - Matching and Grouping

> const stats = await Tour.aggregate([ <br> { <br> $match: { ratingsAverage: { $gte: 4.5 } } <br> }, <br> { <br> $group: { <br> _id: { $toUpper: '$difficulty' }, <br> // _id: '$ratingsAverage', <br> numRatings: { $sum: '$ratingsQuantity' }, <br> numTours: { $sum: 1 }, <br> avgRating: { $avg: '$ratingsAverage' }, <br> avgPrice: { $avg: '$price' }, <br> minPrice: { $min: '$price' }, <br> maxPrice: { $max: '$price' } <br> } <br> }, <br> { <br> $sort: { <br> avgPrice: 1 <br> } <br> }, <br> // { <br> // $match: { _id: { $ne: 'EASY' } } <br> // } <br> ]);

### Aggregation Pipeline - Unwinding and Projection

> const plan = await Tour.aggregate([ <br> { <br> $unwind: '$startDates' <br> }, <br> { <br> $match: { <br> startDates: { <br> $gte: new Date( `${year}-01-01` ), <br> $lte: new Date( `${year}-12-31` ) <br> } <br> } <br> }, <br> { <br> $group: { <br> _id: { $month: '$startDates' }, <br> numTourStarts: { $sum: 1 }, <br> tours: { $push: '$name' } <br> } <br> }, <br> { <br> $addFields: { month: '$_id' } <br> }, <br> { <br> $project: { _id: 0 } <br> }, <br> { <br> $sort: { numTourStarts: -1 } <br> }, <br> // { <br> // $limit: 12 <br> // } <br> ]);

### Virtual Properties

> Virtual properties are not defined at the collection level and are defined at the Schema level. These properties will not be available for querying the actual document in the collections. <br> <br>const tourSchema = new mongoose.Schema( <br> { <br> ... <br> }, {<br> toJSON: { virtuals: true }, <br> toObject: { virtuals: true } <br> } <br> ); <br> <br> tourSchema.virtual('durationWeeks').get(function() { <br> return this.duration / 7; <br> }); <br><br> const Tour = mongoose.model('Tour', tourSchema);

### Middlewares in Mongoose

> <ul> <li>Document</li> <li>Query</li> <li>Aggregate</li> <li>Date model</li> </ul>

Document Middleware

> // Document Middleware : runs before .save() and .create() functions only <br><br> tourSchema.pre('save', function(next) { <br> this.slug = slugify( this.name, { lower: true }); <br> next(); <br> });

Query Middleware

> // Query middleware : .find() <br><br>
> // tourSchema.pre('find', function(next) { <br>
> tourSchema.pre(/^find/, function(next) { <br>
> this.find({ secretTour: { $ne: true } }); <br>
> this.start = Date.now(); <br>
> next(); <br>
> });

Aggregation Middleware

> // Aggregation Middleware : .aggregate() <br><br>
> tourSchema.pre('aggregate', function(next) { <br>
> this.pipeline().unshift({ $match: { secretTour: { $ne: true } } }); <br>
> console.log(this.pipeline()); <br>
> next(); <br>
> });

### Custom Validators - Schema Level Validation

> {<br> ... <br> priceDiscount: { <br> type: Number, <br> validate: { <br> validator: function(value) { <br> return value < this.price; <br> }, <br> message: 'Discount price should be below the regular price' <br> } <br> ... <br> },

### Error Handling with Express

Debugging Node.js with ndb

> npm i ndb --global <br><br>
> define a script in the package.json
> "scripts": { <br> "debug" :"ndb server.js" <br> },

Handling unhandled Routes

> app.use('/api/v1/tours', tourRouter); <br>
> app.use('/api/v1/users', userRouter); <br> <br>
> app.all('\*', (req, res, next) => { <br>
> // console.log(req.originalUrl); <br>
> res.status(404).json({ <br> status: 'failed', <br> message: `Can not find ${req.originalUrl} resource on this server!` <br> }); <br>
> });

Overview of Error Handling

> <ol><li>Operational Errors <ul><li>Invalid path request</li> <li>Invalid user input</li><li>Failed to connect to the server</li><li>Failed to connect to the database</li><li>Request Timeout, etc.</li></ul></li> <li>Programming Errors <ul><li>Reading properties on undefined</li> <li>Using await with async and vice-versa</li><li>Using req.query instead of req.body</li><li>Passing a number where an object is expected, etc.</li></ul></li> </ol>

Implementing a global error handling middleware

> app.use((err, req, res, next) => { <br>
> err.statusCode = err.statusCode || 500; <br>
> err.status = err.status || 'error'; <br>
> res.status(err.statusCode).json({ <br> status: err.status, <br> message: err.message <br>
> }); <br>
> }); <br><br>
> Refracting the error handler as a separate module <br><br>
> module.exports = (err, req, res, next) => { <br>
> err.statusCode = err.statusCode || 500; <br>
> err.status = err.status || 'error'; <br>
> res.status(err.statusCode).json({ <br> status: err.status, <br> message: err.message <br>
> }); <br>
> next(); <br>
> };

### Unhandled Promise Rejection and Uncaught Exception

Handling Promise Rejection

> process.on('unhandledRejection', err => { <br>
> console.log(err.name, err.message); <br>
> server.close(() => { <br> process.exit(1); <br> }); <br> });

Handling Uncaught Exception

> process.on('uncaughtException', err => { <br>
> console.log(err.name, err.message); <br>
> process.exit(1); <br>
> }); <br>

### Authentication, Authorization and Security

> npm i bcryptjs <br> npm package for password hashing

Document middleware for hashing passwords

> userSchema.pre('save', async function(next) { <br>
> if (!this.isModified('password')) return next(); <br>
> // cryptographing the password <br>
> this.password = await bcrypt.hash(this.password, 12); <br>
> this.passwordConfirm = undefined; <br> next(); <br>
> });

Authentication with JWT (JSON web token) - How JWT Works?

> In simple terms <ol><li>Client sends request to server over a HTTPS commection with email/username and password.</li><li>Server checks the user exists and details are correct.</li><li>If the details are correct, a unique JWT is created with a secret stored on the server and sent back.</li><li>Client stores the token either as a cookie or local storage.</li><li>If the user wants to request a protected resource on the server, the user sends the JWT with the request.</li><li>If the JWT is valid, requested data is sent back, else error.</li></ol>All the communication must happen over a secured HTTPS connection. <br><br> Parts of a JWT decoded <ul><li>Header - metadata about the token.</li><li>Payload - data to be encoded in the token.</li><li>Verify Signature - is created using the header, payload and the secret to create a signature</li></ul> <br> Verifying the JWT <ol><li>When a JWT is received, a test signature is constructed with the header+payload in the JWT and the secret on the server</li><li>The JWT consists of a original signature sent with the token.</li><li>Compare the test signature with the original signature</li><li> If, testSignature === originalSignature => Data is not modified, Authenticated</li><li> If, testSignature !== originalSignature => Data is modified, Not Authenticated</li></ol> Without the secret, the signature can't be created again.

# Mongo DB

What is Mongo DB?

> Mongo is a NoSQL database. Tables in Mongo DB are known as Collections and data rows are called Document with data format similar to JSON. <br> Mongo DB stores data in Documents (field-value pair data structures). <br> Mongo DB is scalable to distribute data across multiple machines as the users or amount of data grows. <br> Flexible - No document data schema required, so each document can have different number and type of fields. <br> Preformant - Embedded data models, indexing, sharding, flexible documents, native duplication, etc.

### Working with MongoDB

> Create the database directory to store the collections on localhost. <br>
>
> > md c:\data\db

> Run "mongod" command from terminal to start the server. On a new termial run "mongo" command to start accessing the server via shell.

Creating or Accessing a Database

> use <collectino_name><br> Ex:- use natours-test

Listing all the existing databases

> show dbs

Creating a new Collections with data

> db.tours.insertOne( { name:"Forest", price:297, rating:4.7 } ) <br> This will generate an entry in the tours collection for the current database instance db. The result of the above query will look like: - <br>{ <br>"acknowledged" : true, <br> "insertedId" : ObjectId("6135db10558c29c68e93fa89") <br>}

Reading a Existing Document in the Collection

> db.tours.find()
> <br> This will provide the documents currently in the Collection. <br>
> { "\_id" : ObjectId("6135da64558c29c68e93fa88"), "name" : "Forest", "price" : 297, "rating" : 4.7 }
> <br>{ "\_id" : ObjectId("6135db10558c29c68e93fa89"), "name" : "River", "price" : 297, "rating" : 4.7 }

Listing all the Collection in the current Database.

> show collection

### CRUD Operations in Mongo DB

Create

> db.tours.insertMany( [ <br>{ name:"River", price:297, rating:4.7 }, <br>{ name:"Mountain", price:297, rating:4.7 } <br>] ) <br> This will result in the below output: - <br>{ <br> "acknowledged" : true, <br> "insertedIds" : [ <br> ObjectId("6135dd41558c29c68e93fa8a"), <br> ObjectId("6135dd41558c29c68e93fa8b") <br> ] <br> }

Read

> db.tours.find() - returns all the data in the tours collection <br><br> db.tours.find({ name:"River" }) - returns data for all the document with name = River.<br> <br> db.tours.find({ price: { $lte: 500 } }) - returns the data for tours with price < 500. $lte is mongo representation for less than and the comparison works again with an object defined as $lte. <br> <br> db.tours.find({ price: { $lte: 450 }, rating: { $gte: 4.5 } }) - return data by considering both the conditions to be true. <br><br> db.tours.find({ $or: [ {price: {$lte:450}}, {rating: {$gte:4.5}} ] }) - this returns data if either of the one condition hold true.<br><br>db.tours.find({price : {$lte:450}, rating :{$gte:4.5}}, {name:1} ) - returns only the name in the document that satisfies the comdition. <br> Output: - { "\_id" : ObjectId("6135dd41558c29c68e93fa8b"), "name" : "Mountain" }

Update

> db.tours.updateOne( {name:"River"}, { $set:{price: 1000} }) - updates one document with one field change
<br><br>  db.tours.updateOne( {name:"River"}, { $set:{price: 800 ,rating:4.9} }) - updates multiple field for a given document. <br><br> db.tours.updateMany({rating :{$lt:4.9}, price:{$lte:500}} , {$set:{premium:false}}) - updates the fields for multiple document based on the condition. <br><br> db.tours.replaceOne( {name:"River"} , {test:"test"} ) <br>// db.tours.replaceOne( {search_condition} , {new_data_to_be_updated} ) <br> - replaces the entire data of the matching document with the new data.

Delete

> db.tours.deleteOne({ name:"test"}) - removes one entry from the collection<br><br> db.tours.deleteMany({ premium:false}) - removes multiple document entries, if exists from the collection based on the condition. <br><br> db.tours.deleteMany( {} ) - removes all the documents from the collection. This operation is irreversible and must be done with caution.
