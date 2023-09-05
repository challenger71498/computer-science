# Independent Process, Cooperating Process

- `Independent Process`: does not share any data with other processes.
- `Cooperating Process`: can affect or be affected by the other processes.

> Clearly, any process that shares data with other processes is a cooperating process.

Why provide an environment that allows process cooperation:
1. Information Sharing: concurrent access to information.
2. Computation Speedup: break into subtasks, run in parallel.
3. Modularity: divide system functions into seperate processes or threads.

# Interprocess Communication (IPC)

Cooperating process requires an interprocess communication.

- Allow process to exchange data.
- Send and recieve data to each other.

# IPC in Shared-Memory Systems

A `shared-memory` system is faster than `message-passing`.

Normally, the operating system tries to prevent access overlapping between two or more processes; shared memory requires to remove this restriction.

These are belong to processes, not the operating system:
- the **form** of the data
- the **location**
- responsibility of ensuring that there is **no writing on the same location simultaniously**

## Producer-Consumer Problem

> TBD, from my opinion this should be written to a seperated page.

# IPC in Message-Passing Systems

A message-passing system is useful for exchanging small amount of data.

Also, it is easier to implement in a distributed system.

## Naming

### Direct Communication

Processes that wants to communicate must **explicity** name the recipient or sender.

An addressing could be symmetry or asymmetry:
- `Symmetry`: sender and received process must name the other to communicate.
- `Asymmetry`: only the sender names the recipient.

> In direct communication, if the pid of the process has heen changed, all other dependent process definitions are must also be changed, which is undesirable.

### Indirect Communication

The messages are sent to nad received from `mailboxes` or `ports`.

> A mailbox may be owned either by a **process** or by the **operating system**.

## Synchronization

- `Blocking` (`Synchronous`): A process must wait until the execution is finished.
- `Nonblocking` (`Asynchronous`): A process may continue even if the execution is not finished.

> NOTE: On the internet, they classify blocking-nonblocking and sync-async as different. But the context in the book seems like both are the same. I'll look further on this later..

- `Blocking Send`: sending process is **blocked** until the message is received.
- `Nonblocking Send`: sends the message and resumes operation.
- `Blocking Receive`: receiver blocks until a message is available.
- `Nonblocking Receive`: receiver retrieves a vaild message or null.

## Buffering

- `Zero Capacity`: the sender must block until the recipient recieves the message.
- `Bounded Capacity`: the sender may send until the queue is full; recipient gets the message from the queue.
- `Unbounded Capacity`: the sender may send as many as it can; it never blocks.

Zero capacity is referred as `No Buffering`, the others are referred as `Automatic Buffering`.