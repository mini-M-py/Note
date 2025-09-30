#### Process
The computer program that is currently executing on the processor is called
process. It turns out one want to run multiple program (process) in a single
CPU. For example consider your personal computer play music, run browsers etc
at the same time. To accomplish this kind of behaviour OS create illusion of 
running multiple CPUs running at the same time but in reality there is only one
physical CPU. This method of creating illusing of multiple CPUs is called
virtulization of CPU. 

### Process APIs
- Create: An operating system must include a method to create new process. When
use type comand on shell or click icons OS should create new process. The first
thing os do is load execution code and static data from hard drive to memory. 
In early OSes use to load the whole program at once but new or modern OSes uses
lazy approach ie; only loading certain chunks of code and data from hard drive.

- Destroy: As there is way to create process then there should be a way to 
destroy processes forcefully. Of course processes will run and exit by 
themselves. Sometime we have to kill them forcefully.

- Wait: Sometime processes needed to be wait for other processes or resoponce to
peripheral devices thus waiting interface is quite useful.

- Miscellaneous Control: Other then distroy or wait there are sometime some 
other interface included on Oses. For example: Suspend, it use to pause the 
execution of program and the resume to resume the suspended program.

- status: There should be a way to get current status of processes.

### Process Life cycle
When process is executing it goes through the different states. These states 
are not standers but in general modern OS uses following types of states in 
their process life cycle

1. **Start**: This is the state when process initiated to execute.

2. **Ready**: In this state process is wating to assign to the CPU.

3. **Running**: This state indicates that the process is currently running on 
CPU.

4. **Wating**: Process is wating for the data from resources like input device,
hard drive etc.

5. **Terminated**: This state indicates that the process is finished executing.

#### Process Control Block (PCB)

The process control block (PCB) is used to track the proces's execution. It is 
a block of memeory contains information about process state, program  counter,
stack pointer, status of opened files, scheduling algorithms, etc. When the 
process made transitions from one state to another, the operating system must
update information in the process's PCB.

#### Components of PCB

1. **Process State**: It is use to define the process state of any process. In 
other words, process control block refers the state of the process.

2. **Process privileges**: This is required to allow/disallow acess to system
resources.

3. **Process ID**: In a computer system there are multiple process running
simulteneously and each process has its unique ID. This ID helps to schedling 
the processes.

4. **Pointer**: A pointer to a parent process (More inforamtion is at prcess 
Hierarchies)

5. **Program Counter**: Program counter is pointer to address of the next 
instruction to be executed for this process.

6. **CPU registers**: This information is comprising with various registers,
such index and stack that are associated with process.

7. **CPU Scheduling**: There are many process running simulteneously and each 
process have its prority. Scheduling information is very useful in managing any 
computer system.

8. **Memory management information**: This include information of page table,
memory limits, segment table depending on memory used by operating system.

9. **Accounting information**: This include information  about CPU used for 
process execution, time limits, execution ID etc.

10. **IO status information**: This include a list of I/O devices allocated to 
the process.

#### Process Hierarchies 

The process of creating new process from their parent process and again creating 
new process from previously created process in tree like structure is called
process Hierarchies. 

![process Hierarchies](resource/os_image4.png)

A create B and C\
B create D, E and F\
C create G\
D create H\
H create I

### Process Implementation
In virtulization OS has to share physical CPU among the jobs seemingly at the
same time. In a simple idea, we run a process a little while and run another 
little while. But there are some problems while implementing this idea. Like,
*performance*, *control over the system*.  

**Direct Execution**

The **Direct Execution** means directly run the programme in CPU becaues it
give the maximum performance. When OS wantsto start a new process, it creates 
entry on process entry, allocates the memory load the code and static data 
into memory from disk and execute the code in CPU and jumps back to kernel.
Sounds simple? but it is not we have not consider what happens when process do
something unhealthy to the system or how to switch between processes to 
implement virtulization.

Running natively on CPU has it owns obvious advantages but what if process want
to do some ristricted task like ganing control over I/O, read and write files etc.
we cannot let any processes do whatever it wants. It would be complete disaster.
To over come this problem it take new things to introduce called **Process mode**.
There are two modes in general:

- User mode.
- kernel mode.

**User mode*** is more ristrictive, it has to take promission or ask for kernel help
to take some restictive action like reading and writing on files or I/O 
opeations.

**Kernel mode** is exact opposite of user mode. It has complete control over the 
system. Processes run on kernel mode can performe any kind of ristrictive 
operations.

To performe restrictive task, processes run in usermode make system calls like
reading and writing files and creating new processes, communicating between two
processes then kernel carefully give privilage to process if it allowed. After 
return from the system calls the privilage goes back to use mode.

The another big problem of direct execution is switching process. Switching 
processes should be simple right? Just stop one and start another. When we think
back, if a process is running on cpu then os is not running so what can we do
at all?

- **Coopeartive Approach**: In this apporach OS waits for the process to give 
control to the OS. A process give contorol to the OS after completeing its task,
calling some system calls or doing some illegal activities. This is a passive
approach to switch process. when a process by design or by bugs that doesnot
give control back to OS then OS just strike down the processes which do some
offending behaviour.

- **Non cooperative Approach**: It turn out an OS cannot do anything without 
any help hardware to get control form the process which rufuse to give control
to the OS form cooperative approcach. In a non Coopeartive approach OS takes 
help from timer interrupt device. The timer can programmed to make interrupt 
signal after certain time to halt current processes and switch to OS. The timer
should be start at the boot time. Starting and stoping timer are privilaged
instructions. This works similarly like when an sys-call trap into kernel.

The role of process control block (PCB) shines here the most. After the control
goes over the OS. It has two option run currently running process or switch to
another process. Before swithching OS has to store the some register value of
currently running process in PCB because we have to restore its values and 
continue to execute after it gets its turn to execute. After storing current
process value then it restore value of next process and return control to that 
process. Like this switching between two process happens.\
PCB has the most importat part here because it sotres and restore all  the 
information related to the process.

Every processes has it own user stack and kernel stack. When trap happens all the
necessary register values are push to the kernel stack. If OS decide to run
currently running process then it will restore those value to the use stack
and continue running. If it decide to switch to another process it will save 
those value to PCB. Restoring happend in same ways firstly it resotre all vaues
and put it on kernel stack form PCB then push those value to user stack and 
after that register will restore from the stack.

There are some reason to use kernel stack:
1. If someone mess with user stack while running cpu in kernel mode then kernel
stack is safe.

2. The register value of process won't get disappear while running kernel.





