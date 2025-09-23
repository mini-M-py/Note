#### Process
The computer program that is currently executing on the processor is called
process.

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

4 **Pointer**: A pointer to a parent process (More inforamtion is at prcess 
Hierarchies)

5 **Program Counter**: Program counter is pointer to address of the next 
instruction to be executed for this process.

6 **CPU registers**: This information is comprising with various registers,
such index and stack that are associated with process.

7. **CPU Scheduling **: There are many process running simulteneously and each 
process have its prority. Scheduling information is very useful in managing any 
computer system.

8. **Memory management information**: This include information of page table,
memory limits, segment table depending on memory used by operating system.

9. **Accounting information**: This include information  about CPU used for 
process execution, time limits, execution ID etc.

10. **IO status information**: This include a list of I/O devices allocated to 
the process.
