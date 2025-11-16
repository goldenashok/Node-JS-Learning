# what is the difference between Node.js & a browser javascript environment?
     
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
