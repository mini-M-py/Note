### System calls

The interface between a process and an operating system is provided by 
`system calls`. In most cases these calls are available as assembly language
instructions. System calls are usually called from user's programs and kernel
provides require resources. When system calls are running control over machine
goes to kernel and after finishing it give control back to user's programs.

**Types of system calls:**
Different system call are rquired in different situations. Those call server 
different purpose. There are mainly five types of system calls:

- **Process Control**: These system calls deal with process like creating, 
terminating etc.

- **File Management**: These calls deal with file manipulation like open, close,
read, write etc.

- **Device Management**: These calls are used to manage peripheral devices like 
Keyboard, Mouse, Moniter, Printer etc.

- **Information Maintenance**: These calls are used to handel and transfer 
information between kerneal and user space.

- **Communication**: These calls deals with creating and deleting communication
conncections. These are use to pass information and data between processes.

| Types of system calls | Unix |
|-----------------------|------|
|Process Control|fork(), exit(), wait()|
|File Management|open(), read(), write(), close()|
|Device Management|ioctl(), read(), write()|
|Information Maintenance|getpid(), sleep(), alaram()|
|Communication|pipe(), shmget(), mmap()|
|Protection| chmod(), umask(), chown()|

### System Programs
**System Programs** are different from **system calls**. They provide an 
environment where programs can be deveoped and executed. In the simple term,
they provide bridge between the user interface and system calls. For example,
compiler, shell, web server, networking system  etc. They mostly have low
runtime overhead. Some part of prgrams may be directly written in assembly 
language. The user view of the system is actually defined by system programs
and not system calls. The system programs are used to program the operating
system software. 
