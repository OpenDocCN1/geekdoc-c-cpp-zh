
- **module name**—The name specified in a module’s module declaration. All module units in a given module must have the same module name.
- **module partition**—A module unit in which the module declaration specifies the module name followed by a colon and a partition name. Module partition names in the same named module must be unique. If a module partition is a module interface partition, it must be exported by the module’s primary interface unit.
- **module purview**—The set of identifiers within a module unit from the module declaration to the end of the translation unit.
- **module unit**—An implementation unit containing a module declaration.
- **named module**—All module units with the same module name.
- **named module purview**—The purviews of all the module units in the named module.
- **namespace**—Defines a scope in which identifiers and variables are placed to help prevent naming conflicts with identifiers in your own programs and libraries.
- **partition**—A kind of module unit that defines a portion of a module’s interface or implementation. Partitions are not visible to translation units that import the module.
- **precompiled module interface (.pcm)**—A clang++ file that contains information about a module’s interface. Used when compiling other translation units that depend on a given module.
- **primary module interface unit**—Determines the set of declarations exported by a module for use in other translation units.
- **:private module fragment**—A section in a primary module interface unit that enables you to define a module’s implementation in the same file as its interface without exposing the implementation to other translation units.
- **reachable declaration**—A declaration is reachable if you can use it in your code without referencing it directly. For example, if you import a module into a translation unit and one of the module’s exported functions returns an object of a non-exported type, that type is reachable in importing translation units.
- **translation unit**—A preprocessed source-code file that is ready to be compiled.
- **visible declaration**—A declaration you can use by name in your code. For example, if you import a module into a translation unit, the module’s exported declarations are visible in that translation unit.

*This page intentionally left blank*

## Parallel Algorithms and Concurrency: A High-Level View

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1045_0.png)

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1045_1.png)

### Objectives

In this chapter, you'll:

- Understand concurrency, parallelism and multithreading.
- Use high-level concurrency features such as parallel algorithms and C++20 latches and barriers.
- Understand the thread life cycle.
- Use the `<chrono>` header’s timing features to profile sequential and parallel algorithm performance on multi-core systems.
- Implement correct producer–consumer relationships.
- Synchronize access to shared mutable data by multiple threads using `std::mutex`, `std::lock_guard`, `std::condition_variable` and `std::unique_lock`.
- Use `std::async` and `std::future` to execute long calculations asynchronously and get their results.
- Use other C++20 concurrency features, such as semaphores and enhanced atomics.
- Learn about possible future concurrency features.

### Outline

- **17.1** Introduction
- **17.2** Standard Library Parallel Algorithms
  - 17.2.1 Example: Profiling Sequential and Parallel Sorting Algorithms
  - 17.2.2 When to Use Parallel Algorithms
  - 17.2.3 Execution Policies
  - 17.2.4 Example: Profiling Parallel and Vectorized Operations
  - 17.2.5 Additional Parallel Algorithm Notes
- **17.3** Multithreaded Programming
  - 17.3.1 Thread States and the Thread Life Cycle
  - 17.3.2 Deadlock and Indefinite Postponement
- **17.4** Launching Tasks with `std::jthread`
  - 17.4.1 Defining a Task to Perform in a Thread
  - 17.4.2 Executing a Task in a `jthread`
  - 17.4.3 How `jthread` Fixes Threads
- **17.5** Producer–Consumer Relationship: A First Attempt
- **17.6** Producer–Consumer: Synchronizing Access to Shared Mutable Data
  - 17.6.1 Class `SynchronizedBuffer`: Mutexes, Locks and Condition Variables
  - 17.6.2 Testing `SynchronizedBuffer`
- **17.7** Producer–Consumer: Minimizing Waits with a Circular Buffer
- **17.8** Readers and Writers
- **17.9** Cooperatively Canceling `jthreads`
- **17.10** Launching Tasks with `std::async`
- **17.11** Thread-Safe, One-Time Initialization
- **17.12** A Brief Introduction to Atomics
- **17.13** Coordinating Threads with C++20 Latches and Barriers
  - 17.13.1 C++20 `std::latch`
  - 17.13.2 C++20 `std::barrier`
- **17.14** C++20 Semaphores
- **17.15** C++23: A Look to the Future of C++ Concurrency
  - 17.15.1 Parallel Ranges Algorithms
  - 17.15.2 Concurrent Containers
  - 17.15.3 Other Concurrency-Related Proposals
- **17.16** Wrap-Up

### 17.1 Introduction

It would be nice if we could focus our attention on performing only one task at a time and doing it well. That can be difficult to do in a complex world where so much is happening at once. This chapter presents C++’s features for building applications that create and manage multiple tasks. This can significantly improve program performance and responsiveness.

#### Sequential, Concurrent and Parallel Operation of Multiple Tasks

When we say that two tasks operate sequentially, we mean they operate one after the other “in sequence.” When we say that two tasks are operating concurrently, we mean that they’re both making progress, possibly in small increments and not necessarily simultaneously.

Let’s clarify that. Until the early 2000s, most computers had only a single processor. Operating systems on such computers execute tasks concurrently by rapidly switching between them, doing a portion of each task before moving on to the next so that all tasks keep progressing. For example, it’s common for personal computers to concurrently perform cloud backups, compile a program, send a file to a printer, send and receive email messages and tweets, stream video and audio, download files, and more.

When we say that two tasks operate in parallel, we mean they’re truly executing simultaneously. In this sense, parallelism is a subset of concurrency. The human body performs a great variety of operations in parallel. Respiration, blood circulation, digestion, thinking and walking, for example, can occur in parallel, as can all the senses—sight, hearing, touch, smell and taste. It’s believed that this parallelism is possible because the human brain is thought to contain billions of “processors.” Today’s multi-core computers have multiple processors that can perform tasks in parallel.

#### C++ Concurrency

C++ makes concurrency available to you through the language and standard libraries. Threads of execution are what happen concurrently in a program. According to the C++ standard, "a thread of execution (also known as a thread) is a single flow of control within a program, including the initial invocation of a specific top-level function, and recursively including every function invocation subsequently executed by the thread."^1

Programs can have **multiple threads of execution**, each with its own function-call stack and program counter, allowing it to execute concurrently with other threads. All the threads in a given program can share application-wide resources, such as memory and files. This capability is called multithreading.

A problem with **single-threaded applications** that can lead to poor responsiveness is that lengthy activities must complete before others can begin. In a **multithreaded application**, threads can be distributed across multiple cores (if available), enabling tasks to truly execute in parallel, and the application can operate more efficiently.

Multithreading also can enhance performance on single-processor systems. When one thread cannot proceed (because, for example, it's waiting for the result of an I/O operation), another can use the processor.

#### A Concurrent Programming Use Case: Video Streaming

We'll discuss various concurrent programming applications. For example, when streaming video over the Internet, the user may not want to wait until a lengthy video finishes downloading before starting playback. Multiple threads can be used to solve this problem. One downloads the video a "chunk" at a time (we'll refer to this thread as a **producer**), and another plays it (we'll refer to this thread as a **consumer**). These activities can proceed concurrently. The threads are synchronized to avoid choppy playback. **Their actions are coordinated** so that the player thread doesn't begin until a sufficient portion of the video is in memory to keep the player proceeding smoothly. Producer and consumer threads **share data**. We'll show how to synchronize threads to ensure correct execution. In the case of video streaming, synchronizing threads ensures smooth viewing, even though only a portion of the video might be in memory at once.

#### Thread Safety

When threads share mutable (modifiable) data, you must ensure that they do not corrupt it, which is known as making the code thread-safe. Thread safety approaches include:^2

- **Immutable (constant) data**—A constant object is not modifiable, so any number of threads can access a constant object at once.
- **Mutual exclusion**—You can coordinate access to shared mutable data, allowing only one thread to access the data at a time.
- **Atomic types**—You can use low-level types that automatically ensure their operations are atomic (i.e., not interruptible), so only one thread can access and possibly modify the data at a time.
