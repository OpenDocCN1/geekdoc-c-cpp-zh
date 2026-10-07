
# main
Thread 1 Thread 2

starts running
prints “main: begin"
creates Thread 1
creates Thread 2

runs
prints “B"
returns

waits for T1
runs
prints “A"
returns

waits for T2
returns immediately; T2 is done
prints “main: end”

Figure 26.5: Thread Trace (3)

## 26.3 Why It Gets Worse: Shared Data

The simple example we showed above was useful in showing how threads are created and how they can run in different orders depending on how the scheduler decides to run them. It doesn't show you, though, how threads interact when they access shared data.

Let us imagine a simple example where two threads wish to update a global shared variable. The code we'll see is in Figure 26.4 (page 309). Here are a few notes about the code. First, as Stevens [SR05], we wrap the thread creation and join routines to simply exit or at least notice an error on failure for a program as simple as ours. Thus `pthread_create()` simply makes the return code is 0; if not, `pthread_create()` just prints a message and exits.

Second, instead of using two separate functions for the worker threads, we use a single piece of code, and pass the thread argument (in this case, a string) so we can have each print a different letter before it finishes.

Finally, and most importantly, we can now look at what each thread is trying to do: add a number to the shared variable counter, and so on for 10 million times (in a loop). The desired final result is: 20,000,000.

We now compile and run the program, to see how it behaves. Some times, everything works we might expect:

```
gcc -o main main.c -Wall -pthread; ./main
main: begin (counter = 0)
A: begin
B: begin
A: done
B: done
main: done with both (counter = 20000000)
```

# CONCURRENCY: AN INTRODUCTION

```c
#include <stdio.h>
#include <thread.h>
#include <common.h>
#include <common_threads.h>
static volatile int counter = 0;

// mythread())
// Simply adds 1 to counter repeatedly, in a loop
// No, this is not how you would add 10,000 to
// a counter, but it also shows the problem nicely.

void mythread(void *arg) {
    printf("%s: begin\n", (char *) arg);
    int i;
    for (i = 0; i < 10000; i++) {
        counter = counter + 1;
    }
    printf("%s: done\n", (char *) arg);
    return NULL;
}

void main () {
// Just launches two threads (pthread_create)
// and then waits for them (pthread_join)

int main(int argc, char *argv[]) {
    printf("main: begin (counter = %d\n", counter);
    pthread_create(&p1, NULL, mythread, "A");
    pthread_create(&p2, NULL, mythread, "B");

// join waits for the threads to finish
    pthread_join(p1, NULL);
    pthread_join(p2, NULL);
    printf("main: done with both (counter = %d\n", counter);
    return 0;
}
```

Figure 26.6: Sharing Data: Uh Oh (t1.c)

# CONCURRENCY: AN INTRODUCTION

Unfortunately, when we run this code, even on a single processor, we
don't necessarily get the desired result. Sometimes, we get:

```
prompt> ./main
main: begin (counter = 0)
A: begin
B: begin
A: done
B: done
main: done with both (counter = 19345221)
```

Let's try it one more time, just to see if we've gone crazy. After all,
aren't computers supposed to produce deterministic results, as you have
been taught?! Perhaps your professors have been lying to you? (gasp)

```
prompt> ./main
main: begin (counter = 0)
A: begin
B: begin
A: done
B: done
main: done with both (counter = 19221041)
```

Not is only each wrong, but also yields a different result! A big
question remains: why does this happen?

> TIP: KNOW AND USE YOUR TOOLS

> You should always learn new tools that help you write, debug, and understand computer systems. Here, we use a neat tool called a disassembler. When you run a disassembler on an executable, it shows you what
assembly instructions make up the program. For example, if we wish
to understand the low-level code to update a counter (in our example),
we run objdump (Linux) to see the assembly code:
prompt> objdump -d main

Doing produces a long listing of all the instructions in the program,
nearly labeled (particularly if you compiled with the -g flag), which includes symbols in the program. The objdump program is just
of many tools you should learn how to use; a debugger like gdb,
memory profilers like valgrind or purify, and those of the compiler
itself are others that you should spend time to learn more about; the better
you are at using your tools, the best systems you'll be able to build.

## 26.4 The Heart Of The Problem: Uncontrolled Scheduling

To understand why this happens, we must understand the code sequence that the compiler generates for the update to counter. In this case, we wish to add a number (1) to counter. Thus, the code sequence for doing so might look like this (in x86):

```
mov 0x8049ac, %eax
add $0x1, %eax
mov %eax, 0x8049ac
```

This example assumes that the counter is located at address 0x80491c. In this three-instruction sequence, the x86 mov instruction is used to get the value at the address and put it into register eax. Then, the add is performed, adding 1 to the contents of the eax register, and finally, the contents of eax are stored back into memory at the same address.

Let us imagine one of our threads (Thread 1) enters this region of code, and is about to increment counter by one. It loads the value of counter (let's say 50 to begin) into its register eax. eax=50 for Thread 1. Then it adds one to the register; thus eax=51. Now, something unfortunate: a timer interrupt goes off; the OS saves the state of the currently running thread (it PC, its registers including etc.) to the thread's TCB.

Now worse happens: Thread 2 starts to run, and enters this piece of code. It executes the first instruction, incrementing the value of counter and putting it into its eax (memory: each thread when running has its private registers; the registers are virtualized by the context-switch that saves and restores them). The value of counter is still 50 at this point, and Thread 2 executes the next two instructions, incrementing by 1 (thus eax=51), and then saves the contents of eax into counter (address 0x80491c). Thus, the global variable counter now has 51.
