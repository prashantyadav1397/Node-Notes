# Node JS Runtime

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

### Synchronous vs Asynchronous ( Blocking vs Non-Blocking)

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
> }
