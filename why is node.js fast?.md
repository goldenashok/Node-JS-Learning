Because Node.js doesn't create a new thread for every request. Javascript runs mainly on a single thread. while livuv handles many synchronous I/O Operations and the Event Loop coordinates their callbacks.

For Example
```
Sync Code
   ↓
nextTick
   ↓
Promise Microtasks
   ↓
Event Loop
   ↓
Timers / Poll / Check / Close
```
