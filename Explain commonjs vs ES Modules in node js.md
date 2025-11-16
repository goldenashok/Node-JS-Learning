# Explain commonjs vs ES Modules in node js?

Both CommonJS (CJS) and ES Modules (ESM) are systems for organizing and reusing code in Node.js — but they work differently.

- Definition
  
| Type                 | Description                                                                 |
| -------------------- | --------------------------------------------------------------------------- |
| **CommonJS (CJS)**   | The original Node.js module system — uses `require()` and `module.exports`. |
| **ES Modules (ESM)** | The modern JavaScript standard for modules — uses `import` and `export`.    |

- Syntax Difference
#CommonJS
```
// math.js
const add = (a, b) => a + b;
module.exports = { add };

// main.js
const { add } = require('./math');
console.log(add(2, 3)); // 5

```
#ES Modules 
```
// math.mjs
export const add = (a, b) => a + b;

// main.mjs
import { add } from './math.mjs';
console.log(add(2, 3)); // 5
```

#File Extensions and Configuration
| Feature                       | CommonJS                      | ES Modules                                                |
| ----------------------------- | ----------------------------- | --------------------------------------------------------- |
| **Default in Node.js**        | Yes (default before v13)      | Yes (default in modern versions if configured)            |
| **File Extension**            | `.js`                         | `.mjs` or `.js` with `"type": "module"` in `package.json` |
| **Import/Export**             | `require()`, `module.exports` | `import`, `export`                                        |
| **Synchronous/Async Loading** | Synchronous                   | Asynchronous                                              |

Example configuration for ESM in Node:

```
{
  "type": "module"
}
```
- Execution Behavior

| Concept             | CommonJS                                      | ES Modules                              |
| ------------------- | --------------------------------------------- | --------------------------------------- |
| **Loading**         | Synchronous                                   | Asynchronous (uses Promises internally) |
| **Scope**           | Each file has its own scope                   | Same                                    |
| **Hoisting**        | No hoisting                                   | `import` statements are hoisted         |
| **Mutable Exports** | Exports are mutable (can change after export) | Exports are immutable bindings          |

- Interoperability
You can use both systems together, but with care:
Using CommonJS in ESM:
```
const esm = await import('./module.mjs');

```

Note: Dynamic import() returns a Promise — it’s asynchronous.

- When to Use Which
| Use Case                                 | Recommendation                       |
| ---------------------------------------- | ------------------------------------ |
| Existing Node.js projects                | CommonJS                             |
| Modern apps, bundlers (React, Vue, etc.) | ES Modules                           |
| Library with browser + Node support      | ES Modules (with `"type": "module"`) |

- Performance & Ecosystem
  - CommonJS is slightly faster for local imports (synchronous).
  - ESM enables tree-shaking and static analysis, making it preferred for modern frontend + backend codebases.
