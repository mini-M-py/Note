### Operating systems

There are two ways of describing OS, or we can say two aspects of OS

> 1. OS as an extended machine
> 2. OS as a resource manager

#### OS as an extended machine

OS is in charge of making sure the system (hardware) operates correctly and 
efficiently in an easy-to-use manner. The primary way the OS does this is through
a technique called `virtualization`. That is, OS takes physical resources and
transforms them into a more powerful, easy-to-use virtual form, and is called 
**virtual machine**.

#### OS as a resource manager
`Virtualization` allows many programs to run on cpu and many programs 
Concurrently, access their own instructions and data, and many programs access 
devices. Thus, the OS manages all those devices to run programs. OS is sometimes 
known as the resource manager. 

To utilize all those features of the OS, it provides some interface (APIs) which 
user can call and ask the OS to perform a certain task. Those API calls are also known 
as `system calls`. OS provides a few hundred `system calls`. We also sometimes 
say that OS's provide **standard library**.

People used to call it `supervisor` or even `master control program`.

### Structure of Operating System
Here are some basic structures of an OS. Operating systems are filled with many
complex programs, but one can start developing them small, simple, and limited, and
Then grew beyond their original structure or scope.

#### Simple Structure
This is non modular structure where all the abstract layers of the OS are
interconnected with each other. Changing one part of the OS may significantly 
affect another part of the OS.

![Simple structure](resource/os_image1.png)

#### Layered Structure
This structure breaks up the operating system into different layers. The bottoms
The layer is the hardware, and the topmost layer is the user interface. This allows
The developer has to change and maintain the inner mechanism of each layer without 
disturbing the implementation of the other layer, as long as the external interface of 
Each layer remains the same.

#### Monolithic Structure
In this structure, create a collection of procedures (functions), each of which
can call the others whenever it's needed. The interface of functions like 
parameters or arguments and return values is well defined. A developer can 
change the inner complexity of any procedure without disturbing other one as 
long as the interface of the procedure remains the same.

![ Monolithic Structure](resource/os_image2.jpeg)

#### Microkernel Structure
In this structure, all the nonessential parts of the kernel are removed and make
the kernel as minimal as possible. The operating system is divided into the kernel
and other programs. This makes other programs run over the microkernel and makes
extending of OS efficient. The only overhead of this structure is constant 
message transferring between the kernel and other programs.

![microkernel Structure](resource/os_image3.jpeg)
