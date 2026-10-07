# 8 INTRODUCTION TO OPERATING SYSTEMS

```
prompt> ./mem &; ./mem &\n[1] 24113
[2] 24114
[24113] address pointed to p: 0x200000
[24114] address pointed to p: 0x200000
[24113] p: 1
[24114] p: 1
[24114] p: 2
[24113] p: 2
[24113] p: 3
[24114] p: 3
[24113] p: 4
[24114] p: 4
...
```

Figure 2: Running The Memory Program Multiple Times

The program does a couple of things. First, it allocates some memory (line a1). Then, puts the address of the memory (a2), and then puts the number into the first slot of the newly allocated memory (a3). Finally, it loops, delaying for a second and incrementing the value stored at the address held in p. With every print statement, it also prints what is called the process identifier (PID) of the running program. This PID is unique per running process.

Again, this result is not too interesting. The newly allocated memory is at address 0x200000. As the program runs, it slowly updates the value and prints out the result.

Now, we run multiple instances of this program to see what happens (Figure 2.4). We see that each running program has allocated memory at the same address (0x200000), and yet each seems to be updating the value at 0x200000 independently! It is as if each running program has its own private memory, instead of sharing the physical memory with other running programs.

Indeed, that is what is happening here as the OS is virtualizing memory. Each process accesses its own private virtual address space (sometimes called its address space), which the OS somehow maps onto the physical memory of the machine. A memory reference within one running program does not affect the address space of other processes (or the OS itself); as far as the program is concerned, it has physical memory to all. The reality, however, is that physical memory is a shared resource, managed by the operating system. Exactly how all of this is accomplished is the subject of the first part of this book, on the topic of virtualization.

> For this example to work, you need to make sure address-space randomization is disabled; randomization, as it turns out, can be a good defense against ciertos kinds of security flaws. Read more about it on you, especially if you want to learn how to break into computer systems using stack-smashing attacks. Not that we would recommend such a thing...

OPERATING SYSTEMS [Version 1.01]

WWW.OSTEP.ORG