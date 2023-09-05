> Process creation is time consuming and resource intensive.

# Benefits of Multiprogramming

1. `Resposiveness`
2. `Resource Sharing`
3. `Economy`
4. `Scalability`

# Multithreading Models

- `User Threads`: supported above the kernel and are managed without kernel support.
- `Kernel Threads`: kernel threads are supported and managed directly by the operating system.

## Many-to-One Model

- Maps many user-level threads to one kernel thread.
- The **entire** process will block if a thread makes a blocking system call.
- Only one thread can access the kernel at a time, multiple threads are unable to run in parallel on multicore systems.

`Green Threads`: a thread library available for Solaris systems and adopted in early versions of Java. This library used the many-to-one model.

> Very few systems continue to use the model because of its inability to take advantage of multiple processing cores.

## One-to-One Model

- Maps each user thread to a kernel thread.
- Creating a user thread requires creating the corresponding kernel thread.

> Linux, along with the family of Windows operating systems implement the one-to-one model.

## Many-to-Many Model

- multiplexes many user-level threads to a smaller or equal number of kernel threads.
- Developers can create as many user threads as necessary, and the corresponding kernel threads can run in parallel on a multiprocessor.
- It is difficult to implement.
- Limiting the number of kernel threads has become less important.

> Most operating systems now use the one-to-one model.

### Two-Level Model

- Similar to many-to-many model, but allows a user-level thread to be bound to a kernel thread.