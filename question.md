1. Event Loop & Concurrency
   - 1.1 How Node.JS handles concurrency with a single thread
   - 1.2 Event loop phases ( Timer -> pending -> idle -> Pole -> check -> close)
   - 1.3 Callbacks, microtasks, nextTick(), Promises
   - 1.4 When code runs libuv thread pool(fs, crypto, dns, zlib)
   - 1.5 Explain Node event loop
   - 1.6 How concurrency achived in a single thread ?
   - 1.7 Difference between process.nextTick() and setImmediate()?
   - 1.8 Callbacks vs Promises vs async/await
   - 1.9 Parallel, sequential, and race operations using promise methods
   - 1.10 How do you handle asynchronous errors ?
   - 1.11 promise.all vs Promise.allSettled vs Promise.race
2. Node.Js Architecture
   - 2.1 Common JS vs ES Modules
   - 2.2 requires vs import
   - 2.3 module.exports vs export default
   - 2.4 How Node resolves modules
   - 2.5 package.json "type": "module"
3. Core Node.js Concepts
   - 3.1 What is node js ?
   - 3.2 How does Node.js handle concurrency if it's single-threaded?
     Hint: Event Loop & asynchronous callback
     Node.js uses a single-threaded event loop architecture - but the doesn't mean it can handle only one request at a time.
     instead, Node achieves concurrency through non-blocking I/O and event-driven model

        - Single Threade for Javascript Execution
             - Node runs all your Javascript code in single main thread (one call stack).
             - This thread executes code, register callbacks, and delegates tasks to the system
        - Event Loop
             - The Event Loop continueously checks for tasks to execute.
             - When Node.js receives multiple request, it doesn't block the thread.
             - Instead I/O operations (like file read, DB query, network request) are offloaded to the system's thread pool(via libu)
        - libu &Thread Pool
             - Node.js internally uses libuv, a C library that provides a thread pool(default 4 threads).
             - Time-consuming tasks (e.g file I/O, DNS lookups, encryption) are handled by theses background threads.
             - when thy finish, they notify the event loop to execute the callback.
        - Event loop handles multiple requests
             - While those backgroud operations are running, the main thread continues to handle other requests.
             - When results are ready, their callbacks are pushed into the callback queue, and the event loop executes then one by one.          
   - 3.3 what is the v8 engine?
   - what is the difference between Node.js & a browser javascript environment?
     Both Node.js and browsers use JavaScript, but they run in different environments and serve different purposes.
     - Execution Environment
      | Aspect          | **Node.js**                                     | **Browser**                               |
      | --------------- | ----------------------------------------------- | ----------------------------------------- |
      | **Engine**      | V8 (same as Chrome)                             | V8 (Chrome), SpiderMonkey (Firefox), etc. |
      | **Purpose**     | Run JavaScript on the **server side**           | Run JavaScript on the **client side**     |
      | **Environment** | Outside the browser (server, terminal, backend) | Inside the browser (frontend, UI)         |

      - Global Objects
         | Concept       | **Node.js**            | **Browser**        |
         | ------------- | ---------------------- | ------------------ |
         | Global Object | `global`               | `window` or `self` |
         | Example       | `global.console.log()` | `window.alert()`   |

        - APIs Available
            | Feature            | **Node.js**                             | **Browser**                            |
            | ------------------ | --------------------------------------- | -------------------------------------- |
            | File System Access | ✅ via `fs` module                       | ❌ (for security reasons)               |
            | HTTP Requests      | ✅ via `http`/`https` modules            | ✅ via `fetch()` / `XMLHttpRequest`     |
            | DOM Manipulation   | ❌                                       | ✅                                      |
            | OS Access          | ✅ via `os`, `path`, `child_process`     | ❌                                      |
            | Local Storage      | ❌ (but can use DBs like Redis, MongoDB) | ✅ via `localStorage`, `sessionStorage` |

         - Module System
            | Feature     | **Node.js**                                   | **Browser**                       |
            | ----------- | --------------------------------------------- | --------------------------------- |
            | Module Type | CommonJS (`require`) or ES Modules (`import`) | ES Modules only (`import/export`) |
            | Example     | `const fs = require('fs');`                   | `import data from './file.js';`   |
         - Security Context
              - Browser: Runs in a sandboxed environment — cannot access local files or system-level resources directly (for user safety).
              - Node.js: Has full system access — can read/write files, access the network, and manage processes. 

   - Explain the difference between `process.nextTick()`, `setImmediate()` and `setTimeout()`
   - what are global objects in Node.js?
4. Module & Packages
   - Explain CommonJs vs ES Modules in Node.js
   - How do you export and import modules?
   - what is the difference between `require()` and `import()`
   - How does npm or yarn manage dependencies?
   - What are peer dependencies?
6. Asynchrouns Programming
   - What are callbacks, promises, and async/await?
   - what are `callback hell` and ways to avoid it?
   - what is `promise.all()`, `Promise.race()` and `Promise.any()` ?
   - How does the Node.js event loop work with async functions?
   - what is the difference between microtasks and macrotasks?
8. File System and Streams
   - what is a stream in Node.js?
   - Explain the difference between readable, writabl, duplex, and transform stream.
   - How do you read/write files asynchronously using fs?
   - How does piping work in streams?
   - what's the difference between buffering and streaming?
9. HTTP & APIs
    - How do you create an HTTP server in Node.js?
    - How do you handle JSON requests ad reponse?
    - What are middleswares in express.js?
    - Diffrence between `res.send()`, `res.json()` and `res.end()` in Express?
    - What's th role of `body-parser` or why isn't it needed in recent Express versions?
    - What are CORS and how do you hadle them in Node ?
    - How do you handle file uploads in Node.js?
10. Security
    - How do you protect against SQL Injection and XSS in Node.js?
    - How do you store passwords securely?
      Hint: bcrypt, hashing, salting
    - what are common security middleware packages?
    - How do you handle environment variables securely?
13. Performance & Scaling
    - How does Node handle multiple requests efficiently?
    - What is the cluster module and why is it used?
    - How do you use wrke threads in Node.js?
    - what is load balancing and how can you implement it in Node?
    - How do you identify memory leaks in Node.js?
15. Event Emitter
    - What is an `EventEmitter` in NOde.js?
    - How do you create custom events?
    - what is difference between `on`, `once` and `removeListener`?
17. Tools & Debugging
    - How do you debug a Node.js applicaiton?
    - What's the difference between `console.log`, `console.error` and `console.dir` ?
    - How do you use the `--inspect` flag or Chrome DevTools with Node?
18. Read-World / Practical Questions
    - How would you desing a REST API using Node.js + Express?
    - How do you connect Node.js to MongoDB or MySQL?
    - How do you implement JWT-based authentication?
    - How woluld you handle backgroud jobs( e.g with Bull or Agenda) ?
    - How do you schedule tasks in Node.js?
    - How would you optimize a slow API endpoint?
20. Trick or Deep-Dive Questions
    - Why is Node.js not suitable for CPU-intensive tasks?
    - what happens when you call `require()` for the same file multiple times?
    - How do you handle uncaught exceptions in Node.js?
    - What's the difference between `spawn`, `fork` and `exec` from the `child_process` module?
    - What's the difference between synchronous and asynchrouns I/O in Node?
   
