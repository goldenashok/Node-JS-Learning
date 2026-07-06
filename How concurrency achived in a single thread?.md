A single thread achieves concurrency by switching between tasks instead of waiting for one task to finish completely.
# How it works in Node.js
Node.js uses:

1. One main JavaScript thread
2. Event Loop
3. Non-blocking I/O
4. Callback Queue / Microtask Queue

### Example

```
console.log("Start");

setTimeout(() => {
  console.log("Timer Done");
}, 1000);

console.log("End");

```

### Output
```
Start
End
Timer Done
```

### What happens?
1. console.log("Start") executes.
2. setTimeout() registers a timer and returns immediately.
3. console.log("End") executes.
4. The thread is free to do other work.
5. After 1 second, the callback is placed in the event queue.
6. Event Loop executes the callback when the call stack is empty.

The thread never waited for 1 second.

### Real-world Example
Imagine a restaurant with one waiter.

Blocking approach
```
1. Customer 1 orders coffee.
2. Waiter stands at coffee machine for 5 minutes.
3. Customer 2 waits.
4. Customer 3 waits.
```

### Concurrent approach
```
1. Customer 1 orders coffee.
2. Waiter starts coffee machine.
3. Waiter takes orders from Customer 2 and 3.
4 When coffee is ready, waiter serves it.
```
