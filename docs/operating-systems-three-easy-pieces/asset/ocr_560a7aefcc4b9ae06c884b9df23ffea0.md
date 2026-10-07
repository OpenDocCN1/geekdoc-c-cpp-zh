# OS
Program

Create entry for process list
Allocate memory for program
Load program into memory
Set up stack with argc/argv
Clear registers
Execute call main()

```
Run main()
Execute return from main
```

Free memory of process
Remove from process list

![](bbox=[0.277, 0.329, 0.723, 0.345])

to it, and running the user's code. Figure 6.1 shows this basic direct execution protocol (without any limits, yet), using a normal call and return to jump to the program's main() and later back to the kernel.\ Sounds simple, no? But this approach gives rise to a few problems in our quest to virtual the CPU. The first is simple: if we just run a program, how can the OS sure the program doesn't do anything we don't want it to, while still running it efficiently? The second: when we are running and switching to another process, how does the operating system stop it from running and switching to another process, thus implementing the time sharing we require to virtualize the CPU?
in answering these questions, we'll get a much better sense of what is needed to virtualize the CPU. In developing these techniques, we'll also see where the "limited" part of the name arises from; without limits on running programs, the OS wouldn't be in control of anything and would be "just a library" — a very sad state of affairs for an aspiring operating system!

# 6.2 Problem #1: Restricted Operations

Direct execution has the obvious advantage of being fast; the program runs natively on the hardware CPU and executes as quickly as one would expect. But running on the CPU introduces a problem: what if the process wishes to perform some kind of restricted operation, such as issuing an I/O request to a disk, or gaining access to more system resources as CPU or memory?

> THE CRUX: HOW TO PERFORM RESTRICTED OPERATIONS
A process must be able to perform I/O and some other restricted operations, but without giving the process complete control over the system. How can the OS and hardware work together to do so?