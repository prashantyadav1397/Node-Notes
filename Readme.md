# Node JS Runtime

Node JS is a JavaScript runtime built on google's v8 javascript engine which allows user to run JavaScript outside the browser without having the restrictinos seen in browser

> Node JS = ( v8 ( JavaScript ) )

Adv of Node JS -

> 1.  Accessing the file system
> 2.  Better Network Capabilities
> 3.  Single threaded event driven non-blocking I/O model
> 4.  Perfect for building fast and sclable data intensive apps
> 5.  JavaScript across the entire stack, faster and more efficient development
> 6.  NPM - huge library of open source packages
> 7.  Huge dev community

Use of Node JS -

> 1.  Building API with database
> 2.  Data Streaming supported Apps
> 3.  Real time chat application
> 4.  Server-side web application

Don't use Node JS for -

> 1.  Apps with heavy server side processing ( CPU intensive)

Running Node in CLI mode

> node
> Enter the commands or script to run in the CLI

Exiting the Node in CLI mode

> .exit

Reading and Writing files

> const fs = require("fs"); <br>
> const textIn = fs.readFileSync("./txt/input.txt", "utf-8");

> const textOut = `This is an example of writing file to existing file: ${testIn}. \n Created on ${Date.now()}`; <br>
> fs.writeFileSync("./txt/Output.txt", textOut);

Synchronous vs Asynchronous ( Blocking vs Non-Blocking)

> Sync functions can block the task until the result is obtained from the running process. This is called as blocking code. <br> This problem can be avoided by using the non-blocking code using the async functions that run in the background and carry on with the rest of the process.

Node JS Thread

> For each application only one thread is available. This means when ever the code runs it can be executed on a single thread only, irrespective of the number of users or applicatioons accessing the thread. Only one thread is available to all. So, when a single user blocks the thread with a sync function, the other application or users can not use the thread for execution. Thus the callbacks based async functions are used.
