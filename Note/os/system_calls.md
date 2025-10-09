### System calls

The interface between a process and an operating system is provided by 
`system calls`. In most cases, these calls are available as assembly language
instructions. System calls are usually called from users' programs, and the kernel
provides the required resources. When system calls are running, control over the machine
goes to the kernel, and after finishing, it gives control back to the user's programs.

**Types of system calls:**
Different system calls are required in different situations. Those calls serve 
a different purpose. There are mainly five types of system calls:

- **Process Control**: These system calls deal with processes like creating, 
terminating, etc.

- **File Management**: These calls deal with file manipulation like open, close,
read, write, etc.

- **Device Management**: These calls are used to manage peripheral devices like 
Keyboard, Mouse, Monitor, Printer, etc.

- **Information Maintenance**: These calls are used to handle and transfer 
information between the kernel and the user space.

- **Communication**: These calls deal with creating and deleting communication
connections. These are used to pass information and data between processes.

| Types of system calls | Unix |
|-----------------------|------|
|Process Control|fork(), exit(), wait()|
|File Management|open(), read(), write(), close()|
|Device Management|ioctl(), read(), write()|
|Information Maintenance|getpid(), sleep(), alaram()|
|Communication|pipe(), shmget(), mmap()|
|Protection| chmod(), umask(), chown()|

A system call resembles typical function calls in the C programming language.
The fact that it is a function call, but hidden inside that are famous trap 
instructions. When we call any system calls like open(), we are calling a  C 
library function that agrees upon a calling convention with the kernel.\
Of course, it is not allowed for user-mode processes to jump to the
address of the system calls directly and execute them like other function calls. 
There is something called a trap which is invoke the CPU to go into kernel mode.
*Hey, go to the kernel mode and handle this.* The user code is only responsible for putting 
the syscall number into the desired register or stack. Then the system examines the number
and looks up to the trap table and jumps to the corresponding address to handle
system calls

> **Trap Table**: The system keeps a table in memory at boot time, which has
the addresses of different instructions and jumps to those addresses when different
interrupts and traps happen. In short, it stores the address of the actual code of 
the syscall that the user code invoked.

### System Programs
**System Programs** are different from **system calls**. They provide an 
environment where programs can be developed and executed. In simple terms,
they provide a bridge between the user interface and system calls. For example,
a compiler, a shell, a web server, a networking system, etc. They mostly have low
runtime overhead. Some parts of programs may be directly written in assembly 
language. The user view of the system is actually defined by system programs
and not system calls. The system programs are used to program the operating
system software. 
