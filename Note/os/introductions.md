### Operating systems

There are two ways of describing OS or we can say two aspect of OS

> 1. OS as an extended machine
> 2. OS as a resource manager

#### OS as an extended machine

OS is in charge of making sure the system (hardware) operates correctly and 
efficiently in an easy-to-use manner. The primary way the OS does this through
a technique called `virtualization`. That is OS takes physical resources and
transform it into more powerful easy-to-use virtual form and also called 
**virtual machine**.

#### OS as an resource manager
`Virtualization` allows many programs to run on cpu and many program 
concurrently access their own instructions and data and many prgramme access 
devices. Thus OS manage all those devices to run progrmmes, OS is sometime 
known as resource manager. 

To utilize all those features of OS, it provides some interface (APIs) which 
user can call and ask OS to performe certain task. Those APIs calls also known 
as `system calls`. OS provides few hundred of `system calls`. We also sometimes 
say that OS's provides **standard library**.

People use to call it `supervisor` or even `master control program`.

### Structure of Operating System
Here are some basic strutures of OS. Operating systems are filled with many
complex programs but one can start developing it small, simple and limited and
then grew beyond their original structure or scope.

#### Simple Structure
![Simple structure](resource/os_image1.pn

#### Layered Structure
This structure breaks up the operating system into different layers. The bottoms
layer is the hardware and the topmost layer is the user interface. This allows
developer to change and maintain the inner mechanism of each layer without 
disturbing the implementation of other layer as long as external interface of 
each layer remains same.

#### Monolithic systems
