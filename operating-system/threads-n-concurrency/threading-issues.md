Issues to consider in designing multithreaded programs.

# `fork()` and `exec()`

Some UNIX systems have chosen to have two versions of `fork()`.

1. duplicates all threads
2. duplicates only the thread that invoked the `fork()` system call.

If a thread invokes the `exec()` system call, the program specified in the parameter to `exec()` will replace the entire process, including all threads.

Based on which you call the `exec()`, you need to call different versions of the `fork()`.

# Signal Handling

- `Signal`: notify a process that a particular event has occurred.

Signal may be received either synchronously or asynchronously.

Every signal hs a `Default Signal Handler` that kernel runs.

This default action can be overridden by a `User-Defined Signal Handler`.

Some asynchronous signals, such as a signal that terminates a process (\<control\>\<C\>, for example), should be sent to all threads.

## Signal Handling on UNIX

> The standard UNIX function for delivering a signal is `kill(pid_t pid, int signal)`.

Most of UNIX allow a thread to specify which signals it will accept and which it will block.

However, because signals need to be handled only once, a signal is typically delivered only to the first thread found that is not blocking it.

> POSIX Pthreads provides the `pthread_kill(pthread_t tid, int signal)` function which allows a signal to be delivered to a specified thread.

## Signal Handling on Windows

Windows does not explicitly provide support for signals.

Windows allows us to emulate them using `Asynchronous Procedure Calls` (`APCs`).

An APC is delivered to a particular thread rather than a process.

# Thread Cancellation

`Thread Cancellation` involves terminating a thread before it has completed.

- `Target Thread`: a thread that is to be cancelled.

## Cancellation of a Target Thread

- `Asynchronous Cancellation`: one thread immediately terminates the target-thread.
- `Deferred Cancellation`: the target thread periodically checks, allowing it an oppertunity to terminate itself.

With asynchronous cancellation, it is hard to cancel a thread while in the midst of updating data which is being shared with other threads. It may not free necessary system-wide resource.

With differed cancellation, cancellation occurs only after the target thread has checked a flag to determine whether or not it should be cancelled.

> Pthreads uses `pthread_cancel()` to cancell a thread.

## Cancellation Point

Cancellation occurs only when a thread reaches a `Cancellation Point`.

> Most of the **blocking system calls** in the POSIX and standard C library are defined as cancellation points, such as the `read()` system call.

> Cancellation point can be established with `pthread_testcancel()`.

> Additionally, Pthread allows a funciton known as a `cleanup handler`, allows any resources a thread may have aquired to be released before the thread is terminated.

> Asynchronous cancellation is not recommended in Pthreads documentation.

> In Java thread, invoke `interrupt()` to cancel it.

# Thread-Local Storage (TLS)

TLS is data which is the own copy of each thread.

> TLS is similar to static data. In fact, TLs is usually declared as static.

> `gcc` compiler provides the storage class keyword `__thread` for declaring TLS data.

# Scheduler Activations

- `Lightweight Process` (`LWP`): an intermediate data structure which is in between the user and kernel threads, in many-to-many or two-level model.

To the user-thread library, the LWP appears to be a virtual processor.

Each LWP is attached to a kernel thread.

> Typically, an LWP is required for each concurrent blocking system call.

- `Scheduler Activation`: a scheme for communication between the user-thread library and the kernel.

The kernel provides an application with a set of LWPs, and the application can schedule user threads onto them.

- `Upcall`: a kernel informing about certain events to an application.
- `Upcall Handler`: a thread library which handles upcalls.

Upcall handlers must run on a virtual processor.

> For example, when an application thread is about to block, upcall occurs, informing that a thread is about to block and identifying the specific thread.
