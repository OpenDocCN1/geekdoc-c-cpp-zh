
## 10 Processes

- To describe the concept of a process, and execution of multiple processes on a computer system with a single central processing unit (CPU)
- To explain how a shell executes commands
- To discuss static and dynamic display of process attributes
- To discuss the main memory image of a Linux process
- To briefly describe the concept of CPU scheduling and scheduling classes in Linux
- To explain the concept of foreground and background processes, including a description of a daemon and its uses
- To describe sequential and parallel execution of commands
- To discuss process and job control in Linux: foreground and background processes, sequential and parallel processes, suspending processes, moving foreground processes into the background and vice versa, and terminating processes
- To describe the Linux process hierarchy
- To cover the following commands and primitives:
  `<Ctrl+C>`, `<Ctrl+D>`, `<Ctrl+Z>`, `<Ctrl+\>`, `;`, `&`, `( )`, `bg`, `chrt`, `fg`, `jobs`, `kill`, `nice`, `nohup`, `ps`, `pstree`, `renice`, `sched`, `size`, `sleep`, `top`, `ulimit -s`

As we have mentioned in Chapter 1, a process is a program in execution. The program may be assembly language code, an executable code generated after compiling a source program written in a high-level language such as C++, an interpreted code written in LISP, JavaScript, Perl, Python, Interpreted C (CINT), or a Linux shell. The Linux system creates a process every time you run an external command, and the process is removed from the system when the command finishes its execution. We use the terms *program* and *command* interchangeably.

Process creation and termination are the only mechanisms used by the Linux system to execute external commands. In a typical time-sharing system such as Linux, which allows multiple users to use a computer system and run multiple processes simultaneously, hundreds to thousands of processes are created and terminated every day. Remember that the central processing unit (CPU) in the computer executes processes. The question is, how does a system with a single CPU or with one core execute multiple processes simultaneously? Even for systems with multiple CPUs or multiple cores in a CPU, the number of processes is greater than the number of CPUs or cores. How does a system with the number of processes larger than the number of CPUs or CPU cores execute these processes simultaneously? A detailed discussion of this topic is beyond the scope of this textbook, but we briefly address it in Section 10.5.2 and later in Section 10.5.1. You can get detailed information about CPU scheduling and related algorithms in a book on operating system concepts. Later in the chapter, we discuss viewing the static and dynamic state of processes, foreground and background processes, daemons, jobs, process and job attributes, and process and job control. We use the terms *time-sharing* and *multitasking* synonymously.

You can assign a higher nice value to your processes by using the nice or renice command, but the nice value cannot be set to a negative number by a nonsuperuser. A higher nice value means a higher priority value and, hence, a lower priority. So, when you increase the nice value of your process, you are being nice to other user processes. The formula clearly indicates that the higher the recent CPU usage of a process, the higher its priority value and the lower its priority. Thus, Linux favors processes that have used less CPU time in the recent past. A text editor such as vim gets higher priority than a process that computes the value of pi (π) because vim spends most of the time waiting for I/O—that is, reading keyboard input, reading/writing to disk, and displaying file data or keyboard input on the screen. On the other hand, the process that computes π spends most of its time doing calculations—that is, using the CPU. Recalculating priority values of all the processes every second causes process priorities to change dynamically (up and down). In Section 10.5, we further explore the Linux scheduling concept. We also give a few more details about the use of the nice and renice commands in Section 10.5.2.

### Exercise 10.1

Search the Web for context switch times for different CPUs. What is the range of these times for different CPUs? Which CPU has the shortest context switch time and how much is this time?

### Exercise 10.2

Give three examples each of CPU-bound and I/O-bound processes.

### 10.3 Linux Process States

A Linux process can be in one of many states, moving from one state to another, eventually finishing its execution, normally or abnormally, and getting out of the system. A process terminates normally when it finishes its work and exits the system gracefully. A process terminates abnormally when it exits the system because of an exception (error condition) or intervention by its owner or the superuser. The owner of the process can intervene by using a command or a particular keystroke to terminate the process. We discuss these commands and keystrokes later in the chapter. The primary states that a process can be in are shown in the state diagram in Figure 10.1.

![](img/2a18e06cd9c6395e451f26126ecba1fd_263_0.png)

The waiting state encompasses several states; we use the term here to keep the diagram simple. Some of the states belonging to the waiting state are listed under the oval representing the state. Table 10.1 gives a brief description of these Linux process states.

### Table 10.1
A Brief Description of the Linux Process States

| State | Description |
|-------|-------------|
| Ready | The process is ready to run but does not have the CPU. Based on the scheduling algorithm, the scheduler decided to give the CPU to another process. Several processes can be in this state, but on a machine with a single CPU, only one can be executing/running (i.e., using the CPU). |
| Running | The process is actually running (i.e., using the CPU). |
| Waiting | The process is waiting for an event. Possible events are an I/O operation to complete (e.g., disk/terminal read or write), a child process to complete (the parent is waiting for one or more of its children to exit), or the process itself is waiting to be reawakened having been put to sleep. |
| Swapped | The process is ready to run, but it has been temporarily put on the disk (on the swap space); perhaps it needs more memory and there is not enough available at this time. |
| Zombie | A dying process is said to be in a zombie state. Usually, when the parent of a process terminates before it executes the exit call, it becomes a zombie process. The process finishes and finds that the parent is not waiting. The zombie processes are finished for all practical purposes and do not reside in the memory, but they still have some kernel resources allocated to them and cannot be taken out of the system. All zombies and their live children are eventually adopted by the granddaddy, the systemd process, which removes them from the system. |

In the interest of brevity, and in keeping with the scope of this book, the other states that a Linux process can be in are not included in this discussion.

### 10.4 Execution of Shell Commands

A shell command can be internal (built in) or external. An internal/built-in command is one whose code is part of the shell process. Some of the commonly used internal commands are . (dot command), bg, cd, continue, echo, exec, exit, export, fg, jobs, pwd, read, readonly, return, set, shift, test, times, trap, umask, unset, and wait. An external command is one whose code is in a file; contents of the file can be binary code or a shell script. Some of the commonly used external commands are grep, more, cat, mkdir, rmdir, ls, sort, ftp, telnet, lp, and ps. A shell creates a new process to execute a command. While the command process executes, the shell waits for it to finish. In this section, we describe how a shell (or any process) creates another process and executes external commands. You can use the type command to determine whether your command is built in or external, as shown in the following session. Under Bash, you can also use the `-a` option of `type` to display all the locations of a command. Remember that if you created an alias for the `type` command in Chapter 2, Section 2.6, you will have to unalias it in order for the following session to work!

In the following session, you can see that the `bg` command is built in. The Bash shell may be invoked through an executable available in your file system structure as shown.

```
$ type bg
bg is a shell builtin
$ type -a bash
bash is /bin/bash
$
```

A Linux process can create another process by using the `fork()` system call, which creates an exact main memory copy of the original process (i.e., the process that calls `fork()`). Both processes continue execution, starting with the statement that follows the fork. The forking process is known as the parent process, and the created (forked) process is called the child process, as shown in Figure 10.2. Here, we show a Bash shell that has created a child process (another Bash). We discuss the use of `fork()` and other system calls needed for the creation of processes and interprocess communication in Chapters 15–16.
