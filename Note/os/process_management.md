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


