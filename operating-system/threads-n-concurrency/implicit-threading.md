# What is an Implicit Threading?

- `Implicit Threading`: transfering the creation and management of threading from application developers to compilers and run-time libraries.

> These stratagies generally require application developers to identify tasks, not threads.

# Thread Pools

A thread pool creates a number of threads at start-up, waiting for the work.

Rather than creating a thread, the thread pool provides a thread for the request.

## Benefits of Using Thread Pools

1. Servicing a request with an existing thread is often faster.
2. Limits the number of threads.
3. Seperating the task to be performed from the mechanics of creating the task.

# Fork Join

The main thread creates(*forks*) child threads and then waits for the children to terminate(*join*).

For such jobs, rather than using threads for each fork, parallel tasks are designated.

An important issue to consider is determining when the problem is *small enough* to be solved directly and no longer requires creating additional tasks.

> On java, it can steal a task from another thread's queue using a `work stealing` algorithm, thus balancing the workload.

# OpenMP

OpenMP provides support for parallel programming in shared-memory environments.

- `Parallel Regions`: blocks of code that may run in parallel.

# Grand Central Dispatch (GCD)

GCD is a technology developed by Apple for its macOS and iOS operating systems.

> Internally, GCD's thread pool is composed of POSIX threads.

## Dispatch Queue

- `Dispatch Queue`: a queue where tasks for run-time execution are placed on.

GCD identifies two types of dispatch queues.

- `Serial Queue`
  - Removed in FIFO order.
  - `Main Queue`: A serial queue which belongs to each process.
  - Also known as `Private Dispatch Queue`.
- `Concurrent Queue`
  - Also removed in FIFO order.
  - Several tasks may be removed at a time.

## Global Dispatch Queues

System-wide concurrent queues.

- `QOS_CLASS_USER_INTERACTIVE`: User-interactive class represents tasks that interact with the user.
- `QOS_CLASS_USER_INITIATED`: User-initiated class, may require longer processing times.
- `QOS_CLASS_UTILITY`: Require a longer time to complete but do not demand immediate results.
- `QOS_CLASS_BACKGROUND`: Not visible to user and not time sensitive.

# Intel Thread Building Blocks (TBB)

A template library that supports designing parallel applications in C++.

TBB provides a `parallel_for` template that expects 2 values:

```
parallel_for (range, body);
```

- `range`: the range of elements that will be iterated (known as the `iteration space`).
- `body`: an operation that will be performed.

The TBB library will divide the loop iterations into seperate `chunks` and create a number of tasks that operate on those chunks.
