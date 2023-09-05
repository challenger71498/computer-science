# Process Scheduler
`Process Scheduler` selects an available process for execution on a core.

# Degree of Multiprogramming
The number of processes currently in memory.

> When a system is containing a number of processes, we could say: *'the degree of multiprogramming is **high**'*.

# Scheduling Queues
- `Ready Queue` - the first place to go when processes enter the system
- `Wait Queue` - Processes that are waiting for a certain event to occur, such as I/O completion, or event reception.

## Dispatched
- A process being selected for the **execution**, which is on the `Ready Queue`.

When a process has been `Dispatched`, transitions to the `Ready` state may occur as below:
- Issue **I/O request** and then be placed in an I/O wait queue
- Create a **new child process** and then be placed in a wait queue, awaits the child's termination
- Be Removed forcibly from the core
  - By **interrupt**
  - By time slice **expiration**

# CPU Scheduling

## CPU Scheduler
- Select from among the processes that are in the `Ready Queue` and allocate a CPU core to one of them

> The CPU scheduler executes at least once every 100 milliseconds, typically more frequently.

### Swapping
- A removal of a process from the memory to the storage, such as a hard drive or a solid state drive
- Reduces the degree of multiprogramming

> This is only nessesary when memory is overcommitted and must be freed up.

# Context Switch
`Interrupts` cause the operation system to change a CPU core from its current tasks and to run a *kernel routine*.

When it occurs, system needs to save the current `Context` of the process.

- `State Save` - a `Context` is being saved from running process
- `State Restore` - a `Context` is being restored

Switching the CPU core to another process is **pure overhead**, and there is **no useful work** while switching.

> A typical speed of context switching is about a several microseconds.

> Context-switch times are highly dependent on hardware support.

> Meanwhile in mobile systems, they implement multitasking by using foreground and background application on iOS, or services on Android.