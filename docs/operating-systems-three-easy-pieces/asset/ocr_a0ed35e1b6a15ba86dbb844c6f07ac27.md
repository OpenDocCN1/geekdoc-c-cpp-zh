# CONCURRENCY: AN INTRODUCTION

# 26.4 The Heart Of The Problem: Uncontrolled Scheduling

To understand why this happens, we must understand the code sequence that the compiler generates for the update to counter. In this case, we wish to add a number (1) to counter. Thus, the code sequence for doing so might look like this (in x86):

```
mov 0x8049ac, %eax
add $0x1, %eax
mov %eax, 0x8049ac
```

This example assumes that the counter is located at address 0x80491c. In this three-instruction sequence, the x86 mov instruction is used to get the value at the address and put it into register eax. Then, the add is performed, adding 1(1) to the contents of the eax register, and finally, the contents of eax are stored back into memory at the same address.

Let us imagine one of our threads (Thread 1) enters this region of code, and is about to increment counter by one. It loads the value of counter(let's say 50 to begin) into its register eax. eax=50 for Thread 1. Then it adds one to the register; thus eax=51. Now, something unfortunate: a timer interrupt goes off; the OS saves the state of the currently running thread (it PC, its registers including etc.) to the thread's TCB.

Now worse happens: Thread 2 starts to run, and enters this piece of code. It executes the first instruction, incrementing the value of counter and putting it into its eax (memory: each thread when running has its private registers; the registers are virtualized by the context-switch that saves and restores them). The value of counter is still 50 at this point, and Thread 2 executes the next two instructions, incrementing by 1 (thus eax=51), and then saves the contents of eax into counter (address 0x80491c). Thus, the global variable counter now has the value 51.

Finally, another context switch occurs, and Thread 1 resumes running. Recall that it executed the mov and add, and is now about to perform the mov instruction. Recall also that eax=51. Thus, the mov instruction executes, saves the value to memory; the counter is set to 51.

Put simply what has happened is this: the code to increment counter has run twice, but counter, which started at 50, is now only equal to 51. A "correct" version of this program should have resulted in the variable counter equal to 52.

Let's look at a detailed execution to understand the problem before. Assume, for this example, that the above code is loaded at address 100 in memory, like the following sequence (note for those of you used to be nice, RISC-like instructions: x86 has variable-length instructions; this mov takes up 5 bytes of memory, and the add only 3):