# Process
- A program in execution
- An active entity
- A program becomes a process when an executable file is loaded into memory.
- A process can be an execution environment for other code.

> We also use the terminology `Job` for the same meaning as Process.

# Memory Layout
- `Text` Section - the executable code
- `Data` Section - global variables
- `Heap` Section - dynamically allocated during runtime
- `Stack` Section - temp storage when invoking functions, such as parameters, return addresses, and local variables

Sizes of text section and data section are fixed.

Sizes heap section and stack section may change. They grow **towards** each other, *never* **overlap** though.

# Process State
- `New`- process is being created
- `Running` - instructions are being executed
- `Waiting` - waiting for some event, such as I/O or signal receive
- `Ready` - waiting to be assigned to a processor
- `Terminated` - execution finished

Only **one** process at a time can be a state of `Running`. However, **multiple** processes can be `Waiting` and `Ready` state.

## Process Transitions
- `Admitted` - `New` to `Ready`
- `Scheduler Dispatch` - `Ready` to `Running`; this is where the Task Scheduler shines.
- `Interrupt` - `Running` to `Ready`
- `I/O or Event Wait` - `Running` to `Waiting`
- `I/O or Event Completion` - `Waiting` to `Ready`
- `Exit` - `Running` to `Terminated`

# Process Control Block (PCB)
As known as `Task Control Block`(`TCB`).

- Process State - as described above
- Program Counter - address of the next instruction
- CPU Registers
- CPU-Scheduling Information - process priority, scheduling queues, etc.
- Memory-Management Information - base & limit registers, page tables, segment tables.
- Accouting Information - CPU and real time used, account numbers, process numbers, etc.
- I/O Status Information - list of I/O devices, open files, etc.

> On systems that support threads, the PCB is extended to include information for each thread.

# I/O-Bound Process, CPU-Bound Process
`I/O-Bound Process` spends more time on I/O then computations, `CPU-Bound Process` does the opposite.