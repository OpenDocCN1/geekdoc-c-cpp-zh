# Threads and Tasks

> Keep Calm and Carry On.
> – English slogan

# 42.1 Introduction

Concurrency – the execution of several tasks simultaneously – is widely used to improve throughput (by using several processors for a single computation) or to improve responsiveness (by allowing one part of a program to progress while another is waiting for a response).

The C++ standard support for concurrency is introduced in a tutorial manner in §5.3. This chapter and the previous one provide a more detailed and systematic view.
We call an activity potentially executed concurrently with other activities a task. A thread is the system-level representation of a computer’s facilities for executing a task. A thread can execute a task. A thread may share an address space with other threads. That is, all threads in a single address space can access the same memory locations. One of the central challenges of the programmer of a concurrent system is to make sure that threads access memory in a sensible manner.

# 42.2 Threads

A thread is an abstraction of the computer hardware’s notion of a computation. The C++ standard library threads are intended to map one-to-one with the operating system’s threads. We use threads when several tasks in a program need to progress concurrently. On a system with several processing units (“cores”), threads allows us to use those units. All threads work in the same address space. If you want hardware protection against data races, use some notion of a process. Stacks are not shared between threads, so local variables are not subject to data races, that is, unless you incautiously pass a pointer to a local variable to another thread. In particular, beware of by-reference context bindings in lambdas (§11.4.3). Deliberate and careful sharing of stack memory is useful and common, for example, we might pass sections of a local array to a parallel sort.

If a thread cannot proceed (e.g., because it has encountered a mutex owned by another thread), it is said to be blocked or asleep.

```
id
native_handle_type
thread t {};

thread t {t2};
thread t {f,args}; t.~thread();

t=move(t2) t.swap(t2) t.joinable()
```