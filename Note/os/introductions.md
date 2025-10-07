### Operating systems

There are two ways of describing OS or we can say two aspect of OS

> 1. OS as an extended machine
> 2. OS as a resource manager

#### OS as an extended machine

OS is in charge of making sure the system (hardware) operates correctly and 
efficiently in an easy-to-use manner. The primary way the OS does this through
a technique called `virtualization`. That is OS takes physical resources and
transform it into more powerful easy-to-use virtual form and called 
**virtual machine**.

#### OS as a resource manager
`Virtualization` allows many programs to run on cpu and many program 
concurrently access their own instructions and data and many program access 
devices. Thus, OS manage all those devices to run programmes, OS is sometime 
known as resource manager. 

To utilize all those features of OS, it provides some interface (APIs) which 
user can call and ask OS to perform certain task. Those APIs calls also known 
as `system calls`. OS provides few hundred of `system calls`. We also sometimes 
say that OS's provides **standard library**.

People use to call it `supervisor` or even `master control program`.

### Structure of Operating System
Here are some basic structures of OS. Operating systems are filled with many
complex programs but one can start developing it small, simple, and limited and
then grew beyond their original structure or scope.

#### Simple Structure
This is non modular structure that is all the abstract layer of OS are
interconnected with each other. Changing one part of OS may significantly 
affect on other part of OS.

![Simple structure](resource/os_image1.png)

#### Layered Structure
This structure breaks up the operating system into different layers. The bottoms
layer is the hardware and the topmost layer is the user interface. This allows
developer to change and maintain the inner mechanism of each layer without 
disturbing the implementation of other layer as long as external interface of 
each layer remains same.

#### Monolithic Structure
In this structure create as a collection of procedures (function), each function
can call each other when ever it's needed. The interface of function like 
parameters or arguments and return value are well defined. Developer can 
change inner complexity of any procedure without disturbing other one as 
long as interface of procedure remain same.

![ Monolithic Structure](resource/os_image2.jpeg)

#### Microkernel Structure
In this structure all the nonessential parts of kernel are removed and make
kernel minimal as much as possible.The operating system is divide into kernel
and other programs. This makes other program run over the microkernel and make
extending of OS efficient. The only overhead of this structure is constant 
message transferring between kernel and other programs.

![microkernel Structure](resource/os_image3.jpeg)
