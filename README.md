## Execution Flow and the Event Loop

### Synchronous Code:
- "Top Level code Finished" is printed immediately because it is part of the synchronous execution.

### Timers and Immediate Execution:
- "Timer 1 Finished" and "Immediate 1 Finished" are scheduled for execution. `setImmediate` callbacks are executed after I/O events, but before `setTimeout` with 0ms delay.

### File Read Operation:
- The `fs.readFile` starts an asynchronous read operation.

### After File Read Completes:
- "I/O Finished" is printed.
- Additional `setTimeout` and `setImmediate` callbacks are scheduled.
- Cryptographic operations (`crypto.pbkdf2`) are executed, and when each completes, the time elapsed is logged.

### Expected Output Order:
The output order might vary slightly due to the asynchronous nature of Node.js, but generally, it should be:

1. "Top Level code Finished"
2. "Immediate 1 Finished"
3. "Timer 1 Finished"
4. "I/O Finished"
5. "--------------"
6. "Immediate 2 Finished"
7. "Timer 2 Finished"
8. (Cryptographic operations finish, times vary)
9. "Timer 3 Finished" (after a 4-second delay)

This code showcases how Node.js handles different phases of the event loop, including timers, I/O tasks, and immediate executions. It helps to understand the non-blocking nature of Node.js and the order in which callbacks are executed.
