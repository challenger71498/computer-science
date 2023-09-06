# Gantt Chart

A bar chart that illustrates a particular schedule.

# First-Come, First-Served Scheduling (FCFS)

The process that requests the CPU first is allocated the CPU first.

This algorithm is nonpreemptive.

## Convoy Effect

All the other processes wait for the one big process to get off the CPU.

# Shortest-Job-First Scheduling (SJF)

The process that has the smallest next CPU burst is allocated the CPU first.

If the next CPU bursts of two processes are the same, FCF scheduling is used to break the tie.

> SJF scheduling depends on the length of the **next** CPU burst of a process, rather than its total length.

It cannot be implimented at the level of CPU scheduling, as there is no way to know the length of the next CPU burst.

Therefore, we need to *approximate* it, by using an `exponential average` of the measured lengths of previous CPU bursts.

SJF can be either preemptive of nonpreemptive.

Preemptive SJF scheduling is sometimes called `Shortest-Remaining-Time-First` scheduling.

# Round-Robin Scheduling

Similar to FCFS, but preemption is added.

- `Time Quantum` (or `Time Slice`)
  - A small unit of time.
  - Generally 10~100ms in length.

The scheduler picks the first process, sets a timer to interrupt after 1 time quantum, and dispatches.

One of two things will happen:
- Process have a CPU burst of **less** than 1 time quantum: process itself will release the CPU voluntarily.
- Process have a CPU burst of **more** than 1 time quantum: timer causes an interrupt, context switch is executed.

The average waiting time under the RR policy is often long.

If the time quantum is extremely large, the RR policy is the same as the FCFS policy.

The average `Turnaround Time` can be improved if most processes finish their next CPU burst in a single time quantum.

> A rule of thumb is that 80% of the CPU bursts should be shorter than the time quantum.

# Priority Scheduling

A priority is associated with each process, and the CPU is allocated to the process with the highest priority.

> The SJF algorithm is a special case of the general priority-scheduling algorithm.

There is no geneal agreement on whether 0 is the highest or lowest property.

Priorities can be defined either internally or externally.

Priority scheduling can be either preemptive or nonpreemptive.

## Starvation

- `Starvation` (`Infinite Blocking`): a indefinite failure of resource acquisition, thus being blocked forever.

A priority scheduling algorithm can leave some low-priority processes waiting indefinitely.

## Solutions to the Starvation

### Aging

Gradually increasing the priority of processes that wait in the system for a long time.

By aging the process we can prevent the starvation of a process.

### Combination with Round-Robin

By combining RR with priority scheduling, the system runs processes with the same property using round-robin scheduling.

# Multilevel Queue Scheduling

Seperate queues for each distinct priority, and priority scheduling simply schedules the process in the highest-priority queue.

This approach also works well when priority scheduling is combined with round-robin: if there are multiple processes in the highest-priority queue, they are executed in round-robin order.

> A common division is made between `foreground` and `background` processes.

Each queue might have its own scheduling algorithm.

There is a scheduling among the queues, which is commonly implemented as fixed-priority preemptive scheduling.

Time-slicing among the queues is possible.

# Multilevel Feedback Queue Scheduling

Normally, when the multilevel queue scheduling algorithm is used, processes are permanently assigned to a queue when they enter the system.

The `Multilevel Feedback Queue` scheduling algorithm, in constrast, allows a process to move between queues.

Parameters that defineds multilevel feedback queue:
- The number of queues
- The scheduling algorithm for each queue
- The method used to determine when to upgrade a process to a higher-priority queue
- The method used to determine when to demote a process to a lower-priority queue
- The method used to determine which queue a process will enter when that process needs service

> The definition of a multilevel feedback queue scheduler makes it the most general CPU-scheduling algorithm.
