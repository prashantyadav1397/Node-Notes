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

> const fs = require("fs");
> const textIn = fs.readdirSync("./txt/input.txt", "utf-8");

>const textOut = `This is an example of writing file to existing file: ${testIn}. \n Created on ${Date.now()}`;
fs.writeFileSync("./txt/Output.txt", textOut);