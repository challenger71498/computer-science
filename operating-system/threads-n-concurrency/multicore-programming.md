# Multicore

- A system that has multiple computing cores, on a single processing chip.

# Programming Challenges

1. `Identifying Tasks`: divide a task into seperate, concurrent tasks.
2. `Balance`: ensure that tasks perform equal work of equal value.
3. `Data Splitting`: the data accessed and manipulated by the tasks must be divided.
4. `Data Dependency`: the data accessed by the tasks must be examined for dependencies between 2 or more tasks.
5. `Testing and Debugging`: testing concurrent programs is more difficult than single-threaded ones.

# Types of Parallelism

- `Data Parallelism`: distributing subsets of the same data across multiple computing cores and performing the **same** operation.
- `Task Parallelism`: distributing tasks (threads) across multiple cores. Each thread is performing a unique operation.

However, data and task parallism are **not mutually exclusive**.

# Amdahl's Law

Amdahl's Law is a formula that identifies potential performance gains from adding additional computing cores to an application that has both serial and parallel components.

The serial portion of an application can have a **disproportionate effect** on the performance we gain by adding additional computing cores.