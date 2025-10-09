#### Process
The computer program that is currently executing on the processor is called
a process. It turns out one wants to run multiple programs (processes) in a single
CPU. For example, consider your personal computer playing music, running browsers, etc,
at the same time. To accomplish this kind of behavior, the OS creates an illusion of 
running multiple CPUs running at the same time, but in reality, there is only one
physical CPU. This method of creating an illusion of multiple CPUs is called
virtualization of the CPU. 

### Process APIs
- Create: An operating system must include a method to create a new process. When
the user types a  command on the shell or clicks icons OS should create a new process. The first
thing the OS does is load execution code and static data from the hard drive to memory. 
In early OSes use to load the whole program at once, but new or modern OSes use
lazy approach, i.e., only loading certain chunks of code and data from the hard drive.

- Destroy: As there is a way to create processes, there should be a way to 
destroy processes forcefully. Of course, processes will run and exit by 
themselves. Sometimes we have to kill them forcefully.

- Wait: Sometimes processes need to wait for other processes or respond to
Peripherals device,s thus waiting interface is quite useful.

- Miscellaneous Control: Other than destroy or wait, there are sometimes some 
other interfaces included on OSes. For example, Suspend is used to pause the 
execution of a program, and Resume is used to resume the suspended program.

- Status: There should be a way to get the current status of processes.

### Process Life Cycle
When a process is executing, it goes through different states. These states 
are not standers, but in general, modern OS use the  following types of states in 
their life cycle

1. **Start**: This is the state when the process is initiated to execute.

2. **Ready**: In this state process is waiting to be assigned to the CPU.

3. **Running**: This state indicates that the process is currently running on 
CPU.

4. **Waiting**: Process is waiting for the data from resources like the input device,
hard drive, etc.

5. **Terminated**: This state indicates that the process is finished executing.

#### Process Control Block (PCB)

The process control block (PCB) is used to track the process's execution. It is 
a block of memory contains information about the process state, program  counter,
stack pointer, status of opened files, scheduling algorithms, etc. When the 
processes made transitions from one state to another, the operating system must
Update information in the process's PCB.

#### Components of PCB

1. **Process State**: It is used to define the process state of any process. In 
other words, process control block refers the state of the process.

2. **Process privileges**: This is required to allow/disallow access to the system
resources.

3. **Process ID**: In a computer system, multiple processes are running
simultaneously, and each process has its unique ID. This ID helps to schedule 
the processes.

4. **Pointer**: A pointer to a parent process (More information is at process 
Hierarchies)

5. **Program Counter**: The Program Counter is a pointer to the address of the next 
instruction to be executed for this process.

6. **CPU registers**: This information comprises various registers,
such an index and stack that are associated with the process.

7. **CPU Scheduling**: Many processes are running simultaneously, and each 
process has its own priority. Scheduling information is very useful in managing any 
computer system.

8. **Memory management information**: This include information of page table,
memory limits, segment table depending on memory used by operating system.

9. **Accounting information**: This includes information about the CPU used for 
process execution, time limits, execution ID, etc.

10. **I/O status information**: This include a list of I/O devices allocated to 
the process.

#### Process Hierarchies 

The process of creating a new process from its parent process, and again creating 
A new process from a previously created process in a tree-like structure is called
process Hierarchies. 

![process Hierarchies](resource/os_image4.png)

A creates B and C\
B create D, E, and F\
C create G\
D create H\
H create I

### Process Implementation
In virtualization OS has to share the physical CPU among the jobs seemingly at the
same time. In a simple idea, we run a process for a little while and run another 
little while. But there are some problems while implementing this idea. Like,
*performance*, *control over the system*.  

**Direct Execution**

The **Direct Execution** means directly running the program on the CPU because it
gives the maximum performance. When an OS wants to start a new process, it creates 
an entry in the process table, allocates the memory, loads the code and static data 
into memory from disk, executes the code in the CPU, and jumps back to the kernel.
Sounds simple? But it is not we have not considered what happens when a process does
something unhealthy to the system or how to switch between processes to 
implement virtualization.

Running natively on CPU has its own obvious advantages, but what if a process wants
to do some restricted task like gaining control over I/O, reading and writing files, etc?
We cannot let any processes do whatever they want. It would be a   complete disaster.
To overcome this problem, it takes new things to introduce called **Process mode**.
There are two modes in general:

- User mode.
- Kernel mode.

**User mode*** is more restrictive; it has to take permission or ask for kernel help
to take some restrictive action, like reading and writing on files or I/O 
operations.

**Kernel mode** is the exact opposite of user mode. It has complete control over the 
system. Processes run in kernel mode can perform any kind of restrictive 
operations.

To perform a restrictive task, processes run in user mode make system calls like
reading and writing files, creating new processes, communicating between two
processes, and then the  kernel carefully gives privileges to the process if it is allowed. After 
returning from the system calls, the privilege goes back to use mode.

The other big problem of direct execution is the switching process. Switching 
processes should be simple, right? Just stop one and start another. When we think
back, if a process is running on the CPU, then os is not running, so what can we do
at all?

- **Cooperative Approach**: In this approach OS waits for the process to give 
control to the OS. A process gives control to the OS after completing its task,
calling some system calls, or doing some illegal activities. This is a passive
approach to the switch process. When a process, by design or by bugs that doesn't
give control back to the OS, then the OS just shuts down the processes that exhibit some
offending behavior.

- **Non-cooperative Approach**: It turns out that an OS cannot do anything without 
any help from hardware to get control of the process, which refuses to give control
to the OS from the cooperative approach. In a non-cooperative approach, OS takes 
help from a timer interrupt device. The timer can be programmed to make an interrupt 
signal after a certain time to halt current processes and switch to the OS. The timer
should start at boot time. Starting and stopping the timer are privileged
instructions. This works similarly to when a syscall traps into the kernel.

The role of the process control block (PCB) shines here the most. After the control
goes over the OS. It has two options: run the currently running process or switch to
another process. Before switching OS has to store the same register value of
the currently running process in PCB because we have to restore its values and 
continue to execute after it gets its turn to execute. After storing the current
process value then it restores the value of the next process and returns control to that 
process. Like this, switching between two processes happens.\
PCB is the most important part here because it stores and restores all the 
information related to the process.

Every process has its own user stack and kernel stack. When a trap happens, all the
necessary register values are pushed to the kernel stack. If the OS decides to run
the currently running process, then it will restore those values to the use stack
and continue running. If it decides to switch to another process, it will save 
those values to the  PCB. Restoring happened in the same way, firstly, it restores all values
and puts them on the kernel stack from PCB, then pushes those values to the user stack, and 
after that, registers will be restored from the stack.

There are some reasons to use the  kernel stack:
1. If someone messes with the  user stack while running CPU in kernel mode, then the kernel
stack is safe.

2. The register value of the process won't disappear while running the kernel.





