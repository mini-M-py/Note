# Introduction to Bash: A Beginner’s Guide

It was a part of the GNU system designed to relace or be equivalent to the UNIX shell in the GNU systems.
Bash (Bourne Again Shell) is a command-line interpreter that allows you to interact with your computer by typing commands inside of terminal. It is widely used in Linux and macOS systems (Older systems), and even in Windows via tools like WSL (Windows Subsystem for Linux). Learning Bash can help you automate tasks, manage files, and gain more control over your system. It can be used to automate various things in servers and linux computers in general. It is installed by default in most of Linux systems nowadays.

## 1. What is Bash?

Bash is:

- A **shell**: a program that takes your commands and executes them.
- A **scripting language**: you can write scripts to automate tasks.
- **Widely available**: installed by default on most Unix-like systems.

## 2. Getting Started

### Open a Terminal

- **Linux/macOS:** Press `Ctrl + Alt + T` in ubuntu or ubuntu based distros or search for “Terminal.”
- **Windows:** Use **Windows Terminal** or **Git Bash**.

**Boom!!** Bash is already is running there for you to conquer the world.

### Run a Command

```bash
echo "Hello, world!"
```

## Common commands and it structure.

```txt
command [options] [arguments]
```

- **command**: Command is an OS program that can be run for specific task to be performed. (`ls`,`echo`,`cat`)
- **options**: Options modify command behavior (usually start with `-` or `--` ) (`ls -lah`, `mkdir -p`) 
- **arguments**: Arguments are the targets of the command (`mkdir myNewDir`, `echo "Hello World"`)

> [!NOTE] : If you are in comfusion about what commands have what arguments or options a command has try doing `man myFavcmd`

### Commands for Navigation around file system

| Command | Description                                                     |
| ------- | --------------------------------------------------------------- |
| `pwd`   | Print current working directory                                 |
| `cd`    | Change directory                                                |
| `ls`    | List files and directories (non-recursive)                      |
| `tree`  | Show directory structure recursively (may require installation) |

### Commands for File Systm Manupulation

| Command | Description                                 |
| ------- | ------------------------------------------- |
| `touch` | Create an empty file                        |
| `mkdir` | Create a new directory                      |
| `rm`    | Remove a file (`rm -r` for directories)     |
| `mv`    | Move or rename files/directories            |
| `cp`    | Copy files/directories (`-r` for recursive) |

### Text Manipulation

| Command       | Description                                       |
| ------------- | ------------------------------------------------- |
| `cat`         | Display file content                              |
| `less`        | View file content with scrolling                  |
| `nano`, `vim` | Text editors (Vim is powerful but harder to learn) |
| `grep`        | It searches for given string in file or large text |

## Variables and arithmetics

`$` at the beginning represents we are in shell in normal user shell. At the middle of line `$` represents shell variable.

We can make variables and perform commands with the variables

```bash
$ str="Hello, How you doing??"
$ echo $str
```
For arithmetics, see the example

```bash
$ x=6
$ y=12
$ echo $((x+y))
```

## Input and Output Files

### Redirect Inputs

```bash
$ sort file.txt # Redirect of Input ( Sorts file content )
$ cat file.txt | grep "hello" # Piping of Input ( gives the content of file.txt to grep to work with )
```

### Redirected Output

```bash
$ echo "Hello" > file.txt  # Overwrite file.txt
$ echo "Hello" >> file.txt  # Append to end of file.txt
```

## The Prompt and Permissions

- `$`: for regular user prompt (won't let you have major permissions)
- `#`: for root user with all the previlages

> [!NOTE] :
> add `sudo` at the beginning of command to run the command with root permissions
