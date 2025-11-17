
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
