Mechanism for process creation and termination.

# Process Creation

- `Process Identifier` (as well known as `PID`): a unique id for the process, typically an integer value

> For a typical Linux system, a process creation is being executed like a tree generation.
>
> The `systemd` process is being create at first (therefore it's pid is always 1), serves as the root process.
>
> Then several process are created after, such as `logind`, `sshd`, etc, being child processes of the `systemd`.

> Linux provides `pstree` command to display a tree of all processes in the system.

## Resources

On child creation, its resource could be obtained by:
- directly from the opreating system
- constrained to a subset of the resources of the parent process

## Continuation

On child creation, 2 possible executions are exist:
- continues to execute concurrently with its children
- waits until its children being terminated.

## Address-space

On child creation, its address-spaces could be configured by:
- is a duplicate of the parent
- has a new program loaded into it

> Unix offers a `fork()` system call to create a child process, the newborn.
>
> After a `fork()` system call, call `exec()` to replace the process' memory space with a new program.
>
> `exec()` does not return control unless an error occurs.

> The parent process may call `wait()` to move itself off the ready queue until the child terminates.

# Process Termination

> By `exit()` call, a process asks the opreating system to delete itself.
>
> The process may return a value to the parent process via `wait()`.

A parent may **terminate** the execution of the child process, due to:
- exceeded its usage of some of the resources
- no longer required
- the parent itself is exiting, and the operation system does not allow a child to continue if its parent terminates

Some systems does not allow a child to exist when parent is temrinated.
- `Cascading Termination`: if a process terminates, its children must also terminate.

> Cascading termination is normally initiated by operating system.

## Resource Deallocation

The child process entry in the process table **must be remain there** until the parent calls `wait()`, as the process table contains the process' exit status.

### Zombie Process

A process that has terminated, but whose parent has **not (yet) called** `wait()`.

Once the parent process calls `wait()`, the zombie process is released.

> All processes transition to this state whewn they terminate, but generally they exist as zombies only briefly.

## Orphan Process

A terminated process which parent **did not invoke** `wait()` and **terminated**.

# Android Process Hierachy

Android uses `Importance Hierarchy` to make system consider which process to terminate first, with limited system resources.

Such importance hierarchies are:
- `Foreground Process`: the current process visible on screen.
- `Visible Process`: not directly visible, though the foreground process is referring to.
- `Service Process`: similar to background process, but performing the activity apparent to the user.
- `Background Process`: not apparent to the user.
- `Empty Process`: no active components.

> Android development practices suggest following the guidelines of the `process life cycle`.