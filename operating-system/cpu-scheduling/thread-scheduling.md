On most modern operating system it is `kernel-level threads`, not processes, that are being scheduled by the operating system.

# Contention Scope

- `Process-Contention Scope` (`PCS`): a scheme that thread library schedules user-level threads to run on an available LWP.

Competition for the CPU takes place among threads belonging to the same process.

Typically, PCS is done according to **priority**.

Typically, PCS will **preempt** the thread currently running in favor of a higher-priority thread.

There is no guarantee of time slicing among threads of **equal** property.

- `System-Contention Scope` (`SCS`): a scheme that defines which kernel-level thread to schedule onto a CPU.

> Systems using the one-to-one model schedule threads using only SCS.
