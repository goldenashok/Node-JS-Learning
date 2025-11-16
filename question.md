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
   - 3.3 what is the v8 engine?
   - what is the difference between Node.js & a browser javascript environment?
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
13. 
   
