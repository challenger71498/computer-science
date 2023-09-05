> In my opinion, `pipe` is the most important thing in this chapter. The rest of those are optional; you may read if you have an interest in.

# Pipes

> Pipes are one of the first IPC mechanisms in early UNIX systems.

Here's some considerations:
- Bidirectional, or unidirectional?
- Half duplex, or full duplex?
  - `Half Duplex`: data can travel only one way at a time.
  - `Full Duplex`: data can travel in both directions at the same time.
- Must a relationship exist?
- Over a network, or reside on the same machine?

## Ordinary Pipes

Allows two processes communicate in standard producer-consumer pattern.

- `Write End`: one end of the pipe which producer writes to.
- `Read End`: the other end which consumer reads from.

Ordinary pipes are **unidirectional**, allowing only one-way communication.

Ordinary pipes require a **parent-child relationship** between the communicating processes on both UNIX and Windows, which means that these pipes can be used only for the **same machine**.

Ordinary pipes exist only while the processes are communicating wiht one another. When the process terminates, the pipe is also removed.

### Ordinary Pipes in UNIX

UNIX offers the function `pipe()` to use an ordinary pipe.

Since a pipe is a special type of file, the child inherits it.

> Typically, a parent process creates a pipe and uses it to communicate with a child process that is creates via `fork()`.

The parent and the child should initially close their unused ends of the pipe.

### Ordinary Pipes in Windows

- `Anonymous Pipes`: Window version of ordinary pipes.

## Named Pipes

- Can be directional.
- No parent-child relationship is required.
  - In fact, in a typical scenario, a named pipe has several writers.

### Named Pipes in UNIX (FIFO)

Only half-duplex trasmission is permitted.

Processes must reside on the same machine. If not, `sockets` must be used.

- `mkfifo()`: Creates FIFO.

### Named Pipes in Windows

Full-duplex communication is allowed.

Processes may reside either on the same or different machines.

- `CreateNamedPipe()`
- `ConnectNamedPipe()`

# POSIX Shared Memory

- `shm_open()`: creates a shared-memory object.
- `ftruncate()`: configures the size of the object in bytes.
- `mmap()`: establishes a memory-mapped containg the shared-memory object.
- `shm_unlink()`: removes a shared-memory object.

# Mach Message Passing

> Mach is included in the macOS and iOS operating systems.

- `Tasks`: similar to process but have multiple threads of control and fewer associated resources.
- `Messages`: carries out the most of communication on March, including intertask commuincation.

## Port

In short, a `port` is Mach version of the mailbox.

- Port is unidirectional; for two-way communication, a response is sent to a seperate `reply port`.
- Each port may have multiple senders, but only **one** receiver.

### Port Rights

`Port Rights` identifies the capabilities nessary for a task to interact with the port.

Ownership of port rights is at the task level; all threads belonging to the same task share the same port rights.

### Special Ports

- `Task Self Port`: the kernel has receive rights to this; allows a task to send messages to the kernel.
- `Notify Port`: the kernel send notifications to here.
- `Bootstrap Port`: allows a task to register a port it has created with a system-wide `bootstrap server`.
  -  Once a port has been registered, other tasks can look up the port in this registry and obtain rights for sending.

## Messages

Mach messages contain the following two fields:
- Fixed-size message header: containing metadata of the message, such as size, source, destination, etc.
- Variable-sized body

- `Simple`: contains ordinary, unstructured user data.
- `Complex`: may contain pointers to memory locations, can be used for transferring port rights.

Functions of Mach messaage API are:
- `mach_msg()`: sending and receiving messages.
- `mach_msg_trap()`: system call to Mach kernel.
- `mach_msg_overwrite_trap()`: handles the actual passing of the message.

> The major problem wiht message systems has generally been poor performance caused by copying of messages from the sender's port to the receiver's port.
>
> The Mach message system attepts to avoid this by using virtual-memory-management techniques.
>
> Mach **maps** the address space containing the sender's message into the receiver's address space, make the message never actually copied.
>
> This technique provides a large performance boost but works only for intrasystem messages.

# Windows

- `Subsystems`: multiple operating environments; application programs communicate with these subsystems via a message-passing mechanism.
> Note: Need more description about what the "Window Subsystem" is.
- `Advanced Local Procedure Call` (`ALPC`): communication between two processes on the same machine, similar to the standard `Remote Procedure Call`, or `RPC`.
  - `ALPC` is not the part of the Windows API; hence it is not visible to the application programmer.
  - The RPC is handled indirectly through an ALPC procedure call.

## Ports

- `Connection Port`: a connection request from the client is sent to here.
- `Communication Port`: consists a channel with two communication ports: one for client to server, the other for server to client.

## Message-Passing Techniques

1. Small messages (~256B): port's message queue is used.
2. Larger messages: is passed through `section object`, region of shared memory.
3. Too large: API which reads and writes directly into the address space.