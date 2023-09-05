# Concurrency

- A `concurrent system` supports more than one task by allowing all the tasks to make progress.
- Processing more than one task at the same time[^1].
- A condition that exists when at least two threads are making progress. A more generalized form of parallelism that can include time-slicing as a form of virtual parallelism.[^2]

# Parallelism

- A `parallel system` can perform more tahn one task simultaneously.
- Tasks are divided into smaller sub-tasks that are processed seemingly simultaneously or parallel[^1].
- A condition that arises when at least two threads are executing simultaneously.[^2]

# Difference between Concurrency and Parallelism

- Short answer: Concurrency is two lines of customers ordering from a single cashier (lines take turns ordering); parallelism is two lines of customers ordering from two cashiers (each line gets its own cashier).[^2]

> [!NOTE]
> It is possible to have concurrency without parallelism. Think about time-slicing scheduler.

[^1]: https://www.geeksforgeeks.org/difference-between-concurrency-and-parallelism/
[^2]: https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism
