1. Event Loop & Concurrency
   - 1.1 How Node.JS handles concurrency with a single thread
   - 1.2 Event loop phases ( Timer -> pending -> idle -> Pole -> check -> close)
   - 1.3 Callbacks, microtasks, nextTick(), Promises
   - 1.4 When code runs libuv thread pool(fs, crypto, dns, zlib)
   - 1.5 Explain Node event loop
   - 1.6 [How concurrency achived in a single thread?](https://github.com/goldenashok/Node-JS-Learning/blob/main/How%20concurrency%20achived%20in%20a%20single%20thread%3F.md)
   - 1.7 Difference between process.nextTick() and setImmediate()?
   - 1.8 Parallel, sequential, and race operations using promise methods
   - 1.10 [How do you handle asynchronous errors ?](https://github.com/goldenashok/Node-JS-Learning/blob/main/How%20do%20you%20handle%20asynchronous%20errors%3F.md)
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
   - 3.4 [what is the difference between Node.js & a browser javascript environment?](https://github.com/goldenashok/Node-JS-Learning/blob/main/what%20is%20the%20difference%20between%20Node.js%20&%20a%20browser%20javascript%20environment.md)
   - What is the role of the event loop in Node.js?
         The Event Loop is the heart of Node.js — it allows Node to perform non-blocking I/O operations, even though JavaScript runs on a single thread.
         It continuously checks whether the call stack is empty and executes callbacks from various queues (timers, I/O, microtasks, etc.) in a controlled, cyclic manner.
        - 1. How It Works — Step by Step
          - When Node.js starts:
            - It initializes the event loop, callback queues, and thread pool (libuv).
            - Then executes your top-level code (like file imports, function calls, etc.).
          - If a blocking task (e.g., file read, DB call) appears:
            - Node delegates it to the libuv thread pool or system kernel.
            - Meanwhile, the main thread continues executing other code.
          - When the async task finishes:
            - The callback is pushed into a queue.
            - The event loop picks it up when the call stack is empty.
          - The loop repeats indefinitely, allowing Node.js to handle many concurrent tasks efficiently.
       - Event Loop Phases
         The Node.js event loop runs through phases in each iteration (called a “tick”):
         | Phase                    | Description                                                 |
         | ------------------------ | ----------------------------------------------------------- |
         | **1. Timers**            | Executes callbacks from `setTimeout()` and `setInterval()`. |
         | **2. Pending Callbacks** | Executes I/O callbacks deferred from the previous cycle.    |
         | **3. Idle/Prepare**      | Internal use only.                                          |
         | **4. Poll**              | Retrieves new I/O events; executes I/O callbacks.           |
         | **5. Check**             | Executes callbacks from `setImmediate()`.                   |
         | **6. Close Callbacks**   | Handles close events like `socket.on('close')`.             |

         After each phase, Node checks the microtask queue (Promises, process.nextTick()).
      -  Example — How Event Loop Works
            ```
            console.log('Start');
            setTimeout(() => console.log('Timeout'), 0);
            Promise.resolve().then(() => console.log('Promise'));
            process.nextTick(() => console.log('Next Tick'));         
            console.log('End');
            ```
         Output
            ```
            Start
            End
            Next Tick
            Promise
            Timeout
            
            ```

   - Explain the difference between `process.nextTick()`, `setImmediate()` and `setTimeout()`
   - what are global objects in Node.js?
4. Module & Packages
   - [Explain CommonJs vs ES Modules in Node.js](https://github.com/goldenashok/Node-JS-Learning/blob/main/Explain%20commonjs%20vs%20ES%20Modules%20in%20node%20js.md)
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
21.  Core Node.js Concepts
   ✅ Event Loop & Async
   - How does the Node.js event loop work? Explain phases.
   - Difference between process.nextTick(), setImmediate(), and setTimeout().
   - What are microtasks vs macrotasks?
   - How does Node.js handle concurrency with a single thread?
   ✅ Non-blocking I/O
   - What is non-blocking I/O? Why is it important?
   - Explain synchronous vs asynchronous APIs in Node.js.
   - What happens if you use blocking code in Node?
22. Architecture & Internals
   - Explain libuv and its role in Node.js.
   - How does Node.js handle multi-threading internally?
   - What is the thread pool? When does Node use it?
   - Explain cluster module and when to use it.
   - Difference between cluster vs worker_threads.
23. API Development (Express / Fastify)
   - How does middleware work in Express?
   - [Difference between app.use() and app.get()](https://github.com/goldenashok/Node-JS-Learning/blob/main/Difference%20between%20app.use()%20and%20app.get()%20%3F.md)
   - What are error-handling middleware?
   - How to structure a large-scale Node.js application?
   - How do you implement rate limiting?
24. Asynchronous Programming
   - Callback vs Promise vs Async/Await.
   - How do you handle errors in async/await?
   - What is Promise.all() vs Promise.allSettled()?
   - How to avoid callback hell?
   - What happens if a Promise is not handled?
25. Performance Optimization
   - How do you optimize Node.js performance?
   - What is event loop blocking? How to detect it?
   - Tools used for performance monitoring (e.g., PM2, New Relic).
   - How do you handle CPU-heavy tasks?
   - What is streaming? When should you use it?
26. Memory Management
   - How does garbage collection work in Node.js?
   - What is a memory leak? How to detect it?
   - Tools to debug memory issues (e.g., heapdump, Chrome DevTools).
   - Difference between stack and heap memory.
27. Security
   - Common Node.js security threats (XSS, CSRF, Injection).
   - How do you secure APIs?
   - What is JWT? How do you implement authentication?
   - How to handle sensitive data and secrets?
   - Explain Helmet, CORS.
28. Database & Scaling
   - How do you manage database connections in Node.js?
   - SQL vs NoSQL usage in Node apps.
   - What is connection pooling?
   - How do you handle transactions?
   - How to design scalable APIs?
29. Streams & Buffers
   - What are streams in Node.js?
   - Types: Readable, Writable, Duplex, Transform.
   - Difference between Buffer and Stream.
   - When to use streams over reading full file?
30. Advanced Topics
   - What are worker threads?
   - Explain event emitters.
   - How Node handles child processes?
   - Difference between fork, spawn, and exec.
   - How to implement caching (Redis)?
31. Debugging & Testing
   - How do you debug a Node.js app?
   - Tools: node --inspect, Chrome DevTools.
   - Unit testing frameworks (Jest, Mocha).
   - How to mock APIs?
   - What is integration vs unit testing?
32. Real-world Scenario Questions
   - How would you design a high-traffic API (e.g., like Uber)?
   - How would you reduce API response time?
   - How do you handle 1M concurrent requests?
   - What would you do if your Node server crashes?
       i. use process manager
       ii. Auto restart on crash
       iii. 
   - How to implement logging and monitoring?
33. Coding / Practical Questions
Example tasks:
JavaScript// 1. Debounce function implementation// 2. Implement rate limiter// 3. File upload with streaming (Express)// 4. Create a custom middleware// 5. Implement retry logic for API callsShow more lines

34. Frequently Asked Tricky Questions
   - Why is Node.js single-threaded but still scalable?
   - Can Node.js handle CPU-intensive tasks?
   - Difference between require and import.
   - What happens when you block the event loop?
   - Why async/await is just syntactic sugar?
