# main
Thread 1 Thread2

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

# 26.3 Why It Gets Worse: Shared Data

The simple example we showed above was useful in showing how threads are created and how they can run in different orders depending on how the scheduler decides to run them. It doesn't show you, though, how threads interact when they access shared data.

Let us imagine a simple example where two threads wish to update a global shared variable. The code we'll see is in Figure 26.4 (page 309). Here are a few notes about the code. First, as Stevens [SR05], we wrap the thread creation and join routines to simply exit or at least notice an error on failure for a program as simple as ours. Thus `Pthread_create()` simply makes the return code is 0; if not, `Pthread_create()` just prints a message and exits.

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