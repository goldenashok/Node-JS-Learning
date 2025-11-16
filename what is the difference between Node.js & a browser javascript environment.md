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

   
