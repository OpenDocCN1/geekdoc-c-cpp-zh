
## Interrupt Handlers

Two types of communication can occur between a CPU and the rest of the hardware. In the first type, the CPU can make a request to the hardware. In the second type, the hardware sends a request to the CPU for immediate processing. The second type of communication is known as interrupts. In Linux, hardware interrupts are called Interrupt Requests (IRQs). The two types of IRQs are as follows:

- **Short IRQ**—Takes a shorter time to service the request. During this phase, the machine will be in the blocked state with no other interrupts being handled.
- **Long IRQ**—Takes a longer time to service the request, but other interrupts may occur. It is always recommended to define a long IRQ.

If the CPU receives an interrupt, it stops its current task, saves the runtime parameters, registers the variables on the stack, and calls the interrupt handler. If the CPU is processing some important task, which cannot be aborted or stopped, then the similar set of activities is done once the current task completes its execution. This implies that the interrupt handler does not even allow certain things while the system receives the interrupt request because it is in the unknown state. The only available solution to this problem is to complete the current task execution, schedule the handling of the new interrupt request later (this is called the bottom half), and then return. The kernel then calls the bottom half as soon as possible to process the pending interrupt request. To implement this, we need to call `request_irq()` to get the interrupt handler called when the relevant IRQ is received. This function generally receives the IRQ number, the name of the function, flags, a name for `/proc/interrupts`, and a parameter to pass to the interrupt handler. The flags can include `SA_SHIRQ`, which shares the IRQ with other interrupt handlers, or `SA_INTERRUPT`, which is a fast interrupt. The function will succeed if and only if a handler does not already exist on the IRQ. We can start processing the request by communicating with the hardware and use `queue_work()` and `mark_bh(BH_IMMEDIATE)` to schedule the bottom half from the interrupt handler.

Let's now summarize the main points discussed in the chapter.

## Summary

In this chapter, we have learned about the Linux operating system. Next, we have learned about the kernel modules. Further, the chapter has discussed the character device files, device drivers, and system calls. Finally, we have learned about task scheduling and interrupt handlers, in brief.

## Quick Revise

### Multiple Choice Questions

- **Q1.** A program running in the user mode can issue a system call.
  - a. True
  - b. False

- **Q2.** To register a character device, we need to pass both the major and minor numbers of a device.
  - a. True
  - b. False

- **Q3.** Which of the following features are supported by Linux kernel?
  - a. Supports dynamic loading of modules
  - b. Supports preemptive interrupt processing
  - c. Differentiates between a normal thread and a process
  - d. Supports the Symmetric Multiprocessor architecture

- **Q4.** The init_module call from the Linux kernel module returns a non-zero value on success.
  - a. True
  - b. False

### Subjective Questions

1. What are kernel modules? How are they different from C user-space programs?
2. What happens when a user-space process makes a system call?
3. What is the difference between a user space and a kernel space?
4. What is the normal return value of a kernel module? What if something else is returned from the kernel module?
5. Write a Linux kernel module spanning over five different C program files, compile it, and run it.
6. What are character devices? Why are they required?
7. What are ioctls? Why are they used?
8. What are monolithic kernels?
9. What is microkernel? How is it different from monolithic kernel?
10. What are the properties of Linux kernel that make it different from other UNIX variants?

![](img/43c5f409f9b17790a628c4b4df854b61_290_0.png)

## 10

## Parallel Programming in C

| If you need information on: | See page: |
|---|---|
| POSIX Threads | 250 |
| Thread Programming using the POSIX Library | 250 |
| Cleanup Handlers | 259 |
| Synchronization Problem | 261 |
| Mutex | 262 |
| Semaphore | 266 |
| Conditional Variables | 271 |
| Deadlocks | 273 |

Generally, for any computation, we break down a program into segments and execute each segment one after another. This idea is simple and good if we are using the old technology paradigm. However, with the technological advancements where the CPU's power and memory have grown over 1000 folds, we cannot afford to keep the CPU idle by executing the programs in a sequential manner. This is because lots of CPU cycles are wasted due to its underutilization. Therefore, a certain amount of parallelism is necessary to incorporate in the programs.

In programming, parallelism is achieved by the usage of threads, which are known as lightweight processes. Threads share the same address and the data space within a process. Generally, we can create more than one thread for a single process to make the execution faster by assigning different tasks to each thread. However, as multiple threads share the same address and data space among each other, chances of data corruption are also high for multithreaded programs. Data corruption might result in an operation where one thread is updating a frequently used variable and the other is reading from it at the same time. To protect such scenarios, we need to implement the concepts of mutex and semaphores in the programs.

In this chapter, we first learn about the POSIX threads. Then, we learn about the basics of thread programming using the POSIX library including thread attributes, thread cancellations, and modes. Next, the chapter discusses cleanup handlers and the synchronization problems faced in thread programming. Moreover, we learn about mutexes, semaphores, conditional variables, and deadlocks.

Let's start the chapter by discussing POSIX threads.

## POSIX Threads

POSIX threads or pthreads are a POSIX standard for threads. POSIX stands for Portable Operating System Interface. It is a family of standards specified by the Institute of Electrical and Electronics Engineers (IEEE) and designated as IEEE 1003.1c. POSIX defines the command line shells, utility interfaces, and Application Programming Interfaces (APIs) for software compatibility with the operating systems. These implementations are also available for POSIX-compliant operating systems, such as FreeBSD, NetBSD, GNU/Linux, Mac OS X, and Solaris.

POSIX standard defines a set of C programming language types, functions, and constants that cover the following features:

- Thread Management
- Mutex
- Conditional Variables

The pthread library is known as `libpthread` and is used while compiling the programs on the UNIX systems. All the pthread prototypes, structures, and definitions are present in the `pthread.h` file. Moreover, all the pthread constructs have the `pthread_` prefix. However, POSIX semaphores are prefixed with `sem_`, as they are not part of the pthread standard.

Now, let's write some programs in C using the POSIX library.

## Thread Programming using the POSIX Library

Let's write a program where a main thread creates a child thread and both the threads execute in parallel. However, before writing the program using the pthread library, we should remember the following guidelines:

- Always include the `<pthread.h>` header in the programs
- While compiling the programs, always link them with the pthread library using `-lpthread`
- Do not assign separate process ID to each thread

Now, consider the following program:

```c
/* thread1.c - Demonstrating thread creation using C */
#include <stdio.h>
#include <string.h>
#include <pthread.h>

struct thread_args {
        char name[20];
        int          count;
};

void *thread_function(void *arg);
int main ()
{
        int             local_counter = 1000;
        int             ret           = 0;
        pthread_t       thread;
        struct thread_args    params;

        strcpy(params.name, "I'm thread");
        params.count = 10000;

        ret = pthread_create(&thread, NULL, thread_function, (void*)&params);
        if (ret != 0) {
                fprintf(stderr, "\nThread creation failed\n");
                return 1;
        }
        printf("Output:\n");
        while (local_counter) {
                printf("C in main\n");
                local_counter--;
        }
        return 0;
}

void *thread_function(void *arg)
{
        struct thread_args  *params = (struct thread_args*)arg;

        while (params->count) {
                printf("%s\n", params->name);
                params->count--;
        }
}
```

The preceding program has a user-defined structure known as `thread_args`, which has a character array and an integer count as its members. In the `main()` function, we have defined a variable of type `pthread_t` and made a call to `pthread_create()`.

The `pthread_create()` API starts a new thread in the calling process. Therefore, this API should be used for thread creation. The signature of the `pthread_create()` API is as follows:

```c
int pthread_create (pthread_t                 *thread,
                    const pthread_attr_t       *attr,
                    void * (* start_routine) (void *),
                    void                      *arg);
```
