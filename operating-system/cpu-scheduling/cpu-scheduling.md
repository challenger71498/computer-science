
> When one process has to wait, the operating system takes the CPU away from that process and gives the CPU to another process.

# CPU-I/O Burst Cycle

Process execution consists of a cycle of CPU execution and I/O wait.

- `CPU Burst`
- `I/O Burst`

# CPU Scheduler

Selects a process from the processes in memory and allocates the CPU to that process.

> Note that the ready queue is **not** necessarily a FIFO queue.

# Preemptive and Nonpreemptive Scheduling

CPU-scheduling decisions may take place under the following four circumstances:
1. Running state to the waiting state.
2. Running state to the ready state.
3. Waiting state to the ready state.
4. Process terminates.

- `Nonpreemptive` (`Cooperative`)
  - Scheduling takes place only under 1, 4.
  - Once the CPU has been allocated to a process, the process **keeps** the CPU until it releases. 
- `Preemptive`
  - Scheduling takes place on every circumstances.
  - Can result in `Race Conditions`.
  - Requires mechanisms such as `Mutex Locks` to prevent race conditions when accessing shared kernel data structures.

The sections of code affected by interrupts must be guarded from simultaneous use.

> Operating-system kernels can be designed as either nonpreemptive or preemptive.

> Nonpreemptive scheduling is a poor one for supporting real-time computing.

> All modern operating systems use preemptive scheduling.

# Dispatcher

- `Dispatch`: the module that gives control of the CPU's core to the process selected by the CPU scheduler.

The dispatcher is invoked during every context switch.

- `Dispatch Latency`: the time it takes for the dispatcher to stop one process and start another

> On Linux, `vmstat` shows the number of context switches on a system-wide level.
>
> Also, the `/proc/(pid)/status` file shows the number of context switches for a given process.

- `Voluntary Context Switch`: process has given up control of the CPU.
- `Nonvoluntary Context Switch`: the CPU has been taken away from a process.

# Scheduling Creteria

- `CPU Utilization`: the degree of busyness of the CPU.
- `Throughput`: the number of processes that are completed per time unit.
- `Turnaround Time`: how **long** it takes to execute; the interval from the time of submission of a process.
- `Waiting Time`: the sum of periods spend waiting in the **ready queue**.
- `Response Time`: the time from the submission of a request until the **first response** if produced.

> For interactive systems, it is more important to minimize the variance in the response time than to minimize the average response time.
