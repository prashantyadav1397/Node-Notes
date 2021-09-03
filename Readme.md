# Node JS Runtime - with Express JS and Mongo DB

Node JS is a JavaScript runtime built on google's v8 javascript engine which allows user to run JavaScript outside the browser without having the restrictinos seen in browser

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

> 1.  Apps with heavy server side processing ( CPU intensive)

### Running Node in CLI mode

> node
> Enter the commands or script to run in the CLI

### Exiting the Node in CLI mode

> .exit

### Synchronous Reading and Writing Files

> const fs = require("fs"); <br>
> const textIn = fs.readFileSync("./txt/input.txt", "utf-8");

> const textOut = `This is an example of writing file to existing file: ${testIn}. \n Created on ${Date.now()}`; <br>
> fs.writeFileSync("./txt/Output.txt", textOut);

### Synchronous vs Asynchronous (Blocking vs Non-Blocking Code)

> Sync functions can block the task until the result is obtained from the running process. This is called as blocking code. <br> This problem can be avoided by using the non-blocking code using the async functions that run in the background and carry on with the rest of the process.

### Node JS Thread

> For each application only one thread is available. This means when ever the code runs it can be executed on a single thread only, irrespective of the number of users or applicatioons accessing the thread. Only one thread is available to all. So, when a single user blocks the thread with a sync function, the other application or users can not use the thread for execution. Thus the callbacks based async functions are used. The function can process in the background and the result is returned via a callback function and this allows the other users to use the avtive thread for various other operatinos. <br>Not all callbacks are async.

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

> Web works with the request-response model or the client-server architecture. <br> https://www.google.com/maps/ - https/http refers to protocol, www.google.com refers to the domain name, and /maps refers to the rsource requested.
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

# Express JS

# Mongo DB
