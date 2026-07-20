![](images/title_page.png)

![Concurrency with Modern C++](images/title_page.png)

## Concurrency with Modern C++

### What every professional C++ programmer should know about concurrency.

#### Rainer Grimm

This book is for sale at [http://leanpub.com/concurrencywithmodernc](http://leanpub.com/concurrencywithmodernc)

This version was published on 2019-10-15

![publisher's logo](images/leanpub-logo.png)

*   *   *   *   *

This is a [Leanpub](http://leanpub.com) book. Leanpub empowers authors and publishers with the Lean Publishing process. [Lean Publishing](http://leanpub.com/manifesto) is the act of publishing an in-progress ebook using lightweight tools and many iterations to get reader feedback, pivot until you have the right book and build traction once you do.

*   *   *   *   *

© 2017 - 2019 Rainer Grimm

## Table of Contents

## Guide

1.  [Begin Reading](#chap00.xhtml)

## Reader Testimonials

**Bart Vandewoestyne**

![](images/Testimonials----BartVandewoestyne.jpg)

*Senior Development Engineer Software at Esterline*

```
 "'Concurrency with Modern C++' is your practical guide to getting
       familiar with concurrent programming in Modern C++.  Starting with the
       C++ Memory Model and using many ready-to-run code examples, the book
       covers a good deal of what you need to improve your C++ multithreading
       skills.  Next to the enlightening case studies that will bring you up
       to speed, the overview of upcoming concurrency features might even wet
       your appetite for more!" 
```

**Ian Reeve**

*Senior Storage Software Engineer for Dell Inc.*

```
 "Rainer Grimm's Concurrency with Modern C++ is a well written book 
       covering the theory and practice for working with concurrency per the 
       existing C++ standards, as well as addressing the potential changes 
       for the upcoming C++ 20 standard. He provides a conversational 
       discussion of the applications and best practices for concurrency along 
       with example code to reinforce the details of each topic. An informative 
       and worthwhile read!" 
```

**Robert Badea**

![](images/Testimonials----RobertBadea.jpg)

*Technical Team Leader*

```
 "Concurrency with Modern C++ is the easiest way to become an expert in 
       the multithreading environment. This book contains both simple and advanced 
       topics, and it has everything a developer needs, in order to become an 
       expert in this field: Lots of content, a big number of running code examples, 
       along with great explanation, and a whole chapter for pitfalls. I enjoyed 
       reading it, and I highly recommend it for everyone working with C++." 
```

## Introduction

Concurrency with Modern C++ is a journey through present and upcoming concurrency features in C++.

*   **C++11** and **C++14** have the basic building blocks for creating concurrent and parallel programs.
*   With **C++17** we have the parallel algorithms from the Standard Template Library (STL). That means that most STL based algorithms can be executed sequentially, parallel, or vectorised.
*   The concurrency story in C++ goes on. With **C++20/23** we can hope for extended futures, coroutines, transactions, and more.

This book explains the details of concurrency in modern C++ and gives you, also, many code examples. Therefore you can combine theory with practice to get the most out of it.

Because this book is about concurrency, I present many pitfalls and show you how to overcome them.

### Conventions

Only a few conventions.

#### Special Fonts

*Italic*: I use *Italic* to emphasise an expression.

**Bold**: I use **Bold** to emphasise even more.

`Monospace`: I use `Monospace` for code, instructions, keywords, and names of types, variables, functions, and classes.

#### Special Symbols

**⇒** stands for a conclusion in the mathematical sense. For example, a **⇒** b means if a then b.

#### Special Boxes

Boxes contain special information, tips, and warnings.

### Source Code

All source code examples are complete. That means, assuming you have a conforming compiler, you can compile and run them. The name of the source file is in the title of the listing. I use the `using namespace std` directive in the source files only if necessary.

#### Run the Programs

Compiling and running the examples is quite easy for the C++11 and C++14 examples in this book. Every modern C++ compiler should support them. For both the [GCC](https://gcc.gnu.org/) and the [clang](https://clang.llvm.org/) compiler, the C++ standard must be specified as well as the threading library to link against. For example the g++ compiler from GCC creates an executable program called `thread` with the following command-line: `g++ -std=c++14 -pthread thread.cpp -o thread`.

*   **-std=c++14**: use the language standard C++14
*   **-pthread**: add support for multithreading with the pthread library
*   **thread.cpp**: source file
*   **-o thread**: executable program

The same command-line works for the clang++ compiler. The Microsoft Visual Studio 17 C++ compiler supports C++14 as well.

If you have no modern C++ compiler at your disposal, there are a lot of online compilers available. Arne Mertz’ blog post [C++ Online Compiler](https://arne-mertz.de/2017/05/online-compilers/) gives an excellent overview.

With C++17 and C++20/23, the story becomes quite complicated. I installed the [HPX (High Performance ParalleX)](http://stellar.cct.lsu.edu/projects/hpx/) framework, which is a general purpose C++ runtime system for parallel and distributed applications of any scale. HPX has already implemented the [Parallel STL](#chap01.xhtml_chapterXXXChapterOOOSSSParallelSSSAlgorithmsSSSofSSStheSSSSTL) of C++17 and many of the [concurrency features of C++20/23](#chap01.xhtml_chapterXXXChapterOOOSSSTheSSSFutureOOOSSSCPPP20). Please refer to the corresponding sections in the chapter [The Future: C++20/23](#chap01.xhtml_chapterXXXChapterOOOSSSTheSSSFutureOOOSSSCPPP20) and read how you can see the code examples in action.

### How you should read the book?

If you are not very familiar with concurrency in C++, start at the very beginning with [A Quick Overview](#chap02.xhtml_PartXXXASSSQuickSSSOverview) to get the big picture.

Once you get the big picture, you can proceed with the [The Details](#chap04.xhtml_PartXXXTheSSSDetails). Skip the [memory model](#chap01.xhtml_chapterXXXChapterCCCMemorySSSModel) in your first iteration of the book, unless you are entirely sure that is what you are looking for. The chapter [Case Studies](#chap09.xhtml_chapterXXXCaseSSSStudies) should help you apply the theory, something that is sometimes quite challenging as it requires a basic understanding of the memory model.

The chapter [The Future: C++20/23](#chap01.xhtml_chapterXXXtheSSSfutureSSSCPPP20) is optional. I am very curious about the future. I hope you are too!

The last part, [Further Information](#chap19.xhtml_PartXXXFurtherSSSInformation) provides you additional guidance towards a better understanding of my book and getting the most out of it.

### Personal Notes

#### Acknowledgements

To write this book in English, I started a request in my English blog: [www.ModernesCpp.com](http://www.modernescpp.com/index.php/looking-for-proofreaders-for-my-new-book-concurrency-with-modern-c) and received a much higher response than I expected. About 50 people wanted to proofread my book. Special thanks to all of you, including my daughter Juliette, who improved my layout and my son Marius, who was the first proofreader.

Here are the names in alphabetic order: Nikos Athanasiou, Robert Badea, Joe Das, Jonas Devlieghere, Randy Hormann, Lasse Natvig, Erik Newton, Ian Reeve, Bart Vandewoestyne, Dafydd Walters, Andrzej Warzynski, and Enrico Zschemisch.

#### About Me

I’ve worked as a software architect, team lead and instructor for about 20 years. In my spare time, I enjoy writing articles on topics such as C++, Python and Haskell, and also enjoy speaking at conferences. In 2016 I decided to work for myself. I organise and lead seminars about modern C++ and Python.

#### My Special Circumstances

I began Concurrency With Modern C++ in Oberstdorf while getting a new hip joint. Formally, it was a total endoprosthesis of my left hip joint. I wrote the first half of this book during my stay in the clinic and the rehabilitation clinic. To be honest, writing a book helped me a lot during this challenging period.

![](images/signatur----RainerGrimmSmall.png)

# A Quick Overview

## Concurrency with Modern C++

With the publishing of the C++11 standard, C++ got a multithreading library and a memory model. This library has basic building blocks like atomic variables, threads, locks, and condition variables. That’s the foundation on which future C++ standards such as C++20 and C++23 can establish higher abstractions. However, C++11 already knows tasks, which provide a higher abstraction than the cited basic building blocks.

![Concurrency in C++](images/timeline----timeline.png)

Concurrency in C++

Roughly speaking, you can divide the concurrency story of C++ into three evolution steps.

### C++11 and C++14: The Foundation

Multithreading was introduced in C++11\. This support consists of two parts: A *well-defined* memory model, and a standardised threading interface. C++14 added reader-writer locks to the multithreading facilities of C++.

#### Memory Model

The foundation of multithreading is a *well-defined* [memory model](#chap05.xhtml_chapterXXXMemorySSSModel). This memory model has to deal with the following aspects:

*   Atomic operations: operations that can be performed without interruption.
*   Partial ordering of operations: a sequence of operations that must not be reordered.
*   Visible effects of operations: guarantees when operations on shared variables are visible in other threads.

The C++ memory model was inspired by its predecessor: the Java memory model. Unlike the Java memory model, however, C++ allows us to break the constraints of [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency), which is the default behaviour of atomic operations.

Sequential consistency provides two guarantees.

1.  The instructions of a program are executed in source code order.
2.  There is a global order for all operations on all threads.

The memory model is based on atomic operations on atomic data types (short atomics).

##### Atomics

C++ has a set of simple [atomic data types](#chap05.xhtml_chapterXXXAtomics). These are booleans, characters, numbers and pointers in many variants. You can define your atomic data type with the class template `std::atomic`. Atomics establish synchronisation and ordering constraints that can also hold for non-atomic types.

The standardised threading interface is the core of concurrency in C++.

#### Multithreading

[Multithreading](#chap06.xhtml_chapterXXXMultithreading) in C++ consists of threads, synchronisation primitives for shared data, thread-local data and tasks.

##### Threads

A [`std::thread`](#chap06.xhtml_chapterXXXThreads) represents an independent unit of program execution. The executable unit, which is started immediately, receives its work package as a [callable unit](#chap03.xhtml_glossaryXXXCallableSSSUnitSSSSSSBOBOBOGlossaryBCBCBC). A callable unit can be a named function, a function object, or a lambda function.

The creator of a thread is responsible for its lifecycle. The executable unit of the new thread ends with the end of the callable. Either the creator waits until the created thread `t` is done (`t.join()`) or the creator detaches itself from the created thread: `t.detach()`. A thread `t` is *joinable* if no operation `t.join()` or `t.detach()` was performed on it. A *joinable* thread calls `std::terminate` in its destructor, and the program terminates.

A thread that is detached from its creator is typically called a daemon thread because it runs in the background.

A `std::thread` is a variadic template. This means that it can receive an arbitrary number of arguments; either the callable or the thread can get the arguments.

##### Shared Data

You have to coordinate access to a shared variable if more than one thread is using it at the same time and the variable is mutable (non-const). Reading and writing a shared variable at the same time is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) and therefore undefined behaviour. Coordinating access to a shared variable is achieved with mutexes and locks in C++.

###### Mutexes

A [mutex](#chap06.xhtml_chapterXXXMutexes) (*mutual exclusion*) guarantees that only one thread can access a shared variable at any given time. A mutex locks and unlocks the [critical section](#chap03.xhtml_glossaryXXXCriticalSSSSectionSSSSSSBOBOBOGlossaryBCBCBC), to which the shared variable belongs. C++ has five different mutexes. They can lock recursively, tentatively, and with or without time constraints. Even mutexes can share a lock at the same time.

###### Locks

You should encapsulate a mutex in a [lock](#chap06.xhtml_chapterXXXLocks) to release the mutex automatically. A lock implements the [RAII idiom](#chap03.xhtml_glossaryXXXRAIISSSSSSBOBOBOGlossaryBCBCBC) by binding a mutex’s lifetime to its own. C++ has a `std::lock_guard` / `std::scoped_lock` for the simple, and a `std::unique_lock` / `std::shared_lock` for the advanced use cases such as the explicit locking or unlocking of the mutex, respectively.

###### Thread-safe Initialisation of Data

If shared data is read-only, it’s sufficient to initialize it in a *thread-safe* way. C++ offers various ways to achieve this including using a [constant expression](#chap03.xhtml_chapterXXXConstantSSSexpressions), a [static variable with block scope](#chap06.xhtml_chapterXXXStaticSSSVariables), or using the function [`std::call_once` in combination with the flag `std::once_flag`](#chap06.xhtml_chapterXXXcall_onceZZZonce_flag).

##### Thread Local Data

Declaring a variable as [thread-local](#chap06.xhtml_chapterXXXThreadMMMLocalSSSData) ensures that each thread gets its own copy. Therefore, there is no shared variable. The lifetime of a thread-local data is bound to the lifetime of its thread.

##### Condition Variables

[Condition variables](#chap03.xhtml_chapterXXXConditionSSSVariables) enable threads to be synchronized via messages. One thread acts as the sender while the other one acts as the receiver of the message, where the receiver blocks waiting for the message from the sender. Typical use cases for condition variables are producer-consumer workflows. A condition variable can be either the sender or the receiver of the message. Using condition variables correctly is quite challenging; therefore, tasks are often the easier solution.

##### Tasks

[Tasks](#chap06.xhtml_chapterXXXTasks) have a lot in common with threads. While you explicitly create a thread, a task is just a job you start. The C++ runtime automatically handles, in the simple case of [`std::async`](#chap06.xhtml_chapterXXXasync), the lifetime of the task.

Tasks are like data channels between two communication endpoints. They enable thread-safe communication between threads. The promise as one endpoint puts data into the data channel, the future at the other endpoint picks the value up. The data can be a value, an exception, or simply a notification. In addition to `std::async`, C++ has the class templates [`std::promise`](#chap06.xhtml_chapterXXXpromise) and [`std::future`](#chap06.xhtml_chapterXXXfuture) that give you more control over the task.

### C++17: Parallel Algorithms of the Standard Template Library

![Parallel algorithms in C++17](images/timeline----timeline17.png)

Parallel algorithms in C++17

With C++17, concurrency in C++ has drastically changed, in particular the [parallel algorithms of the Standard Template Library (STL)](#chap07.xhtml_chapterXXXParallelSSSAlgorithmsSSSofSSStheSSSSTL). C++11 and C++14 only provide the basic building blocks for concurrency. These tools are suitable for a library or framework developer but not for the application developer. Multithreading in C++11 and C++14 becomes an assembly language for concurrency in C++17!

#### Execution Policy

With C++17, most of the STL algorithms are available in a parallel implementation. This makes it possible for you to invoke an algorithm with a so-called [execution policy](#chap03.xhtml_chapterXXXExecutionSSSPolicies). This policy specifies whether the algorithm runs sequentially (`std::execution::seq`), in parallel (`std::execution::par`), or in parallel with additional vectorisation (`std::execution::par_unseq`).

#### New Algorithms

In addition to the 69 algorithms that are available in overloaded versions for parallel, or parallel and vectorised execution, we get [eight additional algorithms](#chap03.xhtml_chapterXXXNewSSSAlgorithms). These new ones are well suited for parallel reducing, scanning, or transforming.

### The Near Future: C++20

![Concurrency in C++20](images/timeline----timeline20.png)

Concurrency in C++20

In June 2019, the C++20 standard is worked out. Here are the features, we will get.

#### `std::jthread`

`std::jthread` is a enhanced replacement for `std::thread`. In addition to `std::thread`, a `std::jthread` can signal an interrupt and can automatically join the started thread.

#### Atomic Smart Pointers

The smart pointer [`std::shared_ptr`](http://en.cppreference.com/w/cpp/memory/shared_ptr) and [`std::weak_ptr`](http://en.cppreference.com/w/cpp/memory/weak_ptr) have a conceptional issue in concurrent programs. They share intrinsically mutable state; therefore, they are prone to data races and thus, leading to undefined behaviour. `std::shared_ptr` and `std::weak_ptr` guarantee that the incrementing or decrementing of the reference counter is an atomic operation and the resource is deleted exactly once, but neither of them can guarantee that the access to its resource is atomic. The new atomic smart pointers [`std::atomic<std::shared_ptr<T>>`](#chap03.xhtml_chapterXXXatomic_shared_ptrZZZatomic_weak_ptr) and [`std::atomic<std::weak_ptr<T>>`](#chap03.xhtml_chapterXXXatomic_shared_ptrZZZatomic_weak_ptr) solve this issue. Both are partial template specialisations of [`std::atomic`](#chap05.xhtml_chapterXXXAtomics).

#### Latches and Barriers

C++14 has no semaphores. Semaphores are used to control access to a limited number of resources. Worry no longer, because C++20 gets [latches and barriers](#chap08.xhtml_chapterXXXLatchesSSSandSSSBarriers). You can use latches and barriers for waiting at a synchronisation point until the counter becomes zero. The difference between latches and barriers is that a `std::latch` can only be used once while a `std::barrier` can be used more than once. Additionally, a `std::barrier` can adjust its counter after each iteration.

#### Semaphores

A [counting semaphore](#chap08.xhtml_chapterXXXSemaphores) is a special semaphore which has a counter that is bigger than zero. The counter is initialised when the semaphore is created. Acquiring the semaphore decreases the counter and releasing the semaphore increases the counter.

#### Coroutines

[Coroutines](#chap08.xhtml_chapterXXXCoroutines) are functions that can suspend and resume their execution while maintaining their state. Coroutines are often the preferred approach to implement cooperative multitasking in operating systems, event loops, infinite lists, or pipelines.

### Case Studies

After presenting the theory of the memory model and the multithreading interface, I apply the theory in a few [case studies](#chap09.xhtml_chapterXXXCaseSSSStudies).

#### Calculating the Sum of a Vector

[Calculating the sum of an vector](#chap09.xhtml_chapterXXXCalculatingSSStheSSSSumSSSofSSSaSSSVector) can be done in various ways. You can do it sequentially, or concurrently with maximum and minimum sharing of data. The performance numbers differ drastically.

#### Thread-Safe Initialisation of a Singleton

[Thread-safe initialisation of a singleton](#chap09.xhtml_chapterXXXThreadMMMSafeSSSInitialisationSSSofSSSaSSSSingelton) is the classical use-case for thread-safe initialisation of a shared variable. There are many ways to do it, with varying performance characteristics.

#### Ongoing Optimisation with CppMem

I start with a small program and successively improve it. I verify each step of my process of [ongoing optimisation with CppMem](#chap09.xhtml_chapterXXXOngoingSSSOptimisationXXXWithSSSCppMem). [CppMem](http://svr-pes20-cppmem.cl.cam.ac.uk/cppmem/) is an interactive tool for exploring the behaviour of small code snippets using the C++ memory model.

### The Future: C++23

![Concurrency in C++20](images/timeline----timeline23.png)

Concurrency in C++20

It is difficult to make predictions, especially about the future ([Niels Bohr](https://en.wikipedia.org/wiki/Niels_Bohr)).

#### Executors

An executor consists of a set of rules about where, when and how to run a [callable unit](#chap03.xhtml_glossaryXXXCallableSSSUnitSSSBOBOBOGlossaryBCBCBC). They are the basic building block to execute and specify if callables should run on an arbitrary thread, a thread pool, or even single threaded without concurrency. The [extended futures](#chap10.xhtml_chapterXXXExtendedSSSFutures), the extensions for networking [N4734](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/n4734.pdf) depend on them but also the [parallel algorithms of the STL](#chap07.xhtml_chapterXXXParallelSSSAlgorithmsSSSofSSStheSSSSTL), and the new concurrency features in C++20/23 such as latches and barriers, coroutines, transactional memory, and task blocks eventually use them.

#### Extended futures

Tasks called promises and futures, introduced in C++11, have a lot to offer, but they also have a drawback: tasks are not composable into powerful workflows. That limitation does not hold for the [extended futures](#chap10.xhtml_chapterXXXExtendedSSSFutures) in C++20/23\. Therefore, an extended future becomes ready, when its predecessor (`then`) becomes ready, `when_any` one of its predecessors becomes ready, or `when_all` of its predecessors become ready.

#### Transactional Memory

The [transactional memory](#chap10.xhtml_chapterXXXTransactionalSSSMemory) is based on the ideas underlying transactions in database theory. A transaction is an action that provides the first three properties of ACID database transactions: **A**tomicity, **C**onsistency, and **I**solation. The durability that is characteristic for databases holds not for the proposed transactional memory in C++. The new standard has transactional memory in two flavours: synchronised blocks and atomic blocks. Both are executed in [total order](#chap03.xhtml_glossaryXXXtotalSSSorderSSSSSSBOBOBOGlossaryBCBCBC) and behave as if a global lock protected them. In contrast to synchronised blocks, atomic blocks cannot execute transaction-unsafe code.

#### Task Blocks

[Task Blocks](#chap10.xhtml_chapterXXXTaskSSSBlocks) implement the fork-join paradigm in C++. The following graph illustrates the key idea of a task block: you have a fork phase in which you launch tasks and a join phase in which you synchronise them.

![Task Blocks](images/cpp20_23----ForkJoin.png)

Task Blocks

#### Data-Parallel Vector Library

[The data-parallel vector library](#chap10.xhtml_chapterXXXData-ParallelSSSVectorSSSLibrary) provides data-parallel (SIMD) programming via vector types. SIMD means that one operation is performed on many data in parallel.

### Patterns and Best Practices

[Patterns](#chap03.xhtml_chapterXXXPatterns) are documented best practices from the best. They “… express a relation between a certain context, a problem, and a solution.” [Christopher Alexander](https://en.wikipedia.org/wiki/Christopher_Alexander). Thinking about the challenges of concurrent programming from a more conceptional point of view provides many benefits. In contrast to the more conceptional patterns to concurrency, provides the chapter best practices pragmatic tips to overcome the concurrency challenges.

#### Synchronisation

A necessary prerequisite for a [data races](#chap20.xhtml_chapterXXXDataSSSRaces) is shared, mutable state. [Synchronisation patterns](#chap13.xhtml_chapterXXXSynchronisationSSSPatterns) boil down to two concerns: [dealing with sharing](#chap13.xhtml_chapterXXXDealSSSwithSSSSharing) and [dealing with mutation](#chap13.xhtml_chapterXXXDealingSSSwithSSSMutation).

#### Concurrent Architecture

The chapter to [concurrent architecture](#chap14.xhtml_chapterXXXConcurrentSSSArchitectur) presents three patterns. The two patterns [Active Object](#chap14.xhtml_chapterXXXActiveSSSObject) and the [Monitor Object](#chap14.xhtml_chapterXXXMonitorSSSObject) sychronise and schedulte method invocation. The third pattern [Half-Sync/Half-Async](#chap03.xhtml_chapterXXXHalf-Sync/Half-Async) has an architectural focus and decouples asynchronous and synchronous service processing in concurrent systems.

#### Best Practices

Concurrent programming is inherently complicated, therefore having [best practices](#chap15.xhtml_chapterXXXBestSSSPractices) in [general](#chap15.xhtml_chapterXXXGeneralSSSBOBOBOBestSSSPracticesBCBCBC), but also for [multithreading](#chap15.xhtml_chapterXXXMultithreadingSSSBOBOBOBestSSSPracticesBCBCBC), and the [memory model](#chap15.xhtml_chapterXXXMemorySSSModelSSSBOBOBOBestSSSPracticesBCBCBC) makes a lot of sense.

### Data Structures

### Challenges

Writing concurrent programs is inherently complicated. This is particularly true if you only use C++11 and C++14 features. Therefore I describe in detail the most [challenging](#chap20.xhtml_chapterXXXChallenges) issues. I hope that if I dedicate a whole chapter to the challenges of concurrent programming, you become more aware of the pitfalls. I write about challenges such as [race conditions](#chap03.xhtml_chapterXXXRaceSSSConditions), [data races](#chap20.xhtml_chapterXXXDataSSSRaces), and [deadlocks](#chap20.xhtml_chapterXXXDeadlocks).

### Time Library

The [time library](#chap21.xhtml_chapterXXXTimeSSSLibrary) is a key component of the concurrent facilities of C++. Often you let a thread sleep for a specific time duration or until a particular point in time. The time library consists of: [time points](#chap21.xhtml_chapterXXXTimeSSSPoint), [time durations](#chap21.xhtml_chapterXXXTimeSSSDuration), and [clocks](#chap21.xhtml_chapterXXXClocks).

### CppMem

[CppMem](#chap22.xhtml_chapterXXXCppMem) is an interactive tool to get deeper inside into the memory model. It provides two very valuable services. First, you can verify your lock-free code and second, you can analyse your lock-free code and get, therefore, a more robust understanding of your code. I often uses CppMem in this book. Because the configuration options and the insights of CppMem are quite challenging, the chapter gives you a basic understanding of CppMem.

### Glossary

The [glossary](#chap23.xhtml_chapterXXXGlossary) contains non-exhaustive explanations on the most essential terms.

# The Details

## Memory Model

The foundation of multithreading is a *well-defined* memory model. From the reader’s perspective, it consists of two aspects. On the one hand, there is the enormous complexity of it, which often contradicts our intuition. On the other hand, it helps a lot to get a more-in-depth insight into the multithreading challenges.

However, first of all, what is a memory model?

### Basics of the Memory Model

From the concurrency point of view, there are two main aspects of the memory model:

*   What is a memory location?
*   What happens if two threads access the same memory location?

Let me answer both questions.

#### What is a memory location?

A memory location is according to [cppreference.com](http://en.cppreference.com/w/cpp/language/memory_model)

*   an object of scalar type (arithmetic type, pointer type, enumeration type, or `std::nullptr_t`),
*   or the largest contiguous sequence of bit fields of non-zero length.

Here is an example to a memory location:

```
struct S {
    char a;        // memory location #1
    int b : 5;     // memory location #2
    int c : 11,    // memory location #2 (continued)
          : 0,
        d : 8;     // memory location #3
    int e;         // memory location #4
    double f;      // memory location #5
    std::string g; // several memory locations
};
```

First, the object `obj` consists of seven sub-objects and the two bit fields `b`, and `c` share the same memory location.

Here are a few import observations:

*   Each variable is an object.
*   Scalar types occupy one memory location.
*   Adjacent bit fields (`b` and `c`) have the same memory location.
*   Variables occupies at least one memory location.

Now, to the crucial part of multithreading.

#### What happens if two threads access the same memory location?

If two threads access the same memory location - adjacent bit fields can share the same memory location - and at least one thread wants to modify it, your program has a [data races](#chap20.xhtml_chapterXXXDataSSSRaces) unless

1.  the memory location is modified by an atomic operation.
2.  one access happens-before the other.

The second case is quite interesting because synchronisation primitives such as [mutexes](#chap06.xhtml_chapterXXXMutexes) establish happens-before relations. These happens-before relations are based on operations on atomics and apply in general also on operations on non-atomics. The [memory-ordering](#chap05.xhtml_chapterXXXTheSSSSychronisationSSSandSSSOrderingSSSConstraints) defines the details which causes the happens-before relations and are, therefore, key fundamental part of the memory model.

This was my first formal approach to the memory model. Now, I want to give you a mental model for the memory model. The C++ memory model defines a contract.

### The Contract

This contract is between the programmer and the system. The system consists of the compiler that generates machine code, the processor that executes the machine code and includes the different caches that store the state of the program. Each of the participants wants to optimise its part. For example, the compiler uses registers or modifies loops; the processor performs out of order execution or branch prediction; the caches applies prefetching of instructions or buffering of values. The result is - in the good case - a *well-defined* executable, that is fully optimised for the hardware platform. To be precise, there is not only a single contract, but a fine-grained set of contracts. Or to say it differently: the weaker the rules are that the programmer has to follow, the more potential there is for the system to generate a highly optimised executable.

There is a rule of thumb. The stronger the contract, the fewer liberties for the system to generate an optimised executable. Sadly, the other way around does not work. When the programmer uses an extremely weak contract or memory model, there are many optimisation choices. The consequences are that the program is only manageable by a handful of worldwide recognised experts, to which probably neither you nor I belong to.

Roughly speaking, there are three contract levels in C++11.

![Three levels of the contract](images/MemoryModel----Overview.png)

Three levels of the contract

Before C++11, there was only one contract. The C++ language specification did not include [multithreading](#chap06.xhtml_chapterXXXMultithreading) or [atomics](#chap05.xhtml_chapterXXXAtomics). The system only knew about one control flow, and therefore there were only restricted opportunities to optimise the executable. The key point of the system was to guarantee for the programmer that the observed behaviour of the program corresponded to the sequence of the instructions in the source code. Of course, this means that there was no memory model. Instead, there was the concept of a [sequence point](#chap23.xhtml_glossaryXXXSequenceSSSPointSSSBOBOBOGlossaryBCBCBC). Sequence points are points in the program, at which the effects of all instructions preceding it must be observable. The start or the end of the execution of a function are sequence points. When you invoke a function with two arguments, the C++ standard makes no guarantee about which argument is evaluated first, so the behaviour is unspecified. The reason is straightforward - the comma operator is not a sequence point, and this does not change in C++.

With C++11 everything has changed. C++11 is the first standard aware of multiple threads. The reason for the *well-defined* behaviour of threads is the C++ memory model that was heavily inspired by the [Java memory model](https://en.wikipedia.org/wiki/Java_memory_model), but the C++ memory model goes - as always - a few steps further. The programmer has to obey a few rules in dealing with shared variables to get a *well-defined* program. The program is undefined if there exists at least one [data race](#chap20.xhtml_chapterXXXDataSSSRaces). As I already mentioned, you have to be aware of data races if your threads share mutable data. Tasks are a lot easier to use than threads or condition variables.

With atomics, we enter the domain of the experts. This becomes more evident, the more we weaken the C++ memory model. We often talk about [lock-free programming](#chap23.xhtml_glossaryXXXlockMMMfreeSSSBOBOBOGlossaryBCBCBC) when we use atomics. I spoke in this subsection about the weak and strong rules. Indeed, the [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency) is called the strong memory model, and the [relaxed semantic](#chap05.xhtml_chapterXXXRelaxedSSSSemantic) is called the weak memory model.

#### The Foundation

The C++ memory model has to deal with the following points:

*   Atomic operations: operations that can be performed without interruption.
*   Partial ordering of operations: sequences of operations that must not be reordered.
*   Visible effects of operations: guarantees when operations on shared variables are visible to other threads.

The foundation of the contract are operations on [atomics](#chap05.xhtml_chapterXXXAtomics) that have two characteristics: They are by definition atomic or indivisible, and they create [synchronisation and order constraints](#chap05.xhtml_chapterXXXTheSSSSychronisationSSSandSSSOrderingSSSConstraints) on the program execution. These synchronisation and order constraints also hold for operations on non-atomics. On the one hand, an operation on an atomic is always atomic, but on the other hand, you can tailor the synchronisations and order constraints to your needs.

#### The Challenges

The more we weaken the memory model, the more we change our focus towards other things, such as:

*   The program has more optimisation potential.
*   The possible number of control flows of the program increases exponentially.
*   We are in the domain for the experts.
*   The program breaks our intuition.
*   We apply micro-optimisation.

To deal with multithreading, we should be an expert. In case we want to deal with atomics (sequential consistency), we should open the door to the next level of expertise. What happens when we talk about the [acquire-release semantic](#chap05.xhtml_chapterXXXAcquire-ReleaseSSSSemantic) or relaxed semantic? We advance one step higher to (or deeper into) the next expertise level.

![The expert levels](images/MemoryModel----ExpertLevels.png)

The expert levels

Now, we dive deeper into the C++ memory model and start with lock-free programming. On our journey, I write about atomics and their operations. Once we are done with the basics, the different levels of the memory model follow. The starting point is the straightforward sequential consistency, the acquire-release semantic follows, and the not so intuitive relaxed semantic is the endpoint of our journey.

Let’s start with atomics.

### Atomics

Atomics are the base of the C++ memory model. By default, the strong version of the memory model is applied to the atomics; therefore, it makes much sense to understand the features of the strong memory model.

#### Strong versus Weak Memory Model

As you may already know from the subsection on [Contract: The Challenges](#chap05.xhtml_chapterXXXTheSSSChallenges), with the strong memory model I refer to [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency), and with the weak memory model I refer to [relaxed semantic](#chap05.xhtml_chapterXXXRelaxedSSSSemantic).

##### Strong Memory Model

Java 5.0 got its current memory model in 2004, C++ in 2011\. Before that, Java had an erroneous memory model, and C++ had no memory model. Those who think this is the endpoint of a long process are entirely wrong. The foundations of multithreaded programming are 40 to 50 years old. [Leslie Lamport](https://en.wikipedia.org/wiki/Leslie_Lamport) defined the concept of sequential consistency in 1979.

Sequential consistency provides two guarantees:

*   The instructions of a program are executed in the order written down.
*   There is a global order of all operations on all threads.

Before I dive deeper into these two guarantees, I want to explicitly emphasise that these statements only hold for atomics but influence non-atomics.

This graphic shows two threads. Each thread stores its variable *x* or *y* respectively loads the other variable *y* or *x*, and stores them in the variable *res1* or *res2*.

![Two atomics](images/MemoryModel----twoAtomics.png)

Two atomics

Because the variables are atomic, the operations are executed atomically. By default, sequential consistency applies. The question is: in which order can the statements be executed?

The first guarantee of the sequential consistency is that the instructions are executed in the order defined in the source code. This is easy. No store operation can overtake a load operation.

The second guarantee of the sequential consistency is that all instructions of all threads have to follow a global order. In the case listed above, it means that thread 2 sees the operations of thread 1 in the same order in which thread 1 executes them. This is the critical observation. Thread 2 sees all operations of thread 1 in the source code order of thread 1\. The same holds from the perspective of thread 1\. You can think about characteristic two as a global clock which all threads have to obey. The global clock is the global order. Each time the clock makes a tick, one atomic operation takes place, but you never know which one.

We are not yet done with our riddle. We still need to look at the different interleaving executions of the two threads. So the following six interleavings of the two threads are possible.

![The six interleavings of the two threads](images/MemoryModel----atomicInterleaving.png)

The six interleavings of the two threads

That was easy, right? That was sequential consistency, also known as the strong memory model.

##### Weak Memory Model

Let refer once more to the [contract between the programmer and the system](#chap05.xhtml_chapterXXXTheCCCContract).

The programmer uses atomics in this particular example. He obeys his part of the contract. The system guarantees *well-defined* program behaviour without [data races](#chap20.xhtml_chapterXXXDataSSSRaces). In addition to that, the system can execute the four operations in each combination. If the programmer uses the relaxed semantic, the pillars of the contract dramatically change. On the one hand, it is a lot more difficult for the programmer to understand possible interleavings of the two threads. On the other hand, the system has a lot more optimisation possibilities.

With the relaxed semantic - also called weak memory model - there are a lot more combinations of the four operations possible. The *counter-intuitive* behaviour is that thread 1 can see the operations of thread 2 in a different order, so there is no view of a global clock. From the perspective of thread 1, it is possible that the operation `res2= x.load()` overtakes `y.store(1)`. It is even possible that thread 1 or thread 2 do not perform their operations in the order defined in the source code. For example, thread 2 can first execute `res2= x.load()` and then `y.store(1)`.

Between the sequential consistency and the relaxed-semantic are a few more models. The most important one is the acquire-release semantic. With the [acquire-release semantic](#chap05.xhtml_chapterXXXAcquire-ReleaseSSSSemantic), the programmer has to obey weaker rules than with sequential consistency. In contrast, the system has more optimisation possibilities. The acquire-release semantic is the key to a deeper understanding of synchronisation and partial ordering in multithreading programming because the threads are synchronised at specific synchronisation points in the code. Without these synchronisation points, there is no *well-defined* behaviour of threads, tasks or condition variables possible.

In the last section, I introduced sequential consistency as the default behaviour of atomic operations. What does that mean? You can specify the memory order for each atomic operation. If no memory order is specified, sequential consistency is applied, meaning that the flag `std::memory_order_seq_cst` is implicitly applied to each operation on an atomic.

So this piece of code

```
x.store(1);
res = x.load();
```

is equivalent to the following piece of code:

```
x.store(1, std::memory_order_seq_cst);
res = x.load(std::memory_order_seq_cst);
```

For simplicity, I use the first form in this book. Now it’s time to take a deeper look into the atomics of the C++ memory model. We start with the elementary `std::atomic_flag`.

#### The Atomic Flag

`std::atomic_flag` is a atomic boolean. It has a clear and a set state. For simplicity reasons I call the clear state `false` and the set state `true`. Its `clear` method enables you to set its value to `false`. With the `test_and_set` method, you can set the value back to `true` and return the previous value. There is no method to ask for the current value. This will change with C++20\. With C++20, an `std::atomic_flag` has a `test` method and can be used for thread synchronisation via the methods `notify_one`, `notify_all`, and `wait`.

All operatons of `std::atomic_flag`

| **Method** | **Description** |
| --- | --- |
| `clear` | Clears the atomic flag. |
| `test_and_set` | Sets the atomic flag and returns the old value. |
| `test` (C++20) | Returns the state. |
| `notify_one` (C++20) | Unblocks one atomic wait operation. |
| `notify_all` (C++20) | Unblocks all atomic wait operations. |
| `wait` (C++20) | Blocks until it is notified. |
|   | Compares itself first with the old (expected) value to protect against [spurious wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup). |

To use `std::atomic_flag` it must be initialised to `false` with the constant `ATOMIC_FLAG_INIT`.

`std::atomic_flag` has two outstanding properties.

`std::atomic_flag` is

*   the only [lock-free](#chap23.xhtml_glossaryXXXlockMMMfreeSSSBOBOBOGlossaryBCBCBC) atomic. A non-blocking algorithm is lock-free if there is guaranteed system-wide progress.
*   the building block for higher-level thread abstractions.

The only lock-free atomic? The remaining more powerful atomics can provide their functionality by using a [mutex](#chap06.xhtml_chapterXXXMutexes) internally according to the C++ standard. These remaining atomics have a method called `is_lock_free` to check if the atomic uses a mutex internally. On the popular microprocessor architectures, I always get the answer `true`. You should be aware of this and check it on your target system if you want to program [lock-free](#chap23.xhtml_glossaryXXXlockMMMfreeSSSBOBOBOGlossaryBCBCBC).

The interface of `std::atomic_flag` is powerful enough to build a spinlock. With a spinlock, you can protect a critical section as you would with a mutex.

The example shows the implementation of a spinlock with the help of `std::atomic_flag`

```
 1 // spinLock.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 
 6 class Spinlock{
 7   std::atomic_flag flag = ATOMIC_FLAG_INIT;
 8 public:
 9 
10   void lock(){
11     while( flag.test_and_set() );
12   }
13 
14   void unlock(){
15     flag.clear();
16   }
17   
18 };
19 
20 Spinlock spin;
21 
22 void workOnResource(){
23   spin.lock();
24   // shared resource
25   spin.unlock();
26 }
27 
28 
29 int main(){
30 
31   std::thread t(workOnResource);
32   std::thread t2(workOnResource);
33 
34   t.join();
35   t2.join();
36 
37 }
```

A spinlock with `std::atomic_flag`

Both threads `t` and `t2` (lines 31 and 32) are competing for the critical section. For simplicity, the critical section in line 24 consists only of a comment. How does it work? The class `Spinlock` has - similar to a mutex - the methods `lock` and `unlock`. In addition to this, the `std::atomic_flag` is initialised with class member initialisation to `false` (line 7).

If thread `t` is going to execute the function `workOnResource` the following scenarios can happen.

1.  Thread `t` gets the lock because the `lock` invocation was successful. The `lock` invocation is successful if the initial value of the flag in line 11 is `false`. In this case thread `t` sets it in an atomic operation to `true`. The value `true` is the value of the while loop returns to thread `t2` if it tries to get the lock. So thread `t2` is caught in the rat race. Thread `t2` cannot set the value of the flag to `false` so that `t2` must wait until thread `t1` executes the `unlock` method and sets the flag to `false` (lines 14 - 16).
2.  Thread `t` doesn’t get the lock. So we are in scenario 1 with swapped roles.

I want you to focus your attention on the method `test_and_set` of `std::atomic_flag`. The method `test_and_set` consists of two operations: reading and writing. It’s critical that both operations are performed in one atomic operation. If not, we would have a read and a write on the shared resource (line 24). That is by definition a [data race](#chap20.xhtml_chapterXXXDataSSSRaces), and the program has undefined behaviour.

It’s very interesting to compare the active waiting of a spinlock with the passive waiting of a mutex.

##### Spinlock versus Mutex

What happens to the CPU load if the function `workOnResource` locks the spinlock for 2 seconds (lines 23 - 25)?

```
 1 // spinLockSleep.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 
 6 class Spinlock{
 7   std::atomic_flag flag = ATOMIC_FLAG_INIT;
 8 public:
 9 
10   void lock(){
11     while( flag.test_and_set() );
12   }
13 
14   void unlock(){
15     flag.clear();
16   }
17 
18 };
19 
20 Spinlock spin;
21 
22 void workOnResource(){
23   spin.lock();
24   std::this_thread::sleep_for(std::chrono::milliseconds(2000));
25   spin.unlock();
26 }
27 
28 
29 int main(){
30 
31   std::thread t(workOnResource);
32   std::thread t2(workOnResource);
33 
34   t.join();
35   t2.join();
36 
37 }
```

Waiting with a spinlock

If the theory is correct, one of the four cores of my PC is fully utilised. This is precisely what happens. Take a look at the screenshot.

![A spinlock which sleeps for two seconds](images/MemoryModel----spinLockSleep.png)

A spinlock which sleeps for two seconds

The screenshot shows nicely that the load of one core reaches 100% on my PC. Each time a different core performs busy waiting.

Now I use a mutex instead of a spinlock. Let’s see what happens.

```
 1 // mutex.cpp
 2 
 3 #include <mutex>
 4 #include <thread>
 5 
 6 std::mutex mut;
 7 
 8 void workOnResource(){
 9   mut.lock();
10   std::this_thread::sleep_for(std::chrono::milliseconds(5000));
11   mut.unlock();
12 }
13 
14 int main(){
15 
16   std::thread t(workOnResource);
17   std::thread t2(workOnResource);
18 
19   t.join();
20   t2.join();
21 
22 }
```

Waiting with a mutex

Although I executed the program several times, I did not observe a significant load on any of the cores.

![A mutex which sleeps for two seconds](images/MemoryModel----mutex.png)

A mutex which sleeps for two seconds

|   |

Let’s go one step further from the basic building block `std::atomic_flag` to the more advanced atomics: the class template `std::atomic`.

#### The Class Template `std::atomic`

They are various variations of the class template `std::atomic` available. `std::atomic<bool>` and `std::atomic<user-defined type>` use the primary template. Partial specialisations are available for pointers `std::atomic<T*>`, full specialisations for integral types `std::atomic<integral type>` and with C++20 for floating-point types `std::atomic<floating-point>`. The full specialisations for integral and floating-point types behave similarly, and I will, therefore, refer to them together as arithmetic types.

The atomic booleans and atomic user-defined types support the same interface. The atomic pointer extends the interface of the atomic booleans. The same applies to the atomic arithmetic types: they extend the interface of the atomic pointers.

The downside of the various variations of `std::atomic` is that you do not have the guarantee that they are [lock-free](#chap23.xhtml_glossaryXXXlockMMMfreeSSSBOBOBOGlossaryBCBCBC).

##### `std::atomic<bool>`

Let’s start with bool: `std::atomic<bool>` uses the primary template.

`std::atomic<bool>` has a lot more to offer than `std::atomic_flag`. It can explicitly be set to `true` or `false`.

`std::atomic<bool>` is already sufficient to synchronise two threads and I can, therefore, implement a kind of a [condition variable](#chap05.xhtml_chapterXXXConditionSSSVariables) with a `std::atomic<bool>`.

Let’s first use a condition variable to synchronise two threads.

```
 1 // conditionVariable.cpp
 2 
 3 #include <condition_variable>
 4 #include <iostream>
 5 #include <thread>
 6 #include <vector>
 7 
 8 std::vector<int> mySharedWork;
 9 std::mutex mutex_;
10 std::condition_variable condVar;
11 
12 bool dataReady{false};
13 
14 void waitingForWork(){
15     std::cout << "Waiting " << std::endl;
16     std::unique_lock<std::mutex> lck(mutex_);
17     condVar.wait(lck, []{ return dataReady; });
18     mySharedWork[1] = 2;
19     std::cout << "Work done " << std::endl;
20 }
21 
22 void setDataReady(){
23     mySharedWork = {1, 0, 3};
24     {
25         std::lock_guard<std::mutex> lck(mutex_);
26         dataReady = true;
27     }
28     std::cout << "Data prepared" << std::endl;
29     condVar.notify_one();
30 }
31 
32 int main(){
33     
34   std::cout << std::endl;
35 
36   std::thread t1(waitingForWork);
37   std::thread t2(setDataReady);
38 
39   t1.join();
40   t2.join();
41   
42    for (auto v: mySharedWork){
43       std::cout << v << " ";
44   }
45       
46   
47   std::cout << "\n\n";
48   
49 }
```

Usage of a condition variable

Let me say a few words about the program. For a in-depth discussion of condition variables, read the chapter [condition variables](#chap05.xhtml_chapterXXXConditionSSSVariables) in this book.

Thread `t1` waits in line 17 for the notification of thread `t2`. Both threads use the same condition variable `condVar` and synchronise on the same mutex `mutex_`. How does the workflow run?

*   Thread `t1`
    *   prepares the work package `mySharedWork = {1, 0, 3}`
    *   set the non-atomic boolean `dataReady` to `true`
    *   send its notification `condVar.notify_one`
*   Thread `t2`
    *   waits for the notification `condVar.wait(lck, []{ return dataReady; })` while holding the lock `lck`
    *   continues its work `mySharedWork[1] = 2` after getting the notification

The boolean `dataReady` that thread `t1` sets to `true` and thread `t2` checks in the lambda-function `[]{ return dataReady; }` stands for a kind of memory for the stateless condition variable. Condition variables may be a victim to two phenomena:

1.  [spurious wakeup](#chap23.xhtml_glossaryXXXSpuriousSSSwakeupSSSBOBOBOGlossaryBCBCBC): the receiver of the message wakes up, although no notification happened,
2.  [lost wakeup](#chap23.xhtml_glossaryXXXLostSSSWakeupSSSBOBOBOGlossaryBCBCBC): the sender sends its notification before the receiver is in the wait state.

And now the pendant with `std::atomic<bool>`.

```
 1 // atomicCondition.cpp
 2 
 3 #include <atomic>
 4 #include <chrono>
 5 #include <iostream>
 6 #include <thread>
 7 #include <vector>
 8 
 9 std::vector<int> mySharedWork;
10 std::atomic<bool> dataReady(false);
11 
12 void waitingForWork(){
13     std::cout << "Waiting " << std::endl;
14     while (!dataReady.load()){                
15         std::this_thread::sleep_for(std::chrono::milliseconds(5));
16     }
17     mySharedWork[1] = 2;                     
18     std::cout << "Work done " << std::endl;
19 }
20 
21 void setDataReady(){
22     mySharedWork = {1, 0, 3};                  
23     dataReady = true;                          
24     std::cout << "Data prepared" << std::endl;
25 }
26 
27 int main(){
28     
29   std::cout << std::endl;
30 
31   std::thread t1(waitingForWork);
32   std::thread t2(setDataReady);
33 
34   t1.join();
35   t2.join();
36   
37   for (auto v: mySharedWork){
38       std::cout << v << " ";
39   }
40       
41   
42   std::cout << "\n\n";
43   
44 }
```

Implementation of a condition variable with `std::atomic<bool>`

What guarantees that line 17 is executed after the line 14? Or more generally that the thread `t1` executes mySharedWork[1] = 2 (line 17) after thread `t2` had executed `mySharedWork = {1, 0, 3}` (line 22). Now it gets more formal.

*   Line 22 *happens-before* line 23
*   Line 14 *happens-before* line 17
*   Line 23 *synchronizes-with* line 14
*   Because *synchronizes-with* establishes a *happens-before* relation and *happens-before* is transitive, it follows: `mySharedWork = {1, 0, 3}` *happens-before* `mySharedWork[1] = 2`

That was easy, wasn’t it? For simplicity, I ignored that *synchronizes-with* establishes an *inter-thread happens before* and *inter-thread happens before* establishes a *happens-before* relation. In case you are curious, here are the details: [memory_order](http://en.cppreference.com/w/cpp/atomic/memory_order).

I want to mention the critical point explicitly: access to the shared variable `mySharedWork` is synchronised using the condition variable `condVar` or the atomic `dataReady`. This holds, although `mySharedWork` itself is not protected by a lock or is an atomic.

Both programs produce the same result for `mySharedWork`.

![Synchronisations of two threads with an atomic and a condition variable](images/MemoryModel----conditionVariableAtomic.png)

Synchronisations of two threads with an atomic and a condition variable

`std::atomic<bool>` and the other full or partial specialisations of `std::atomic` support the bread and butter of all atomic operations: `compare_exchange_strong` and `compare_exchange_weak`.

The weak forms of the functions are allowed to fail spuriously, that is, act as if `*this != expected` even if they are equal. When a compare-and-exchange is in a loop, the weak version may has better performance on some platforms.

In addition to booleans, there are atomics for pointers, integrals and user-defined types. The rules for user-defined types are unique.

All variations of `std::atomic` support the [CAS](#chap05.xhtml_textXXXcompare_exchange_strongZZZcompare_exchange_weakZZZCAS) operations.

##### User Defined Atomics `std::atomic<user-defined type>`

Thanks to the class template `std::atomic`, you can define your user-defined atomic type.

There are a lot of strong restrictions on a user-defined type if you use it for an atomic type `std::atomic<user-defined type>`. The atomic type `std::atomic<user-defined type>` supports the same interface as `std::atomic<bool>`.

Here are the restrictions for a user-defined type to become an atomic type:

*   The copy assignment operator for a user-defined type, for all its base classes and all non-static members, must be trivial This means that you must not define the copy assignment operator, but you can request it from the compiler by using [`default`](http://en.cppreference.com/w/cpp/keyword/default).
*   a user-defined type must not have virtual methods or virtual base classes
*   a user-defined type must be bitwise comparable so that the C functions [memcpy](http://en.cppreference.com/w/cpp/string/byte/memcpy) or [memcmp](http://en.cppreference.com/w/cpp/string/byte/memcmp) can be applied

Most popular platforms can use atomic operations for `std::atomic<user-defined type>` if the size of the `user-defined type` is not bigger as the size of an `int`.

##### `std::atomic<T*>`

`std::atomic<T*>` is a partial specialisation of the class template `std::atomic`. The atomic pointer `std::atomic<T*>` supports all methods that `std::atomic<bool>` or `std::atomic<user-defined type>` support. It behaves like a plain pointer `T*`. `std::atomic<T*>` supports pointer arithmetic and pre- and post-increment or pre- and post-decrement operations.

Have a look at the short example.

```
int intArray[5];
std::atomic<int*> p(intArray);
p++;
assert(p.load() == &intArray[1]);
p+=1;
assert(p.load() == &intArray[2]);
--p;
assert(p.load() == &intArray[1]);
```

In C++11, there are atomic types for the known arithmetic data types.

##### `std::atomic<arithmetic type>`

For each integral type there is a full specialisation `std::atomic<integral type>` of `std::atomic`. An `std::atomic<integral type>` supports all operations that `std::atomic<T*>` support, and more. Additionally, we get with C++20 atomic types for the known floating-point types. First of all. Which specialisations for arithmetic types exists? Here are the details:

*   character types: `char`, `char8_t` (C++20), `char16_t`, `char32_t`, and `wchar_t`
*   standard signed integer types: `signed char`, `short`, `int`, `long`, and `long long`
*   standard unsigned integer types: `unsigned char`, `unsigned short`, `unsigned int`, `unsigned long`, and `unsigned long long`
*   additional integer types, defined in the header [`<cstdint>`](http://en.cppreference.com/w/cpp/header/cstdint):
    *   `int8_t`, `int16_t`, `int32_t`, and `int64_t` (signed integer with exactly 8, 16, 32, and 64 bits)
    *   `uint8_t`, `uint16_t`, `uint32_t`, and `uint64_t` (unsigned integer with exactly 8, 16, 32, and 64 bits)
    *   `int_fast8_t`, `int_fast16_t`, `int_fast32_t`, and `int_fast64_t` (fastest signed integer with at least 8, 16, 32, and 64 bits)
    *   `uint_fast8_t`, `uint_fast16_t`, `uint_fast32_t`, and `uint_fast64_t` (fastest unsigned integer with at least 8, 16, 32, and 64 bits)
    *   `int_least8_t`, `int_least16_t`, `int_least32_t`, and `int_least64_t` (smallest signed integer with at least 8, 16, 32, and 64 bits)
    *   `uint_least8_t`, `uint_least16_t`, `uint_least32_t`, and `uint_least64_t` (smallest unsigned integer with at least 8, 16, 32, and 64 bits)
    *   `intmax_t`, and `uintmax_t` (maximum signed and unsigned integer)
    *   `intptr_t`, and `uintptr_t` (signed and unsigned integer for holding a pointer)
*   standard floating-point types: `float`, `double`, and `long double`

`std::atomic<arithmetic type>` supports the composite assignment operators `+=`, `-=`, `&=`, `|=` and `^=` and their `fetch` pedants: `fetch_add`, `fetch_sub`, `fetch_and`, `fetch_or` and `fetch_xor`. There is a small difference in the composite assignment and the fetch version. The composite assignment operators return the new value; the fetch variations returns the old value. Additionally, the pre- and post-increment and pre- and post-decrement (`++x`, `x++`, `--x`, and `x--`) are available.

A more in-depth look provides more insight: there is no atomic multiplication, atomic division, nor an atomic shift operation available. This is not a significant limitation because these operations are seldom needed and can easily be implemented. Here is an example of an atomic `fetch_mult` function.

```
 1 // fetch_mult.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 
 6 template <typename T>
 7 T fetch_mult(std::atomic<T>& shared, T mult){
 8   T oldValue = shared.load();
 9   while (!shared.compare_exchange_strong(oldValue, oldValue * mult));
10   return oldValue;
11 }
12 
13 int main(){
14   std::atomic<int> myInt{5};
15   std::cout << myInt << std::endl;          
16   fetch_mult(myInt,5);
17   std::cout << myInt << std::endl;         
18 }
```

An atomic multiplication with `compare_exchange_strong`

One point worth mentioning is that the multiplication in line 9 only happens if the relation `oldValue == shared` holds. I put the multiplication in a while loop to be sure that the multiplication always takes place because there are two instructions for the reading of `oldValue` in line 8 and its usage in line 9\. Here is the result of the atomic multiplication.

![An atomic multiplication](images/MemoryModel----fetch_mult.PNG)

An atomic multiplication

##### Type Aliases

For all [`std::atomic<bool>`](#chap05.xhtml_chapterXXXatomicBBBboolEEE) and all [`std::atomic<integral type>`](#chap05.xhtml_chapterXXXatomicBBBarithmeticSSStypeEEE) the C++ standard provide type aliases if the integral type is available.

Type aliases for `std::atomic<bool>` and `std::atomic<integral type>`

| **Type alias** | **Definition** |
| --- | --- |
| `std::atomic_bool` | `std::atomic<bool>` |
| `std::atomic_char` | `std::atomic<char>` |
| `std::atomic_schar` | `std::atomic<signed char>` |
| `std::atomic_uchar` | `std::atomic<unsigned char>` |
| `std::atomic_short` | `std::atomic<short>` |
| `std::atomic_ushort` | `std::atomic<unsigned short>` |
| `std::atomic_int` | `std::atomic<int>` |
| `std::atomic_uint` | `std::atomic<unsigned int>` |
| `std::atomic_long` | `std::atomic<long>` |
| `std::atomic_ulong` | `std::atomic<unsigned long>` |
| `std::atomic_llong` | `std::atomic<long long>` |
| `std::atomic_ullong` | `std::atomic<unsigned long long>` |
| `std::atomic_char8_t` (C++20) | `std::atomic<char8_t>` (C++20) |
| `std::atomic_char16_t` | `std::atomic<char16_t>` |
| `std::atomic_char32_t` | `std::atomic<char32_t>` |
| `std::atomic_wchar_t` | `std::atomic<wchar_t>` |
| `std::atomic_int8_t` | `std::atomic<std::int8_t>` |
| `std::atomic_uint8_t` | `std::atomic<std::uint8_t>` |
| `std::atomic_int16_t` | `std::atomic<std::int16_t>` |
| `std::atomic_uint16_t` | `std::atomic<std::uint16_t>` |
| `std::atomic_int32_t` | `std::atomic<std::int32_t>` |
| `std::atomic_uint32_t` | `std::atomic<std::uint32_t>` |
| `std::atomic_int64_t` | `std::atomic<std::int64_t>` |
| `std::atomic_uint64_t` | `std::atomic<std::uint64_t>` |
| `std::atomic_int_least8_t` | `std::atomic<std::int_least8_t>` |
| `std::atomic_uint_least8_t` | `std::atomic<std::uint_least8_t>` |
| `std::atomic_int_least16_t` | `std::atomic<std::int_least16_t>` |
| `std::atomic_uint_least16_t` | `std::atomic<std::uint_least16_t>` |
| `std::atomic_int_least32_t` | `std::atomic<std::int_least32_t>` |
| `std::atomic_uint_least32_t` | `std::atomic<std::uint_least32_t>` |
| `std::atomic_int_least64_t` | `std::atomic<std::int_least64_t>` |
| `std::atomic_uint_least64_t` | `std::atomic<std::uint_least64_t>` |
| `std::atomic_int_fast8_t` | `std::atomic<std::int_fast8_t>` |
| `std::atomic_uint_fast8_t` | `std::atomic<std::uint_fast8_t>` |
| `std::atomic_int_fast16_t` | `std::atomic<std::int_fast16_t>` |
| `std::atomic_uint_fast16_t` | `std::atomic<std::uint_fast16_t>` |
| `std::atomic_int_fast32_t` | `std::atomic<std::int_fast32_t>` |
| `std::atomic_uint_fast32_t` | `std::atomic<std::uint_fast32_t>` |
| `std::atomic_int_fast64_t` | `std::atomic<std::int_fast64_t>` |
| `std::atomic_uint_fast64_t` | `std::atomic<std::uint_fast64_t>` |
| `std::atomic_intptr_t` | `std::atomic<std::intptr_t>` |
| `std::atomic_uintptr_t` | `std::atomic<std::uintptr_t>` |
| `std::atomic_size_t` | `std::atomic<std::size_t>` |
| `std::atomic_ptrdiff_t` | `std::atomic<std::ptrdiff_t>` |
| `std::atomic_intmax_t` | `std::atomic<std::intmax_t>` |
| `std::atomic_uintmax_t` | `std::atomic<std::uintmax_t>` |
| `std::atomic_signed_lock_free` (C++20) | `std::atomic<signed integral>` |
| `std::atomic_unsigned_lock_free` (C++20) | `std::atomic<unsigned integral>` |

The type aliases `atomic_signed_lock_free` and `atomic_unsigned_lock_free` are specializations of atomics whose template arguments are signed or unsigned integral types. Only implementations which support lock-free integral specialisations provide this aliases. An implementation can choose the most efficient integral specialisation.

#### All Atomic Operations

First, here is the list of all operations on atomics.

All operations on `atomic`

| **Method** | **Description** |
| --- | --- |
| `test_and_set` | Atomically set the flag to `true` and returns the previous value. |
| `clear` | Atomically sets the flag to `false`. |
| `is_lock_free` | Checks if the atomic object is lock-free. |
| `load` | Atomically returns the value of the atomic. |
| `store` | Atomically replaces the value of the atomic with a non-atomic. |
| `exchange` | Atomically replaces the value with the new value. Returns the old value. |
| `compare_exchange_strong` | Atomically compares and eventually exchanges the value. Details are [here](#chap05.xhtml_textXXXcompare_exchange_strongZZZcompare_exchange_weakZZZCAS). |
| `compare_exchange_weak` |   |
| `fetch_add`, `+=` | Atomically adds(subtracts) the value. |
| `fetch_sub`, `-=` | Returns the old value. |
| `fetch_or`, `&#124;=` | Atomically performs bitwise (OR, AND, and XOR) operation with the value. |
| `fetch_and`, `&=` | Returns the old value. |
| `fetch_xor`, `^=` |   |
| `++`, `--` | Increments or decrements (pre- and post-increment) the atomic. |
| `notify_one` (C++20) | Unblocks one atomic wait operation. |
| `notify_all` (C++20) | Unblocks all atomic wait operations. |
| `wait` (C++20) | Blocks until it is notified. |
|   | Compares itself with the `old` value to protect against [spurious wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) and [lost wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup). |
|   | If the `old` value compares to unequal, returns. |

The atomic types have no copy constructor or copy assignment operator but they support assignment from and implicit conversion to the underlying built-in type. The composite assignment operators return the new value; the fetch variations returns the old value. The composite assignment operators return values and not references to the assigned object.

```
std::atomic<long long> atomObj(2011);
atomObj = 2014;
long long nonAtomObj = atomObj;
```

Implicit conversion to the underlying type

Each method supports an additional memory-ordering argument. The default for the memory-ordering argument is `std::memory_order_seq_cst` but you can also use `std::memory_order_relaxed`, `std::memory_order_consume`, `std::memory_order_acquire`, `std::memory_order_release`, or `std::memory_order_acq_rel`. The `compare_exchange_strong` and `compare_exchange_weak` method can be parametrised with two memory-orderings. One for the success and one for the failure case. If you only explicitly provide one memory-ordering, it is used for the success and the failure case. Here are the details to [memory-ordering](#chap05.xhtml_chapterXXXTheSSSSychronisationSSSandSSSOrderingSSSConstraints).

Of course, not all operations are available on each atomic type. The table shows the list of the atomic operations depending on the atomic type.

All atomic operations depending on the atomic type

| **Method** | **atomic_flag** | **atomic<bool>** | **atomic<user>** | **atomic<T*>** | **atomic<arithmetic>** |
| --- | --- | --- | --- | --- | --- |
| `test_and_set` | yes |   |   |   |   |
| `clear` | yes |   |   |   |   |
| `is_lock_free` |   | yes | yes | yes | yes |
| `load` |   | yes | yes | yes | yes |
| `store` |   | yes | yes | yes | yes |
| `exchange` |   | yes | yes | yes | yes |
| `compare_exchange_strong` |   | yes | yes | yes | yes |
| `compare_exchange_weak` |   | yes | yes | yes | yes |
| `fetch_add`, `+=` |   |   |   | yes | yes |
| `fetch_sub`, `-=` |   |   |   | yes | yes |
| `fetch_or`, `&#124;=` |   |   |   |   | yes |
| `fetch_and`, `&=` |   |   |   |   | yes |
| `fetch_xor`, `^=` |   |   |   |   | yes |
| `++`, `--` |   |   |   | yes | yes |
| `notify_one` | yes | yes |   | yes | yes |
| `notify_all` | yes | yes |   | yes | yes |
| `wait` | yes | yes |   | yes | yes |

#### Free Atomic Functions

The functionality of the flag `std::atomic_flag` and the class template `std::atomic` can also be used with free functions. Because these functions use pointers instead of references they are compatible with C. The atomic free functions are available for the [`std::atomic_flag`](#chap05.xhtml_chapterXXXTheSSSAtomicSSSFlag) and the types such as the types you can use with the class template [`std::atomic`](#chap05.xhtml_chapterTheSSSClassSSSTemplateXXXstdCCCatomic).

The free functions for a `std::atomic_flag` are called: `std::atomic_clear()`, `std::atomic_clear_explicit`, `std::atomic_flag_test_and_set()`, and `std::atomic_flag_test_set_explicit()`. The first argument of all four variations is a pointer to a `std::atomic_flag`. Additionally, the two `_exclicit` variations expect a [memory-ordering](#chap05.xhtml_chapterXXXTheSSSSychronisationSSSandSSSOrderingSSSConstraints).

For each `std::atomic` type their is a corresponding free function available. They free functions follow a straightforward naming convention: add just the prefix `atomic_` in front of it. For example, a method call `at.store()` on a `std::atomic` becomes `std::atomic_store()`, and `std::atomic_store_explicit()`. The first overload expects in this case a pointer and the second overload, additionally, an memory-ordering.

For completeness, here are all overloads: [atomic](http://en.cppreference.com/w/cpp/atomic).

With one exception, free functions are only available on atomic types. The prominent exception to this rule is `std::shared_ptr`.

#### `std::shared_ptr`

`std::shared_ptr` is the only non-atomic data type on which you can apply atomic operations. First, let me write about the motivation for this exception.

The C++ committee saw the necessity that instances of smart pointers should provide a minimum atomicity guarantee in multithreading programs. What is the meaning of the minimal atomicity guarantee for `std::shared_ptr`? The control block of the `std::shared_ptr` is thread-safe. This means that the increase and decrease operations of the reference-counter are atomic. You also have the guarantee that the resource is destroyed exactly once.

The assertion that a `std::shared_ptr` provides, are described by [Boost](http://www.boost.org/doc/libs/1_57_0/libs/smart_ptr/shared_ptr.htm#ThreadSafety).

1.  A shared_ptr instance can be “read” (accessed using only constant operations) simultaneously by multiple threads.
2.  Different `shared_ptr` instances can be “written to” (accessed using mutable operations such as operator= or reset) simultaneously by multiple threads (even when these instances are copies, and share the same reference count underneath).

To make the two statements clear, let me show a simple example. When you copy a `std::shared_ptr` in a thread, all is fine.

```
1 std::shared_ptr<int> ptr = std::make_shared<int>(2011);
2 
3 for (auto i = 0; i < 10; i++){
4    std::thread([ptr]{                           
5      std::shared_ptr<int> localPtr(ptr);       
6      localPtr = std::make_shared<int>(2014);     
7     }).detach(); 
8 }
```

Thread-safe copying of a `std::shared_ptr`

Let’s first look at line 5\. By using copy construction for the `std::shared_ptr localPtr`, only the control block is used. This is thread-safe. Line 6 is a little bit more interesting. The `localPtr` is set to a new `std::shared_ptr`. This is not a problem from the multithreading point of view: the lambda-function (line 4) binds `ptr` by copy. Therefore, the modification of `localPtr` takes place on a copy.

The story changes dramatically if I get the `std::shared_ptr` by reference.

```
1 std::shared_ptr<int> ptr = std::make_shared<int>(2011);  
2 
3 for (auto i = 0; i < 10; i++){
4    std::thread([&ptr]{                         
5      ptr = std::make_shared<int>(2014);         
6    }).detach(); 
7 }
```

A data race on a `std::shared_ptr`

The lambda-function binds the `std::shared_ptr ptr` in line 4 by reference. This means, the assignment (line 5) may become a concurrent reading and writing of the underlying resource; therefore, the program has undefined behaviour.

Admittedly that last example was not very easy to achieve. `std::shared_ptr` requires special attention in a multithreading environment. `std::shared_ptr` is the only non-atomic data type in C+ for which atomic operations exist.

##### Atomic Operations on `std::shared_ptr`

There are specialisations for the atomic operations `load`, `store`, `compare_and_exchange` for a `std::shared_ptr`. By using the explicit variant you can even specify the memory-ordering. Here are the free atomic operations for `std::shared_ptr`.

```
std::atomic_is_lock_free(std::shared_ptr)
std::atomic_load(std::shared_ptr)
std::atomic_load_explicit(std::shared_ptr)
std::atomic_store(std::shared_ptr)
std::atomic_store_explicit(std::shared_ptr)
std::atomic_exchange(std::shared_ptr)
std::atomic_exchange_explicit(std::shared_ptr)
std::atomic_compare_exchange_weak(std::shared_ptr)
std::atomic_compare_exchange_strong(std::shared_ptr)
std::atomic_compare_exchange_weak_explicit(std::shared_ptr)
std::atomic_compare_exchange_strong_explicit(std::shared_ptr)
```

Atomic operations for `std::shared_ptr`

For the details, have a look at [cppreference.com](http://en.cppreference.com/w/cpp/memory/shared_ptr). Now it is quite easy to modify a shared pointer that is bound by reference in a thread-safe way.

```
1 std::shared_ptr<int> ptr = std::make_shared<int>(2011);
2 
3 for (auto i = 0;i < 10; i++){
4    std::thread([&ptr]{ 
5      auto localPtr = std::make_shared<int>(2014);
6      std::atomic_store(&ptr, localPtr);            
7    }).detach(); 
8 }
```

A data race for a `std::shared_ptr` resolved

The update of the `std::shared_ptr ptr` in the expression `auto localPtr = std::make_shared<int>(2014)` is thread-safe. All is well? NO! Finally, we need atomic smart pointers.

Let’s jump to C++20.

### The Class Template `std::atomic_ref` (C++20)

The class template `std::atomic_ref` applies atomic operations to the referenced non-atomic object. Concurrent writing and reading of atomic object is, therefore, no [data race](#chap20.xhtml_chapterXXXDataSSSRaces). The lifetime of the referenced object must exceed the lifetime of the `atomic_ref`. Accessing a subobject of the referenced object with an `atomic_ref` is not well-defined.

Accordingly to `std::atomic`, `std::atomic_ref` can be specialised and supports specialisations for the built-in data types.

#### Specialisations of `std::atomic_ref`

You can specialise `std::atomic_ref` for user-defined type, use partially specialisations for pointer types, or full specialisations for arithmetic types such as integral or floating-point types.

##### Primary Template

The primary template `std::atomic_ref` can be instantiated with a [TriviallyCopyable](#chap23.xhtml_glossaryXXXTriviallyCopyableSSSBOBOBOGlossaryBCBCBC) type T.

```
struct Counters { 
    int a; 
    int b; 
};

Counter counter;
std::atomic_ref<Counters> cnt(counter); 
```

##### Partial Specialisations for Pointer Types

The standard provides partial specialisations for a pointer types: `std::atomic_ref<T*>`.

##### Specialisation for Arithmetic Types

The standard provides specialisation for the integral and floating-point types: `std::atomic_ref<arithmetic type>`.

*   character types: `char`, `char8_t` (C++20), `char16_t`, `char32_t`, and `wchar_t`
*   standard signed integer types: `signed char`, `short`, `int`, `long`, and `long long`
*   standard unsigned integer types: `unsigned char`, `unsigned short`, `unsigned int`, `unsigned long`, and `unsigned long long`
*   additional integer types, defined in the header [`<cstdint>`](http://en.cppreference.com/w/cpp/header/cstdint):
    *   `int8_t`, `int16_t`, `int32_t`, and `int64_t` (signed integer with exactly 8, 16, 32, and 64 bits)
    *   `uint8_t`, `uint16_t`, `uint32_t`, and `uint64_t` (unsigned integer with exactly 8, 16, 32, and 64 bits)
    *   `int_fast8_t`, `int_fast16_t`, `int_fast32_t`, and `int_fast64_t` (fastest signed integer with at least 8, 16, 32, and 64 bits)
    *   `uint_fast8_t`, `uint_fast16_t`, `uint_fast32_t`, and `uint_fast64_t` (fastest unsigned integer with at least 8, 16, 32, and 64 bits)
    *   `int_least8_t`, `int_least16_t`, `int_least32_t`, and `int_least64_t` (smallest signed integer with at least 8, 16, 32, and 64 bits)
    *   `uint_least8_t`, `uint_least16_t`, `uint_least32_t`, and `uint_least64_t` (smallest unsigned integer with at least 8, 16, 32, and 64 bits)
    *   `intmax_t`, and `uintmax_t` (maximum signed and unsigned integer)
    *   `intptr_t`, and `uintptr_t` (signed and unsigned integer for holding a pointer)
*   standard floating-point types: `float`, `double`, and `long double`

##### All Atomic Operations

First, here is the list of all operations on `atomic_ref`.

All operations on `atomic_ref`

| **Method** | **Description** |
| --- | --- |
| `is_lock_free` | Checks if the `atomic_ref` object is lock-free. |
| `load` | Atomically returns the value of the referenced object. |
| `store` | Atomically replaces the value of the referenced object with a non-atomic. |
| `exchange` | Atomically replaces the value of the referenced object with the new value. |
| `compare_exchange_strong` | Atomically compares and eventually exchanges the value of the referenced object. Details are [here](#chap05.xhtml_textXXXcompare_exchange_strongZZZcompare_exchange_weakZZZCAS). |
| `compare_exchange_weak` |   |
| `fetch_add`, `+=` | Atomically adds(subtracts) the value to(from) the referenced object. |
| `fetch_sub`, `-=` |   |
| `fetch_or`, `&#124;=` | Atomically performs bitwise OR, AND, and XOR) operation on the referenced object. |
| `fetch_and`, `&=` |   |
| `fetch_xor`, `^=` |   |
| `++`, `--` | Increments or decrements (pre- and post-increment) the referenced object. |
| `notify_one` | Unblocks one atomic wait operation. |
| `notify_all` | Unblocks all atomic wait operations. |
| `wait` | Blocks until it is notified. |
|   | Compares itself with the `old` value to protect against [spurious wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) and [lost wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup). |
|   | If the `old` value compares to unequal, returns. |

The composite assignment operators return the new value; the fetch variations returns the old value.

Each method supports an additional memory-ordering argument. The default for the memory-ordering argument is `std::memory_order_seq_cst` but you can also use `std::memory_order_relaxed`, `std::memory_order_consume`, `std::memory_order_acquire`, `std::memory_order_release`, or `std::memory_order_acq_rel`. The `compare_exchange_strong` and `compare_exchange_weak` method can be parametrised with two memory-orderings. One for the success and one for the failure case. If you only explicitly provide one memory-ordering, it is used for the success and the failure case. Here are the details to [memory-ordering](#chap05.xhtml_chapterXXXTheSSSSychronisationSSSandSSSOrderingSSSConstraints).

Of course, not all operations are available on all types referenced by `std::atomic_ref`. The table shows the list of all atomic operations depending on the type referenced by `std::atomic_ref`.

All atomic operations depending on the type referenced by `std::atomic_ref`

| **Method** | **atomic_ref<T>** | **atomic_ref<integral>** | **atomic_ref<floating>** | **atomic_ref<T*>** |
| --- | --- | --- | --- | --- |
| `is_lock_free` | yes | yes | yes | yes |
| `load` | yes | yes | yes | yes |
| `store` | yes | yes | yes | yes |
| `exchange` | yes | yes | yes | yes |
| `compare_exchange_strong` | yes | yes | yes | yes |
| `compare_exchange_weak` | yes | yes | yes | yes |
| `fetch_add`, `+=` |   | yes | yes | yes |
| `fetch_sub`, `-=` |   | yes | yes | yes |
| `fetch_or`, `&#124;=` |   | yes |   |   |
| `fetch_and`, `&=` |   | yes |   |   |
| `fetch_xor`, `^=` |   | yes |   |   |
| `++`, `--` |   | yes |   | yes |
| `notify_one` | yes | yes | yes | yes |
| `notify_all` | yes | yes | yes | yes |
| `wait` | yes | yes | yes | yes |

Atomics and their atomic operations are the basic building blocks for the memory model. They establish synchronisation and ordering constraints that hold for both atomics and non-atomics. Let’s have a more in-depth look into the synchronisation and ordering constraints.

### The Synchronisation and Ordering Constraints

You cannot configure the atomicity of an atomic data type, but you can accurately adjust the synchronisation and ordering constraints of atomic operations. Adjusting the synchronisation and ordering constraints is a possibility which is unique to C++ and is not possible in C#’s or Java’s memory model.

There are six different variants of the memory model in C++. The key question is what their characteristics are?

#### The Six Variants of Memory Orderings in C++

We already know C++ has six variants of the memory ordering. The default for atomic operations is `std::memory_order_seq_cst`. This expression stands for [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency). In addition, you can explicitly specify one of the other five. So what does C++ have to offer?

```
enum memory_order{
    memory_order_relaxed,
    memory_order_consume,
    memory_order_acquire,
    memory_order_release,
    memory_order_acq_rel,
    memory_order_seq_cst
}
```

The memory orderings

To classify these six memory ordering, it helps to answer two questions:

1.  Which kind of atomic operations should use which memory model?
2.  Which synchronisation and ordering constraints are defined by the six variants?

My plan is quite simple: I answer both questions.

##### Kind of Atomic Operation

There are three different kinds of operations:

*   Read operations: `memory_order_acquire` and `memory_order_consume`
*   Write operations: `memory_order_release`
*   Read-modify-write operations: `memory_order_acq_rel` and `memory_order_seq_cst`

`memory_order_relaxed` defines no synchronisation and ordering constraints. It does not fit in this taxonomy.

The following table orders the atomic operations based on their reading and writing characteristics.

Characteristics of Atomic Operations

| **Operation** | **read** | **write** | **read-modify-write** |
| --- | --- | --- | --- |
| `test_and_set` |   |   | yes |
| `clear` |   | yes |   |
| `is_lock_free` | yes |   |   |
| `load` | yes |   |   |
| `store` |   | yes |   |
| `exchange` |   |   | yes |
| `compare_exchange_strong` |   |   | yes |
| `compare_exchange_weak` |   |   | yes |
| `fetch_add`, `+=` |   |   | yes |
| `fetch_sub`, `-=` |   |   |   |
| `fetch_or`, `&#124;=` |   |   | yes |
| `fetch_and`, `&=` |   |   |   |
| `fetch_xor`, `^=` |   |   |   |
| `++`, `--` |   |   | yes |
| `notify_one` |   | yes |   |
| `notify_all` |   | yes |   |
| `wait` | yes |   |   |

Read-modify-write operations have an additional guarantee: they always provide the newest value. This means a sequence of `atomVar.fetch_sub(1)` operations on different threads counts down one after the other without any gaps or duplicates.

If you use an atomic operation `atomVar.load()` with a memory model that is designed for a write or read-modify-write operation, the write part has no effect. The result is that operation `atomVar.load(std::memory_order_acq_rel)` is equivalent to operation `atomVar.load(std::memory_order_acquire)`; operation `atomVar.load(std::memory_order_release)` is equivalent to `atomVar.load(std::memory_order_relaxed)`.

##### Different Synchronisation and Ordering Constraints

There are, roughly speaking, three different types of synchronisation and ordering constraints in C++:

*   Sequential consistency: `memory_order_seq_cst`
*   Acquire-release: `memory_order_consume`, `memory_order_acquire`, `memory_order_release`, and `memory_order_acq_rel`
*   Relaxed: `memory_order_relaxed`

While the sequential consistency establishes a global order between threads, the acquire-release semantic establishes an ordering between reading and writing operations on the same atomic variable with different threads. The relaxed semantic only guarantees the modification order of some atomic `m`. Modification order means that all modifications on a particular atomic `m` occur in some particular [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC). Consequently, reads of an atomic object by a particular thread never see “older” values than those the thread has already observed.

The different memory models and their effects on atomic and non-atomic operations make the C++ memory model an interesting, but also challenging, topic. Let us discuss the synchronisation and ordering constraints of the sequential consistency, the acquire-release semantic, and the relaxed semantic.

#### Sequential Consistency

Let us dive deeper into sequential consistency. The key for sequential consistency is that all operations on all threads obey a universal clock. This global clock makes it quite intuitive to think about it.

The intuitiveness of the sequential consistency comes with a price. The downside is that the system has to synchronise threads.

The following program synchronises the producer and the consumer thread with the help of sequential consistency.

```
 1 // producerConsumer.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <string>
 6 #include <thread>
 7 
 8 std::string work;
 9 std::atomic<bool> ready(false);
10 
11 void consumer(){
12   while(!ready.load()){}
13   std::cout<< work << std::endl;    
14 }
15 
16 void producer(){
17   work= "done";
18   ready=true; 
19 }
20 
21 int main(){
22   std::thread prod(producer);
23   std::thread con(consumer);
24   prod.join(); 
25   con.join();
26 }
```

Producer-Consumer synchronisation with sequential consistency

The output of the program is not very exciting.

![Producer-Consumer synchronisation with sequential consistency](images/MemoryModel----producerConsumer.png)

Producer-Consumer synchronisation with sequential consistency

Because of sequential consistency, the program execution is deterministic. Its output is always “done”.

The graphic depicts the sequence of operations. The consumer thread waits in the while-loop until the atomic variable `ready` is set to `true`. When this happens, the consumer threads continues its work.

![Execution order of the sequential consistency](images/MemoryModel----SequenzielleKonsistenz.png)

Execution order of the sequential consistency

It is quite easy to understand that the program always returns “done”. We only have to use the two characteristics of sequential consistency. On the one hand, both threads execute their instructions in source code order; on the other hand, each thread sees the operations of the other thread in the same order. Both threads follow the same universal clock. This synchronisation does also hold - with the help of the `while(!ready.load()){}` loop - for the synchronisation of the producer and the consumer thread.

I can explain the reasoning a lot more formally by using the terminology of the memory ordering. Here is the formal version:

1.  `work= "done"` is *sequenced-before* `ready = true`
    **⇒** work= `"done"` *happens-before* `ready = true`
2.  `while(!ready.load()){}` is *sequenced-before* `std::cout << work << std::endl`
    **⇒** `while(!ready.load()){}` *happens-before* `std::cout<< work << std::endl`
3.  `ready= true` *synchronizes-with* `while(!ready.load()){}`
    **⇒** `ready= true` *inter-thread happens-before* `while (!ready.load()){}`
    **⇒** `ready= true` *happens-before* `while (!ready.load()){}`

The final conclusion: because the *happens-before* relation is transitive, it follows `work = "done"` *happens-before* `ready= true` *happens-before* `while(!ready.load()){}` *happens-before* `std::cout<< work << std::endl`

In sequential consistency, a thread sees the operations of another thread and therefore of all other threads in the same order. The critical characteristic of sequential consistency does not hold if we use the acquire-release semantic for atomic operations. The acquire-release semantic is an area where C# and Java does not follow. That’s also an area where our intuition begins to wane.

#### Acquire-Release Semantic

There is no global synchronisation between threads in the acquire-release semantic; there is only synchronisation between atomic operations **on the same atomic variable**. A write operation on one thread synchronises with a read operation on another thread on the same atomic variable.

The acquire-release semantic is based on one fundamental idea: a release operation synchronises with an acquire operation on the same atomic and establishes an ordering constraint. The ordering constraint means all read and write operations cannot be moved after a release operation, and all read and write operations cannot be moved before an acquire operation.

What is an acquire or a release operation? The reading of an atomic variable with `load` or `test_and_set` is an acquire operation. There is more: the releasing of a lock or mutex *synchronizes-with* the acquiring of a lock or a mutex. The construction of a thread *synchronizes-with* the invocation of the callable. The completion of the thread *synchronizes-with* the `join`-call. The completion of the callable of the task *synchronizes-with* the call to `wait` or `get` on the future. Acquire and release operations come in pairs.

It helps a lot to keep that picture in mind.

![The critical region](images/MemoryModel----criticalRegion.png)

The critical region

Now, let us look once more at the spinlock in the subsection [std::atomic_flag](#chap05.xhtml_chapterXXXTheSSSAtomicSSSFlag). We can write it more efficiently because the synchronisation is done with the atomic_flag `flag`. Therefore the acquire-release semantic applies.

```
 1 // spinlockAcquireRelease.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 
 6 class Spinlock{
 7   std::atomic_flag flag;
 8 public:
 9   Spinlock(): flag(ATOMIC_FLAG_INIT) {}
10 
11   void lock(){
12     while(flag.test_and_set(std::memory_order_acquire));
13   }
14 
15   void unlock(){
16     flag.clear(std::memory_order_release);
17   }
18 };
19 
20 Spinlock spin;
21 
22 void workOnResource(){
23   spin.lock();
24   // shared resource
25   spin.unlock();
26 }
27 
28 
29 int main(){
30 
31   std::thread t(workOnResource);
32   std::thread t2(workOnResource);
33 
34   t.join();
35   t2.join();
36 
37 }
```

A Spinlock with acquire-release semantic

The `flag.clear` call in line 16 is a release, the `flag.test_and_set` call in line 12 an acquire operation, and the acquire synchronises with the release operation. The heavyweight synchronization of two threads with sequential consistency (`std::memory_order_seq_cst`) is replaced by the more lightweight and performant acquire-release semantic (`std::memory_order_acquire` and `std::memory_order_release`). The behaviour is not affected.

Although the `flag.test_and_set(std::memory_order_acquire)` call is a [read-modify-write](#chap05.xhtml_chapterXXXKindSSSofSSSAtomicSSSOperations) operation, the acquire semantic is sufficient. In summary, `flag` is an atomic and guarantees, therefore, modification order. This means all modifications to `flag` occur in some particular [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC).

The acquire-release semantic is transitive. That means if you have an acquire-release semantic between two threads (a, b) and an acquire-release semantic between (b, c), you get an acquire-release semantic between (a, c).

##### Transitivity

A release operation synchronises with an acquire operation on the same atomic variable and, additionally, establishes ordering constraint. These are the components to synchronise threads in a performant way if they act on the same atomic. How can that work if two threads share no atomic variable? We do not want any sequential consistency because that is too expensive, but we want the light-weight acquire-release semantic.

The answer to this question is straightforward. Applying the transitivity of the acquire-release semantic, we can synchronise threads that are independent.

In the following example, thread `t2` with its work package `deliveryBoy` is the connection between two independent threads `t1` and `t3`.

```
 1 // transitivity.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <thread>
 6 #include <vector>
 7 
 8 std::vector<int> mySharedWork;
 9 std::atomic<bool> dataProduced(false);
10 std::atomic<bool> dataConsumed(false);
11 
12 void dataProducer(){
13     mySharedWork = {1,0,3};
14     dataProduced.store(true, std::memory_order_release);
15 }
16 
17 void deliveryBoy(){
18     while(!dataProduced.load(std::memory_order_acquire));
19     dataConsumed.store(true, std::memory_order_release);
20 }
21 
22 void dataConsumer(){
23     while(!dataConsumed.load(std::memory_order_acquire));
24     mySharedWork[1] = 2;
25 }
26 
27 int main(){
28     
29   std::cout << std::endl;
30 
31   std::thread t1(dataConsumer);
32   std::thread t2(deliveryBoy);
33   std::thread t3(dataProducer);
34 
35   t1.join();
36   t2.join();
37   t3.join();
38   
39   for (auto v: mySharedWork){
40       std::cout << v << " ";
41   }
42       
43   std::cout << "\n\n";
44   
45 }
```

Transitivity of the acquire-release semantics

The output of the program is deterministic. `mySharedWork` has the values 1,2 and 3.

![Output of the program transitivity.cpp](images/MemoryModel----trans.png)

Output of the program transitivity.cpp

There are two important observations:

1.  Thread `t2` waits in line 18, until thread `t3` sets `dataProduced` to `true` (line 14).
2.  Thread `t1` waits in line 23, until thread `t2` sets `dataConsumed` to `true` (line 19).

Let me explain the rest with a graphic.

![Transitivity of the acquire-release semantic](images/MemoryModel----transitivity.PNG)

Transitivity of the acquire-release semantic

The essential parts of the picture are the arrows.

*   The **blue** arrows are the *sequenced-before* relations. This means that all operations in one thread are executed in source code order.
*   The **red** arrows are the *synchronizes-with* relations. The reason is the acquire-release semantic of the atomic operations on the same atomic. The synchronisation between the atomics, and therefore between the threads happen at specific points.
*   *sequenced-before* establishes a *happens-before* and *synchronizes-with* a *inter-thread happens-before* relation.

The rest is pretty simple. The *happens-before* and *inter-thread happens-before* order of the instructions corresponds to the direction of the arrows from top to bottom. Finally, we have the guarantee that `mySharedWork[1] == 2` is executed last.

A release operation *synchronizes-with* an acquire operation on the same atomic variable, so we can easily synchronise threads, **if** … . The typical misunderstanding is about the **if**.

##### The Typical Misunderstanding

What is my motivation for writing about the typical misunderstanding of the acquire-release semantic? Many of my readers and students have already fallen into this trap. Let’s look at the straightforward case.

###### Waiting Included

Here is a simple program as a starting point.

```
 1 // acquireReleaseWithWaiting.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <thread>
 6 #include <vector>
 7 
 8 std::vector<int> mySharedWork;
 9 std::atomic<bool> dataProduced(false);
10 
11 void dataProducer(){
12     mySharedWork = {1, 0, 3};
13     dataProduced.store(true, std::memory_order_release);
14 }
15 
16 void dataConsumer(){
17     while( !dataProduced.load(std::memory_order_acquire) );
18     mySharedWork[1] = 2;
19 }
20 
21 int main(){
22     
23   std::cout << std::endl;
24 
25   std::thread t1(dataConsumer);
26   std::thread t2(dataProducer);
27 
28   t1.join();
29   t2.join();
30   
31   for (auto v: mySharedWork){
32       std::cout << v << " ";
33   }
34       
35   std::cout << "\n\n";
36   
37 }
```

Acquire-release with waiting

The consumer thread `t1` in line 17 waits until the consumer thread `t2` in line 13 sets `dataProduced` to `true`. `dataProduced` is the guard, and it guarantees that access to the non-atomic variable `mySharedWork` is synchronised. Synchronised means that the producer thread `t2` initialises `mySharedWork`, then the consumer thread `t2` finishes the work by setting `mySharedWork[1]` to `2`. The program is well-defined.

![Execution of the acquireReleaseWithWaiting program](images/MemoryModel----acquireReleaseWithWaiting.png)

Execution of the acquireReleaseWithWaiting program

The graphic shows the *happens-before* relation within the threads and the *synchronizes-with* relation between the threads. *synchronizes-with* establishes an *inter-thread happens-before* relation. The rest of the reasoning is the transitivity of the *happens-before* relation.

Finally it holds that `mySharedWork = {1, 0, 3}` *happens-before* `mySharedWork[1] = 2`.

![Acquire-release semantic with waiting](images/MemoryModel----withWaiting.png)

Acquire-release semantic with waiting

What aspect is often missing in this reasoning? The **if**.

###### If …

What happens if the consumer thread `t1` in line 17 doesn’t wait for the producer thread `t2`?

```
 1 // acquireReleaseWithoutWaiting.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <thread>
 6 #include <vector>
 7 
 8 std::vector<int> mySharedWork;
 9 std::atomic<bool> dataProduced(false);
10 
11 void dataProducer(){
12     mySharedWork = {1, 0, 3};
13     dataProduced.store(true, std::memory_order_release);
14 }
15 
16 void dataConsumer(){
17     dataProduced.load(std::memory_order_acquire);
18     mySharedWork[1] = 2;
19 }
20 
21 int main(){
22     
23   std::cout << std::endl;
24 
25   std::thread t1(dataConsumer);
26   std::thread t2(dataProducer);
27 
28   t1.join();
29   t2.join();
30   
31   for (auto v: mySharedWork){
32       std::cout << v << " ";
33   }
34       
35   std::cout << "\n\n";
36   
37 }
```

Acquire-release without waiting

The program has undefined behaviour because there is a data race on the variable `mySharedWork`. When we let the program run, we get the following non-deterministic behaviour.

![Undefined behaviour with the acquire-release semantic](images/MemoryModel----acquireReleaseWithoutWaiting.png)

Undefined behaviour with the acquire-release semantic

What is the issue? It holds that `dataProduced.store(true, std::memory_order_release)` *synchronizes-with* `dataProduced.load(std::memory_order_acquire)`. But that doesn’t mean the acquire operation waits for the release operation, and that is exactly what is displayed in the graphic. In the graphic the `dataProduced.load(std::memory_order_acquire)` instruction is performed before the instruction `dataProduced.store(true, std::memory_order_release)`. We have no *synchronizes-with* relation.

![Acquire-release semantic without waiting](images/MemoryModel----withoutWaiting.png)

Acquire-release semantic without waiting

###### The Solution

*synchronizes-with* means: if `dataProduced.store(true, std::memory_order_release)` happens before `dataProduced.load(std::memory_order_acquire)`, then all visible effects of the operations before `dataProduced.store(true, std::memory_order_release)` are visible after `dataProduced.load( std::memory_order_acquire)`. The key is the word **if**. That **if** is guaranteed in the first program with the predicate `(while(!dataProduced.load(std::memory_order_acquire))`.

Here it comes once again, but more formally.

All operations before `dataProduced.store(true, std::memory_order_release)` *happens-before* all operations after `dataProduced.load(std::memory_order_acquire)`, if the following holds : `dataProduced.store(true, std::memory_order_release)` *happens-before* `dataProduced.load(std::memory_order_acquire)`.

##### Release Sequence

A release sequence is a quite advanced concept when dealing with acquire-release semantic. So let first start with the acquire-release semantic in the following example.

```
 1 // releaseSequence.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 #include <iostream>
 6 #include <mutex>
 7 
 8 std::atomic<int> atom{0};
 9 int somethingShared{0};
10 
11 using namespace std::chrono_literals;
12 
13 void writeShared(){
14     somethingShared = 2011;
15     atom.store(2, std::memory_order_release); 
16 }
17 
18 void readShared(){
19      while ( !(atom.fetch_sub(1, std::memory_order_acquire) > 0) ){
20          std::this_thread::sleep_for(100ms);
21      }
22          
23      std::cout << "somethingShared: " << somethingShared << std::endl;   
24 }
25 
26 int main(){
27     
28     std::cout << std::endl;
29     
30     std::thread t1(writeShared);
31     std::thread t2(readShared);
32     // std::thread t3(readShared);
33     
34     t1.join();
35     t2.join();
36     // t3.join();
37     
38     std::cout << "atom: " << atom << std::endl;
39     
40     std::cout << std::endl;
41     
42 }
```

Acquire-release without waiting

Left first look at the example without thread `t3`. The atomic store on line 15 *synchronizes-with* the atomic load in line 19\. The synchronisation guarantees that all that happens before the store is available after the load. This means in particular that the access to the non-atomic variable `somethingShared` is not a data race.

What changes if I use the thread `t3`? Now there seems to be a data race. As I already mentioned, the first call to `atom.fetch_sub(1, std::memory_order_acquire)` (line 19) has an acquire-release semantic with `atom.store(2, std::memory_order_release)` (line 15); therefore, their is no data race on `somethingShared`.

This does not hold for the second call to `atom.fetch_sub(1, std::memory_order_acquire)`. It is a ready-modify-write operation without a `std::memory_order_release` tag. This means in particular that the second call to `atom.fetch_sub(1, std::memory_order_acquire)` does not synchronize-with the first call and a data race may occur on `sharedVariable`. May because thanks to the release sequence, this does not happen. The release sequence is extended to the second call to `atom.fetch_sub(1, std::memory_order_acquire)`; therefore, the second call `atom.fetch_sub(1, std::memory_order_acquire)` *has a happens-before* relation with the first call.

Finally, here is the output of the program.

![A release sequence](images/MemoryModel----releaseSequence.png)

A release sequence

More formally, the definition of a release sequence by the [N4659: Working Draft, Standard for Programming Language C++](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/n4659.pdf).

If you carefully follow my explanation such as the one in the subsection [Challenges](#chap05.xhtml_chapterXXXTheSSSChallenges), you probably expect [Relaxed Semantic](#chap05.xhtml_chapterXXXRelaxedSSSSemantic) to come next; however I’ll look first at the memory model `std::memory_order_consume` which is quite similar to `std::memory_order_acquire`.

#### `std::memory_order_consume`

`std::memory_order_consume` is the most legendary of the six memory orderings. That is for two reasons: first, `std::memory_order_consume` is extremely hard to understand and second - and this may change in the future - no compiler supports it currently. With C++17 the situation gets even worse. Here is the official wording: “The specification of release-consume ordering is being revised, and the use of memory_order_consume is temporarily discouraged.”

How can it be that a compiler that implements the C++11 standard doesn’t support the memory model `std::memory_order_consume`? The answer is that the compiler maps `std::memory_order_consume` to `std::memory_order_acquire`. This mapping is acceptable because both are load or acquire operations. `std::memory_order_consume` requires weaker synchronisation and ordering constraints than `std::memory_order_acquire`. Therefore, the release-acquire ordering is potentially slower than the release-consume ordering but - and this is the key point - *well-defined*.

To get an understanding of the release-consume ordering, it is a good idea to compare it with the release-acquire ordering. I speak in the following subsection explicitly about the release-acquire ordering and not about the acquire-release semantic to emphasise the strong relationship of `std::memory_order_consume` and `std::memory_order_acquire`.

##### Release-acquire ordering

As a starting point, let us use the following program with two threads `t1` and `t2`. `t1` plays the role of the producer, `t2` the role of the consumer. The atomic variable `ptr` helps to synchronise the producer and consumer.

```
 1 // acquireRelease.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 #include <iostream>
 6 #include <string>
 7 
 8 using namespace std;
 9  
10 atomic<string*> ptr;
11 int data;
12 atomic<int> atoData;
13  
14 void producer(){
15     string* p  = new string("C++11");
16     data = 2011;
17     atoData.store(2014, memory_order_relaxed);
18     ptr.store(p, memory_order_release);
19 }
20  
21 void consumer(){
22     string* p2;
23     while (!(p2 = ptr.load(memory_order_acquire)));
24     cout << "*p2: " << *p2 << endl;
25     cout << "data: " << data << endl;
26     cout << "atoData: " << atoData.load(memory_order_relaxed) << endl;
27 }
28  
29 int main(){
30     
31     cout << endl;
32     
33     thread t1(producer);
34     thread t2(consumer);
35     
36     t1.join();
37     t2.join();
38     
39     cout << endl;
40     
41 }
```

Release-acquire ordering

Before analysing the program, I want to introduce a small variation.

##### Release-consume ordering

I replace the memory order `std::memory_order_acquire` in line 21 with `std::memory_order_consume`.

```
 1 // acquireConsume.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 #include <iostream>
 6 #include <string>
 7 
 8 using namespace std;
 9  
10 atomic<string*> ptr;
11 int data;
12 atomic<int> atoData;
13  
14 void producer(){
15     string* p  = new string("C++11");
16     data = 2011;
17     atoData.store(2014,memory_order_relaxed);
18     ptr.store(p, memory_order_release);
19 }
20  
21 void consumer(){
22     string* p2;
23     while (!(p2 = ptr.load(memory_order_consume)));
24     cout << "*p2: " << *p2 << endl;
25     cout << "data: " << data << endl;
26     cout << "atoData: " << atoData.load(memory_order_relaxed) << endl;
27 }
28  
29 int main(){
30     
31     cout << endl;
32     
33     thread t1(producer);
34     thread t2(consumer);
35     
36     t1.join();
37     t2.join();
38     
39     cout << endl;
40     
41 }
```

Release-acquire ordering

Now the program has undefined behaviour. This statement is very hypothetical because my GCC 5.4 compiler implements `std::memory_order_consume` by using `std::memory_order_acquire`. Under the hood, both programs do the same thing.

##### Release-acquire versus Release-consume ordering

The outputs of the programs are identical.

![Release-acquire and release-consume ordering](images/MemoryModel----acquireReleaseConsume.png)

Release-acquire and release-consume ordering

At the risk of repeating myself, I want to add a few words explaining why the first program `acquireRelease.cpp` is well-defined.

The store operation on line 16 *synchronizes-with* the load operation in line 21\. The reason is that the store operation uses `std::memory_order_release` and the load operation uses `std::memory_order_acquire`. This store/load relation is the synchronisation. What are the ordering constraints for the release-acquire operations? The release-acquire ordering guarantees that the results of all operations before the store operation (line 16) are available after the load operation (line 21). So also, the release-acquire operation orders access to the non-atomic variable `data` (line 14) and the atomic variable `atoData` (line 15). That holds, although `atoData` uses the `std::memory_order_relaxed` memory ordering.

The crucial question is: what happens if I replace `std::memory_order_acquire` with `std::memory_order_consume`?

##### Data dependencies with `std::memory_order_consume`

`std::memory_order_consume` deals with data dependencies on atomics. Data dependencies exist in two ways. First, let us look at *carries-a-dependency-to* in a thread and *dependency-ordered before* between two threads. Both dependencies introduce a *happens-before* relation. These are the kind of relations we are looking for. What does *carries-a-dependency-to* and *dependency-order-before* mean?

*   *carries-a-dependency-to*: if the result of operation A is used as an operand in operation B, then: A *carries-a-dependency-to* B.
*   *dependency-ordered-before*: a store operation (with *std::memory_order_release*, *std::memory_order_acq_rel*, or *std::memory_order_seq_cst*) is *dependency-ordered-before* a load operation B (with *std::memory_order_consume*) if the result of load operation B is used in a further operation C in the same thread. It is important to note that operations B and C have to be in the same thread.

I know from personal experience that both definitions might not be easy to digest. Here is a graphic to visualise them.

![Data dependencies of std::memory_order_consume](images/MemoryModel----dependency.png)

Data dependencies of std::memory_order_consume

The expression `ptr.store(p, std::memory_order_release)` is *dependency-ordered-before* the expression `while (!(p2 = ptr.load(std::memory_order_consume)))`, because the following line `std::cout << "*p2: " << *p2 << std::endl` is be read as the result of the load operation. Furthermore it holds that: `while (!(p2 = ptr.load(std::memory_order_consume))` *carries-a-dependency-to* `std::cout << "*p2: " << *p2 << std::endl`, because the output of `*p2` uses the result of the `ptr.load` operation.

We have no guarantee regarding the output of `data` and `atoData`. That’s because neither has a *carries-a-dependency* relation to the `ptr.load` operation. It gets even worse: since `data` is a non-atomic variable, there is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) on the variable `data`. The reason is that both threads can access data at the same time, and thread t1 wants to modify `data`. Therefore the program has undefined behaviour.

Finally, we have reached the relaxed semantic.

#### Relaxed Semantic

The relaxed semantic is the other end of the spectrum. The relaxed semantic is the weakest of all memory models and only guarantees the modification order of atomics. This means all modifications on an atomic happen in some particular [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC).

##### No synchronisation and ordering constraints

It is quite easy. If there are no rules, we cannot violate them. However, that is too easy; the program should have *well-defined* behaviour. *Well-defined* behaviour means in particular that you typically use synchronisation and ordering constraints of stronger memory orderings to control operations with relaxed semantic. How does this work? A thread can see the effects of another thread in arbitrary order, so you have to make sure there are points in your program where all operations on all threads get synchronised.

A typical example of an atomic operation, in which the sequence of operations doesn’t matter, is a counter. The critical observation for a counter is not in which order the different threads increment the counter; the critical observation for a counter is that all increments are atomic and that all increments are done at the end. Have a look at the following example.

```
 1 // relaxed.cpp
 2 
 3 #include <vector>
 4 #include <iostream>
 5 #include <thread>
 6 #include <atomic>
 7  
 8 std::atomic<int> count = {0};
 9  
10 void add()
11 {
12     for (int n = 0; n < 1000; ++n) {
13         count.fetch_add(1, std::memory_order_relaxed);
14     }
15 }
16  
17 int main()
18 {
19     std::vector<std::thread> v;
20     for (int n = 0; n < 10; ++n) {
21         v.emplace_back(add);
22     }
23     for (auto& t : v) {
24         t.join();
25     }
26     std::cout << "Final counter value is " << count << '\n';
27 }
```

A counter with relaxed semantic

The three most exciting lines are 13, 24, and 26.

In line 13, the atomic number `count` is incremented using the relaxed semantic, so we have a guarantee that the operation is atomic. The `fetch_add` operation establishes an ordering on `count`. The function `add` (lines 10 - 15) is the work package of the threads. Each thread gets its work package on line 21.

Thread creation is one synchronisation point - the other one being `t.join()` on line 24.

The creator thread synchronises with all its children in line 24\. It waits with the `t.join()` call until all its children are done. `t.join()` is the reason that the results of the atomic operations are published. To say it more formally: `t.join()` is a release operation.

In conclusion, there is a *happens-before* relation between the increment operation in line 13 and the reading of the counter `count` in line 26.

The result is that the program always returns 10000\. Boring? No, it’s reassuring!

![The atomic counter with relaxed semantic](images/MemoryModel----relaxed.png)

The atomic counter with relaxed semantic

A typical example of an atomic counter which uses the relaxed semantic is the reference counter of `std::shared_ptr`. The relaxed semantic only holds for the increment operation. The key property for incrementing the reference counter is that the operation is atomic. The order of the increment operations does not matter. The relaxed semantic does not hold for the decrement of the reference counter. These operations need an acquire-release semantic for the destructor.

The fundamental idea of `std::atomic_thread_fence` is to establish synchronisation and ordering constraints between threads without an atomic operation.

### Fences

C++ support two kind of fences: a `std::atomic_thread_fence` and a `std::atomic_signal_fence`.

*   `std::atomic_thread_fence`: synchronises memory accesses between threads.
*   `std::atomic_signal_fence`: synchronises between a signal handler and code running on the same thread.

#### `std::atomic_thread_fence`

A `std::atomic_thread_fence` prevents specific operations from crossing a fence.

`std::atomic_thread_fence` needs no atomic variable. They are frequently just referred to as fences or memory barriers. You quickly get an idea of what a `std::atomic_thread_fence` is all about.

##### Fences as Memory Barriers

What does that mean? Specific operations cannot cross a memory barrier. What kind of operations? From a bird’s-eye view, we have two kinds of operations: read and write or load and store operations. The expression `if(resultRead) return result` is a load, followed by a store operation.

There are four different ways to combine load and store operations:

*   **LoadLoad**: A load followed by a load.
*   **LoadStore**: A load followed by a store.
*   **StoreLoad**: A store followed by a load.
*   **StoreStore**: A store followed by a store.

Of course, there are more complicated operations consisting of multiple load and stores (`count++`), and these operations fall into my general classification.

What about memory barriers? If you place memory barriers between two operations like LoadLoad, LoadStore, StoreLoad or StoreStore, you have the guarantee that specific LoadLoad, LoadStore, StoreLoad or StoreStore operations are not be reordered. The risk of reordering is always present if non-atomics or atomic operations with relaxed semantic are used.

##### The Three Fences

Typically, three kinds of fences are used. They are called full fence, acquire fence and release fence. As a reminder, acquire is a load, and release is a store operation. What happens if I place one of the three memory barriers between the four combinations of load and store operations?

*   **Full fence**: A full fence `std::atomic_thread_fence()` between two arbitrary operations prevents the reordering of these operations with one exception: StoreLoad operations can be reordered.
*   **Acquire fence**: An acquire fence `std::atomic_thread_fence(std::memory_order_acquire)` prevents a read operation before an acquire fence from being reordered with a read or write operation after the acquire fence.
*   **Release fence**: A release fence `std::atomic_thread_fence(std::memory_order_release)` prevents a write operation after a release fence from being reorderd with a read or write operation before a release fence.

A lot of energy goes into getting the definitions of the acquire and release fence and their consequences for lock-free programming right. Especially challenging to understand are the subtle differences between the acquire-release semantic of atomic operations. Before I get to that point, I illustrate the definitions with graphics.

Which kind of operations can cross a memory barrier? Have a look at the following three graphics. If the arrow is crossed with a red bar, the fence prevents this type of operation.

###### Full fence

![Full fence](images/MemoryModel----FullFence.png)

Full fence

Of course, instead of writing `std::atomic_thread_fence()` you can explicitly write `std::atomic_thread_fence(std::memory_order_seq_cst)`. [Sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency%7D) is applied to fences by default. If you use sequential consistency for a full fence, the `std::atomic_thread_fence` follows a global order.

###### Acquire fence

![Acquire fence](images/MemoryModel----AcquireFence.png)

Acquire fence

###### Release fence

![Release fence](images/MemoryModel----ReleaseFence.png)

Release fence

The three memory barriers can be depicted even more concisely.

###### All Fences at a Glance

![All fences at a glance](images/MemoryModel----loadStore.png)

All fences at a glance

Acquire and release fences guarantee similar synchronisation and ordering constraints as atomics with acquire-release semantic.

##### Acquire-Release Fences

The most apparent difference between acquire and release fences and atomics with acquire-release semantics is that fences need no atomics. There is also a more subtle difference; the acquire and release fences are more heavyweight than the corresponding atomics.

###### Atomic Operations versus Fences

For the sake of simplicity, I now refer to acquire operations when I use fences or atomic operations with acquire semantics. The same holds for release operations.

The main idea of an acquire, and a release operation is that it establishes synchronisation and ordering constraints between threads. These synchronisation and ordering constraints also hold for atomic operations with relaxed semantic or non-atomic operations. Note that acquire and release operations come in pairs. Besides, operations on atomic variables with acquire-release semantic must act on the same atomic variable. Having said that I now look at these operations in isolation.

Let’s start with the acquire operation.

###### Acquire Operation

A load (read) operation on an atomic variable with the memory-ordering set to `std::memory_order_acquire` is an acquire operation.

![Atomic operation with acquire semantic](images/MemoryModel----acquireOperation.png)

Atomic operation with acquire semantic

`std::atomic_thread_fence` with the memory order set to `std::memory_order_acquire` imposes stricter constraints on memory access reordering:

![Fence with acquire semantic](images/MemoryModel----AcquireFence.png)

Fence with acquire semantic

This comparison emphasises two points:

1.  A fence with acquire semantic establishes stronger ordering constraints. Although the acquire operation on an atomic and on a fence require that no read or write operation can be moved before the acquire operation, there is an additional guarantee with the acquire fence. No read operation can be moved after the acquire fence.
2.  The relaxed semantic is sufficient for the reading of the atomic variable `var`. Thanks to `std::atomc_thread_fence(std::memory_order_acquire)`, this operation cannot be moved after the acquire fence.

Similar observations can be made for the release fence.

###### Release Operation

The store (write) operation on an atomic variable with the memory-ordering set to `std::memory_order_release` is a release operation.

![Atomic operation with release semantic](images/MemoryModel----releaseOperation.png)

Atomic operation with release semantic

Here is the corresponding image for the release fence.

![Fence with release semantic](images/MemoryModel----ReleaseFence.png)

Fence with release semantic

In addition to the constraints imposed by the release operation on an atomic variable `var`, the release fence guarantees two properties:

1.  Store operations can’t be moved before the fence.
2.  It’s sufficient for the variable `var` to have relaxed semantic.

However now, it’s time to go one step further and build a program that uses fences.

##### Synchronisation with Atomic Variables or Fences

As a starting point, I’ve implemented a typical consumer-producer workflow with the acquire-release semantic. Initially, I use atomics and then switch to fences.

###### Atomic Operations

Let’s start with atomics because most of us are comfortable with them.

```
 1 // acquireRelease.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 #include <iostream>
 6 #include <string>
 7 
 8 using namespace std;
 9  
10 atomic<string*> ptr;
11 int data;
12 atomic<int> atoData;
13  
14 void producer(){
15     string* p  = new string("C++11");
16     data = 2011;
17     atoData.store(2014, memory_order_relaxed);
18     ptr.store(p, memory_order_release);
19 }
20  
21 void consumer(){
22     string* p2;
23     while (!(p2 = ptr.load(memory_order_acquire)));
24     cout << "*p2: " << *p2 << endl;
25     cout << "data: " << data << endl;
26     cout << "atoData: " << atoData.load(memory_order_relaxed) << endl;
27 }
28  
29 int main(){
30     
31     cout << endl;
32     
33     thread t1(producer);
34     thread t2(consumer);
35     
36     t1.join();
37     t2.join();
38     
39     cout << endl;
40     
41 }
```

Acquire-release ordering with atomics

This program should be quite familiar to you. It is the classic example that I used in the subsection about [`std::memory_order_consume`](#chap05.xhtml_chapterZZZmemory_order_consume). The graphics emphasise exactly that the consumer thread `t2` sees all values from the producer thread `t1`.

![Acquire-release semantic with atomic operations](images/MemoryModel----acquireRelease.png)

Acquire-release semantic with atomic operations

The program is well-defined because the happens-before relation is transitive. I only have to combine the three happens-before relations:

1.  Lines 15 - 17 *happens-before* line 18 `ptr.store(p, std::memory_order_release)`.
2.  Line 23 `while(!(p2= ptrl.load(std::memory_order_acquire)))` *happens-before* the lines 24 - 26.
3.  Line 18 *synchronizes-with* line 23\. **⇒** Line 18 *inter-thread happens-before* line 23.

However, the story becomes more interesting. Now I come to fences. They are almost completely ignored in the literature on the C++ memory model.

###### Fences

It’s quite straightforward to port the program to use fences.

```
 1 // acquireReleaseFences.cpp
 2 
 3 #include <atomic>
 4 #include <thread>
 5 #include <iostream>
 6 #include <string>
 7 
 8 using namespace std;
 9  
10 atomic<string*> ptr;
11 int data;
12 atomic<int> atoData;
13  
14 void producer(){
15     string* p  = new string("C++11");
16     data = 2011;
17     atoData.store(2014, memory_order_relaxed);
18     atomic_thread_fence(memory_order_release);
19     ptr.store(p, memory_order_relaxed);
20 }
21  
22 void consumer(){
23     string* p2;
24     while (!(p2 = ptr.load(memory_order_relaxed)));
25     atomic_thread_fence(memory_order_acquire);
26     cout << "*p2: " << *p2 << endl;
27     cout << "data: " << data << endl;
28     cout << "atoData: " << atoData.load(memory_order_relaxed) << endl;
29 }
30  
31 int main(){
32     
33     cout << endl;
34     
35     thread t1(producer);
36     thread t2(consumer);
37     
38     t1.join();
39     t2.join();
40     
41     delete ptr;
42     
43     cout << endl;
44     
45 }
```

Acquire-release ordering with fences

The first step was to add fences with release and acquire semantic (lines 18 and 25). Next, I changed the atomic operations with acquire or release semantic to relaxed semantic (lines 19 and 24). That was straightforward. Of course, I can only replace an acquire or release operation with the corresponding fence. The key point is that the release fence establishes a *synchronizes-with* relation with the acquire fence and therefore an *inter-thread happens-before* relation.

Here is the output of the program.

![Synchronisation with fences](images/MemoryModel----acquireReleaseAcquireReleaseFences.png)

Synchronisation with fences

For the more visual reader, here’s the entire relation graphically.

![Acquire-release semantic with fences](images/MemoryModel----acquireReleaseFences.png)

Acquire-release semantic with fences

The key question is: why do the operations after the acquire fence see the effects of the operations before the release fence? This guarantee is interesting because `data` is a non-atomic variable and `atoData.store` is used with relaxed semantic. This would suggest they can be reordered; however, thanks to the `std::atomic_thread_fence(std::memory_order_release)` as a release operation in combination with the `std::atomic_thread_fence(std::memory_order_acquire)`, neither can be reordered.

For clarity, the whole reasoning in a more concise form.

1.  The acquire and release fences prevent the reordering of the atomic and non-atomic operations across the fences.
2.  The consumer thread `t2` is waiting in the `while (!(p2= ptr.load(std::memory_order_relaxed)))` loop, until the pointer `ptr.store(p,std::memory_order_relaxed)` is set in the producer thread `t1`.
3.  The release fence *synchronizes-with* the acquire fence.
4.  In the end, all effects of relaxed or non-atomic operations that *happen-before* the release fence are visible after the acquire fence.

You can even mix the acquire and release operations on an atomic in the program `acquireRelease.cpp` with the acquire and release fence in the program `acquireReleaseFence.cpp` without affecting the *synchronize-with* relation.

#### `std::atomic_signal_fence`

`std::atomic_signal_fence` establishes memory synchronisation ordering of non-atomic and relaxed atomic accesses between a thread and a signal handler executed on the same thread. The following program shows the usage of a `std::atomic_signal_fence`.

```
 1 // atomicSignal.cpp
 2 
 3 #include <atomic>
 4 #include <cassert>
 5 #include <csignal>
 6 
 7 std::atomic<bool> a{false};
 8 std::atomic<bool> b{false};
 9 
10 extern "C" void handler(int) {
11     if (a.load(std::memory_order_relaxed)) {
12         std::atomic_signal_fence(std::memory_order_acquire);
13         assert(b.load(std::memory_order_relaxed));
14     }
15 }
16 
17 int main() {
18     
19     std::signal(SIGTERM, handler);
20 
21     b.store(true, std::memory_order_relaxed);
22     std::atomic_signal_fence(std::memory_order_release);
23     a.store(true, std::memory_order_relaxed);
24     
25 }
```

Synchronisation with a signal handler

First, I set in line 19 the signal handler `handler` for the particular signal `SIGTERM`. `SIGTERM` is a termination request for the program. Both `std::atomic_signal_handler` establish an acquire-release fence between the release operation `std::atomic_signal_fence(std::memory_order_release)` (line 22) and the acquire operation `std::atomic_signal_fence(std::memory_order_acquire)` (line 12). This means in particular that release operations can not be reordered across the release fence (line 22) and that acquire operations can not be reordered across the acquire fence (line 11). Consequently, the assertion in line 13 `assert(b.load(std::memory_order_relaxed))` never fires because if `a.store(true, std::memory_order_relaxed)` (line 23) happened, `b.store(true, std::memory_order_relaxed)` (line 21) must have happened before.

## Multithreading

C++ has a multithreading interface since C++11 and this interface has all the basic building blocks for creating multithreaded programs. These are [threads](#chap06.xhtml_chapterXXXThread), synchronisation primitives for shared data such as [mutexes](#chap06.xhtml_chapterXXXMutexes) and [locks](#chap06.xhtml_chapterXXXLocks), [thread-local data](#chap06.xhtml_chapterXXXThreadSSSLocalSSSData), synchronisation mechanism for threads such as [condition variables](#chap06.xhtml_chapterXXXConditionSSSVariables), and [tasks](#chap06.xhtml_chapterXXXTasks). Tasks, usually called promises and futures, provide a higher abstraction than native threads.

![Multithreading in C++11 and C++14](images/timeline----timeline11_14.png)

Multithreading in C++11 and C++14

### Threads

To launch a thread in C++, you have to include the `<thread>` header.

#### Thread Creation

A [thread](#chap06.xhtml_chapterXXXThreads) `std::thread` represents an executable unit. This executable unit, which the thread immediately starts, gets its work package as a [callable unit](#chap06.xhtml_glossaryXXXCallableSSSUnitSSSBOBOBOGlossaryBCBCBC). A thread is not copy-constructible or copy-assignable but move-constructible or move-assignable.

A callable unit is an entity that behaves like a function. Of course it can be a function but also a [function object](#chap06.xhtml_glossaryXXXfunctionSSSObjectsSSSBOBOBOGlossaryBCBCBC), or a [lambda function](#chap23.xhtml_glossaryXXXLambdaSSSFunctionsSSSBOBOBOGlossaryBCBCBC). The return value of the callable unit is ignored.

After discussing theory, here is a small example.

```
 1 // createThread.cpp
 2 
 3 #include <iostream>
 4 #include <thread>
 5 
 6 void helloFunction(){
 7   std::cout << "Hello from a function." << std::endl;
 8 }
 9 
10 class HelloFunctionObject{
11   public:
12     void operator()() const {
13       std::cout << "Hello from a function object." << std::endl;
14     }
15 };
16 
17 int main(){
18 
19   std::cout << std::endl;
20 
21   std::thread t1(helloFunction);
22 
23   HelloFunctionObject helloFunctionObject;
24   std::thread t2(helloFunctionObject);
25 
26   std::thread t3([]{std::cout << "Hello from a lambda." << std::endl;});
27 
28   t1.join();
29   t2.join();
30   t3.join();
31 
32   std::cout << std::endl;
33 
34 };
```

Creation of a thread with callable units

All three threads (`t1`, `t2`, and `t3`) write their messages to the console. The work package of thread `t2` is a function object (lines 10 - 15), the work package of thread `t3` is a lambda function (line 26). In lines 28 - 30 the main thread is waiting until its children are done.

Let’s have a look at the output. This is more interesting.

![Creation of threads with various callables](images/Multithreading----createThread.png)

Creation of threads with various callables

The three threads are executed in an arbitrary order. Even the three output operations can interleave.

The creator of the child - in our case this was the main thread - is responsible for the lifetime of the child.

#### Thread Lifetime

The parent has to take care of its children. This simple principle has big consequences for the lifetime of a thread. This small program starts a thread that displays its id.

```
 1 // threadWithoutJoin.cpp
 2 
 3 #include <iostream>
 4 #include <thread>
 5 
 6 int main(){
 7 
 8   std::thread t([]{std::cout << std::this_thread::get_id() << std::endl;});
 9 
10 }
```

Forget to join a thread

But the program does not print the id.

![Forget to join a thread](images/Multithreading----threadForgetJoin.png)

Forget to join a thread

What’s the reason for the exception?

##### `join` and `detach`

The lifetime of a created thread `t` ends with its callable unit. The creator has two choices.

1.  It can wait until its child is done: `t.join()`.
2.  It can detach itself from its child: `t.detach()`.

A `t.join()` call is useful when the subsequent code relies on the result of the calculation performed in the thread. `t.detach()` permits the thread to execute independently from the thread handle `t`; therefore, the detached thread runs for the lifetime of the executable. Typically you use a detached thread for a long-running background service such as a server.

A thread `t` with a callable unit - you can create threads without a [callable unit](#chap23.xhtml_glossaryXXXCallableSSSUnitZZZcallableSSSBOBOBOGlossaryBCBCBC) - is called joinable if neither a `t.join()` nor a `t.detach()` call happened. The destructor of a joinable thread throws the `std::terminate` exception. This was the reason the program execution of `threadWithoutJoin.cpp` terminated with an exception. If you invoke `t.join()` or `t.detach()` more than once on a thread `t`, you get a `std::system_error` exception.

The solution to this problem is quite simple: call `t.join()`.

```
 1 // threadWithJoin.cpp
 2 
 3 #include <iostream>
 4 #include <thread>
 5 
 6 int main(){
 7 
 8   std::thread t([]{std::cout << std::this_thread::get_id() << std::endl;});
 9 
10   t.join(); 
11 
12 }
```

Joining a thread

Now we get the expected output.

![Join a thread](images/Multithreading----threadJoin.png)

Join a thread

The thread’s id serves as a unique identifier of the std::thread.

#### Thread Arguments

A thread such as an arbitrary function can get its arguments by copy, by move, or by reference. `std::thread` is a [variadic template](http://en.cppreference.com/w/cpp/language/parameter_pack). This means it can get an arbitrary number of arguments.

In the case where your thread gets its data by reference, you have to be extremely careful about the lifetime of the arguments and the sharing of data.

##### Copy or Reference

Let’s have a look at a small code snippet.

```
std::string s{"C++11"}

std::thread t1([=]{ std::cout << s << std::endl; });
t1.join();

std::thread t2([&]{ std::cout << s << std::endl; });
t2.detach();
```

Thread `t1` gets its argument by copy, thread `t2` by reference.

What issues are hiding in these lines of code? Thread `t2` gets its string `s` by reference, and afterwards is detached from the lifetime of its creator. The lifetime of the string `s` is bound to the lifetime of the creator; the lifetime of the global object `std::cout` is bound to the lifetime of the main thread. So it is possible that the lifetime of `s` or the lifetime of `std::cout` is shorter than the lifetime of the thread `t2`. Now we are deep in the area of undefined behaviour.

Not convinced? Let’s take a closer look at what undefined behaviour may look like.

```
 1 // threadArguments.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <thread>
 6 
 7 class Sleeper{
 8   public:
 9     Sleeper(int& i_): i{i_}{};
10     void operator() (int k){
11       for (unsigned int j = 0; j <= 5; ++j){
12         std::this_thread::sleep_for(std::chrono::milliseconds(100));
13         i += k;
14       }
15       std::cout << std::this_thread::get_id() << std::endl;
16     }
17   private:
18     int& i;
19 };
20 
21 
22 int main(){
23 
24   std::cout << std::endl;
25 
26   int valSleeper = 1000;
27   std::thread t(Sleeper(valSleeper), 5);
28   t.detach();
29   std::cout << "valSleeper = " << valSleeper << std::endl;
30 
31   std::cout << std::endl;
32 
33 }
```

Passing the arguments to a thread by reference

The question is: what value does `valSleeper` have in line 29? `valSleeper` is a global variable. Thread `t` gets as its work package a function object with the variable `valSleeper` and the number 5 (line 27). The crucial observation is that the thread gets `valSleeper` by reference (line 9) and is detached from the main thread (line 28). Next it executes the call operator of the function object (lines 10 - 16). In this method it counts from 0 to 5, sleeps in each iteration 1/10 of a second, and increments `i` by `k`. In the end, it displays its id on the screen. [Nach Adam Riese](https://de.wikipedia.org/wiki/Liste_gefl%C3%BCgelter_Worte/N#Nach_Adam_Riese) (a German proverb), the result should be 1000 + 6 * 5 = 1030.

However, what happened? Something is going very wrong.

![Undefined behaviour with a reference](images/Multithreading----Sleeper.png)

Undefined behaviour with a reference

The program has two strange properties. First, `valSleeper` is 1000 and second, the id is not displayed.

The program has at least two issues.

1.  `valSleeper` is shared by all threads. This is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) because the threads may read and write `valSleeper` at the same time.
2.  The lifetime of the main thread ends before the child thread has performed its calculation or written its id to `std::cout`.

Both issues are [race conditions](#chap20.xhtml_chapterXXXRaceSSSCondition) because the result of the program depends on the interleaving of the operations. The race condition is the cause of the data race.

Fixing the data race is quite easy. `valSleeper` should be protected using either a [lock](#chap06.xhtml_chapterXXXLocks) or an [atomic](#chap05.xhtml_chapterXXXAtomics). To overcome the lifetime issues of `valSleeper` and `std::cout`, you have to join the thread instead of detaching it.

Here is the modified main function.

```
int main(){

  std::cout << std::endl;

  int valSleeper= 1000;
  std::thread t(Sleeper(valSleeper),5);
  t.join();
  std::cout << "valSleeper = " << valSleeper << std::endl;

  std::cout << std::endl;

}
```

Now we get the right result. Of course, the execution becomes slower.

![Fixed the undefined behaviour](images/Multithreading----Sleeper2.png)

Fixed the undefined behaviour

To complete the story of `std::thread`, here are the remaining methods.

#### Methods

Here is the interface of `std::thread t` in a concise table. For additional details, please refer to [cppreference.com](http://de.cppreference.com/w/cpp/thread/thread).

Methods of a thread `t`

| **Method** | **Description** |
| --- | --- |
| `t.join()` | Waits until thread `t` has finished its executable unit. |
| `t.detach()` | Executes the created thread `t` independently of the creator. |
| `t.joinable()` | Returns true if thread `t` is still joinable. |
| `t.get_id()` and | Returns the identity of the thread. |
| `std::this_thread::get_id()` |   |
| `std::thread::hardware_concurrency()` | Indicates the number of threads that can be run concurrently. |
| `std::this_thread::sleep_until(absTime)` | Puts thread `t` to sleep until the time point `absTime`. |
| `std::this_thread::sleep_for(relTime)` | Puts thread `t` to sleep for the time duration `relTime`. |
| `std::this_thread::yield()` | Enables the system to run another thread. |
| `t.swap(t2)` and | Swaps the threads. |
| `std::swap(t1, t2)` |   |

The static method `std::thread::hardware_concurrency` returns the number of concurrent threads supported by the implementation, or 0 if the runtime can not determine the number. This is according to the C++ standard. The `sleep_until` and `sleep_for` operations need a [time point](#chap21.xhtml_chapterXXXTimeSSSPoint) or a [time duration](#chap21.xhtml_chapterXXXTimeSSSDuration) as an argument.

Threads cannot be copied but can be moved. The swap method performs a move when possible.

To conclude this subsection, here are a few of the mentioned methods in practice.

```
 1 // threadMethods.cpp
 2 
 3 #include <iostream>
 4 #include <thread>
 5 
 6 using namespace std;
 7 
 8 int main(){
 9 
10   cout << boolalpha << endl;
11 
12   cout << "hardware_concurrency()= "<< thread::hardware_concurrency() << endl;
13 
14   thread t1([]{cout << "t1 with id= " << this_thread::get_id() << endl;});
15   thread t2([]{cout << "t2 with id= " << this_thread::get_id() << endl;});
16 
17   cout << endl;
18 
19   cout << "FROM MAIN: id of t1 " << t1.get_id() << endl;
20   cout << "FROM MAIN: id of t2 " << t2.get_id() << endl;
21 
22   cout << endl;
23   swap(t1,t2);
24 
25   cout << "FROM MAIN: id of t1 " << t1.get_id() << endl;
26   cout << "FROM MAIN: id of t2 " << t2.get_id() << endl;
27 
28   cout << endl;
29 
30   cout << "FROM MAIN: id of main= " << this_thread::get_id() << endl;
31   
32   cout << endl;
33   
34   cout << "t1.joinable(): " << t1.joinable() << endl;
35   
36   cout << endl;
37 
38   t1.join();
39   t2.join();
40   
41   cout << endl;
42   
43   cout << "t1.joinable(): " << t1.joinable() << endl;
44 
45   cout << endl;
46 
47 }
```

Methods of a thread

In combination with the output, the program should be quite easy to follow.

![Methods of a thread](images/Multithreading----threadMethods.png)

Methods of a thread

Maybe it looks a little weird that threads `t1` and `t2` (lines 14 and 15) run at different points in time of the program execution. You have no guarantee when each thread runs; you only have the guarantee that both threads run before `t1.join()` and `t2.join()` in lines 38 and 39.

The more mutable (non-const) variables threads share, the more challenging multithreading becomes.

### Shared Data

To make the point clear, you only need to think about synchronisation if you have shared, mutable data because shared, mutable data is prone to [data races](#chap20.xhtml_chapterXXXDataSSSRaces). If you have concurrent non-synchronised read and write access to data, your program has undefined behaviour.

The easiest way to visualise concurrent, unsynchronised read and write operations is to write something to `std::cout`.

Let’s have a look.

```
 1 // coutUnsynchronised.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <thread>
 6 
 7 class Worker{
 8 public:
 9   Worker(std::string n):name(n){};
10     void operator() (){
11       for (int i = 1; i <= 3; ++i){
12         // begin work
13         std::this_thread::sleep_for(std::chrono::milliseconds(200));
14         // end work
15         std::cout << name << ": " << "Work " << i << " done !!!" << std::endl;
16       }
17     }
18 private:
19   std::string name;
20 };
21 
22 
23 int main(){
24 
25   std::cout << std::endl;
26   
27   std::cout << "Boss: Let's start working.\n\n";
28  
29   std::thread herb= std::thread(Worker("Herb"));
30   std::thread andrei= std::thread(Worker("  Andrei"));
31   std::thread scott= std::thread(Worker("    Scott"));
32   std::thread bjarne= std::thread(Worker("      Bjarne"));
33   std::thread bart= std::thread(Worker("        Bart"));
34   std::thread jenne= std::thread(Worker("          Jenne"));
35   
36   
37   herb.join();
38   andrei.join();
39   scott.join();
40   bjarne.join();
41   bart.join();
42   jenne.join();
43   
44   std::cout << "\n" << "Boss: Let's go home." << std::endl;
45   
46   std::cout << std::endl;
47   
48 }
```

Writing unsynchronised to `std::cout`

The program describes a workflow. The boss has six workers (lines 29 - 34). Each worker has to take care of 3 work packages. The work package takes 1/5 second (line 13). After the worker is done with his work package, he screams out loudly to the boss (line 15). Once the boss receives notifications from all workers, he sends them home (line 43).

What a mess for such a simple workflow.

![Non-synchronised writing to `std::cout`](images/Multithreading----bossWorker.png)

Non-synchronised writing to `std::cout`

The most straightforward solution is to use a mutex.

#### Mutexes

Mutex stands for **mut**ual **ex**clusion. It ensures that only one thread can access a [critical section](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) at any one time.

By using a mutex, the mess of the workflow turns into a harmony.

```
 1 // coutSynchronised.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 std::mutex coutMutex;
 9 
10 class Worker{
11 public:
12   Worker(std::string n):name(n){};
13  
14     void operator() (){
15       for (int i = 1; i <= 3; ++i){ 
16         // begin work
17         std::this_thread::sleep_for(std::chrono::milliseconds(200));
18         // end work
19         coutMutex.lock();
20         std::cout << name << ": " << "Work " << i << " done !!!" << std::endl;
21         coutMutex.unlock();
22       }
23     }
24 private:
25   std::string name;
26 };
27 
28 
29 int main(){
30 
31   std::cout << std::endl;
32   
33   std::cout << "Boss: Let's start working." << "\n\n";
34  
35   std::thread herb= std::thread(Worker("Herb"));
36   std::thread andrei= std::thread(Worker("  Andrei"));
37   std::thread scott= std::thread(Worker("    Scott"));
38   std::thread bjarne= std::thread(Worker("      Bjarne"));
39   std::thread bart= std::thread(Worker("        Bart"));
40   std::thread jenne= std::thread(Worker("          Jenne"));
41   
42   herb.join();
43   andrei.join();
44   scott.join();
45   bjarne.join();
46   bart.join();
47   jenne.join();
48   
49   std::cout << "\n" << "Boss: Let's go home." << std::endl;
50   
51   std::cout << std::endl;
52 
53 }
```

Writing synchronised to `std::cout`

`std::cout` is protected by the `coutMutex` in line 8\. A simple `lock()` in line 19 and the corresponding `unlock()` call in line 21 ensure that the workers won’t scream all at once.

![Synchronised writing to `std::cout`](images/Multithreading----bossWorkerSynchronized.png)

Synchronised writing to `std::cout`

C++11 has four different exclusive mutexes that can lock recursively, tentative with and without time constraints.

Exclusive mutex variations

| **Method** | **mutex** | **recursive_mutex** | **timed_mutex** | **recursive_timed_mutex** |
| --- | --- | --- | --- | --- |
| `m.lock` | yes | yes | yes | yes |
| `m.try_lock` | yes | yes | yes | yes |
| `m.try_lock_for` |   |   | yes | yes |
| `m.try_lock_until` |   |   | yes | yes |
| `m.unlock` | yes | yes | yes | yes |

A recursive mutex allows the same thread to lock the mutex many times. The mutex stays locked until it was unlocked as many times as it was locked. The maximum number of times that a recursive mutex can be locked is unspecified. If the maximum number is reached, an [std::system_error](http://en.cppreference.com/w/cpp/error/system_error) exception is thrown.

With C++14 we have a `std::shared_timed_mutex` and with C++17 a `std::shared_mutex`. `std::shared_mutex` and `std::shared_timed_mutex` are quite similar. You can use both mutexes for exclusive or shared locking. Additionally, with `std::shared_timed_mutex` you can specify a time point or a time duration.

Shared mutex variations

| **Method** | **shared_timed_mutex** | **shared_mutex** |
| --- | --- | --- |
| `m.lock` | yes | yes |
| `m.try_lock` | yes | yes |
| `m.try_lock_for` | yes |   |
| `m.try_lock_until` | yes |   |
| `m.unlock` | yes | yes |
| `m.lock_shared` | yes | yes |
| `m.try_lock_shared` | yes | yes |
| `m.try_lock_shared_for` | yes |   |
| `m.try_lock_shared_until` | yes |   |
| `m.unlock_shared` | yes | yes |

The `std::shared_timed_mutex`(`std::shared_mutex`) enables you to implement [reader-writer locks](#chap06.xhtml_chapterXXXshared_lock). This means you can use `std::shared_timed_mutex` (`std::shared_mutex`) for exclusive or for shared locking. You get an exclusive lock, if you put the `std::shared_timed_mutex` (`std::shared_mutex`) into a [`std::lock_guard`](#chap06.xhtml_chapterXXXlock_guard) or into a [`std::unique_lock`](#chap06.xhtml_chapterXXXunique_lock); you get a shared lock, if you put the `std::shared_timed_mutex` (`std::shared_lock`) into a [`std::shared_lock`](#chap06.xhtml_chapterXXXshared_lock). The methods `m.try_lock_for(relTime)` and `m.try_lock_shared_for(relTime)`) need a relative [time duration](#chap21.xhtml_chapterXXXTimeSSSDuration); the methods `m.try_lock_until(absTime)` and `m.try_lock_shared_until(absTime)` need an absolute [time point](#chap21.xhtml_chapterXXXTimeSSSPoint).

`m.try_lock` (`m.try_lock_shared`) tries to lock the mutex and returns immediately. On success, it returns true, otherwise false. In contrast the methods `m.try_lock_for` (`m.try_lock_shared_for`) and `m.try_lock_until` (`m.try_lock_shared_until`) try to lock until the specified time out occurs or the lock is acquired, whichever comes first. You should use a [steady clock](#chap21.xhtml_textXXXsystem_clockZZZsteady_clockZZZhigh_resulution_clock) for your time constraint. A steady clock can not be adjusted.

You should not use mutexes directly; you should put mutexes into locks. Here is the reason why.

##### Issues of Mutexes

The issues with mutexes boil down to one main concern: deadlocks.

Deadlock

A deadlock is a state where two or more threads are blocked because each thread waits for the release of a resource before it releases its resource.

The result of a deadlock is a total standstill. The thread that tries to acquire the resource, and usually the whole program is blocked forever. Producing a deadlock is easy. Curious?

###### Exceptions and Unknown Code

The small code snippet has many issues.

```
std::mutex m;
m.lock();
sharedVariable = getVar();
m.unlock();
```

Here are the issues:

1.  If the function `getVar()` throws an exception, the mutex `m` is not released.
2.  **Never ever** call an unknown function while holding a lock. If the function `getVar` tries to lock the mutex `m`, the program has undefined behaviour because `m` is not a recursive mutex. Most of the time, the undefined behaviour causes a deadlock.
3.  Avoid calling a function while holding a lock. Maybe the function is from a library and you get a new version of the library, or the function is rewritten. There is always the danger of a deadlock.

The more locks your program needs, the more challenging it becomes. The dependency is very non-linear.

###### Lock Mutexes in Different Order

Here is a typical scenario of a deadlock resulting from locking in a different order.

![Deadlock of two threads](images/Multithreading----Deadlock.png)

Deadlock of two threads

Thread 1 and thread 2 need access to two resources to finish their work. The problem arises when the requested resources are protected by two separate mutexes and are requested in different orders (Thread 1: Lock 1, Lock 2; Thread 2: Lock 2, Lock 1). In this case, the thread executions interleave in such a way that thread 1 gets mutex 1, then thread 2 gets mutex 2, and we reach a standstill. Each thread wants to get the other’s mutex but to get the other mutex the other thread has to release it first. The expression “deadly embrace” describes this kind of deadlock very well.

Translating this picture into code is easy.

```
 1 // deadlock.cpp
 2 
 3 #include <iostream>
 4 #include <chrono>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 struct CriticalData{
 9   std::mutex mut;
10 };
11 
12 void deadLock(CriticalData& a, CriticalData& b){
13 
14   a.mut.lock();
15   std::cout << "get the first mutex" << std::endl;
16   std::this_thread::sleep_for(std::chrono::milliseconds(1));
17   b.mut.lock();
18   std::cout << "get the second mutex" << std::endl;
19   // do something with a and b
20   a.mut.unlock();
21   b.mut.unlock();
22   
23 }
24 
25 int main(){
26 
27   CriticalData c1;
28   CriticalData c2;
29 
30   std::thread t1([&]{deadLock(c1,c2);});
31   std::thread t2([&]{deadLock(c2,c1);});
32 
33   t1.join();
34   t2.join();
35 
36 }
```

Locking mutexes in different order

Threads `t1` and `t2` call `deadlock` (lines 12 - 23). The function `deadlock` needs variables `CriticalData c1` and `c2` (lines 27 and 28). Because objects `c1` and `c2` have to be protected from shared access, they internally hold a mutex (to keep this example short and simple, `CriticalData` doesn’t have any other methods or members apart from a mutex).

A short sleep of about 1 millisecond in line 16 is sufficient to produce the deadlock.

![Deadlock of two threads](images/Multithreading----deadlockCode.png)

Deadlock of two threads

The only choice left is to press CTRL+C and kill the process.

Locks do not solve all the issues with mutexes, but they come to our rescue in many cases.

#### Locks

Locks take care of their resource following the [RAII](#chap23.xhtml_glossaryXXXRAIISSSBOBOBOGlossaryBCBCBC) idiom. A lock automatically binds its mutex in the constructor and releases it in the destructor. This considerably reduces the risk of a deadlock, because the runtime takes care of the mutex.

Locks are available in four different flavours: `std::lock_guard` for the simple use-cases; `std::unique_lock` for the advanced use-cases. `std::shared_lock` is available since C++14 and can be used to implement reader-writer locks. With C++17 we got the `std::scoped_lock` which can lock more mutexes in an atomic step.

First, the simple use-case.

##### `std::lock_guard`

```
std::mutex m;
m.lock();
sharedVariable = getVar();
m.unlock();
```

The mutex `m` ensures that access to the critical section `sharedVariable = getVar()` is sequential. Sequential means in this special case that each thread gains access to the critical section after the other. This establishes a [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC) in the system. The code is simple but prone to deadlocks. A deadlock may appear if the critical section throws an exception or if the programmer forgets to unlock the mutex. With `std::lock_guard` we can do this more elegantly:

```
{
  std::mutex m,
  std::lock_guard<std::mutex> lockGuard(m);
  sharedVariable = getVar();
}
```

That was easy, but what’s the story with the opening and closing brackets? The lifetime of `std::lock_guard` is limited by its scope and the scope is defined by the curly [brackets](http://en.cppreference.com/w/cpp/language/scope#Block_scope). This means that its lifetime ends when it passes the closing curly brackets. Exactly then, the `std::lock_guard` destructor is called and - as you may have guessed - the mutex is released. This happens automatically and, it happens also if `getVar()` in `sharedVariable = getVar()` throws an exception. A function scope and loop scope also limit the lifetime of an object.

##### `std::scoped_lock`

With C++17 we got the `std::scoped_lock`. It’s very similar to `std::lock_guard`, but `std::scoped_lock` can, additionally, lock an arbitrary number of mutexes atomically. You have to keep a few facts in mind.

1.  If `std::scoped_lock` is invoked with one mutex `m` it behaves such as a `std::lock_guard` and locks the mutex m: `m.lock`. If the `std::scoped_lock` is invoked with more than one mutex (`std::scoped_lock(MutexTypes& ... m`) it uses the function [`std::lock(m ...)`](#chap06.xhtml_textXXXlock).
2.  If one of the current threads already owns the corresponding mutex and the mutex is not recursive, the behaviour is undefined. With high probability, you get a [deadlock](#chap20.xhtml_chapterXXXDeadlocks).
3.  You can just take the ownership of the mutex without locking them. In this case, you have to provide the `std::adopt_lock_t` flag to the constructor: `std::scoped_lock(std::adopt_lock_t, MutexTypes& ... m)`.

You can quite elegantly solve the previous deadlock by using a `std::scoped_lock`. I discuss the resolution of the deadlock in the following section.

##### `std::unique_lock`

A `std::unique_lock` is stronger but more expensive than its little brother `std::lock_guard`.

In addition to what’s offered by a `std::lock_guard`, a `std::unique_lock` enables you to

*   create it without an associated mutex.
*   create it without locking the associated mutex.
*   explicitly and repeatedly set or release the lock of the associated mutex.
*   recursively lock its mutex.
*   move the mutex.
*   try to lock the mutex.
*   delay the lock on the associated mutex.

The following table shows the methods of a `std::unique_lock lk`.

The interface of `std::unique_lock`

| **Method** | **Description** |
| --- | --- |
| `lk.lock()` | Locks the associated mutex. |
| `lk.try_lock()` and | Tries to lock the associated mutex. |
| `lk.try_lock_for(relTime)` and |   |
| `lk.try_lock_until(absTime)` |   |
| `lk.unlock()` | Unlocks the associated mutex. |
| `lk.release()` | Release the mutex. The mutex remains locked. |
| `lk.swap(lk2)` and | Swaps the locks. |
| `std::swap(lk, lk2)` |   |
| `lk.mutex()` | Returns a pointer to the associated mutex. |
| `lk.owns_lock()` and | Checks if the lock `lk` has a locked mutex. |
| `operator bool` |   |

`lk.try_lock_for(relTime)` needs a relative [time duration](#chap21.xhtml_chapterXXXTimeSSSDuration); `lk.try_lock_until(absTime)` an absolute [time point](#chap21.xhtml_chapterXXXTimeSSSPoint). `lk.try_lock_for`(`lk.try_lock_until`) calls effectively the method `mut.try_lock_for`(`mut.try_lock_until`) on the associated mutex `mut`. The associated mutex has to support [exclusive timed blocking](#chap06.xhtml_textXXXmutexZZZrecursive_mutexZZZtimed_mutexZZZrecursive_timed_mutex). You should use a [steady clock](#chap21.xhtml_textXXXsystem_clockZZZsteady_clockZZZhigh_resulution_clock) for your time constraint. A steady clock can not be adjusted.

`lk.try_lock` tries to lock the mutex and returns immediately. On success, it returns true, otherwise false. In contrast, the methods `lk.try_lock_for` and `lk.try_lock_until` the lock `lk` blocks until the specified timeout occurs or the lock is acquired, whichever comes first. All three methods `lk.try_lock`, `lk.try_lock_for`, and `lk.try_lock_until` throw a `std::system_error` exception if there is no associated mutex or if the mutex is already locked by this `std::unique_lock`.

The method `lk.release()` returns the mutex; therefore, you have to unlock it manually.

Thanks to `std::unique_lock`, it is quite easy to lock many mutexes in one atomic step. Therefore you can overcome deadlocks by locking mutexes in a different order. Remember the deadlock from the subsection [Issues of Mutexes](#chap06.xhtml_chapterXXXIssuesSSSofSSSMutexes)?

```
 1 // deadlock.cpp
 2 
 3 #include <iostream>
 4 #include <chrono>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 struct CriticalData{
 9   std::mutex mut;
10 };
11 
12 void deadLock(CriticalData& a, CriticalData& b){
13 
14   a.mut.lock();
15   std::cout << "get the first mutex" << std::endl;
16   std::this_thread::sleep_for(std::chrono::milliseconds(1));
17   b.mut.lock();
18   std::cout << "get the second mutex" << std::endl;
19   // do something with a and b
20   a.mut.unlock();
21   b.mut.unlock();
22   
23 }
24 
25 int main(){
26 
27   CriticalData c1;
28   CriticalData c2;
29 
30   std::thread t1([&]{deadLock(c1,c2);});
31   std::thread t2([&]{deadLock(c2,c1);});
32 
33   t1.join();
34   t2.join();
35 
36 }
```

Locking mutexes in different order

Let’s solve the issue. The function `deadLock` has to lock its mutexes atomically, and that’s exactly what happens in the following example.

```
 1 // deadlockResolved.cpp
 2 
 3 #include <iostream>
 4 #include <chrono>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 using namespace std;
 9 
10 struct CriticalData{
11   mutex mut;
12 };
13 
14 void deadLock(CriticalData& a, CriticalData& b){
15 
16   unique_lock<mutex> guard1(a.mut,defer_lock);
17   cout << "Thread: " << this_thread::get_id() << " first mutex" << endl;
18 
19   this_thread::sleep_for(chrono::milliseconds(1));
20 
21   unique_lock<mutex> guard2(b.mut,defer_lock);
22   cout << "  Thread: " << this_thread::get_id() << " second mutex" <<  endl;
23 
24   cout << "    Thread: " << this_thread::get_id() << " get both mutex" << endl;
25   lock(guard1,guard2);
26   // do something with a and b
27 }
28 
29 int main(){
30 
31   cout << endl;
32 
33   CriticalData c1;
34   CriticalData c2;
35 
36   thread t1([&]{deadLock(c1,c2);});
37   thread t2([&]{deadLock(c2,c1);});
38 
39   t1.join();
40   t2.join();
41 
42   cout << endl;
43 
44 }
```

Delayed locking of mutexes

If you call the constructor of `std::unique_lock` with `std::defer_lock`, the underlying mutex is not locked automatically. At this point (lines 16 and 21), the `std::unique_lock` is just the owner of the mutex. Thanks to the variadic template [`std::lock`](#chap06.xhtml_textXXXlock), the lock operation is performed in an atomic step (line 25).

In this example, `std::unique_lock` manages the lifetime of the resources and `std::lock` locks the associated mutex. You can do it the other way around. In the first step the mutexes are locked, in the second `std::unique_lock` manages the lifetime of resources. Here is an example of the second approach.

```
std::lock(a.mut, b.mut);
std::lock_guard<std::mutex> guard1(a.mut, std::adopt_lock);
std::lock_guard<std::mutex> guard2(b.mut, std::adopt_lock);
```

Both variants resolve the deadlock.

![Deadlock resolved with `std::unique_lock`](images/Multithreading----deadlockResolved.png)

Deadlock resolved with `std::unique_lock`

##### `std::shared_lock`

With C++14, C++ adds support for `std::shared_lock`.

A `std::shared_lock` has the same interface as a `std::unique_lock` but behaves differently when used with a `std::shared_timed_mutex` or a `std::shared_mutex`. Many threads can share one `std::shared_timed_mutex` (`std::shared_mutex`) and, therefore, implement a reader-writer lock. The idea of reader-writer locks is straightforward and extremely useful. An arbitrary number of threads executing read operations can access the critical region at the same time, but only one thread is allowed to write.

Reader-writer locks do not solve the fundamental problem - threads competing for access to a critical region, but they do help to minimise the bottleneck.

A telephone book is a typical example using a reader-writer lock. Usually, many people want to look up a telephone number, but only a few want to change them. Let’s look at an example.

```
 1 // readerWriterLock.cpp
 2 
 3 #include <iostream>
 4 #include <map>
 5 #include <shared_mutex>
 6 #include <string>
 7 #include <thread>
 8 
 9 std::map<std::string,int> teleBook{{"Dijkstra", 1972}, {"Scott", 1976}, 
10                                    {"Ritchie", 1983}};
11 
12 std::shared_timed_mutex teleBookMutex;
13 
14 void addToTeleBook(const std::string& na, int tele){
15   std::lock_guard<std::shared_timed_mutex> writerLock(teleBookMutex);
16   std::cout << "\nSTARTING UPDATE " << na;
17   std::this_thread::sleep_for(std::chrono::milliseconds(500));
18   teleBook[na]= tele;
19   std::cout << " ... ENDING UPDATE " << na << std::endl;
20 }
21 
22 void printNumber(const std::string& na){
23   std::shared_lock<std::shared_timed_mutex> readerLock(teleBookMutex);
24   std::cout << na << ": " << teleBook[na];
25 }
26 
27 int main(){
28 
29   std::cout << std::endl;
30 
31   std::thread reader1([]{ printNumber("Scott"); });
32   std::thread reader2([]{ printNumber("Ritchie"); });
33   std::thread w1([]{ addToTeleBook("Scott",1968); });
34   std::thread reader3([]{ printNumber("Dijkstra"); });
35   std::thread reader4([]{ printNumber("Scott"); });
36   std::thread w2([]{ addToTeleBook("Bjarne",1965); });
37   std::thread reader5([]{ printNumber("Scott"); });
38   std::thread reader6([]{ printNumber("Ritchie"); });
39   std::thread reader7([]{ printNumber("Scott"); });
40   std::thread reader8([]{ printNumber("Bjarne"); });
41 
42   reader1.join();
43   reader2.join();
44   reader3.join();
45   reader4.join();
46   reader5.join();
47   reader6.join();
48   reader7.join();
49   reader8.join();
50   w1.join();
51   w2.join();
52 
53   std::cout << std::endl;
54 
55   std::cout << "\nThe new telephone book" << std::endl;
56   for (auto teleIt: teleBook){
57     std::cout << teleIt.first << ": " << teleIt.second << std::endl;
58   }
59 
60   std::cout << std::endl;
61 
62 }
```

Reader-writer locks

The telephone book in line 9 is the shared variable, which has to be protected. Eight threads want to read the telephone book; two threads want to modify it (lines 31 - 40). To access the telephone book at the same time, the reading threads use the `std::shared_lock<std::shared_timed_mutex>>` in line 23\. This is in contrast to the writing threads, which need exclusive access to the critical section. The exclusivity is given by the `std::lock_guard<std::shared_timed_mutex>>` in line 15\. At the end, the program displays the updated telephone book (lines 55 - 58).

![Reader-writer lock for reading and writing of a telephone book](images/Multithreading----readerWriterLocks.png)

Reader-writer lock for reading and writing of a telephone book

The screenshot shows that the output of the reading threads overlaps, while the writing threads are executed one after the other. This means that the reading operations are performed at the same time.

That was easy. Too easy. The telephone book has undefined behaviour.

###### Undefined behaviour

The program has undefined behaviour. To be more precise it has a [data race](#chap20.xhtml_chapterXXXDataSSSRaces). What? Before you continue, stop for a few seconds and think. By the way the concurrent access to `std::cout` is not the issue.

The characteristic of a data race is that at least two threads access the shared variable at the same time and at least one of them is a writer. This exact scenario may occur during program execution. One of the features of the associative container is that reading of the container using the index operator can modify it. This happens if the element is not available in the container. If “Bjarne” is not found in the telephone book, a pair (“Bjarne”, 0) is created from the read access. You can force the data race by putting the printing of Bjarne in line 40 in front of all the threads (lines 31 - 40). Let’s have a look.

You can see it right at the top, Bjarne has the value 0.

![The program has a data race](images/Multithreading----readerWriterLocksDataRace.png)

The program has a data race

An obvious way to fix this issue is to use only reading operations in the function `printNumber`:

```
 1 // readerWriterLocksResolved.cpp
 2 
 3 ...
 4 
 5 void printNumber(const std::string& na){
 6   std::shared_lock<std::shared_timed_mutex> readerLock(teleBookMutex);
 7   auto searchEntry = teleBook.find(na);
 8   if(searchEntry != teleBook.end()){
 9     std::cout << searchEntry->first << ": " << searchEntry->second << std::endl;
10   }
11   else {
12     std::cout << na << " not found!" << std::endl;
13   }
14 }
15 
16 ...
17 
18 }
```

Reader-writer locks resolved

If a key is not in the telephone book, I just write the key and the text `not found!` to the console.

![Data race resolved](images/Multithreading----readerWriterLocksResolved.png)

Data race resolved

You can see the message `Bjarne not found!` in the output of the second program execution. In the first program execution, `addToTeleBook` is executed first; therefore, Bjarne is found.

#### Thread-safe Initialisation

If the variable is never modified there is no need for synchronisation by using an expensive lock or an atomic. You only have to ensure that it is initialised in a thread-safe way.

There are three ways in C++ to initialise variables in a thread-safe way.

*   Constant expressions
*   The function `std::call_once` in combination with the flag `std::once_flag`
*   A static variable with block scope

##### Constant Expressions

Constant expressions are expressions that the compiler can evaluate at compile time. They are implicitly thread-safe. Placing the keyword `constexpr` in front of a variable makes the variable a constant expression. The constant expression must be initialised immediately.

```
constexpr double pi = 3.14;
```

Besides, user defined types can also be constant expressions. For those types there are a few restrictions that must be met to initialise it at compile time.

*   They must not have virtual methods or a virtual base class.
*   Their constructor must be empty and itself be a constant expression.
*   Every base class and each non-static member must be initialized.
*   Their methods, which should be callable at compile time, must be constant expressions.

Instances of `MyDouble` satisfy all these requirements. So it is possible to instantiate them at compile time. This instantiation is thread-safe.

```
 1 // constexpr.cpp
 2 
 3 #include <iostream>
 4 
 5 class MyDouble{
 6   private:
 7     double myVal1;
 8     double myVal2;
 9   public:
10     constexpr MyDouble(double v1, double v2): myVal1(v1), myVal2(v2){}
11     constexpr double getSum() const { return myVal1 + myVal2; }
12 };
13 
14 int main() {
15 
16   constexpr double myStatVal = 2.0;
17   constexpr MyDouble myStatic(10.5, myStatVal);
18   constexpr double sumStat = myStatic.getSum();
19 
20 }
```

User defined constant expressions

##### `std::call_once` and `std::once_flag`

By using the `std::call_once` function, you can register a callable. The `std::once_flag` ensures that only one registered function is invoked. You can register additional functions via the same `std::once_flag`. Only one function from that group is called.

`std::call_once` obeys the following rules:

*   Exactly one execution of exactly one of the functions is performed. It is undefined which function is selected for execution. The selected function runs in the same thread as the `std::call_once` invocation it was passed to.
*   No invocation in the group returns before the above-mentioned execution of the selected function completes successfully.
*   If the selected function exits via an exception, it is propagated to the caller. Another function is then selected and executed.

The short example demonstrates the application of `std::call_once` and the `std::once_flag`. Both of them are declared in the header `<mutex>`.

```
 1 // callOnce.cpp
 2 
 3 #include <iostream>
 4 #include <thread>
 5 #include <mutex>
 6  
 7 std::once_flag onceFlag;
 8  
 9 void do_once(){
10   std::call_once(onceFlag, [](){ std::cout << "Only once." << std::endl; });
11 }
12 
13 void do_once2(){
14   std::call_once(onceFlag, [](){ std::cout << "Only once2." << std::endl; });
15 }
16  
17 int main(){
18   
19   std::cout << std::endl;
20   
21   std::thread t1(do_once);
22   std::thread t2(do_once);
23   std::thread t3(do_once2);
24   std::thread t4(do_once2);
25  
26   t1.join();
27   t2.join();
28   t3.join();
29   t4.join();
30   
31   std::cout << std::endl;
32 
33 }
```

User defined constant expressions

The program starts with four threads (lines 21 - 24). Two of them invoke `do_once` and the other two `do_once2`. The expected result is that the string “Only once” or the string “Only once2” is displayed only once.

![Usage of `std::call_once` and `std::once_flag`](images/Multithreading----callOnce.png)

Usage of `std::call_once` and `std::once_flag`

The famous singleton pattern guarantees that only one instance of a class is created. This is a challenging task in multithreading environments. Thanks to `std::call_once` and `std::once_flag` the job is a piece of cake.

Now the singleton is initialised in a thread-safe way.

```
 1 // singletonCallOnce.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 
 6 using namespace std;
 7 
 8 class MySingleton{
 9 
10   private:
11     static once_flag initInstanceFlag;
12     static MySingleton* instance;
13     MySingleton() = default;
14     ~MySingleton() = default;
15 
16   public:
17     MySingleton(const MySingleton&) = delete;
18     MySingleton& operator=(const MySingleton&) = delete;
19 
20     static MySingleton* getInstance(){
21       call_once(initInstanceFlag, MySingleton::initSingleton);
22       return instance;
23     }
24 
25     static void initSingleton(){
26       instance = new MySingleton();
27     }
28 };
29 
30 MySingleton* MySingleton::instance = nullptr;
31 once_flag MySingleton::initInstanceFlag;
32 
33 int main(){
34 
35   cout << endl;
36 
37   cout << "MySingleton::getInstance(): "<< MySingleton::getInstance() << endl;
38   cout << "MySingleton::getInstance(): "<< MySingleton::getInstance() << endl;
39 
40   cout << endl;
41 
42 }
```

Singleton pattern with `std::call_once` and the `std::once_flag`

Let’s first review the static flag `initInstanceFlag`. It is declared in line 11 and initialised in line 31\. The static method `getInstance` (lines 20 - 23) uses the flag `initInstanceFlag` to ensure that the static method `initSingleton` (line 25 - 27) is executed exactly once. The singleton is created in the body of the method.

The `MySingleton::getIstance()` method displays the address of the singleton.

![Thread-safe implementation of the singleton with `std::call_once` and `std::once_flag`](images/Multithreading----singletonCallOnce.png)

Thread-safe implementation of the singleton with `std::call_once` and `std::once_flag`

##### Static Variables with Block Scope

Static variables with block scope are created exactly once and lazily. Lazily means that they are created just at the moment of the usage. This characteristic is the basis of the so-called Meyers Singleton, named after [Scott Meyers](https://en.wikipedia.org/wiki/Scott_Meyers). This is by far the most elegant implementation of the singleton pattern in C++. With C++11, static variables with block scope have an additional guarantee; they are initialised in a thread-safe way.

Here is the thread-safe Meyers Singleton pattern.

```
 1 // meyersSingleton.cpp
 2 
 3 class MySingleton{
 4 public:
 5   static MySingleton& getInstance(){
 6     static MySingleton instance;
 7     return instance;
 8   }
 9 private:
10   MySingleton();
11   ~MySingleton();
12   MySingleton(const MySingleton&)= delete;
13   MySingleton& operator=(const MySingleton&)= delete;
14 
15 };
16 
17 MySingleton::MySingleton()= default;
18 MySingleton::~MySingleton()= default;
19 
20 int main(){
21 
22   MySingleton::getInstance();
23 
24 }
```

The thread-safe Meyers Singleton pattern

`thread_local` data has no sharing issues.

### Thread-Local Data

Thread-local data, also known as thread-local storage, is created for each thread separately. It behaves like static data because it’s bound for the lifetime of the thread and is created at its first usage. This means exactly that thread-local variables at namespace scope or as static class members are created before its first use and that thread-local variables declared in a function are created with its first use. Thread-local data belongs exclusively to the thread.

```
 1 // threadLocal.cpp
 2 
 3 #include <iostream>
 4 #include <string>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 std::mutex coutMutex;
 9 
10 thread_local std::string s("hello from ");
11 
12 void addThreadLocal(std::string const& s2){
13 
14   s += s2;
15   // protect std::cout
16   std::lock_guard<std::mutex> guard(coutMutex);
17   std::cout << s << std::endl;
18   std::cout << "&s: " << &s << std::endl;
19   std::cout << std::endl;
20 
21 }
22 
23 int main(){
24 
25   std::cout << std::endl;
26 
27   std::thread t1(addThreadLocal,"t1"); 
28   std::thread t2(addThreadLocal,"t2"); 
29   std::thread t3(addThreadLocal,"t3"); 
30   std::thread t4(addThreadLocal,"t4"); 
31 
32   t1.join();
33   t2.join();
34   t3.join();
35   t4.join();
36 
37 }
```

Thread-local data

By using the keyword `thread_local` in line 10, the `thread-local` string `s` is created. Threads t1 - t4 (lines 27 - 30) use the function `addThreadLocal` (lines 12 - 21) as their work package. Threads get as their argument the strings `t1` to `t4` respectively, and add them to the thread-local string `s`. Also, `addThreadLocal` displays the address of `s` in line 18.

![Thread-local data](images/Multithreading----threadLocal.png)

Thread-local data

The output of the program shows it implicitly in line 17 and explicitly in line 18\. The thread-local string is created for each string `s`. First, each output shows a new thread-local string, second, each string `s` has a different address.

I often discuss in my seminars: What is the difference between a `static`, a `thread_local`, and a local variable? A `static` variable is bound to the lifetime of the main thread, a `thread_local` variable is bound to the lifetime of its thread, and a local variable is bound to the lifetime of the scope in which it was created. Here is a variation of the previous program `threadLocal.cpp` to make my point clear.

```
 1 // threadLocalState.cpp
 2 
 3 #include <iostream>
 4 #include <string>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 std::mutex coutMutex;
 9 
10 thread_local std::string s("hello from ");
11 
12 void first(){
13     s += "first ";
14 }
15 
16 void second(){
17     s += "second ";
18 }
19 
20 void third(){
21     s += "third";
22 }
23 
24 void addThreadLocal(std::string const& s2){
25 
26   s += s2;
27 
28   first();
29   second();
30   third();
31   // protect std::cout
32   std::lock_guard<std::mutex> guard(coutMutex);
33   std::cout << s << std::endl;
34   std::cout << "&s: " << &s << std::endl;
35   std::cout << std::endl;
36 
37 }
38 
39 int main(){
40 
41   std::cout << std::endl;
42 
43   std::thread t1(addThreadLocal,"t1: "); 
44   std::thread t2(addThreadLocal,"t2: "); 
45   std::thread t3(addThreadLocal,"t3: "); 
46   std::thread t4(addThreadLocal,"t4: "); 
47 
48   t1.join();
49   t2.join();
50   t3.join();
51   t4.join();
52 
53 }
```

State between function calls

In this variation to the previous program, the function `addThreadLocal` (line 24) invokes the functions `first`, `second`, and `third`. Each of the function uses the `thread_local` string `s` to add its function name. The key point of this variation is that the string `s` is used as a kind of thread-local state between the function calls `first`, `second`, and `third` (lines 28 - 30). The output shows that the strings are independent.

![Thread-local data](images/Multithreading----threadLocalState.png)

Thread-local data

In contrast to thread-local data, condition variables are not easy to use.

### Condition Variables

Condition variables enable threads to be synchronised via messages. They need the `<condition_variable>` header. One thread acts as a sender, and the other as a receiver of the message. The receiver waits for the notification from the sender. Typical use cases for condition variables are sender-receiver or producer-consumer workflows.

A condition variable can be the sender but also the receiver of the message.

The methods of the condition variable cv

| **Method** | **Description** |
| --- | --- |
| `cv.notify_one()` | Notifies a waiting thread. |
| `cv.notify_all()` | Notifies all waiting threads. |
| `cv.wait(lock, ...)` | Waits for the notification while holding a `std::unique_lock`. |
| `cv.wait_for(lock, relTime, ...)` | Waits for a time duration for the notification while holding a `std::unique_lock`. |
| `cv.wait_until(lock, absTime, ...)` | Waits until a time point for the notification while holding a `std::unique_lock`. |
| `cv.native_handle()` | Returns the native handle of this condition variable. |

The subtle difference between `cv.notify_one` and `cv.notify_all` is that `cv.notify_all` notifies all waiting threads. In contrast, `cv.notify_one` notifies only one of the waiting threads. The other condition variables does stay in the wait state. Before we cover the gory details - which are the three dots in the wait operations - of condition variables, here is an example.

```
 1 // conditionVariable.cpp
 2 
 3 #include <iostream>
 4 #include <condition_variable>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 std::mutex mutex_;
 9 std::condition_variable condVar;
10 
11 bool dataReady{false};
12 
13 void doTheWork(){
14   std::cout << "Processing shared data." << std::endl;
15 }
16 
17 void waitingForWork(){
18     std::cout << "Worker: Waiting for work." << std::endl;
19     std::unique_lock<std::mutex> lck(mutex_);
20     condVar.wait(lck, []{ return dataReady; });
21     doTheWork();
22     std::cout << "Work done." << std::endl;
23 }
24 
25 void setDataReady(){
26     {
27       std::lock_guard<std::mutex> lck(mutex_);
28       dataReady = true;
29     }
30     std::cout << "Sender: Data is ready."  << std::endl;
31     condVar.notify_one();
32 }
33 
34 int main(){
35 
36   std::cout << std::endl;
37 
38   std::thread t1(waitingForWork);
39   std::thread t2(setDataReady);
40 
41   t1.join();
42   t2.join();
43 
44   std::cout << std::endl;
45   
46 }
```

First usage of condition variables

The program has two child threads: `t1` and `t2`. They get their work package `waitingForWork` and `setDataRead` in lines 38 and 39. `setDataReady` notifies - using the condition variable `condVar` - that it is done with the preparation of the work: `condVar.notify_one()`. While holding the lock, thread `t1` waits for its notification: `condVar.wait(lck, []{ return dataReady; })`. The sender and receiver need a lock. In the case of the sender a `std::lock_guard` is sufficient, because it calls lock and unlock only once. In the case of the receiver, a `std::unique_lock` is necessary because it frequently locks and unlocks its mutex.

Here is the output of the program.

![Sychronisation of two threads with condition variables](images/Multithreading----conditionVariable.png)

Sychronisation of two threads with condition variables

#### The Predicate

Maybe you are wondering why you need a predicate for the `wait` call because you can invoke `wait` without a predicate. Let’s try it out.

```
 1 // conditionVariableBlock.cpp
 2 
 3 #include <iostream>
 4 #include <condition_variable>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 std::mutex mutex_;
 9 std::condition_variable condVar;
10 
11 void waitingForWork(){
12 
13     std::cout << "Worker: Waiting for work." << std::endl;
14 
15     std::unique_lock<std::mutex> lck(mutex_);
16     condVar.wait(lck);                          
17     // do the work
18     std::cout << "Work done." << std::endl;
19 
20 }
21 
22 void setDataReady(){
23 
24     std::cout << "Sender: Data is ready."  << std::endl;
25     condVar.notify_one();                        
26 
27 }
28 
29 int main(){
30 
31   std::cout << std::endl;
32 
33   std::thread t1(setDataReady);
34   std::thread t2(waitingForWork);               
35 
36   t1.join();
37   t2.join();
38 
39   std::cout << std::endl;
40   
41 }
```

Blocking condition variables

The first invocation of the program seems to work fine. The second invocation locks because the notification call (line 25) happens before thread `t2` (line 34) enters its waiting state (line 16).

![Deadlock with condition variables](images/Multithreading----conditionVariableBlock.png)

Deadlock with condition variables

Now it is clear. The predicate is a kind of memory for the stateless condition variable; therefore, the wait call always checks the predicate at first. Condition variables are victim to two known phenomena: lost wakeup and spurious wakeup.

#### Lost Wakeup and Spurious Wakeup

**Lost Wakeup**

The phenomenon of the lost wakeup is that the sender sends its notification before the receiver gets to its wait state. The consequence is that the notification is lost. The C++ standard describes condition variables as a simultaneous synchronisation mechanism: “The condition_variable class is a synchronisation primitive that can be used to block a thread, or multiple threads **at the same time**, …”. So the notification gets lost, and the receiver is waiting and waiting and … .

**Spurious Wakeup**

It may happen that the receiver wakes up, although no notification happened. At a minimum [POSIX Threads](https://en.wikipedia.org/wiki/POSIX_Threads) and the [Windows API](https://en.wikipedia.org/wiki/Windows_API) can be victims of these phenomena. One reason for a spurious wakeup can be a stolen wakeup. This means, before the awoken thread gets the chance to run, another thread kicks in and runs.

#### The Wait Workflow

The waiting thread has quite a complicated workflow.

Here are the two key lines 19 and 20 from the previous example `conditionVariable.cpp`.

```
std::unique_lock<std::mutex> lck(mutex_);
condVar.wait(lck, []{ return dataReady; });
```

The two lines are equivalent to the following four lines:

```
std::unique_lock<std::mutex> lck(mutex_);
while ( ![]{ return dataReady; }() {
    condVar.wait(lck);
}
```

First, you have to distinguish between the first call of `std::unique_lock<std::mutex> lck(mutex_)` and the notification of the condition variable: `condVar.wait(lck)`.

*   **`std::unique_lock<std::mutex> lck(mutex_)`**: In the initial processing, the thread locks the mutex and then check the predicate `[]{ return dataReady; }`.
    *   If the call of the predicated evaluates to
        *   **`true`**: the thread continues its work.
        *   **`false`**: `condVar.wait()` unlocks the mutex and puts the thread in a waiting (blocking) state
*   **`condVar.wait(lck)`**: If the condition_variable `condVar` is in the waiting state and gets a notification or a spurious wakeup the following steps happen.
    *   The thread is unblocked and reacquires the lock on the mutex.
    *   The thread checks the predicate.
    *   If the call of the predicated evaluates to
        *   **`true`**: the thread continues its work.
        *   **`false`**: `condVar.wait()` unlocks the mutex and puts the thread in a waiting (blocking) state.

Even if the shared variable is atomic, it must be modified under the mutex to publish the modification to the waiting thread correctly.

In most of the use-cases, tasks are the less error-prone way to synchronise threads. I compare condition variables and tasks in the section [Returning a Notification](#chap06.xhtml_chapterXXXReturningSSSaSSSNotification).

### Tasks

In addition to threads, C++ has tasks to perform work asynchronously. Tasks need the `<future>` header. A task is parameterised with a work package, and consists of the two associated components: a promise and a future. Both are connected via a data channel. The promise executes the work packages and puts the result in the data channel; the associated future picks up the result. Both communication endpoints can run in separate threads. It is special that the future can pick up the result at a later time; therefore, the calculation of the result by the promise is independent of the query of the result by the associated future.

![Tasks as data channels between communication endpoints](images/Multithreading----tasks.png)

Tasks as data channels between communication endpoints

#### Tasks versus Threads

Tasks are very different threads.

```
 1 // asyncVersusThread.cpp
 2 
 3 #include <future>
 4 #include <thread>
 5 #include <iostream>
 6 
 7 int main(){
 8 
 9   std::cout << std::endl;
10 
11   int res;
12   std::thread t([&]{ res = 2000 + 11; });
13   t.join();
14   std::cout << "res: " << res << std::endl;             
15 
16   auto fut= std::async([]{ return 2000 + 11; });
17   std::cout << "fut.get(): " << fut.get() << std::endl;   
18 
19   std::cout << std::endl;   
20 
21 }
```

`std:async` versus threads

The child thread `t` and the asynchronous function call `std::async` calculate both the sum of `2000` and `11`. The creator thread gets the result from its child thread `t` via the shared variable `res` and displays it in line 14\. The call `std::async` in line 16 creates the data channel between the sender (promise) and the receiver (future). The future asks the data channel with `fut.get()` (line 17) for the result of the calculation. This `fut.get` call is blocking.

Here is the output of the program.

![Tasks versus threads](images/Multithreading----asyncVersusThreads.png)

Tasks versus threads

Based on this program, I want to emphasise the differences between threads and tasks explicitly.

Tasks versus threads

| **Criteria** | **Threads** | **Tasks** |
| --- | --- | --- |
| Participants | creator and child thread | promise and future |
| Communication | shared variable | communication channel |
| Thread creation | obligatory | optional |
| Synchronisation | via `join()` (waits) | `get` call blocks |
| Exception in child thread | child and creator threads terminates | return value of the promise |
| Kinds of communication | values | values, notifications, and exceptions |

Threads need the `<thread>` header; tasks the `<future>` header.

Communication between the creator thread and the created thread requires the use of a shared variable. The task communicates via its implicitly protected data channel; therefore, a task must not use a protection mechanism like a [mutex](#chap06.xhtml_chapterXXXmutex).

While you can *misuse* a shared mutable variable to communicate between the child and its creator, the communication of a task is more explicit. The future can request the result of the task only once (by calling `fut.get()`). Calling it more than once results in undefined behaviour. This is not true for a [`std::shared_future`](#chap06.xhtml_chapterXXXshared_future), which can be queried multiple times.

The creator thread waits for its child with the call to `join`. The future `fut` uses the `fut.get()` call which blocks until the result is available.

If an exception is thrown in the created thread, the created thread terminates and so the creator and the whole process. In contrast, the promise can send the exception to the future, which has to handle the exception.

A promise can serve one or many futures. It can send a value, an exception, or just a notification. You can use them as a safe replacement for a condition variable.

`std::async` is the easiest way to create a future.

#### `std::async`

`std::async` behaves like an asynchronous function call. This function call takes a [callable](#chap06.xhtml_glossaryXXXCallableSSSUnitSSSBOBOBOGlossaryBCBCBC) together with its arguments. `std::async` is a variadic template and can, therefore, take an arbitrary number of arguments. The call to `std::async` returns a future object `fut`. That’s your handle on getting the result via `fut.get()`.

Optionally you can specify a start policy for `std::async`.

##### The Start Policy

With the start policy you can explicitly specify whether the asynchronous call should be executed in the same thread (`std::launch::deferred`) or in another thread (`std::launch::async`).

It is special about the call `auto fut = std::async(std::launch::deferred, ... )` that the promise is not be executed immediately. The call `fut.get()` starts the promise lazily. This means that the promise only runs if the future asks via `fut.get()` for the result.

```
 1 // asyncLazy.cpp
 2 
 3 #include <chrono>
 4 #include <future>
 5 #include <iostream>
 6 
 7 int main(){
 8 
 9   std::cout << std::endl;
10 
11   auto begin= std::chrono::system_clock::now();
12 
13   auto asyncLazy=std::async(std::launch::deferred,
14                             []{ return std::chrono::system_clock::now(); });
15 
16   auto asyncEager=std::async(std::launch::async,
17                              []{ return std::chrono::system_clock::now(); });
18 
19   std::this_thread::sleep_for(std::chrono::seconds(1));
20 
21   auto lazyStart= asyncLazy.get() - begin;
22   auto eagerStart= asyncEager.get() - begin;
23 
24   auto lazyDuration= std::chrono::duration<double>(lazyStart).count();
25   auto eagerDuration=  std::chrono::duration<double>(eagerStart).count();
26 
27   std::cout << "asyncLazy evaluated after : " << lazyDuration 
28             << " seconds." << std::endl;
29   std::cout << "asyncEager evaluated after: " << eagerDuration 
30             << " seconds." << std::endl;
31 
32   std::cout << std::endl;
33 
34 }
```

Eager and lazy evaluation of a future

Both `std::async` calls (lines 13 and 16) return the current [time point](#chap21.xhtml_chapterXXXTimeSSSPoint). However, the first call is lazy while the second eager. The short sleep of one second in line 19 makes that obvious. The call `asyncLazy.get()` in line 21 triggers the execution of the promise in line 13 - the result is available after a short nap of one second (line 19). This is not true for `asyncEager`. `asyncEager.get()` which gets the result from the immediately executed work package.

Here are the numbers.

![Lazy versus eager evaluation](images/Multithreading----asyncLazy.png)

Lazy versus eager evaluation

You do not have to bind a future to a variable.

##### Fire and Forget

Fire and forget futures are special futures. They execute just in place because their future is not bound to a variable. It is necessary for a fire and forget future that the promise runs in a separate thread so it can immediately start its work. This is done by the `std::launch::async` policy.

Let’s compare an ordinary future with a fire and forget future.

```
auto fut= std::async([]{ return 2011; });
std::cout << fut.get() << std::endl;         

std::async(std::launch::async, 
           []{ std::cout << "fire and forget" << std::endl; });
```

Fire and forget futures look very promising but have a big drawback. A future that is created by `std::async` waits on its destructor, until its promise is done. In this context, waiting is not very different from blocking. The future blocks the progress of the program in its destructor. This becomes more evident, when you use fire and forget futures. What seems to be concurrent actually runs sequentially.

```
 1 // fireAndForgetFutures.cpp
 2 
 3 #include <chrono>
 4 #include <future>
 5 #include <iostream>
 6 #include <thread>
 7 
 8 int main(){
 9 
10   std::cout << std::endl;
11 
12   std::async(std::launch::async, []{
13       std::this_thread::sleep_for(std::chrono::seconds(2));
14       std::cout << "first thread" << std::endl;
15     });
16     
17   std::async(std::launch::async, []{
18       std::this_thread::sleep_for(std::chrono::seconds(1));  
19       std::cout << "second thread" << std::endl;}
20     );
21   
22   std::cout << "main thread" << std::endl;  
23 
24   std::cout << std::endl;
25 
26 }
```

Fire and forget futures

The program executes two promises in their threads. The resulting futures are fire and forget futures. These futures block in their destructors until the associated promise is done. The result is that the promises is executed in the sequence which you find in the source code. The execution sequence is independent of the execution time. This is precisely what you see in the output of the program.

![Fire and forget futures](images/Multithreading----fireAndForgetFutures.png)

Fire and forget futures

`std::async` is a convenient mechanism used to distribute a bigger compute job on more shoulders.

##### Concurrent Calculation

The calculation of the scalar product can be spread across four asynchronous function calls.

```
 1 // dotProductAsync.cpp
 2 
 3 #include <iostream>
 4 #include <future>
 5 #include <random>
 6 #include <vector>
 7 #include <numeric>
 8 
 9 using namespace std;
10 
11 static const int NUM= 100000000;
12 
13 long long getDotProduct(vector<int>& v, vector<int>& w){
14   
15   auto vSize = v.size();
16 
17   auto future1 = async([&]{ 
18     return inner_product(&v[0], &v[vSize/4], &w[0], 0LL); 
19   });
20   
21   auto future2 = async([&]{ 
22     return inner_product(&v[vSize/4], &v[vSize/2], &w[vSize/4], 0LL); 
23   });
24   
25   auto future3 = async([&]{ 
26     return inner_product(&v[vSize/2], &v[vSize* 3/4], &w[vSize/2], 0LL);
27   });
28   
29   auto future4 = async([&]{ 
30     return inner_product(&v[vSize * 3/4], &v[vSize], &w[vSize * 3/4], 0LL); 
31   });
32 
33   return future1.get() + future2.get() + future3.get() + future4.get();
34 }
35 
36 
37 int main(){
38 
39   cout << endl;
40 
41   random_device seed;
42 
43   // generator
44   mt19937 engine(seed());
45 
46   // distribution
47   uniform_int_distribution<int> dist(0, 100);
48 
49   // fill the vectors
50   vector<int> v, w;
51   v.reserve(NUM);
52   w.reserve(NUM);
53   for (int i=0; i< NUM; ++i){
54     v.push_back(dist(engine));
55     w.push_back(dist(engine));
56   }
57 
58   cout << "getDotProduct(v, w): " << getDotProduct(v, w) << endl;
59 
60   cout << endl;
61 
62 }
```

Dot product with four futures

The program uses the functionality of the random and the time libraries. Both libraries are part of C++11\. The two vectors `v` and `w` are created and filled with random numbers (lines 50 - 56). Each of the vectors gets (lines 53 - 56) one hundred million elements. `dist(engine)` in lines 54 and 55 generates the random numbers, which are uniformly distributed in the range 0 to 100\. The calculation of the scalar product takes place in `getDotProduct` (lines 13 - 34). Internally, `std::async` uses the standard template library algorithm `std::inner_product`. The return statement sums up the results of the futures.

![Scalar product with four asynchronous function calls](images/Multithreading----dotProductAsync.png)

Scalar product with four asynchronous function calls

`std::packaged_task` is also usually used to perform a concurrent computation.

#### `std::packaged_task`

`std::packaged_task` `pack` is a wrapper for a [callable](#chap06.xhtml_glossaryXXXCallableSSSUnitSSSBOBOBOGlossaryBCBCBC) in order to be invoked asynchronously. By calling `pack.get_future()` you get the associated future. Invoking the call operator on pack (`pack()`) executes the `std::packaged_task` and, therefore, executes the callable.

Dealing with `std::packaged_task` usually consists of four steps:

I. Wrap your work:

```
 std::packaged_task<int(int, int)> sumTask([](int a, int b){ return a + b; });
```

II. Create a future:

```
 std::future<int> sumResult= sumTask.get_future();
```

III. Perform the calculation:

```
 sumTask(2000, 11);
```

IV. Query the result:

```
 sumResult.get();
```

Here is an example showing the four steps.

```
 1 // packagedTask.cpp
 2 
 3 #include <utility>
 4 #include <future>
 5 #include <iostream>
 6 #include <thread>
 7 #include <deque>
 8 
 9 class SumUp{
10   public:
11     int operator()(int beg, int end){
12       long long int sum{0};
13       for (int i = beg; i < end; ++i ) sum += i;
14       return sum;
15     }
16 };
17 
18 int main(){
19 
20   std::cout << std::endl;
21 
22   SumUp sumUp1;
23   SumUp sumUp2;
24   SumUp sumUp3;
25   SumUp sumUp4;
26 
27   // wrap the tasks
28   std::packaged_task<int(int, int)> sumTask1(sumUp1);
29   std::packaged_task<int(int, int)> sumTask2(sumUp2);
30   std::packaged_task<int(int, int)> sumTask3(sumUp3);
31   std::packaged_task<int(int, int)> sumTask4(sumUp4);
32 
33   // create the futures
34   std::future<int> sumResult1 = sumTask1.get_future();
35   std::future<int> sumResult2 = sumTask2.get_future();
36   std::future<int> sumResult3 = sumTask3.get_future();
37   std::future<int> sumResult4 = sumTask4.get_future();
38 
39   // push the tasks on the container
40   std::deque<std::packaged_task<int(int,int)>> allTasks;
41   allTasks.push_back(std::move(sumTask1));
42   allTasks.push_back(std::move(sumTask2));
43   allTasks.push_back(std::move(sumTask3));
44   allTasks.push_back(std::move(sumTask4));
45   
46   int begin{1};
47   int increment{2500};
48   int end = begin + increment;
49 
50   // perform each calculation in a separate thread
51   while (not allTasks.empty()){
52     std::packaged_task<int(int, int)> myTask = std::move(allTasks.front());
53     allTasks.pop_front();
54     std::thread sumThread(std::move(myTask), begin, end);
55     begin = end;
56     end += increment;
57     sumThread.detach();
58   }
59 
60   // pick up the results
61   auto sum = sumResult1.get() + sumResult2.get() + 
62              sumResult3.get() + sumResult4.get();
63 
64   std::cout << "sum of 0 .. 10000 = " << sum << std::endl;
65 
66   std::cout << std::endl;
67 
68 }
```

Concurrency with `std::packaged_task`

The purpose of the program is it to calculate the sum of all numbers from 0 to 10000 - with the help of four `std::packaged_task` each running in a separate thread. The associated futures are used, to sum up the final result. Of course, you can use the [Gaußschen Summenformel](https://de.wikipedia.org/wiki/Gau%C3%9Fsche_Summenformel). Strange, I didn’t find an English web page.

I. **Wrap the tasks**: I pack the work packages in `std::packaged_task` (lines 28 - 31) objects. Work packages are instances of the class `SumUp` (lines 9 - 16). The work is done in the call operator (lines 11 - 15). The call operator sums up all numbers from `beg` to `end - 1` and returns the sum as the result. `std::packaged_task` in lines 28 - 31 can deal with callables that need two `int`s and return an `int`: `int(int, int)`.

II. **Create the futures**: I have to create the future objects with the help of `std::packaged_task` objects. This is done in the lines 34 to 37\. The `packaged_task` is the promise in the communication channel. The type of the future is defined explicitly: `std::future<int> sumResult1 = sumTask1.get_future()`, but the compiler can do that job for me: `auto sumResult1 = sumTask1.get_future()`.

III. **Perform the calculations**: Now the calculation takes place. The `packaged_task` are moved onto the [`std::deque`](http://en.cppreference.com/w/cpp/container/deque) (lines 40 - 44). In the while loop, each `packaged_task` (lines 51 - 58) is executed. For doing that, I move the head of the `std::deque` in a `std::packaged_task` (line 52), move the `packaged_task` in a new thread (line 54) and let it run in the background (line 57). `std::packaged_task` objects are not copyable. That’s the reason I used the move semantic in lines 52 and 54\. This restriction holds for all promises, but also for futures and threads. There is one exception to this rule: [std::shared_future](#chap06.xhtml_chapterXXXshared_future).

IV. **Pick up the results**: In the final step I ask all futures for their value and sum them up (line 61).

Here is the overall result of the concurrent computation.

![Summation with `std::packaged_task`](images/Multithreading----packagedTask.png)

Summation with `std::packaged_task`

The following table shows the interface of an`std::packaged_task pack`.

The methods of the `std::packaged_task`

| **Method** | **Description** |
| --- | --- |
| `pack.swap(pack2)` and | Swaps the task objects. |
| `std::swap(pack, pack2)` |   |
| `pack.valid()` | Checks if the task object has a valid function. |
| `pack.get_future()` | Returns the future. |
| `pack.make_ready_at_thread_exit(ex)` | Executes the function. The result is available if the current thread exists. |
| `pack.reset()` | Resets the state of the task. Abandons the stored results from previous executions. |

A `std::packaged_task` can be in contrast to a `std::async`, or a `std::promise` reset and resused. The following example shows this special use-case on a `std::packaged_task`.

```
 1 // packagedTaskReuse.cpp
 2 
 3 #include <functional>
 4 #include <future>
 5 #include <iostream>
 6 #include <utility>
 7 #include <vector>
 8 
 9 void calcProducts(std::packaged_task<int(int, int)>& task, 
10                   const std::vector<std::pair<int, int>>& pairs){
11     for (auto& pair: pairs){
12         auto fut = task.get_future();
13         task(pair.first, pair.second); 
14         std::cout << pair.first << " * " << pair.second << " = " <<  fut.get() 
15                   << std::endl;
16         task.reset();
17     }
18 }
19     
20 int main(){
21 
22     std::cout << std::endl;
23 
24     std::vector<std::pair<int, int>> allPairs;
25     allPairs.push_back(std::make_pair(1, 2));
26     allPairs.push_back(std::make_pair(2, 3));
27     allPairs.push_back(std::make_pair(3, 4));
28     allPairs.push_back(std::make_pair(4, 5));
29     
30     std::packaged_task<int(int, int)> task{[](int fir, int sec){ 
31         return fir * sec; }
32     }; 
33     
34     calcProducts(task, allPairs);
35     
36     std::cout << std::endl;
37     
38     std::thread t(calcProducts, std::ref(task), allPairs);
39     t.join();
40     
41     std::cout << std::endl;
42     
43 }
```

Reuse of a `std::packaged_task`

The function `calcProduct` (line 9) gets two arguments: the task and the vector of int-pairs. It uses the task to calculate for each int-pair the product (line 13). In the end, the task is reset in line 16\. `calcProduct` runs in the main-thread (line 34) and in a separate thread (line 38). Here is the output of the program.

![Reuse of a `std::packaged_task`](images/Multithreading----packagedTaskReuse.png)

Reuse of a `std::packaged_task`

#### `std::promise` and `std::future`

The class templates `std::promise` and `std::future` provide you with the full control over the task.

Promise and future are a mighty pair. A promise can put a value, an exception, or simply a notification into the shared data channel. One promise can serve many `std::shared_future` futures. With C++20/23 we may get [extended futures](#chap10.xhtml_chapterXXXExtendedSSSFutures) that are composable.

Here is an introductory example of the usage of `std::promise` and `std::future`. Both communication endpoints can be moved to separate threads, so the communication takes place between threads.

```
 1 // promiseFuture.cpp
 2 
 3 #include <future>
 4 #include <iostream>
 5 #include <thread>
 6 #include <utility>
 7 
 8 void product(std::promise<int>&& intPromise, int a, int b){
 9   intPromise.set_value(a*b);
10 }
11 
12 struct Div{
13 
14   void operator() (std::promise<int>&& intPromise, int a, int b) const {
15     intPromise.set_value(a/b);
16   }
17 
18 };
19 
20 int main(){
21 
22   int a = 20;
23   int b = 10;
24 
25   std::cout << std::endl;
26 
27   // define the promises
28   std::promise<int> prodPromise;
29   std::promise<int> divPromise;
30 
31   // get the futures
32   std::future<int> prodResult = prodPromise.get_future();
33   std::future<int> divResult = divPromise.get_future();
34 
35   // calculate the result in a separate thread
36   std::thread prodThread(product, std::move(prodPromise), a, b);
37   Div div;
38   std::thread divThread(div, std::move(divPromise), a, b);
39 
40   // get the result
41   std::cout << "20*10 = " << prodResult.get() << std::endl;
42   std::cout << "20/10 = " << divResult.get() << std::endl;
43 
44   prodThread.join();
45   
46   divThread.join();
47 
48   std::cout << std::endl;
49   
50 }
```

Usage of `std::promise` and `std::future`

Thread `prodThread` (line 36) gets the function `product` (lines 8 -10), the `prodPromise` (line 32) and the numbers `a` and `b`. To understand the arguments of `prodThread`, you have to look at the signature of the function. `prodThread` needs as its first argument a [callable](#chap06.xhtml_glossaryXXXCallableSSSUnitSSSBOBOBOGlossaryBCBCBC). This is the previously mentioned function `product`. The function `product` requires a promise of the kind rvalue reference (`std::promise<int>&& intPromise`) and two numbers. These are the last three arguments of `prodThread`. `std::move` in line 36 creates an rvalue reference. The rest is a piece of cake. `divThread` (line 38) divides the two numbers `a` and `b`. For its work, it uses the instance `div` of the class `Div` (lines 12 - 18). `div` is an instance of a function object.

The future picks up the results by calling `prodResult.get()` and `divResult.get()`.

![Division and multiplikation with tasks](images/Multithreading----promiseFuture.png)

Division and multiplikation with tasks

##### `std::promise`

`std::promise` enables you to set a value, a notification, or an exception. In addition the promise can provide its result in a delayed fashion.

The methods of the `std::promise` prom

| **Method** | **Description** |
| --- | --- |
| `prom.swap(prom2)` and | Swaps the promises. |
| `std::swap(prom, prom2)` |   |
| `prom.get_future()` | Returns the future. |
| `prom.set_value(val)` | Sets the value. |
| `prom.set_exception(ex)` | Sets the exception. |
| `prom.set_value_at_thread_exit(val)` | Stores the value and makes it ready if the promise exits. |
| `prom.set_exception_at_thread_exit(ex)` | Stores the exception and makes it ready if the promise exits. |

If the promise sets the value or the exception more then once, a `std::future_error` exception is thrown.

##### `std::future`

A `std::future` enables you to

*   pick up the value from the promise.
*   ask the promise if the value is available.
*   wait for the notification of the promise. This waiting can be done with a relative time duration or an absolute time point.
*   create a shared future (std::shared_future).

The methods of the future `fut`

| **Method** | **Description** |
| --- | --- |
| `fut.share()` | Returns a `std::shared_future`. After calling `fut.share()`, `fut.valid()` returns `false`. |
| `fut.get()` | Returns the result which can be a value or an exception. |
| `fut.valid()` | Checks if the shared state is available. After calling `fut.get()` it returns `false`. |
| `fut.wait()` | Waits for the result. |
| `fut.wait_for(relTime)` | Waits for the result, but not longer than for a `relTime`. Returns a `std::future_status`. |
| `fut.wait_until(absTime)` | Waits for the result, but not longer than until `abstime`. Returns a `std::future_status`. |

In contrast to the `wait` call, the `wait_for`and `wait_until` variants return the statuts of the future.

###### `std::future_status`

The `wait_for` and `wait_until` calls of the future and a [shared future](#chap06.xhtml_chapterXXXshared_future) return its state. Three states are possible:

```
enum class future_status {
    ready,
    timeout,
    deferred
};
```

State of a future or a shared future

The following table describe each possible state:

The state of a future or a shared future

| **State** | **Description** |
| --- | --- |
| `deferred` | The function has not been started. |
| `ready` | The result is ready. |
| `timeout` | The timeout has expired. |

Thanks to the `wait_for` or `wait_until` variants of a future, your future can wait until its associated promise is done.

```
 1 // waitFor.cpp
 2 
 3 #include <iostream>
 4 #include <future>
 5 #include <thread>
 6 #include <chrono>
 7 
 8 using namespace std::literals::chrono_literals;
 9 
10 void getAnswer(std::promise<int> intPromise){
11     std::this_thread::sleep_for(3s);
12     intPromise.set_value(42);
13 }
14  
15 int main(){
16 	
17 	std::cout << std::endl;
18 
19     std::promise<int> answerPromise;
20     auto fut = answerPromise.get_future();	
21 	
22 	std::thread prodThread(getAnswer, std::move(answerPromise));
23 	
24 	std::future_status status{};
25 	do{
26         status = fut.wait_for(0.2s);
27 		std::cout << "... doing something else" << std::endl;
28 	} while (status != std::future_status::ready);
29     
30     std::cout << std::endl;
31  
32     std::cout << "The Answer: " << fut.get() << '\n';
33     
34     prodThread.join();
35 	
36 	std::cout << std::endl;
37 }
```

Waiting for the promise

While the future `fut` is waiting for the promise, it can perform *something else*.

![Waiting for the promise](images/Multithreading----waitFor.png)

Waiting for the promise

If a future `fut` asks for the result more than once, a `std::future_error` exception is thrown.

There is a one-to-one relationship between the promise and the future. In contrast, `std::shared_future` supports a one-to-many relationship between a promise and many futures.

#### `std::shared_future`

There are two ways to create a `std::shared future`.

1.  You can take the future from the Promise `prom` by a `std::shared_future`: `std::shared_future<int> fut = prom.get_future()`.
2.  You can either invoke `fut.share()` on a future `fut`. After the `fut.share()` call `fut.valid()` returns `false`.

A shared future is associated with its promise and can independently ask for the result. A `std::shared future` has the same interface as a `std::future`.

In addition to the `std::future`, a `std::shared_future` enables you to query the promise independently of the other associated futures.

The handling of a `std::shared_future` is special. The following program creates directly a `std::shared_future`.

```
 1 // sharedFuture.cpp
 2 
 3 #include <future>
 4 #include <iostream>
 5 #include <thread>
 6 #include <utility>
 7 
 8 std::mutex coutMutex;
 9 
10 struct Div{
11 
12   void operator()(std::promise<int>&& intPromise, int a, int b){
13     intPromise.set_value(a/b);
14   }
15 
16 };
17 
18 struct Requestor{
19 
20   void operator ()(std::shared_future<int> shaFut){
21 
22     // lock std::cout
23     std::lock_guard<std::mutex> coutGuard(coutMutex);
24 
25     // get the thread id
26     std::cout << "threadId(" << std::this_thread::get_id() << "): " ;
27     
28     std::cout << "20/10= " << shaFut.get() << std::endl;
29 
30   }
31 
32 };
33 
34 int main(){
35 
36   std::cout << std::endl;
37 
38   // define the promises
39   std::promise<int> divPromise;
40 
41   // get the futures
42   std::shared_future<int> divResult = divPromise.get_future();
43 
44   // calculate the result in a separat thread
45   Div div;
46   std::thread divThread(div, std::move(divPromise), 20, 10);
47 
48   Requestor req;
49   std::thread sharedThread1(req, divResult);
50   std::thread sharedThread2(req, divResult);
51   std::thread sharedThread3(req, divResult);
52   std::thread sharedThread4(req, divResult);
53   std::thread sharedThread5(req, divResult);
54 
55   divThread.join();
56 
57   sharedThread1.join();
58   sharedThread2.join();
59   sharedThread3.join();
60   sharedThread4.join();
61   sharedThread5.join();
62 
63   std::cout << std::endl;
64 
65 }
```

Taking a future with a `std::shared_future`

Both work packages of the promise and the future are function objects in this current example. In line 46 `divPromise` is moved and executed in thread `divThread`. Accordingly, `std::shared_future`’s are copied in all five threads (lines 57 - 61). It’s important to emphasise it once more. In contrast to a `std::future` object that can only be moved, you can copy a `std::shared_future` object.

The main thread waits in lines 57 to 61 for its child threads to finish their jobs and to display their the results.

![Taking a `std::shared_future`](images/Multithreading----sharedFuture.png)

Taking a `std::shared_future`

As I previously mentioned it you can create a `std::shared_future` from a `std::future` by using its method `share`.

```
 1 // sharedFutureFromFuture.cpp
 2 
 3 #include <future>
 4 #include <iostream>
 5 #include <thread>
 6 #include <utility>
 7 
 8 std::mutex coutMutex;
 9 
10 struct Div{
11 
12   void operator()(std::promise<int>&& intPromise, int a, int b){
13     intPromise.set_value(a/b);
14   }
15 
16 };
17 
18 struct Requestor{
19 
20   void operator ()(std::shared_future<int> shaFut){
21 
22     // lock std::cout
23     std::lock_guard<std::mutex> coutGuard(coutMutex);
24 
25     // get the thread id
26     std::cout << "threadId(" << std::this_thread::get_id() << "): " ;
27     
28     std::cout << "20/10= " << shaFut.get() << std::endl;
29 
30   }
31 
32 };
33 
34 int main(){
35 
36   std::cout << std::boolalpha << std::endl;
37 
38   // define the promises
39   std::promise<int> divPromise;
40 
41   // get the future
42   std::future<int> divResult = divPromise.get_future();
43   
44   std::cout << "divResult.valid(): " << divResult.valid() << std::endl;
45   
46   // calculate the result in a separat thread
47   Div div;
48   std::thread divThread(div, std::move(divPromise), 20, 10);
49   
50   std::cout << "divResult.valid(): " << divResult.valid() << std::endl;
51   
52   std::shared_future<int> sharedResult = divResult.share();
53   
54   std::cout << "divResult.valid(): " << divResult.valid() << "\n\n";
55 
56   Requestor req;
57   std::thread sharedThread1(req, sharedResult);
58   std::thread sharedThread2(req, sharedResult);
59   std::thread sharedThread3(req, sharedResult);
60   std::thread sharedThread4(req, sharedResult);
61   std::thread sharedThread5(req, sharedResult);
62 
63   divThread.join();
64 
65   sharedThread1.join();
66   sharedThread2.join();
67   sharedThread3.join();
68   sharedThread4.join();
69   sharedThread5.join();
70 
71   std::cout << std::endl;
72 
73 }
```

Creating a `std::shared_future` from a `std::future`

The first two calls of `divResult.valid()` on the `std::future` (lines 44 and 50) return `true`. This change after the call `divResult.share()` in line 52 because this call transfers the shared state.

![Creating a `std::shared_future`](images/Multithreading----sharedFutureFromFuture.png)

Creating a `std::shared_future`

#### Exceptions

If the callable used by `std::async` or by `std::packaged_task` throws an error, the exception is store in the shared state. When the future `fut` then calls `fut.get()`, the exception is rethrown, and the future has to handle it.

A `std::promise prom` provides the same facility but has the method `prom.set_value(std::current_exception())` to set the exception as shared state.

Dividing a number by 0 is undefined behaviour. The function `executeDivision` displays the result of the calculation or the exception.

```
 1 // promiseFutureException.cpp
 2 
 3 #include <exception>
 4 #include <future>
 5 #include <iostream>
 6 #include <thread>
 7 #include <utility>
 8 
 9 struct Div{
10   void operator()(std::promise<int>&& intPromise, int a, int b){
11     try{
12       if ( b==0 ){
13           std::string errMess = std::string("Illegal division by zero: ") + 
14                                 std::to_string(a) + "/" + std::to_string(b);
15           throw std::runtime_error(errMess);
16       }
17       intPromise.set_value(a/b);
18     }
19     catch (...){
20       intPromise.set_exception(std::current_exception());
21     }
22   }
23 };
24 
25 void executeDivision(int nom, int denom){
26   std::promise<int> divPromise;
27   std::future<int> divResult= divPromise.get_future();
28   
29   Div div;
30   std::thread divThread(div,std::move(divPromise), nom, denom);
31 
32   // get the result or the exception
33   try{
34     std::cout << nom << "/" << denom << " = " << divResult.get() << std::endl;
35   }
36   catch (std::runtime_error& e){
37     std::cout << e.what() << std::endl;
38   }
39 
40   divThread.join();
41 }
42 
43 int main(){
44     
45   std::cout << std::endl;
46     
47   executeDivision(20, 0);
48   executeDivision(20, 10);
49   
50   std::cout << std::endl;
51     
52 }
```

Returning an exception

The promise deals with the issue that the denominator is 0\. If the denominator is 0, it sets the exception as return value: `intPromise.set_exception(std::current_exception())` in line 20\. The future has to deal with the exception in its try-catch block (lines 33 - 38).

Here is the output of the program.

![Exception handling with `std::promise` and `std::future`](images/Multithreading----promiseFutureException.png)

Exception handling with `std::promise` and `std::future`

If you destroy the `std::promise` without calling the `set`-method or a `std::packaged_task` before invoking it, a `std::future_error` exception with an error code `std::future_errc::broken_promise` would be stored in the shared state.

#### Notifications

Tasks are a save replacement for condition variables. If you use promises and futures to synchronise threads, they have a lot in common with condition variables. Most of the time, promises and futures are the better choices.

Before I present you an example, here is the big picture.

Condition variables versus tasks

| **Criteria** | **Condition Variables** | **Tasks** |
| --- | --- | --- |
| Multiple synchronisations | Yes | No |
| Critical section | Yes | No |
| Error handling in receiver | No | Yes |
| Spurious wakeup | Yes | No |
| Lost wakeup | Yes | No |

The advantage of a condition variable to a promise and future is that you can use condition variables to synchronise threads multiple times. In contrast to that, a promise can send its notification only once, so you have to use more promise and future pairs to get the functionality of a condition variable. If you use the condition variable for only one synchronisation, the condition variable is a lot more challenging to use in the right way. A promise and future pair needs no shared variable and therefore no lock, and is not prone to spurious or lost wakeups. In addition to that, tasks can handle exceptions. There are lots of reasons to prefer tasks to condition variables.

Do you remember how difficult it was to use [condition variables](#chap06.xhtml_chapterXXXConditionSSSVariables)? If not here are the key parts required to synchronise two threads.

```
void waitingForWork(){
    std::cout << "Worker: Waiting for work." << std::endl;

    std::unique_lock<std::mutex> lck(mutex_);
    condVar.wait(lck, []{ return dataReady; });
    doTheWork();
    std::cout << "Work done." << std::endl;
}

void setDataReady(){
    std::lock_guard<std::mutex> lck(mutex_);
    dataReady=true;
    std::cout << "Sender: Data is ready."  << std::endl;
    condVar.notify_one();
}
```

The function `setDataReady` performs the notification part of the synchronisation - the function `waitingForWork` the waiting part of the synchronisation.

Here is the same workflow with tasks.

```
 1 // promiseFutureSynchronise.cpp
 2 
 3 #include <future>
 4 #include <iostream>
 5 #include <utility>
 6 
 7 void doTheWork(){
 8   std::cout << "Processing shared data." << std::endl;
 9 }
10 
11 void waitingForWork(std::future<void>&& fut){
12 
13     std::cout << "Worker: Waiting for work." << std::endl;
14     fut.wait();
15     doTheWork();
16     std::cout << "Work done." << std::endl;
17 
18 }
19 
20 void setDataReady(std::promise<void>&& prom){
21 
22     std::cout << "Sender: Data is ready."  << std::endl;
23     prom.set_value();
24 
25 }
26 
27 int main(){
28 
29   std::cout << std::endl;
30 
31   std::promise<void> sendReady;
32   auto fut = sendReady.get_future();
33 
34   std::thread t1(waitingForWork, std::move(fut));
35   std::thread t2(setDataReady, std::move(sendReady));
36 
37   t1.join();
38   t2.join();
39 
40   std::cout << std::endl;
41   
42 }
```

Thread synchronisation with tasks

That was quite easy.

Thanks to `sendReady` (line 32) you get a future `fut` (line 33). The promise communicates using its return value `void` (`std::promise<void> sendReady`) that it is only capable of sending notifications. Both communication endpoints are moved into threads `t1` and `t2` (lines 35 and 36). The future waits using the call `fut.wait()` (line 15) for the notification of the promise: `prom.set_value()` (line 24).

The structure and the output of the program matches the corresponding program in the section [condition variable](#chap06.xhtml_chapterXXXConditionSSSVariables).

![`std::promise` and `std::future` as condition variable](images/Multithreading----promiseFutureSynchronise.png)

`std::promise` and `std::future` as condition variable

## Parallel Algorithms of the Standard Template Library

The Standard Template Library has more than 100 algorithms for searching, counting, and manipulation of ranges and their elements. With C++17, 69 of them get new overloads and eight new ones are added. The overloaded, and new algorithms can be invoked with a so-called execution policy.

![Parallel algorithms of C++17](images/timeline----timeline17.png)

Parallel algorithms of C++17

By using an execution policy, you can specify whether the algorithm should run sequentially, in parallel, or parallel with vectorisation. For using the execution policy, you have to include the header `<execution>`.

### Execution Policies

The standard defines three execution policies:

*   **`std::execution::sequenced_policy`**
*   **`std::execution::parallel_policy`**
*   **`std::execution::parallel_unsequenced_policy`**

The corresponding policy tag specifies whether a program should run sequentially, in parallel, or parallel with vectorisation.

*   **`std::execution::seq`**: runs the program sequentially
*   **`std::execution::par`**: runs the program in parallel on multiple threads
*   **`std::execution::par_unseq`**: runs the program in parallel on multiple threads and allows the interleaving of individual loops; permits a vectorised version with [SIMD](https://en.wikipedia.org/wiki/SIMD) (**S**ingle **I**nstruction **M**ultiple **D**ata) extensions.

The usage of the execution policy `std::execution::par` or `std::execution::par_unseq` allows the algorithm to run parallel or parallel and vectorised. This policy is a permission and not a requirement.

The following code snippet applies all execution policies.

```
 1 std::vector<int> v = {1, 2, 3, 4, 5, 6, 7, 8, 9};
 2 
 3 // standard sequential sort
 4 std::sort(v.begin(), v.end());
 5 
 6 // sequential execution
 7 std::sort(std::execution::seq, v.begin(), v.end());
 8 
 9 // permitting parallel execution
10 std::sort(std::execution::par, v.begin(), v.end());
11 
12 // permitting parallel and vectorised execution
13 std::sort(std::execution::par_unseq, v.begin(), v.end());
```

The execution policy

The example shows that you can still use the classic variant of `std::sort` (line 4). Besides, in C++17 you can specify explicitly whether the sequential (line 7), parallel (line 10), or the parallel and vectorised (line 13) version should be used.

Thanks to `std::is_execution_policy` you can check, whether `T` is a standard or implementation-defined execution policy type: `std::is_execution_policy<T>::value`. The function checks whether T is a standard or implementation-defined execution policy type. The expression evaluates to `true`,if `T` is `std::execution::sequenced_policy`, `std::execution::parallel_policy`, `std::execution::parallel_unsequenced_policy`, or an implementation-defined execution policy type. Otherwise, value is equal to `false`.

#### Parallel and Vectorised Execution

Whether an algorithm runs in a parallel and vectorised way depends on many factors. For example, it depends on whether the CPU and the operating system support SIMD instructions. Additionally, it also depends on the compiler and the optimisation level that you used to translate your code.

The following example shows a simple loop for filling a vector.

```
 1 const int SIZE= 8;
 2  
 3 int vec[] = {1, 2, 3, 4, 5, 6, 7, 8};
 4 int res[] = {0, 0, 0, 0, 0, 0, 0, 0};
 5  
 6 int main(){
 7     for (int i = 0; i < SIZE; ++i) {
 8         res[i] = vec[i]+5;
 9     }
10 }
```

Filling a vector

Line 8 is the crucial line in this small example. Thanks to the [compiler explorer](https://godbolt.org/) we can have a closer look at the assembler instructions generated by clang 3.6.

##### Without Optimisation

Here are the assembler instructions. Each addition is done sequentially.

![Sequential execution](images/ParallelSTL----seq.png)

Sequential execution

##### With Maximum Optimisation

By using the highest optimisation level, `-O3`, special registers such as `xmm0` are used that can hold 128 bits or 4 `int`s. This special register means that the addition takes place in parallel on four elements of the vector.

![Vectorised execution](images/ParallelSTL----vec.png)

Vectorised execution

An overload of an algorithm without an execution policy and an overload of an algorithm with a sequential execution policy `std::execution::seq` differ in one aspect: exceptions.

#### Exceptions

If an exception occurs during the usage of an algorithm with an execution policy, [`std::terminate`](https://en.cppreference.com/w/cpp/error/terminate) is called. `std::terminate` calls the installed [`std::terminate_handler`](https://en.cppreference.com/w/cpp/error/terminate_handler). The consequence is that per default [`std::abort`](https://en.cppreference.com/w/cpp/utility/program/abort) is called, which causes abnormal program termination. The handling of exceptions is the difference between the invocation of an algorithm without an execution policy and an algorithm with a sequential `std::execution::seq` execution policy. The invocation of the algorithm without an execution policy propagates the exception and, therefore, the exception can be handled. The program `exceptionExecutionPolicy.cpp` shows my point.

```
 1 // exceptionExecutionPolicy.cpp
 2 
 3 #include <algorithm>
 4 #include <execution>
 5 #include <iostream>
 6 #include <stdexcept>
 7 #include <string>
 8 #include <vector>
 9 
10 int main(){
11 	
12     std::cout << std::endl;
13 
14     std::vector<int> myVec{1, 2, 3, 4, 5};
15 
16     try{
17         std::for_each(myVec.begin(), myVec.end(),
18             [](int){ throw std::runtime_error("Without execution policy"); }
19         );
20     }
21     catch(const std::runtime_error& e){
22         std::cout << e.what() << std::endl;
23     }
24     
25     try{
26         std::for_each(std::execution::seq, myVec.begin(), myVec.end(),
27             [](int){ throw std::runtime_error("With execution policy"); }
28         );
29     }
30     catch(const std::runtime_error& e){
31         std::cout << e.what() << std::endl;
32     }
33     catch(...){
34         std::cout << "Catch-all exceptions" << std::endl;
35     }
36     
37 }
```

Exceptions with execution policies

The exception handler in line 21 catches the exception `std::runtime_error` but doesn’t work with the exception handler in line 30 or even in line 33 with a catch-all exception handler.

With a new MSVC compiler and the flag `std:c++latest`, the program gives the expected output.

![The new algorithms](images/ParallelSTL----exceptionExecutionPolicy.PNG)

The new algorithms

Only the first exception handler is executed.

#### Hazards of Data Races and Deadlocks

The parallel algorithm does not automatically protect you from [data races](#chap20.xhtml_chapterXXXDataSSSRaces) and [deadlocks](#chap20.xhtml_chapterXXXDeadlocks).

```
std::vector<int> v = {1, 2, 3 };
int sum = 0;

std::for_each(std::execution::par, v.begin(), v.end(), [&sum](int i){
    sum += i + i;
});
```

Parallel execution with a data race

The small code snippet has a data race on `sum`. `sum` builds the sum of all `i + i` and is concurrently modified. `sum` has to be protected.

```
std::vector<int> v = {1, 2, 3 };
int sum = 0;
std::mutex m;

std::for_each(std::execution::par, v.begin(), v.end(), [&sum](int i){
    std::lock_guard<std::mutex> lock(m);
    sum += i + i;
});
```

Parallel execution

When I change the execution policy to `std::execution::par_unseq`, I have a race condition that usually results in a deadlock.

```
std::vector<int> v = {1, 2, 3 };
int sum = 0;
std::mutex m;

std::for_each(std::execution::par_unseq, v.begin(), v.end(), [&sum](int i){
    std::lock_guard<std::mutex> lock(m);
    sum += i + i;
});
```

Parallel and vectorised execution with a deadlock

The lambda function may result in two consecutive calls of `m.lock` on the same thread. Two times trying to lock a non-recursive `std::mutex` is undefined behaviour and gives most of the times a deadlock. You can avoid the deadlock by using an atomic.

```
std::vector<int> v = {1, 2, 3 };
std::atomic<int> sum = 0;
std::mutex m;
std::for_each(std::execution::par_unseq, v.begin(), v.end(), [&sum](int i){
    sum += i + i;
});
```

Parallel and vectorised execution without a deadlock

Because `sum` is an atomic counter, relaxed semantic is also fine: `sum.fetch_add(i * i, std::memory_order_relaxed);`.

69 of the STL algorithms can be parametrised with an execution policy. Additionally, C++17 has 8 new algorithms.

### Algorithms

Here are the 69 algorithms with parallelised versions.

The 69 algorithms with parallelised versions

| std::adjacent_difference | std::adjacent_find | std::all_of | std::any_of |
| std::copy | std::copy_if | std::copy_n | std::count |
| std::count_if | std::equal | std::fill | std::fill_n |
| std::find | std::find_end | std::find_first_of | std::find_if |
| std::find_if_not | std::generate | std::generate_n | std::includes |
| std::inner_product | std::inplace_merge | std::is_heap | std::is_heap_until |
| std::is_partitioned | std::is_sorted | std::is_sorted_until | std::lexicographical_compare |
| std::max_element | std::merge | std::min_element | std::minmax_element |
| std::mismatch | std::move | std::none_of | std::nth_element |
| std::partial_sort | std::partial_sort_copy | std::partition | std::partition_copy |
| std::remove | std::remove_copy | std::remove_copy_if | std::remove_if |
| std::replace | std::replace_copy | std::replace_copy_if | std::replace_if |
| std::reverse | std::reverse_copy | std::rotate | std::rotate_copy |
| std::search | std::search_n | std::set_difference | std::set_intersection |
| std::set_symmetric_difference | std::set_union | std::sort | std::stable_partition |
| std::stable_sort | std::swap_ranges | std::transform | std::uninitialized_copy |
| std::uninitialized_copy_n | std::uninitialized_fill | std::uninitialized_fill_n | std::unique |
| std::unique_copy |   |   |   |

Besides, we get eight new algorithms.

### The New Algorithms

The new algorithms are in the `std` namespace. The algorithms `std::for_each` and `std::for_each_n` require the header `<algorithm>`. The remaining six other algorithms require the header `<numeric>`.

Here is an overview of the new algorithms.

The new algorithms

| **Algorithm** | **Description** |
| --- | --- |
| `std::for_each` | Applies a unary [callable](#chap23.xhtml_glossaryXXXCallableSSSUnitZZZcallableSSSBOBOBOGlossaryBCBCBC) to the range. |
| `std::for_each_n` | Applies a unary callable to the first n elements of the range. |
| `std::exclusive_scan` | Applies from the left a binary callable up to the ith (exclusive) element of the range. The left argument of the callable is the previous result. Stores intermediate results. If the binary callable is non-[associative](#chap23.xhtml_glossaryXXXassociativeSSSBOBOBOGlossaryBCBCBC) the result is non-deterministic. |
|   | Similar to [`std::partial_sum`](http://en.cppreference.com/w/cpp/algorithm/partial_sum) |
| `std::inclusive_scan` | Applies from the left a binary callable up to the ith (inclusive) element of the range. The left argument of the callable is the previous result. Stores intermediate results. If the binary callable is non-[associative](#chap23.xhtml_glossaryXXXassociativeSSSBOBOBOGlossaryBCBCBC) the result is non-deterministic. |
|   | Similar to `std::partial_sum` |
| `std::transform_exclusive_scan` | First applies a unary callable to the range and then applies `std::exclusive_scan`. If the binary callable is non-[associative](#chap23.xhtml_glossaryXXXassociativeSSSBOBOBOGlossaryBCBCBC) the result is non-deterministic. |
| `std::transform_inclusive_scan` | First applies a unary callable to the range and then applies `std::inclusive_scan`. If the binary callable is non-[associative](#chap23.xhtml_glossaryXXXassociativeSSSBOBOBOGlossaryBCBCBC) the result is non-deterministic. |
| `std::reduce` | Applies from the left a binary callable to the range. If the binary callable is non-[associative](#chap23.xhtml_glossaryXXXassociativeSSSBOBOBOGlossaryBCBCBC) or non-[commutative](#chap23.xhtml_glossaryXXXcommutativeSSSBOBOBOGlossaryBCBCBC) the result is non-deterministic. |
|   | Similar to [`std::accumulate`](http://en.cppreference.com/w/cpp/algorithm/accumulate) |
| `std::transform_reduce` | Applies first a unary callable to the range and then `std::reduce`. If the binary callables are non-[associative](#chap23.xhtml_glossaryXXXassociativeSSSBOBOBOGlossaryBCBCBC) or non-[commutative](#chap23.xhtml_glossaryXXXcommutativeSSSBOBOBOGlossaryBCBCBC) the result is non-deterministic. |

Admittedly this description is not easy to digest but if you already know `std::accumulate` and `std::partial_sum`, the reduce and scan variations should be quite familiar. `reduce` is the parallel pendant to accumulate and scan the parallel pendant to partial_sum. The parallel execution is the reason that `std::reduce` needs an associative and commutative callable. The corresponding statement hold for the scan variations in contrary to the partial_sum variations.

First, I present an exhaustive example to the algorithms and then write about the functional heritage of these functions. In my example, I ignore the new `std::for_each` algorithm. In contrast to the C++98 variant that returns a unary function, the additional C++17 variant returns nothing. While `std::accumulate` processes its elements from left to right, `std::reduce` does it in an arbitrary order. Let me start with a small code snippet using `std::accumulate` and `std::reduce`. The callable is the lambda function `[](int a, int b){ return a * b; }`.

```
std::vector<int> v{1, 2, 3, 4};

std::accumulate(v.begin(), v.end(), 1, [](int a, int b){ return a * b; });
std::reduce(std::execution::par, v.begin(), v.end(), 1 , 
            [](int a, int b){ return a * b; });
```

The two following graphs show the different fold strategies of `std::accumulate` and `std::reduce`.

`std::accumulate` starts at the left and successively applies the binary operator.

![Fold strategy of `std::accumulate`](images/ParallelSTL----Accumulate.png)

Fold strategy of `std::accumulate`

To the contrary, `std::reduce` applies the binary operator in a non-deterministic way.

![Fold strategy of `std::reduce`](images/ParallelSTL----Reduce.png)

Fold strategy of `std::reduce`

The associativity allows the `std::reduce` algorithm to compute the reduction step on arbitrary adjacents pairs of elements. Thanks to the commutativity, the intermediate results can be computed in an arbitrary order.

```
 1 // newAlgorithm.cpp
 2 
 3 #include <algorithm>
 4 #include <execution>
 5 #include <numeric>
 6 #include <iostream>
 7 #include <string>
 8 #include <vector>
 9 
10 
11 int main(){
12   
13   std::cout << std::endl;
14   
15   // for_each_n
16   
17   std::vector<int> intVec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};                       
18   std::for_each_n(std::execution::par,                      
19                   intVec.begin(), 5, [](int& arg){ arg *= arg; });
20   
21   std::cout << "for_each_n: ";
22   for (auto v: intVec) std::cout << v << " ";
23   std::cout << "\n\n";
24   
25   // exclusive_scan and inclusive_scan
26   std::vector<int> resVec{1, 2, 3, 4, 5, 6, 7, 8, 9};
27   std::exclusive_scan(std::execution::par,                   
28                       resVec.begin(), resVec.end(), resVec.begin(), 1,
29                       [](int fir, int sec){ return fir * sec; });
30   
31   std::cout << "exclusive_scan: ";
32   for (auto v: resVec) std::cout << v << " ";
33   std::cout << std::endl; 
34   
35   std::vector<int> resVec2{1, 2, 3, 4, 5, 6, 7, 8, 9};
36   
37   std::inclusive_scan(std::execution::par,                                      
38                       resVec2.begin(), resVec2.end(), resVec2.begin(),        
39                       [](int fir, int sec){ return fir * sec; }, 1);
40   
41   std::cout << "inclusive_scan: ";
42   for (auto v: resVec2) std::cout << v << " ";
43   std::cout << "\n\n";
44   
45   // transform_exclusive_scan and transform_inclusive_scan
46   std::vector<int> resVec3{1, 2, 3, 4, 5, 6, 7, 8, 9};
47   std::vector<int> resVec4(resVec3.size());             
48   std::transform_exclusive_scan(std::execution::par,         
49                                 resVec3.begin(), resVec3.end(), 
50                                 resVec4.begin(), 0,
51                                 [](int fir, int sec){ return fir + sec; },
52                                 [](int arg){ return arg *= arg; });
53   
54   std::cout << "transform_exclusive_scan: ";
55   for (auto v: resVec4) std::cout << v << " ";
56   std::cout << std::endl;
57   
58   std::vector<std::string> strVec{"Only", "for", "testing", "purpose"};       
59   std::vector<int> resVec5(strVec.size());
60   
61   std::transform_inclusive_scan(std::execution::par,        
62                                 strVec.begin(), strVec.end(), 
63                                 resVec5.begin(), 0,
64                                 [](auto fir, auto sec){ return fir + sec; },
65                                 [](auto s){ return s.length(); });
66                                   
67   std::cout << "transform_inclusive_scan: ";
68   for (auto v: resVec5) std::cout << v << " ";
69   std::cout << "\n\n";
70   
71   // reduce and transform_reduce
72   std::vector<std::string> strVec2{"Only", "for", "testing", "purpose"};
73   
74   std::string res = std::reduce(std::execution::par,        
75                     strVec2.begin() + 1, strVec2.end(), strVec2[0], 
76                     [](auto fir, auto sec){ return fir + ":" + sec; });
77   
78   std::cout << "reduce: " << res << std::endl;
79   
80   std::size_t res7 = std::transform_reduce(std::execution::par,        
81                      strVec2.begin(), strVec2.end(), 
82                      [](std::string s){ return s.length(); }, 
83                      0, [](std::size_t a, std::size_t b){ return a + b; });
84                                                                             
85     
86   std::cout << "transform_reduce: " << res7 << std::endl;
87   
88   std::cout << std::endl;
89 
90 }
```

The new algorithms

I apply the new algorithms to a `std::vector<int>` (line 17) and a `std::vector<std::string>` (line 58).

The `std::for_each_n` algorithm in line 18 maps the first `n` ints of the vector to their powers of 2.

`std::exclusive_scan` (line 27) and `std::inclusive_scan` (line 37) are quite similar. Both apply a binary operation to their elements. The difference is that `std::exclusive_scan` excludes the last element in each iteration.

The `std::transform_exclusive_scan` in line 48 is quite challenging to read. Let me try to explain it. In the first step I apply the lambda function `[](int arg){ return arg *= arg; }` to each element of the range `resVec3.begin()` to `resVec3.end()`. In the second step, I apply the binary operation `[](int fir, int sec){ return fir + sec; }` to the intermediate vector. This means, sum up all elements using 0 as the initial value. The result is placed in `resVec4.begin()`.

The `std::transform_inclusive_scan` function in line 61 is similar. This function maps each element to its length.

The `std::reduce` function should be quite easy to read; it puts `":"` characters between every two elements of the input vector. The resulting string should not start with a `":"` character; therefore, the range starts at the second element (`strVec2.begin() + 1`) and uses the first element of the vector `strVec2[0]` as the initial element.

Studying the output of the program should help you.

![The new algorithms](images/ParallelSTL----newAlgorithm.png)

The new algorithms

#### More overloads

All C++ variants of reduce and scan have more overloads. In the simplest form, you can invoke them without a binary callable and an initial element. If you do not use a binary callable, the addition is used as the binary operation. If you do not specify an initial element, the initial element depends on the used algorithm:

*   `std::inclusive_scan` and `std::transform_inclusive_scan`: the first element.
*   `std::reduce` and `std::transform_reduce`: `typename std::iterator_traits<InputIt>::value_type{}`.

Let’s look at these new algorithms from a functional perspective.

#### The functional Heritage

Long story short: all new functions have a pendant in the pure functional language Haskell.

*   `std::for_each_n` is called `map` in Haskell.
*   `std::exclusive_scan` and `std::inclusive_scan` are called `scanl` and `scanl1` in Haskell.
*   `std::transform_exclusive_scan` and `std::transform_inclusive_scan` is a composition of the Haskell functions `map` and `scanl` or `scanl1`.
*   `std::reduce` is called `foldl` or `foldl1` in Haskell.
*   `transform_reduce` is a composition of the Haskell functions `map` and `foldl` or `foldl1`.

Before I show you Haskell in action, let me say a few words about the different functions.

*   `map` applies a function to a list.
*   `foldl` and `foldl1` applies a binary operation to a list and reduces the list to a value. `foldl` needs, in contrast to `foldl1` an initial value.
*   `scanl` and `scanl1` apply the same strategy such as `foldl` and `foldl1`, but they produce all intermediate results so that you get back a list.
*   `foldl`, `foldl1`, `scanl`, and `scanl1` start their job from the left.

Let’s have a look at the Haskell functions. Here is Haskell’s interpreter shell.

![New algorithms in Haskell](images/ParallelSTL----newAlgorithmHaskell.png)

New algorithms in Haskell

(1) and (2) define a list of integers and a list of strings. In (3), I apply the lambda function `(\a -> a * a)` to the list of integers. (4) and (5) are more sophisticated. The expression (4) multiplies (*) all pairs of integers starting with the 1 as the neutral element of multiplication. Expression (5) does the corresponding for addition. Expressions (6), (7), and (9) are for the imperative eye quite challenging. You have to read them from right to left. `scanl1 (+) . map(\a -> length)` (7) is a function composition. The dot (.) symbol composes the two functions. The first function maps each element to its length; the second function adds the list of lengths together. (9) is similar to (7), the difference is that `foldl` produces one value and requires an initial element that is in case 0\. Now expression (8) should be readable; it successively joins two strings with the “:” character.

### Performance

The reason for using the parallel STL is performance. Here are the first numbers.

```
 1 // parallelSTLPerformance.cpp
 2 
 3 #include <algorithm>
 4 #include <cmath>
 5 #include <chrono>
 6 #include <execution>
 7 #include <iostream>
 8 #include <random>
 9 #include <string>
10 #include <vector>
11 
12 constexpr long long size = 500'000'000;  
13   
14 const double pi = std::acos(-1);
15 
16 template <typename Func>
17 void getExecutionTime(const std::string& title, Func func){
18     
19      const auto sta = std::chrono::steady_clock::now();
20      func();
21      const std::chrono::duration<double> dur = std::chrono::steady_clock::now() - st\
22 a;
23      std::cout << title << ": " << dur.count() << " sec. " << std::endl;
24      
25 }
26     
27 int main(){
28 
29     std::cout << std::endl;
30     
31     std::vector<double> randValues;
32     randValues.reserve(size);
33    
34     std::mt19937 engine;
35     std::uniform_real_distribution<> uniformDist(0, pi / 2);
36     for (long long i = 0 ; i < size ; ++i) randValues.push_back(uniformDist(engine));
37     
38     std::vector<double> workVec(randValues);
39     
40     getExecutionTime("std::execution::seq", [workVec]() mutable {
41         std::transform(std::execution::seq, workVec.begin(), workVec.end(), 
42 		                   workVec.begin(), 
43                            [](double arg){ return std::tan(arg); }
44                        );
45     });
46         
47      getExecutionTime("std::execution::par", [workVec]() mutable {
48         std::transform(std::execution::par, workVec.begin(), workVec.end(), 
49 		                   workVec.begin(), 
50                            [](double arg){ return std::tan(arg); }
51                        );
52     });
53      
54     getExecutionTime("std::execution::par_unseq", [workVec]() mutable {
55         std::transform(std::execution::par_unseq, workVec.begin(), workVec.end(), 
56 		                   workVec.begin(), 
57                            [](double arg){ return std::tan(arg); }
58                       );
59     });
60     
61 }
```

Performance of the various execution policies

The program `parallelSTLPerformance.cpp` calculates the tangents with the sequential (line 39), parallel (line 46), and parallel and vectorised (line 53) execution policy. First, the vector `randValues` is filled with 500 million numbers from the half-open interval [0, pi / 2 [. The function template `getExecutionTime (lines 16 - 24) gets the title and the lambda function executes the lambda function (line 20), and shows the execution time (line 22). There is one particular point about the three lambda functions (lines 39, 46, and 53) used in this program. They are declared as` mutable`. This is necessary because the lambda functions modify its argument` workVec`. Lambda functions are per default constant. If a lambda function wants to modify its values, it has to be declared` mutable`.

My windows laptop has eight logical cores but the parallel execution is more than ten times faster.

![Sequential, parallel, and parallel and vectorised execution](images/ParallelSTL----parallelSTLPerformance.PNG)

Sequential, parallel, and parallel and vectorised execution

The numbers for the parallel and the parallel and vectorised execution are in the same ballpark. Here is the explanation for the Visual C++ Team Blog: [Using C++17 Parallel Algorithms for Better Performance](https://blogs.msdn.microsoft.com/vcblog/2018/09/11/using-c17-parallel-algorithms-for-better-performance/): *Note that the Visual C++ implementation implements the parallel and parallel unsequenced policies the same way, so you should not expect better performance for using par_unseq on our implementation, but implementations may exist that can use that additional freedom someday.*

## The Near Future: C++20

This chapter is about the near future of C++: C++20\. In this chapter, I can not be as precise as in the other chapters in this book. That’s for one reason. The interface of the features, which makes it into the C++20 standard will change very likely. I update this book regulary and, therefore, reflect the updates in this chapter.

My goal in this chapter is quite simple: give you an idea about the upcoming concurrency features in C++.

![Concurrency in C++20](images/timeline----timeline20.png)

Concurrency in C++20

### A Cooperatively Interruptible Joining Thread

`std::jthread` stands for joining thread. In addition to [`std::thread`](#chap06.xhtml_chapterXXXThreads) from C++11, `std::jthread` can automatically join the started thread and signal an interrupt. Its characteristics are described in the proposal [P0660R8](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0660r8.pdf): *A Cooperatively Interruptible Joining Thread*.

#### Automatically Joining

Here is the *non-intuitive* behaviour of `std::thread`. If a `std::thread` is still joinable, `std::terminate` is called in its destructor. A thread `thr` is joinable if either `thr.join()` nor `thr.detach()` was called.

```
// threadJoinable.cpp

#include <iostream>
#include <thread>

int main(){

    std::cout << std::endl;
    std::cout << std::boolalpha;

    std::thread thr{[]{ std::cout << "Joinable std::thread" << std::endl; }};

    std::cout << "thr.joinable(): " << thr.joinable() << std::endl;

    std::cout << std::endl;

}
```

Terminating a still joinable `std::thread`

When executed, the program terminates.

![Terminating a joinable `std::jthread`](images/cpp20_23----threadJoinable.png)

Terminating a joinable `std::jthread`

Both executions of `std::thread` terminate. In the second run, the thread `thr` has enough time to display its message: “Joinable std::thread”.

In the next example, I replace the header `<thread>` with `"jthread.hpp"` and use `std::jthread` from the upcoming C++20 standard.

```
// jthreadJoinable.cpp

#include <iostream>
#include "jthread.hpp"

int main(){

    std::cout << std::endl;
    std::cout << std::boolalpha;

    std::jthread thr{[]{ std::cout << "Joinable std::thread" << std::endl; }};

    std::cout << "thr.joinable(): " << thr.joinable() << std::endl;

    std::cout << std::endl;

}
```

Terminating a still joinable `std::jthread`

Now, the thread `thr` automatically joins in its destructor such as in this case if still joinable.

![Using a `std::jthread` which automatically joins](images/cpp20_23----jthreadJoinable.png)

Using a `std::jthread` which automatically joins

#### Interrupt a `std::jthread`

To get the general idea, let me present a simple example.

```
 1 // interruptJthread.cpp
 2 
 3 #include "jthread.hpp"
 4 #include <chrono>
 5 #include <iostream>
 6 
 7 using namespace::std::literals;
 8 
 9 int main(){
10     
11     std::cout << std::endl;
12     
13     std::jthread nonInterruptable([]{ 
14         int counter{0};
15         while (counter < 10){
16             std::this_thread::sleep_for(0.2s);
17             std::cerr << "nonInterruptable: " << counter << std::endl; 
18             ++counter;
19         }
20     });
21     
22     std::jthread interruptable([](std::stop_token stoken){ 
23         int counter{0};
24         while (counter < 10){
25             std::this_thread::sleep_for(0.2s);
26             if (stoken.stop_requested()) return;
27             std::cerr << "interruptable: " << counter << std::endl; 
28             ++counter;
29         }
30     });
31     
32     std::this_thread::sleep_for(1s);
33     
34     std::cerr << std::endl;
35     std::cerr << "Main thread interrupts both jthreads" << std:: endl;
36     nonInterruptable.request_stop();
37     interruptable.request_stop();
38     
39     std::cout << std::endl;
40     
41 }
```

Interrupt an non-interruptable and interruptable `std::jthread`

I started in the main program the two threads `nonInterruptable` and `interruptable` (lines 13 and 22). In contrast to the thread `nonInterruptable`, the thread `interruptable` gets a `std::stop_token` and uses it in line 26 to check if it was interrupted: `stoken.stop_requested()`. In case of an interrupt the lambda function returns and, therefore, the thread ends. The call `interruptable.request_stop()` (line 37) triggers the end of the thread. This does not hold for the previous call `nonInterruptable.request_stop()`, which does not have an effect.

![Interrupt an non-interruptable and interruptable `std::jthread`"](images/cpp20_23----interruptJthread.png)

Interrupt an non-interruptable and interruptable `std::jthread`”

Here are more details to stop tokens, the joining threads, and condition variables.

#### Stop Tokens

The additional functionality of the cooperatively joining thread is based on the `std::stop_token`, the `std::stop_callback`, and the `std::stop_source`.

##### `std::stop_token`, `std::stop_source`, and `std::stop_callback`

A `stop_token`, a `std::stop_callback`, or a `std::stop_source` enables it to asynchronously request an execution to stop or ask if an execution gets a stop signal. The `std::stop_token` can be passed to an operation and afterwards be used to actively poll the token for a stop request or to register a callback via `std::stop_callback`. The stop request is sent by a `std::stop_source`. This signal affects all associated `std::stop_token`. The three classes `std::stop_source`, `std::stop_token`, and `std::stop_callback` share the ownership of an associated stop state. The calls `request_stop()`, `stop_requested()`, and `stop_possible()` are atomic operations.

The components `std::stop_source` and `std::stop_token` provide the following attributes for stop handling.

The methods of the `std::stop_source src`

| **Method** | **Description** |
| --- | --- |
| `src.get_token()` | If `!stop_possible()`, constructs an `stop_token` object that does not share a stop state. Otherwise, constructs a `stop_token` object that shares the ownership of the stop state with `*this`. |
| `src.stop_possible()` | `true` if the stop source can be used to request stops. |
| `src.stop_requested()` | `true` if `stop_possible()` and `request_stop()` was called by one of the owners. |
| `src.request_stop()` | If `!stop_possible()` or `stop_requested()` the call has no effect. Otherwise, requests a stop so that `stop_requested() == true` and all registered callbacks are synchronously called. |

The methods of the `std::stop_token stoken`

| **Method** | **Description** |
| --- | --- |
| `stoken.stop_possible()` | `false` if a subsequent call to `stop_requested()` will never return `true`. |
| `stoken.stop_requested()` | `true` if `request_stop()` was called on an associated `std::stop_source`, otherwise `false`. |

If the `std::stop_token` should be temporarily disabled, you can replace it with a default constructed token. A default constructed token is not valid. The following code snippet shows how to disable and enable the capability of a thread to accept signals.

```
1 std::jthread jthr([](std::stop_token stoken){
2     ...
3     std::stop_token interruptDisabled; 
4     std::swap(stoken, interruptDisabled);       
5     ...
6     std::swap(stoken, interruptDisabled);       
7     ...
8 }
```

Temporarily disable a stop token

`std::stop_token interruptDisabled` is not valid. This means, from line 4 to 5 the stop token is disabled, form line 6 on enabled.

The next example shows the usage of callbacks.

```
 1 // invokeCallback.cpp
 2 
 3 #include "jthread.hpp"
 4 #include <chrono>
 5 #include <iostream>
 6 #include <vector>
 7 
 8 using namespace::std::literals;
 9 
10 auto func = [](std::stop_token stoken){ 
11         int counter{0};
12         auto thread_id = std::this_thread::get_id();
13         std::stop_callback callBack(stoken, [&counter, thread_id] {
14             std::cout << "Thread id: " << thread_id 
15                       << "; counter: " << counter << std::endl;
16         });
17         while (counter < 10){
18             std::this_thread::sleep_for(0.2s);
19             ++counter;
20         }
21     };
22 
23 int main(){
24     
25     std::cout << std::endl;
26     
27     std::vector<std::jthread> vecThreads(10);
28     for(auto& thr: vecThreads) thr = std::jthread(func);
29     
30     std::this_thread::sleep_for(1s);
31     
32     for(auto& thr: vecThreads) thr.request_stop();
33 
34     std::cout << std::endl;
35     
36 }
```

Usage of callbacks

Each of the ten threads invokes the lambda-function `func` (lines 10 - 21). The callback in the lines 13 - 16 displays the thread id and the counter. Due to the 1 seconds sleeping of the main-thread and the sleeping of the child threads, the counter is 4 when the callbacks are invoked. The call `thr.request_stop()` triggers the callback on each thread.

![Usage of callbacks](images/cpp20_23----invokeCallback.png)

Usage of callbacks

##### Joining Threads

A `std::jhread` is a [`std::thread`](#chap06.xhtml_chapterXXXThreads) with the additional functionality to signal an interrupt and to automatically [`join()`](#chap06.xhtml_chapterXXXjoinSSSandSSSdetach). To support this functionality it has a `std::stop_token`.

The methods of the `std::jthread jthr` for stop token handling

| **Method** | **Description** |
| --- | --- |
| `jthr.get_stop_source()` | Returns the `stop_token`. |
| `jthr.request_stop()` | Equivalent to `src.request_stop()`. |

##### New `wait` Overloads for the `condition_variable_any`

The three wait variations to `wait_for`, and `wait_until` of the [`std::condition_variable_any`](#chap06.xhtml_textXXXcondition_variable_any) get new overloads. They take a `std::stop_token`.

```
 1 template <class Predicate>
 2 bool wait_until(Lock& lock, 
 3                 Predicate pred, 
 4                 stop_token stoken);
 5                 
 6 template <class Clock, class Duration, class Predicate>
 7 bool wait_until(Lock& lock, 
 8                 const chrono::time_point<Clock, Duration>& abs_time, 
 9                 Predicate pred, 
10                 stop_token stoken);
11 
12 template <class Rep, class Period, class Predicate>
13 bool wait_for(Lock& lock, 
14               const chrono::duration<Rep, Period>& rel_time, 
15               Predicate pred, 
16               stop_token stoken);
```

Three new wait overloads

These new overloads require a predicate. The versions ensure to get notified if an interrupt is signalled for the passed `std::stop_token stoken`. The three overloads are equivalent to the following expressions. They return a boolean which indicates whether the predicate evaluates to `true`. This returned boolean is independent of whether a stop was requested or of whether the timeout was triggered.

```
// wait_until in lines 1 - 4
while(!pred() && !stoken.stop_requested()) {
    wait(lock, [&pred, &stoken] {
        return pred() || stoken.stop_requested();
    });
}
return pred();

// wait_until in lines 6 - 10
while(!pred() && !stoken.stop_requested() && Clock::now() < abs_time) {
    cv.wait_until(lock,
                  abs_time,
                  [&pred, &stoken] {
                      return pred() || stoken.stop_requested();
                  });
}
return pred();

// wait_for in lines 12 - 16
return wait_until(lock, 
                  chrono::steady_clock::now() + rel_time, 
                  std::move(pred), 
                  std::move(stoken)
                  );
```

Equivalent expression for the three overloads

After the wait calls, you can check if a stop request occurred.

```
cv.wait_until(lock, predicate, stoken);
if (stoken.stop_requested()){
    // interrupt occurred
}
```

Handle interrupts with `wait`

The following example shows the usage of a condition variable with a stop request.

```
 1 // waitUntilStopRequest.cpp
 2 
 3 #include "condition_variable_any2.hpp"
 4 #include "jthread.hpp"
 5 
 6 #include <iostream>
 7 #include <chrono>
 8 #include <mutex>
 9 #include <thread>
10 
11 using namespace std::literals;
12 
13 std::mutex mutex_;
14 std::condition_variable_any2 condVar;
15 
16 bool dataReady;
17 
18 void receiver(std::stop_token stopToken){
19 
20     std::cout << "Waiting" << std::endl;
21 
22     std::unique_lock<std::mutex> lck(mutex_);
23     bool ret = condVar.wait_until(lck, []{return dataReady;}, stopToken);
24     if (ret){
25         std::cout << "Notification received: " << std::endl;
26     }
27     else{
28          std::cout << "Stop request received" << std::endl;
29     }
30 }
31 
32 void sender(){
33 
34     std::this_thread::sleep_for(5ms);
35     {
36         std::lock_guard<std::mutex> lck(mutex_);
37         dataReady = true;
38         std::cout << "Send notification"  << std::endl;
39     }
40     condVar.notify_one();
41 
42 }
43 
44 int main(){
45 
46   std::cout << std::endl;
47 
48   std::jthread t1(receiver);
49   std::jthread t2(sender);
50   
51   t1.request_stop();
52 
53   t1.join();
54   t2.join();
55 
56   std::cout << std::endl;
57   
58 }
```

Usage of condition variables with a stop request

The `receiver` thread (lines 18 - 30) is waiting for the notification of the `sender` thread (lines 32 - 42). Before the `sender` thread sends its notification in line 40, the `main` thread triggered a stop request in line 51\. The output of the program shows that the stop request happened before the notification.

![Usage of callbacks](images/cpp20_23----waitUntilStopRequest.png)

Usage of callbacks

### Atomic Smart Pointers

A `std::shared_ptr` consists of a control block and its resource. The control block is thread-safe, but access to the resource is not. This means modifying the reference counter is an atomic operation and you have the guarantee that the resource is deleted exactly once. These are the guarantees [`std::shared_ptr`](#chap05.xhtml_chapterXXXshared_ptr) gives you.

The proposal [N4162](http://wg21.link/n4162) for atomic smart pointers directly addresses the deficiencies of the current implementation. The deficiencies boil down to these three points: consistency, correctness, and performance. I provide an overview of these three points. See the proposal N4162 for details.

*   **Consistency**: the atomic operations for `std::shared_ptr` are the only atomic operations for a non-atomic data type.
*   **Correctness**: the usage of the global atomic operations is quite error-prone because the correct usage is based on discipline. It is easy to forget to use an atomic operation - such as using `ptr = localPtr` instead of `std::atomic_store(&ptr, localPtr)`. The result is undefined behaviour because of a data race. If we used an atomic smart pointer instead, the type-system would not allow it.
*   **Performance**: the atomic smart pointers have a big advantage compared to the free `atomic_`* functions. The atomic versions are designed for the special use case and can internally have a `std::atomic_flag` as a kind of cheap [spinlock](#chap05.xhtml_chapterXXXSpinlockSSSversusSSSMutex). Designing the non-atomic versions of the pointer functions to be thread-safe would be overkill if they are used in a single-threaded scenario. They would have a performance penalty.

For me, the correctness argument is the most important one. Why? The answer lies in the proposal. The proposal presents a thread-safe singly linked list that supports insertion, deletion, and searching of elements. This singly linked list is implemented in a lock-free way.

#### A thread-safe singly linked list

![A thread-safe singly linked list](images/cpp20_23----AtomicSinglyLinkedList.png)

A thread-safe singly linked list

All changes that are required to compile the program with a C++11 compiler are marked in red. The implementation with atomic smart pointers is a lot easier and hence less error-prone. C++20’s type system does not permit it to use a non-atomic operation on an atomic smart pointer.

The proposal [N4162](http://wg21.link/n4162) proposed the new types `std::atomic_shared_ptr` and `std::atomic_weak_ptr` as atomic smart pointers. By merging them in the mainline ISO C++ standard, they became partial template specialisation of [`std::atomic`](#chap05.xhtml_chapterXXXAtomics): *`std::atomic<std::shared_ptr<T>>`*, and *`std::atomic<std::weak_ptr<T>>`*.

Consequently, the atomic operations for `std::shared_ptr` are deprecated with C++20.

### Latches and Barriers

Latches and barriers are simple thread synchronisation mechanisms which enable some threads to block until a counter becomes zero. At first, don’t confuse the new barriers with [memory barriers](#chap05.xhtml_chapterXXXMemorySSSBarriers), also known as fences. In C++20 we get latches and barriers in two variations: `std::latch`, and `std::barrier`.

First, there are two questions:

1.  What are the differences between these two mechanisms to synchronise threads? You can use a `std::latch` only once, but you can use a `std::barrier` more than once. A `std::latch` is useful for managing one task by multiple threads; a `std::barrier` is useful for managing repeated tasks by multiple threads. Additionally, a `std::barrier` enables you to execute a function in the so-called completion step. The completion step is the state when the counter becomes zero.
2.  What use cases do latches and barriers support that cannot be done in C++11 and C++14 with futures, threads, or condition variables in combination with locks? Latches and barriers address no new use cases, but they are a lot easier to use. They are also more performant because they often use a [lock-free](#chap23.xhtml_glossaryXXXlockMMMfreeSSSBOBOBOGlossaryBCBCBC) mechanism internally.

#### `std::latch`

Now, I have a closer look at the interface of a `std::latch`.

Methods of a latch `lat`

| **Method** | **Description** |
| --- | --- |
| `lat.count_down(upd = 1)` | Atomically decrements counter by `upd`. |
| `lat.try_wait()` | Return `counter == 0`. |
| `lat.wait()` | If `counter == 0`, returns immediately. If not blocks until `counter == 0`. |
| `lat.arrive_and_wait(update = 1)` | Equivalent to `count_down(upd); wait();`. |

The default value for `upd` is `1`. The call `lat.try_wait()` does never wait as its name suggests.

Here is a short code snippet from the [N4204](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4204.html) proposal.

```
 1 void DoWork(threadpool* pool) {
 2   latch completion_latch(NTASKS);
 3   for (int i = 0; i < NTASKS; ++i) {
 4     pool->add_task([&] {
 5       // perform work
 6       ...
 7       completion_latch.count_down();
 8       }));
 9   }
10   // Block until work is done
11   completion_latch.wait();
12 }
```

std::latch

I set the `std::latch completion_latch` in its constructor to `NTASKS` (line 2). The thread pool executes `NTASKS` (lines 4 - 8). At the end of each task (line 7), the counter is decremented. Line 11 is the barrier for the thread running the function `DoWork` and hence for the small workflow. This thread is blocked until all tasks have been finished.

A `std::barrier` is similar to a `std::latch`.

#### `std::barrier`

There are two differences between a `std::latch` and a `std::barrier`. First, you can use a `std::barrier` more than once and second, you can set the counter for the next phase (iteration). Immediately after the counter becomes zero, the so-called completion step starts. In this completion step, a [callable unit](#chap23.xhtml_glossaryXXXCallableSSSUnitZZZcallableSSSBOBOBOGlossaryBCBCBC) is invoked. The `std::barrier` gets its callable in its constructor. The callable has to return a number. This number sets the counter for the next iteration. A return value of -1 means that the counter keeps the same value. Numbers smaller than -1 are not allowed.

The completion step performs the following steps:

1.  All threads are blocked.
2.  An arbitrary thread is unblocked and executes the callable unit.
3.  If the completion phase is done, all threads are unblocked.

Methods of a barrier `bar`

| **Method** | **Description** |
| --- | --- |
| `bar.arrive(upd)` | Atomically decrements counter by `upd`. |
| `bar.wait()` | Blocks at the synchronisation point until the completion step is done. |
| `bar.arrive_and_wait()` | Equivalent to `wait(arrive())` |
| `bar.arrive_and_drop()` | Decrements the initial expected count for all subsequent phases by one. |

Here is a short example demonstrating the usage of `std::barrier`.

```
 1 void DoWork() {
 2   Tasks& tasks;
 3   int initial_threads;
 4   int n_threads{NTASKS}; 
 5   atomic<int> current_threads(initial_threads);
 6   vector<thread*> workers;
 7 
 8   // Create a barrier, and set a lambda that will be
 9   // invoked every time the barrier counts down. If one or more
10   // active threads have completed, reduce the number of threads.
11   std::function rf = [&]{ return current_threads; };
12   barrier task_barrier(n_threads, rf);
13 
14   for (int i = 0; i < n_threads; ++i) {
15     workers.push_back(new thread([&] {
16       bool active = true;
17       while(active) {
18         Task task = tasks.get();
19         // perform task
20         ...
21         if (finished(task)) {
22           current_threads--;
23           active = false;
24         }
25         task_barrier.arrive_and_wait();
26       }
27     });
28   }
29 
30   // Read each stage of the task until all stages are complete.
31   while (!finished()) {
32     GetNextStage(tasks);
33   }
34 }
```

std::barrier

The `barrier` in line 12 is used to coordinate several threads that perform their task multiple times. The number of threads is `n_threads` (line 4). Each thread takes its task at line 18 via `tasks.get()`, performs it and blocks - once it is done with its task (line 25) - until all threads are done with their tasks. The `std::barrier` counter is adjusted at runtime. Hence, the `std::barrier task_barrier` in line 11 gets a lambda function. This lambda function captures its variable `current_thread` by reference: `[&] { return current_threads; }`. The variable is decremented in line 22 and `active` is set to `false` if the thread has completed its task. The counter is decremented in line 22.

You can read further details of [`std::latch`](http://en.cppreference.com/w/cpp/experimental/latch), and [`std::barrier`](http://en.cppreference.com/w/cpp/experimental/barrier) at cppreference.com.

### Semaphores

Semaphores are a synchronisation mechanism used to control concurrent access to a shared resource. A counting semaphore is a special semaphore which has a counter that is bigger than zero. The counter is initialised in the constructor. Acquiring the semaphore decreases the counter and releasing the semaphore increases the counter. If a thread tries to acquire the semaphore when the counter is zero, the thread will block until another thread increments the counter by releasing the semaphore.

Methods of a semaphore `sem`

| **Method** | **Description** |
| --- | --- |
| `counting_semaphore::max()` | Return the maximum value of the `counter`. |
| `sem.release(upd = 1)` | Atomically increases `counter` by `upd`. |
| `sem.acquire()` | Performs `sem.try_acquire` and blocks until `counter` is greater than zero. |
| `sem.try_acquire()` | Atomically decrements the `counter`. |
| `sem.try_acquire_for(reTime)` | Performs `sem.try_acquire` until the time point. |
| `sem.try_acquire_until(absTime)` | Performs `sem.try_acquire` for the time duration. |

The method `sem.try_lock_for(relTime)` needs a relative [time duration](#chap21.xhtml_chapterXXXTimeSSSDuration); the method `sem.try_lock_until(absTime)` needs an absolute [time point](#chap21.xhtml_chapterXXXTimeSSSPoint).

### Coroutines

Coroutines are functions that can suspend and resume their execution while keeping their state. The evolution of functions goes in C++ one step further. Coroutines are with high probability part of C++20.

What I present in this section as a new idea in C++20 is quite old. The term coroutine was coined by [Melvin Conway](https://en.wikipedia.org/wiki/Melvin_Conway). He used it in his publication on compiler construction in 1963\. [Donald Knuth](https://en.wikipedia.org/wiki/Donald_Knuth) called procedures a special case of coroutines. Sometimes, it just takes a while to get your ideas accepted.

With the new keywords `co_await` and `co_yield`, C++20 extends the execution of C++ functions with two new concepts.

Thanks to `co_await expression` it is possible to suspend and resume the execution of the `expression`. If you use `co_await expression` in a function `func`, the call `auto getResult = func()` does not block if the result of the function is not available. Instead of resource-consuming blocking, you have resource-friendly waiting.

`co_yield expression` allows it to write a generator function. The generator function returns a new value each time. A generator function is a kind of data stream from which you can pick values. The data stream can be infinite. Therefore, we are in the centre of lazy evaluation with C++.

#### A Generator Function

The following program is as simple as possible. The function `getNumbers` returns all integers from `begin` to `end` incremented by `inc`. `begin` has to be smaller than `end` and `inc` has to be positive.

```
 1 // greedyGenerator.cpp
 2 
 3 #include <iostream>
 4 #include <vector>
 5 
 6 std::vector<int> getNumbers(int begin, int end, int inc = 1){
 7   
 8   std::vector<int> numbers;
 9   for (int i = begin; i < end; i += inc){
10     numbers.push_back(i);
11   }
12   
13   return numbers;
14   
15 }
16 
17 int main(){
18 
19   std::cout << std::endl;
20 
21   const auto numbers= getNumbers(-10, 11);
22   
23   for (auto n: numbers) std::cout << n << " ";
24   
25   std::cout << "\n\n";
26 
27   for (auto n: getNumbers(0, 101, 5)) std::cout << n << " ";
28 
29   std::cout << "\n\n";
30 
31 }
```

A greedy generator function

Of course, I am reinventing the wheel with `getNumbers` because that job could be done with [`std::iota`](http://en.cppreference.com/w/cpp/algorithm/iota) since C++11.

For completeness, here is the output.

![A generator function](images/cpp20_23----greedyGenerator.png)

A generator function

Two observations about the program are essential. On the one hand, the vector `numbers` in line 8 always gets all values. This holds even if I’m only interested in the first 5 elements of a vector with 1000 elements. On the other hand, it’s quite easy to transform the function `getNumbers` into a lazy generator.

```
 1 // lazyGenerator.cpp
 2 
 3 #include <iostream>
 4 #include <vector>
 5 
 6 generator<int> generatorForNumbers(int begin, int inc = 1){
 7   
 8   for (int i = begin;; i += inc){
 9     co_yield i;
10   }
11   
12 }
13 
14 int main(){
15 
16   std::cout << std::endl;
17 
18   const auto numbers= generatorForNumbers(-10);
19   
20   for (int i= 1; i <= 20; ++i) std::cout << numbers << " ";
21   
22   std::cout << "\n\n";
23 
24   for (auto n: generatorForNumbers(0, 5)) std::cout << n << " ";
25 
26   std::cout << "\n\n";
27 
28 }
```

A lazy generator function

While the function `getNumbers` in the file `greedyGenerator.cpp` returns a `std::vector<int>`, the coroutine `generatorForNumbers` in `lazyGenerator.cpp` returns a generator. The generator `numbers` in line 18 or `generatorForNumbers(0, 5)` in line 24 returns a new number on request. The range-based for-loop triggers the query. To be more precise, the query of the coroutine returns the value `i` via `co_yield i` and immediately suspends its execution. If a new value is requested, the coroutine resumes its execution exactly at that place.

The expression `generatorForNumbers(0, 5)` in line 24 is a just-in-place usage of a generator.

I want to stress one point explicitly. The coroutine `generatorForNumbers` creates an infinite data stream because the for-loop in line 8 has no end condition. This is fine if I only ask for a finite number of values such as in line 20\. This does not hold for line 24 since there is no end condition. Therefore, the expression runs *forever*.

Because coroutines are a new concept to C++, I want to provide a few more details about them.

#### Details

##### Typical Use-Cases

Coroutines are the usual way to write [event-driven applications](https://en.wikipedia.org/wiki/Event-driven_programming). Event-driven application can be simulations, games, servers, user interfaces, or even algorithms. Coroutines are typically used for [cooperative multitasking](https://de.wikipedia.org/wiki/Multitasking). The key to cooperative multitasking is that each task takes as much time as it needs. Cooperative multitasking is in contrast to pre-emptive multitasking, for which we have a schedule that decides how long each task gets the CPU.

There are different kinds of coroutines.

##### Underlying Concepts

Coroutines in C++20 are asymmetric, first-class, and stackless.

The workflow of an **asymmetric** coroutine goes back to the caller. This does not hold for a symmetric coroutine. A symmetric coroutine can delegate its workflow to another coroutine.

**First-class** coroutines are similar to First-Class Functions since coroutines behave like data. Behaving like data means that you can use them as an argument to or return value from a function, or store them in a variable.

A **stackless** coroutine enables it to suspend and resume the top-level coroutine. The execution of the coroutine and the yielding from the coroutine comes back to the caller. Stackless coroutines are often called resumable functions.

##### Design Goals

Gor Nishanov describes the design goals of coroutines.

Coroutines should

*   be highly scalable (to billions of concurrent coroutines).
*   have highly efficient resume and suspend operations comparable in cost to the overhead of a function.
*   seamlessly interact with existing facilities with no overhead.
*   have open-ended coroutine machinery allowing library designers to develop coroutine libraries exposing various high-level semantics such as generators, [goroutines](https://tour.golang.org/concurrency/1), tasks and more.
*   usable in environments where exceptions are forbidden or not available.

Due to the design goals of scalability and seamless interaction with existing facilities the coroutines are stackless. In contrast, a stackful coroutine reserve a default stack for 1MB on Windows, and 2MB on Linux.

There are four ways for a function to become a coroutine.

##### Becoming a Coroutine

A function becomes a coroutine if it uses

*   `co_return`, or
*   `co_await`, or
*   `co_yield`, or a
*   `co_await` expression in a range-based for-loop.

###### Restrictions

Coroutines cannot have `return` statements, or placeholder return types. This holds for unconstrained placeholders (`auto`), and constrained placeholders (concepts).

Additionally, `constexpr` functions, constructors, destructors, and the main function cannot be coroutines.

This explanation was from proposal N4628.

Finally, I discuss the new keywords `co_return`, `co_yield`, and `co_await`.

##### `co_return`, `co_yield`, and `co_await`

**co_return**: a coroutine uses **co_return** as its return statement.

**co_yield**: thanks to `co_yield` you can implement a generator which generates an infinite data stream from which you can successively query values. The return type of the generator `generator<int> generatorForNumbers(int begin, int inc= 1)` is `generator<int>`. `generator<int>` internally holds a special promise `p` such that a call `co_yield i` is equivalent to a call `co_await p.yield_value(i)`. `co_yield i` can be called an arbitrary number of times. Immediately after the call, the execution of the coroutine is suspended.

**co_await**: `co_await` eventually causes the execution of the coroutine to be suspended and resumed. The expression `exp` in `co_await exp` has to be a so-called awaitable expression. `exp` has to implement a specific interface. This interface, consisting of the three functions `await_ready, await_suspend,` and `wait_resume`.

The C++20 standard already defines two awaitables: `std::suspend_always`, and `std::suspend_never`.

```
struct suspend_always {
    constexpr bool await_ready() const noexcept { return false; }
    constexpr void await_suspend(coroutine_handle<>) const noexcept {}
    constexpr void await_resume() const noexcept {}
};
```

The awaitable `std::suspend_always`

As its name suggests, the awaitable `suspend_always` suspends always. Therefore, the call `await_ready` returns `false`. Consequently, the opposite holds for `suspend_never`.

```
struct suspend_never {
    constexpr bool await_ready() const noexcept { return true; }
    constexpr void await_suspend(coroutine_handle<>) const noexcept {}
    constexpr void await_resume() const noexcept {}
};
```

The awaitable `std::suspend_never`

A typical use case for `co_await` is a server that waits for events.

```
1 Acceptor acceptor{443};
2 while (true){
3     Socket socket= acceptor.accept();              // blocking
4     auto request= socket.read();                   // blocking
5     auto response= handleRequest(request);     
6     socket.write(response);                        // blocking  
7 }
```

A blocking server

The server is quite simple because it sequentially answers each request in the same thread. The server listens on port 443 (line 1), accepts its connections (line 3), reads the incoming data from the client (line 4), and writes its answer to the client (line 6). All calls in lines 3, 4, and 6 are blocking.

Thanks to `co_await`, the blocking calls can now be suspended and resumed.

```
1 Acceptor acceptor{443};
2 while (true){
3     Socket socket= co_await acceptor.accept();           
4     auto request= co_await socket.read();              
5     auto response= handleRequest(request);     
6     co_await socket.write(response);                 
7 } 
```

A waiting server

#### The Framework

The framework for writing coroutines consists of more than 20 functions which you partially have to implement and partially could overwrite. Therefore, you can tailor the coroutine to your needs.

A coroutine consists of three parts: the promise object, the coroutine handle, and the coroutine frame.

**Promise object**: The promise object is manipulated from inside the coroutine, and it delivers its result via the promise object.

**Coroutine handle**: The coroutine handle is a non-owning handle to resume or to destroy the coroutine frame from outside.

**Coroutine frame**: The coroutine frame is an internal, typically heap-allocated state. It consists of the already mentioned promise object, the copied parameters of the coroutine, the representation of the suspensions point, local variables which lifetime ends before the current suspension point, and local variables which lifetime exceeds the current suspension point.

Two requirements are necessary to optimise out the allocation of the coroutine:

1.  The lifetime of the coroutine has to be nested inside the lifetime of the caller.
2.  The caller of the coroutine knows the size of the coroutine frame.

##### The Simplified Workflow

When you use `co_yield`, or `co_await`, or `co_return` in a function, the function becomes a coroutine, and the compiler transforms its body to something equivalent to the following lines.

```
 1 {
 2   Promise promise;
 3   co_await promise.initial_suspend();
 4   try
 5   {
 6     <function body>
 7   }
 8   catch (...)
 9   {
10     promise.unhandled_exception();
11   }
12 FinalSuspend:
13   co_await promise.final_suspend();
14 }
```

Body of a coroutine

The simplified workflow of the coroutine consists of the following phases.

*   Coroutine begins execution
    *   allocates the coroutine frame if necessary
    *   copies all functions parameters to the coroutine frame
    *   creates the promise object `promise`
    *   calls `promise.get_return_object()` to create the coroutine handle and keeps it in a local variable. The result of the call will be returned to the caller when the coroutine first suspends.
    *   calls `promise.initial_suspend()` and `co_await`’s its result. The promise type typically returns `suspend_never` for eagerly-started coroutines or `suspend_always` for lazily-started coroutines.
    *   the body of the coroutine is executed, when `co_await promise.initial_suspend()` resumes
*   Coroutines reaches a suspension point
    *   the return object (`promise.get_return_object()`) is returned to the caller, which resumed the coroutine
*   Coroutine reaches `co_return`
    *   calls `promise.return_void()` for `co_return` or `co_return expression`, where `expression` has type `void`
    *   calls `promise.return_value(expression)` for `co_return expression`, where `expression` has non-type `void`
    *   destroys all stack created variables
    *   calls `promise.final_suspend()` and `co_await`’s its result
*   Coroutine is destroyed (by terminating via `co_return`, an uncaught exception, or via the coroutine handle)
    *   calls the destruction of the promise object
    *   calls the destructor of the function parameters
    *   frees the memory used by the coroutine frame
    *   transfers control back to the caller.

When a coroutine ends with an uncaught exception, the following happens:

*   catches the exception and calls `promise.unhandled_exception()` from the catch-block
*   calls `promise.final_suspend()` and `co_await`’s the result.

Let me bring this theory to praxis.

##### An Infinite Data Stream with `co_yield`

The following program produces an infinite data stream. The coroutine `getNext` uses `co_yield` to create a data stream which starts at `start` and gives on request the next value, incremented by `step`.

```
 1 // infiniteDataStream.cpp
 2 
 3 #include <experimental/coroutine>
 4 #include <memory>
 5 #include <iostream>
 6 
 7 template<typename T>
 8 struct Generator {
 9     
10     struct promise_type;
11     using handle_type = std::experimental::coroutine_handle<promise_type>;
12     
13     Generator(handle_type h): coro(h) {}                         // (3)
14     handle_type coro;
15     std::shared_ptr<T> value;
16     
17     ~Generator() {
18         if ( coro ) coro.destroy();
19     }
20     Generator(const Generator&) = delete;
21     Generator& operator = (const Generator&) = delete;
22     Generator(Generator&& oth): coro(oth.coro) {
23         oth.coro = nullptr;
24     }
25     Generator& operator = (Generator&& oth) {
26         coro = oth.coro;
27         oth.coro = nullptr;
28         return *this;
29     }
30     int getValue() {
31         return coro.promise().current_value;
32     }
33     bool next() {                                                // (5)
34         coro.resume();
35         return not coro.done();
36     }
37     struct promise_type {
38          promise_type()  = default;                              // (1)
39           
40         ~promise_type() = default;
41         
42         auto initial_suspend() {                                 // (4)
43             return std::experimental::suspend_always{};
44         }
45         auto final_suspend() {
46             return std::experimental::suspend_always{};
47         }
48         auto get_return_object() {                               // (2)
49             return Generator{handle_type::from_promise(*this)};
50         }
51         auto return_void() {
52             return std::experimental::suspend_never{};
53         }
54       
55         auto yield_value(int value) {                            // (6) 
56             current_value = value;
57             return std::experimental::suspend_always{};
58         }
59         void unhandled_exception() {
60             std::exit(1);
61         }
62         T current_value;
63        };
64 
65 };
66 
67 Generator<int> getNext(int start = 0, int step = 1){
68     auto value = start;
69     for (int i = 0;; ++i){
70         co_yield value;
71         value += step;
72     }
73 }
74 
75 int main() {
76     
77     std::cout << std::endl;
78   
79     std::cout << "getNext():";
80     auto gen = getNext();
81     for (int i = 0; i <= 10; ++i) {
82         gen.next();
83         std::cout << " " << gen.getValue();                      // (7)
84     }
85     
86     std::cout << "\n\n";
87     
88     std::cout << "getNext(100, -10):";
89     auto gen2 = getNext(100, -10);
90     for (int i = 0; i <= 20; ++i) {
91         gen2.next();
92         std::cout << " " << gen2.getValue();
93     }
94     
95     std::cout << std::endl;
96     
97 }
```

An infinite data stream

The `main` program creates two coroutines. The first one `gen` (line 80) returns the values from 0 to 10, and the second one `gen2` (line 89) the values from 100 to -100. Before I dive into the workflow, thanks to the online compiler [Wandbox](https://wandbox.org/), here is the output of the program.

![An infinite data stream](images/cpp20_23----infiniteDataStream.PNG)

An infinite data stream

The numbers in the program `infiniteDataStream.cpp` stand for the steps in the first iteration of the workflow.

1.  creates the promise
2.  calls `promise.get_return_object()` and keeps the result in a local variable
3.  creates the generator
4.  calls `promise.initial_suspend()`. The generator is lazy and, therefore, suspends always.
5.  asks for the next value and returns if the generator is consumed
6.  triggered by the `co_yield` call. The next value is afterwards available.
7.  gets the next value

In additional iterations, only the steps 5 and 6 are performed.

##### Thread Synchronisation with `co_await`

It is a typical use-case to synchronise threads. One thread prepares a work-package another thread is waiting for. [Condition variables](#chap06.xhtml_chapterXXXConditionSSSVariablesZZZcondition_variable), [promises and futures](#chap06.xhtml_chapterXXXNotifications), and also an [atomic boolean](#chap05.xhtml_chapterXXXatomicBBBboolEEE) can be used to create a sender/receiver workflow. Thanks to coroutines, thread synchronisation is quite easy without the inherent risks of condition variables such as [spurious wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) and [lost wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup).

```
 1 // senderReceiver.cpp
  2 
  3 #include <experimental/coroutine>
  4 #include <chrono>
  5 #include <iostream>
  6 #include <functional>
  7 #include <string>
  8 #include <stdexcept>
  9 #include <atomic>
 10 #include <thread>
 11 
 12 class Event
 13 {
 14 public:
 15 
 16   Event() = default;
 17 
 18   Event(const Event&) = delete;
 19   Event(Event&&) = delete;
 20   Event& operator=(const Event&) = delete;
 21   Event& operator=(Event&&) = delete;
 22 
 23   class Awaiter;
 24   Awaiter operator co_await() const ;
 25 
 26   void notify() ;
 27 
 28 private:
 29 
 30   friend class Awaiter;
 31   
 32   mutable std::atomic<void*> suspendedWaiter{nullptr};
 33   mutable std::atomic<bool> notified{false};
 34 
 35 };
 36 
 37 class Event::Awaiter
 38 {
 39 public:
 40   Awaiter(const Event& eve): event(eve){}
 41 
 42   bool await_ready() const ;
 43   bool await_suspend(std::experimental::coroutine_handle<> corHandle) ;
 44   void await_resume() {}
 45 
 46 private:
 47   friend class Event;
 48 
 49   const Event& event;
 50   std::experimental::coroutine_handle<> coroutineHandle;
 51 };
 52 
 53 bool Event::Awaiter::await_ready() const {
 54   
 55   // allow at most one waiter
 56   if (event.suspendedWaiter.load() != nullptr){
 57     throw std::runtime_error("More than one waiter is not valid");
 58   }
 59   
 60   // evaluated.notified == false; suspends the coroutine
 61   // evaluated.notified == true; the coroutine is executed such as a usual function
 62   return event.notified;
 63 }
 64 
 65 bool Event::Awaiter::await_suspend(std::experimental::coroutine_handle<> corHandle) {
 66 
 67   coroutineHandle = corHandle;
 68   
 69   if (event.notified) return false;
 70   
 71   // store the waiter for later notification
 72   event.suspendedWaiter.store(this);
 73 
 74   return true;
 75 }
 76 
 77 void Event::notify()  {
 78   notified = true;
 79   
 80   // try to load the waiter
 81   auto* waiter = static_cast<Awaiter*>(suspendedWaiter.load());
 82  
 83   // check if a waiter is available
 84   if (waiter != nullptr) {
 85       // resume the coroutine => await_resume
 86       waiter->coroutineHandle.resume();
 87   }
 88 }
 89 
 90 Event::Awaiter Event::operator co_await() const 
 91 {
 92   return Awaiter{ *this };
 93 }
 94 
 95 struct Task{
 96   struct promise_type{
 97     Task get_return_object() { return {}; }
 98     std::experimental::suspend_never initial_suspend() { return {}; }
 99     std::experimental::suspend_never final_suspend() { return {}; }
100     void return_void() {}
101     void unhandled_exception() {}
102   };
103 };
104 
105 Task receiver(Event& event){ 
106   auto start = std::chrono::high_resolution_clock::now();
107   co_await event; 
108   std::cout << "Got the notification! " << std::endl;
109   auto end = std::chrono::high_resolution_clock::now();
110   std::chrono::duration<double> elapsed = end - start;
111   std::cout << "Waited " << elapsed.count() << " seconds." << std::endl;
112 }
113 
114 using namespace std::chrono_literals;
115 
116 int main(){
117     
118     std::cout << std::endl;
119     
120     std::cout << "Notification before waiting" << std::endl;
121     Event event1{};
122     auto senderThread1 = std::thread([&event1]{ event1.notify(); });  // Notification
123     auto receiverThread1 = std::thread(receiver, std::ref(event1));
124     
125     receiverThread1.join();
126     senderThread1.join();
127     
128     std::cout << std::endl;
129     
130     std::cout << "Notification after 2 seconds waiting" << std::endl;
131     Event event2{};
132     auto receiverThread2 = std::thread(receiver, std::ref(event2));
133     auto senderThread2 = std::thread([&event2]{
134       std::this_thread::sleep_for(2s);
135       event2.notify();                                               // Notification
136     });
137     
138     receiverThread2.join();
139     senderThread2.join();
140      
141     std::cout << std::endl;
142     
143 }
```

Thread Synchronisation

Thread synchronisation with coroutines is quite easy from the users perspective. Let’s have a look at the program `senderReiver.cpp`. The threads `senderThread1` (line 122) and `senderThread2` (line 133) uses an event to send its notification in the lines 122 and 135\. The function `receiver` in lines 105 - 112 is the coroutine which is executed in the thread `receiverThread1` (line 123) and `receiverThread2` (line 132). I measured the time between the begin and the end of the coroutine and displayed it. This number shows how long the coroutine waits. The following screenshot shows the output of the program.

![Thread synchronisation](images/cpp20_23----senderReceiver.png)

Thread synchronisation

If you compare the class `Generator` in the [infinite data stream](#chap08.xhtml_chapterXXXAnSSSInfiniteSSSDataSSSStreamSSSwithSSSco_yield) with the class `Event` in this example, there is a subtle difference. In the first case, the `Generator` is the awaitable and the awaiter, in the second case, the `Event` uses the `operator co_await` to return the awaiter. This separation of concerns into the awaitable and the awaiter improves the structure of the code.

The output displays that the execution of the second coroutine takes about two seconds. The reason is that the `event1` send its notification before the coroutine is suspended (line 107), but the `event2` sends it notification after a time duration of 2 seconds (line 134).

Now, I put the implementer’s hat on. The workflow of the coroutine is quite challenging to grasp. The class `Event` has two interesting members: `suspendedWaiter` and `notified`. `suspendedWaiter` in line 32 holds the waiter for the signal and `notified` in line 33 holds the state of the notification.

In my explanation to both workflows, I assume, the in the first case (first workflow) the event notification happens before the coroutine awaits the events. For the second case (second workflow), I assume it the other way around.

Let’s first looks at `event1` and the first workflow. `event1` send its notification before `receiverThread1` is started. The call `event1` (line 122) triggers the method `notify` (lines 77 to 88). First the notification flag is set and then, the call `auto* waiter = static_cast<Awaiter*>(suspendedWaiter.load());` loads the potential `waiter`. In this case, the `waiter` is a `nullptr` because it was not set before. This means the following `resume` call on the `waiter` in line 86 is not executed. The subsequentially performed function `await_ready` (lines 53 - 63) checks first if there is more than one `waiter`. In this case, I throw a `std::runtime` exception. The crucial part of this method is the return value. `event.notification` was already set to `true` in the `notify` method. `true` means in this case that the coroutine is not suspended and executes such as a usual function.

In the second workflow, the `co_await event2` call happens before `event2` sends its notification. `co_wait event2` triggers the call `await_ready` (line 53). The big difference to the first workflow is now that `event.notified` is `false`. This `false` value causes the suspension of the coroutine. Technically the method `await_suspend` (lines 65 - 75) is executed. `await_suspend` gets the coroutine handle `corHandle` and stores it for later invocation in the variable `coroutineHandle` (line 67). Of course, later invocation means resumption. Secondly, the `waiter` is stored in the variable `suspendedWaiter`. When later `event2.notify` triggers its notification, the method `notify` (line 77) is executed. The difference to the first workflow is that the condition `waiter != nullptr` evaluates to `true`. The result is that the `waiter` uses the `coroutineHandle` to resume the coroutine.

## Case Studies

After providing the theory on the [memory model](#chap05.xhtml_chapterXXXMemorySSSModel) and [the multithreading interface](#chap06.xhtml_chapterXXXMultithreading), I now apply the theory in practice and provide you a few performance numbers.

You should take the performance numbers with a **grain of salt**. I’m not interested in the exact number for each variation of the algorithms on Linux and Windows. I’m more interested in getting a gut feeling of which algorithms may work and which algorithms may not work. I’m not comparing the absolute numbers of my Linux desktop with the numbers on my Windows laptop, but I’m interested to know if some algorithms work better on Linux or Windows.

### Calculating the Sum of a Vector

What is the fastest way to add the elements of a `std::vector`? To get the answer, I fill a `std::vector` with one hundred million arbitrary but [uniformly distributed](https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)) numbers between 1 and 10\. The task is to calculate the sum of the numbers in various ways. I use the performance of a single threaded addition as the reference execution time. I discuss [atomics](#chap05.xhtml_chapterXXXAtomics), [locks](#chap06.xhtml_chapterXXXLocks), [thread-local data](#chap06.xhtml_chapterXXXThreadMMMLocalSSSData) and [tasks](#chap06.xhtml_chapterXXXTasks).

Let’s start with the single threaded scenario.

#### Single Threaded addition of a Vector

The straightforward strategy is it to add the numbers in a range-based for loop.

##### Range-based for Loop

The summation takes place in line 27.

```
 1 // calculateWithLoop.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <random>
 6 #include <vector>
 7 
 8 constexpr long long size = 100000000;
 9 
10 int main(){
11 
12   std::cout << std::endl;
13 
14   std::vector<int> randValues;
15   randValues.reserve(size);
16 
17   // random values
18   std::random_device seed;
19   std::mt19937 engine(seed());
20   std::uniform_int_distribution<> uniformDist(1, 10);
21   for (long long i = 0 ; i < size ; ++i) 
22        randValues.push_back(uniformDist(engine));
23  
24   const auto sta = std::chrono::steady_clock::now();
25   
26   unsigned long long sum = {};
27   for (auto n: randValues) sum += n;
28  
29   const std::chrono::duration<double> dur = 
30         std::chrono::steady_clock::now() - sta;
31         
32   std::cout << "Time for addition " << dur.count() 
33             << " seconds" << std::endl;
34   std::cout << "Result: " << sum << std::endl;
35 
36   std::cout << std::endl;
37 
38 }
```

Summation of a vector in a range-based for loop

How fast are my computers?

![Explicit summation on Linux](images/CaseStudies----CalculateWithLoop.png)

Explicit summation on Linux

![Explicit summation on Windows](images/CaseStudies----CalculateWithLoop_win.PNG)

Explicit summation on Windows

You should not use loops explicitly. Most of the time you can use an algorithm from the Standard Template Library.

##### Summation with `std::accumulate`

`std::accumulate` is the right way to calculate the sum of a vector. For the sake of simplicity, I show the application of `std::accumulate`. The entire source file can be found in the resources for this book.

```
// calculateWithStd.cpp

...

const unsigned long long sum = std::accumulate(randValues.begin(), 
                                               randValues.end(), 0);

... 
```

Summation of a vector with `std::accumulate`

On Linux, the performance of `std::accumulate` is roughly the same as the performance of the range-based for loop. However, using `std::accumulate` on Windows makes a big difference, making its performance much better than Linux.

![Summation with `std::acccumulate` on Linux](images/CaseStudies----CalculateWithStd.png)

Summation with `std::acccumulate` on Linux

![Summation with `std::acccumulate` on Windows](images/CaseStudies----CalculateWithStd_win.PNG)

Summation with `std::acccumulate` on Windows

Now we have our reference timings. Let me run two additional single threaded scenarios. One with a lock and the other with an atomic. Why? We get the performance numbers indicating how expensive the protection by a lock or an atomic is when there is no contention.

##### Protection with a Lock

If I protect access to the summation variable with a lock, I get the answers to two questions.

1.  How expensive is the synchronisation of a lock without contention?
2.  How fast can a lock be in the optimal case?

I only show the application of `std:lock_guard`. The entire source file is part of the resources for this book.

```
// calculateWithLock.cpp

...

std::mutex myMutex;

for (auto i: randValues){
  std::lock_guard<std::mutex> myLockGuard(myMutex);
  sum += i;
}

...
```

Summation of a vector by using a lock for the summation variable

The execution times are as expected: the access to the protected variable `sum` is slower.

![Single-threaded summation with `std::acccumulate` on Linux using a lock](images/CaseStudies----CalculateWithLock.png)

Single-threaded summation with `std::acccumulate` on Linux using a lock

![Single-threaded summation with `std::acccumulate` on Windows using a lock](images/CaseStudies----CalculateWithLock_win.PNG)

Single-threaded summation with `std::acccumulate` on Windows using a lock

Using a `std::lock_guard` without contention is about 50 - 150 times slower than using `std::accumulate`.

Let’s finally get to atomics.

##### Protection with Atomics

Accordingly, I have the same questions for atomics that I had for locks.

1.  How expensive is the synchronisation of an atomic?
2.  How fast can an atomic be if there is no contention?

I have an additional question; what is the performance difference of an atomic compared to a lock?

```
 1 // calculateWithAtomic.cpp
 2 
 3 #include <atomic>
 4 #include <chrono>
 5 #include <iostream>
 6 #include <numeric>
 7 #include <random>
 8 #include <vector>
 9 
10 constexpr long long size = 100000000;
11 
12 int main(){
13 
14   std::cout << std::endl;
15 
16   std::vector<int> randValues;
17   randValues.reserve(size);
18 
19   // random values
20   std::random_device seed;
21   std::mt19937 engine(seed());
22   std::uniform_int_distribution<> uniformDist(1, 10);
23   for (long long i = 0 ; i < size ; ++i) 
24       randValues.push_back(uniformDist(engine));
25   
26   std::atomic<unsigned long long> sum = {};
27   std::cout << std::boolalpha << "sum.is_lock_free(): " 
28             << sum.is_lock_free() << std::endl;
29   std::cout << std::endl;
30  
31   auto sta = std::chrono::steady_clock::now();
32   
33   for (auto i: randValues) sum += i;
34  
35   std::chrono::duration<double> dur = std::chrono::steady_clock::now() - sta;
36   
37   
38   std::cout << "Time for addition " << dur.count() 
39             << " seconds" << std::endl;
40   std::cout << "Result: " << sum << std::endl;
41     
42   std::cout << std::endl;
43   
44   sum = 0;
45   sta = std::chrono::steady_clock::now();
46   
47   for (auto i: randValues) sum.fetch_add(i);
48   
49   dur = std::chrono::steady_clock::now() - sta;
50   std::cout << "Time for addition " << dur.count() 
51             << " seconds" << std::endl;
52   std::cout << "Result: " << sum << std::endl;
53     
54   std::cout << std::endl;
55 
56 }
```

Summation of a vector by using an atomic as summation variable

First, I check in line 28 if the atomic `sum` has a lock. That is crucial because otherwise there would be no difference between using locks and atomics. On all mainstream platforms I know, atomics are [lock-free](#chap23.xhtml_glossaryXXXlockMMMfreeSSSBOBOBOGlossaryBCBCBC). Second, I calculate the sum in two ways. I use in line 33 the `+= operator`, in line 45 the method `fetch_add`. In the single threaded case both variants have comparable performance; however, for `fetch_add` I can explicitly specify the memory-ordering. More about that point in the next subsection.

Here are the results.

![Summation with an atomic on Linux](images/CaseStudies----CalculateWithAtomic.png)

Summation with an atomic on Linux

![Summation with an atomic on Windows](images/CaseStudies----CalculateWithAtomic_win.PNG)

Summation with an atomic on Windows

##### All Single Threaded Numbers

I want to stress three points.

1.  Atomics are 12 - 50 times slower on Linux and Windows than `std::accumulate` without synchronisation.
2.  Atomics are 2 - 3 times faster on Linux and Windows than locks.
3.  `std::accumulate` seems to be highly optimised on Windows.

Before we look at the multithreaded scenarios, here is a table summarising the results for single threaded execution. The unit is seconds.

Performance of all single threaded summations

| **Operating System (Compiler)** | **Range-based for loop** | **std::accumulate** | **Locks** | **Atomics** |
| --- | --- | --- | --- | --- |
| Linux (GCC) | 0.07 | 0.07 | 3.34 | 1.34 |
|   |   |   |   | 1.33 |
| Windows (cl.exe) | 0.08 | 0.03 | 4.07 | 1.50 |
|   |   |   |   | 1.61 |

#### Multithreaded Summation with a Shared Variable

You may have already guessed it. Using a shared variable for the summation with four threads is not optimal because the synchronisation overhead outweighs the performance benefit. Let me show you the numbers.

The questions I want to answer are still the same.

1.  What is the difference in performance between the summation using a lock and an atomic?
2.  What is the difference in performance between single threaded and multithreaded execution of `std::accumulate`?

##### Using a `std::lock_guard`

The simplest way to make the thread-safe summation is to use a [`std::lock_guard`](#chap06.xhtml_chapterXXXlock_guard).

```
 1 // synchronisationWithLock.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <mutex>
 6 #include <random>
 7 #include <thread>
 8 #include <utility>
 9 #include <vector>
10 
11 constexpr long long size = 100000000;   
12 
13 constexpr long long fir =  25000000;
14 constexpr long long sec =  50000000;
15 constexpr long long thi =  75000000;
16 constexpr long long fou = 100000000;
17 
18 std::mutex myMutex;
19 
20 void sumUp(unsigned long long& sum, const std::vector<int>& val, 
21            unsigned long long beg, unsigned long long end){
22     for (auto it = beg; it < end; ++it){
23         std::lock_guard<std::mutex> myLock(myMutex);
24         sum += val[it];
25     }
26 }
27 
28 int main(){
29 
30   std::cout << std::endl;
31 
32   std::vector<int> randValues;
33   randValues.reserve(size);
34 
35   std::mt19937 engine;
36   std::uniform_int_distribution<> uniformDist(1,10);
37   for (long long i = 0 ; i < size ; ++i) 
38       randValues.push_back(uniformDist(engine));
39  
40   unsigned long long sum = 0;
41   const auto sta = std::chrono::steady_clock::now();
42   
43   std::thread t1(sumUp, std::ref(sum), std::ref(randValues), 0, fir);
44   std::thread t2(sumUp, std::ref(sum), std::ref(randValues), fir, sec);
45   std::thread t3(sumUp, std::ref(sum), std::ref(randValues), sec, thi);
46   std::thread t4(sumUp, std::ref(sum), std::ref(randValues), thi, fou);   
47   
48   t1.join();
49   t2.join();
50   t3.join();
51   t4.join();
52   
53   std::chrono::duration<double> dur= std::chrono::steady_clock::now() - sta;
54   std::cout << "Time for addition " << dur.count() 
55             << " seconds" << std::endl;
56   std::cout << "Result: " << sum << std::endl;
57 
58   std::cout << std::endl;
59 
60 }
```

Multithreaded summation of a vector using a std::lock_guard

The program is easy to explain. The function `sumUp` (lines 20 - 26) is the work package that each thread executes. `sumUp` gets the summation variable `sum` and the `std::vector val` by reference. `beg` and `end` specifies the range of the summation. The `std::lock_guard` (line 23) is used to protect the shared sum. Each thread (lines 43 - 46) performs a quarter of the summation.

Here are the performance numbers of the program.

![Summation with a shared variable on Linux](images/CaseStudies----synchronisationWithLock.png)

Summation with a shared variable on Linux

![Summation with a shared variable on Windows](images/CaseStudies----synchronisationWithLock_win.png)

Summation with a shared variable on Windows

The bottleneck of the program is the shared variable `sum` because a `std::lock_guard` heavily synchronises it. One obvious solution comes immediately to mind: replace the heavyweight lock with a lightweight atomic.

##### Using an atomic variable

Now, the summation variable `sum` is an atomic. That means I don’t need the `std::lock_guard` anymore. Here is the modified `sumUp` function.

```
// synchronisationWithAtomic.cpp

...

void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
           unsigned long long beg, unsigned long long end){
    for (auto it = beg; it < end; ++it){
        sum += val[it];
    }
}

...
```

Summation of a vector by using an atomic

The performance numbers are quite weird on my Windows Laptop. The synchronisation with `std::lock_guard` is more than twice as fast as the atomic version.

![Summation with an atomic on Linux](images/CaseStudies----synchronisationWithAtomic.png)

Summation with an atomic on Linux

![Summation with an atomic on Windows](images/CaseStudies----synchronisationWithAtomic_win.png)

Summation with an atomic on Windows

In addition to using the `+=` operator on an atomic, you can use the `fetch_add` method. Let’s try it out.

##### Using the method `fetch_add`

Once more. The modification of the source code is minimal. I have only changed the summation expression to `sum.fetch_add(val[it])`.

```
// synchronisationWithFetchAdd.cpp

...

void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
           unsigned long long beg, unsigned long long end){
    for (auto it = beg; it < end; ++it){
        sum.fetch_add(val[it]);
    }
}

...
```

Summation of a vector by using the method fetch_add

Now we have similar performance as the previous example; there is little difference between the `operator +=` and `fetch_add`.

![Summation with an atomic on Linux](images/CaseStudies----synchronisationWithFetchAdd.png)

Summation with an atomic on Linux

![Summation with an atomic on Windows](images/CaseStudies----synchronisationWithFetchAdd_win.png)

Summation with an atomic on Windows

Although there is no performance difference between the `+=` operation and the `fetch_add` method on an atomic, `fetch_add` has an advantage; it allows me to weaken the memory-ordering explicitly and to apply relaxed semantic.

##### Using the method `fetch_add` with relaxed semantic

```
 1 // synchronisationWithFetchAddRelaxed.cpp
 2 
 3 ...
 4 
 5 void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
 6            unsigned long long beg, unsigned long long end){
 7     for (auto it = beg; it < end; ++it){
 8         sum.fetch_add(val[it], std::memory_order_relaxed);
 9     }
10 }
11 
12 ...
```

The default behaviour for atomics is [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency). This statement is true for the addition and assignment of an atomic and of course for the `fetch_add` method, but we can optimise even more. I adjust the memory-ordering in the summation expression to the [relaxed semantic](#chap05.xhtml_chapterXXXRelaxedSSSSemantic): `sum.fetch_add(val[it], std::memory_order_relaxed)`. The relaxed semantic is the weakest memory-ordering; therefore, the endpoint of my optimisation.

The relaxed semantic is fine in this use-case because we have two guarantees: each addition with `fetch_add` takes place atomically, and the threads synchronise with the join calls.

Because of the weakest memory model, we have the best performance.

![Summation with a relaxed atomic on Linux](images/CaseStudies----synchronisationWithFetchAddRelaxed.png)

Summation with a relaxed atomic on Linux

![Summation with a relaxed atomic on Windows](images/CaseStudies----synchronisationWithFetchAddRelaxed_win.png)

Summation with a relaxed atomic on Windows

##### All Multithreading Numbers with a Shared Variable

The units of the performance numbers are seconds.

Performance of all multi threaded summations

| **Operating System (Compiler)** | **std::lock_guard** | **atomic +=** | **fetch_add** | **fetch_add (relaxed)** |
| --- | --- | --- | --- | --- |
| Linux (GCC) | 20.81 | 7.78 | 7.87 | 7.66 |
| Windows (cl.exe) | 6.22 | 15.73 | 15.78 | 15.01 |

The result of the performance numbers is not promising. Using a shared atomic variable with relaxed semantic and calculating the sum with the help of four threads is about 100 times slower than using a single thread with the algorithm `std::accumulate`.

Let’s combine the two previous strategies for adding the numbers. I use four threads and minimise the synchronisation between the threads.

#### Thread-Local Summation

There are different ways to minimise the synchronisation. I can use local variables, [thread-local data](#chap09.xhtml_chapterXXXThreadSSSLocalSSSData), and [tasks](#chap06.xhtml_chapterXXXTasks).

##### Using a Local Variable

Since each thread can use a local summation variable, it can do its job without synchronisation. The synchronisation is only necessary, to sum up the local variables. The summation of the local variables is the critical section that must be protected. This can be done in various ways. A quick remark: since only four additions take place, it doesn’t matter from a performance perspective which synchronisation I use. I use a `std::lock_guard`, an atomic with sequential consistency and relaxed semantic for the summation.

###### `std::lock_guard`

```
 1 // localVariable.cpp
 2 
 3 #include <mutex>
 4 #include <chrono>
 5 #include <iostream>
 6 #include <random>
 7 #include <thread>
 8 #include <utility>
 9 #include <vector>
10 
11 constexpr long long size = 100000000;   
12 
13 constexpr long long fir =  25000000;
14 constexpr long long sec =  50000000;
15 constexpr long long thi =  75000000;
16 constexpr long long fou = 100000000;
17 
18 std::mutex myMutex;
19 
20 void sumUp(unsigned long long& sum, const std::vector<int>& val, 
21            unsigned long long beg, unsigned long long end){
22     unsigned long long tmpSum{};
23     for (auto i = beg; i < end; ++i){
24         tmpSum += val[i];
25     }
26     std::lock_guard<std::mutex> lockGuard(myMutex);
27     sum += tmpSum;
28 }
29 
30 int main(){
31 
32   std::cout << std::endl;
33 
34   std::vector<int> randValues;
35   randValues.reserve(size);
36 
37   std::mt19937 engine;
38   std::uniform_int_distribution<> uniformDist(1, 10);
39   for (long long i = 0; i < size; ++i) 
40        randValues.push_back(uniformDist(engine));
41  
42   unsigned long long sum{}; 
43   const auto sta = std::chrono::system_clock::now();
44   
45   std::thread t1(sumUp, std::ref(sum), std::ref(randValues), 0, fir);
46   std::thread t2(sumUp, std::ref(sum), std::ref(randValues), fir, sec);
47   std::thread t3(sumUp, std::ref(sum), std::ref(randValues), sec, thi);
48   std::thread t4(sumUp, std::ref(sum), std::ref(randValues), thi, fou);   
49   
50   t1.join();
51   t2.join();
52   t3.join();
53   t4.join();
54   
55   const std::chrono::duration<double> dur= 
56         std::chrono::system_clock::now() - sta;
57   
58   
59   std::cout << "Time for addition " << dur.count() 
60             << " seconds" << std::endl;
61   std::cout << "Result: " << sum << std::endl;
62 
63   std::cout << std::endl;
64 
65 }
```

Summation with minimal synchronisation using a `std::lock_guard`

Lines 26 and 27 are the interesting lines. These are the lines where the local summation result `tmpSum` is added to the global summation variable `sum`.

![Summation with a local variable on Linux](images/CaseStudies----localVariable.png)

Summation with a local variable on Linux

![Summation with a local variable on Windows](images/CaseStudies----localVariable_win.png)

Summation with a local variable on Windows

In the next two variations using a local variable, only the function `sumUp` changes; therefore, I just display the function. For the entire program, please refer to the source files.

###### Using an Atomic Variable with Sequential Consistency

Let’s replace the non-atomic global summation variable `sum` by an atomic.

```
 1 // localVariableAtomic.cpp
 2 
 3 ...
 4 
 5 void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
 6            unsigned long long beg, unsigned long long end){
 7     unsigned int long long tmpSum{};
 8     for (auto i = beg; i < end; ++i){
 9         tmpSum += val[i];
10     }
11     sum+= tmpSum;
12 }
13 
14 ...
```

Summation of a vector with minimal synchronisation and an atomic

Here are the performance numbers.

![Summation with a local variable on Linux](images/CaseStudies----localVariableAtomic.png)

Summation with a local variable on Linux

![Summation with a local variable on Windows](images/CaseStudies----localVariableAtomic_win.png)

Summation with a local variable on Windows

###### Using an Atomic Variable with Relaxed Semantic

We can do better. I use relaxed semantic now instead of the default memory-ordering. That’s well defined because the only guarantee we need is that all summations take place and are atomic.

```
 1 // localVariableAtomicRelaxed.cpp
 2 
 3 void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
 4            unsigned long long beg, unsigned long long end){
 5     unsigned int long long tmpSum{};
 6     for (auto i = beg; i < end; ++i){
 7         tmpSum += val[i];
 8     }
 9     sum.fetch_add(tmpSum, std::memory_order_relaxed);
10 }
11 
12 ...
```

Summation of a vector with minimal synchronisation and an atomic using relaxed semantic

As expected, it doesn’t make any difference whether I use a `std::lock_guard` or an atomic with sequential consistency or relaxed semantic.

![Summation with a local variable on Linux](images/CaseStudies----localVariableAtomicRelaxed.png)

Summation with a local variable on Linux

![Summation with a local variable on Windows](images/CaseStudies----localVariableAtomicRelaxed_win.png)

Summation with a local variable on Windows

Thread-local data is a particular kind of local data. It is lifetime is bound to the scope of the thread and not to the scope of the function, such as for the variable `tmpSum` in this example.

##### Using Thread-Local Data

Thread-local data belongs to the thread in which it was created; it is only be created when needed. Thread-local data is an ideal fit for the local summation variable `tmpSum`.

```
 1 // threadLocalSummation.cpp
 2 
 3 #include <atomic>
 4 #include <chrono>
 5 #include <iostream>
 6 #include <random>
 7 #include <thread>
 8 #include <utility>
 9 #include <vector>
10 
11 constexpr long long size = 100000000;   
12 
13 constexpr long long fir =  25000000;
14 constexpr long long sec =  50000000;
15 constexpr long long thi =  75000000;
16 constexpr long long fou = 100000000;
17 
18 thread_local unsigned long long tmpSum = 0;
19 
20 void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
21            unsigned long long beg, unsigned long long end){
22     for (auto i = beg; i < end; ++i){
23         tmpSum += val[i];
24     }
25     sum.fetch_add(tmpSum, std::memory_order_relaxed);
26 }
27 
28 int main(){
29 
30   std::cout << std::endl;
31 
32   std::vector<int> randValues;
33   randValues.reserve(size);
34 
35   std::mt19937 engine;
36   std::uniform_int_distribution<> uniformDist(1, 10);
37   for (long long i = 0; i < size; ++i) 
38       randValues.push_back(uniformDist(engine));
39  
40   std::atomic<unsigned long long> sum{}; 
41   const auto sta = std::chrono::system_clock::now();
42   
43   std::thread t1(sumUp, std::ref(sum), std::ref(randValues), 0, fir);
44   std::thread t2(sumUp, std::ref(sum), std::ref(randValues), fir, sec);
45   std::thread t3(sumUp, std::ref(sum), std::ref(randValues), sec, thi);
46   std::thread t4(sumUp, std::ref(sum), std::ref(randValues), thi, fou);   
47   
48   t1.join();
49   t2.join();
50   t3.join();
51   t4.join();
52   
53   const std::chrono::duration<double> dur= 
54         std::chrono::system_clock::now() - sta;
55         
56   std::cout << "Time for addition " << dur.count() 
57             << " seconds" << std::endl;
58   std::cout << "Result: " << sum << std::endl;
59 
60   std::cout << std::endl;
61 
62 }
```

Summation of a vector with minimal synchronisation using thread-local data

I declare in line 18 the thread-local variable `tmpSum` and use it for the addition in lines 23 and 25.

Here are the performance numbers using thread-local data.

![Summation with a thread-local variable on Linux](images/CaseStudies----threadLocalSummation.png)

Summation with a thread-local variable on Linux

![Summation with a thread-local variable on Windows](images/CaseStudies----threadLocalSummation_win.png)

Summation with a thread-local variable on Windows

In the last scenario, I use tasks.

##### Using Tasks

Using tasks, we can do the whole job without explicit synchronisation. Each partial summation is performed in a separate thread, and the final summation takes place in the main thread.

Here is the program:

```
 1 // tasksSummation.cpp
 2 
 3 #include <chrono>
 4 #include <future>
 5 #include <iostream>
 6 #include <random>
 7 #include <thread>
 8 #include <utility>
 9 #include <vector>
10 
11 constexpr long long size = 100000000;   
12 
13 constexpr long long fir =  25000000;
14 constexpr long long sec =  50000000;
15 constexpr long long thi =  75000000;
16 constexpr long long fou = 100000000;
17 
18 void sumUp(std::promise<unsigned long long>&& prom, const std::vector<int>& val, 
19            unsigned long long beg, unsigned long long end){
20     unsigned long long sum={};
21     for (auto i = beg; i < end; ++i){
22         sum += val[i];
23     }
24     prom.set_value(sum);
25 }
26 
27 int main(){
28 
29   std::cout << std::endl;
30 
31   std::vector<int> randValues;
32   randValues.reserve(size);
33 
34   std::mt19937 engine;
35   std::uniform_int_distribution<> uniformDist(1,10);
36   for (long long i = 0; i < size; ++i) 
37       randValues.push_back(uniformDist(engine));
38  
39   std::promise<unsigned long long> prom1;
40   std::promise<unsigned long long> prom2;
41   std::promise<unsigned long long> prom3;
42   std::promise<unsigned long long> prom4;
43   
44   auto fut1= prom1.get_future();
45   auto fut2= prom2.get_future();
46   auto fut3= prom3.get_future();
47   auto fut4= prom4.get_future();
48   
49   const auto sta = std::chrono::system_clock::now();
50 
51   std::thread t1(sumUp, std::move(prom1), std::ref(randValues), 0, fir);
52   std::thread t2(sumUp, std::move(prom2), std::ref(randValues), fir, sec);
53   std::thread t3(sumUp, std::move(prom3), std::ref(randValues), sec, thi);
54   std::thread t4(sumUp, std::move(prom4), std::ref(randValues), thi, fou);
55   
56   auto sum= fut1.get() + fut2.get() + fut3.get() + fut4.get();
57  
58   std::chrono::duration<double> dur= std::chrono::system_clock::now() - sta;
59   std::cout << "Time for addition " << dur.count() 
60             << " seconds" << std::endl;
61   std::cout << "Result: " << sum << std::endl;
62   
63   t1.join();
64   t2.join();
65   t3.join();
66   t4.join();
67 
68   std::cout << std::endl;
69 
70 }
```

Summation of a vector with minimal synchronisation using tasks

I define in lines 39 - 47 the four promises and the associated futures. In lines 51 - 54 each promise is moved to its thread. A promise can only be moved but not copied. The threads execute the function `sumUp` (lines 18 - 25). `sumUp` takes as its first argument a promise by rvalue reference. The futures ask in line 56 for the result of the summation by using the blocking `get` call.

![Summation with a local variable on Linux](images/CaseStudies----tasksSummation.png)

Summation with a local variable on Linux

![Summation with a local variable on Windows](images/CaseStudies----tasksSummation_win.png)

Summation with a local variable on Windows

To conclude this section, there is an overview of all performance numbers.

##### All Numbers for the Thread-Local Summation

It does not make a big difference whether I use local variables or tasks for the calculation of the partial sum or if I use various synchronisation primitives such as atomics. Only the thread-local data seems to make the program a little slower. This observation holds for Linux and Windows. Don’t be surprised by the higher performance of Linux relative to Windows. The program was optimised for 4 cores, and my Windows laptop has only two. The numbers are in seconds.

Performance of all thread-local summations

| **Operating System (Compiler)** | **std::lock_guard** | **Atomic using sequential consistency** | **Atomic using relaxed semantic** | **Thread-local data** | **Tasks** |
| --- | --- | --- | --- | --- | --- |
| Linux (GCC) | 0.03 | 0.03 | 0.03 | 0.04 | 0.03 |
| Windows (cl.exe) | 0.10 | 0.10 | 0.10 | 0.20 | 0.10 |

I want to draw our focus to a fascinating point. The thread-local multithreaded summation of the vector is about twice as fast as the single threaded summation. In the optimal case, I would expect a fourfold performance improvement because there is hardly a synchronisation necessary between the threads. What is the reason?

#### Summation of a Vector: The Conclusion

##### Single Threaded

The range-based for loop and the STL algorithm `std::accumulate` are in the same performance range. In the optimised version, the compiler uses for the summation case the optimised version vectorised [SIMD](https://en.wikipedia.org/wiki/SIMD) instruction (SSE or AVX). Therefore, the loop counter is increased by 4 (SSE) or 8 (AVX).

##### Multithreading with a Shared Variable

The usage of a shared variable for the summation variable makes one point clear: synchronisation is very expensive and should be avoided as much as possible. Although I used an atomic variable and even broke the sequential consistency, the four threads are 100 times slower than one thread. From a performance perspective, minimising expensive synchronisation has to be our first goal.

##### Thread-local Summation

The thread-local summation is only two times faster than the single-threaded range-based for loop or `std::accumulate`. That holds even though each of the four threads can work independently. That surprised me because I was expecting a nearly fourfold improvement. What surprised me even more, was that my four cores are not fully utilised.

![Utilisation of the four cores](images/CaseStudies----threadUtilization.png)

Utilisation of the four cores

The reason is simple; the cores can’t get the data fast enough from memory. The execution is [memory bound](https://en.wikipedia.org/wiki/Memory_bound_function). Or to say it the other way around, the memory slows down the cores. The following pictures show the bottleneck memory.

![The bottleneck memory](images/CaseStudies----MemoryArchitecture.png)

The bottleneck memory

The [Roofline model](https://en.wikipedia.org/wiki/Roofline_model) is an intuitive performance model to provide performance estimates of applications running on multi-core, or many-core architecture. The model depends on the peak performance, peak bandwidth, and arithmetic intensity of the architecture.

### Thread-Safe Initialisation of a Singleton

Before I start with this case study, let me emphasise: I am not advocating the use of the singleton pattern. Therefore, let me start this chapter to the thread-safe initialisation of a singleton with a warning.

I want to start my discussion of the thread-safe initialisation of the singleton with a short detour.

#### Double-Checked Locking Pattern

The [double-checked locking](http://www.cs.wustl.edu/~schmidt/PDF/DC-Locking.pdf) pattern is the classical way to initialise a singleton in a thread-safe way. What sounds like established best practice or as a pattern, is more a kind of [anti-pattern](https://en.wikipedia.org/wiki/Anti-pattern). It assumes guarantees in the traditional implementation, which aren’t given by the Java, C# or C++ memory model anymore. The wrong assumption is that the creation of a singleton is an atomic operation; therefore, a solution that seems to be thread-safe is not thread-safe.

What is the double-checked locking pattern? The first idea to implement a thread-safe singleton is to protect the initialisation of the singleton with a lock.

```
 1 std::mutex myMutex;
 2 
 3 class MySingleton{
 4 public:  
 5   static MySingleton& getInstance(){    
 6     std::lock_guard<mutex> myLock(myMutex);      
 7     if(!instance) instance = new MySingleton();    
 8     return *instance;  
 9   }
10 private:  
11   MySingleton() = default; 
12   ~MySingleton() = default;
13   MySingleton(const MySingleton&) = delete;  
14   MySingleton& operator= (const MySingleton&) = delete;
15   static MySingleton* instance;
16 };
17 
18 MySingleton* MySingleton::instance = nullptr;
```

Thread-safe initialisation with a lock

Any issues? Yes and no. Yes because there is a considerable performance penalty. No because the implementation is thread-safe. A heavyweight lock protects each access to the singleton in line 7\. This also applies to the read access, which after the initial construction of `MySingleton` is not necessary. Here comes the double-checked locking pattern to our rescue. Let’s have a look at the `getInstance` function.

```
1 static MySingleton& getInstance(){    
2   if (!instance){                                   // check
3     lock_guard<mutex> myLock(myMutex);              // lock
4     if(!instance) instance = new MySingleton();     // check
5   } 
6   return *instance; 
7 }
```

The double-checked locking pattern

Instead of the heavyweight lock, I use a lightweight pointer comparison in line 2\. If I get a null pointer, I apply the heavyweight lock on the singleton (line 3). Because there is the possibility that another thread initialises the singleton between the pointer comparison in line 2 and the lock call in line 3, I have to perform an additional pointer comparison in line 4\. So the name is obvious; two times a check and one time a lock.

Smart? Yes. Thread-safe? No.

What is the issue? The call `instance= new MySingleton()` in line 4 consists of at least three steps.

1.  Allocate memory for `MySingleton`
2.  Initialise the `MySingleton` object
3.  Let `instance` refer to the fully initialised `MySingleton` object

The issue is that the C++ runtime provides no guarantee that the steps are performed in that sequence. For example, it is possible that the processor may reorder the steps to the sequence 1,3 and 2\. So in the first step, the memory is allocated, and in the second step `instance` refers to a non-initialised singleton. If just at that moment another thread `t2` tries to access the singleton and makes the pointer comparison, the comparison succeeds. The consequence is that thread `t2` refers to a non-initialised singleton, and the program behaviour is undefined.

#### Performance Measurement

I want to measure how expensive it is to access a singleton object. For reference timing, I use a singleton which I access 40 million times sequentially. Of course, the first access initialises the singleton object. In contrast, the accesses from four threads is done concurrently. I’m only interested in the performance numbers. Therefore I sum up the execution time of the four threads. I measure the performance using a [static variable with block scope](#chap06.xhtml_chapterXXXStaticSSSVariables) (Meyers Singleton), a lock [`std::lock_guard`](#chap06.xhtml_chapterXXXlock_guard), the function [`std::call_once` in combination with the `std::once_flag`](#chap06.xhtml_chapterXXXcall_onceZZZonce_flag), and atomics with [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency) and [acquire release semantic](#chap05.xhtml_chapterXXXAcquire-ReleaseSSSSemantic).

The program runs on two PCs. My Linux PC with the GCC compiler has four cores while my Windows PC with the cl.exe compiler has two. I compile the program with maximum optimisation. Please refer to the beginning of this chapter for the [details about my setup](#chap09.xhtml_textXXXReferenceSSSPCs).

I want to answer two questions:

1.  What are the performance numbers of the various singleton implementations?
2.  Is there a significant difference between Linux (GCC) and Windows (cl.exe)?

Finally, I collect all numbers in a table.

Before I present the performance numbers of the various multithreading implementations, here is the sequential program. The `getInstance` method is not thread-safe with the C++03 standard.

```
 1 // singletonSingleThreaded.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 
 6 constexpr auto tenMill = 10000000;
 7 
 8 class MySingleton{
 9 public:
10   static MySingleton& getInstance(){
11     static MySingleton instance;
12     volatile int dummy{};
13     return instance;
14   }
15 private:
16   MySingleton() = default;
17   ~MySingleton() = default;
18   MySingleton(const MySingleton&) = delete;
19   MySingleton& operator=(const MySingleton&) = delete;
20   
21 };
22 
23 int main(){
24     
25   constexpr auto fourtyMill = 4 * tenMill;
26   
27   const auto begin= std::chrono::system_clock::now();
28   
29   for ( size_t i = 0; i <= fourtyMill; ++i){
30     MySingleton::getInstance();
31   }
32   
33   const auto end = std::chrono::system_clock::now() - begin;
34   
35   std::cout << std::chrono::duration<double>(end).count() << std::endl;
36 
37 }
```

Single-threaded singleton implementation

As the reference implementation, I use the so-called Meyers Singleton, named after [Scott Meyers](https://en.wikipedia.org/wiki/Scott_Meyers). The elegance of this implementation is that the singleton object in line 11 is a static variable with a block scope; therefore, `instance` is initialised only once. This initialisation happens when the static method `getInstance` (lines 10 - 14) is executed the first time.

Here are the reference numbers for the single threaded use-case.

![Meyers Singelton on Linux (single theaded)](images/CaseStudies----singletonSingleThreaded_opt.png)

Meyers Singelton on Linux (single theaded)

![Meyers Singleton on Windows (single theaded)](images/CaseStudies----singletonSingleThreaded_win_opt.png)

Meyers Singleton on Windows (single theaded)

The beauty of the Meyers Singleton is that it becomes thread-safe with C++11.

#### Thread-Safe Meyers Singleton

The C++11 standard guarantees that [static variables with block scope](#chap06.xhtml_chapterXXXStaticSSSVariables) are initialised in a thread-safe way. The Meyers Singleton uses a static variable with block scope, so we are done. The only work that is left to do is to rewrite the previously used [classical Meyers Singleton](#chap09.xhtml_textXXXMeyersSSSSingleton) for the multithreading use-case.

```
 1 // singletonMeyers.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <future>
 6 
 7 constexpr auto tenMill = 10000000;
 8 
 9 class MySingleton{
10 public:
11   static MySingleton& getInstance(){
12     static MySingleton instance;
13     volatile int dummy{};
14     return instance;
15   }
16 private:
17   MySingleton() = default;
18   ~MySingleton() = default;
19   MySingleton(const MySingleton&) = delete;
20   MySingleton& operator=(const MySingleton&) = delete;
21 
22 };
23 
24 std::chrono::duration<double> getTime(){
25 
26   auto begin = std::chrono::system_clock::now();
27   for (size_t i = 0; i <= tenMill; ++i){
28       MySingleton::getInstance();
29   }
30   return std::chrono::system_clock::now() - begin;
31   
32 };
33 
34 int main(){
35  
36     auto fut1= std::async(std::launch::async, getTime);
37     auto fut2= std::async(std::launch::async, getTime);
38     auto fut3= std::async(std::launch::async, getTime);
39     auto fut4= std::async(std::launch::async, getTime);
40     
41     const auto total= fut1.get() + fut2.get() + fut3.get() + fut4.get();
42     
43     std::cout << total.count() << std::endl;
44 
45 }
```

Meyers-Singleton in the multithreading use-case

I use the singleton object in the function `getTime` (lines 24 - 32). The function is executed by the four promises in lines 36 - 39\. The results of the associated futures are summed up in line 41. That’s all. Only the execution time is missing.

![Meyers Singleton on Linux (multi threaded)](images/CaseStudies----singletonMeyers_opt.png)

Meyers Singleton on Linux (multi threaded)

![Meyers Singleton on Windows (multi threaded)](images/CaseStudies----singletonMeyers_win_opt.png)

Meyers Singleton on Windows (multi threaded)

Let’s go for the most obvious one, and use a lock.

#### `std::lock_guard`

The mutex wrapped in a `std::lock_guard` guarantees that the singleton is initialised in a thread-safe way.

```
 1 // singletonLock.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <future>
 6 #include <mutex>
 7 
 8 constexpr auto tenMill = 10000000;
 9 
10 std::mutex myMutex;
11 
12 class MySingleton{
13 public:
14   static MySingleton& getInstance(){
15     std::lock_guard<std::mutex> myLock(myMutex);
16     if (!instance){
17         instance= new MySingleton();
18     }
19     volatile int dummy{};
20     return *instance;
21   }
22 private:
23   MySingleton() = default;
24   ~MySingleton() = default;
25   MySingleton(const MySingleton&) = delete;
26   MySingleton& operator=(const MySingleton&) = delete;
27 
28   static MySingleton* instance;
29 };
30 
31 
32 MySingleton* MySingleton::instance = nullptr;
33 
34 ...
```

A thread-safe singleton using a lock

You may have already guessed that this approach is pretty slow.

![Multi-threaded singleton on Linux using std::lock_guard](images/CaseStudies----singletonLock_opt.png)

Multi-threaded singleton on Linux using std::lock_guard

![Multi-threaded singleton on Windows using std::lock_guard](images/CaseStudies----singletonLock_win_opt.png)

Multi-threaded singleton on Windows using std::lock_guard

The next version of the thread-safe singleton pattern is also based on the multithreading library: it uses `std::call_once` in combination with the `std::once_flag`.

#### `std::call_once` with `std::once_flag`

You can use the function [std::call_once](#chap06.xhtml_chapterXXXcall_onceZZZonce_flag) together with the [std::once_flag](#chap06.xhtml_chapterXXXcall_onceZZZonce_flag) to register callables so that exactly one callable is executed in a thread-safe way.

```
 1 // singletonCallOnce.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <future>
 6 #include <mutex>
 7 #include <thread>
 8 
 9 constexpr auto tenMill = 10000000;
10 
11 class MySingleton{
12 public:
13   static MySingleton& getInstance(){
14     std::call_once(initInstanceFlag, &MySingleton::initSingleton);
15     volatile int dummy{};
16     return *instance;
17   }
18 private:
19   MySingleton() = default;
20   ~MySingleton() = default;
21   MySingleton(const MySingleton&) = delete;
22   MySingleton& operator=(const MySingleton&) = delete;
23 
24   static MySingleton* instance;
25   static std::once_flag initInstanceFlag;
26 
27   static void initSingleton(){
28     instance= new MySingleton;
29   }
30 };
31 
32 MySingleton* MySingleton::instance = nullptr;
33 std::once_flag MySingleton::initInstanceFlag;
34 
35 ...
```

A thread-safe singleton using std::call_once together with the `std::once_flag`

Here are the performance numbers.

![Multi-threaded singleton on Linux using `std::call_once` and `std::once_flag`](images/CaseStudies----singletonCallOnce_opt.png)

Multi-threaded singleton on Linux using `std::call_once` and `std::once_flag`

![Multi-threaded singleton on Windows using `std::call_once` and `std::once_flag`](images/CaseStudies----singletonCallOnce_win_opt.png)

Multi-threaded singleton on Windows using `std::call_once` and `std::once_flag`

Let’s continue our thread-safe singleton implementation using atomics.

#### Atomics

With atomic variables, my implementation becomes a lot more challenging. I can even specify the [memory-ordering](#chap05.xhtml_chapterXXXTheSSSSychronisationSSSandSSSOrderingSSSConstraints) for my atomic operations. The following two implementations of the thread-safe singletons are based on the previously mentioned [double-checked locking pattern](#chap09.xhtml_chapterXXXDoubleMMMCheckedSSSLockingSSSPattern).

##### Sequential consistency

In my first implementation I use atomic operations without explicitly specifying the memory-ordering; therefore [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency) applies.

```
 1 // singletonSequentialConsistency.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <future>
 6 #include <mutex>
 7 #include <thread>
 8 
 9 constexpr auto tenMill = 10000000;
10 
11 class MySingleton{
12 public:
13   static MySingleton* getInstance(){
14     MySingleton* sin = instance.load();
15     if (!sin){
16       std::lock_guard<std::mutex> myLock(myMutex);
17       sin = instance.load(std::memory_order_relaxed);
18       if(!sin){
19         sin= new MySingleton();
20         instance.store(sin);
21       }
22     }
23     volatile int dummy{};
24     return sin;
25   }
26 private:
27   MySingleton() = default;
28   ~MySingleton() = default;
29   MySingleton(const MySingleton&) = delete;
30   MySingleton& operator=(const MySingleton&) = delete;
31 
32   static std::atomic<MySingleton*> instance;
33   static std::mutex myMutex;
34 };
35 
36 
37 std::atomic<MySingleton*> MySingleton::instance;
38 std::mutex MySingleton::myMutex;
39 
40 ...
```

A thread-safe singleton using atomics with sequential consistency

In contrast to the double-checked locking pattern, I now have the guarantee that the expression `sin= new MySingleton()` in line 19 happens before the store expression `instance.store(sin)` in line 20\. This is due to the sequential consistency as default memory-ordering for atomic operations. Have a look at line 17: `sin = instance.load(std::memory_order_relaxed)`. This additional load is necessary because, between the first load in line 14 and the usage of the lock in line 16, another thread may kick in and change the value of `instance`.

![Multi-threaded singleton on Linux using atomics](images/CaseStudies----singletonSequentialConsistency_opt.png)

Multi-threaded singleton on Linux using atomics

![Multi-threaded singleton on Windows using atomics](images/CaseStudies----singletonSequentialConsistency_win_opt.png)

Multi-threaded singleton on Windows using atomics

We can optimise the program even more.

##### Acquire-release semantic

Let’s have a closer look at the previous thread-safe implementation of the singleton pattern using atomics. The loading (or reading) of the singleton in line 14 is an acquire operation, the storing (or writing) in line 20 a release operation. Both operations take place on the same atomic. Therefore sequential consistency is overkill. The C++11 standard guarantees that a release operation synchronises with an acquire operation on the same atomic and establishes an ordering constraint. This means that all previous read and write operations cannot be moved after a release operation, and all subsequent read and write operations cannot be moved before an acquire operation.

These are the minimum guarantees required to implement a thread-safe singleton.

```
 1 // singletonAcquireRelease.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <future>
 6 #include <mutex>
 7 #include <thread>
 8 
 9 constexpr auto tenMill = 10000000;
10 
11 class MySingleton{
12 public:
13   static MySingleton* getInstance(){
14     MySingleton* sin = instance.load(std::memory_order_acquire);
15     if (!sin){
16       std::lock_guard<std::mutex> myLock(myMutex);
17       sin = instance.load(std::memory_order_relaxed);
18       if(!sin){
19         sin = new MySingleton();
20         instance.store(sin, std::memory_order_release);
21       }
22     }   
23     volatile int dummy{};
24     return sin;
25   }
26 private:
27   MySingleton() = default;
28   ~MySingleton() = default;
29   MySingleton(const MySingleton&) = delete;
30   MySingleton& operator=(const MySingleton&) = delete;
31 
32   static std::atomic<MySingleton*> instance;
33   static std::mutex myMutex;
34 };
35 
36 
37 std::atomic<MySingleton*> MySingleton::instance;
38 std::mutex MySingleton::myMutex;
39 
40 ...
```

A thread-safe singleton using atomics with acquire-release semantic

The acquire-release semantic has similar performance as the sequential consistency.

![Multi-threaded singleton on Linux using atomics](images/CaseStudies----singletonAcquireRelease_opt.png)

Multi-threaded singleton on Linux using atomics

![Multi-threaded singleton on Windows using atomics](images/CaseStudies----singletonAcquireRelease_win_opt.png)

Multi-threaded singleton on Windows using atomics

This is not surprising because on the x86 architecture both memory-orderings are very similar. We would probably more significant difference in the performance numbers on the [ARMv7](https://en.wikipedia.org/wiki/ARM_architecture) or [PowerPC](https://en.wikipedia.org/wiki/PowerPC) architecture. You can read the details Jeff Preshings blog [Preshing on Programming](http://preshing.com/).

At the end here is an overview of all performance numbers.

#### Performance Numbers of the various Thread-Safe Singleton Implementations

The numbers give a clear indication. The Meyers Singleton is the fastest one. It is not only the fastest one, but it is also the easiest one to get. The Meyers Singleton is about two times faster than the atomic versions. As expected the synchronisation with the lock is the most heavyweight and, therefore, the slowest. `std::call_once` in particular on Windows is a lot slower than on Linux.

Performance of all singleton implementations

| **Operating System (Compiler)** | **Single Threaded** | **Meyers Singleton** | **std::lock_guard** | **std::call_once** | **Sequential Consistency** | **Acquire-Release Semantic** |
| --- | --- | --- | --- | --- | --- | --- |
| Linux (GCC) | 0.03 | 0.04 | 12.47 | 0.22 | 0.09 | 0.07 |
| Windows (cl.exe) | 0.02 | 0.03 | 15.48 | 1.74 | 0.07 | 0.07 |

I want to stress one point about the numbers explicitly. These are the summed up numbers for all four threads. That means that we get optimal concurrency with the Meyers Singleton because the Meyers Singleton is nearly as fast as the single threaded implementation.

### Ongoing Optimisation with CppMem

I start with a small program and improve it successively. I verify each step of my process with CppMem. [CppMem](http://svr-pes20-cppmem.cl.cam.ac.uk/cppmem/) is an interactive tool for exploring the behaviour of small code snippets using the C++ memory model.

First, here is the small program.

```
 1 // ongoingOptimisation.cpp
 2 
 3 #include <iostream>
 4 #include <thread>
 5 
 6 int x = 0;
 7 int y = 0;
 8 
 9 void writing(){
10   x = 2000;
11   y = 11;
12 }
13 
14 void reading(){ 
15   std::cout << "y: " << y << " ";
16   std::cout << "x: " << x << std::endl;
17 }
18 
19 int main(){
20   std::thread thread1(writing);
21   std::thread thread2(reading);
22   thread1.join();
23   thread2.join();
24 }
```

The reference program for the ongoing optimisation

The program is quite simple. It consists of the two threads `thread1` and `thread2`. `thread1` writes the values `x` and `y`. `thread2` reads the values `x` and `y` in the **opposite sequence**. This idea sounds straightforward, but even in this simple program, we get three different results:

![The reference program](images/CaseStudies----ongoingOptimisation.png)

The reference program

I have two questions in mind for my process of ongoing optimisation.

1.  Is the program well-defined? In particular: is there a [data-race](#chap20.xhtml_chapterXXXDataSSSRaces)?
2.  Which values for `x` and `y` are possible?

The first question is often very challenging to answer. In the first step, I think about the answer to the first question, and in the second step, I verify my reasoning with CppMem. Once I have answered the first question, the second answer can easily be determined from the first answer. I also present the possible values for `x` and `y` in a table.

However, I haven’t explained what I mean by ongoing optimisation. It’s pretty simple; I successively optimise the program by weakening the C++ memory-ordering. These are my optimisation steps:

*   Non-atomic variables
*   Locks
*   Atomics with sequential consistency
*   Atomics with acquire-release semantic
*   Atomics with relaxed semantic
*   Volatile variables

Before I start my process of ongoing optimisation, you should have a basic understanding of CppMem. The chapter [CppMem](#chap22.xhtml_chapterXXXCppMem) gives you a simplified introduction.

#### CppMem: Non-Atomic Variables

Using the run button shows it immediately there is a data race. To be more precise, it has two data races. Neither the access to the variable `x` nor the variable `y` is protected. As a result, the program has undefined behaviour. In C++ jargon, this means that the program has so-called catch fire semantic; therefore, all results are possible. Your PC can even catch fire.

So, we are not able to conclude the values of `x` and `y`.

This were my thoughts to `int`. Now we should have a look at what CppMem reports about the undefined behaviour of the program.

CppMem allows me to reduce the program to its bare minimum.

```
 1 int main() {
 2   int x = 0; 
 3   int y = 0;
 4   {{{ { 
 5         x = 2000; 
 6         y = 11;
 7       }
 8   ||| {
 9         y;
10         x;
11       }  
12   }}}
13 }
```

CppMem: unsynchronised access

You can define a thread in CppMem with the curly braces (lines 4 and 12) and the pipe symbol (line 8). The additional curly braces in lines 4 and 7 or lines 8 and 11 define the work package of the thread. Because I’m not interested in the output of the variables `x` and `y`, I only read them in lines 9 and 10.

That was the theory for CppMem, now to the practice.

##### The Analysis

When I execute the program, CppMem complains (1) (in red) that one of the four possible interleavings of threads is not race free. Only the first execution is consistent. Now I can use CppMem to switch between the four executions (2) and analyse the annotated graph (3).

![A data race with non-atomics](images/CaseStudies----FullExection.png)

A data race with non-atomics

You get the most out of CppMem by analysing the various graphs.

###### First Execution

What conclusions can we derive from the following graph?

![First execution](images/CaseStudies----first.png)

First execution

The nodes of the graph represent the expressions of the program, the edges the relation between the expressions. In my explanation, I refer to the names (a) to (f). What can I conclude from the annotations in this graph?

*   **a:Wna x = 0**: Is the first expression (a), which is a non-atomic write of `x`.
*   **sb (sequenced-before)**: The writing of the first expression (a) is sequenced before the writing of the second expression (b). These relations also holds between the expressions (c) and (d), and (e) and (f).
*   **rf (read from)**: The expression (e) reads the value of `y` from the expression (b). Accordingly, (f) reads from (a).
*   **sw (synchronizes-with)**: The expression (a) synchronises with (f). This relation holds because the expressions (f) takes place in a separate thread. Creation of a thread is a synchronisation point. Everything that happens before the thread creation is visible in the thread. For symmetry reasons, the same argument holds between (b) and (e).
*   **dr (data race)**: Here is the data race between the reading and writing of the variables `x` and `y`. The program has undefined behaviour.

The next three executions are not consistent.

###### Second Execution

![Second execution](images/CaseStudies----second.png)

Second execution

The expression (e) reads in this non-consistent execution the value of y from the expression (d). The writing of (d) happens concurrently with the reading of (e).

###### Third Execution

![Third execution](images/CaseStudies----third.png)

Third execution

This execution is symmetric to the previous execution. The expression (f) reads from expression (c) concurrently.

###### Fourth Execution

![Fourth exection](images/CaseStudies----four.png)

Fourth exection

Now everything goes wrong. The expressions (e) and (f) read from the expressions (d) and (c) concurrently.

###### A Short Conclusion

Although I just used the default configuration of CppMem, I got a lot of valuable information and insight. In particular, the graphs from CppMem showed:

*   All four combinations of `x` and `y` are possible: (0,0), (11,0), (0,2000), and (11,2000).
*   The program has at least one data race and, therefore, has undefined behaviour.
*   Only one of the four possible executions is consistent.

The access to `x` and `y` in this example was not synchronised, and we got a data race; therefore, undefined behaviour. The most obvious way for synchronisation is to use locks.

#### CppMem: Locks

Both threads `thread1` and `thread2` use the same mutex, wrapped in a [`std::lock_guard`](#chap06.xhtml_chapterXXXlock_guard).

```
 1 // ongoingOptimisationLock.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 #include <thread>
 6 
 7 int x = 0;
 8 int y = 0;
 9 
10 std::mutex mut;
11 
12 void writing(){
13   std::lock_guard<std::mutex> guard(mut);
14   x = 2000;
15   y = 11;
16 }
17 
18 void reading(){
19   std::lock_guard<std::mutex> guard(mut);
20   std::cout << "y: " << y << " ";
21   std::cout << "x: " << x << std::endl;
22 }
23 
24 int main(){
25   std::thread thread1(writing);
26   std::thread thread2(reading);
27   thread1.join();
28   thread2.join();
29 };
```

ongoing optimisation with locks

The program is well-defined. Depending on the execution order (`thread1` vs `thread2`), either both values are either at first read and then overwritten, or at first overwritten and then read. The following values for `x` and `y` are possible.

Possible values for locks

| **y** | **x** | **Values possible?** |
| --- | --- | --- |
| 0 | 0 | Yes |
| 11 | 0 |   |
| 0 | 2000 |   |
| 11 | 2000 | Yes |

Locks are easy to use, but the synchronisation is often too heavyweight. I now switch to a more lightweight strategy and use atomics.

#### CppMem: Atomics with Sequential Consistency

If you don’t specify the memory-ordering, [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency) is applied. Sequential consistency guarantees two properties. Each thread executes its instructions in source code order, and all threads follow the same global order.

Here is the optimised version of the program using atomics.

```
 1 // ongoingOptimisationSequentialConsistency.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <thread>
 6 
 7 std::atomic<int> x{0};
 8 std::atomic<int> y{0};
 9 
10 void writing(){  
11   x.store(2000);  
12   y.store(11);
13 }
14 
15 void reading(){  
16   std::cout << y.load() << " ";  
17   std::cout << x.load() << std::endl;
18 }
19 
20 int main(){
21   std::thread thread1(writing);
22   std::thread thread2(reading);
23   thread1.join();
24   thread2.join();
25 };
```

ongoing optimisation with atomics (sequential consistency)

Let’s analyse the program. The program is data race free because `x` and `y` are atomics. Therefore, only one question is left to answer. What values are possible for `x` and `y`? This question is easy to answer. Thanks to the sequential consistency, all threads have to follow the same global order.

It holds true:

*   `x.store(2000);` **happens-before** `y.store(11);`
*   `std::cout << y.load() << " ";` **happens-before** `std::cout << x.load() << std::endl;`

Hence: the value of `x.load()` cannot be `0` if `y.load()` has the value `11`, because `x.store(2000)` happens before `y.store(11)`.

All other values for `x` and `y` are possible. Here are three possible interleavings resulting in the three different values for `x` and `y`.

1.  `thread1` is completely executed before `thread2`.
2.  `thread2` is completely executed before `thread1`.
3.  `thread1` executes its first instruction `x.store(2000)` before `thread2` is completely executed.

Now all values for `x` and `y`.

Possible values for the atomics(sequential consistency)

| **y** | **x** | **Values possible?** |
| --- | --- | --- |
| 0 | 0 | Yes |
| 11 | 0 |   |
| 0 | 2000 | Yes |
| 11 | 2000 | Yes |

Let me verify my reasoning with CppMem.

##### CppMem

Here is the corresponding program in CppMem.

```
 1 int main(){
 2   atomic_int x = 0; 
 3   atomic_int y = 0;
 4   {{{ { 
 5         x.store(2000);
 6         y.store(11);
 7       }
 8   ||| {
 9         y.load();
10         x.load();
11       } 
12   }}}
13 }
```

CppMem: atomics (sequential consistency

First, a little bit of syntax. CppMem uses in lines 2 and 3 the `typedef atomic_int` for `std::atomic<int>`.

When I execute the program, I’m overwhelmed by the number of execution candidates.

![Ongoing Optimisation (sequential consistency)](images/CaseStudies----SequenzielleKonsistenz.png)

Ongoing Optimisation (sequential consistency)

There are 384 **(1)** possible execution candidates, only 6 of them are consistent. No candidate has a [data race](#chap20.xhtml_chapterXXXDataSSSRaces). I’m only interested in the six consistent executions and ignore the other 378 non-consistent executions. Non-consistent means, for example, that they do not respect the [modification order](#chap23.xhtml_glossaryXXXModificationSSSOrderSSSBOBOBOGlossaryBCBCBC) of the [memory model](#chap05.xhtml_chapterXXXMemorySSSModel).

I use the interface **(2)** to get the six annotated graphs.

We already know that all values for `x` and `y` are possible except for `y = 11` and `x = 0`. These results are possible because of sequential consistency. Now I’m curious, which interleaving of threads produces which values for `x` and `y`?

###### Execution for (y = 0, x = 0)

![Execution for (y = 0, x = 0)](images/CaseStudies----first_.png)

Execution for (y = 0, x = 0)

###### Executions for (y = 0, x = 2000)

![Execution for (y = 0, x = 2000)](images/CaseStudies----second_.png)

Execution for (y = 0, x = 2000)

![Execution for (y = 0, x = 2000)](images/CaseStudies----third_.png)

Execution for (y = 0, x = 2000)

![Execution for (y = 0, x = 2000)](images/CaseStudies----four_.png)

Execution for (y = 0, x = 2000)

![Execution for (y = 0, x = 2000)](images/CaseStudies----five_.png)

Execution for (y = 0, x = 2000)

###### Execution for (y = 11, x = 2000)

![Execution for (y = 11, x = 2000)](images/CaseStudies----six_.png)

Execution for (y = 11, x = 2000)

I’m not done with my analysis. I’m interested to get the answer to the question: Which sequence of instructions corresponds to which of the six graphs?

##### Sequence of Instructions

I have assigned to each sequence of instructions the corresponding graph.

![Sequence of instructions](images/CaseStudies----atomicInterleavingEng.png)

Sequence of instructions

Let me start with the more straightforward cases.

*   **(1)**: It’s quite simple to assign the graph (1) to the sequence (1). In the sequence (1) `x` and `y` have the values 0 because `y.load()` and `x.load()` are executed before the operations `x.store(2000)` and `y.store(11)`.
*   **(6)**: The reasoning for the execution (6) is similar. `y` has the value 11 and `x` the value 2000 because all load operations happen after all store operations.
*   **(2), (3), (4), (5)**: Now to the more interesting cases in which `y` has the value `0`, and `x` has the value `2000`. The yellow arrows (sc) in the graph are the key to my reasoning because they stand for the sequence of instructions. For example, let’s look at execution (2).
    *   **(2)**: The sequence of the yellow arrows (sc) in the graph (2) is: write `x = 2000` ⇒ read `y = 0` ⇒ write `y = 11` ⇒ read `x = 2000`. This sequence corresponds to the sequence of instructions of the second interleaving of threads (2).

Let’s break the sequential consistency with the acquire-release semantic.

#### CppMem: Atomics with Acquire-Release Semantic

The synchronisation in the [acquire-release semantic](#chap05.xhtml_chapterXXXAcquire-ReleaseSSSSemantic) takes place between atomic operations on the same atomic. This synchronisation on atomic operations on the same atomic is in contrast to the sequential consistency where we have synchronisation between threads. Due to this fact, the acquire-release semantic is more lightweight and, therefore, faster.

Here is the program with acquire-release semantic.

```
 1 // ongoingOptimisationAcquireRelease.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <thread>
 6 
 7 std::atomic<int> x{0};
 8 std::atomic<int> y{0};
 9 
10 void writing(){  
11   x.store(2000, std::memory_order_relaxed);  
12   y.store(11, std::memory_order_release);
13 }
14 
15 void reading(){  
16   std::cout << y.load(std::memory_order_acquire) << " ";  
17   std::cout << x.load(std::memory_order_relaxed) << std::endl;
18 }
19 
20 int main(){
21   std::thread thread1(writing);
22   std::thread thread2(reading);
23   thread1.join();
24   thread2.join();
25 };
```

ongoing optimisation with atomics (acquire-release semantic)

On first glance, you notice that all operations are atomic, so the program is well-defined. But the second glance shows more; the atomic operations on `y` are attached with the flag `std::memory_order_release` (line 12) and `std::memory_order_acquire` (line 16). In contrast to that, the atomic operations on `x` are annotated with `std::memory_order_relaxed` (lines 11 and 17). So there are no synchronisation and ordering constraints for `x`. The answer to the possible values for `x` and `y` can only be given by `y`.

It holds:

*   `y.store(11,std::memory_order_release)` **synchronizes-with** `y.load(std::memory_order_acquire)`
*   `x.store(2000,std::memory_order_relaxed)` **is visible before** `y.store(11, std::memory_order_release)`
*   `y.load(std::memory_order_acquire)` **is visible before** `x.load(std::memory_order_relaxed)`

I elaborate a little bit more on these three statements. The key idea is that the store of `y` in line 12 synchronises with the load of `y` in line 16\. This is because the operations take place on the same atomic, and they use the acquire-release semantic. `y` uses `std::memory_order_release` in line 12 and `std::memory_order_acquire` in line 16\. The pairwise operation on `y` has another very impressive property. They establish a kind of barrier relative to `y`. So `x.store(2000, std::memory_order_relaxed)` cannot be executed after `y.store(std::memory_order_release)` and x.load() cannot be executed before `y.load()`.

The reasoning in the case of the acquire-release semantic is more sophisticated than in the case of the previous sequential consistency, but the possible values for `x` and `y` are the same. Only the combination `y == 11` and `x == 0` is not possible.

There are three different interleavings of the threads possible, which produce the three different combinations of the values `x` and `y`.

*   `thread1` is executed before `thread2`.
*   `thread2` is executed before `thread1`.
*   `thread1` executes `x.store(2000)` before `thread2` is executed.

To make a long story short, here are all possible values for `x` and `y`.

Possible values for the atomics(acquire-release semantic)

| **y** | **x** | **Values possible?** |
| --- | --- | --- |
| 0 | 0 | Yes |
| 11 | 0 |   |
| 0 | 2000 | Yes |
| 11 | 2000 | Yes |

Once more. Let’s verify our thinking with CppMem.

##### CppMem

Here is the corresponding program.

```
 1 int main(){
 2   atomic_int x = 0; 
 3   atomic_int y = 0;
 4   {{{ { 
 5       x.store(2000, memory_order_relaxed);
 6       y.store(11, memory_order_release);
 7       }
 8   ||| {
 9       y.load(memory_order_acquire);
10       x.load(memory_order_relaxed);
11       } 
12   }}}
13 }
```

CppMem: atomics(acquire-release semantic

We already know that all results are possible except for (y = 11, x = 0).

###### Possible executions

I only refer to the three graphs with consistent execution. The graphs show that there is an acquire-release semantic between the store-release of `y` and the load-acquire operation of `y`. It makes no difference if the reading of `y` **(rf)** takes places in the main thread or a separate thread. The graphs show the *synchronizes-with* relation using a **sw** annotated arrow.

###### Execution for (y = 0, x = 0)

![Execution for (y = 0, x = 0)](images/CaseStudies----first_ar.png)

Execution for (y = 0, x = 0)

###### Execution for (y = 0, x = 2000)

![Execution for (y = 0, x = 2000)](images/CaseStudies----second_ar.png)

Execution for (y = 0, x = 2000)

###### Execution for (y = 11, x = 2000)

![Execution for (y = 11, x = 2000)](images/CaseStudies----third_ar.png)

Execution for (y = 11, x = 2000)

`x` does not have to be atomic. This was my first and wrong assumption. See why.

#### CppMem: Atomics with Non-atomics

A [typical misunderstanding](#chap05.xhtml_chapterXXXTheSSSTypicalSSSMinunderstanding) in the application of the acquire-release semantic is to assume that the acquire operation is waiting for the release operation. Based on this wrong assumption, you may think that `x` does not has to be an atomic variable, and we can further optimise the program.

```
 1 // ongoingOptimisationAcquireReleaseBroken.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <thread>
 6 
 7 int x = 0;
 8 std::atomic<int> y{0};
 9 
10 void writing(){  
11   x = 2000;  
12   y.store(11, std::memory_order_release);
13 }
14 
15 void reading(){  
16   std::cout << y.load(std::memory_order_acquire) << " ";  
17   std::cout << x << std::endl;
18 }
19 
20 int main(){
21   std::thread thread1(writing);
22   std::thread thread2(reading);
23   thread1.join();
24   thread2.join();
25 };
```

ongoing optimisation with atomics with non-atomics

The program has a data race on `x` and, therefore, undefined behaviour. The acquire-release semantic guarantees if `y.store(11, std::memory_order_release)` (line 12) is executed before `y.load(std::memory_order_acquire)` (line 16), that `x = 2000` (line 11) is executed before the reading of `x` (line 17). If not the reading of `x` is executed at the same time as the writing of `x`. So we have concurrent access to a shared variable, and one of them is a write operation. That is by definition a [data race](#chap20.xhtml_chapterXXXDataSSSRaces).

To make my point more clear, let me use CppMem.

##### CppMem

```
 1 int main(){
 2   int x = 0;
 3   atomic_int y = 0;
 4   {{{ { 
 5       x = 2000;
 6       y.store(11, memory_order_release);
 7       }
 8   ||| {
 9       y.load(memory_order_acquire);
10       x;
11       }
12   }}}
13 }
```

CppMem: atomics and non-atomics

The data race occurs when one thread is writing `x = 2000` and the other thread is reading `x`. We get a **dr** symbol (data race) on the corresponding yellow arrow.

![A data race](images/CaseStudies----raceAcquireRelease.png)

A data race

The final step in the process of ongoing optimisation is still missing: relaxed semantic.

#### CppMem: Atomics with Relaxed Semantic

With the relaxed semantic, we have no synchronisation and ordering constraints on atomic operations, only the atomicity of the operations is guaranteed.

```
 1 // ongoingOptimisationRelaxedSemantic.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 #include <thread>
 6 
 7 std::atomic<int> x{0};
 8 std::atomic<int> y{0};
 9 
10 void writing(){  
11   x.store(2000, std::memory_order_relaxed);  
12   y.store(11, std::memory_order_relaxed);
13 }
14 
15 void reading(){  
16   std::cout << y.load(std::memory_order_relaxed) << " ";  
17   std::cout << x.load(std::memory_order_relaxed) << std::endl;
18 }
19 
20 int main(){
21   std::thread thread1(writing);
22   std::thread thread2(reading);
23   thread1.join();
24   thread2.join();
25 };
```

Ongoing optimisation with atomics (relaxed semantic)

For the relaxed semantic, my fundamental questions are straightforward to answer. These are my questions:

1.  Does the program have well-defined behaviour?
2.  Which values for `x` and `y` are possible?

On the one hand, all operations on `x` and `y` are atomic, so the program is well-defined. On the other hand, there are no restrictions on the possible interleavings of threads. The result may be that `thread2` sees the operations on `thread1` in a different order. This is the first time in our process of ongoing optimisation that `thread2` can display `x == 0` and `y == 11` and, therefore, all combinations of `x` and `y` are possible.

Possible values for the atomics(relaxed semantic)

| **y** | **x** | **Values possible?** |
| --- | --- | --- |
| 0 | 0 | Yes |
| 11 | 0 | Yes |
| 0 | 2000 | Yes |
| 11 | 2000 | Yes |

Now I’m curious how the graph of CppMem looks like for `x == 0` and `y == 11`?

##### CppMem

```
 1 int main(){
 2   atomic_int x = 0;
 3   atomic_int y = 0;
 4   {{{ { 
 5       x.store(2000, memory_order_relaxed);
 6       y.store(11, memory_order_relaxed);
 7       }
 8   ||| {
 9       y.load(memory_order_relaxed);
10       x.load(memory_order_relaxed);
11       }
12   }}}
13 }
```

CppMem: atomics (relaxed semantic)

That was the CppMem program. Now to the graph that produces the counter-intuitive behaviour.

![Execution for (y = 11, x = 0)](images/CaseStudies----first_rs.PNG)

Execution for (y = 11, x = 0)

`x` reads the value 0 (line 10) but `y` reads the value 11 (line 9). This happens, although the writing of `x` (line 5) is sequenced before the writing of `y` (line 6).

### Conclusion

Using a small program and successively improve it was quite enlighting. First, with each step more interleavings of threads were possible; therefore, more different values for `x` and `y` were possible. Second, the challenge of the program increases with each improvement. Even for this small program, CppMem provides invaluable services.

## The Future: C++23

This chapter is about the future of C++: C++23\. In this chapter, my intent is not to be as precise as the other chapters in this book. That’s for two reasons. First, not all of the presented features make it into the C++23 standard. Second, if a feature makes it into the C++23 standard, the interface of that feature changes very likely. This hold in particular true for the executors. I update this book on a regular basis and, therefore, reflect the updated and new proposals in this chapter.

My goal in this chapter is quite simple: give you an idea about the upcoming concurrency features in C++23.

![Concurrency in C++23](images/timeline----timeline23.png)

Concurrency in C++23

### Executors

Executors are the basic building block for execution in C++ and fulfil a similar role for execution such as allocators for the containers in C++. Functions such as [`async`](#chap06.xhtml_chapterXXXasync), the [parallel algorithms of the Standard Template Library](#chap07.xhtml_chapterXXXParallelSSSAlgorithmsSSSofSSStheSSSSTL), the [`then`](#chap10.xhtml_chapterXXXExtendedSSSFutures) continuation of futures, the run methods of [task blocks](#chap10.xhtml_chapterXXXTaskSSSBlocks), or the `post`, `dispatch`, or `defer` calls of the [Networking TS](https://en.cppreference.com/w/cpp/experimental) use them. Also, execution is a fundamental concern of programming there is no standardised way to perform execution.

Here is the introductory example of the proposal [P0761](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0761r2.pdf).

```
void parallel_for(int facility, int n, function<void(int)> f) {
  if(facility == OPENMP) {
    #pragma omp parallel for
    for(int i = 0; i < n; ++i) {
      f(i);
    }
  }
else if(facility == GPU) {
  parallel_for_gpu_kernel<<<n>>>(f);
}
else if(facility == THREAD_POOL) {
  global_thread_pool_variable.submit(n, f);
  }
}
```

Various parallel_for implementations

This `parallel_for` function has a few issues.

*   A simple function such as `parallel_for` is entirely **complex** to maintain. The complexity gets worse and worser if new algorithms or new parallel paradigms should be supported.
*   Each branch of the function has different **synchronisation** properties. [OpenMP](https://en.wikipedia.org/wiki/OpenMP) may block until all spawning threads are done, GPU runs typically asynchronously, and a thread pool may block or not. Insufficient synchronisation may end in a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) or [deadlock](#chap20.xhtml_chapterXXXDeadlocks). In the best case, you get a [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition).
*   The `parallel_for` loop is too **restrictive**. For example, there is no way to use your thread pool instead of the global thread pool in the function: `global_thread_pool_variable.submit(n, f);`.

#### A long Way

At October 2018 many proposals were written for executors, and many design decisions are still open. The expectation is that they are part of C++23\. There is the chance the one-way execution is even standardised with C++20\. This chapter is mainly based on the proposals to the design of executors [P0761](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0761r2.pdf), and to their formal description in [P0443](http://open-std.org/JTC1/SC22/WG21/docs/papers/2018/p0443r7.html) and [P1244](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1244r0.html). P0443 (A Unified Executors Proposal for C++) propose the one-way execution which may be part of C++20 and P1244 (Dependent Execution for a Unified Executors Proposal for C++) propose the dependent execution which may be part of C++23\. This chapter also refers to the relatively new “Modest Executor Proposal” [P1055](http://open-std.org/JTC1/SC22/WG21/docs/papers/2018/p1055r0.pdf).

#### What is an Executor?

First of all. What is an executor? An executor consists of a set of rules about **where**, **when** and **how** to run a [callable unit](#chap10.xhtml_glossaryXXXCallableSSSUnit).

*   **Where**: The callable may run on an internal or external processor and that the result is read back from the internal or external processor.
*   **When**: The callable may run immediately or be scheduled for a later time.
*   **How**: The callable may run on a CPU or GPU or even be executed in a vectorised way.

More formally, each executor has properties associated with the performed [execution function](#chap10.xhtml_chapterXXXexecutionSSSfunction).

##### Executor Properties

You can associate these properties with an executor in two ways: `execution::require`, or `execution::prefer`.

1.  **Directionality**: The execution function can be of kind “fire and forget” (`execution::oneway`), return a future (`execution::twoway`), or return a continuation (`execution::then`).
2.  **Cardinality:** The execution function can create one (`execution::single`) or multiple execution agents (`execution::bulk`).
3.  **Blocking**: The function may block or not. There are three mutually-exclusive blocking properties: `execution::blocking.never`, `execution::blocking.possibly`, and `execution::blocking.always`.
4.  **Continuations**: The task may be performed on the client’s calling thread (`execution::continuation`) or not (`execution::not_continuation`).
5.  **Future task submission**: Specify if outstanding work is likely (`exection::outstanding_work.tracked`) or not (`execution::outstanding_work.untracked`):
6.  **Bulk forward progress guarantees**: Specifies the the mutually-exclusive forward progress guarantees of execution agents created in bulk: `execution::bulk_sequenced_execution`, `execution::bulk_parallel_execution`, and `execution::bulk_unsequenced_execution`.
7.  **Thread execution mapping guarantees**: Should each execution agent be mapped to a new thread (`execution::new_thread_execution_mapping`) or not (`execution::thread_execution_mapping`).
8.  **Allocators**: Associates an allocator (`execution::allocator`) with an executor.

You can even define your properties.

#### First Examples

##### Using an Executor

Here are a few code snippets showing the usage of executors:

###### The promise `std::async`

```
// get an executor through some means
my_executor_type my_executor = ...

// launch an async using my executor
auto future = std::async(my_executor, [] {
    std::cout << "Hello world, from a new execution agent!" << std::endl;
});
```

Executing an `std::async`

###### The STL Algorithm `std::for_each`

```
// get an executor through some means
my_executor_type my_executor = ...

// execute a parallel for_each "on" my executor
std::for_each(std::execution::par.on(my_executor), 
              data.begin(), data.end(), func);
```

Performing `std::for_each` in parallel on `my_executor`

###### Networking TS: Accepting a Client Connection with the Default System Executor

```
// obtain an acceptor (a listening socket) through some means
tcp::acceptor my_acceptor = ...

// perform an asynchronous operation to accept a new connection
acceptor.async_accept(
    [](std::error_code ec, tcp::socket new_connection)
    {
      ...
    }
  );
```

Using the system executor to accept new connections

###### Networking TS: Accepting a Client Connection with a Thread Pool Executor

```
// obtain an acceptor (a listening socket) through some means
tcp::acceptor my_acceptor = ...

// obtain an executor for a specific thread pool
auto my_thread_pool_executor = ...

// perform an asynchronous operation to accept a new connection
acceptor.async_accept(
    std::experimental::net::bind_executor(my_thread_pool_executor,
      [](std::error_code ec, tcp::socket new_connection)
      {
        ...
      }
    )
  );
```

Using a thread pool executor to accept new connections

The function `std::experimental::net::bind_executor` from the networking TS [N4734](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/n4734.pdf) allows it to use a specific executor. In this case, the completion handler runs on a thread pool and executes the lambda function.

To use an executor you have to obtain it.

##### Obtaining an Executor

There are various ways to obtain an executor.

###### From the Execution Context `static_thread_pool`

```
// create a thread pool with 4 threads
static_thread_pool pool(4);

// get an executor from the thread pool
auto exec = pool.executor();

// use the executor on some long-running task
auto task1 = long_running_task(exec);
```

An executor from an execution context

###### From the [Execution Policy](#chap10.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseq) `std::execution::par`

```
// get par's associated executor
auto par_exec = std::execution::par.executor();

// use the executor on some long-running task
auto task2 = long_running_task(par_exec);
```

An executor from an execution policy

###### From the System Executor

This is the default executor that usually uses a thread for the execution. It is used if another one is not specified.

###### From an Executor Adapter

```
// get an executor from a thread pool
auto exec = pool.executor();

// wrap the thread pool's executor in a logging_executor
logging_executor<decltype(exec)> logging_exec(exec);

// use the logging executor in a parallel sort
std::sort(std::execution::par.on(logging_exec), my_data.begin(), my_data.end());
```

An executor from an executor adaptor

`logging_executor` is in the code snippet a wrapper for the `pool` executor.

#### Goals of an Executor Concept

What are the goals of an executor concept according to the proposal [P1055](http://open-std.org/JTC1/SC22/WG21/docs/papers/2018/p1055r0.pdf)?

1.  **Batchable**: control the trade-off between the cost of the transition of the callable and the size of it.
2.  **Heterogenous**: allow the callable to run on heterogeneous contexts and get the result back.
3.  **Orderable**: specify the order in which the callables are invoked. The goal includes ordering guarantees such as [LIFO](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) (**L**ast **I**n, **F**irst **O**ut), [FIFO](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)) (**F**irst **I**n, **F**irst **O**ut) execution, priority or time constraints, or even sequential execution.
4.  **Controllable**: the callable has to be targetable to a specific computing resource, deferred, or even cancelled.
5.  **Continuable**: to control an asynchronous callable signals are needed. These signals have to indicate, whether the result is available, whether an error occurred, when the callable is done or if the callee wants to cancel the callable. The explicit starting of the callable or the stopping of the starting callable should also be possible.
6.  **Layerable**: hierarchies allow capabilities to be added without increasing the complexity of the simpler use-cases.
7.  **Usable**: ease of use for the implementer and the user should be the main goal.
8.  **Composable**: allows a user to extend the executors for features that are not part of the standard.
9.  **Minimal**: nothing should exist on the executor concepts that could be added externally in a library on top of the concept.

#### Terminology

The Proposal [P0761](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0761r2.pdf) defines a few new terms for the execution of a callable:

*   **Execution resource**: is an instance of a hardware and/or software capability capable of executing a callable. An execution unit can range from a SIMD vector unit to an entire runtime managing a large collection of threads. Execution resources such as a CPU or a GPU are heterogeneous, because they have different freedoms and restrictions.
*   **Execution context**: is a program object that represents a specific collection of execution resources and the execution agents that exist within those resources. Typical examples are a thread pool or a distributed or a heterogenous runtime.
*   **Execution agent**: is a unit of execution of a specific execution context that is mapped to a single invocation of a callable on an execution resource. Typical examples are a CPU thread or an GPU execution unit.
*   **Executor**: is an object associated with a specific execution context. It provides one or more execution functions for creating execution agents from a callable function object.

#### Execution Functions

According to the previous paragraph, an executor provides one or more execution function for creating execution agents from a callable. An executor has to support at least one of the six following functions.

The execution functions of an executor

| **Name** | **Cardinality** | **Direction** |
| --- | --- | --- |
| `execute` | `single` | `oneway` |
| `twoway_execute` | `single` | `twoway` |
| `then_execute` | `single` | `then` |
| `bulk_execute` | `bulk` | `oneway` |
| `bulk_twoway_execute` | `bulk` | `twoway` |
| `bulk_then_execute` | `bulk` | `then` |

Each execution function has two properties: cardinality and direction.

*   Cardinality
    *   `single`: creates one execution agents
    *   `bulk`: creates a group of execution agents
*   Direction
    *   `oneway`: creates an execution agent and does not return a result
    *   `twoway`: creates an execution agent and does return a future that can be used to wait for execution to complete
    *   `then`: creates an execution agent and does return a future that can be used to wait for execution to complete. The execution agent begins execution after a given future `pred` becomes ready.

Let me explain the execution functions more informally.

All of them take a callable.

##### Single Cardinality

The single cardinality is straightforward. A `oneway` execution function is a fire and forget job and returns `void`. It’s quite similar to a [fire and forget future](#chap06.xhtml_chaperXXXFireSSSandSSSForget), but it does not automatically block in the destructor of the future. A `twoway` execution function returns you a future which you can use to pick up the result. This behaves similarly to a [`std::promise`](#chap06.xhtml_chapterXXXpromise) that give you back the handle to the associated `std::future`. In the `then` case it is a kind of continuation. It gives you back a future, but the execution agent runs only if the provided future `pred` is `ready`.

##### Bulk Cardinality

The bulk cardinality case is more complicated. These functions create a group of execution agents, and each of these execution agents calls the given callable `f`. They return the result of a result factory and not the result of a single callable `f` invoked by the execution agents. The first parameter of `f` is the shape parameter, which is an integral type and stands for the index of the type of the agent. Further arguments are the result factory if it is a `twoway` executor and a shape factory, which is shared by all agents. The lifetime of the shared parameter created by the shared factory is bound to the lifetime of the agents. Both are called factories because they produce their value by executing a callable and run before the agents. The client is responsible to disambiguate the right result via this result factory.

When the function `bulk_then_execute` is used, the callable `f` takes its predecessor future as an additional argument. The callable `f` takes the result, the shared parameter, and the predecessor by reference because no agent is an owner.

##### `execution::require`

How can you be sure that your executor supports the specific execution function?

In the special case, you know it.

```
void concrete_context(const my_oneway_single_executor& ex)
{
  auto task = ...;
  ex.execute(task);
}
```

Use an oneway single executor

In the general case, you can use the function `execution::require` to ask for it.

```
template<class Executor>
void generic_context(const Executor& ex)
{
  auto task = ...;

  // ensure .toway_execute() is available with execution::require()
  execution::require(ex, execution::single, execution::twoway).toway_execute(task);
}
```

Ask for an twoway_execute single executor

#### A Prototype Implementation

Based on the proposal [P0443R5](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0443r5.html), an protoype implementation of the executor proposal is available. This prototype implementation helped me a lot to get a deeper understanding of the bulk cardinality in particular.

```
 1 // executor.cpp
 2 
 3 #include <atomic>
 4 #include <experimental/thread_pool>
 5 #include <iostream>
 6 #include <utility>
 7 
 8 namespace execution = std::experimental::execution;
 9 using std::experimental::static_thread_pool;
10 using std::experimental::executors_v1::future;
11 
12 int main(){
13     
14     static_thread_pool pool{4};
15     auto ex = pool.executor();
16 
17     // One way, single.
18     ex.execute([]{ std::cout << "We made it!" << std::endl; });
19   
20     std::cout << std::endl;
21 
22     // Two way, single.
23     future<int> f1 = ex.twoway_execute([]{ return 42; });
24     f1.wait();
25     std::cout << "The result is: " << f1.get() << std::endl;
26   
27     std::cout << std::endl;
28 
29     // One way, bulk.
30     ex.bulk_execute([](int n, int& sha){ 
31         std::cout << "part " << n << ": " << "shared: " << sha <<  "\n"; 
32         }, 8, 
33         []{ return 0; }
34     );
35   
36     std::cout << std::endl;
37 
38     // Two way, bulk, void result.
39     future<void> f2 = ex.bulk_twoway_execute(
40         [](int n, std::atomic<short>& m){
41             std::cout << "async part " << n ;
42             std::cout << " atom: " << m++ << std::endl;
43         }, 8, 
44         []{}, 
45         []{
46             std::atomic<short> atom(0);
47             return std::ref(atom); 
48         }
49     );
50     f2.wait();
51     std::cout << "bulk result available" << std::endl;
52   
53     std::cout << std::endl;
54 
55     // Two way, bulk, non-void result.
56     future<double> f3 = ex.bulk_twoway_execute(
57         [](int n, double&, int &){ 
58             std::cout << "async part " << n << " ";
59             std::cout << std::this_thread::get_id() << std::endl;
60         }, 8, 
61         []{ 
62             std::cout << "Result factory: " 
63                       << std::this_thread::get_id() << std::endl;
64             return 123.456; }, 
65         []{ 
66             std::cout << "Shared Parameter: " 
67                       << std::this_thread::get_id() << std::endl;
68             return 0; }
69     );
70     f3.wait();
71     std::cout << "bulk result is " << f3.get() << std::endl;
72   
73 }
```

A prototype implementation of the executors

The program uses as executor a thread pool of four threads (lines 14 and 15). The lines 18 and 23 uses execution functions of single cardinality and create two agents of single cardinality. The second one is a `twoway` execution function and returns, therefore, a result.

The remaining execution functions in lines 30, 39, and 56 are of bulk cardinality. Each function creates eight agents (lines 32, 43, and 60). In the first case, the callable displays the index `n` and the shared value `sha` which is created by the shared factory in line 33\. The next execution function `bulk_twoway_execute` is more interesting. Although it’s result factory returns `void`, the shared state is the atomic variable `atom`. Each agent increments its value by one (line 42). Thanks to the result factory, the last execution function (lines 56 to 69) returns the result `123.456`. It’s quite interesting to see, how many threads are involved in the execution of the callable and the execution of the result and the shared factory. The output of the program shows that result and shared factory run in the same thread but the agents in a different thread.

![A prototype implementation of executors](images/cpp20_23----executor.png)

A prototype implementation of executors

### Extended Futures

Tasks in the form of promises and futures have an ambivalent reputation in C++11\. On the one hand, they are a lot easier to use than threads or condition variables; on the other hand, they have a significant deficiency. They cannot be composed. C++20/23 overcomes this deficiency.

I have written about tasks in the form of `std::async`, `std::packaged_task`, or `std::promise` and `std::future`. The details are here: [tasks](#chap06.xhtml_chapterXXXTasks). With C++20/23 we may get extended futures.

#### Concurrency TS v1

##### `std::future`

The name extended futures is quite easy to explain. First, the interface of the C++11 `std::future` was extended; second, there are new functions for creating special futures that are composable. I start with my first point.

The extended future has three new methods:

*   The unwrapping constructor that unwraps the outer future of a wrapped future (`future<future<T>>`).
*   The [predicate](#chap23.xhtml_glossaryXXXPredicateSSSBOBOBOGlossaryBCBCBC) `is_ready` that returns if a shared state is available.
*   The method `then` that attaches a continuation to a future.

At first, the state of a future can be `valid` or `ready`.

###### valid versus ready

*   **valid**: a future is valid if it has a shared state (with a promise). This does not have to be the case because you can default-construct a `std::future` without a promise.
*   **ready**: a future is ready if the shared state is available, or to put it differently if the promise has already produced its value.

Therefore, (`valid == true`) is a requirement for (`ready == true`).

My mental model of promise and future is that they are the endpoints of a data channel.

![Tasks as data channels between communication endpoints](images/cpp20_23----tasks.png)

Tasks as data channels between communication endpoints

Now the difference between valid and ready becomes quite natural. The future is valid if there is a data channel to a promise. The future is ready if the promise has already put its value into the data channel.

Now to the method `then` for the continuation of a future.

###### Continuations with `then`

`then` empowers you to attach a future to another future. It often happens that a future is packed into another future. The job of the unwrapping constructor is it to unwrap the outer future.

```
 1 #include <future>
 2 using namespace std;
 3 int main() {
 4 
 5   future<int> f1 = async([]() { return 123; });
 6   future<string> f2 = f1.then([](future<int> f) {
 7     return to_string(f.get());      // here .get() won't block
 8   });
 9 
10   auto myResult= f2.get();
11 
12 }
```

Continuations with `std::future`

There is a subtle difference between the `to_string(f.get())` call (line 7) and the `f2.get()` call in line 10\. As I already mentioned in the code snippet: the first call is non-blocking/asynchronous and the second call is blocking/synchronous. The `f2.get()` call waits until the result of the future-chain is available. This statement also holds for chains such as `f1.then(...).then(...).then(...).then(...)` as it holds for the composition of extended futures. The final `f2.get()` call is blocking.

##### `std::async`, `std::packaged_task`, and `std::promise`

There is not much to say about the extensions of `std::async`, `std::package_task`, and `std::promise`. I only have to add that in C++20/23 all three return extended futures.

The composition of futures is more exciting. Now we can compose asynchronous tasks.

##### Creating new Futures

C++20 gets four new functions for creating special futures. These functions are `std::make_ready_future`, `std::make_execptional_future`, `std::when_all`, and `std::when_any`. First, let’s look at the functions `std::make_ready_future`, and `std::make_exceptional_future`.

###### `std::make_ready_future` and `std::make_exceptional_future`

Both functions create a future that is immediately ready. In the first case the future has a value; in the second case an exception. What seems to be strange at first, actually makes much sense. In C++11 the creation of a ready future requires a promise. This is necessary even if the shared state is immediately available.

```
future<int> compute(int x) {
  if (x < 0) return make_ready_future<int>(-1);
  if (x == 0) return make_ready_future<int>(0);
  future<int> f1 = async([]() { return do_work(x); });
  return f1;
}
```

Creating a future with make_ready_future

Hence the result must only be calculated by a promise, if `(x > 0)` holds.

A short remark: both functions are the pendant to the return function in a [monad](#chap23.xhtml_glossaryXXXMonadSSSBOBOBOGlossaryBCBCBC). Now let’s begin with future composition.

###### `std::when_any` and `std::when_all`

Both functions have a lot in common.

First, let’s look at the input.

```
template < class InputIt >
auto when_any(InputIt first, InputIt last)
    -> future<when_any_result<
	          std::vector<typename std::iterator_traits<InputIt>::value_type>>>;

template < class... Futures >
auto when_any(Futures&&... futures)
    -> future<when_any_result<std::tuple<std::decay_t<Futures>...>>>;

template < class InputIt >
auto when_all(InputIt first, InputIt last)
    -> future<std::vector<typename std::iterator_traits<InputIt>::value_type>>;

template < class... Futures >
auto when_all(Futures&&... futures)
    -> future<std::tuple<std::decay_t<Futures>...>>;
```

when_any and when_all

Both functions accept a pair of iterators for a future range or an arbitrary number of futures. The big difference is that in the case of the pair of iterators, the futures have to be of the same type; while in the case of the arbitrary number of futures, the futures can have different types and even `std::future` and `std::shared_future` can be used.

The output of the function depends on whether a pair of iterators or an arbitrary number of futures (variadic template) was used. Both functions return a future. If a pair of iterators was used, you get a future of futures in a `std::vector`: `future<vector<future<R>>>`. If you use a variadic template, you get a future of futures in a `std::tuple`: `future<tuple<future<R0>, future<R1>, ... >>`.

This covers their commonalities. The future that both functions return is ready if all input futures (`when_all`), or if any of the input futures (`when_any`) are ready.

The next two examples show the usage of `std::when_all` and `std::when_any`.

###### `std::when_all`

```
 1 #include <future>
 2 
 3 using namespace std;
 4 
 5 int main() {
 6 
 7   shared_future<int> shared_future1 = async([] { return intResult(125); });
 8   future<string> future2 = async([]() { return stringResult("hi"); });
 9 
10   future<tuple<shared_future<int>, future<string>>> all_f = 
11         when_all(shared_future1, future2);
12 
13   future<int> result = all_f.then(
14         [](future<tuple<shared_future<int>, future<string>>> f){ 
15           return doWork(f.get()); 
16         });
17 
18   auto myResult = result.get();
19 
20 }
```

Future composition with std::when_all

The future `all_f` (line 10) composes both the future `shared_future1` (line 7) and `future2` (line 8). The future `result` in line 13 is executed if all underlying futures are ready. In this case, the future `all_f` in line 15 is executed. The result is in the future `result` and can be used in line 18.

###### `std::when_any`

```
 1 #include <future>
 2 #include <vector>
 3 
 4 using namespace std;
 5 
 6 int main(){
 7 
 8   vector<future<int>> v{ .... };
 9   auto future_any = when_any(v.begin(), v.end());
10 
11   when_any_result<vector<future<int>>> result = future_any.get();
12 
13   future<int>& ready_future = result.futures[result.index];
14 
15   auto myResult = ready_future.get();
16 
17 }
```

Future composition with std::when_any

The future in `when_any` can be taken by `result` in line 11\. `result` provides the information indicating which input future is ready. If you don’t use `when_any_result`, you have to ask each future if it is ready. That is tedious.

`future_any` is the future that is ready if one of its input futures is ready. `future_any.get()` in line 11 returns the future `result`. By using `result.futures[result.index]` (line 13) you have the `ready_future` and thanks to `ready_future.get()` you can ask for the result of the job.

Either the already standardised futures nor the [concurrency TS v1 futures](http://en.cppreference.com/w/cpp/experimental/concurrency) are “not as generic, expressive or powerful as they should be” [P0701r1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0701r1.html). Additionally, the [executors](#chap10.xhtml_chapterXXXExecutors) as basic building block for executing something have to be unified with the new futures.

#### Unified Futures

What are the disadvantages of the already standardised and the futures from the concurrency TS 1?

##### Disadvantages

The already mentioned document gives an excellent description to the deficiencies of the futures.

###### `future/promise` Should Not Be Coupled to `std::thread` Execution Agents

C++11 had only one executor: `std::thread`. Consequently, futures and `std::thread` were inseparable. This changed with C++17 and the parallel algorithms of the STL. This changes even more with the new executors which you can use to configure the future. For example, the future may run in a separate thread, or in a thread pool, or just sequentially.

###### Where are `.then` Continuations are Invoked?

Imagine, you have a simple continuation such as in the following example.

```
future<int> f1 = async([]() { return 123; });
future<string> f2 = f1.then([](future<int> f) {
    return to_string(f.get());     
});
```

Continuations with `std::future`

The question is: Where should the continuation run? There are a few possibilities today:

1.  Consumer Side: The consumer execution agent always executes the continuation.
2.  Producer Side: The producer execution agent always executes the continuation.
3.  inline_executor semantics: If the shared state is ready when the continuation is set, the consumer thread executes the continuation. If the shared state is not ready when the continuation is set, the producer thread executes the continuation.
4.  thread_executor semantics: A new `std::thread` executes the continuation.

In particular, the first two possibilities have a significant drawback: they block. In the first case, the consumer blocks until the producer is ready. In the second case, the producer blocks, until the consumer is ready.

Here are a few nice use-cases of executor propagation from the document [P0701r1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0701r1.html):

```
auto i = std::async(thread_pool, f).then(g).then(h);
// f, g and h are executed on thread_pool.

auto i = std::async(thread_pool, f).then(g, gpu).then(h);
// f is executed on thread_pool, g and h are executed on gpu.

auto i = std::async(inline_executor, f).then(g).then(h);
// h(g(f())) are invoked in the calling execution agent.
```

Executor propagation

###### Passing futures to `.then` Continuations is Unwieldy

Because the future is passed to the continuation and not its value, the syntax is quite complicated. First, once more the correct but verbose version.

```
std::future<int> f1 = std::async([]() { return 123; });
std::future<std::string> f2 = f1.then([](std::future<int> f) {
    return std::to_string(f.get());     
});
```

Continuations with `std::future`

Now, I assume that I can pass the value because `to_string` is overloaded on `std::future<int>`.

```
std::future<int> f1 = std::async([]() { return 123; });
std::future<std::string> f2 = f1.then(std::to_string); 
```

Continuations with `std::future`passingthevalue

###### `when_all` and `when_any` Return Types are Unwieldy

The chapter to [`std::when_all` and `std::when_any`](#chap10.xhtml_chapterXXXwhen_anyZZZwhen_all) shows their quite complicated usage.

###### Conditional Blocking in futures Destructor Must Go

Fire and forget futures look very promising but have a big drawback. A future that is created by `std::async` waits on its destructor, until its promise is done. What seems to be concurrent runs sequentially. According to the document P0701r1, this is not acceptable and error-prone.

I describe the peculiar behaviour of [Fire and Forget Futures](#chap06.xhtml_chaperXXXFireSSSandSSSForget) in the referenced chapter.

###### Immediate Values and future Values Should Be Easy to Composable

In C++11, there is no convenient way to create a future. We have to start with a promise.

```
std::promise<std::string> p;
std::future<std::string> fut = p.get_future();
p.set_value("hello"); 
```

Creating a future in the current standard

This may change with the function [`std::make_ready_future`](#chap10.xhtml_chapterXXXmake_ready_futureZZZmake_exceptional_future) concurreny TS v1.

```
std::future<std::string> fut = make_ready_future("hello"); 
```

Creating a future in the concurrency TS v1

Using future and non-future arguments would make our job even more comfortable.

```
bool f(std::string, double, int);

std::future<std::string> a = /* ... */;
std::future<int>    c = /* ... */;

std::future<bool> d1 = when_all(a, make_ready_future(3.14), c).then(f);  
// f(a.get(), 3.14, c.get())

std::future<bool> d2 = when_all(a, 3.14, c).then(f);  
// f(a.get(), 3.14, c.get())
```

Using future and non-future arguments

Neither the syntactic form `d1` nor the syntactic form `d2` is possible with the concurrency ts v1.

##### Five New Concepts

Their are five new concepts for futures and promises in the Proposal [1054R0](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1054r0.html).

*   **FutureContinuation**, invocable objects that are called with the value or exception of a future as an argument.
*   **SemiFuture**, which can be bound to an executor, an operation which produces a `ContinuableFuture` (`f = sf.via(exec)`).
*   **ContinuableFuture**, which refines SemiFuture and instances can have one `FutureContinuation` attached to them (`f.then(c)`), which is executed on the future’s associated executor when the future becomes ready.
*   **SharedFuture**, which refines `ContinuableFuture` and instances can have multiple `FutureContinuation`s attached to them.
*   **Promise**, each of which is associated with a future and make the future ready with either a value or an exception.

The paper also provides the declaration of this new concepts.

```
template <typename T>
struct FutureContinuation
{
  // At least one of these two overloads exists:
  auto operator()(T value);
  auto operator()(exception_arg_t, exception_ptr exception);
};

template <typename T>
struct SemiFuture
{
  template <typename Executor>
  ContinuableFuture<Executor, T> via(Executor&& exec) &&;
};

template <typename Executor, typename T>
struct ContinuableFuture
{
  template <typename RExecutor>
  ContinuableFuture<RExecutor, T> via(RExecutor&& exec) &&;

  template <typename Continuation>
  ContinuableFuture<Executor, auto> then(Continuation&& c) &&;
};

template <typename Executor, typename T>
struct SharedFuture
{
  template <typename RExecutor>
  ContinuableFuture<RExecutor, auto> via(RExecutor&& exec);

  template <typename Continuation>
  SharedFuture<Executor, auto> then(Continuation&& c);
};

template <typename T>
struct Promise
{
  void set_value(T value) &&;

  template <typename Error>
  void set_exception(Error exception) &&;
  bool valid() const;
};
```

The five new concepts for futures and promises

Based on the declaration of the concepts, here are a few observations:

*   A `FutureContinuation` can be invoked with a value or with an exception. It a [callable unit](#chap23.xhtml_glossaryXXXCallableSSSUnitZZZcallableSSSBOBOBOGlossaryBCBCBC) that consumes the value or exception of a future
*   All futures (`SemiFuture`, `ContinuableFuture`, and `SharedFuture`) have a method `via` that excepts an executor and returns a `ContinuableFuture`. `via` allows it to convert from one future type to a different one by using a different executor.
*   Only a `ContinuableFuture` or a `SharedFuture` have a `then` method for continuation. The `then` method takes a `FutureContinuation` and returns a `ContinuableFuture`.
*   A `SharedFuture` is a non-uniquely owned future that is copyable.
*   A Promise can set a value or an exception.

##### Future Work

The Proposal [1054R0](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1054r0.html) left a few questions open.

*   Forward progress guarantees for futures and promises.
*   Requirements on synchronization for use of futures and promises from non-concurrent execution agents.
*   `std::future/std::promise` interoperability.
*   Future unwrapping, both `future<future<T>>` and more advanced forms.
*   `when_all/when_any/when_n`.
*   `async`.

### Transactional Memory

Transactional memory is based on the idea of a transaction from database theory. Transactional memory makes working with threads a lot easier for two reasons: first [data races](#chap20.xhtml_chapterXXXDataSSSRaces) and [deadlocks](#chap20.xhtml_chapterXXXDeadlocks) disappear and second transactions are composable.

A transaction is an action that has the following properties **A**tomicity, **C**onsistency, **I**solation, and **D**urability (ACID). Except for the durability or storing the result of an action, all properties hold for transactional memory in C++. Now three short questions are left.

#### ACI(D)

What do atomicity, consistency, and isolation mean for an atomic block consisting of some statements?

```
atomic{
    statement1;
    statement2;
    statement3;
} 
```

An atomic block

Atomicity

Either all or none of the statements in the block are performed.

Consistency

The system is always in a consistent state. All transactions establish a [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC).

Isolation

Each transaction runs in total isolation from other transactions.

How do these properties apply? A transaction remembers its initial state and is performed without synchronisation. If a conflict happens during its execution, the transaction is interrupted and restored to its initial state. This rollback causes the transaction to be executed again. If the initial state of the transaction still exists at the end of the transaction, the transaction is committed. Conflicts are typically detected with a [tagged state reference](#chap10.xhtml_textXXXtaggedSSSstateSSSreference).

A transaction is a kind of speculative action that is only committed if the initial state holds. In contrast to a mutex it is an optimistic approach. A transaction is performed without synchronisation. It is only be published if no conflict occurs. A mutex is a pessimistic approach. First, the mutex ensures that no other thread can enter the critical region. Next, the thread enters the critical region if it is the exclusive owner of the mutex and hence all other threads are blocked.

C++ supports transactional memory in two flavours: synchronised blocks and atomic blocks.

#### Synchronized and Atomic Blocks

So far I only wrote about transactions. Now I write about synchronised blocks and atomic blocks. Both can be encapsulated in each other. To be more specific synchronised blocks are not transactions because they can execute transaction-unsafe. An example for transaction-unsafe code would be code like the output to the console which can not be undone. For this reason, synchronized blocks are often called relaxed blocks.

##### Synchronized Blocks

Synchronized blocks behave like a global lock protects them. This means that all synchronised blocks follow a [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC) and in particular: all changes to a synchronised block are available in the next synchronized block. There is a *synchronizes-with* relation between the synchronised blocks because the commit of the transaction *synchronizes-with* the next start of a transaction. Synchronised blocks can not cause a deadlock because they create a [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC). While a classical mutex protects a critical region of the program, a global lock of a synchronised block protects the total program.

This is the reason the following program is *well-defined*:

```
 1 // synchronized.cpp
 2 
 3 #include <iostream>
 4 #include <vector>
 5 #include <thread>
 6 
 7 int i= 0;
 8 
 9 void increment(){
10   synchronized{ 
11     std::cout << ++i << " ,";
12   }
13 }
14 
15 int main(){
16   
17   std::cout << std::endl;
18     
19   std::vector<std::thread> vecSyn(10);
20   for(auto& thr: vecSyn)
21     thr = std::thread([]{ for(int n = 0; n < 10; ++n) increment(); });
22   for(auto& thr: vecSyn) thr.join();
23   
24   std::cout << "\n\n";
25   
26 } 
```

A synchronized block

Although the variable `i` in line 7 is a global variable and the operations in the synchronised block are transaction-unsafe, the program is well-defined. Ten threads concurrently invoke the function `increment` (line 21) ten times incrementing the variable `i` in line 11\. The access to `i` and `std::cout` happens in [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC). This is the characteristic of the synchronised block.

The program returns the expected result. The values for `i` are written in an increasing sequence, separated by a comma. For completeness, here is the output.

![Incrementing with synchronised blocks](images/cpp20_23----synchronized.png)

Incrementing with synchronised blocks

What about data races? You can have them with synchronised blocks. A small modification of the source code is sufficient to introduce a [data race](#chap20.xhtml_chapterXXXDataSSSRaces).

```
 1 // nonsynchronized.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <vector>
 6 #include <thread>
 7 
 8 using namespace std::chrono_literals;
 9 using namespace std;
10 
11 int i= 0;
12 
13 void increment(){
14   synchronized{ 
15     cout << ++i << " ,";
16     this_thread::sleep_for(1ns);
17   }
18 }
19 
20 int main(){
21   
22   cout << endl;
23     
24   vector<thread> vecSyn(10);
25   vector<thread> vecUnsyn(10);
26     
27   for(auto& thr: vecSyn)
28     thr = thread([]{ for(int n = 0; n < 10; ++n) increment(); });
29   for(auto& thr: vecUnsyn)
30     thr = thread([]{ for(int n = 0; n < 10; ++n) cout << ++i << " ,"; });
31     
32   for(auto& thr: vecSyn) thr.join();
33   for(auto& thr: vecUnsyn) thr.join();
34   
35   cout << "\n\n";
36   
37 }
```

A data race with a synchronized block

To observe the data race, I let the synchronised block sleep for a nanosecond (line 16). At the same time, I access the output stream `std::cout` without a synchronised block (line 30). In total 20 threads increment the global variable `i`, half of them without synchronisation. The output shows the issue.

![A data race with synchronised blocks](images/cpp20_23----nonsynchronizedEdit.png)

A data race with synchronised blocks

I put red circles around the issues in the output. These are the locations where `std::cout` is written by at least two threads at the same time. The C++11 standard guarantees that the characters are written atomically; that is not an issue. What is worse is that the variable `i` is written by at least two threads. This is a data race; hence, the program has undefined behaviour. If you look carefully at the output, you see a data race in action. The final result for the counter is 199 but should be 200\. This means, one of the intermediate values of the counter was overwritten.

The [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC) of synchronised blocks also holds for atomic blocks.

##### Atomic Blocks

You can execute transaction-unsafe code in a synchronised block but not in an atomic block. Atomic blocks are available in three forms: `atomic_noexcept`, `atomic_commit`, and `atomic_cancel`. The three suffixes `_noexcept`, `_commit`, and `_cancel` define how an atomic block manages an exception:

`atomic_noexcept`

If an exception is thrown, `std::abort` is called and the program aborts.

`atomic_cancel`

In the default case, `std::abort` is called. This does not hold if a transaction-safe exception is thrown that is responsible for ending the transaction. In this case, the transaction is cancelled, put to its initial state and the exception is thrown.

`atomic_commit`

If an exception is thrown, the transaction is committed.

Transaction-safe exceptions are: [`std::bad_alloc`](http://en.cppreference.com/w/cpp/memory/new/bad_alloc),[`std::bad_array_length`](https://www.cs.helsinki.fi/group/boi2016/doc/cppreference/reference/en.cppreference.com/w/cpp/memory/new/bad_array_length.html), [`std::bad_array_new_length`](http://en.cppreference.com/w/cpp/memory/new/bad_array_new_length), [`std::bad_cast`](http://en.cppreference.com/w/cpp/types/bad_cast), [`std::bad_typeid`](http://en.cppreference.com/w/cpp/types/bad_typeid), [`std::bad_exception`](http://en.cppreference.com/w/cpp/error/bad_exception), [`std::exception`](http://en.cppreference.com/w/cpp/error/exception), and all exceptions that are derived from one of these.

#### `transaction_safe` versus `transaction_unsafe` Code

You can declare a function as `transaction_safe` or attach the `transaction_unsafe` attribute to it.

```
int transactionSafeFunction() transaction_safe;

[[transaction_unsafe]] int transactionUnsafeFunction();
```

transaction_safe versus transaction_unsafe

`transaction_safe` belongs to the type of the function. What does `transaction_safe` mean? A `transaction_safe` function is, according to the proposal [N4265](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4265.html), a function that has a `transaction_safe` definition. This holds true if the following properties **do not** apply to its definition:

*   It has a `volatile` parameter or a `volatile` variable.
*   It has `transaction-unsafe` statements.
*   If the function uses a constructor or destructor of a class in its body that has a `volatile` non-static member.

Of course, this definition of `transaction_safe` is not sufficient because it uses the term `transaction_unsafe`. You can read the proposal [N4265](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4265.html) for the details.

### Task Blocks

Task blocks use the well-known fork-join paradigm for the parallel execution of tasks. They are already part for the [Technical Specification for C++ Extension Parallelism Version 2](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/n4742.html); therefore, it’s quite probable that we get them with C++20.

Who invented it in C++? Both Microsoft with its [Parallel Patterns Library (PPL)](https://en.wikipedia.org/wiki/Parallel_Patterns_Library) and Intel with its [Threading Building Blocks (TBB)](https://en.wikipedia.org/wiki/Threading_Building_Blocks) were involved in the proposal [N4441](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/n4411.pdf). Additionally, Intel used its experience with their [Cilk Plus library](https://en.wikipedia.org/wiki/Cilk).

The name fork-join is quite easy to explain.

#### Fork and Join

The most straightforward approach to explain the fork-join paradigm is a graphic.

![The fork-join paradigm](images/cpp20_23----ForkJoin.png)

The fork-join paradigm

How does it work?

The creator invokes `define_task_block` or `define_task_block_restore_thread`. This call creates a task block that can create tasks or it can wait for their completion. The synchronisation is at the end of the task block. The creation of a new task is the fork phase; the synchronisation of the task block is the join phase of the workflow. Admittedly that was simple description. Let’s have a look at a piece of code.

```
 1 template <typename Func> 
 2 int traverse(node& n, Func && f){ 
 3     int left = 0, right = 0; 
 4     define_task_block(                 
 5         [&](task_block& tb){ 
 6             if (n.left) tb.run([&]{ left = traverse(*n.left, f); }); 
 7             if (n.right) tb.run([&]{ right = traverse(*n.right, f); });
 8          }
 9     );                                                         
10     return f(n) + left + right; 
11 } 
```

Define a task block

`traverse` is a function template that invokes function `f` on each node of its tree. The keyword `define_task_block` defines the task block. The task block `tb` can start a new task in this block. Exactly that happens at the left and right branches of the tree in lines 6 and 7\. Line 9 is the end of the task block and hence the synchronisation point.

You can define a task block by using either the function `define_task_block` or the function `define_task_block_restore_thread`.

#### `define_task_block` versus `define_task_block_restore_thread`

The subtle difference is that the function `define_task_block_restore_thread` guarantees in contrast to the function `define_task_block` that the creator thread of the task block is the same thread that runs after the task block.

```
 1 ...
 2 define_task_block([&](auto& tb){  
 3   tb.run([&]{[] func(); });
 4   define_task_block_restore_thread([&](auto& tb){
 5     tb.run([&]([]{ func2(); });
 6     define_task_block([&](auto& tb){
 7        tb.run([&]{ func3(); }
 8     });
 9     ...
10     ...
11   });
12   ...
13   ...
14 });
15 ...
16 ... 
```

`define_task_block` versus `define_task_block_restore_thread`

Task blocks ensure that the creator thread of the outermost task block (lines 2 - 14) is exactly the same thread that runs the statements after finishing the task block. This means that the thread that executes line 2 is the same thread that executes lines 15 and 16\. This guarantee does not hold for nested task blocks; therefore, the creator thread of the task block in lines 6 - 8 does not automatically execute lines 9 and 10\. If you need that guarantee, you should use the function `define_task_block_restore_thread` (line 4). Now it holds that the creator thread executing line 4 is the same thread executing lines 12 and 13.

#### The Interface

A task block has a very limited interface. You can not construct, destroy, copy, or move an object of the class `task_block`; you have to use either function `define_task_block` or `define_task_block_restore_thread`. The task_block `tb` is in the scope of the defined task block active and can, therefore, start new tasks (`tb.run`) or wait (`tb.wait`) until the task is done.

```
1 define_task_block([&](auto& tb){  
2   tb.run([&]{ process(x1, x2) });
3   if (x2 == x3) tb.wait();
4   process(x3, x4);
5 }); 
```

The minimal interface of a task block

What is the code snippet doing? In line 2 a new task is started. This task needs the data `x1` and `x2`. Line 4 uses the data `x3` and `x4`. If `x2 == x3` is true, the variables have to be protected from shared access. This is the reason why the task block `tb` waits until the task in line 2 is done.

If the functions `task_block::run` or `task_block::wait` detect that an exception is pending within the current task block they throw an exception of kind `task_cancelled_exception`.

#### The Scheduler

The scheduler manages which thread is running. This means that it is no longer the responsibility of the programmer to decide who executes the task. Threads are just an implementation detail.

There are two strategies for executing the newly created task. The parent represents the creator thread and the child the new task.

Child stealing

The scheduler steals the task and executes it.

Parent stealing

The task block `tb` itself executes the task. Now the scheduler steals the parent.

Proposal [N4441](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/n4411.pdf) supports both strategies.

### Data-Parallel Vector Library

The data-parallel vector library provides data-parallel (SIMD) programming via vector types. [SIMD](https://en.wikipedia.org/wiki/SIMD) stands for **S**ingle **I**nstruction **M**ultiple **D**ata and means that one operation is performed on many data in parallel. Each modern processor architecture provides SIMD extensions, but there exists no standardised C++ interface to use them. The following table gives an overview of various SIMD extensions.

SIMD Extensions

| **Architecture** | **SIMD Extension** | **Register Width** |
| --- | --- | --- |
| ARM 32 / 64 | NEON | 128 bit |
| Power / PowerPC | AltiVec | 128 bit |
|   | VSX | 128 bit |
| x86 / AMD 64 | MMX / 3DNow | 64 bit |
|   | SSE | 128 bit |
|   | AVX / AVX2 / AVX-512 | 128 bit / 256 bit / 512 bit |

For example, the [SSE](https://en.wikipedia.org/wiki/Streaming_SIMD_Extensions) extension allows it to add four 32 bit `int`s in parallel. The effect is that it is four times faster than adding four `int`s sequential because single and vector operations are equally fast on modern CPU’s.

The SIMD extension in C++ consists now of two data-parallel vectors and special operations on them.

#### Data-Parallel Vectors

The data-parallel vectors are `std::simd` and `std::simd_mask`:

```
template< class T, class Abi = simd_abi::compatible<T> >
class simd;

template< class T, class Abi = simd_abi::compatible<T> >
class simd_mask;
```

*   `T` is the element type of the vectors.
*   `Abi` stands for the number of elements and storage.

The element type of `simd_mask` is `bool` and `simd_mask<T, Abi>::size()` is always `simd<T, Abi>::size()`.

#### The Interface of the Data-Parallel Vectors

The data-parallel vector library supports tags for the ABI and alignment, various operations, and traits.

##### Tags

The tags let you specify and ask for the ABI and the alignment.

###### ABI Tags

The ABI tag indicates a choice of size and binary representation for objects of the vector type.

ABI tags

| **ABI tags** | **Description** |
| --- | --- |
| `scalar` | Tag type for storing a single element. |
| `fixed_size` | Tag type for storing a specified number of elements. |
| `compatible` | Tag type that ensures ABI compatibility. |
| `native` | Tag type that is most efficient. |
| `max_fixed_size` | The maximum number of elements guaranteed to be supported by fixed. |

###### Alignment Tags

The alignment tags indicates the alignment of the elements and of the vector type.

Alignment tags

| **Alignment tags** | **Description** |
| --- | --- |
| `element_aligned_tag` and `element_aligned` | Tag type that indicates the alignment of the elements. |
| `vector_aligned_tag` and `vector_aligned` | Tag type that indicates the alignment of the vector type. |
| `overaligned_tag` and `overaligned` | Tag type that indicates the specified alignment. |

##### Where Expression

The where expression abstracts the operation of selected elements of a given object of arithmetic or data-parallel type.

Where expression

| **Where expression** | **Description** |
| --- | --- |
| `const_where_expression` | Selects elements with non-mutating operations. |
| `where_expression` | Selects elements with mutating operations. |
| `where` | Generated `const_where_expression` and `where expression`. |

##### Casts

Cast operations cast element-wise or split or concat between SIMD objects and single ones.

Casts

| **Where expression** | **Description** |
| --- | --- |
| `simd_cast` and `static_simd_cast` | Performs a element-wise static cast. |
| `to_fixed_size`, `to_compatible`, and `to_native` | Performs an element-wise ABI cast. |
| `split` | Splits a single SIMD object to multiple objects. |
| `concat` | Concatenates multiple SIMD objects into a single SIMD object. |

##### Algorithms

The SIMD algorithms are applied to two SIMD objects and return a SIMD object.

Algorithms

| **Algorithms** | **Description** |
| --- | --- |
| `min` | Applies the `min` operation element-wise and returns a SIMD object. |
| `max` | Applies the `min` operation element-wise and returns a SIMD object. |
| `minmax` | Applies the `minmax` operation element-wise and returns a SIMD object. |
| `clamp` | Applies the `clamp` operation element-wise and returns a SIMD object. |

The clamp algorithm applies element-wise the following operation for i in [0, `size()`]:

This means, the resulting SIMD object `sim` will have the following values:

*   `v[i] < lo[i]: sim[i] = lo[i]`
*   `lo[i] < v[i] < hi[i]: sim[i] = vi[i]`
*   `hi[i] < v[i]: sim[i] = hi[i]`

##### Reduction

Reduction reduces the SIMD vector to a single element.

Reduction

| **Reduction** | **Description** |
| --- | --- |
| `reduce` | Reduces the SIMD vector to a single element. |
| --- | --- |
| `hmin` | Returns the minimum element. |
| `hmax` | Return the maximum element. |

##### Mask Reduction

Applies the predicate only to that elements of the SIMD vector `v[i]` for which the `mask m[i] == true` holds.

Mask Reduction

| **Mask Reduction** | **Description** |
| --- | --- |
| `all_of, any_of, none_of`, and `some_of` | Applies the predicates on each element `v[i]` for which the mask `m[i] == true` holds. |
| `popcount` | Return the number of true values. |
| `find_first_set` and `find_last_set` | Return the position of the first or last true value. |

##### Traits

Traits give you SIMD characteristics at compile time.

Traits

| **Traits** | **Description** |
| --- | --- |
| `is_abi_tag` and `is_abi_tag_v` | Checks if a type is an ABI tag type. |
| `is_simd` and `is_simd_v` | Checks if a type is SIMD type. |
| `is_simd_mask` and `is_simd_mask_v` | Checks if a type is a simd_mask type. |
| `is_simd_flag_type` and `is_simd_flag_type_v` | Checks if a type is a SIMD flag type. |
| `simd_size` and `simd_size_v` | Returns the number of elements of a given element type and ABI. |
| `memory_alignment` and `memory_alignment_v` | Returns an appropriate alignment for `vector_aligned`. |
| `abi_for_size` and `abi_for_size_t` | Returns an ABI type for a given element type and number of elements. |

# Patterns

## Patterns and Best Practices

The goal of this chapter is to give you an idea what patterns are and what are they good for. My pragmatic view is informal and is wearing C++ glasses. For a more formal and comprehensive discussion of this topic, I provide links to further literature.

First of all: What is a pattern?

Pattern

“Each pattern is a three-part rule, which express a relation between a certain context, a problem, and a solution.” [Christopher Alexander](https://en.wikipedia.org/wiki/Christopher_Alexander)

To say it more informally. A pattern is a well-established and documented solution to a design challenge in a specific domain.

### History

The father of patterns is the already mentioned Cristopher Alexander, who’s patterns about the nature of human-centred design for towns, buildings, and construction, in general, were seminal for software design. 1994, the so-called **G**ang **o**f **F**our (Eric Gamma, Richard Helm, Ralph Johnson, and John Vlissides) published their book [Design Patterns: Elements of Reusable Object-Oriented Software](https://en.wikipedia.org/wiki/Design_Patterns). The book includes 23 software design patterns aimed for object-oriented software design. The patterns fall into three categories creational, structural, and behavioural. The book defined the vocabulary for the entire software industry. Here are a few of the most known design patterns:

*   Creational
    *   Factory method pattern
    *   Singleton pattern
*   Structural
    *   Adapter
    *   Bridge
    *   Composite
    *   Decorator
    *   Facade
    *   Proxy
*   Behavioural
    *   Command
    *   Iterator
    *   Observer
    *   Strategy
    *   Template method
    *   Visitor

One year later, Frank Buschmann, Regine Meunier, Hans Rohnert, Peter Sommerlad, and Michael Stal published their highly influential book [Pattern-Oriented Software-Architecture: A System of Patterns](https://www.wiley.com/WileyCDA/Section/id-406899.html), or in short POSA. This book was the starting point to a series of five books. It was published 1995 and has three categories of patterns: architectural patterns, design patterns, and idioms. Many of the patterns are now common terminology:

*   Architectural Patterns
    *   Layers
    *   Pipes-and_Filters
    *   Broker
    *   Model-View-Controller
*   Design Patterns
    *   Master-Slave
    *   Publish-Subscriber
*   Idioms
    *   Counted-Pointer

What the difference between these three categories? The focus of the architectural patterns is the entire software system. They are more abstract than the design patterns which defines the interplay between the subsystems. Idioms are implementations of an architectural or design pattern in a given programming language. They have the lowest abstraction level of all three.

Each of the books two to five of the POSA series has a different focus. They deal with “Patterns for Concurrent and Networked Objects” (volume 2), with “Patterns for Resource Management” (volume 3), with “A Pattern Language for Distributed Computing” (volume 4), and “On Patterns and Pattern Languages” (volume 5). The book sections [Synchronisation Patterns](#chap13.xhtml_chapterXXXSynchronisationSSSPatterns) and [Concurrent Architecture](#chap14.xhtml_chapterXXXConcurrentSSSArchitectur) are strongly influenced by the second volume of the series.

### Invaluable Value

Patterns added an invaluable value to software development in general. Of course, this also holds true for concurrency in particular. The added value boils down to three points. A well-defined terminology, improved documentation, and learning from the best.

The **well-defined terminology** means that software developers can now use common and unambiguous vocabulary. Misunderstandings or verbose explanations are mainly stories of the past. If a software developer asks for an advice about how a family of similar algorithms can be implemented in such a way that they can be exchanged during runtime the answer may be as short as: use the strategy pattern. If the software developer knows the strategy pattern, he can immediately think about the consequences of using the strategy pattern; if not, he can look it up in the literature.

The **documentation improves** in two aspects. First, the documentation about the software system, may it be in a graphical or textual description, improves because if I read in the documentation that the observer pattern was used, I know that the system has a kind of Subject/Observer structure. This means that the observer will register or unregister themselves on the subject and the subject will send notifications to all of its observers if necessary. Now, secondly, I can directly jump into the source code and search for keywords such as observer, subject or notify because I have an idea about the concrete implementation.

Patterns is just about learning from the best. You learn from the documented experience from the best and do not repeat their mistakes. They provide proven solutions for typical problems and help to master complexity. Each pattern provides information, when it should be used, what are the consequences of using it, how to implement it, and its known usages.

### Pattern versus Best Practices

You may wonder that I write in this part of the book also about best practices. Why? Honestly, I had often an intensive fight if a practice such as immutable values or pure functions are patterns or just best practices. Patterns are documented best practices and, therefore, quite related. I learned from this fight a few lessons.

*   Both terms can not be exact distinguished.
*   If the practice I describe is a well-defined pattern, I put it in the pattern bucket.
*   If the practice has a kind of tip character and no formal defined structure, I put it in the best practices bucket.
*   Today’s best practices may become tomorrows well-defined patterns.

### Anti-Pattern

Pattern stands for best practices, anti-pattern stands for lesson learned, or to use the words from [Andrew Koenig](https://en.wikipedia.org/wiki/Andrew_Koenig_(programmer)): “Those that describe a bad solution to a problem which resulted in a bad situation.” If you carefully read the literature to concurrency patterns, you often find the [double-checked locking pattern](#chap09.xhtml_chapterXXXDoubleMMMCheckedSSSLockingSSSPattern). The general idea of the double-checked locking pattern is in one sentence the thread-safe initialisation of shared state in an optimised way. This shared state is typically a [singleton](https://en.wikipedia.org/wiki/Singleton_pattern). I intentionally put the double-checked locking pattern in the [case studies](#chap09.xhtml_chapterXXXCaseSSSStudies) chapter of this book to emphasise it explicitly: naively usage of the double-checked locking pattern may end in undefined behaviour. The issues of the double-checked locking pattern boil essentially down to the issues of the singleton pattern.

If you want to use the singleton pattern, you have to think about the following challenges:

*   First and foremost, the singleton is a global object. Due to this fact, the usage of the singleton is most of the times not visible in the interface. The effect is that you have a hidden dependency in the code which uses the singleton.
*   A singleton is a static object and is, therefore, once created never destroyed. Its lifetime ends with the lifetime of the program.
*   If your static member of class such as a singleton depends on another static member which is defined in another translation unit, you have no guarantee which one is initialised first. The probability that it fails is 50 %.
*   A singleton is often used when just an instance of a class would also do the job. Many developers use the singleton to proof that they know their design pattern.

## Synchronisation Patterns

The main concern when you deal with concurrency is shared, mutable state or as [Tony Van Eerd](https://github.com/tvaneerd) put it in his CppCon 2014 talk “Lock-free by Example”: “Forget what you learned in Kindergarten (ie stop Sharing)”.

![Mutable, shared state](images/SynchronisationPatterns----MutableShared.png)

Mutable, shared state

A necessary condition for a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) is a mutable, shared state. If you handle sharing or mutation, no data race can happen. This is exactly the focus of the next two sections: [Dealing with Sharing](#chap13.xhtml_chapterXXXDealSSSwithSSSSharing) and [Dealing with Mutation](#chap13.xhtml_chapterXXXDealingSSSwithSSSMutation).

### Dealing with Sharing

If you don’t share, no [data races](#chap20.xhtml_chapterXXXDataSSSRaces) can happen. Not sharing means that your thread works on local variables. This can be achieved by [copying the value](#chap13.xhtml_chapterXXXCopiedSSSValueSSSBOBOBOPatternBCBCBC), by using [thread-specific storage](#chap13.xhtml_chapterXXXThread-SpecificSSSStorageSSSBOBOBOPatternBCBCBC), or by transferring the result to the [future](#chap13.xhtml_chapterXXXFutureSSSBOBOBOPatternBCBCBC) via a protected data channel. The patterns in this section are quite obvious, but for completeness, I will present them with a short explanation.

#### Copied Value

If a thread gets its arguments by copy and not by reference, there is no need to synchronise accesses to any data. No [data races](#chap20.xhtml_chapterXXXDataSSSRaces) and no lifetime issues are possible.

##### Data Races with References

The following program starts three threads. One thread gets its argument by copy, the other by reference and the last by constant reference.

```
 1 // copiedValueDataRace.cpp
 2 
 3 #include <functional>
 4 #include <iostream>
 5 #include <string>
 6 #include <thread>
 7 
 8 using namespace std::chrono_literals;
 9 
10 void byCopy(bool b){
11     std::this_thread::sleep_for(1ms);
12     std::cout << "byCopy: " << b << std::endl;
13 }
14 
15 void byReference(bool& b){
16     std::this_thread::sleep_for(1ms);
17     std::cout << "byReference: " << b << std::endl;
18 }
19 
20 void byConstReference(const bool& b){
21     std::this_thread::sleep_for(1ms);
22     std::cout << "byConstReference: " << b << std::endl;
23 }
24 
25 int main(){
26 
27     std::cout << std::boolalpha << std::endl;
28 
29     bool shared{false};
30     
31     std::thread t1(byCopy, shared);
32     std::thread t2(byReference, std::ref(shared));
33     std::thread t3(byConstReference, std::cref(shared));
34     
35     shared = true;
36     
37     t1.join();
38     t2.join();
39     t3.join();
40 
41     std::cout << std::endl;
42 
43 }
```

Data races with references

Each thread sleeps for one millisecond (lines 11, 16, and 21) before it displays the boolean value. Only thread `t1` has a local copy of the boolean and has, therefore, no data race. The output of the program shows that the boolean values of thread `t2` and `t3` are modified without synchronisation.

![Data races with references](images/SynchronisationPatterns----copiedValueDataRace.png)

Data races with references

I made in my example `copiedValueDataRace.cpp` an assumption which is trivial for a boolean but not for a more complex type. Passing the argument by copy is data race free if the argument is a so-called value object.

###### When a reference is a copy

You may think that the thread `t3` in the previous example `copiedValueDataRace.cpp` can just be replaced with `std::thread t3(byConstReference, shared)`. The program compiles and runs but what seems like a reference is a copy. The reason is that [`std::decay`](https://en.cppreference.com/w/cpp/types/decay) is applied to each argument of the thread. `std::decay` performs lvalue-to-rvalue, array-to-pointer, and function-to-pointer implicit conversions to its type T. In particular, it invokes in this use-case [`std::remove_reference`] on the type T.

The program `perConstReference.cpp` uses a non-copyable type `NonCopyableClass`.

```
 1 // perConstReference.cpp
 2 
 3 #include <thread>
 4 
 5 class NonCopyableClass{
 6     public:
 7 
 8     // the compiler generated default constructor
 9     NonCopyableClass() = default;
10 
11     // disallow copying
12     NonCopyableClass& operator = (const NonCopyableClass&) = delete;
13     NonCopyableClass (const NonCopyableClass&) = delete;
14   
15 };
16 
17 void perConstReference(const NonCopyableClass& nonCopy){}
18 
19 int main(){
20 
21     NonCopyableClass nonCopy;
22 
23     perConstReference(nonCopy);
24     
25     std::thread t(perConstReference, nonCopy);
26     t.join();
27 
28 }
```

Implicit copying of a per-reference thread argument

The object `nonCopy` (line 21) is not copyable. This is fine if I invoke the function `perConstReference` with the argument `nonCopy` because the function accepts its argument per constant reference. Using the same function in the thread `t` (line 25) causes GCC 6 to generate a verbose compiler error with more than 300 lines:

![A verbose error message](images/SynchronisationPatterns----numberOfLinesPerConstReference.png)

A verbose error message

The important part of the error message is in the middle of the screenshot in red: “error: use of deleted function”. The copy-constructor of the class `NonCopyableClass` is not available.

![Use of deleted function](images/SynchronisationPatterns----perConstReference.png)

Use of deleted function

##### Lifetime Issues with References

If your thread uses its argument by reference and you detach it, you have to be extremely careful. The small program `copiedValueLifetimeIssues.cpp` has undefined behaviour.

```
 1 // copiedValueLifetimeIssues.cpp
 2 
 3 #include <iostream>
 4 #include <string>
 5 #include <thread>
 6 
 7 void executeTwoThreads(){
 8     
 9     const std::string localString("local string");
10     
11     std::thread t1([localString]{
12         std::cout << "Per Copy: " << localString << std::endl;
13     });
14     
15      std::thread t2([&localString]{
16         std::cout << "Per Reference: " << localString << std::endl;
17     });
18     
19     t1.detach();
20     t2.detach();
21 }
22     
23 using namespace std::chrono_literals;
24 
25 int main(){
26     
27     std::cout << std::endl;
28     
29     executeTwoThreads();
30     
31     std::this_thread::sleep_for(1s);
32     
33     std::cout << std::endl;
34     
35 }
```

Lifetime issues with references

`executeTwoThreads` (lines 7 - 21) starts two threads. Both threads are detached (lines 19 and 20) and print the local variable `localString` (line 9). The first thread captures the local variable by copy and the second the local variable by reference. For simplicity reasons, in both cases I used a lambda function to bind the arguments.

Because the `executeTwoThreads` function doesn’t wait until the two threads are done, the thread `t2` refers to the local string which is bound to the lifetime of the invoking function. This is undefined behaviour. Curiously, with GCC 6 the maximum optimised executable `-O3` seems to work and the non-optimised executable crashes.

![Lifetime issues with references](images/SynchronisationPatterns----copiedValueLifetimeIssues.png)

Lifetime issues with references

##### Further Information

*   [Pattern-Oriented Software Architecture: A Pattern Language for Distributed Computing](http://www.dre.vanderbilt.edu/~schmidt/POSA/POSA4/)

#### Thread-Specific Storage

Thread-specific or thread-local storage allows multiple threads to use local storage via a global access point. By using the storage specifier `thread_local`, a variable becomes a thread-local variable. This means you can use the thread-local variable without synchronisation.

Here is a typical use-case. Assume, you want to calculate the sum of all elements of a vector `randValues`. Doing it with a range-based for-loop is straightforward.

```
// calculateWithLoop.cpp

... 

unsigned long long sum = {};
for (auto n: randValues) sum += n;
```

But your PC has four cores. Therefore, you make a concurrent program out of the sequential program.

```
// threadLocalSummation.cpp

...

thread_local unsigned long long tmpSum = 0;

void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
           unsigned long long beg, unsigned long long end){
    for (auto i = beg; i < end; ++i){
        tmpSum += val[i];
    }
    sum.fetch_add(tmpSum, std::memory_order_relaxed);
}

... 

std::atomic<unsigned long long> sum{}; 

std::thread t1(sumUp, std::ref(sum), std::ref(randValues), 0, fir);
std::thread t2(sumUp, std::ref(sum), std::ref(randValues), fir, sec);
std::thread t3(sumUp, std::ref(sum), std::ref(randValues), sec, thi);
std::thread t4(sumUp, std::ref(sum), std::ref(randValues), thi, fou);
```

You put the range-based for-loop into a function, let each thread calculate a fourth of the sum in the thread-local variable `tmpSum`. The line `sum.fetch_add(tmpSum, std::memory_order_relaxed)` finally sums up all values in the atomic `sum`.

I already discussed the various ways, to sum up all elements of a vector in the chapter [Calculating the Sum of a Vector](#chap09.xhtml_chapterXXXCalculatingSSStheSSSSumSSSofSSSaSSSVector). You can study the entire programs their.

##### Further Information

*   [ValueObject](https://martinfowler.com/bliki/ValueObject.html)
*   [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

#### Future

C++11 provides futures and promise in three [flavours](#chap06.xhtml_chapterXXXTasks): `std::async`, `std::packaged_task`, and the pair `std::promise` and `std::future`. The term promise goes back to the seventies. The future is a read-only placeholder for the value which a writeable promise sets. From the synchronisation perspective, the critical property of a promise/future pair is that both are connected by a protected data channel.

There are a few decisions to make when implementing a future.

*   A future can ask for its value implicitly or explicitly with the get call such as in C++.
*   A future can [eagerly](#chap23.xhtml_glossaryyXXXEagerSSSevaluationSSSBOBOBOGlossaryBCBCBC) or [lazily](#chap23.xhtml_glossaryyXXXLazySSSevaluationSSSBOBOBOGlossaryBCBCBC) start the computation in an eager or lazy fashion. Only the promise `std::async` supports lazy evaluation via launch policies.

```
auto lazyOrEager = std::async([]{ return "LazyOrEager"; });
auto lazy = std::async(std::launch::deferred, []{ return "Lazy"; });
auto eager = std::async(std::launch::async, []{ return "Eager"; });

lazyOrEager.get();
lazy.get();
eager.get();
```

If I don’t specify a launch policy, it’s up to the system to start the job eager or lazy. By using the launch policy `std::launch::async`, a new thread is created and the promise starts immediately its job. This is in contrast to the launch policy `std::launch::async`. The call `eager.get()` starts the promise. Additionally, the promise is executed in the thread of the creator thread.

*   A future can block or throw an exception if the value of the promise is not available. C++11 blocks in this case the `wait` or `get` call. Additionally, you can wait with a timeout on the promise (`wait_for` and `wait_until`).
*   There are various ways to implement futures: [coroutines](https://en.wikipedia.org/wiki/Coroutine), [generators](https://en.wikipedia.org/wiki/Generator_(computer_programming)), or [channels](https://en.wikipedia.org/wiki/Channel_(programming)).

##### Further Information

*   [Futures and promises](https://en.wikipedia.org/wiki/Futures_and_promises)

### Dealing with Mutation

If you don’t write and read data concurrently, no [data races](#chap20.xhtml_chapterXXXDataSSSRaces) can happen. The easiest way to achieve this is by [immutable values](#chap15.xhtml_chapterXXXGeneralSSSBOBOBOBestSSSPracticesBCBCBC). Additionally to this best practice, there are two typical strategies. First, protect the [critical sections](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) by a lock such as a [scoped lock](#chap13.xhtml_chapterXXXScopedSSSLockingSSSBOBOBOPatternBCBCBC) or [strategized locking](#chap13.xhtml_chapterXXXStrategizedSSSLockingSSSBOBOBOPatternBCBCBC). In object-oriented design, the [critical section](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) is typically an object including its interface. The [Thread-Safe Interface](#chap13.xhtml_chapterXXXThread-SafeSSSInterfaceSSSBOBOBOPatternBCBCBC) protects the entire object. Second, the modifying thread just signals when it is done with it’s work. This is the strategy of [guarded suspension](#chap13.xhtml_chapterXXXGuardSSSSuspensionSSSBOBOBOPatternBCBCBC).

#### Scoped Locking

Scoped locking is the idea of RAII (**R**esource **A**cquisition **I**s **I**nitialization) applied to a [mutex](#chap06.xhtml_chapterXXXMutexes). The key idea of this idiom is to bind the resource acquisition and release to the lifetime of an object. As the name suggests it, the lifetime of the objects is scoped. Scoped means in particular that the C++ runtime is responsible for invoking the destructor of the object and, therefore, to release the resource.

The class `ScopedLock` implements scoped locking.

```
 1 // scopedLock.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 #include <new>
 6 #include <string>
 7 #include <utility>
 8 
 9 class ScopedLock{
10   private:
11     std::mutex& mut;
12   public:
13     explicit ScopedLock(std::mutex& m): mut(m){
14         mut.lock();
15         std::cout <<  "Lock the mutex: " << &mut <<   std::endl;
16     }
17     ~ScopedLock(){
18         std::cout << "Release the mutex: " << &mut << std::endl;
19         mut.unlock();
20     }
21 };
22 
23 int main(){
24 
25   std::cout << std::endl;
26 
27   std::mutex mutex1;
28   ScopedLock scopedLock1{mutex1};
29 
30   std::cout << "\nBefore local scope" << std::endl;
31   {
32     std::mutex mutex2;
33     ScopedLock scopedLock2{mutex2};
34   }
35   std::cout << "After local scope" << std::endl;
36   
37   std::cout << "\nBefore try-catch block" << std::endl;
38   try{
39       std::mutex mutex3;
40       ScopedLock scopedLock3{mutex3};
41       throw std::bad_alloc();
42   }   
43   catch (std::bad_alloc& e){
44       std::cout << e.what();
45   }
46   std::cout << "\nAfter try-catch block" << std::endl;
47   
48   std::cout << std::endl;
49   
50 }
```

Scoped Locking

`ScopedLock` gets its mutex by reference (line 13). The mutex is locked in the constructor (line 15) and unlocked in the destructor (line 19). Thanks to the RAII idiom, the destruction of the object and, therefore, the unlocking of the mutex is done automatically.

![Deterministic destruction with scoped locking](images/SynchronisationPatterns----scopedLock.png)

Deterministic destruction with scoped locking

The scope of `scopedLock1` ends at the end of the main function. Consequentially, `mutex1` is unlocked. The same holds for `mutex2` in line 34 and `mutex3` in line 42\. For `mutex3` this means, that the destructor of the `scopedLock3` is also invoked if an exception occurs. Interestingly, `mutex3` reuses the memory of `mutex2` because both have the same address.

C++17 supports locks in four variations. C++ has a `std::lock_guard` / `std::scoped_lock` for the simple, and a `std::unique_lock` / `std::shared_lock` for the advanced use cases such as the explicit locking or unlocking of the mutex. You can read all details in the subsection [locks](#chap06.xhtml_chapterXXXLocks).

##### Further Information

*   [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

#### Strategized Locking

Imagine, you write code such as a library, which should be used in various domains including concurrent ones. To be on the safe side, you protect the [critical sections](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) with a [lock](#chap06.xhtml_chapterXXXLocks). If your library now runs in a single threaded environment, you have a performance issue because you implemented expensive synchronisation mechanism that is not necessary. Now, strategized locking comes to your rescue.

Strategized locking is the idea of the strategy pattern applied to locking. This means, put your locking strategy into an object and make it to a pluggable component of your system. First of all: What is the strategy pattern?

##### Strategy Pattern

![The Strategy Pattern](images/SynchronisationPatterns----StrategyPattern.png)

The Strategy Pattern

The strategy pattern is one of the classic behavioural patterns of the book [Design Patterns: Elements of Reusable Object-Oriented Software](https://en.wikipedia.org/wiki/Design_Patterns). It’s also known as policy. The critical idea is it to define a family of algorithms and encapsulate each in an object and make it, therefore, to a pluggable component.

```
 1 // strategy.cpp
 2 
 3 #include <iostream>
 4 #include <memory>
 5 
 6 class Strategy {
 7 public:
 8     virtual void operator()() = 0;
 9     virtual ~Strategy() = default;
10 };
11 
12 class Context {
13     std::shared_ptr<Strategy> _strat;
14 public:
15     explicit Context() : _strat(nullptr) {}
16     void setStrategy(std::shared_ptr<Strategy> strat)  { _strat = strat; }
17     void strategy()  { if (_strat) (*_strat)(); }
18 };
19 
20 class Strategy1 : public Strategy {
21     void operator()() override { 
22         std::cout << "Foo" << std::endl; 
23     }
24 };
25 
26 class Strategy2 : public Strategy {
27     void operator()() override { 
28         std::cout << "Bar" << std::endl; 
29     }
30 };
31 
32 class Strategy3 : public Strategy {
33     void operator()() override { 
34         std::cout << "FooBar" << std::endl; 
35     }
36 };
37 
38 int main() {
39     
40     std::cout << std::endl;
41     
42     Context con;
43     
44     con.setStrategy( std::shared_ptr<Strategy>(new Strategy1) );
45     con.strategy();
46 
47     con.setStrategy( std::shared_ptr<Strategy>(new Strategy2) );
48     con.strategy();
49 
50     con.setStrategy( std::shared_ptr<Strategy>(new Strategy3) );
51     con.strategy();
52     
53     std::cout << std::endl;
54     
55 }
```

The Strategy Pattern

The abstract class `Strategy` in lines 6 to 10 defines the strategy. Each particular strategy such as `Strategy1` (line 20), `Strategy2` (line 26), or `Strategy3` (line 32) has to support the function call operator (line 8). The `Context` is the user of various strategies. It sets the particular strategy in line 16 and executes it in line 17\. Because the `Context` executes the strategy via a pointer to the `Strategy` class, the overriden methods of `Strategy1`, `Strategy2`, and `Strategie3` can be private. The context `con` uses various strategies.

![The Strategy Pattern applied](images/SynchronisationPatterns----strategy.png)

The Strategy Pattern applied

##### Implementation

There are two typical ways to implement strategized locking: runtime polymorphism (object-orientation) or compile-time polymorphism (templates). Both ways to implement it have their advantages and disadvantages.

*   Advantages:
    *   Runtime Polymorphism
        *   allows it to configure the locking strategy during runtime.
        *   is easier to understand for developers who have an object-oriented background.
    *   Compile-Time Polymorphism
        *   has no abstraction penalty.
        *   has a flat hierarchy.
*   Disadvantages:
    *   Runtime Polymorphism
        *   needs an additional pointer indirection.
        *   may have a deep derivation hierarchy.
    *   Compile-Time Polymorphism
        *   may generate in the error case a very verbose message.

After this theoretical discussion, I implement the strategized locking in both variations. The strategized locking supports in my example no-locking, exclusive locking, and shared locking. For simplicity reasons, I used internally already existing [mutexes](#chap06.xhtml_chapterXXXMutexes). Additionally, the strategized locking models [scoped locking](#chap13.xhtml_chapterXXXScopedSSSLockingSSSBOBOBOPatternBCBCBC).

###### Runtime Polymorphism

The program `strategizedLockingRuntime.cpp` presents three different mutexes.

```
 1 // strategizedLockingRuntime.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 #include <shared_mutex>
 6 
 7 class Lock {
 8 public:
 9     virtual void lock() const = 0;
10     virtual void unlock() const = 0;
11 };
12 
13 class StrategizedLocking {
14     Lock& lock;
15 public:
16     StrategizedLocking(Lock& l): lock(l){
17         lock.lock();
18     }
19     ~StrategizedLocking(){
20         lock.unlock();
21     }
22 };
23 
24 struct NullObjectMutex{
25     void lock(){}
26     void unlock(){}
27 };
28 
29 class NoLock : public Lock {
30     void lock() const override {
31         std::cout << "NoLock::lock: " << std::endl;
32         nullObjectMutex.lock();
33     }
34     void unlock() const override {
35         std::cout << "NoLock::unlock: " << std::endl;
36          nullObjectMutex.unlock();
37     }
38     mutable NullObjectMutex nullObjectMutex;
39 };
40 
41 class ExclusiveLock : public Lock {
42     void lock() const override {
43         std::cout << "    ExclusiveLock::lock: " << std::endl;
44         mutex.lock();
45     }
46     void unlock() const override {
47         std::cout << "    ExclusiveLock::unlock: " << std::endl;
48         mutex.unlock();
49     }
50     mutable std::mutex mutex;
51 };
52 
53 class SharedLock : public Lock {
54     void lock() const override {
55         std::cout << "        SharedLock::lock_shared: " << std::endl;
56         sharedMutex.lock_shared();
57     }
58     void unlock() const override {
59         std::cout << "        SharedLock::unlock_shared: " << std::endl;
60         sharedMutex.unlock_shared();
61     }
62     mutable std::shared_mutex sharedMutex;
63 };
64 
65 int main() {
66     
67     std::cout << std::endl;
68     
69     NoLock noLock;
70     StrategizedLocking stratLock1{noLock};
71     
72     {
73         ExclusiveLock exLock;
74         StrategizedLocking stratLock2{exLock};
75         {
76             SharedLock sharLock;
77             StrategizedLocking startLock3{sharLock};
78         }
79     }
80     
81     std::cout << std::endl;
82     
83 }
```

Strategized Locking via Runtime Polymorphism

The class `StrategizedLocking` has a lock (line 14). `StrategizedLocking` models scoped locking and, therefore, locks the mutex in the constructor (line16) and unlocks it in the destructor (line 19). `Lock` (lines 7 - 11) is an abstract class and defines the interface for all derived classes. These are the classes `NoLock` (line 29), `ExclusiveLock` (line 41), and `SharedLock` (line 53). `SharedLock` invokes `lock_shared` (line 56) and `unlock_shared` on its `std::shared_mutex`. Each of these locks holds one of the mutexes `NullObjectMutex` (line 38), `std::mutex` (line 50), or `std::shared_mutex` (line 62). `NullObjectMutex` is a *no-op* placeholder. The mutexes are declared as `mutable`. This means they can be used in constant methods such as the methods `lock` and `unlock`.

###### Compile-Time Polymorphism

The template-based implementation is quite similar to the object-oriented based implementation.

```
 1 // StrategizedLockingCompileTime.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 #include <shared_mutex>
 6 
 7 
 8 template <typename LOCK>
 9 class StrategizedLocking {
10     LOCK& lock;
11 public:
12     StrategizedLocking(LOCK& l): lock(l){
13         lock.lock();
14     }
15     ~StrategizedLocking(){
16         lock.unlock();
17     }
18 };
19 
20 struct NullObjectMutex {
21     void lock(){}
22     void unlock(){}
23 };
24 
25 class NoLock{
26 public:
27     void lock() const {
28         std::cout << "NoLock::lock: " << std::endl;
29         nullObjectMutex.lock();
30     }
31     void unlock() const {
32         std::cout << "NoLock::unlock: " << std::endl;
33          nullObjectMutex.lock();
34     }
35     mutable NullObjectMutex nullObjectMutex;
36 };
37 
38 class ExclusiveLock {
39 public:
40     void lock() const {
41         std::cout << "    ExclusiveLock::lock: " << std::endl;
42         mutex.lock();
43     }
44     void unlock() const {
45         std::cout << "    ExclusiveLock::unlock: " << std::endl;
46         mutex.unlock();
47     }
48     mutable std::mutex mutex;
49 };
50 
51 class SharedLock {
52 public:
53     void lock() const {
54         std::cout << "        SharedLock::lock_shared: " << std::endl;
55         sharedMutex.lock_shared();
56     }
57     void unlock() const {
58         std::cout << "        SharedLock::unlock_shared: " << std::endl;
59         sharedMutex.unlock_shared();
60     }
61     mutable std::shared_mutex sharedMutex;
62 };
63 
64 int main() {
65 
66     std::cout << std::endl;
67     
68     NoLock noLock;
69     StrategizedLocking<NoLock> stratLock1{noLock};
70     
71     {
72         ExclusiveLock exLock;
73         StrategizedLocking<ExclusiveLock> stratLock2{exLock};
74         {
75             SharedLock sharLock;
76             StrategizedLocking<SharedLock> startLock3{sharLock};
77         }
78     }
79     
80     std::cout << std::endl;
81 
82 }
```

Strategized Locking via Compile-Time Polymorphism

The locks `NoLock` (line 25), `ExclusiveLock` (line 38), and `SharedLock` (line 51) have no abstract base class. The consequence is that `StrategizedLocking` can be instantiated with an object which does not support the right interface. This would end in a compile-time error. This loophole is closed with C++20\. Instead of `template <typename Lock> class StrategizedLocking` you can use the concept `Lockable`: `template <Lockable Lock> class StrategizedLocking`. This means that all used locks have to support the [concept](https://en.cppreference.com/w/cpp/language/constraints) `Lockable`. A concept is a named requirement, and the concept [`Lockable`](https://en.cppreference.com/w/cpp/named_req) is already defined in C++20\. If this requirement is not provided, the compilation will fail with a concise error message.

Both programs produce the same output:

![StrategizedLocking](images/SynchronisationPatterns----strategizedLocking.png)

StrategizedLocking

##### Further Information

*   [Design Patterns: Elements of Reusable Object-Oriented Software](https://en.wikipedia.org/wiki/Design_Patterns)
*   [Strategy Pattern](https://en.wikipedia.org/wiki/Strategy_pattern)
*   [Null Object Pattern](https://en.wikipedia.org/wiki/Null_object_pattern)
*   [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

#### Thread-Safe Interface

The thread-safe interface fits very well when the [critical sections](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) is just an objects. The naive idea to protect all methods with a lock causes in the best case a performance issue and in the worst case a [deadlock](#chap20.xhtml_chapterXXXDeadlocks). The small pseudocode makes my point clear.

```
struct Critical{
    void method1(){
        lock(mut);
        method2();
        ...
    }
    void method2(){
        lock(mut);
        ...
    }
    mutex mut;
};

Critical crit;
crit.method1();
```

Calling `crit.method1` causes the mutex `mut` being locked twice. For simplicity reasons the `lock` is a [scoped lock](#chap13.xhtml_chapterXXXScopedSSSLockingSSSBOBOBOPatternBCBCBC). Here are the two issues:

1.  when `lock` is a recursive lock, the second `lock(mut)` in `method2` is superfluous.
2.  when `lock` is a non-recursive lock, the second `lock(mut)` in `method2` leads to undefined behaviour. Most of the times, you get a [deadlock](#chap20.xhtml_chapterXXXDeadlocks).

The thread-safe interface overcomes both issues. This is the simple and straightforward idea:

*   All interface methods (`public`) should use a lock.
*   All implementation methods (`protected` and `private`) must not use a lock.
*   The interface methods call only `protected` or `private` methods but no `public` methods.

The `threadSafeInterface.cpp` program shows its usage.

```
 1 // threadSafeInterface.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 #include <thread>
 6 
 7 class Critical{
 8 
 9 public:
10     void interface1() const {
11         std::lock_guard<std::mutex> lockGuard(mut);
12         implementation1();
13     }
14     void interface2(){
15         std::lock_guard<std::mutex> lockGuard(mut);
16         implementation2();
17         implementation3();
18         implementation1();
19     }
20 private: 
21     void implementation1() const {
22         std::cout << "implementation1: " 
23                   << std::this_thread::get_id() << std::endl;
24     }
25     void implementation2(){
26         std::cout << "    implementation2: " 
27                   << std::this_thread::get_id() << std::endl;
28     }
29     void implementation3(){    
30         std::cout << "        implementation3: " 
31                   << std::this_thread::get_id() << std::endl;
32     }
33   
34 
35 mutable std::mutex mut;
36 
37 };
38 
39 int main(){
40     
41     std::cout << std::endl;
42     
43     std::thread t1([]{ 
44         const Critical crit;
45         crit.interface1();
46     });
47     
48     std::thread t2([]{
49         Critical crit;
50         crit.interface2();
51         crit.interface1();
52     });
53     
54     Critical crit;
55     crit.interface1();
56     crit.interface2();
57     
58     t1.join();
59     t2.join();    
60     
61     std::cout << std::endl;
62     
63 }
```

The Thread-Safe Interface

Three threads, including the main-thread, use instances of `Critical`. Thanks to the thread-safe interface, all calls to the public API are synchronised. The mutex `mut` in line 35 is mutable and can, therefore, be used in the constant method `implementation1`.

The benefits of the thread-safe interface are threefold.

1.  A recursive call of a mutex is not possible. Recursive calls on a non-recursive mutex are undefined behaviour in C++ and usually end in a deadlock.
2.  The program uses minimal locking and, therefore, minimal synchronisation. Using just a `std::recursive_mutex` in each public or private method of the class `Critical` would end in more expensive synchronisations.
3.  From the user perspective, `Critical` is straightforward to use because the synchronisation is only an implementation detail.

The output of the program shows the interleaving of the three threads.

![Thread-Safe Interface](images/SynchronisationPatterns----threadSafeInterface.png)

Thread-Safe Interface

Although the thread-safe interface seems easy to implement, there are two grave perils you have to keep in mind.

##### Perils

Using a static member in your class or having virtual interfaces requires special care.

###### Static members

When your class has a static member which is not constant, you have to synchronise all method calls on instances of the class.

```
 1 class Critical{
 2     
 3 public:
 4     void interface1() const {
 5         std::lock_guard<std::mutex> lockGuard(mut);
 6         implementation1();
 7     }
 8     void interface2(){
 9         std::lock_guard<std::mutex> lockGuard(mut);
10         implementation2();
11         implementation3();
12         implementation1();
13     }
14     
15 private: 
16     void implementation1() const {
17         std::cout << "implementation1: " 
18                   << std::this_thread::get_id() << std::endl;
19         ++called;
20     }
21     void implementation2(){
22         std::cout << "    implementation2: " 
23                   << std::this_thread::get_id() << std::endl;
24         ++called;
25     }
26     void implementation3(){    
27         std::cout << "        implementation3: " 
28                   << std::this_thread::get_id() << std::endl;
29         ++called;
30     }
31     
32     inline static int called{0};
33     inline static std::mutex mut;
34 
35 };
```

The Thread-Safe Interface with a static member

The class `Critical` has now the static member `called` (line 32) to count how often the implementation functions were called. All instances of `Critical` use the same static member `called` and have, therefore, to be synchronised. The critical section contains, in this case, all instances of `Critical`.

###### Virtuality

When you override a virtual interface function, the overriding function should have a lock even if the function is private.

```
 1 // threadSafeInterfaceVirtual.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 #include <thread>
 6 
 7 class Base{
 8     
 9 public:
10     virtual void interface() {
11         std::lock_guard<std::mutex> lockGuard(mut);
12         std::cout << "Base with lock" << std::endl;
13     }
14 private:
15     std::mutex mut;
16 };
17 
18 class Derived: public Base{
19 
20     void interface() override {
21         std::cout << "Derived without lock" << std::endl;
22     }
23 
24 };
25 
26 int main(){
27 
28     std::cout << std::endl;
29 
30     Base* base1 = new Derived;
31     base1->interface();
32 
33     Derived der;
34     Base& base2 = der;
35     base2.interface();
36 
37     std::cout << std::endl;
38 
39 }
```

The Thread-Safe Interface with a virtual method

In the calls `base1->interface` and `base2.interface` the static type of `base1` and `base2` is `Base` and, therefore, `interface` is a public method. Because the interface method is virtual the call dispatch happens at run-time using the dynamic types which is `Derived`. At last, the private method `interface` of the class `Derived` is invoked.

![Thread-Safe Interface with virtual method](images/SynchronisationPatterns----threadSafeInterfaceVirtual.png)

Thread-Safe Interface with virtual method

There are two typical ways to overcome this issue.

1.  Make the method `interface` a non-virtual method. This technique is called [NVI (**N**on-**V**irtual **I**nterfac)](https://en.wikibooks.org/wiki/More_C%2B%2B_Idioms/Non-Virtual_Interface)
2.  Declare the method `interface` as final: `virtual void interface() final;`

##### Further Information

*   [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

#### Guarded Suspension

A guarded suspension is its basic variant a combination of a [lock](#chap06.xhtml_chapterXXXLocks) and a precondition that must be satisfied. If the precondition is not fulfilled, that calling thread puts itself to sleep. To avoid a [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition) which may result in a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) or a [deadlock](#chap20.xhtml_chapterXXXDeadlocks), the checking thread uses a lock.

Now, the various variants exist:

*   The waiting thread can be passively notified about the state change, or actively ask for the state change. In short, I call this push versus pull principle.
*   The waiting can be done with or without a time boundary.
*   The notification can be sent to one or all waiting threads.

I have already discussed in depth each of the three variants. What is, therefore, left for this subsection is to bundle all information in one place. For the details, please follow the links in this subsection to the guarded suspension.

##### Push versus Pull Principle

Let me start with the push principle.

###### Push Principle

Most of the time, you use a [condition variable](#chap06.xhtml_chapterXXXConditionSSSVariablesZZZcondition_variable) or a [future/promise](#chap06.xhtml_chapterXXXNotifications) pair to synchronise threads. The condition variable or the promise send the notification to the waiting thread. A promise has no `notify_one` or `notify_all` method. Instead, an empty `set_value` call is typically used to simulate a notification. The following program snippets show the thread sending the notification and the waiting thread.

*   Condition variables

```
void waitingForWork(){
    std::cout << "Worker: Waiting for work." << std::endl;
    std::unique_lock<std::mutex> lck(mutex_);
    condVar.wait(lck, []{ return dataReady; });
    doTheWork();
    std::cout << "Work done." << std::endl;
}

void setDataReady(){
    {
      std::lock_guard<std::mutex> lck(mutex_);
      dataReady = true;
    }
    std::cout << "Sender: Data is ready."  << std::endl;
    condVar.notify_one();
}
```

*   Future/promise pair

```
void waitingForWork(std::future<void>&& fut){

    std::cout << "Worker: Waiting for work." << std::endl;
    fut.wait();
    doTheWork();
    std::cout << "Work done." << std::endl;

}

void setDataReady(std::promise<void>&& prom){

    std::cout << "Sender: Data is ready."  << std::endl;
    prom.set_value();

}
```

###### Pull Principle

Instead of passively waiting for the state change, you can actively ask for it. This pull principle is not natively supported in C++ but can be, for example, implemented with [atomics](#chap05.xhtml_chapterXXXatomicBBBboolEEE).

```
std::vector<int> mySharedWork;
std::atomic<bool> dataReady(false);

void waitingForWork(){
    std::cout << "Waiting " << std::endl;
    while (!dataReady.load()){                
        std::this_thread::sleep_for(std::chrono::milliseconds(5));
    }
    mySharedWork[1] = 2;                     
    std::cout << "Work done " << std::endl;
}

void setDataReady(){
    mySharedWork = {1, 0, 3};                  
    dataReady = true;                          
    std::cout << "Data prepared" << std::endl;
}
```

##### Waiting with and without time boundary

A condition variable and a future have three methods for waiting: `wait`, `wait_for`, and `wait_until`. The `wait_for` variant requires a [time duration](#chap21.xhtml_chapterXXXTimeSSSDuration) and the `wait_until` variant a [time point](#chap21.xhtml_chapterXXXTimeSSSPoint). In order not to bore you, I skip waiting without time boundaries (`wait`) in this section. The last subsection to the push principle already provides two examples.

The consumer thread in [various waiting strategies](#chap21.xhtml_chapterXXXVariousSSSwaitingSSSstrategies) waits for the time duration `steady_clock::now() + dur`. If the promise is ready it asks for the value; if not, it just displays its id: `this_thread::get_it()`.

```
void producer(promise<int>&& prom){
    cout << "PRODUCING THE VALUE 2011\n\n"; 
    this_thread::sleep_for(seconds(5));
    prom.set_value(2011);
}

void consumer(shared_future<int> fut,
              steady_clock::duration dur){
    const auto start = steady_clock::now();
    future_status status= fut.wait_until(steady_clock::now() + dur);
    if ( status == future_status::ready ){
        lock_guard<mutex> lockCout(coutMutex);
        cout << this_thread::get_id() << " ready => Result: " << fut.get() 
             << endl;
    }
    else{
        lock_guard<mutex> lockCout(coutMutex);
        cout << this_thread::get_id() << " stopped waiting." << endl;
    }
    const auto end= steady_clock::now();
    lock_guard<mutex> lockCout(coutMutex);
    cout << this_thread::get_id() << " waiting time: " 
         << getDifference(start,end) << " ms" << endl;
}
```

##### Notify one or all waiting threads

`notify_one` awakes one of the waiting threads, `notify_all` awakes all of the waiting threads. With `notify_one`, you have no guarantee which one will be awaken. The other condition variables do stay in the wait state. This could not happen with a `std::future`, because there is a one-to-one association between the future and the promise. If you want to simulate a one-to-many association, use a [`std::shared_future`](#chap06.xhtml_chapterXXXshared_future) instead of a `std::future` because a `std::shared_future` can be copied.

The following program shows a simple workflow with an one-to-one and an one-to-many association between promises and futures.

```
 1 // bossWorker.cpp
 2 
 3 #include <future>
 4 #include <chrono>
 5 #include <iostream>
 6 #include <random>
 7 #include <string>
 8 #include <thread>
 9 #include <utility>
10 
11 int getRandomTime(int start, int end){
12   
13   std::random_device seed;
14   std::mt19937 engine(seed());
15   std::uniform_int_distribution<int> dist(start,end);
16   
17   return dist(engine);
18 };
19 
20 class Worker{
21 public:
22   explicit Worker(const std::string& n):name(n){};
23   
24   void operator() (std::promise<void>&& preparedWork, 
25                    std::shared_future<void> boss2Worker){
26       
27     // prepare the work and notfiy the boss
28     int prepareTime= getRandomTime(500, 2000);
29     std::this_thread::sleep_for(std::chrono::milliseconds(prepareTime));
30     preparedWork.set_value();
31     std::cout << name << ": " << "Work prepared after " 
32               << prepareTime << " milliseconds." << std::endl;
33 
34     // still waiting for the permission to start working
35     boss2Worker.wait();
36   }    
37 private:
38   std::string name;
39 };
40 
41 int main(){
42   
43   std::cout << std::endl;
44   
45   // define the std::promise => Instruction from the boss
46   std::promise<void> startWorkPromise;
47 
48   // get the std::shared_future's from the std::promise
49   std::shared_future<void> startWorkFuture= startWorkPromise.get_future();
50 
51   std::promise<void> herbPrepared;
52   std::future<void> waitForHerb = herbPrepared.get_future();
53   Worker herb("  Herb");
54   std::thread herbWork(herb, std::move(herbPrepared), startWorkFuture);
55   
56   std::promise<void> scottPrepared;
57   std::future<void> waitForScott = scottPrepared.get_future();
58   Worker scott("    Scott");
59   std::thread scottWork(scott, std::move(scottPrepared), startWorkFuture);
60   
61   std::promise<void> bjarnePrepared;
62   std::future<void> waitForBjarne = bjarnePrepared.get_future();
63   Worker bjarne("      Bjarne");
64   std::thread bjarneWork(bjarne, std::move(bjarnePrepared), startWorkFuture);
65   
66   std::cout << "BOSS: PREPARE YOUR WORK.\n " << std::endl;
67   
68   // waiting for the worker 
69   waitForHerb.wait(), waitForScott.wait(), waitForBjarne.wait();
70   
71   // notify the workers that they should begin to work
72   std::cout << "\nBOSS: START YOUR WORK. \n" << std::endl;
73   startWorkPromise.set_value();
74   
75   herbWork.join();
76   scottWork.join();
77   bjarneWork.join();
78    
79 }
```

A boss/worker workflow

The key idea of the program is that the boss (main-thread) has three workers: `herb` (line 53), `scott` (line 58), and `bjarne` (line 63). Each worker is represented by a thread. In line 64, the boss waits until all workers are done with the preparation of their work package. This means each worker sends after an arbitrary time the notification to the boss that it is done. The worker to boss notification is a one-to-one relation (line 30) because it goes to a `std::future`. In contrast, the instruction to start the work is an one-to-many notification (line 73) form the boss to its workers. For this one-to-many notification, a `std::shared_future` is necessary.

![A Boss/Worker Workflow](images/SynchronisationPatterns----bossWorker.png)

A Boss/Worker Workflow

##### Further Information

*   [Concurrent Programming in Java: Design Principles and Patterns (Doug Lea)](http://gee.cs.oswego.edu/dl/cpj/)

## Concurrent Architecture

The three patterns presented in this chapter are classics. The presented patterns are very well explained in the invaluable book [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/). My goal for this chapter is it to give a concise overview of the [Active Object](#chap14.xhtml_chapterXXXActiveSSSObject), the [Monitor Object](#chap14.xhtml_chapterXXXMonitorSSSObject), and the [Half-Sync/Half-Async](#chap14.xhtml_chapterXXXHalf-Sync/Half-Async) pattern. As in the last chapter on [Synchronisation Patterns](#chap13.xhtml_chapterXXXSynchronisationSSSPatterns), I’m wearing C++ glasses. Before I dive into the three patterns, here are the patterns from a birds-eye perspective.

*   The **Active Object** design pattern decouples method execution from method invocation for objects that each reside in their own thread of control. The goal is to introduce concurrency, by using asynchronous method invocation and a scheduler for handling requests. [Wikipedia: Active object](https://en.wikipedia.org/wiki/Active_object)
*   The **Monitor Object** design pattern synchronizes concurrent method execution to ensure that only one method at a time runs within an object. It also allows object’s methods to schedule their execution sequences cooperatively. [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

Both patterns synchronise and schedule method invocation. The main difference is that the Active Object executes its method in a different thread but the monitor in the same thread as the client. In contrast to the Active Object and the Monitor Object which have a subsystem focus and are, therefore, typically called design patterns, the following pattern have a system perspective and is called consequently architectural pattern.

*   The **Half-Sync/Half-Async** architectural pattern decouples asynchronous and synchronous service processing in concurrent systems, to simplify programming without unduly reducing performance. The pattern introduces two intercommunicating layers, one for asynchronous and one for synchronous service processing. [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

### Active Object

The Active Object design pattern decouples method execution from method invocation for objects that each reside in their own thread of control. The goal is to introduce concurrency, by using asynchronous method invocation and a scheduler for handling requests. [Wikipedia: Active object](https://en.wikipedia.org/wiki/Active_object). This pattern is also known as Concurrent Object.

Here are more details on the Active Object. The method invocation of the client goes to a proxy, which represents the interface of the Active Object. The servant provides the implementation of the Active Object, which runs in the separate thread. At run-time, the proxy transforms the invocation into a method invocation on the servant. This method invocations are enqueued in an activation list by the scheduler. A scheduler’s event loop runs in the same thread as the servant, dequeues the method invocations from the activation list and dispatches them on the servant. The client obtains the result via a future from the proxy.

#### Components

The Active Object pattern consists of six components:

1.  The **proxy** provides an interface for the accessible methods on the Active Object. The proxy triggers the construction of a method request object which goes into the activation list. The proxy runs in the same thread as the client.
2.  The **method request** class defines the interface for the method executing of an Active Object.
3.  The **activation list** maintains the pending method requests. The activation list decouples the clients thread from the Active Object thread. The proxy inserts the method requests and the scheduler removes them.
4.  The **scheduler** runs in a different thread than the proxy. It runs in the thread of the Active Object and decides which method request from the activation list is executed next.
5.  The **servant** implements the Active Object and runs in the thread of the Active Object. The servant supports the interface of the proxy.
6.  The **future** is created by the proxy. The future allows the client to obtain the result of the method invocation on the Active Object. The client can wait for the result or poll for it.

The following picture shows the sequence of messages.

![Active Object](images/ArchitecturePatterns----ActiveObject.jpg)

Active Object

#### Advantages and Disadvantages

Before I present a minimal implementation of the Active Object pattern, here are the advantages and disadvantages of using it.

*   Advantages:
    *   The synchronisation is only necessary on the Active Object’s thread but not on the client’s threads.
    *   Clear separation between the client (user) and the server (implementer). The synchronisation challenges are on the implementer’s side.
    *   Enhanced throughput of the system because of the asynchronous execution of the client requests. Invoking processing-intensive methods do not block the entire system.
    *   The scheduler can implement various strategies to execute the pending requests. If so, the jobs can be executed in a different order they are enqueued.
*   Disadvantages:
    *   If the method requests are too fine-grained, the performance overhead of the Active Object pattern such as the proxy, the activation list, and the scheduler may be excessive.
    *   Due to the scheduling strategy of the scheduler and the scheduling of the operating system, it is often quite difficult to debug the Active Object pattern. This holds in particular true, if the jobs are executed in a different order they are enqueued.

#### Implementation

The following example presents a simple implementation of the Active Object pattern. In particular, I don’t define a class method request, which should be implemented by the proxy and the servant. Further, the scheduler just executes the next job when asked for it.

The involved types `future<vector<future<pair<bool, int>>>>` are often quite verbose. To improve the readability, I heavily applied using declarations (lines 16 - 37).

```
 1 // activeObject.cpp
  2 
  3 #include <algorithm>
  4 #include <deque>
  5 #include <functional>
  6 #include <future>
  7 #include <iostream>
  8 #include <memory>
  9 #include <mutex>
 10 #include <numeric>
 11 #include <random>
 12 #include <thread>
 13 #include <utility>
 14 #include <vector>
 15 
 16 using std::async;
 17 using std::boolalpha;
 18 using std::cout;
 19 using std::deque;
 20 using std::distance;
 21 using std::endl;
 22 using std::for_each;
 23 using std::find_if;
 24 using std::future;
 25 using std::lock_guard;
 26 using std::make_move_iterator;
 27 using std::make_pair;
 28 using std::move;
 29 using std::mt19937;
 30 using std::mutex;
 31 using std::packaged_task;
 32 using std::pair;
 33 using std::random_device;
 34 using std::sort;
 35 using std::thread;
 36 using std::uniform_int_distribution;
 37 using std::vector;
 38 
 39 class IsPrime{
 40 public:
 41     pair<bool, int> operator()(int i){
 42         for (int j=2; j*j <= i; ++j){
 43             if (i % j == 0) return std::make_pair(false, i);
 44         }
 45         return std::make_pair(true, i);
 46     }       
 47 };
 48 
 49 class ActiveObject{
 50 public:
 51     
 52     future<pair<bool, int>> enqueueTask(int i){
 53         IsPrime isPrime;
 54         packaged_task<pair<bool, int>(int)> newJob(isPrime);
 55         auto isPrimeFuture = newJob.get_future();
 56         auto pair = make_pair(move(newJob), i);
 57         {
 58             lock_guard<mutex> lockGuard(activationListMutex);
 59             activationList.push_back(move(pair));
 60         }
 61         return isPrimeFuture;
 62     }
 63         
 64     void run(){
 65         thread servant([this]{ 
 66             while ( !isEmpty() ){   
 67                 auto myTask = dequeueTask();
 68                 myTask.first(myTask.second);
 69             }
 70         });
 71         servant.join();
 72     }
 73 
 74 private:
 75     
 76     pair<packaged_task<pair<bool, int>(int)>, int > dequeueTask(){
 77         lock_guard<mutex> lockGuard(activationListMutex);
 78         auto myTask= std::move(activationList.front());
 79         activationList.pop_front();
 80         return myTask;
 81     }
 82     
 83     bool isEmpty(){
 84         lock_guard<mutex> lockGuard(activationListMutex);
 85         auto empty = activationList.empty();
 86         return empty;
 87     }
 88     
 89     deque<pair<packaged_task<pair<bool, int>(int)>, int >> activationList; 
 90     mutex activationListMutex;
 91 };
 92 
 93 vector<int> getRandNumbers(int number){
 94     random_device seed;
 95     mt19937 engine(seed());
 96     uniform_int_distribution<> dist(1000000, 1000000000);
 97     vector<int> numbers;
 98     for (long long i = 0 ; i < number; ++i) numbers.push_back(dist(engine)); 
 99     return numbers;
100 }
101 
102 future<vector<future<pair<bool, int>>>> getFutures(ActiveObject& activeObject, 
103                                                    int numberPrimes){
104     return async([&activeObject, numberPrimes]{
105         vector<future<pair<bool, int>>> futures;
106         auto randNumbers = getRandNumbers(numberPrimes);
107         for (auto numb: randNumbers){
108             futures.push_back(activeObject.enqueueTask(numb));
109         }
110         return futures;
111     });
112 }
113     
114 
115 int main(){
116     
117     cout << boolalpha << endl;
118     
119      ActiveObject activeObject;
120         
121     // a few clients enqueue work concurrently 
122     auto client1 = getFutures(activeObject, 1998);
123     auto client2 = getFutures(activeObject, 2003);
124     auto client3 = getFutures(activeObject, 2011);
125     auto client4 = getFutures(activeObject, 2014);
126     auto client5 = getFutures(activeObject, 2017);
127     
128     // give me the futures
129     auto futures = client1.get();
130     auto futures2 = client2.get();
131     auto futures3 = client3.get();
132     auto futures4 = client4.get();
133     auto futures5 = client5.get();
134     
135     // put all futures together
136     futures.insert(futures.end(),make_move_iterator(futures2.begin()), 
137                                  make_move_iterator(futures2.end()));
138     
139     futures.insert(futures.end(),make_move_iterator(futures3.begin()), 
140                                  make_move_iterator(futures3.end()));
141     
142     futures.insert(futures.end(),make_move_iterator(futures4.begin()), 
143                                  make_move_iterator(futures4.end()));
144     
145     futures.insert(futures.end(),make_move_iterator(futures5.begin()), 
146                                  make_move_iterator(futures5.end()));
147     
148     // run the promises
149     activeObject.run();
150     
151     // get the results from the futures
152     vector<pair<bool, int>> futResults;
153     futResults.reserve(futures.size());
154     for (auto& fut: futures) futResults.push_back(fut.get());
155     
156     sort(futResults.begin(), futResults.end());
157     
158     // separate the primes from the non-primes
159     auto prIt = find_if(futResults.begin(), futResults.end(), 
160                         [](pair<bool, int> pa){ return pa.first == true; });
161  
162     cout << "Number primes: " << distance(prIt, futResults.end()) << endl;
163     cout << "Primes:" << endl;
164     for_each(prIt, futResults.end(), [](auto p){ cout << p.second << " ";} );
165     
166     cout << "\n\n";
167     
168     cout << "Number no primes: " << distance(futResults.begin(), prIt) << endl;
169     cout << "No primes:" << endl;
170     for_each(futResults.begin(), prIt, [](auto p){ cout << p.second << " ";} );
171     
172     cout << endl;
173     
174 }
```

Active Object

First of all. The general idea of the example is that clients can enqueue concurrently jobs on the activation list. The job for the servant is to determine which numbers are prime. The activation list is part of the Active Object. Afterwards, the Active Object runs the jobs enqued in the activation list on a separate thread, and the clients can ask for the results.

Here are the details. The five clients enqueue the work (lines 121 - 126) on the `activeObject` via the `getFutures` function. `getFutures` takes the `activeObject` and a number `numberPrimes`. `numberPrimes` random numbers are generated (line 106) between 1000000 and 1000000000 (line 96) and pushed on the return value: `vector<future<pair<bool, int>>`. `future<pair<bool, int>` hold a `bool` and an `int`. The bool indicates if the `int` is a prime. Let’s have a closer look at line 108: `futures.push_back(activeObject.enqueueTask(numb))`. This call triggers that a new job is enqueued on the activation list. All call to the activation list have to be protected. The activation list is a deque of promises (line 89): `deque<pair<packaged_task<pair<bool, int>(int)>, int >>`. Each promise performs the function object `IsPrime` (lines 39 - 47) when called. The return value is a pair of a `bool` and an `int` which indicated if the number is prime. Now, the work packages are prepared. Let’s start the calculation. All clients return in the lines 129 - 133 the handle to the associated future. Putting all futures together (lines 136 - 146) makes my job easier. The call `activeObject.run()` in line 149 start the execution. The method `run` (line 64 - 72) starts the separate thread and executes the promises (line 68) until all jobs are performed (line 66). The method `isEmpty` (lines 83 - 87) determines if the deque is empty and the method `dequeTask` returns a new task. By calling `futResults.push_back(fut.get())` (line 154) on each future, all results are requested and pushed on `futResults`. Line 156 sorts the vector of pairs: `vector<pair<bool, int>>`. The remaining lines present the calculation. The iterator `prIt` in line 159 holds the first iterator to a pair which has a prime number.

The screenshot shows the number of primes `distance(prIt, futResults.end())` (line 162) and the primes (line 164). Only the first non-primes are displayed.

![Active Object](images/ArchitecturePatterns----activeObject.png)

Active Object

#### Further Information

*   [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)
*   [Prefer Using Active Object instead of Naked Thread (Herb Sutter)](http://www.drdobbs.com/parallel/prefer-using-active-objects-instead-of-n/225700095)
*   [Active Object implementation in C++11](https://github.com/lightful/syscpp/)

### Monitor Object

The Monitor Object design pattern synchronizes concurrent method execution to ensure that only one method at a time runs within an object. It also allows object’s methods to schedule their execution sequences cooperatively. This pattern is also known as Thread-Safe Passive Object.

#### Requirements

If many threads access a shared object concurrently, the following requirements must be fulfilled.

1.  Due to the concurrent access, the shared object must be protected from non-synchronised read and write operations to avoid [data races](#chap20.xhtml_chapterXXXDataSSSRaces).
2.  The necessary synchronisation should be part of the implementation and not part of the interface.
3.  When a thread is done with the shared object, a notification should be triggered so that the next thread can use the shared object. This mechanism helps to avoid [deadlocks](#chap20.xhtml_chapterXXXDeadlocks) and improves the overall performance of the system.
4.  After a method was performed, the invariants of the shared object must hold.

The solution to these four requirements is a Monitor Object. A client (thread) can access the synchronised methods of the Monitor Object, and due to the monitor lock only one synchronised method can run at any given point in time. Each Monitor Object has a monitor condition which notifies the waiting clients.

#### Components

The Monitor Object consists of four components.

![Monitor Object](images/ArchitecturePatterns----MonitorObject.jpg)

Monitor Object

1.  **Monitor Object**: The Monitor Object supports one or more methods. Each client must access the object through these methods. Each method runs in the thread of the client.
2.  **Synchronised methods**: The synchronised methods are the methods supported by the Monitor Object. Only one method can execute at any given point in time. [The Thread-Safe Interface](#chap13.xhtml_chapterXXXThread-SafeSSSInterfaceSSSBOBOBOPatternBCBCBC) helps to distinguish between the interface methods (synchronised methods) and the implementation methods of the Monitor Object.
3.  **Monitor lock**: Each Monitor Object has one monitor lock which ensures that at most one client can access the Monitor Object at any given point in time.
4.  **Monitor condition**: The monitor condition allows separate threads to schedule their method invocations on the Monitor Object. When the current client is done with its invocation of the synchronised methods, the next waiting client is awakened to invoke the synchronised methods on the Monitor Object.

While the monitor lock ensures the exclusive access to the synchronised methods, the monitor condition guarantees minimal waiting for the clients. Essentially, the monitor lock protects from [data races](#chap20.xhtml_chapterXXXDataSSSRaces) and the condition monitor from [deadlocks](#chap20.xhtml_chapterXXXDeadlocks).

#### Runtime behaviour

The interaction between the Monitor Object and its components has different phases.

*   When a client invokes a synchronised method on a Monitor Object, it must first lock the global monitor lock. If the client is successful it executes the synchronised method and unlocks the monitor lock at the end. If the client is not successful, the client is blocked.
*   When the client is blocked because it cannot make any progress it waits until the monitor condition sends a notification. This notification happens when the monitor is unlocked. The notification can be sent only to one or to all of the waiting clients. Typically, waiting means resource-friendly sleeping in contrast to [busy-waiting](#chap05.xhtml_textXXXbusySSSwaiting).
*   When a client gets the notification to resume, it locks the monitor lock and executes the synchronised method. At the end of the synchronised method, the monitor lock is unlocked and a notification of the monitor condition is sent to signal that the next client can execute its synchronised method.

#### Advantages and Disadvantages

What are the advantages and disadvantages of the Monitor Object?

*   Advantages:
    *   The client is not aware of the implicit synchronisation of the Monitor Object. The synchronisation is fully encapsulated in the implementation.
    *   The invoked synchronised methods will be eventually automatically scheduled. The notification/waiting mechanism of the monitor condition behaves as a simple scheduler.
*   Disadvantages:
    *   It is often quite difficult to change the synchronisation mechanism of the synchronisation methods because the functionality and the synchronisation are strongly coupled.
    *   When a synchronised method invokes directly or indirectly the same Monitor Object, a [deadlock](#chap20.xhtml_chapterXXXDeadlocks) may occur.

The following examples defines a `ThreadSafeQueue`.

```
 1 // monitorObject.cpp
 2 
 3 #include <condition_variable>
 4 #include <functional>
 5 #include <queue>
 6 #include <iostream>
 7 #include <mutex>
 8 #include <random>
 9 #include <thread>
10 
11 template <typename T>
12 class Monitor{
13 public:
14     void lock() const {
15         monitMutex.lock();
16     }
17     void unlock() const {
18         monitMutex.unlock();
19     }
20     
21     void notify_one() const noexcept {
22         monitCond.notify_one();
23     }
24     void wait() const {
25         std::unique_lock<std::recursive_mutex> monitLock(monitMutex);
26         monitCond.wait(monitLock);
27     }
28     
29 private:
30     mutable std::recursive_mutex monitMutex;
31     mutable std::condition_variable_any monitCond;
32 };
33 
34 template <typename T>
35 class ThreadSafeQueue: public Monitor<ThreadSafeQueue<T>>{
36 public:
37     void add(T val){ 
38         derived.lock();
39         myQueue.push(val);
40         derived.unlock();
41         derived.notify_one();
42     } 
43     
44     T get(){ 
45         derived.lock();
46         while (myQueue.empty()) derived.wait();
47         auto val = myQueue.front();
48         myQueue.pop();
49         derived.unlock();
50         return val;
51     }
52 private:
53     std::queue<T> myQueue;
54     ThreadSafeQueue<T>& derived = static_cast<ThreadSafeQueue<T>&>(*this);
55 };
56 
57 class Dice{
58 public:
59     int operator()(){ return rand(); }
60 private:
61     std::function<int()> rand = std::bind(std::uniform_int_distribution<>(1, 6), 
62                                           std::default_random_engine());
63 };
64 
65 
66 int main(){
67     
68     std::cout << std::endl;
69     
70     constexpr auto NUM = 100;
71     
72     ThreadSafeQueue<int> safeQueue;
73     auto addLambda = [&safeQueue](int val){ safeQueue.add(val); };
74     auto getLambda = [&safeQueue]{ std::cout << safeQueue.get() << " " 
75                                    << std::this_thread::get_id() << "; "; };
76         
77     std::vector<std::thread> addThreads(NUM);
78     Dice dice;
79     for (auto& thr: addThreads) thr = std::thread(addLambda, dice() );
80     
81     std::vector<std::thread> getThreads(NUM);
82     for (auto& thr: getThreads) thr = std::thread(getLambda);
83 
84     for (auto& thr: addThreads) thr.join();
85     for (auto& thr: getThreads) thr.join();
86     
87     std::cout << "\n\n";
88      
89 }
```

Monitor Object

The central idea of the example is that the Monitor Object is encapsulated in a class and can, therefore, be reused. The class `Monitor` uses [`std::recursive_mutex`](#chap06.xhtml_textXXXmutexZZZrecursive_mutexZZZtimed_mutexZZZrecursive_timed_mutex) as monitor lock and [`std::condition_variable_any`](#chap06.xhtml_textXXXcondition_variable_any) as monitor condition. In contrast to [`std::condition_variable`](#chap06.xhtml_chapterXXXConditionSSSVariablesZZZcondition_variable), [`std::condition_variable_any`](#chap06.xhtml_textXXXcondition_variable_any) accepts a recursive mutex. Both are declared as `mutable` and can, therefore, be used in constant methods. The class `Monitor` provides the minimal interface which a Monitor Object should support.

`ThreadSafeQueue` in line 34 - 55 extends the `std::queue` in line 53 with a thread-safe interface. `ThreadSafeQueue` derives from the class `Monitor` and uses its methods to support the synchronised methods `add` and `get`. The methods `add` and `get` use the monitor lock to protect the Monitor Object and in particular the non-thread-safe `myQueue`. `add` notifies the waiting thread when a new item was added to `myQueue`. This notification is thread-safe. Deriving a class such as `ThreadSafeQueue` from a base class which has the same class as template parameter is a typically used idiom in C++ and called [CRTP](#chap14.xhtml_textXXXCRTPZZZCuriouslySSSRecurringSSSTemplateSSSPattern): `class ThreadSafeQueue: public Monitor<ThreadSafeQueue<T>>`. The key observation to understand this idiom is line 54: `ThreadSafeQueue<T>& derived = static_cast<ThreadSafeQueue<T>&>(*this)`. This expression downcast the `this`-pointer to the derived class. The Monitor Object `safeQueue` line 72 uses the lambda-function in line 73 and 74 to add a number or remove a number from the synchronised `safeQueue`. `ThreadSafeQueue` itself is a class template and can hold values from an arbitrary type. 100 clients add 100 random numbers between 1 - 6 to the `safeQueue` (line 77) while 100 clients remove these 100 numbers concurrently from the `safeQueue`. The output of the program shows the numbers and the ids of the used threads.

![Monitor Object](images/ArchitecturePatterns----monitorObject.png)

Monitor Object

The [Active Object](#chap14.xhtml_chapterXXXActiveSSSObject) and the Monitor Object are similar but distinct in a few important points. Both architectural patterns synchronise the access to a shared object. The methods of an Active Object are executed in a different thread, but the methods of an Monitor Object in the same thread. The Active Object decouples it’s method invocation better from its method execution and is, therefore, easier to maintain.

#### Further Information

*   [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

### Half-Sync/Half-Async

The Half-Sync/Half-Async architectural pattern decouples asynchronous and synchronous service processing in concurrent systems, to simplify programming without unduly reducing performance. The pattern introduces two intercommunicating layers, one for asynchronous and one for synchronous service processing.

![Half-Sync/Half-Async](images/ArchitecturePatterns----HalfSyncAsync.jpg)

Half-Sync/Half-Async

The Half-Sync/Half-Async pattern is often used in event-loops of servers or graphical user interfaces. The typical workflow of the event-loop is to accept the client or user event, insert the request into a queue and process the request synchronously in a separate thread. Accepting requests asynchronously ensures efficiency and the synchronous processing simplifies the processing of the request. The asynchronous and the synchronous service layers are decomposed into two layers and the queue coordinates between both. The asynchronous layer consists of the lower-level system services such as interrupts, whereas the synchronous layer of high-level services such as database queries, or file manipulations. The asynchronous and the synchronous layer can talk to each other via the queueing layer.

#### Advantages and Disadvantages

What are the advantages and disadvantages of the Half-Sync/Half-Async pattern?

*   Advantages:
    *   A clear separation of asynchronous and synchronous services. Low-level system services are handled in the asynchronous and high-level services are handled in the synchronous layer.
    *   The queueing layer ensures the loose coupling of the asynchronous and the synchronous layer.
    *   The clear separation makes the software easier to understand, debug, maintain, and extend.
    *   Blocking in the synchronous services does not affect the asynchronous services.
*   Disadvantages:
    *   The boundary-crossing between the asynchronous and synchronous layer may cause overhead. Often, the boundary-crossing involves a context switch between the kernel-space and the user-space because the asynchronous services run typically in the kernel-space and the synchronous services in the user-space.
    *   The strict separation of the layers requires that the data is either copied or is immutable

The Half-Sync/Half-Async pattern is typically used in an event demultiplexing and dispatching frameworks such as the Reactor or Proactor pattern.

#### Reactor

The Reactor pattern is an event-driven framework to demultiplex and dispatch service requests concurrently onto various service providers. The Reactor pattern is also known as dispatcher or notifier.

##### Requirements

The server should handle more client requests concurrently. Each client request has a unique identifier, which enables the mapping to the specific service provider. The following points must hold. The Reactor should

*   not block.
*   support maximum throughput, avoid unnecessary context switches, and, therefore, the copying or synchronisation of data.
*   be easily expandable to support improved or new services.
*   don’t use complex synchronisation mechanisms.

##### Solution

For each supported service type implement an event handler which fulfils the specific client request. Register this service handler within the Reactor. The Reactor uses an event demultiplexer to wait synchronously on all incoming events. When an event arrives, the Reactor is notified and dispatches it to the specific service.

##### Components

![Reactor](images/ArchitecturePatterns----Reactor.jpg)

Reactor

*   **Handles**:
    *   The handles identify different event sources such as network connections, open files, or GUI events.
    *   The event source generates events such as connect, read, or write which are queued on the associated handle.
*   **Synchronous event demultiplexer**:
    *   The synchronous event demultiplexer waits for one or more indication events. It blocks until the associated handle can process the event.
*   **Event handler**:
    *   The event handler defines the interface for processing the indication events.
    *   The event handler defines the supported services of the application.
*   **Concrete event handler**.
    *   The concrete event handler implements the interface of the application defined by the event handler.
*   **Reactor**:
    *   The Reactor supports an interface to register and deregister the concrete event handler.
    *   The Reactor uses the synchronous event demultiplexer such as the system calls [`select`](https://en.wikipedia.org/wiki/Select_(Unix)), [`epoll`](https://en.wikipedia.org/wiki/Epoll), or [`WaitForMultipleObjects`](https://docs.microsoft.com/en-us/windows/desktop/api/synchapi/nf-synchapi-waitformultipleobjects) to wait for indication events.
    *   The Reactor maps the events to their concrete event handler.
    *   The Reactor manages the lifetime of the event loop.

The Reactor (and not the application) waits for the indication events to demultiplex and dispatch the event. The concrete event handlers are registered within the Reactor. The Reactor inverts the flow of control. The Reactor (and not the application) waits for the indication events and calls the concrete event handler. This inversion of control is often called [Hollywood principle](https://en.wikipedia.org/wiki/Inversion_of_control).

The following code snippet shows the event-loop of the C++ framework [The ADAPTIVE Communication Environment (ACE)](https://www.dre.vanderbilt.edu/~schmidt/ACE.html).

```
 1 // CTRL c
 2 SignalHandler *mutateTimer1= new SignalHandler( timerId1 );
 3 
 4 // CTRL z
 5 SignalHandler *mutateTimer2= new SignalHandler( timerId2 );
 6 
 7 ACE_Reactor::instance()->register_handler( SIGINT, mutateTimer1); 
 8 ACE_Reactor::instance()->register_handler( SIGTSTP, mutateTimer2);
 9 
10 
11 // "run" the timer.
12 Timer::instance ()->wait_for_event ();
```

Event-loop of ACE

Line 2 and 5 define signal handlers for the keyboard events `CTRL c` and `CTRL z`. The lines 7 and 8 register them. The event-loop starts in line 12.

##### Advantages and Disadvantages

What are the advantages and disadvantages of the reactor pattern?

*   Advantages:
    *   A clear separation of framework and application logic.
    *   The modularity of various concrete event handler.
    *   The separation of interface and implementation enables easy adaption or extension of the services.
    *   Overall structure supports the concurrent execution.
*   Disadvantages:
    *   Requires an event demultiplexing system-call.
    *   Long-running event handler can block the Reactor.
    *   The inversion of control makes testing and debugging more difficult.

The Half-Sync/Half-Async pattern is typically used in the Reactor pattern to answer client requests in a separate thread.

The Proactor pattern is the asynchronous variant of the reactor pattern. The Reactor pattern demultiplexes and dispatches its event handler synchronously but the Proactor pattern asynchronously.

#### Proactor

The Proactor pattern enables event-driven applications to demultiplex and dispatch service requests, which are triggered by the completion of an asynchronous operation.

##### Requirements

The performance of event-driven applications such as servers can often be improved by processing multiple service request asynchronously. To achieve this performance, event-driven applications must process multiple events synchronously, avoid expensive data synchronisation or context switching. Further, the new or improved services should be easily integrated, and application should be shielded from the multi-threading and synchronisation challenges.

##### Solution

Split the application services into two parts: long-duration operations which should run asynchronously and completion handlers which process the result of the long-duration asynchronous operations. The processing of the completion handler is quite similar to the processing of the event handler in the [Reactor pattern](#chap14.xhtml_chapterXXXReactor), but the asynchronous operation is typically the job of the operating system. As the [Reactor pattern](#chap14.xhtml_chapterXXXReactor), the Proactor pattern defines an event loop.

Here is the unique part of the Proactor pattern compared to the [Reactor pattern](#chap14.xhtml_chapterXXXReactor). An asynchronous operation such as a connection request is initiated, and the operation is performed without blocking the caller’s thread. When the long-duration operation is done it puts a completion event into the completion event queue. The Proactor waits on the queue by using the asynchronous event demultiplexer. The asynchronous event demultiplexer removes completion events from the queue, and the Proactor dispatches it to the specific completion handler. This completion handler processes the result of the asynchronous operation.

##### Components

The Proactor consists of nine components.

![Proactor](images/ArchitecturePatterns----Proactor.png)

Proactor

*   **Handle**:
    *   stands for an entity of the operating system such as a socket, that can generate a completion event
*   **Asynchronous operation**:
    *   is typically a long-duration operation that is executed asynchronously. This can be a read or a write operation on a socket.
*   **Asynchronous operation processor**:
    *   executes an asynchronous operation and enqueues a completion event on the completion event queue when done
*   **Completion handler**:
    *   defines an interface for processing results of asynchronous operations
*   **Concrete completion handler**:
    *   processes the results of the asynchronous operations in an application-specific way
*   **Completion event queue**:
    *   buffers completion events until the asynchronous event demultiplexer dequeues them
*   **Asynchronous event demultiplexer**:
    *   can block while waiting for completion events to occur on a completion event queue
    *   removes the completion event from the completion event queue
*   **Proactor**:
    *   calls the asynchronous event demultiplexer to dequeue a completion event
    *   demultiplexes and dispatches completion events and invokes the concrete completion handler
*   **Initiator**:
    *   invokes the asynchronous operation
    *   it interacts with the asynchronous operation processor

##### Advantages and Disadvantages

What are the advantages and disadvantages of the Proactor pattern?

*   Advantages:
    *   The application separates the application-independent asynchronous functionality from the application-specific functionality.
    *   The interface of the Proactor can be used on various operating systems supporting different asynchronous event demultiplexer.
    *   Applications do not need to start new threads because the long-duration asynchronous operations run in the caller’s thread.
    *   The Proactor pattern can avoid the cost of context switching.
    *   The application logic doesn’t start any threads and, therefore, no synchronisation is necessary.
*   Disadvantages:
    *   To apply the Proactor pattern most efficiently, the operating system should support asynchronous operations.
    *   Due to the separation in time and space between the operation initiation and completion, it is quite difficult to debug or test the program.
    *   The invocation of the asynchronous operation and maintaining of the completion event requires memory.

#### Further Information

*   [Adaptive Communication Environment (ACE)](https://en.wikipedia.org/wiki/Adaptive_Communication_Environment)
*   [Boost.Asio](https://www.boost.org/doc/libs/1_69_0/doc/html/boost_asio.html)
*   [Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects](https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/)

## Best Practices

This chapter provides you with a simple set of rules for writing well-defined and fast, concurrent programs in modern C++. Multithreading, and in particular parallelism and concurrency, is quite a new topic in C++; therefore, more and more best practices are discovered in the coming years. Consider the rules in this chapter not as a complete list; but rather as a necessary starting point that evolves over time. This holds particularly true for the parallel STL. At the time of updating this book (12/2018), the parallel algorithms of C++17 are only partially available; therefore, it is too early to formulate best practices for it.

### General

Let’s start with a few very general best practices that applies to atomics and threads.

#### Code Reviews

Code reviews should be part of each professional software development process. This holds especially true when you deal with concurrency. Concurrency is inherently complicated and requires a lot of thoughtful analysis and experience.

To make the review most effective, send the code you want to discuss to the reviewers before the review. Explicitly state which invariants should apply to your code. The reviewers should have enough time to analyse the code before the official review starts.

Not convinced? Let me give you an example. Do you remember the [data races](#chap20.xhtml_chapterXXXDataSSSRaces) in the program `readerWriterLock.cpp` in the chapter [`std::shared_lock`](#chap06.xhtml_chapterXXXshared_lock)?

```
 1 // readerWriterLock.cpp
 2 
 3 #include <iostream>
 4 #include <map>
 5 #include <shared_mutex>
 6 #include <string>
 7 #include <thread>
 8 
 9 std::map<std::string,int> teleBook{{"Dijkstra", 1972}, {"Scott", 1976}, 
10                                    {"Ritchie", 1983}};
11 
12 std::shared_timed_mutex teleBookMutex;
13 
14 void addToTeleBook(const std::string& na, int tele){
15   std::lock_guard<std::shared_timed_mutex> writerLock(teleBookMutex);
16   std::cout << "\nSTARTING UPDATE " << na;
17   std::this_thread::sleep_for(std::chrono::milliseconds(500));
18   teleBook[na]= tele;
19   std::cout << " ... ENDING UPDATE " << na << std::endl;
20 }
21 
22 void printNumber(const std::string& na){
23   std::shared_lock<std::shared_timed_mutex> readerLock(teleBookMutex);
24   std::cout << na << ": " << teleBook[na];
25 }
26 
27 int main(){
28 
29   std::cout << std::endl;
30 
31   std::thread reader1([]{ printNumber("Scott"); });
32   std::thread reader2([]{ printNumber("Ritchie"); });
33   std::thread w1([]{ addToTeleBook("Scott",1968); });
34   std::thread reader3([]{ printNumber("Dijkstra"); });
35   std::thread reader4([]{ printNumber("Scott"); });
36   std::thread w2([]{ addToTeleBook("Bjarne",1965); });
37   std::thread reader5([]{ printNumber("Scott"); });
38   std::thread reader6([]{ printNumber("Ritchie"); });
39   std::thread reader7([]{ printNumber("Scott"); });
40   std::thread reader8([]{ printNumber("Bjarne"); });
41 
42   reader1.join();
43   reader2.join();
44   reader3.join();
45   reader4.join();
46   reader5.join();
47   reader6.join();
48   reader7.join();
49   reader8.join();
50   w1.join();
51   w2.join();
52 
53   std::cout << std::endl;
54 
55   std::cout << "\nThe new telephone book" << std::endl;
56   for (auto teleIt: teleBook){
57     std::cout << teleIt.first << ": " << teleIt.second << std::endl;
58   }
59 
60   std::cout << std::endl;
61 
62 }
```

Reader-writer locks

The issue is that the call `teleBook[na]` is line 24 can modify the telephone book. You can provoke the data race by putting the reading thread `reader8` in front of the other readers. I use this program in my C++ seminars as a kind of an exercise. The exercise is to spot the data race. About 10% of the participants find the data race within 5 minutes.

#### Minimise Sharing of Mutable Data

You should minimise data sharing of mutable data for two reasons: performance and safety. Safety is mainly about [data races](#chap20.xhtml_chapterXXXDataSSSRaces). Let me focus on performance in this paragraph. I deal with correctness in the following best practices section.

In the chapter [Calculating the Sum of a Vector](#chap09.xhtml_chapterXXXCalculatingSSStheSSSSumSSSofSSSaSSSVector) I made a exhaustive performance study. How fast can I sum up the values of a `std::vector`?

This was the key part of the single threaded summation.

```
...

constexpr long long size = 100000000;

std::cout << std::endl;

std::vector<int> randValues;
randValues.reserve(size);

// random values
std::random_device seed;std::mt19937 engine(seed());
std::uniform_int_distribution<> uniformDist(1, 10);

const unsigned long long sum = std::accumulate(randValues.begin(), 
                                               randValues.end(), 0);

...
```

Single threaded summation

Afterwards, I performed the summation on four threads. I started naively with a shared summation variable.

```
...

void sumUp(unsigned long long& sum, const std::vector<int>& val, 
           unsigned long long beg, unsigned long long end){
    for (auto it = beg; it < end; ++it){
        std::lock_guard<std::mutex> myLock(myMutex);
        sum += val[it];
    }
}

...
```

Multi threaded summation with a shared variable

Optimised a little bit by using an atomic summation variable.

```
...

void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val, 
           unsigned long long beg, unsigned long long end){
    for (auto it = beg; it < end; ++it){
        sum.fetch_add(val[it]);
    }
}

...
```

Multi threaded summation with an atomic

And I got my performance improvement by calculating the partial sums locally.

```
...

void sumUp(unsigned long long& sum, const std::vector<int>& val, 
           unsigned long long beg, unsigned long long end){
    unsigned long long tmpSum{};
    for (auto i = beg; i < end; ++i){
        tmpSum += val[i];
    }
    std::lock_guard<std::mutex> lockGuard(myMutex);
    sum += tmpSum;
}

...
```

Multi threaded summation with local variables

The performance numbers are quite impressing and give a clear indication. The less you share state, the more you get out of your cores.

Performance of the variuous summations on Linux

| **Single threaded** | **std::lock_guard** | **Atomics** | **Local summation** |
| --- | --- | --- | --- |
| 0.07 sec | 3.34 sec | 1.34 sec | 0.03 sec |

#### Minimise Waiting

You may have heard of [Amdahl’s law](https://en.wikipedia.org/wiki/Amdahl%27s_law). It predicts the theoretical maximum speedup you can get using multiple processors. The law is quite simple. If p is the proportion of your code, that can run concurrently, you get a maximum speedup of ![ \frac{1}{1-p} ](images/leanpub_equation_0.png). So, if 90% of your code can run concurrently, you get at most a 10 times speedup: ![ \frac{1}{1-p} == \frac{1}{1-0.9} == \frac{1}{0.1} == 10 ](images/leanpub_equation_1.png).

To see it from the opposite perspective; if 10% of your code has to run sequentially because you use a lock, you get at most a ten times speedup. Of course, I assumed that you have access to infinite processing resources.

The graphic shows a direct consequence of Amdahl’s law explicitly.

![By Daniels220 at English Wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=6678551](images/BestPractices----amdahl.png)

By Daniels220 at English Wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=6678551

The optimum number of cores depends highly on the parallel portion of your code. For example: If you have 50% parallel code, you reach the peak performance with 16 cores. Using more cores makes your program not faster. If you have 95% parallel code, you reach the peak performance with 2048 cores.

#### Prefer Immutable Data

A data race is a situation, in which at least two threads access a shared variable at the same time. At least one thread tries to modify the variable. The definition makes it quite obvious. A necessary condition for a data race is mutable, shared state. The graphic makes my point clear.

![Mutable and shared state](images/BestPractices----MutableShared.png)

Mutable and shared state

If you have immutable data, no data race can happen. You only have to guarantee that the immutable data are initialised in a thread-safe way. I presented in the chapter [Thread-safe initialisation](#chap06.xhtml_chaperXXXThreadSSSSafeSSSInitialization) four ways to guarantee this. Here are they:

*   early initialisation before a thread is created
*   constant expressions
*   the function `std::call_once` in combination with the flag `std::once_flag`
*   a static variable with block scope

Their are two typically ways to create immutable data in C++: `const` and `constexpr`. While `const` is a runtime technique, `constexpr` guarantees that the value is initialised at compile time and, therefore, thread-safe. Even user-defined types can be initialized at compile time.

##### A User-defined Type

There are a few restrictions for user-defined types which instances should be created at compile time.

The `constexpr` constructor

*   can only be invoked with a constant expression.
*   can not use exception handling.
*   has to be declared as `default` or `delete` or the function body must be empty (C++11).

The `constexpr` user-defined type

*   can not have virtual base classes.
*   requires that each base object and each non-static member has to be initialised in the initialisation list of the constructor or directly in the class body. Consequently, it holds that each used constructor (e.g. of a base class) has to be `constexpr` constructor and that the applied initialisers have to be constant expressions.

[cppreference.com](https://en.cppreference.com/w/cpp/language/constexpr) provides additional information to `constexpr` user-defined types. To add praxis to the theory, I define the class `MyInt`. `MyInt` shows the just mentioned points. The class has also `constexpr` methods.

```
 1 // userdefinedTypes.cpp
 2 
 3 #include <iostream>
 4 #include <ostream>
 5 
 6 class MyInt{
 7 public:
 8     constexpr MyInt()= default;
 9     constexpr MyInt(int fir, int sec): myVal1(fir), myVal2(sec){}
10     MyInt(int i){
11         myVal1= i - 2;
12         myVal2= i + 3;
13     }
14   
15     constexpr int getSum() const { return myVal1 + myVal2; }
16   
17     friend std::ostream& operator<< (std::ostream &out, const MyInt& myInt){
18         out << "(" << myInt.myVal1 << "," << myInt.myVal2 << ")";  
19         return out;
20      }
21 
22 private:
23     int myVal1= 1998;
24     int myVal2= 2003;
25 
26 };
27 
28 int main(){
29   
30     std::cout << std::endl;
31   
32     constexpr MyInt myIntConst1;
33   
34     constexpr int sec = 2014;
35     constexpr MyInt myIntConst2(2011, sec);
36     std::cout << "myIntConst2.getSum(): " << myIntConst2.getSum() << std::endl;
37   
38     int arr[myIntConst2.getSum()];
39     static_assert( myIntConst2.getSum() == 4025, "2011 + 2014 should be 4025" );
40   
41     std::cout << std::endl;
42   
43 }
```

Immutable user-defined types

The class `MyInt` has two `constexpr` constructors. A default constructor (line 8) and a constructor taking two arguments (line 9). Additionally, the class has two methods, but only the method `getSum` is a constant expression. I declared the method `const` because a `constexpr` method is in contrast to C++11 with C++14 not automatically `const`. There are two ways to define the variables `myVal1` and `myVal2` (lines 23 and 24) if I want to use them in `constexpr` objects. First, I can initialise them in the initialisation list of the constructor (line 9); second, I can initialise them in the class body (lines 23 and 24). The initialisation in the initialisation list of the constructor has the higher priority.

The lines 38 and 39 shows that I can invoke the `constexpr` method in a constant expression. This is the output of the program.

![Using a `constexpr` object](images/BestPractices----userdefinedTypes.png)

Using a `constexpr` object

I want to emphasise it once more explicitly: **A `constexpr` object can only use `constexpr` methods.**

Functional programming languages such as Haskell, having no mutable data, are very suitable for concurrent programming.

#### Use pure functions

Haskell is called a pure functional language because it is based on pure functions. A pure function is a function which always produces the same results when given the same arguments. It has no side effect and can, therefore, not change the state of the program.

Pure functions have a significant advantage from the concurrency perspective. They can be reordered or automatically run on another thread.

Functions in C++ are per default impure. The following three functions are all pure, but each function has a different characteristic.

```
int powFunc(int m, int n){
    if (n == 0) return 1;
    return m * powFunc(m, n-1);
}
```

`powFunc` is an ordinary function that runs at runtime.

```
template<int m, int n>
struct PowMeta{
    static int const value = m * PowMeta<m, n-1>::value;
};

template<int m>
struct PowMeta<m, 0>{
    static int const value = 1;
};
```

`PowMeta` is a so-called meta-function because it runs at compile time.

```
constexpr int powConst(int m, int n){
    int r = 1;
    for(int k = 1; k <= n; ++k) r *= m;
    return r;
}
```

The function `powCont` can run at runtime and at compile time. It is a `constexpr` function.

#### Look for the Right Abstraction

There are various ways to [initialise a Singleton in a multithreading environment](#chap09.xhtml_chapterXXXThreadMMMSafeSSSInitialisationSSSofSSSaSSSSingelton). You can rely on the standard library using a `lock_guard` or `std::call_once`, rely on the core language using a static variable, or rely on atomics using acquire-release semantic. The acquire-release semantic is by far the most challenging one. It’s a big challenge in various aspects. You have to implement it, to maintain it, and explain it to your coworkers. In contrast to your effort, the well-known [Meyers Singleton](#chap09.xhtml_textXXXMeyersSSSSingleton) is a lot easier to implement and runs faster.

The story with the right abstractions goes on. Instead of implementing a parallel loop for summing up a container, use [`std::reduce`](#chap15.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduce). You can parametrise `std::reduce` with a [binary callable](#chap23.xhtml_glossaryXXXCallableSSSUnitZZZcallableSSSBOBOBOGlossaryBCBCBC) and the parallel [execution policy](#chap15.xhtml_chapterXXXExecutionSSSPoliciesZZZparallelOOOseqZZZparallelOOOparZZZparallelOOOpar_unseq).

The more you go for the right abstraction, the less likely it becomes that you shoot yourself in the foot.

#### Use Static Code Analysis Tools

In the chapter on case studies, I introduced [CppMem](#chap15.xhtml_chapterXXXCppMemSSSMMMSSSAnSSSOverview). [CppMem](http://svr-pes20-cppmem.cl.cam.ac.uk/cppmem/) is an interactive tool for exploring the behaviour of small code snippets using the C++ memory model. CppMem can help you in two aspects. First, you can verify the correctness of your code. Second, you get a deeper understanding of the memory model and, therefore, of the multithreading issues in general.

#### Use Dynamic Enforcement Tools

[ThreadSanitizer](https://github.com/google/sanitizers/wiki/ThreadSanitizerCppManual) is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) detector for C/C++. ThreadSanitizer is part of Clang 3.2 and GCC 4.8\. To use ThreadSanitizer, you have to compile and link your program using the flag `-fsanitize=thread`.

The following program has a data race.

```
 1 // dataRace.cpp
 2 
 3 #include <thread>
 4 
 5 int main(){
 6   
 7   int globalVar{};
 8 
 9   std::thread t1([&globalVar]{ ++globalVar; });
10   std::thread t2([&globalVar]{ ++globalVar; });
11 
12   t1.join();
13   t2.join();
14   
15 }
```

A data race on globalVar

`t1` and `t2` access `globalVar` at the same time. Both threads try to modify the `globalVar`. Let’s compile and run the program.

```
g++ -std=c++11 dataRace.cpp -fsanitize=thread  -pthread -g -o dataRace
```

The output of the program is quite verbose.

![A data race detected with ThreadSanitizer](images/BestPractices----dataRace.png)

A data race detected with ThreadSanitizer

I highlighted in red the critical line of the screenshot. There is a data race on line 10.

### Multithreading

#### Threads

Threads are the basic building blocks for writing concurrent programs.

##### Minimise thread creation

How expensive is a thread? Quite expensive! This is the issue behind this best practice. Let me first talk about the usual size of a thread and than about the costs of its creation.

###### Size

A `std::thread is a thin wrapper around the native thread. This means I’m interested in the size of a Windows thread and a [POSIX thread](https://en.wikipedia.org/wiki/POSIX_Threads) because most of the times they are internally used.

*   Windows systems: the post [Thread Stack Size](https://msdn.microsoft.com/en-us/library/windows/desktop/ms686774(v=vs.85).aspx) gave me the answer: 1 MB.
*   POSIX systems: the [pthread_create](http://man7.org/linux/man-pages/man3/pthread_create.3.html) man-page provides me with the answer: 2MB. This is the sizes for the i386 and x86_64 architectures. If you want to know the sizes for further architectures that support POSIX, here are they:

![Stack size of an `std::thread`](images/BestPractices----threadStackSize.png)

Stack size of an `std::thread`

###### Creation

I didn’t find numbers how much time it takes to create a thread. To get a gut feeling, I made a simple performance test on Linux and Windows.

I used GCC 6.2.1 on a desktop and cl.exe on a laptop for my performance tests. The cl.exe is part of the Microsoft Visual Studio 2017\. I compiled the programs with maximum optimisation. This means on Linux the flag `O3` and on Windows `Ox`.

Here is my small test program.

```
 1 // threadCreationPerformance.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <thread>
 6 
 7 static const long long numThreads= 1'000'000;
 8 
 9 int main(){
10 
11     auto start = std::chrono::system_clock::now();
12 
13     for (volatile int i = 0; i < numThreads; ++i) std::thread([]{}).detach();
14 
15     std::chrono::duration<double> dur= std::chrono::system_clock::now() - start;
16     std::cout << "time: " << dur.count() << " seconds" << std::endl;
17 
18 }
```

A small performance test for thread creation

The program creates 1 million threads which execute the empty lambda function in line 13\. These are the numbers for Linux and Windows:

###### Linux

![Thread creation on Linux](images/BestPractices----threadCreationLinux.png)

Thread creation on Linux

This means that the creation of a thread took about 14.5 sec / 1000000 = **14.5 microseconds on Linux**.

###### Windows

![Thread creation on Windows](images/BestPractices----threadCreationWindows.png)

Thread creation on Windows

The thread creation took about 44 sec / 1000000 = **44 microseconds on Windows**.

To put it the other way around. You can create about **69 thousand threads on Linux and 23 thousand threads on Windows in one second**.

##### Use tasks instead of threads

```
 1 // asyncVersusThread.cpp
 2 
 3 #include <future>
 4 #include <thread>
 5 #include <iostream>
 6 
 7 int main(){
 8 
 9   std::cout << std::endl;
10 
11   int res;
12   std::thread t([&]{ res = 2000 + 11; });
13   t.join();
14   std::cout << "res: " << res << std::endl;             
15 
16   auto fut= std::async([]{ return 2000 + 11; });
17   std::cout << "fut.get(): " << fut.get() << std::endl;   
18 
19   std::cout << std::endl;   
20 
21 }
```

std:async versus threads

Based on the program there are many reasons for preferring tasks over threads. The main reasons are:

*   you can use a safe communication channel for returning the result of the communication. If you use a shared variable, you have to synchronise the access to it.
*   you can quite easily return values, notifications, and exceptions to the caller.

With [extended futures](#chap10.xhtml_chapterXXXExtendedSSSFutures) we get the possibility to compose futures and build highly sophisticated workflows. These workflows are based on the continuation `then`, and the combinations `when_any` and `when_all`.

##### Be extremely careful if you detach a thread

The following code snippet requires our full attention.

```
std::string s{"C++11"}

std::thread t([&s]{ std::cout << s << std::endl; });
t.detach();
```

Because thread `t` is detached from the lifetime of its creator, two [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition) can cause undefined behaviour.

1.  Thread `t` may outlive the lifetime of its creator. The consequence is that `t` refers to a non-existing `std::string`.
2.  The program shuts down before thread `t` can do its work because the lifetime of the output stream `std::cout` is bound to the lifetime of the main thread.

##### Consider using an automatic joining thread

A thread `t` with a [callable unit](#chap15.xhtml_glossaryXXXCallableSSSUnitZZZcallable) is called joinable if neither a `t.join()` nor a `t.detach()` call happened. The destructor of a joinable thread throws the `std::terminate` exception. In order not to forget the `t.join()`, you can create your wrapper around `std::thread`. This wrapper checks in the constructor, if the given thread is still joinable and joins the given thread in the destructor.

You don’t have to build this wrapper by your own. Use the [`scoped_thread`](#chap06.xhtml_textXXXscoped_thread) from Anthony Williams or the `gsl::joining_thread` from the [guideline support library](https://github.com/Microsoft/GSL).

#### Data Sharing

With data sharing of mutable data the challenges in multithreading programming start.

##### Pass data per default by copy

```
std::string s{"C++11"}

std::thread t1([s]{ ... }); // do something with s
t1.join();

std::thread t2([&s]{ ... }); // do something with s
t2.join();

// do something with s
```

If you pass data such as the `std::string s` to a thread `t1` by copy, the creator thread and the created thread `t1` use independent data. This is in contrast to the thread `t2`. It gets its `std::string s` by reference. This means you have to synchronise the access to `s` in the creator thread and the created thread `t2` preventively. This is error-prone and expensive.

##### Use `std::shared_ptr` to share ownership between unrelated threads

Imagine, you have a object which you want to share between unrelated threads. The key question is, who is the owner of the object and, therefore, responsible for releasing the memory? Now you can choose between a memory leak if you don’t deallocate the memory or undefined behaviour because you invoked delete more than once. Most of the times, the undefined behaviour ends in a runtime crash.

The following program shows this non-solvable issue.

```
 1 // threadSharesOwnership.cpp
 2 
 3 #include <iostream>
 4 #include <thread>
 5 
 6 using namespace std::literals::chrono_literals;
 7 
 8 struct MyInt{
 9   int val{2017};
10   ~MyInt(){
11     std::cout << "Good Bye" << std::endl;
12   }
13 };
14 
15 void showNumber(MyInt* myInt){
16     std::cout << myInt->val << std::endl;
17 }
18 
19 void threadCreator(){
20     MyInt* tmpInt= new MyInt; 
21     
22     std::thread t1(showNumber, tmpInt);
23     std::thread t2(showNumber, tmpInt);
24     
25     t1.detach();
26     t2.detach();
27 }
28 
29 int main(){
30     
31     std::cout << std::endl;
32     
33     threadCreator();
34     std::this_thread::sleep_for(1s);
35     
36     std::cout << std::endl;
37     
38 }
```

Unrelated threads share ownership

This example is intentionally easy. I let the main thread sleep for one second (line 34) to be sure that it outlives the lifetime of the child thead `t1` and `t2`. This is, of course, no appropriate synchronisation, but it helps me to make my point. The vital issue of the program is: Who is responsible for the deletion of `tmpInt`in line 20? Thread `t1` (line 22), thread `t2` (line 23), or the function (main thread) itself. Because I can not forecast how long each thread runs I decided to go with a memory leak. Consequentially, the destructor of `MyInt` in line 10 is never called:

![Unrelated threads share ownership](images/BestPractices----threadSharesOwnership.png)

Unrelated threads share ownership

The lifetime issues are quite easy to handle if I use a std::shared_ptr.

![Unrelated threads share ownership via `std::shared_ptr`](images/BestPractices----threadSharesOwnershipSharedPtr.png)

Unrelated threads share ownership via `std::shared_ptr`

```
 1 // threadSharesOwnershipSharedPtr.cpp
 2 
 3 #include <iostream>
 4 #include <memory>
 5 #include <thread>
 6 
 7 using namespace std::literals::chrono_literals;
 8 
 9 struct MyInt{
10   int val{2017};
11   ~MyInt(){
12     std::cout << "Good Bye" << std::endl;
13   }
14 };
15 
16 void showNumber(std::shared_ptr<MyInt> myInt){    
17     std::cout << myInt->val << std::endl;
18 }
19 
20 void threadCreator(){
21     auto sharedPtr = std::make_shared<MyInt>();   
22     
23     std::thread t1(showNumber, sharedPtr);
24     std::thread t2(showNumber, sharedPtr);
25     
26     t1.detach();
27     t2.detach();
28 }
29 
30 int main(){
31     
32     std::cout << std::endl;
33     
34     threadCreator();
35     std::this_thread::sleep_for(1s);
36     
37     std::cout << std::endl;
38     
39 }
```

Unrelated threads share ownership via `std::shared_ptr`

Two small changes to the source code were necessary. First, the pointer in line 21 became a `std::shared_ptr` and second, the function `showNumber` in line 16 takes a smart pointer instead of a plain pointer.

##### Minimise the time holding a lock

If you hold a lock, only one thread can enter the [critical section](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) and make progress.

```
void setDataReadyBad(){
    std::lock_guard<std::mutex> lck(mutex_);
    mySharedWork = {1, 0, 3};
    dataReady = true;
    std::cout << "Data prepared" << std::endl;
    condVar.notify_one();
}                                // unlock the mutex

void setDataReadyGood(){
    mySharedWork = {1, 0, 3};
    {
        std::lock_guard<std::mutex> lck(mutex_);
        dataReady = true;       
    }                           // unlock the mutex
    std::cout << "Data prepared" << std::endl;
    condVar.notify_one();
}
```

The functions `setDataReadyBad` and `setDataReadyGood` are the notification components of a [condition variable](#chap15.xhtml_chapterXXXConditionSSSVariables). The variable `dataReady` is necessary to protect against [spurious wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) and [lost wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup). Because `dataReady` is a non-atomic variable, it has to be synchronised using the lock `lck`. To make the lifetime of the lock as short as possible, use an artificial scope (`{ ... }`) such as in the function `setDataReadyGood`.

##### Put a mutex into a lock

You should not use a mutex without a lock.

```
std::mutex m;
m.lock();
// critical section
m.unlock();
```

Something unexpected may happen in the critical section, or you forget to unlock the mutex: the result is the same. If you don’t unlock a mutex, another thread requiring the mutex is blocked and you end with a [deadlock](#chap20.xhtml_chapterXXXDeadlocks).

Thanks to locks that automatically take care of the underlying mutex, your risk of getting a deadlock is considerably reduced. According to the [RAII](#chap23.xhtml_glossaryXXXRAIISSSBOBOBOGlossaryBCBCBC) idiom, a lock automatically binds its mutex in the constructor and releases it in the destructor.

```
{
  std::mutex m,
  std::lock_guard<std::mutex> lockGuard(m);
  // critical section
}          // unlock the mutex
```

The artificial scope (`{ ... }`) ensures that the lifetime of the lock automatically ends; therefore, the underlying mutex is unlocked.

##### Try to lock at most one mutex at one point in time

Of course, sometimes you need more than one mutex at one point in time. In this case, you may become the victim of a [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition) which causes a [deadlock](#chap20.xhtml_chapterXXXDeadlocks) such as in the following chapter; therefore, you should try to avoid holding more than one mutex at one point in time if possible.

##### Give your locks a name

If you use a lock such as `std::lock_guard` without a name, it will be immediately destroyed.

```
{
    std::mutex m,
    std::lock_guard<std::mutex>{m};
    // critical section
} 
```

In this innocent looking code snippet, the [`std::lock_guard`](#chap06.xhtml_chapterXXXlock_guard) is immediately destroyed. Therefore, the following critical section is executed without synchronisation. The locks from the C++ standard follow all the same pattern. They lock its mutex and its constructor and unlock it in its destructor. This pattern is called [RAII](#chap15.xhtml_glossaryXXXRAIIBOBOBOGlossaryBCBCBC).

The following example shows the surprising behaviour:

```
 1 // myGuard.cpp
 2 
 3 #include <mutex>
 4 #include <iostream>
 5 
 6 template <typename T>
 7 class MyGuard{
 8   T& myMutex;
 9   public:
10     MyGuard(T& m):myMutex(m){
11       myMutex.lock();
12 	  std::cout << "lock" << std::endl;
13     }
14     ~MyGuard(){
15 	  myMutex.unlock();
16       std::cout << "unlock" << std::endl;
17     }
18 };
19 
20 int main(){
21 	
22   std::cout << std::endl;
23 	
24   std::mutex m;
25   MyGuard<std::mutex> {m};                        
26   std::cout << "CRITICAL SECTION" << std::endl;   
27   
28   std::cout << std::endl;
29 
30 } 
```

The `MyGuard` calls lock and unlock in its constructor and in its destructor. Because of the temporary, the call to the constructor and destructor happens in line 25\. In particular, this means that the call of the destructor happens at line 25 and not, as usual, in line 31. As consequence, the critical section in line 26 is executed without synchronisation.

This screenshot of the program shows that the output of *unlock* happens before the output of *CRITICAL SECTION*.

![Locks having no name](images/BestPractices----myGuard.png)

Locks having no name

##### Use `std::lock` or `std::scoped_lock` for locking more mutexes atomically

If a thread needs more than one mutex, you have to be extremely careful that you lock the mutex always in the same sequence. If not, a bad interleaving of threads may cause a [deadlock](#chap20.xhtml_chapterXXXDeadlocks).

```
void deadLock(CriticalData& a, CriticalData& b){
  std::lock_guard<std::mutex> guard1(a.mut);
  // some time passes
  std::lock_guard<std::mutex> guard2(b.mut);
  // do something with a and b
}

...

std::thread t1([&]{deadLock(c1,c2);});
std::thread t2([&]{deadLock(c2,c1);});

...
```

Thread `t1` and `t2` need two resources `CriticalData` to perform their job. `CriticalData` has its own mutex `mut` to synchronise the access. Unfortunately, both invoke the function `deadlock` with the arguments `c1` and `c2` in a different sequence. Now we have a race condition. If thread `t1` can lock the first mutex `a.mut` but not the second one `b.mut` because in the meantime thread `t2` locks the second one, we get a deadlock.

Thanks to `std::unique_lock` you can defer the locking of its mutex. The function `std::lock`, which can lock an arbitrary number of mutexes atomically, does the locking.

```
void deadLock(CriticalData& a, CriticalData& b){
  unique_lock<mutex> guard1(a.mut,defer_lock);
  // some time passes
  unique_lock<mutex> guard2(b.mut,defer_lock);
  std::lock(guard1,guard2);
  // do something with a and b
}

...

std::thread t1([&]{deadLock(c1,c2);});
std::thread t2([&]{deadLock(c2,c1);});

...
```

C++17 has a new lock `std::scoped_lock`, which can get an arbitrary number of mutexes and locks them atomically. Now, the workflow becomes even more straightforward.

```
void deadLock(CriticalData& a, CriticalData& b){
   std::scoped_lock(a.mut, b.mut);
   // do something with a and b
}

...

std::thread t1([&]{deadLock(c1,c2);});
std::thread t2([&]{deadLock(c2,c1);});

...
```

##### Never call unknown code while holding a lock

Calling an `unknownFunction` while holding a mutex is a recipe for undefined behaviour.

```
std::mutex m;
{
  std::lock_guard<std::mutex> lockGuard(m);
  sharedVariable= unknownFunction();
}
```

I can only speculate about the `unknownFunction`. If `unknownFunction`

*   tries to lock the mutex `m`, that is undefined behaviour. Most of the times, you get a deadlock.
*   starts a new thread that tries to lock the mutex `m`, you get a deadlock.
*   locks another mutex `m2` you may get a deadlock because you lock the two mutexes `m` and `m2` at the same time.
*   does not directly or indirectly try to lock the mutex `m`; all seems to be okay. “Seems” because your coworker can modify the function or the function is dynamically linked, and you get a different version. All bets are open what may happen.
*   work as expected you may have a performance problem because you don’t know how long the function `unknownFunction` would take.

To solve this issue, use a local variable.

```
auto tempVar = unknownFunction();
std::mutex m, 
{
  std::lock_guard<std::mutex> lockGuard(m);
  sharedVariable = tempVar;
}
```

This additional indirection solves all issues. `tempVar` is a local variable and can, therefore, not be the victim of a data race. This means that you can invoke `unknownFunction` without a synchronisation mechanism. Additionally, the time for holding a lock is reduced to its bare minimum: assigning the value of `tempVar` to `sharedVariable`.

#### Condition Variables

Synchronising threads via notifications is a simple concept, but [condition variables](#chap15.xhtml_chapterXXXConditionSSSVariables) make this task very challenging. The main reason is that a condition variable has no state.

*   If a condition variable gets a notification, it may be the wrong one ([spurious wakeup](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup)).
*   If a condition variable gets its notification before it was ready, the notification is lost ([lost wakeup](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup)).

##### Don’t use condition variables without a predicate

Using a condition variable without a predicate is often a [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition).

```
 1 // conditionVariableLostWakeup.cpp
 2 
 3 #include <condition_variable>
 4 #include <mutex>
 5 #include <thread>
 6 
 7 std::mutex mutex_;
 8 std::condition_variable condVar;
 9 
10 void waitingForWork(){
11     std::unique_lock<std::mutex> lck(mutex_);
12     condVar.wait(lck);                          
13     // do the work
14 }
15 
16 void setDataReady(){
17     condVar.notify_one();                        
18 }
19 
20 int main(){
21 
22   std::thread t1(setDataReady);
23   std::thread t2(waitingForWork);               
24 
25   t1.join();
26   t2.join();
27   
28 }
```

Condition variables without a predicate

If the thread `t1` runs before the thread `t2`, you get a deadlock. `t1` sends its notification before `t2` can accept it. The notification is lost. This happens very often because thread `t1` starts before thread `t2` and thread `t1` has less work to perform.

Adding a bool variable `dataReady` to the workflow solves this issue. `dataReady` also protect against a [spurious wakeup](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) because of the waiting thread checks at first if the notification was from the right thread.

```
 1 // conditionVarialbleLostWakeupSolved.cpp
 2 
 3 #include <condition_variable>
 4 #include <mutex>
 5 #include <thread>
 6 
 7 std::mutex mutex_;
 8 std::condition_variable condVar;
 9 
10 bool dataReady{false};
11 
12 void waitingForWork(){
13     std::unique_lock<std::mutex> lck(mutex_);
14     condVar.wait(lck, []{ return dataReady; });
15     // do the work 
16 }
17 
18 void setDataReady(){
19     {
20       std::lock_guard<std::mutex> lck(mutex_);
21       dataReady = true;
22     }
23     condVar.notify_one();
24 }
25 
26 int main(){
27 
28   std::thread t1(waitingForWork);
29   std::thread t2(setDataReady);
30 
31   t1.join();
32   t2.join();
33   
34 }
```

Condition variables with a predicate

##### Use Promises and Futures instead of Condition Variables

For one-time notifications [promises](#chap06.xhtml_chapterXXXpromise) and [futures](#chap06.xhtml_chapterXXXfuture) are the better choice. The workflow of previous program `conditioVarialbleLostWakeupSolved.cpp` can directly be implemented with a promise and a future.

```
 1 // notificationWithPromiseAndFuture.cpp
 2 
 3 #include <future>
 4 #include <utility>
 5 
 6 void waitingForWork(std::future<void>&& fut){
 7     fut.wait();
 8     // do the work
 9 }
10 
11 void setDataReady(std::promise<void>&& prom){
12     prom.set_value();
13 }
14 
15 int main(){
16 
17   std::promise<void> sendReady;
18   auto fut = sendReady.get_future();
19 
20   std::thread t1(waitingForWork, std::move(fut));
21   std::thread t2(setDataReady, std::move(sendReady));
22 
23   t1.join();
24   t2.join();
25   
26 }
```

Notification with promise and future

The workflow is reduced to its bare minimum. The promise `prom.set_value()` sends the notification the future `fut.wait()` is waiting for. The program needs no mutexes and locks because there is no [critical section](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC). Because no [lost wakeup](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) or [spurious wakeup](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) can happen, a predicate is also not necessary.

If your workflow requires that you use a condition variable many times, then a promise and future pair is no alternative.

#### Promises and Futures

Promises and futures an often be used as an easy-to-use replacement for threads or condition variables.

##### If possible, go for `std::async`

If possible, you should go for `std::async` to execute an asynchronous task.

```
auto fut = std::async([]{ return 2000 + 11; });
// some time passes
std::cout << "fut.get(): " << fut.get() << std::endl;
```

By invoking `auto fut = std::async([]{ return 2000 + 11; })` you say to the C++ runtime: “Run my job”. I don’t care, if is is executed immediately, if it runs on the same thread, if it runs on a thread-pool, if it runs on a [GPU](https://en.wikipedia.org/wiki/Graphics_processing_unit). You are only interested in picking up the result in the future: `fut.get()`.

From a conceptional view, a thread is just an implementation detail for running your job. You only specify *what* should be done and not *how* it should be done.

### Memory Model

The foundation of multithreading is a *well-defined* memory model. Having a basic understanding of the memory helps a lot to get a deeper insight into the multithreading challenges.

#### Don’t use volatile for synchronisation

In C++ `volatile` has no multithreading semantic in contrast to C# or Java. In C# or Java, `volatile` declares an atomic such as `std::atomic` declares an atomic in C++ and is typically used for objects which can change independently of the regular program flow. Due to this characteristic, no optimised storing in caches takes place.

#### Don’t program Lock Free

This advice sounds ridiculous after writing a book about concurrency and having an entire chapter dedicated to the memory model. The reason for this advice is quite simple. Lock-free programming is very error-prone and requires an expert level in this unique domain. In particular, if you want to implement a lock-free data structure, be aware of the [ABA problem](#chap20.xhtml_chapterXXXABA).

#### If you program Lock-Free, use well-established patterns

If you have identified a bottleneck that could benefit from a lock-free solution, apply established patterns.

1.  Sharing an [atomic boolean](#chap05.xhtml_chapterXXXatomicBBBboolEEE) or an atomic counter is straightforward.
2.  Use a thread-safe or even lock-free container to support consumer/producer scenario. If your container is thread-safe, you can put and get values from the container without worrying about synchronisation. You shift the application challenges to the infrastructure.

#### Don’t build your abstraction, use guarantees of the language

[Thread-safe initialisation](#chap05.xhtml_chapterXXXatomicBBBboolEEE) of a shared variable can be done in various ways. You can rely on guarantees of the C++ runtime such as constant expressions, static variables with block scope, or use the function `std::call_once` in combination with the flag `std::once_flag`. We program in C++; therefore, you can build your abstraction based on atomics using even the highly sophisticated acquire-release semantic. Don’t do this in the first place, unless you have to do it. This means if you have identified a bottleneck by measuring the performance of a critical code path; only make the change if you know that your handcrafted version outperforms the default guarantees of the language.

#### Don’t reinvent the wheel

Writing thread-safe data structures is a quite challenging endeavour. Writing lock-free data-structures is way harder; therefore, use existing libraries such as [Boost.Lockfree](http://www.boost.org/doc/libs/1_66_0/doc/html/lockfree.html) or [CDS](http://%20http://libcds.sourceforge.net/).

##### Boost.Lockfree

Boost.Lockfree supports three different data structures:

**Queue**

a lock-free multi-produced/multi-consumer queue

**Stack**

a lock-free multi-produced/multi-consumer stack

**spsc_queue**

a wait-free single-producer/single-consumer queue (commonly known as ring buffer)

##### CDS

CDS stands for Concurrent Data Structures and contains a lot of intrusive (non-owning) and non-intrusive (owning) containers. The containers of the Standard Template Library are non-intrusive because they automatically manage their elements.

*   **Stacks** (lock-free)
*   **Queues** and **priority-queues** (lock-free)
*   **Ordered lists**
*   **Ordered sets** and **maps** (lock-free and lock-based)
*   **Unordered sets** and **maps** (lock-free and lock-based)

# Data Structures

## Lock-Based Data Structures

When threads share a data structure, and the data structure is mutable, you have to protect the data structure from concurrent access. Conceptually, protection can be done from outside or from inside. From outside means that it is in the responsibility of the caller (application) to protect the data. This outside perspective is the perspective, I mainly used in this book until now. Form inside means that the data structure is responsible for protecting itself. A data structure that protects itself so that no [data race](#chap20.xhtml_chapterXXXDataSSSRaces) can appear is called thread-safe. This inside perspective is the perspective, I write about in this and in the next chapter.

I want to emphasise explicitly, I could never have written a book about concurrency without the help of previous authors. This statement holds, in particular, true for the chapters about concurrent data structures. My book is, therefore, heavily influenced by the book [The Art of Multiprocessing Programmming](https://www.oreilly.com/library/view/the-art-of/9780123705914/) by Maurice Herlihy and Nir Shavit and by the book [C++ Concurrency in Action](https://www.manning.com/books/c-plus-plus-concurrency-in-action) by Anthony Williams.

First of all, what are the general consideration you have to keep in mind to design a concurrent data structure?

### General Considerations

Implementing thread-safe data structures is special. Before I dive into each of these special concerns, here is a concise overview including the answers you have to give.

*   **Locking Strategy**: Should the data structure support coarse-grained or fine-grained locking? Coarse-grained locking might be easier to implement but introduces contention.
*   **Granularity of the Interface**: The bigger the interface of the thread-safe data structure, the more difficult becomes it to reason about the concurrent usage of the data structure.
*   **Typical Usage Pattern**: When readers use your data structure mainly, you should not optimise for writers.
*   **Avoidance of Loopholes**: Don’t pass internals of your data structure to clients.
*   **Contention**: Do concurrent client requests seldom or often use your data structure?
*   **Scalability**: How is the performance characteristic of your data structure when the number of concurrent clients increases or the data structure is bounded?
*   **Invariants**: Which invariant must hold for your data structure when used?
*   **Exceptions**: What should happen if an exception occurs?

Of course, these considerations are dependent on each other. For example, using a coarse-grained locking strategy let you easier think about the granularity of the interface and the invariances. In contrast, it may increase the contention on the data structure and breaks scalability.

#### Locking Strategy

Should the data structure support coarse-grained or fine-grained locking? First of all, what do I mean by coarse-grained locking? Coarse-grained locking means that only one thread uses the data structure at one point in time. The [thread-safe interface pattern](#chap13.xhtml_chapterXXXThread-SafeSSSInterfaceSSSBOBOBOPatternBCBCBC) when using one lock is a typical way to implement coarse-grained locking. Here is the straightforward idea of the thread-safe interface pattern.

*   All interface methods (`public`) should use a lock.
*   All implementation methods (`protected` and `private`) must not use a lock.
*   The interface methods call only `protected` or `private` methods but no `public` methods.

The thread-safe interface pattern has two nice properties: all public methods are thread-safe per design and deadlock-free per design. The thread-safe interface is thread-safe, because each `public` method use a lock and the thread-safe interface is deadlock-free, because a `public` method can not invoke another `public` method of the class. I assume, the following implementation makes my point:

```
 1 // threadSafeInterface.cpp
 2 
 3 #include <iostream>
 4 #include <mutex>
 5 #include <thread>
 6 
 7 class Critical{
 8 
 9 public:
10     void interface1() const {
11         std::lock_guard<std::mutex> lockGuard(mut);
12         implementation1();
13     }
14     void interface2(){
15         std::lock_guard<std::mutex> lockGuard(mut);
16         implementation2();
17         implementation3();
18         implementation1();
19     }
20 private: 
21     void implementation1() const {
22         std::cout << "implementation1: " 
23                   << std::this_thread::get_id() << std::endl;
24     }
25     void implementation2(){
26         std::cout << "    implementation2: " 
27                   << std::this_thread::get_id() << std::endl;
28     }
29     void implementation3(){    
30         std::cout << "        implementation3: " 
31                   << std::this_thread::get_id() << std::endl;
32     }
33   
34 
35 mutable std::mutex mut;
36 
37 };
38 
39 int main(){
40     
41     std::cout << std::endl;
42     
43     std::thread t1([]{ 
44         const Critical crit;
45         crit.interface1();
46     });
47     
48     std::thread t2([]{
49         Critical crit;
50         crit.interface2();
51         crit.interface1();
52     });
53     
54     Critical crit;
55     crit.interface1();
56     crit.interface2();
57     
58     t1.join();
59     t2.join();    
60     
61     std::cout << std::endl;
62     
63 }
```

The Thread-Safe Interface

The thread-safe interface pattern sounds promising but also has an obvious drawback. The data structure implementing the thread-safe interface is a bottleneck because only one thread can use the data structure at one point in time. This characteristic means if you have many threads working concurrently on the data structure, you should look for a more fine-grained locking. For example, instead of protection the entire interface to a singly-linked list with one lock, you can use a lock on individual nodes of the singly-linked list.

#### Granularity of the Interface

Imagine, you want to implement a lock-based wrapper `ThreadSafeQueue` for a `std::deque`. The following code snippet gives a rough idea of the `ThreadSafeQueue`.

```
class ThreadSafeQueue{
    ...
public:
    bool empty() const;
    std::shared_ptr<int> pop();
    ...
private:
    std::deque<int> data;
    ...
};
```

For simplicity reasons, I only display the methods `empty` and `pop`. `empty` returns if the `ThreadSafeQueue` is empty and `pop` returns and removes the head of the `ThreadSafeQueue`. The interface has the wrong granularity! Why? Assume that two threads want to perform the following function on the same `threadSafeQueue`.

```
ThreadSafeQueue threadSafeQueue;

std::shared_ptr<int> getHead(){
    if (!threadSafeQueue.empty()){
        auto head = threadSafeQueue.pop();
        return head;
    }
    return std::shared_ptr<int>();
}
...
std::thread t1([&]{ auto res = getHead();
                  ...
                  });
std::thread t2([&]{ auto res = getHead();
                  ...
                  });
```

This code has a [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition) which can cause undefined behaviour. Between the check `!threadSafeQueue.empty()` that the queue is not empty and the removing of the head-element via `threadSafeQueue.pop()`, there is a time window. For example, the following interleaving can happen.

Undefined behaviour with `ThreadSafeQueue`

| **thread t1** | **`thread t2`** |
|   |   |
| (1) `!threadSafeQueue.empty() == true` |   |
|   | (2) `!threadSafeQueue.empty() == true` |
| (3) `auto head = threadSafeQueue.pop();` |   |
|   | (4) `auto head = threadSafeQueue.pop();` |

If `threadSafeQueue` has only one element, the second call `threadSafeQueue.pop()` from thread `t2` has undefined behaviour. Although both methods are thread-safe, the combination of both methods has undefined behaviour. The interface puts the burden to synchronise the access to `threadSafeQueue` on the shoulder of the client. The is far from ideal.

Changing the granularity of the methods on `ThreadSafeQueue` solves this issue quite elegantly. Just combine the two calls `empty` and `pop` into one method.

```
class ThreadSafeQueue{
    ...
public:
    std::shared_ptr<int> tryPop(){
        std::lock_guard<std::mutex> queLock(queMute);
        if (!data.empty()){
            auto head = data.pop();
            return head;
        }
        return std::shared_ptr<int>();
    }
    ...
private:
    std::deque<int> data;
    mutable std::lock_mutex queMutex;
    ...
};
```

#### Typical Usage Pattern

The typical usage pattern for a data structure is the read access. [Reader-writer locks](#chap06.xhtml_chapterXXXshared_lock) allow you to optimise for the read access. When you put a [`std::shared_timed_mutex`](#chap06.xhtml_XXXshared_mutexZZZshared_timed_mutex) into a [`std::shared_lock`](#chap06.xhtml_chapterXXXshared_lock), the lock becomes a shared lock but when you put a [`std::shared_timed_mutex`](#chap06.xhtml_XXXshared_mutexZZZshared_timed_mutex) into a [`std::lock_guard`](#chap06.xhtml_chapterXXXlock_guard) or into a [`std::unique_lock`](#chap06.xhtml_chapterXXXunique_lock), you get a shared lock.

A telephone book is a data structure which is way more often read than modified and is, therefore, the ideal candidate for a reader-writer lock. Let me start with an exclusive lock to have an initial performance number. I have a telephone book with roughly 89,000 entries. Ten threads read all 89,000 names in an arbitrary order, and one thread adds 1 to telephone number of each tenth family name. Of course, all threads run at the same time.

The following image shows you a part of the telephone book. You can see the name/number pairs separated by a colon and the name separated from the number by a comma.

![The initial telephone book](images/DataStructures----telebook.png)

The initial telephone book

The following program crates a `std::unordered_map<std::string, int>` from the file.

```
 1 // exclusiveLockingTelebook.cpp
  2 
  3 #include <chrono>
  4 #include <fstream>
  5 #include <future>
  6 #include <iostream>
  7 #include <mutex>
  8 #include <random>
  9 #include <regex>
 10 #include <shared_mutex>
 11 #include <sstream>
 12 #include <string>
 13 #include <unordered_map>
 14 #include <vector>
 15 
 16 using map = std::unordered_map<std::string, int>;
 17 
 18 class TeleBook{
 19 
 20     mutable std::mutex teleBookMutex;
 21     mutable map teleBook;
 22     const std::string teleBookFile;
 23     
 24 public:
 25     TeleBook(const std::string& teleBookFile_): teleBookFile(teleBookFile_){
 26         auto fileStream = openFile(teleBookFile);
 27         auto fileContent = readFile(std::move(fileStream));
 28         teleBook = createTeleBook(fileContent);
 29         std::cout << "teleBook.size(): " <<  teleBook.size() << std::endl;
 30     }
 31     
 32     map get() const {
 33         std::lock_guard<std::mutex> lockTele(teleBookMutex);
 34         return teleBook;    
 35     }
 36     
 37     int getNumber(const std::string& name) const {
 38         std::lock_guard<std::mutex> lockTele(teleBookMutex);
 39         return teleBook[name];
 40     }
 41     
 42     void setNewNumber(const std::string& name) {
 43         std::lock_guard<std::mutex> lockTele(teleBookMutex);
 44         teleBook[name]++;
 45     }
 46         
 47 private:        
 48 
 49     std::ifstream openFile(const std::string& myFile){                  
 50         std::ifstream file(myFile, std::ios::in);
 51         if ( !file ){
 52             std::cerr << "Can't open file "+ myFile + "!" << std::endl;
 53             exit(EXIT_FAILURE);
 54         }
 55     return file;
 56 }
 57 
 58     std::string readFile(std::ifstream file){                        
 59         std::stringstream buffer;
 60         buffer << file.rdbuf();
 61         return buffer.str();
 62 }
 63 
 64     map createTeleBook(const std::string& fileCont){                 
 65         map teleBook; 
 66     
 67         std::regex regColon(":");
 68         std::sregex_token_iterator fileContIt(fileCont.begin(), fileCont.end(), 
 69                                           regColon, -1);
 70         const std::sregex_token_iterator fileContEndIt;
 71     
 72         std::string entry;
 73         std::string key;
 74         int value;
 75         while (fileContIt != fileContEndIt){
 76             entry = *fileContIt++;
 77             auto comma = entry.find(",");
 78             key = entry.substr(0, comma);
 79             value = std::stoi(entry.substr(comma + 1, entry.length() -1));
 80             teleBook[key] = value;
 81         }
 82         return teleBook;
 83     }
 84 };
 85 
 86 std::vector<std::string> getRandomNames(const map& teleBook){    
 87     
 88     std::vector<std::string> allNames;
 89     for (const auto& pair: teleBook) allNames.push_back(pair.first);
 90     
 91     std::random_device randDev;
 92     std::mt19937 generator(randDev());
 93  
 94     std::shuffle(allNames.begin(), allNames.end(), generator);
 95     
 96     return allNames;
 97 }
 98 
 99 void getNumbers(const std::vector<std::string>& randomNames, TeleBook& teleBook){ 
100     for (const auto& name: randomNames) teleBook.getNumber(name);
101 }
102     
103 int main(){
104 
105     std::cout << std::endl;
106   
107     // get the filename
108     const std::string myFileName = "tele.txt";
109     TeleBook teleBook(myFileName);
110     
111     std::vector<std::string> allNames = getRandomNames(teleBook.get());
112     std::vector<std::string> tenthOfAllNames(allNames.begin(), 
113                                              allNames.begin() + allNames.size()/10);
114     
115     auto start = std::chrono::steady_clock::now();
116     
117     auto futReader0 = std::async(std::launch::async, 
118                                  [&]{ getNumbers(allNames, teleBook); });
119     auto futReader1 = std::async(std::launch::async, 
120                                  [&]{ getNumbers(allNames, teleBook); });
121     auto futReader2 = std::async(std::launch::async, 
122                                  [&]{ getNumbers(allNames, teleBook); });
123     auto futReader3 = std::async(std::launch::async, 
124                                  [&]{ getNumbers(allNames, teleBook); });
125     auto futReader4 = std::async(std::launch::async, 
126                                  [&]{ getNumbers(allNames, teleBook); });
127     auto futReader5 = std::async(std::launch::async, 
128                                  [&]{ getNumbers(allNames, teleBook); });
129     auto futReader6 = std::async(std::launch::async, 
130                                  [&]{ getNumbers(allNames, teleBook); });
131     auto futReader7 = std::async(std::launch::async, 
132                                  [&]{ getNumbers(allNames, teleBook); });
133     auto futReader8 = std::async(std::launch::async, 
134                                  [&]{ getNumbers(allNames, teleBook); });
135     auto futReader9 = std::async(std::launch::async, 
136                                  [&]{ getNumbers(allNames, teleBook); });
137     
138     auto futWriter = std::async(std::launch::async, [&]{ 
139         for (const auto& name: tenthOfAllNames) teleBook.setNewNumber(name); 
140     });
141 
142     futReader0.get(), futReader1.get(), futReader2.get(), futReader3.get(), 
143     futReader4.get(), futReader5.get(), futReader6.get(), futReader7.get(), 
144     futReader8.get(), futReader9.get(), futWriter.get();
145                     
146     std::chrono::duration<double> duration = std::chrono::steady_clock::now() 
147                                              - start;              
148                                              
149     std::cout << "Process time: " << duration.count() << " seconds" << std::endl;
150     
151     std::cout << std::endl;
152     
153 }
```

Exclusive locking on a telephone book

Let me start with the constructor of the class `TeleBook` (lines 25 - 30). It opens the file, reads the content, and creates a telephone book. The function `getRandomNames` (lines 86 - 97) generates an arbitrary permutation of the family names. Each tenth family name goes to the `std::vector` `tenthOfAllNames`. These are the family names, for which the telephone number is modified. Now, to the most interesting lines 117 - 149\. `futReader0` to `futReader9` are the futures, representing ten threads. Each thread reads all family names using the function `getNumbers` in line 99 - 101\. The updating Future `futWriter` performs it job directly in the lambda function (lines 138 - 140). When all futures are done, line 149 displays the overall process time. I want to mention explicitly, that the interface functions (`get`, `getNumber`, and `setNewNumber`) of `TeleBook` use the `std::mutex teleBookMutex` (line 20) for the synchronisation. `teleBookMuex` is `mutable` and can, therefore, be used in a `const` method.

Now, I come to the optimisation step. The methods `get` (lines 32 - 35) and `getNumber` (lines 37 - 40) don’t modify the `telebook` and can, therefore, use a reader-writer lock. Of course, this optimisation can not be applied to the method `setNewNumber` (lines 42 - 45). For simplicity, I only display the interface of the new class `TeleBook` in the optimised program. The other parts of the program are identical.

```
 1 // sharedLockingTelebook.cpp
 2 
 3 ...
 4 
 5 class TeleBook{
 6 
 7     mutable std::shared_timed_mutex teleBookMutex;
 8     mutable map teleBook;
 9     const std::string teleBookFile;
10     
11 public:
12     TeleBook(const std::string& teleBookFile_): teleBookFile(teleBookFile_){
13         auto fileStream = openFile(teleBookFile);
14         auto fileContent = readFile(std::move(fileStream));
15         teleBook = createTeleBook(fileContent);
16         std::cout << "teleBook.size(): " <<  teleBook.size() << std::endl;
17     }
18     
19     map get() const {
20         std::shared_lock<std::shared_timed_mutex> lockTele(teleBookMutex);
21         return teleBook;    
22     }
23     
24     int getNumber(const std::string& name) const {
25         std::shared_lock<std::shared_timed_mutex> lockTele(teleBookMutex);
26         return teleBook[name];
27     }
28     
29     void setNewNumber(const std::string& name) {
30         std::lock_guard<std::shared_timed_mutex> lockTele(teleBookMutex);
31         teleBook[name]++;
32     }
33     
34 private:
35 ...
```

Shared locking on a telephone book

You should not compare the performance of Linux(GCC) with the performance of Windows(cl.exe) because the underlying computers are not comparable. Instead, you should compare the relative performance of exclusive versus shared locking on both platforms. The numbers are quite astonishing.

##### Linux (GCC)

###### Exclusive Locking

![The initial telephone book](images/DataStructures----exclusiveLockingTelebookLinux.png)

The initial telephone book

###### Shared Locking

![The initial telephone book](images/DataStructures----sharedLockingTelebookLinux.png)

The initial telephone book

Exclusive locking is on Linux about 15 % slower than shared locking. This difference is less than I expected because the read/write ratio is 100 to 1.

##### Windows (cl.exe)

###### Exclusive Locking

![The initial telephone book](images/DataStructures----exclusiveLockingTelebookWindows.png)

The initial telephone book

###### Shared Locking

![The initial telephone book](images/DataStructures----sharedLockingTelebookWindows.png)

The initial telephone book

Honestly, the Windows numbers surprised me because shared locking is on Windows two times slower than exclusive locking. It seems that the usage of a `std::shared_lock` and a `std::lock_guard` together with a `std::shared_time_mutex` is a heavyweight operation so that sharing does not pay off.

#### Avoidance of Loopholes

Don’t pass internals of your data structure to clients. Internals can be passed by reference or pointer to the outside world. Passing an arbitrary callable to the data structure opens a loophole, which is difficult challenging to spot.

```
 1 // lockDouble.cpp
 2 
 3 #include <future>
 4 #include <iostream>
 5 #include <mutex>
 6 
 7 class LockDouble{
 8     public:
 9         double get() const {
10             std::lock_guard<std::mutex> lockDoubGuard(lockDoubMutex);
11             return lockDoub;
12         }
13         
14         void set(double val) {
15             std::lock_guard<std::mutex> lockDoubGuard(lockDoubMutex);
16             lockDoub = val;
17         }
18         
19         template <typename Func>
20         void apply(Func func){
21             std::lock_guard<std::mutex> lockDoubGuard(lockDoubMutex);
22             func(lockDoub);
23         }
24     
25 
26     private:
27         double lockDoub{};
28         mutable std::mutex lockDoubMutex;
29     
30 };
31 
32 int main(){
33     
34     LockDouble lck1;
35     
36     auto fut1 = std::async([&lck1]{ lck1.set(20.11); });
37     auto fut2 = std::async([&lck1]{ std::cout << lck1.get() << std::endl; });
38     
39     double* loophole = nullptr;
40     lck1.apply([&loophole](double& d) mutable { loophole = &d; });
41     *loophole = 11.22;
42     
43     auto fut3 = std::async([&lck1]{ std::cout << lck1.get() << std::endl; });
44     
45 }
```

Loophole in the interface

The class `LockDouble` has a clean interface. Each access to the variable `lockDouble` is protected by the same mutex `lockDoubMutex` put into a `std::lock_guard`. The method `get` returns a copy and not a non-const reference to `lockDouble`. If the method `get` would return a non-const reference to `lockDoub`, a client could quite easily produce a [data race](#chap20.xhtml_chapterXXXDataSSSRaces).

```
...
double& get() {
    std::lock_guard<std::mutex> lockDoubGuard(lockDoubMutex);
    return lockDoub;
}
...
LockDouble lck;
lck.set(22.11);
double& d = lck.get();
d = 11.22;
```

Of course, the issue is that the reference `d` can change `lockDoub` which should be protected by the mutex `lockDoubMutex`. I assume this issue was quite easy to detect.

The method `apply` in lines 19 - 23 opens the loophole. I create in line 40 a lambda function which returns a reference to `lockDoub`. The expression `*loophole = 11.22` changes the value of `lockDoub` without synchronisation. Of course, this is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces). The screenshot shows the effects of the non-synchronised access to `lockDoub`.

![Sychronised and unsynchronised access to `lockDoub`](images/DataStructures----lockDouble.png)

Sychronised and unsynchronised access to `lockDoub`

[ThreadSanitizer](https://github.com/google/sanitizers/wiki/ThreadSanitizerCppManual) shows the [data race](#chap20.xhtml_chapterXXXDataSSSRaces) explicitly.

![Data race detection with the Threadsanitizer](images/DataStructures----lockDoubleSanitize.png)

Data race detection with the Threadsanitizer

#### Contention

Do concurrent client requests seldom or often use your data structure? When the contention is low, straightforward synchronisation primitives such as [locks](#chap06.xhtml_chapterXXXLocks) are usually fast enough. Using sophisticated and challenging solutions such as [atomics](#chap05.xhtml_chapterXXXAtomics) could be an overkill. Before you go for the advanced solutions, you should measure. To get an idea, how expensive [locks](#chap06.xhtml_chapterXXXLocks) are, let me make a straightforward test.

Now, I can make it short. I already did this test in the chapter [Calculating the Sum of a Vector](#chap09.xhtml_chapterXXXCalculatingSSStheSSSSumSSSofSSSaSSSVector). I filled a `std::vector` with one hundred million arbitrary but [uniformly distributed](https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)) numbers between 1 and 10\. Then I calculated the sum of the numbers in various ways. Two ways are, in particular, interesting for this section.

##### Single-Threaded Summation without Synchronisation

First, I show the straightforward range-based for loop to calculate the sum.

```
 1 // calculateWithLoop.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 #include <random>
 6 #include <vector>
 7 
 8 constexpr long long size = 100000000;
 9 
10 int main(){
11 
12   std::cout << std::endl;
13 
14   std::vector<int> randValues;
15   randValues.reserve(size);
16 
17   // random values
18   std::random_device seed;
19   std::mt19937 engine(seed());
20   std::uniform_int_distribution<> uniformDist(1, 10);
21   for (long long i = 0 ; i < size ; ++i) 
22        randValues.push_back(uniformDist(engine));
23  
24   const auto sta = std::chrono::steady_clock::now();
25   
26   unsigned long long sum = {};
27   for (auto n: randValues) sum += n;
28  
29   const std::chrono::duration<double> dur = 
30         std::chrono::steady_clock::now() - sta;
31         
32   std::cout << "Time for addition " << dur.count() 
33             << " seconds" << std::endl;
34   std::cout << "Result: " << sum << std::endl;
35 
36   std::cout << std::endl;
37 
38 }
```

Summation of a vector in a range-based for loop

The reference number for Linux

![Explicit summation on Linux](images/DataStructures----CalculateWithLoop.png)

Explicit summation on Linux

and for Windows.

![Explicit summation on Windows](images/DataStructures----CalculateWithLoop_win.PNG)

Explicit summation on Windows

##### Single-Threaded Summation with Synchronisation ([lock](#chap06.xhtml_chapterXXXLocks))

In contrast, the range-based for-loop with additional synchronisation. I show only the source code difference to the non-sychronised version.

```
// calculateWithLock.cpp

...

std::mutex myMutex;

for (auto i: randValues){
  std::lock_guard<std::mutex> myLockGuard(myMutex);
  sum += i;
}

...
```

Summation of a vector by using a lock for the summation variable

Respectively, the performance numbers for Linux

![Single-threaded summation on Linux using a lock](images/DataStructures----CalculateWithLock.png)

Single-threaded summation on Linux using a lock

and Windows.

![Single-threaded summation on Windows using a lock](images/DataStructures----CalculateWithLock_win.PNG)

Single-threaded summation on Windows using a lock

##### The Comparison

Of course, the non-synchronised version is about 50 - 150 times faster as the version using locks. This difference holds for Linux and Windows. The performance numbers seem to speak a clear statement against locks, but you have to consider that this was a synchronisation-heavy job. Additionally, when you have to synchronise only a few times, a lock may be your best and sufficiently performant version.

#### Scalability

How is the performance characteristic of your data structure when the number of concurrent clients increases or the data structure is bounded? These are two questions which you should have to answer. Scalability means that there is a 1 to 1 relation between clients of the data structure and the throughput.

*   For example when you have a thread-safe queue with one producer/consumer, each additional producer or consumer must be blocked until the previous one is done. This blocking restriction does not hold for a thread-safe many producers/many consumers queue. For simplicity reasons, I call the second scenario a n/n relation. n can also be 1\. The question in the second scenario is if the producer can satisfy all consumers or the other way around. If not, producers or consumers have to wait which hinters scalability.
*   When your data structure is a bounded thread-safe queue, you can not expect perfect scalability because the producer/consumer fail at one point out of lockstep. An internally used puffer between the producers and consumers may decouple them but will not solve the original issue.

Let me answer the two questions for the concrete `ThreadSafeQueue` from chapter [Concurrent Architecture](#chap14.xhtml_chapterXXXConcurrentSSSArchitectur).

```
 1 template <typename T>
 2 class Monitor{
 3 public:
 4     void lock() const {
 5         monitMutex.lock();
 6     }
 7     void unlock() const {
 8         monitMutex.unlock();
 9     }
10     
11     void notify_one() const noexcept {
12         monitCond.notify_one();
13     }
14     void wait() const {
15         std::unique_lock<std::recursive_mutex> monitLock(monitMutex);
16         monitCond.wait(monitLock);
17     }
18     
19 private:
20     mutable std::recursive_mutex monitMutex;
21     mutable std::condition_variable_any monitCond;
22 };
23 
24 template <typename T>
25 class ThreadSafeQueue: public Monitor<ThreadSafeQueue<T>>{
26 public:
27     void add(T val){ 
28         derived.lock();
29         myQueue.push(val);
30         derived.unlock();
31         derived.notify_one();
32     } 
33     
34     T get(){ 
35         derived.lock();
36         while (myQueue.empty()) derived.wait();
37         auto val = myQueue.front();
38         myQueue.pop();
39         derived.unlock();
40         return val;
41     }
42 private:
43     std::queue<T> myQueue;
44     ThreadSafeQueue<T>& derived = static_cast<ThreadSafeQueue<T>&>(*this);
45 };
```

The Monitor Object

The method `add` adds (line 27) an element of type `T` to the `std::queue`, and the method `get` (line 34) removes an element from the `std::queue`. The class `ThreadSafeQueue` implements the Monitor Object. The Monitor Object design pattern synchronizes concurrent method execution to ensure that only one method at a time runs within an object. When a producer is done, one consumer will be notified by the `std::condition_variable_any` (line 21). A `std::recursive_mutex` (line 20) protects modification on an internal queue. This description should be sufficient to answer our two question. If you want to know more about this architecture pattern, read the previous chapter to the [Monitor Object](#chap14.xhtml_chapterXXXMonitorSSSObject).

*   It’s quite evident that the consumer can be blocked in line 36, if no values are available.
*   The second question is straightforward to answer because the thread-safe queue is not bounded.

#### Invariants

An invariant is a condition or relation that is always true. For example, the sum of all credit and debts for all accounts should be zero at any time. Should, because for the following program, the invariant will not hold.

```
 1 // invariant.cpp
 2 
 3 #include <functional>
 4 #include <iostream>
 5 #include <mutex>
 6 #include <numeric>
 7 #include <random>
 8 #include <thread>
 9 #include <vector>
10 
11 class Accounts{
12 public:
13     void deposit(int account){
14         std::lock_guard<std::mutex> lockAcc(mutAcc);
15         accounts[account] += 10;
16     }
17     
18     void takeOff(int account){
19         std::lock_guard<std::mutex> lockAcc(mutAcc);
20         accounts[account] -= 10;
21     }
22     
23     int getSum() const {
24         std::lock_guard<std::mutex> lockAcc(mutAcc);
25         return std::accumulate(accounts.begin(), accounts.end(), 0);
26     }
27         
28 private:
29     std::vector<int> accounts = std::vector<int>(100, 0);
30     mutable std::mutex mutAcc;
31 };
32 
33 class Dice{
34 public:
35     int operator()(){ return rand(); }
36 private:
37     std::function<int()> rand = std::bind(std::uniform_int_distribution<>(0, 99), 
38                                           std::default_random_engine());
39 };
40 
41 using namespace std::chrono_literals;
42 
43 int main(){
44     
45     constexpr auto TRANS = 1000;
46     constexpr auto OBS = 10;
47     Accounts acc;
48     Dice dice;
49     
50     std::vector<std::thread> transactions(TRANS);
51     for (auto& thr: transactions) thr = std::thread([&acc, &dice]{
52         acc.deposit(dice());
53         std::this_thread::sleep_for(10ns);
54         acc.takeOff(dice()); }
55     );
56     
57     std::mutex coutMutex;
58     
59     std::vector<std::thread> observers(OBS);
60     for (auto& thr: observers) thr = std::thread([&acc, &coutMutex]{
61         std::lock_guard<std::mutex> coutLock(coutMutex);
62         std::this_thread::sleep_for(1ms);
63         std::cout << "Total sum: " << acc.getSum() << std::endl; }
64     );
65     
66     for (auto& thr: transactions) thr.join();
67     for (auto& thr: observers) thr.join();
68 }
```

Broken Invariants

The class `Accounts` has 100 accounts, all initialised to zero (line 24). You can deposit 10 unit (lines 13 - 16) from an account, given by the index. The method `takeOff` (lines 18 - 21) allows it to withdraw 10 units from a given account. The method `getSum` (lines 23 - 26) helps to check if all invariants hold. All three methods are synchronised via the `std::mutex mutAcc`. Now, to the provocation of the invariants. I create 1000 threads (lines 50 - 56) which adds (line 52) and removes (54) 10 units to and from an arbitrary account which is given by the dice. In contrast, 10 threads observe the sum of all accounts (lines 59 - 64). The longer the sleeping between the `deposit` and the `takeOff` call is (line 53), the more probable is it to observe the invariant such as in the following screenshot.

![Broken invariants caught in action](images/DataStructures----invariant.png)

Broken invariants caught in action

Of course, putting the `deposit` and the `takeOff` call into one [critical section](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) would guarantee the invariant.

#### Exceptions

What should happen if an exception occurs? The answer to this question depends on the data structure you use to create the thread. Here are a few options?

*   [`std::thread`](#chap06.xhtml_chapterXXXThreads): When the created thread throws an exception, `std::terminate` is called. This means that `std::terminate` passes the `main`-thread.
*   Task: Tasks such as [`std::async`](#chap06.xhtml_chapterXXXasync), [`std::packaged_task`](#chap06.xhtml_chapterXXXpackaged_task), and [`std::promise`](#chap06.xhtml_chapterXXXpromise) can throw an exception which has to be handled by the associated [`std::future`](#chap06.xhtml_chapterXXXfuture) .
*   Parallel algorithms of the STL: If an exception occurs during the usage of an algorithm with an execution policy, `std::terminate` is called.

`std::terminate` calls the installed [`std::terminate_handler`](https://en.cppreference.com/w/cpp/error/terminate_handler). The consequence is that per default [`std::abort`](https://en.cppreference.com/w/cpp/utility/program/abort) is called, which causes abnormal program termination.

Now, it’s time to consider these concerns in practice. Typically concurrent data structures are stacks and queues.

### Concurrent Stack

First of all: What is a stack?

Let me implement the concurrent stack successively.

#### A Simplified Implementation

My first implementation only supports the `push` method. The class `ConcurrentStackPush` is a thin wrapper around a `std::stack`.

```
 1 // concurrentStackPush.cpp
 2 
 3 #include <list>
 4 #include <mutex>
 5 #include <stack>
 6 #include <string>
 7 #include <utility>
 8 #include <vector>
 9 
10 template<typename T, template <typename, typename> class Cont = std::deque> 
11 class ConcurrentStackPush{
12 public:
13     void push(T val){
14         std::lock_guard<std::mutex> lockStack(mutexStack);
15         myStack.push(std::move(val));
16     }
17     ConcurrentStackPush() = default;
18     ConcurrentStackPush(const ConcurrentStackPush&) = delete;
19     ConcurrentStackPush& operator= (const ConcurrentStackPush&) = delete;   
20 private:
21     mutable std::mutex mutexStack;
22     std::stack<T, Cont<T, std::allocator<T>>> myStack;
23 };
24 
25 int main(){
26 
27     ConcurrentStackPush<int> conStack;
28     conStack.push(5);
29     
30     ConcurrentStackPush<double, std::vector> conStack2;
31     conStack2.push(5.5);
32     
33     ConcurrentStackPush<std::string, std::list> conStack3;
34     conStack3.push("hello");
35 
36 }
```

A concurrent Stack supporting push

From the concurrency perspective, the type `ConcurrentStackPush` supports the `push` method (lines 13 - 16), which copies a new element to the internal `myStack` (line 22). Thanks to the `mutexStack` in line 21, the copy-operation is thread-safe. I assume, you are irritated by the second template parameter: `template <typename, typename> class Cont = std::deque`. The second template parameter is a so-called template-template parameter. It’s default is `std::deque`. `Cont` is the container for holding the elements. `Cont` needs the type and the allocator of its arguments. In line 22, you see the usage of the parameter `Cont`. `Cont` is the second argument of the internal `std::stack`. The lines 27, 30, and 33 show how you can instantiate a `ConcurrentStackPush` with various containers. `conStack` (line 27) uses a `std::deque`. `contStack2` (line 30) uses a `std::vector`, and `contStack2` (line 33) uses a `std::list`.

[`std::stack`](http://en.cppreference.com/w/cpp/container/stack) and the following [`std::queue`](http://en.cppreference.com/w/cpp/container/queue) are so-called container adapter, because they use an existing container and support a stack-like or queue-like interface.

You may ask yourself why I use the `ConcurrentStackPush` in a single-threaded environment and why I don’t show any output, here is my answer: just having one method `push` is too restricting. `ConcurrentStackPush` should only serve as a starting point for a complete Implementation.

#### A Complete Implementation

According to the info box [stack](#chap17.xhtml_chapterXXXStackSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC), my concurrent stack should at least support the methods `push`, `pop`, and `top`.

You may have the assumption, that the straightforward extension of the previous type `ConcurrentStackPush` would do the job. This assumption is wrong.

```
template<typename T, template <typename, typename> class Cont = std::deque> 
class ConcurrentStackBroken{
public:
    void push(T val){
        std::lock_guard<std::mutex> lockStack(mutexStack);
        myStack.push(std::move(val));
    }
    void pop(){
        std::lock_guard<std::mutex> lockStack(mutexStack);
        myStack.pop();
    }
    T& top(){
        std::lock_guard<std::mutex> lockStack(mutexStack);
        return myStack.top();
    } 
    ConcurrentStackBroken() = default;
    ConcurrentStackBroken(const ConcurrentStackBroken&) = delete;
    ConcurrentStackBroken& operator= (const ConcurrentStackBroken&) = delete; 
private:
    mutable std::mutex mutexStack;
    std::stack<T, Cont<T, std::allocator<T>>> myStack;
};
```

A broken Concurrent Stack

The `ConcurrentStackBroken` has in addition to the method `push` the two methods `pop`, and `top`. Just using the same mutex `mutexStack` for all three methods is not correct. This native implementation has at least two issues. One is obvious; the second one is more involved.

First, the method `top` returns a reference. The reference can be used to modify an element which is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces) such as in the following code snippet.

```
int main(){

    ConcurrentStackBroken<int> conStack;
    conStack.push(5);

    auto fut = std::async(std::launch::async, [&conStack]{ conStack.top() += 5; });
    auto fut2 = std::async(std::launch::async, 
                           [&conStack]{ std::cout << conStack.top() << std::endl; });

}
```

Returning a reference

The issue is that the write operation of the first `std::async` is not synchronised with the read operation of the second `std::async.

The second issue is that the `top` method followed by the `pop` method is not an atomic operation. Let’s see what I mean.

```
int main(){

    ConcurrentStackBroken<int> conStack;
    constexpr auto SENTINEL = std::numeric_limits<int>::min();
    conStack.push(SENTINEL);
    conStack.push(5);

    auto saveRemove = [&conStack]{ if (conStack.top() != SENTINEL) conStack.pop(); };

    auto fut = std::async(std::launch::async, saveRemove);
    auto fut2 = std::async(std::launch::async, saveRemove);
    auto fut3 = std::async(std::launch::async, saveRemove);  

}
```

`top` and `pop` are not atomic

To ensure, that the `ConcurrentStackBroken` always has a valid element before I `pop` it, I `push`ed a `SENTINEL` on it. `SENTINEL` is the [invariant](#chap17.xhtml_chapterXXXInvariantsSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBCinvariant) that should hold for the concurrent data structure. The lambda-function `saveRemove` applies my protocol. The issue in `saveRemove` is that more than one `pop` operation could happen in sequence, based on the wrong assumption that `contStack` has a valid element. Of course, the three `std::async` all interleave and, therefore, the following sequence of operations can happen. The operations `top` and `pop` do not interleave because they use the same mutex.

```
conStack.top() // associated promise to `fut`
conStack.top() // associated promise to `fut2`
conStack.top() // associated promise to `fut3`
conStack.pop() // associated promise to `fut`
conStack.pop() // associated promise to `fut2`    // (2)
conStack.pop() // associated promise to `fut3`    // (3)
```

A possible interleaving

The constructed sequence of operations is fatal. With the call (2), the `SENTINEL` is removed and, therefore, the invariant broken. The call (3) has undefined behaviour because the `pop` call on the `std::stack` triggers a `pop_back` call on the internal container. Calling `pop_back` on an empty container is undefined behaviour.

Changing the interface of a concurrent data structure is often a viable way to overcome concurrency issues. In this case, I change the granularity of the interface and combine the methods `top` and `pop` into on method `topAndPop`. Of course, this combination of methods `top` and `pop` violates the [Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle).

```
 1 // concurrentStack.cpp
 2 
 3 #include <future>
 4 #include <limits>
 5 #include <iostream>
 6 #include <mutex>
 7 #include <stack>
 8 #include <stdexcept>
 9 #include <utility>
10 
11 template<typename T, template <typename, typename> class Cont = std::deque> 
12 class ConcurrentStackBroken{
13 public:
14     void push(T val){
15         std::lock_guard<std::mutex> lockStack(mutexStack);
16         myStack.push(std::move(val));
17     }
18     T topAndPop(){
19         std::lock_guard<std::mutex> lockStack(mutexStack);
20         if ( myStack.empty() ) throw std::out_of_range("The stack is empty!");
21         auto val = myStack.top();
22         myStack.pop();
23         return val;
24     } 
25     ConcurrentStackBroken() = default;
26     ConcurrentStackBroken(const ConcurrentStackBroken&) = delete;
27     ConcurrentStackBroken& operator= (const ConcurrentStackBroken&) = delete; 
28 private:
29     mutable std::mutex mutexStack;
30     std::stack<T, Cont<T, std::allocator<T>>> myStack;
31 };
32 
33 int main(){
34 
35     ConcurrentStackBroken<int> conStack;
36     
37     auto fut = std::async([&conStack]{ conStack.push(2011); });
38     auto fut1 = std::async([&conStack]{ conStack.push(2014); });
39     auto fut2 = std::async([&conStack]{ conStack.push(2017); });
40     
41     auto fut3 = std::async([&conStack]{ return conStack.topAndPop(); });
42     auto fut4 = std::async([&conStack]{ return conStack.topAndPop(); });
43     auto fut5 = std::async([&conStack]{ return conStack.topAndPop(); });
44     
45     fut.get(), fut1.get(), fut2.get();
46     
47     std::cout << fut3.get() << std::endl;
48     std::cout << fut4.get() << std::endl;
49     std::cout << fut5.get() << std::endl;
50     
51 }
```

A concurrent Stack

The method `topAndPop` (lines 18 - 24) returns a copy instead of a reference such as the method `top` before. Calling `pop` on an empty container is undefined behaviour. I prefer to throw a `std::out_of_range` exception (line 20) if the stack is empty. Returning a special non-value or returning a [`std::optional`](https://en.cppreference.com/w/cpp/utility/optional) is also a valid option. Copying the value has a downside. If the copy constructor of the value throws an exception such as [`std::bad_alloc`](https://en.cppreference.com/w/cpp/memory/new/bad_alloc), the value is lost.

The calls `fut.get(), fut1.get(), fut2.get()` (line 45) ensure, that the associated promise will run. If you don’t specify the launch policy, the promise may run lazily in the thread of the caller. Lazily means that the promise will execute if and only if the future asks for its result with `get` or `wait`. Launching the promises in a separate thread is also a valid option:

```
 auto fut = std::async(std::launch::asnyc, [&conStack]{ conStack.push(2011); });
    auto fut1 = std::async(std::launch::asnyc, [&conStack]{ conStack.push(2014); });
    auto fut2 = std::async(std::launch::asnyc, [&conStack]{ conStack.push(2017); });
```

Launching each promise in a separate thread

Finally, the output of the program:

![A Concurrent Stack](images/DataStructures----concurrentStack.PNG)

A Concurrent Stack

### Concurrent Queue

Accordingly to the chapter to the [Concurrent Stack](#chap17.xhtml_chapterXXXConcurrentSSSStackSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) I want to answer the question: What is a queue?

Based on my discussion to the concurrent stack, the first implementation of the concurrent queue is quite similar.

#### Coarse-Grained Locking

Let’s start straightforward. My first implementation combines the `front` and `pop` method into a method `frontAndPop`. In contrast, the method `push` adds the elements to the end of the queue. The method `back`, which is optional for a [`queue`](https://en.wikipedia.org/wiki/Queue_(abstract_data_type)), returns the last element of the queue. Honestly, I’m biased if I should support the method `back`. Here are my thoughts.

1.  Not support `back` limits the interface because you can never ask for the last element.
2.  Combine `back` and `push` into one method `backAndPush`. `backAndPush` should, in this case, return the to the `push` operation previous value. This combination seems to be promising but has two serious issues. First, the previous value has to be copied because a reference or a pointer would break the synchronisation. This copy operation is a performance penalty. Second, the copy constructor could throw an exception.
3.  Supporting both methods `back` and `push` separately introduces a data race. Assume, a user makes an assumption based on the value of the last element. Now, we have the same issue, such as supporting `front` and `pop` as two separate methods. The argumentation to the methods `top` and `pop` in [concurrent stack](#chap17.xhtml_chapterXXXStackSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) also apply here. Honestly, this usage of the concurrent queue seems quite untypical to me, but caution counts.

Implementing the first variant is straightforward because it is quite similar to the concurrent stack. Here it is:

```
 1 // concurrentQueueCoarseLocking.cpp
 2 
 3 #include <future>
 4 #include <limits>
 5 #include <iostream>
 6 #include <mutex>
 7 #include <queue>
 8 #include <stdexcept>
 9 #include <utility>
10 
11 template<typename T, template <typename, typename> class Cont = std::deque> 
12 class ConcurrentQueue{
13 public:
14     void push(T val){
15         std::lock_guard<std::mutex> lockStack(mutexQueue);
16         myQueue.push(std::move(val));
17     }
18     T frontAndPop(){
19         std::lock_guard<std::mutex> lockStack(mutexQueue);
20         if ( myQueue.empty() ) throw std::out_of_range("The queue is empty!");
21         auto val = myQueue.front();
22         myQueue.pop();
23         return val;
24     } 
25     ConcurrentQueue() = default;
26     ConcurrentQueue(const ConcurrentQueue&) = delete;
27     ConcurrentQueue& operator= (const ConcurrentQueue&) = delete; 
28 private:
29     mutable std::mutex mutexQueue;
30     std::queue<T, Cont<T, std::allocator<T>>> myQueue;
31 };
32 
33 int main(){
34 
35     ConcurrentQueue<int> conQueue;
36     
37     auto fut = std::async([&conQueue]{ conQueue.push(2011); });
38     auto fut1 = std::async([&conQueue]{ conQueue.push(2014); });
39     auto fut2 = std::async([&conQueue]{ conQueue.push(2017); });
40     
41     auto fut3 = std::async([&conQueue]{ return conQueue.frontAndPop(); });
42     auto fut4 = std::async([&conQueue]{ return conQueue.frontAndPop(); });
43     auto fut5 = std::async([&conQueue]{ return conQueue.frontAndPop(); });
44     
45     fut.get(), fut1.get(), fut2.get();
46     
47     std::cout << fut3.get() << std::endl;
48     std::cout << fut4.get() << std::endl;
49     std::cout << fut5.get() << std::endl;
50     
51 }
```

A concurrent Queue with Coarse-Grained Locking

Without further ado, the output of the program.

![A Concurrent Stack](images/DataStructures----concurrentQueueCoarseLocking.PNG)

A Concurrent Stack

Done? No, I ignored an optimisation possibility.

#### Fine-Grained Locking

In contrast to a stack, the `push` and `pop` operations on the queue happen separately on different ends.

##### A Broken Implementation

So instead of a coarse-grained locking with one mutex, a more fine-grained locking with two mutexes should reduce the synchronisation.

```
template<typename T, template <typename, typename> class Cont = std::deque> 
class ConcurrentQueue{
public:

    void push(T val){
        std::lock_guard<std::mutex> lockStack(mutexBackQueue);
        myQueue.push(std::move(val));
    }
    T frontAndPop(){
        std::lock_guard<std::mutex> lockStack(mutexFrontQueue);
        if (myQueue.empty()) throw std::out_of_range("The queue is empty!");
        auto val = myQueue.front();
        myQueue.pop();
        return val;
    } 
    ConcurrentQueue() = default;
    ConcurrentQueue(const ConcurrentQueue&) = delete;
    ConcurrentQueue& operator= (const ConcurrentQueue&) = delete; 
private:
    mutable std::mutex mutexFrontQueue;
    mutable std::mutex mutexBackQueue;
    std::queue<T, Cont<T, std::allocator<T>>> myQueue;
};
```

A broken implementation of fine-grained concurrent queue

There is an issue, which makes the implementation incorrect. When the queue is empty, `push` and `pop` operate on the same element, which is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces). Adding an element to separate the `push` from the `pop` operations, solves this issue.

I could not achieve the fine-grained concurrent queue, based on the abstraction, `std::queue` provides. Now, I have to do it by myself. First of all, how could a queue be implemented?

##### A Simple Queue

The straightforward way to implement a queue is it by using a singly-linked list. Singly-linked means that one node points to the next node but not the other way around. Additionally, a `head` pointer points to the head and the `tail` pointer to the tail of the data structure. Items can be removed (`pop`) from and added (`push`) to the queue. Elements are removed from the queue by putting the `head` pointer one position further. The remove operation will also return the old `head` node due to concurrency reasons. Elements are added to the queue by pointing the previous `tail` node to the new node. The remove and the add operation adjust the `head` and the `tail` pointer.

![A Simple Queue](images/DataStructures----SimpleQueue.png)

A Simple Queue

Here is the implementation to the simple queue.

```
 1 // simpleQueue.cpp
 2 
 3 #include <iostream>
 4 #include <memory>
 5 #include <utility>
 6 
 7 template <typename T>
 8 class Queue{
 9 private:
10     struct Node{
11         T data;
12         std::unique_ptr<Node> next;
13         Node(T data_): data(std::move(data_)){}
14     };
15     std::unique_ptr<Node> head;
16     Node* tail;
17 public:
18     Queue(): tail(nullptr){};
19     std::unique_ptr<T> pop(){
20         if (!head) throw std::out_of_range("The queue is empty!");
21         std::unique_ptr<T> res = std::make_unique<T>(std::move(head->data));
22         std::unique_ptr<Node> oldHead = std::move(head);
23         head = std::move(oldHead->next);
24         if (!head) tail = nullptr;
25         return res;
26     }
27     void push(T val){
28         std::unique_ptr<Node> newNode = std::make_unique<Node>(Node(std::move(val)));
29         Node* newTail = newNode.get();
30         if (tail) tail->next= std::move(newNode);
31         else head = std::move(newNode);
32         tail = newTail;
33     }
34     Queue(const Queue& other) = delete;
35     Queue& operator=(const Queue& other) = delete;
36 };
37 
38 int main(){
39     
40     std::cout << std::endl;
41     
42     Queue<int> myQueue;
43     myQueue.push(1998);
44     myQueue.push(2003);
45     std::cout << *myQueue.pop() << std::endl;
46     std::cout << *myQueue.pop() << std::endl;
47     myQueue.push(2011);
48     myQueue.push(2014);
49     std::cout << *myQueue.pop() << std::endl;
50     myQueue.push(2017);
51     myQueue.push(2020);
52     std::cout << *myQueue.pop() << std::endl;
53     std::cout << *myQueue.pop() << std::endl;
54     std::cout << *myQueue.pop() << std::endl;
55     
56     std::cout << std::endl;
57 
58 }
```

A Simple Queue

I use `std::unique_ptr`s to automatically manage the lifetime of the nodes. Only the `tail` pointer is a raw pointer (line 16) because the pointed-to node has already an owner. The method `push(T val)` (lines 27 - 33) adds a new value to the `Queue`. First, a new `Node` (line 28) is created. This `Node` becomes the new tail (line 29). If `tail` points to an existing `Node` (line 30), `tail`’s pointer is adjusted to the `newNode`; if not, `head` becomes the `newNode` (line 31). Finally, `tail` becomes the `newTail` (line 32). The method `pop` (lines 19 - 26) removes a node and returns the value (line 25). When the queue is empty, the method throws an exception (line 20). Line 21 creates the return value and creates the `oldHead` (line 22). `oldHead->next` becomes the new head (line 23). When the queue becomes empty by this `pop` operation, `tail` is set to a `nullptr`.

The screenshot shows the output of the program.

![Usage of the Simple Queue](images/DataStructures----SimpleQueueScreenshot.png)

Usage of the Simple Queue

You may ask, why I introduced my queue implementation because we have the same issue such as with the broken implementation before: `head` and `tail` can operate on the same node if the queue has one node. Subsequent interleaving `pop` and `push` calls could race. For example, the `tail->next` call (line 30) might interleave with the `oldHead->next` call (line 23). This interleaving means at the end, that I need one mutex to protect the entire data structure. Let me first answer your question. This queue implementation could not be made thread-safe by using two mutexes, but this implementation is the base for a thread-safe queue with fine-grained locking. I have to apply a trick to separate the head from the tail.

##### A Simple Queue with a Dummy Node

A dummy node does the trick. It separates the head from the tail. Now, the calls next on the head and on the tail could not interleave. Of course, the implementation becomes more difficult due to the fact that the dummy node has to be dealt with.

```
 1 // simpleQueueWithDummy.cpp
 2 
 3 #include <iostream>
 4 #include <memory>
 5 #include <utility>
 6 
 7 template <typename T>
 8 class Queue{
 9 private:
10     struct Node{
11         T data;
12         std::unique_ptr<Node> next;
13         Node(T data_): data(std::move(data_)){}
14     };
15     std::unique_ptr<Node> head;
16     Node* tail;
17 public:
18     Queue(): head(new Node(T{})), tail(head.get()){};
19     std::unique_ptr<T> pop(){
20         if (head.get() == tail) throw std::out_of_range("The queue is empty!");
21         std::unique_ptr<T> res = std::make_unique<T>(std::move(head->data));
22         std::unique_ptr<Node> oldHead = std::move(head);
23         head = std::move(oldHead->next);
24         if (!head) tail = nullptr;
25         return res;
26     }
27     void push(T val){
28         std::unique_ptr<Node> dummyNode = std::make_unique<Node>(Node(T{}));
29         Node* newTail = dummyNode.get();
30         tail->next= std::move(dummyNode);
31         tail->data = val;
32         tail = newTail;
33     }
34     Queue(const Queue& other) = delete;
35     Queue& operator=(const Queue& other) = delete;
36 };
37 
38 int main(){
39     
40     std::cout << std::endl;
41     
42     Queue<int> myQueue;
43     myQueue.push(1998);
44     myQueue.push(2003);
45     std::cout << *myQueue.pop() << std::endl;
46     std::cout << *myQueue.pop() << std::endl;
47     myQueue.push(2011);
48     myQueue.push(2014);
49     std::cout << *myQueue.pop() << std::endl;
50     myQueue.push(2017);
51     myQueue.push(2020);
52     std::cout << *myQueue.pop() << std::endl;
53     std::cout << *myQueue.pop() << std::endl;
54     std::cout << *myQueue.pop() << std::endl;
55     
56     std::cout << std::endl;
57 
58 }
```

A Simple Queue with a Dummy Node

The differences between the new simple queue to the previous one without a dummy node are not that big. First, `head` and `tail` are initialised to point to the dummy node. Let’s first analyse the `pop` method. Line 20 checks consequently, if the queue is logically empty; meaning, that the queue has only the dummy node. The method `push` changes more than the method `pop`. First, a new dummy node is created (line 28) which becomes at the end the node `tail` point’s to (line 29 and line 32). The old dummy points to the new dummy node (line 30) and gets the value `val` (line 31).

As expected, the output of the program using a queue with a dummy node is the same such as the previous one without a dummy node.

![Usage of the Simple Queue with a Dummy Node](images/DataStructures----SimpleQueueWithDummy.png)

Usage of the Simple Queue with a Dummy Node

Now, I’m done with my refactorisation. The crucial observation for the queue with a dummy node is that the `push` method and the `push` method work almost entirely on different ends. This separation allows it to use a mutex for each end. Only the check `(head.get() == tail)` (line 20) in the `pop` method requires both mutexes. This is not so bad because this critical region is short-lived.

With this knowledge in mind, let me put the pieces together and finally come to the concurrent queue with fine-grained locking.

##### The Implementation

The synchronisation of the queue is based on two mutexes. One mutex protects the head and one mutex protects the tail of the queue. The final question is: Where to put the two mutexes? To get maximum performance, the criticial regions should be as short-lived as possible. This means for the method `pop` that the entire method has to be proteced but for the method `push` only the instructions which uses the tail of the queue. The other operations are local and, therefore, per-se thread-safe.

```
 1 // concurrentQueueFineLocking.cpp
 2 
 3 #include <future>
 4 #include <iostream>
 5 #include <memory>
 6 #include <mutex>
 7 #include <utility>
 8 
 9 template <typename T>
10 class ConcurrentQueue{
11 private:
12     struct Node{
13         T data;
14         std::unique_ptr<Node> next;
15         Node(T data_): data(std::move(data_)){}
16     };
17     std::unique_ptr<Node> head;
18     Node* tail;
19     std::mutex headMutex;
20     std::mutex tailMutex;
21 public:
22     ConcurrentQueue(): head(new Node(T{})), tail(head.get()){};
23     std::unique_ptr<T> pop(){
24         std::lock_guard<std::mutex> headLock(headMutex);
25         {
26             std::lock_guard<std::mutex> tailLock(tailMutex);
27             if (head.get() == tail) throw std::out_of_range("The queue is empty!");
28         }
29         std::unique_ptr<T> res = std::make_unique<T>(std::move(head->data));
30         std::unique_ptr<Node> oldHead = std::move(head);
31         head = std::move(oldHead->next);
32         if (!head) tail = nullptr;
33         return res;
34     }
35     void push(T val){
36         std::unique_ptr<Node> dummyNode = std::make_unique<Node>(Node(T{}));
37         Node* newTail = dummyNode.get();
38         std::lock_guard<std::mutex> tailLock(tailMutex);
39         tail->next= std::move(dummyNode);
40         tail->data = val;
41         tail = newTail;
42     }
43     ConcurrentQueue(const ConcurrentQueue& other) = delete;
44     ConcurrentQueue& operator=(const ConcurrentQueue& other) = delete;
45 };
46 
47 int main(){
48     
49     std::cout << std::endl;
50     
51     ConcurrentQueue<int> conQueue;
52     
53     auto fut = std::async([&conQueue]{ conQueue.push(2011); });
54     auto fut1 = std::async([&conQueue]{ conQueue.push(2014); });
55     auto fut2 = std::async([&conQueue]{ conQueue.push(2017); });
56     
57     auto fut3 = std::async([&conQueue]{ return *conQueue.pop(); });
58     auto fut4 = std::async([&conQueue]{ return *conQueue.pop(); });
59     auto fut5 = std::async([&conQueue]{ return *conQueue.pop(); });
60     
61     fut.get(), fut1.get(), fut2.get();
62     
63     std::cout << fut3.get() << std::endl;
64     std::cout << fut4.get() << std::endl;
65     std::cout << fut5.get() << std::endl;
66     
67     std::cout << std::endl;
68 
69 }
```

A Fine-Grained Concurrent Queue

First of all: Is the implementation thread-safe? The `ConcurrentQueue` has only two methods. Operations on the shared singly-linked list of `Nodes` are protected by two mutexes. The `headMutex` (line 19) is responsible for protecting the head of the data structure and the `tailMutex` (line 20) is responsible for protecting the tail of the data structure. The only operation, which could work on the `head` and the `tail` of the singly-linked list, is protected by both mutexes (line 27). Consequently, the `ConcurrentQueue` is [data race](#chap20.xhtml_chapterXXXDataSSSRaces) free. You should avoid to acquire more than one mutex at one point in time because this can provoke a [deadlock](#chap20.xhtml_chapterXXXDeadlocks) if both mutexe are acquired in different order. Although the method `pop` acquires first the `headMutex` (line 24) and then the `tailMutex` (line 26), there is no potential for a deadlock because the mutexes are always acquired in the same order.

Executing the fine-grained concurrent queue works as expected.

![A concurrent Queue with Fine-Grained Locking](images/DataStructures----concurrentQueueFineLocking.png)

A concurrent Queue with Fine-Grained Locking

Sometimes a program run throws an exception. This exception is fine due to my design decision. When the queue is empty, I throw a `std::out_of_range` exception in the `pop` method. Instead of throwing an exception, a more appropriate strategy is to wait.

##### Waiting for the Value

Using a `std::condition_variable` enables the `pop` call to wait until a value is available.

```
 1 // concurrentQueueFineLockingWithWaiting.cpp
 2 
 3 #include <condition_variable>
 4 #include <future>
 5 #include <iostream>
 6 #include <memory>
 7 #include <mutex>
 8 #include <utility>
 9 
10 template <typename T>
11 class Queue{
12 private:
13     struct Node{
14         T data;
15         std::unique_ptr<Node> next;
16         Node(T data_): data(std::move(data_)){}
17     };
18     std::unique_ptr<Node> head;
19     Node* tail;
20     std::mutex headMutex;
21     std::mutex tailMutex;
22     std::condition_variable condVar;
23 public:
24     Queue(): head(new Node(T{})), tail(head.get()){};
25     std::unique_ptr<T> pop(){
26         std::lock_guard<std::mutex> headLock(headMutex);
27         {
28             std::unique_lock<std::mutex> tailLock(tailMutex);
29             if (head.get() == tail) condVar.wait(tailLock);
30         }
31         std::unique_ptr<T> res = std::make_unique<T>(std::move(head->data));
32         std::unique_ptr<Node> oldHead = std::move(head);
33         head = std::move(oldHead->next);
34         if (!head) tail = nullptr;
35         return res;
36     }
37     void push(T val){
38         std::unique_ptr<Node> dummyNode = std::make_unique<Node>(Node(T{}));
39         Node* newTail = dummyNode.get();
40         {
41             std::unique_lock<std::mutex> tailLock(tailMutex);
42             tail->next= std::move(dummyNode);
43             tail->data = val;
44             tail = newTail;
45         }
46         condVar.notify_one();
47     }
48     Queue(const Queue& other) = delete;
49     Queue& operator=(const Queue& other) = delete;
50 };
51 
52 int main(){
53     
54     std::cout << std::endl;
55     
56     Queue<int> conQueue;
57     
58     auto fut = std::async([&conQueue]{ conQueue.push(2011); });
59     auto fut1 = std::async([&conQueue]{ conQueue.push(2014); });
60     auto fut2 = std::async([&conQueue]{ conQueue.push(2017); });
61     
62     auto fut3 = std::async([&conQueue]{ return *conQueue.pop(); });
63     auto fut4 = std::async([&conQueue]{ return *conQueue.pop(); });
64     auto fut5 = std::async([&conQueue]{ return *conQueue.pop(); });
65     
66     fut.get(), fut1.get(), fut2.get();
67     
68     std::cout << fut3.get() << std::endl;
69     std::cout << fut4.get() << std::endl;
70     std::cout << fut5.get() << std::endl;
71     
72     std::cout << std::endl;
73 
74 }
```

A Concurrent Queue with Fine-Grained Locking and Waiting

The modification to the previous concurrent queue with fine-grained locking are minimal. The `pop` call waits in line 29 if no value is available. `std::condition_variable` requires a `std::unique_lock` instead of a `std::lock_guard`. The `push` call notifies its waiter with `condVar.notify_one` that a new value is available (line 46). `condVar.notify_one` is per-se thread-safe and needs, therefore, no synchronisation. Maybe, you miss the predicate in the `wait` call (line 29). This predicate should protect against [spurious wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) and [lost wakeups](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup). This protection is exactly the job of the condition `head.get() == tail`.

The screenshot ends my story to the lock-based concurrent queue.

![A concurrent Queue with Fine-Grained Locking and Waiting](images/DataStructures----concurrentQueueFineLockingWithWaiting.png)

A concurrent Queue with Fine-Grained Locking and Waiting

## Lock-Free Data Structures

# Further Information

## Challenges

Programming concurrent applications is inherently complicated. This still holds true if you use C++11 and C++14 features, and that is before I mention the memory model. I hope that if I dedicate a whole chapter to the challenges of concurrent programming, you may become more aware of the pitfalls.

### ABA Problem

ABA means you read a value twice and each time it returns the same value A. Therefore you conclude that nothing changed in between. However, you missed the fact that the value was updated to B somewhere in between.

Let me first use a simple scenario to introduce the problem.

##### An Analogy

The scenario consists of you sitting in a car and waiting for the traffic light to become green. Green stands in our case for B, and red for A. What’s happening?

1.  You look at the traffic light, and it is red (A).
2.  Because you are bored, you begin to check the news on your smartphone and forget the time.
3.  You look once more at the traffic light. Damn, it is still red (A).

Of course, the traffic light became green (B) between your two checks. Therefore, what seems to be one red phase was a full cycle.

What does this mean for threads (processes)? Now more formally.

1.  Thread 1 reads the variable `var` with value A.
2.  Thread 1 is preempted, and thread 2 runs.
3.  Thread 2 changes the variable `var` from A to B to A.
4.  Thread 1 continues to run and checks the value of variable `var` and gets A. Because of the value `A`, thread 1 proceeds.

Often that is a not a problem, and you can ignore it.

##### Non-critical ABA

The functions `compare_exchange_strong` and `compare_exchange_weak` suffer the ABA problem that can be observed in the `fetch_mult` (line 6). Here, it is non-critical. `fetch_mult` multiplies a `std::atomic<T>& shared` by `mult`.

```
 1 // fetch_mult.cpp
 2 
 3 #include <atomic>
 4 #include <iostream>
 5 
 6 template <typename T>
 7 T fetch_mult(std::atomic<T>& shared, T mult){
 8   T oldValue = shared.load();
 9   while (!shared.compare_exchange_strong(oldValue, oldValue * mult));
10   return oldValue;
11 }
12 
13 int main(){
14   std::atomic<int> myInt{5};
15   std::cout << myInt << std::endl;          
16   fetch_mult(myInt,5);
17   std::cout << myInt << std::endl;         
18 }
```

An atomic multiplication with `compare_exchange_strong`

The key observation is that there is a small time window between the reading of the old value `T oldValue = shared.load` in line 8 and the comparison with the new value in line 9\. Therefore, another thread can kick in and change the `oldValue` from `oldValue` to another value and back to `oldValue`. The `oldValue` is the A, the another value is the B in ABA.

Often it makes no difference if Read-Operations address the same, unchanged variable. However, in a lock-free concurrent data structure, ABA may have a significant impact.

##### A lock-free data structure

I do not present a lock-free data structure in detail here. I use a lock-free stack that is implemented as a singly linked list. The stack supports only two operations.

1.  Pop the top object and return a pointer to it.
2.  Push the specified object to stack.

Let me describe the pop operation in pseudo-code to give you an idea of the ABA problem. The pop operation executes the following steps until the operation is successful.

1.  Get the head node: `head`
2.  Get the subsequent node: `headNext`
3.  Make `headNext` to the new head if `head` is still the head of the stack

Here are the first two nodes of the stack:

```
Stack: TOP -> head -> headNext -> ...
```

Let’s construct the ABA problem.

##### ABA in Action

Let’s start with the following stack:

```
Stack: TOP -> A -> B -> C
```

Thread 1 is active and wants to pop the head of the stack.

*   Thread 1 stores

```
 head = A
    headNext = B
```

Before thread 1 finishes the pop step, thread 2 kicks in.

*   Thread 2 pops A

```
 Stack: TOP -> B -> C
```

*   Thread 2 pops B and deletes B

```
 Stack: TOP -> C
```

*   Thread 2 pushed A back

```
 Stack: TOP -> A -> C
```

Thread 1 is rescheduled and checks if `A == head`. Because of `A == head, headNext` which is B becomes the new head. However, B was already deleted. Therefore, the program has undefined behaviour.

There are a few remedies to the ABA problem.

##### Remedies

The conceptional problem of ABA is quite easy to understand. A node such as `B == headNext` was deleted although another node `A == head` was referring to it. The solution to our problem is to get rid of the premature deletion of the node. Here are a few remedies.

###### Tagged state reference

You can use the low bits of the address to add a tag to each node indicating how often the node has been successfully modified. The result is that compare and swap (CAS) method eventually fails although the check returns true. This idea does not solve the issue because the tag bits may eventually wrap around. Architectures which support a double word CAS operation can have a bigger counter.

Tagged state reference are typically used in [transactional memory](#chap10.xhtml_chapterXXXTransactionalSSSMemory).

The next three techniques are based on the idea of deferred reclamation.

###### Garbage Collection

Garbage collection guarantees that the variables are only deleted if it is not needed anymore. This sounds promising but has a significant drawback. Most garbage collectors are not lock-free, therefore, even if you have a lock-free data structure, the overall system won’t be lock-free.

###### Hazard Pointers

From Wikpedia: [Hazard Pointers](https://en.wikipedia.org/wiki/Hazard_pointer):

In a hazard-pointer system, each thread keeps a list of hazard pointers indicating which nodes the thread is currently accessing. (In many systems this “list” may be probably limited to only one or two elements.) Nodes on the hazard pointer list must not be modified or deallocated by any other thread. (…) When a thread wishes to remove a node, it places it on a list of nodes “to be freed later”, but does not deallocate the node’s memory until no other thread’s hazard list contains the pointer. A dedicated garbage-collection thread can do this manual garbage collection (if the list “to be freed later” is shared by all the threads); alternatively, cleaning up the “to be freed” list can be done by each worker thread as part of an operation such as “pop”.

##### RCU

RCU stands for **R**ead **C**opy **U**pdate and is a synchronisation technique for almost read-only data structures. RCU was created by Paul McKenney and has been used in the Linux Kernel since 2002.

The idea is quite simple and follows the acronym. To modify data, you make a copy of the data and modify that copy. In contrast, all readers work with the original data. If there is no reader, you can safely replace the data structure with its copy.

For more details about RCU, read the article [What is RCU, Fundamentally?](https://lwn.net/Articles/262464/) by Paul McKenney.

### Blocking Issues

To make my point clear, you have to use a [condition variable](#chap20.xhtml_chapterXXXConditionSSSVariables) in combination with a [predicate](#chap23.xhtml_glossaryXXXPredicateSSSBOBOBOGlossaryBCBCBC). If you don’t, your program may become a victim of a [spurious wakeup](#chap20.xhtml_glossaryXXXSpuriousSSSWakeupSSSBOBOBOGlossaryBCBCBC) or [lost wakeup](#chap23.xhtml_glossaryXXXLostSSSWakeupSSSBOBOBOGlossaryBCBCBC).

If you use a condition variable without a predicate, the notifying thread may send its notification before the waiting thread is waiting. Therefore, the waiting thread waits forever. This phenomenon is called a lost wakeup.

Here is the program.

```
 1 // conditionVariableBlock.cpp
 2 
 3 #include <iostream>
 4 #include <condition_variable>
 5 #include <mutex>
 6 #include <thread>
 7 
 8 std::mutex mutex_;
 9 std::condition_variable condVar;
10 
11 bool dataReady;
12 
13 
14 void waitingForWork(){
15 
16     std::cout << "Worker: Waiting for work." << std::endl;
17 
18     std::unique_lock<std::mutex> lck(mutex_);
19     condVar.wait(lck);                          
20     // do the work
21     std::cout << "Work done." << std::endl;
22 
23 }
24 
25 void setDataReady(){
26 
27     std::cout << "Sender: Data is ready."  << std::endl;
28     condVar.notify_one();                        
29 
30 }
31 
32 int main(){
33 
34   std::cout << std::endl;
35 
36   std::thread t1(setDataReady);
37   std::thread t2(waitingForWork);               
38 
39   t1.join();
40   t2.join();
41 
42   std::cout << std::endl;
43   
44 }
```

Blocking condition variables

By chance, the first invocation of the program works fine. The second invocation locks because the notify call (line 28) happens before the thread `t2` (line 37) is waiting (line 19).

![A blocking condition variable](images/Challenges----conditionVariableBlock.png)

A blocking condition variable

Of course, deadlocks and livelocks are side effects of race conditions. A deadlock depends in general on the interleaving of the threads and may sometimes occur or not. A livelock is similar to a deadlock. While a deadlock blocks, a livelock seems to make progress, with the emphasis on “seems”. Think about a transaction in a transactional memory use case. Each time the transaction should be committed a conflict happens; therefore a rollback takes place. Here are the details of [transactions](#chap10.xhtml_chapterXXXTransactionalSSSMemory).

### Breaking of Program Invariants

Program invariants are invariants that should hold for the entire lifetime of your program.

Malicious [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition) breaks an invariant of the program. The invariant of the program is that the sum of all balances should be the same amount. Which in our case is 200 euros because each account starts with 100 euro (line 9). I neither want to create money by transferring it nor do I want to destroy it.

```
 1 // breakingInvariant.cpp
 2 
 3 #include <atomic>
 4 #include <functional>
 5 #include <iostream>
 6 #include <thread>
 7 
 8 struct Account{
 9   std::atomic<int> balance{100};                               
10 };
11                                                             
12 void transferMoney(int amount, Account& from, Account& to){
13   using namespace std::chrono_literals;
14   if (from.balance >= amount){
15     from.balance -= amount;  
16     std::this_thread::sleep_for(1ns);                           
17     to.balance += amount;
18   }
19 }
20 
21  void printSum(Account& a1, Account& a2){
22   std::cout << (a1.balance + a2.balance) << std::endl;         
23 }
24 
25 int main(){
26   
27   std::cout << std::endl;
28 
29   Account acc1;
30   Account acc2;
31   
32   std::cout << "Initial sum: ";                          
33   printSum(acc1, acc2);                                       
34   
35   std::thread thr1(transferMoney, 5, std::ref(acc1), std::ref(acc2));
36   std::thread thr2(transferMoney, 13, std::ref(acc2), std::ref(acc1));
37   std::cout << "Intermediate sum: ";                
38   std::thread thr3(printSum, std::ref(acc1), std::ref(acc2));  
39   
40   thr1.join();
41   thr2.join();
42   thr3.join();
43                                                                
44   std::cout << "     acc1.balance: " << acc1.balance << std::endl;
45   std::cout << "     acc2.balance: " << acc2.balance << std::endl;
46   
47   std::cout << "Final sum: ";
48   printSum(acc1, acc2);                                        
49   
50   std::cout << std::endl;
51 
52 }
```

Breaking an invariant of the program

At the beginning, the sum of the accounts is 200 euros. Line 33 displays the sum by using the function `printSum` in lines 21 - 23\. Line 38 makes the invariant visible. Because there is a short sleep of 1ns in line 16, the intermediate sum is 182 euro. In the end, all is fine; each account has the right balance (line 44 and line 45), and the sum is 200 euro (line 48).

Here is the output of the program.

![The invariant of the accounts](images/Challenges----breakingInvariant.PNG)

The invariant of the accounts

### Data Races

A data race is a situation, in which at least two threads access a shared variable at the same time. At least one thread tries to modify the variable.

If your program has a data race, it has undefined behaviour. This means all outcomes are possible and therefore, reasoning about the program makes no sense anymore.

Let me show you a program with a data race.

```
 1 // addMoney.cpp
 2 
 3 #include <functional>
 4 #include <iostream>
 5 #include <thread>
 6 #include <vector>
 7 
 8 struct Account{
 9   int balance{100};                             
10 };
11 
12 void addMoney(Account& to, int amount){
13   to.balance += amount;                         
14 }
15 
16 int main(){
17   
18   std::cout << std::endl;
19 
20   Account account;
21   
22   std::vector<std::thread> vecThreads(100);
23   
24                                                  
25   for (auto& thr: vecThreads) thr = std::thread(addMoney, std::ref(account), 50);
26   
27   for (auto& thr: vecThreads) thr.join();
28   
29                                                  
30   std::cout << "account.balance: " << account.balance << std::endl;
31   
32   std::cout << std::endl;
33 
34 }
```

A data race

100 threads are adding 50 euros (line 25) to the same account (line 20). They use the function `addMoney`. The critical observation is that the writing to the account is done without synchronisation. Therefore we have a data race, and the result is not valid. This is undefined behaviour, and the final balance (line 30) differs between 5000 and 5100 euro.

![A data race causes incorrect balances](images/Challenges----addMoney.png)

A data race causes incorrect balances

### Deadlocks

A deadlock is a state in which at least one thread is blocked forever because it waits for the release of a resource it does never get.

There are two main reasons for deadlocks:

1.  A mutex has not been unlocked.
2.  You lock your mutexes in a different order.

For overcoming the second issue, techniques such as [lock hierachies](http://collaboration.cmc.ec.gc.ca/science/rpn/biblio/ddj/Website/articles/DDJ/2008/0801/071201hs01/071201hs01.html) are used in classical C++.

For the details about deadlocks and how to overcome them with modern C++, read the subsection [issues of mutexes](#chap06.xhtml_chapterXXXIssuesSSSofSSSMutexes) and [locks](#chap06.xhtml_chapterXXXLocks).

### False Sharing

When a processor reads a variable such as an `int` from main memory, it reads more than the size of an `int` from memory. The processor reads an entire cache line (typically 64 bytes) from memory. False sharing occurs if two threads read at the same time different variables `a` and `b` that are located on the same cache line. Although `a` and `b` are logically separated, they are physically connected. An expensive hardware synchronisation on the cache line is necessary because `a` and `b` share the same one. The result is that you get the right results, but the performance of your concurrent application decreases. Precisely this phenomenon happen in the following program.

```
 1 // falseSharing.cpp
 2 
 3 #include <algorithm>
 4 #include <chrono>
 5 #include <iostream>
 6 #include <random>
 7 #include <thread>
 8 #include <vector>
 9 
10 constexpr long long size{100000000};   
11 
12 struct Sum{
13     long long a{0};
14     long long b{0};
15 };
16 
17 int main(){
18     
19     std::cout << std::endl;
20     
21     Sum sum;
22     
23     std::cout << &sum.a << std::endl;
24     std::cout << &sum.b << std::endl;
25     
26     std::cout << std::endl;
27 
28     std::vector<int> randValues, randValues2;
29     randValues.reserve(size);
30     randValues2.reserve(size);
31 
32     std::mt19937 engine;
33     std::uniform_int_distribution<> uniformDist(1,10);
34 
35     int randValue;
36     for (long long i = 0; i < size; ++i){ 
37         randValue = uniformDist(engine);
38         randValues.push_back(randValue);
39         randValues2.push_back(randValue);
40     }
41     
42     auto sta = std::chrono::steady_clock::now();
43     
44     std::thread t1([&sum, &randValues]{ 
45         for (auto val: randValues) sum.a += val; 
46     });
47     
48     std::thread t2([&sum, &randValues2]{ 
49         for (auto val: randValues2) sum.b += val; 
50     });
51     
52     t1.join(), t2.join();
53     
54     std::chrono::duration<double> dur= std::chrono::steady_clock::now() - sta;
55     std::cout << "Time for addition " << dur.count() 
56             << " seconds" << std::endl;
57     
58     std::cout << "sum.a: " << sum.a << std::endl;
59     std::cout << "sum.b: " << sum.b << std::endl;
60     
61     std::cout << std::endl;
62     
63 }
```

False sharing

The variables `a` and `b` in line 13 and 14 share the same cache line. Thread `t1` (line 44) and the thread `t2` use both variables to concurrently add up the vectors `randValues` and `randValues2`. Both vectors have 100 million integers between 1 and 10\. The output of the program shows the interesting facts. `a` and `b` are aligned at 8-byte boundaries because this is the alignment for `long long` ints on my system.

![False sharing](images/Challenges----falseSharing.png)

False sharing

What happens if I change the alignment of `a` and `b` to 64 bytes? 64 is the size of the cache line on my system. Here is the small change I have to make to the struct `Sum`. I don’t use a seed for my random number generator; therefore, I get the same random numbers each time.

```
struct Sum{
    alignas(64) long long a{0};
    alignas(64) long long b{0};
};
```

![False sharing resolved](images/Challenges----falseSharing64.png)

False sharing resolved

Now `a` and `b` are aligned at 64-byte boundaries, and the program becomes more than six times faster. The reason is that `a` and `b` are now on different cache lines.

### Lifetime Issues of Variables

Creating a C++ example with lifetime related issues is quite easy. Let the created thread `t` run in the background (i.e. it was detached with a call to `t.detach()`) and let it be only half completed. The creator thread don’t wait until its child is done. In this case, you have to be extremely careful not to use anything in the child thread that belongs to the creator thread.

```
 1 // lifetimeIssues.cpp
 2 
 3 #include <iostream>
 4 #include <string>
 5 #include <thread>
 6 
 7 int main(){
 8     
 9   std::cout << "Begin:" << std::endl;               
10 
11   std::string mess{"Child thread"};
12 
13   std::thread t([&mess]{ std::cout << mess << std::endl;});
14   t.detach();                                   
15   
16   std::cout << "End:" << std::endl;             
17 
18 }
```

Lifetime issues of variables

This is too simple. The thread `t` is using `std::cout` and the variable `mess`. Both belong to the main thread. The effect is that we don’t see the output of the child thread in the second run. Only “Begin:” (line 9) and “End:” (line 16) are printed.

![Lifetime issues of variables](images/Challenges----lifetimeIssues.PNG)

Lifetime issues of variables

### Moving Threads

Moving threads make the [lifetime issues](#chap20.xhtml_chapterXXXLifetimeSSSIssuesSSSofSSSVariables) of threads even harder.

A thread supports the move semantic but not the copy semantic. The reason being the copy constructor of `std::thread` is set to `delete`: `thread(const thread&) = delete;`. Imagine what happens if you copy a thread while the thread is holding a lock.

Let’s move a thread.

```
 1 // threadMoved.cpp
 2 
 3 #include <iostream> 
 4 #include <thread> 
 5 #include <utility>
 6 
 7 int main(){ 
 8 
 9   std::thread t([]{std::cout << std::this_thread::get_id();}); 
10   std::thread t2([]{std::cout << std::this_thread::get_id();}); 
11   
12   t = std::move(t2); 
13   t.join(); 
14   t2.join(); 
15 
16 }
```

Erronous moving a thread

Both threads `t` and `t2` should do their simple job: printing their IDs. In addition to that, thread `t2` is moved to `t` (line 12). In the end, the main thread takes care of its children and joins them. But wait, the result is very different from my expectations:

![Erronous moving a thread](images/Challenges----threadMove.png)

Erronous moving a thread

What is going wrong? We have two issues:

1.  By moving the thread `t2`, `t` gets a new callable unit and its destructor is called. As a result `t`’s destructor calls `std::terminate`, because it is still joinable.
2.  Thread `t2` has no associated callable unit. The invocation of join on a thread without callable unit leads to the exception `std::system_error`.

Knowing this, fixing the errors is straightforward.

```
 1 // threadMovedFixed.cpp
 2 
 3 #include <iostream> 
 4 #include <thread> 
 5 #include <utility>
 6 
 7 int main(){ 
 8 
 9   std::thread t([]{std::cout << std::this_thread::get_id() << std::endl;}); 
10   std::thread t2([]{std::cout << std::this_thread::get_id() << std::endl;}); 
11   
12   t.join();
13   t = std::move(t2); 
14   t.join(); 
15   
16   std::cout << "\n";
17   std::cout << std::boolalpha << "t2.joinable(): " << t2.joinable() << std::endl;
18 
19 }
```

Moving a thread

The result is that thread `t2` is not joinable anymore.

![Erronous moving resolved](images/Challenges----threadMoveFixed.png)

Erronous moving resolved

### Race Conditions

A race condition is a situation, in which the result of an operation depends on the interleaving of certain individual operations.

Race conditions are quite difficult to spot. It depends on the interleaving of the threads whether they occur. That means the number of cores, the utilisation of your system, or the optimisation level of your executable may all be reasons why a race condition appears or does not.

Race conditions are not bad per se. It is the nature of threads that they interleave in different ways, but this can often cause serious problems. In this case, I call them malign race conditions. Typical effects of malign race conditions are [data races](#chap20.xhtml_chapterXXXDataSSSRaces), breaking of [program invariants](#chap20.xhtml_chapterXXXBreakingSSSofSSSProgramSSSInvariants), [blocking issues](#chap20.xhtml_chapterXXXDeadlocks) of threads, or lifetime issues of [variables](#chap20.xhtml_chapterXXXLifetimeSSSIssuesSSSofSSSVariables).

## The Time Library

A book dealing with concurrency in modern C++ would not be complete without writing a chapter about the time library. The time library consists of three parts: time point, time duration, and clock. They depend on each other.

### The Interplay of Time Point, Time Duration, and Clock

Time point

The time point is given by its starting point - the so-called [epoch](https://en.wikipedia.org/wiki/Epoch_(reference_date)) - and the time that has elapsed since the epoch (expressed as a time duration).”

Time duration

The time duration is the difference between two time points. It is measured in the number of time ticks.

Clock

The clock consists of a starting point and a time tick. This information enables you to calculate the current time.

You can compare time points. When you add a time duration to a time point, you get a new time point. The time tick is the accuracy of the clock in which you measure the time duration. The birth of Jesus is in my culture the starting time point and a year is a typical time tick.

I illustrate the three concepts using the lifetime of [Dennis Ritchie](https://en.wikipedia.org/wiki/Dennis_Ritchie). The creator of C who died in 2011\. For the sake of simplicity, I’m only interested in the years.

Here is the lifetime.

![The lifetime of Dennis Ritchie](images/time----ZeitPunktDauerGeberEng.png)

The lifetime of Dennis Ritchie

The birth of Jesus is our epoch. The time points 1941, and 2011 are defined by the epoch and the time duration. Of course, the epoch is also a time point. When I subtract 1941 from 2011, I get the time duration. This dime duration is measured to an accuracy of one year in our example. Dennis Ritchie died at 70.

Let’s dive deeper into the components of the time library.

### Time Point

The time point `std::chrono::time_point` is defined by the starting point (epoch) and the additional time duration. The class template consists of the two components: clock and time duration. By default, the time duration is derived from the clock.

```
template<
  class Clock,
  class Duration= typename Clock::duration
>
class time_point;
```

The class template std::chrono::time_point

The following four special time points depend on the clock:

*   **epoch**: the starting point of the clock
*   **now**: the current time
*   **min**: the minimum time point that the clock can have
*   **max**: the maximum time point that the clock can have

The accuracy of the minimum and maximum time point depends on the clock used: `std::system::system_clock`, `std::chrono::steady_clock`, or `std::chrono::high_resolution_clock`.

C++ gives no guarantee about the accuracy, the starting point or the valid time range of a clock. The starting point of `std::chrono::system_clock` is typically 1st January 1970, the so-called [UNIX-epoch](https://en.wikipedia.org/wiki/Unix_time). It holds further that `std::chrono::high_resolution_clock` has the highest accuracy.

#### From Time Point to Calendar Time

Thanks to `std::chrono::system_clock::to_time_t` you can convert a time point that internally uses `std::chrono::system_clock` to an object of type `std::time_t`. Further conversion of the `std::time_t` object with the function [`std::gmtime`](http://en.cppreference.com/w/cpp/chrono/c/gmtime) gives you the calendar time, expressed in [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (UTC). In the end this calendar time can be used as the input for the function [`std::asctime`](http://en.cppreference.com/w/cpp/chrono/c/asctime) to get a textual representation of the calendar time.

```
 1 // timepoint.cpp
 2 
 3 #include <chrono>
 4 #include <ctime>
 5 #include <iostream>
 6 #include <string>
 7 
 8 int main(){  
 9     
10     std::cout << std::endl;
11     
12     std::chrono::time_point<std::chrono::system_clock> sysTimePoint;
13     std::time_t tp= std::chrono::system_clock::to_time_t(sysTimePoint);
14     std::string sTp= std::asctime(std::gmtime(&tp));
15     std::cout << "Epoch: " << sTp << std::endl;
16     
17     tp= std::chrono::system_clock::to_time_t(sysTimePoint.min());
18     sTp= std::asctime(std::gmtime(&tp));
19     std::cout << "Time min: " << sTp << std::endl;
20     
21     tp= std::chrono::system_clock::to_time_t(sysTimePoint.max());
22     sTp= std::asctime(std::gmtime(&tp));
23     std::cout << "Time max: " << sTp << std::endl;
24     
25     sysTimePoint= std::chrono::system_clock::now();
26     tp= std::chrono::system_clock::to_time_t(sysTimePoint);
27     sTp= std::asctime(std::gmtime(&tp));
28     std::cout << "Time now: " << sTp << std::endl;
29     
30 }
```

Display the calendar time

The output of the program shows the valid range of `std::chrono::system_clock`. On my Linux PC `std::chrono::system_clock` has the UNIX-epoch as starting point and can have time points between the years 1677 and 2262.

![The valid range of std::chrono::system_clock](images/time----timepoint.png)

The valid range of std::chrono::system_clock

You can add time durations to time points to get new time points. Adding time durations beyond the valid time range is undefined behaviour.

#### Cross the valid Time Range

The following example uses the current time and adds or subtracts 1000 years. For the sake of simplicity, I ignore leap years and assume that a year has 365 days.

```
 1 // timepointAddition.cpp
 2 
 3 #include <chrono>
 4 #include <ctime>
 5 #include <iostream>
 6 #include <string>
 7 
 8 using namespace std::chrono;
 9 using namespace std;
10 
11 string timePointAsString(const time_point<system_clock>& timePoint){
12   time_t tp= system_clock::to_time_t(timePoint);
13   return asctime(gmtime(&tp));
14 }
15 
16 int main(){  
17     
18   cout << endl;
19     
20   time_point<system_clock> nowTimePoint= system_clock::now();
21   cout << "Now:              " << timePointAsString(nowTimePoint) << endl;
22      
23   const auto thousandYears=  hours(24*365*1000);
24   time_point<system_clock>  historyTimePoint= nowTimePoint - thousandYears;
25   cout << "Now - 1000 years: " << timePointAsString(historyTimePoint) << endl;
26     
27   time_point<system_clock>  futureTimePoint= nowTimePoint + thousandYears;
28   cout << "Now + 1000 years: " << timePointAsString(futureTimePoint) << endl;
29      
30 }
```

Crossing the valid time range

For readability, I introduced the namespace `std::chrono`. The output of the program shows that an overflow of the time points in lines 25 and 28 causes incorrect results. Subtracting 1000 years from the current time point gives a time point in the future; adding 1000 years to the current time point gives a time point in the past, respectively.

![Overflow of the valid time range](images/time----timepointAddition.png)

Overflow of the valid time range

The difference between two time points is a time duration. Time durations support the basic arithmetic and can be displayed in different time ticks.

### Time Duration

Time duration `std::chrono::duration` is a class template that consists of the type of the tick `Rep` and the length of a tick `Period`.

```
template<
    class Rep,
    class Period = std::ratio<1>
> class duration;
```

The class template std::chrono::duration

The tick length is by default `std::ratio<1>`. `std::ratio<1>` stands for a second and can also be written as `std::ratio<1, 1>`. The rest is quite easy. `std::ratio<60>` is a minute and `std::ratio<1,1000>` a millisecond. When the type of `Rep` is a floating-point number, you can use it to hold fractions of time ticks.

C++11 predefines the most important time durations:

```
typedef duration<signed int, nano> nanoseconds;
typedef duration<signed int, micro> microseconds;
typedef duration<signed int, milli> milliseconds;
typedef duration<signed int> seconds;
typedef duration<signed int, ratio< 60>> minutes;
typedef duration<signed int, ratio<3600>> hours;
```

Important time durations

How much time has passed since the UNIX epoch (1.1.1970)? Thanks to type aliases for the different time durations, I can answer the question quite easily. In the following example, I ignore leap years and assume that a year has 365 days.

```
 1 // timeSinceEpoch.cpp
 2 
 3 #include <chrono>
 4 #include <iostream>
 5 
 6 using namespace std;
 7 
 8 int main(){
 9 
10   cout << fixed << endl;
11   
12   cout << "Time since 1.1.1970:\n" << endl;
13 
14   const auto timeNow= chrono::system_clock::now();
15   const auto duration= timeNow.time_since_epoch();
16   cout << duration.count() << " nanoseconds " << endl;
17 
18   typedef chrono::duration<long double, ratio<1, 1000000>> MyMicroSecondTick;
19   MyMicroSecondTick micro(duration);
20   cout << micro.count() << " microseconds" << endl;
21   
22   typedef chrono::duration<long double, ratio<1, 1000>> MyMilliSecondTick;
23   MyMilliSecondTick milli(duration);
24   cout << milli.count() << " milliseconds" << endl;
25   
26   typedef chrono::duration<long double> MySecondTick;
27   MySecondTick sec(duration);
28   cout << sec.count() << " seconds " << endl;
29   
30   typedef chrono::duration<double, ratio<60>> MyMinuteTick;
31   MyMinuteTick myMinute(duration);
32   cout << myMinute.count() << " minutes" << endl;
33 
34   typedef chrono::duration<double, ratio<60*60>> MyHourTick;
35   MyHourTick myHour(duration);
36   cout << myHour.count() << " hours" << endl;
37   
38   typedef chrono::duration<double, ratio<60*60*24*365>> MyYearTick;
39   MyYearTick myYear(duration);
40   cout << myYear.count() << " years" << endl;
41 
42   typedef chrono::duration<double, ratio<60*45>> MyLessonTick;
43   MyLessonTick myLesson(duration);
44   cout << myLesson.count() << " lessons" << endl;
45 
46   cout << endl;
47 
48 }
```

Crossing the valid time range

The typical time durations are microsecond (line 18), millisecond (line 22), second (line 26), minute (line 30), hour (line 34), and year (line 38). Also, I define the German school hour (45 min) in line 42.

![Time since epoch](images/time----timeSinceEpoch.png)

Time since epoch

It’s quite convenient to calculate with time durations, as the next section illustrates.

#### Calculations

The time durations support basic arithmetic operations. This means that you can multiply or divide a time duration by a number. Of course, you can compare time durations. I explicitly want to emphasise that all these calculations and comparisons respect the units.

With the C++14 standard, it gets even better. The C++14 standard supports the typical time literals.

Predefined time literals

| **Type** | **Suffix** | **Example** |
| --- | --- | --- |
| std::chrono::hours | h | 5h |
| std::chrono::minutes | min | 5min |
| std::chrono::seconds | s | 5s |
| std::chrono::milliseconds | ms | 5ms |
| std::chrono::microseconds | us | 5us |
| std::chrono::nanoseconds | ns | 5ns |

How much time does my 17 years old son Marius spend during a typical school-day? I answer the question in the following example and show the result in various time duration formats.

```
 1 // schoolDay.cpp
 2 
 3 #include <iostream>
 4 #include <chrono>
 5 
 6 using namespace std::literals::chrono_literals;
 7 using namespace std::chrono;
 8 using namespace std;
 9 
10 int main(){
11 
12   cout << endl;
13 
14   constexpr auto schoolHour= 45min;
15 
16   constexpr auto shortBreak= 300s;
17   constexpr auto longBreak= 0.25h;
18 
19   constexpr auto schoolWay= 15min;
20   constexpr auto homework= 2h;
21 
22   constexpr auto schoolDaySec= 2*schoolWay + 6 * schoolHour + 4 * shortBreak + 
23                                longBreak + homework;
24 
25   cout << "School day in seconds: " << schoolDaySec.count() << endl;
26 
27   constexpr duration<double, ratio<3600>> schoolDayHour = schoolDaySec;
28   constexpr duration<double, ratio<60>> schoolDayMin = schoolDaySec;
29   constexpr duration<double, ratio<1,1000>> schoolDayMilli= schoolDaySec;
30 
31   cout << "School day in hours: " << schoolDayHour.count() << endl;
32   cout << "School day in minutes: " << schoolDayMin.count() << endl;
33   cout << "School day in milliseconds: " << schoolDayMilli.count() << endl;
34 
35   cout << endl;
36 
37 }
```

A typical school-day in various time durations

I have time durations for a German school hour (line 14), for a short break (line 16), for an extended break (line 17), for Marius way to school (line 19), and his homework (line 20). The result of the calculation `schoolDaysInSeconds` (line 22) is available at compile time.

![A typical school-day in various time durations](images/time----schoolDay.png)

A typical school-day in various time durations

The accuracy of the time tick is dependent on the clock used. In C++ we have the clocks `std::chrono::system_clock`, `std::chrono::steady_clock`, and `std::chrono::high_resolution_clock`.

### Clocks

The fact that there are three different types of clocks begs the question: What are the differences?

*   **std::chrono::sytem_clock**: is the system-wide real time clock ([wall-clock](https://en.wikipedia.org/wiki/Wall-clock_time)). The clock has the auxiliary functions `to_time_t` and `from_time_t` to [convert time points into calendar time](#chap21.xhtml_chapterXXXFromSSSTimeSSSPointSSStoSSSCalendarSSSTime).
*   **std::chrono::steady_clock**: is the only clock to provide the guarantee that you can not adjust it. Therefore, `std::chrono::steady_clock` is the preferred clock to measure time intervals.
*   **std::chrono::high_resolution_clock**: is the clock with the highest accuracy but it can be simply an alias for the clocks `std::chrono::system_clock` or `std::chrono::steady_clock`.

#### Accuracy and Steadiness

It is quite interesting to know which clocks are steady and what accuracy they provide. Steady means that the clock cannot be adjusted. You can get the answers directly from the clocks.

```
 1 // clockProperties.cpp
 2 
 3 #include <chrono>
 4 #include <iomanip>
 5 #include <iostream>
 6 
 7 using namespace std::chrono;
 8 using namespace std;
 9 
10 template <typename T>
11 void printRatio(){ 
12     cout << "  precision: " << T::num << "/" << T::den << " second " << endl;
13     typedef typename ratio_multiply<T,kilo>::type MillSec;
14     typedef typename ratio_multiply<T,mega>::type MicroSec;
15     cout << fixed;
16     cout << "             " << static_cast<double>(MillSec::num)/MillSec::den 
17                             << " milliseconds " << endl;
18     cout << "             " << static_cast<double>(MicroSec::num)/MicroSec::den 
19                             << " microseconds " << endl;
20 }
21 
22 int main(){
23     
24     cout << boolalpha << endl;
25     
26     cout << "std::chrono::system_clock: " << endl;
27     cout << "  is steady: " << system_clock::is_steady << endl;
28     printRatio<chrono::system_clock::period>();
29     
30     cout << endl;
31     
32     cout << "std::chrono::steady_clock: " << endl;
33     cout << "  is steady: " << chrono::steady_clock::is_steady << endl;
34     printRatio<chrono::steady_clock::period>();
35     
36     cout << endl;
37     
38     cout << "std::chrono::high_resolution_clock: " << endl;
39     cout << "  is steady: " << chrono::high_resolution_clock::is_steady 
40          << endl;
41     printRatio<chrono::high_resolution_clock::period>();
42     
43     cout << endl;
44     
45 }
```

Accuracy and steadiness of the three clocks

I show in lines 27, 33, and 39 for each clock whether it is steady. The function `printRatio` (lines 10 - 20) is more challenging to read. First, I display the accuracy of the clocks as a fraction with the unit in seconds. Additionally, I use the function template `std::ratio_multiply` and the constants `std::kilo` and `std::mega` to adjust the units to milliseconds and microseconds displayed as floating-point numbers. You can get the details of the calculation at compile time at [cppreference.com](http://en.cppreference.com/w/cpp/numeric/ratio).

The output on Linux differs from that on Windows. `std::chrono::system_clock` is far more accurate on Linux; `std::chrono::high_resultion_clock` is steady on Windows.

![Accuracy and steadiness of the three clocks on Linux](images/time----clockProperties.png)

Accuracy and steadiness of the three clocks on Linux

![Accuracy and steadiness of different clocks on Windows](images/time----clockPropertiesWin.png)

Accuracy and steadiness of different clocks on Windows

Although the C++ standard doesn’t specify the epoch of the clock, you can calculate it.

#### Epoch

Thanks to the auxiliary function [`time_since_epoch`](http://en.cppreference.com/w/cpp/chrono/time_point/time_since_epoch), each clock returns how much time has passed since the epoch.

```
 1 // now.cpp
 2 
 3 #include <chrono>
 4 #include <iomanip>
 5 #include <iostream>
 6 
 7 using namespace std::chrono;
 8 
 9 template <typename T>
10 void durationSinceEpoch(const T dur){
11     std::cout << "     Counts since epoch:  " << dur.count() << std::endl;
12     typedef duration<double, std::ratio<60>> MyMinuteTick;
13     const MyMinuteTick myMinute(dur);
14     std::cout << std::fixed;
15     std::cout << "     Minutes since epoch: "<< myMinute.count() << std::endl;
16     typedef duration<double, std::ratio<60*60*24*365>> MyYearTick;
17     const MyYearTick myYear(dur);
18     std::cout << "     Years since epoch:   " << myYear.count() << std::endl;
19 }
20     
21 int main(){
22     
23     std::cout << std::endl;
24     
25     system_clock::time_point timeNowSysClock = system_clock::now(); 
26     system_clock::duration timeDurSysClock= timeNowSysClock.time_since_epoch();
27     std::cout << "system_clock: " << std::endl;
28     durationSinceEpoch(timeDurSysClock);
29     
30     std::cout << std::endl;
31      
32     const auto timeNowStClock = steady_clock::now(); 
33     const auto timeDurStClock= timeNowStClock.time_since_epoch();
34     std::cout << "steady_clock: " << std::endl;
35     durationSinceEpoch(timeDurStClock);
36     
37     std::cout << std::endl;
38     
39     const auto timeNowHiRes = high_resolution_clock::now(); 
40     const auto timeDurHiResClock= timeNowHiRes.time_since_epoch();
41     std::cout << "high_resolution_clock: " << std::endl;
42     durationSinceEpoch(timeDurHiResClock);
43     
44     std::cout << std::endl;
45 
46 }
```

Calculating the epoch for each clock

The variables `timeDurSysClock` (line 26), `timeDurStClock` (line 33), and `timeDurHiResClock` (line 40) contain the amount of time that has passed since the starting point of the corresponding clock. Without automatic type deduction with `auto`, the exact types of the time point and time duration are extremely verbose to write. In the function `durationSinceEpoch` (lines 9 - 19) I display the time duration in different resolutions. First, I display the number of time ticks (line 11), then the number of minutes (line 15), and at the end the years (lines 18) since the epoch. All values depend on the clock used. For the sake of simplicity, I ignore leap years and assume that a year has 365 days.

Once more, the results are different on Linux and Windows.

![The epoch for each clock on Linux](images/time----now.png)

The epoch for each clock on Linux

![The epoch for each clock on Windows](images/time----nowWin.PNG)

The epoch for each clock on Windows

To draw the right conclusion, I have to mention that my Linux PC had been running for about 5 hours (305 minutes) and my Windows PC had been running for more than 6 hours (391 minutes).

`std::chrono::system_clock` and `std::chrono::high_resolution_clock` have the UNIX-epoch as starting point on my linux PC. The starting point of `std::chrono::steady_clock` is the boot time of my PC. While it seems that `std::high_resolution_clock` is an alias for `std::system_clock` on Linux, `std::high_resolution_clock` seems to be an alias for `std::steady_clock` on Windows. This conclusion is in accordance with the result from the previous subsection [Accuracy and Steadiness](#chap21.xhtml_chapterXXXAccuracySSSandSSSSteadiness).

Thanks to the time library, you can put a thread to sleep. The arguments of the sleep and wait functions are time points or time durations.

### Sleep and Wait

One crucial feature that multithreading components such as threads, locks, condition variables, and futures have in common is the notion of time.

##### Conventions

The methods for handling time in multithreading programs follow a simple convention. Methods ending with `_for` have to be parametrised by a [time duration](#chap21.xhtml_chapterXXXTimeSSSPoint); methods ending with `_until` by a [time point](#chap21.xhtml_chapterXXXTimeSSSPoint). Here is a concise overview of the methods dealing with sleeping, blocking, and waiting.

Methods for sleeping, blocking, and waiting

| **Multithreading Component** | **_until** | **_for** |
| --- | --- | --- |
| `std::thread th` | `th.sleep_until(in2min)` | `th.sleep_for(2s)` |
| `std::unique_lock lk` | `lk.try_lock_until(in2min)` | `lk.try_lock(2s)` |
| `std::condition_variable cv` | `cv.wait_until(in2min)` | `cv.wait_for(2s)` |
| `std::future fu` | `fu.wait_until(in2min)` | `fu.wait_for(2s)` |
| `std::shared_future shFu` | `shFu.wait(in2min)` | `shFu.wait_for(2s)` |

`in2min` stands for a time 2 minutes in the future. `2s` is a time duration of 2 seconds. Although I use `auto` in the initialisation of the time point `in2min`, the following is still verbose:

```
auto in2min= std::chrono::steady_clock::now() + std::chrono::minutes(2);
```

Defining a time point

[Time literals](#chap21.xhtml_textXXXhSSSminSSSsSSSmsSSSusSSSns) from C++14 come to our rescue when using time durations. `2s` stands for 2 seconds.

Let’s look at different waiting strategies.

##### Various waiting strategies

The main idea of the following program is that the promise provides its result for four shared futures. That is possible because more than one [`shared_future`](#chap06.xhtml_chapterXXXshared_future) can wait for the notification of the same promise. Each future has a different waiting strategy. Both the promise and every future are executed in different threads. For simplicity reasons I speak in the rest of this subsection only about a waiting thread, although it is the corresponding future that is waiting. Here are the details of the [promises and the futures](#chap06.xhtml_chapterXXXTasks).

Here are the strategies for the four waiting threads:

*   **consumeThread1**: waits up to 4 seconds for the result of the promise.
*   **consumeThread2**: waits up to 20 seconds for the result of the promise.
*   **consumeThread3**: asks the promise for the result and goes back to sleep for 700 milliseconds.
*   **consumeThread4**: asks the promise for the result and goes back to sleep. Its sleep duration starts with one millisecond and doubles each time.

Here is the program.

```
 1 // sleepAndWait.cpp
  2 
  3 #include <utility>
  4 #include <iostream>
  5 #include <future>
  6 #include <thread>
  7 #include <utility>
  8 
  9 using namespace std;
 10 using namespace std::chrono;
 11 
 12 mutex coutMutex;
 13 
 14 long double getDifference(const steady_clock::time_point& tp1, 
 15                           const steady_clock::time_point& tp2){
 16     const auto diff= tp2 - tp1;
 17     const auto res= duration <long double, milli> (diff).count();
 18     return res;
 19 }
 20 
 21 void producer(promise<int>&& prom){
 22     cout << "PRODUCING THE VALUE 2011\n\n"; 
 23     this_thread::sleep_for(seconds(5));
 24     prom.set_value(2011);
 25 }
 26 
 27 void consumer(shared_future<int> fut,
 28               steady_clock::duration dur){
 29     const auto start = steady_clock::now();
 30     future_status status= fut.wait_until(steady_clock::now() + dur);
 31     if ( status == future_status::ready ){
 32         lock_guard<mutex> lockCout(coutMutex);
 33         cout << this_thread::get_id() << " ready => Result: " << fut.get() 
 34              << endl;
 35     }
 36     else{
 37         lock_guard<mutex> lockCout(coutMutex);
 38         cout << this_thread::get_id() << " stopped waiting." << endl;
 39     }
 40     const auto end= steady_clock::now();
 41     lock_guard<mutex> lockCout(coutMutex);
 42     cout << this_thread::get_id() << " waiting time: " 
 43          << getDifference(start,end) << " ms" << endl;
 44 }
 45 
 46 void consumePeriodically(shared_future<int> fut){
 47     const auto start = steady_clock::now();
 48     future_status status;
 49     do {
 50         this_thread::sleep_for(milliseconds(700));
 51         status = fut.wait_for(seconds(0));
 52         if (status == future_status::timeout) {
 53             lock_guard<mutex> lockCout(coutMutex);
 54             cout << "     " << this_thread::get_id() 
 55                  << " still waiting." << endl;
 56         }
 57         if (status == future_status::ready) {
 58             lock_guard<mutex> lockCout(coutMutex);
 59             cout << "     " << this_thread::get_id() 
 60                  << " waiting done => Result: " << fut.get() << endl;
 61         }
 62     } while (status != future_status::ready); 
 63     const auto end= steady_clock::now();
 64     lock_guard<mutex> lockCout(coutMutex);
 65     cout << "     " << this_thread::get_id() << " waiting time: " 
 66          << getDifference(start,end) << " ms" << endl;
 67 }
 68 
 69 void consumeWithBackoff(shared_future<int> fut){
 70     const auto start = steady_clock::now();
 71     future_status status;
 72     auto dur= milliseconds(1);
 73     do {
 74         this_thread::sleep_for(dur);
 75         status = fut.wait_for(seconds(0));
 76         dur *= 2;
 77         if (status == future_status::timeout) {
 78             lock_guard<mutex> lockCout(coutMutex);
 79             cout << "         " << this_thread::get_id() 
 80                  << " still waiting." << endl;
 81         }
 82         if (status == future_status::ready) {
 83             lock_guard<mutex> lockCout(coutMutex);
 84             cout << "         " << this_thread::get_id() 
 85                  << " waiting done => Result: " << fut.get() << endl;
 86         }
 87     } while (status != future_status::ready);
 88     const auto end= steady_clock::now();
 89     lock_guard<mutex> lockCout(coutMutex);
 90     cout << "         " << this_thread::get_id() 
 91          << " waiting time: " << getDifference(start,end) << " ms" << endl;
 92 }
 93 
 94 int main(){
 95     
 96     cout << endl;
 97 
 98     promise<int> prom;
 99     shared_future<int> future= prom.get_future();
100     thread producerThread(producer, move(prom));
101     
102     thread consumerThread1(consumer, future, seconds(4));
103     thread consumerThread2(consumer, future, seconds(20));
104     thread consumerThread3(consumePeriodically, future);
105     thread consumerThread4(consumeWithBackoff, future);
106     
107     consumerThread1.join();
108     consumerThread2.join();
109     consumerThread3.join();
110     consumerThread4.join();
111     producerThread.join();
112     
113     cout << endl;
114 
115 }
```

Various waiting strategies

I create the promise in the main function (line 98), use the promise to create the associated future (line 99) and move the promise into a separate thread (line 100). I have to move the promise into the thread because it does not support the copy semantic. That is not necessary for the shared futures (lines 102 - 105); they support the copy semantic and can hence be copied.

Before I talk about the work package of the thread, let me say a few words about the auxiliary function `getDifference` (lines 14 - 19). The function takes two time points and returns the time duration between this two timepoints in milliseconds. I use the function a few times.

What about the five created threads?

*   **producerThread**: executes the function `producer` (lines 21 - 25) and publishes its result 2011 after 5 seconds of sleep. This is the result the futures are waiting for.
*   **consumerThread1**: executes the function `consumer` (lines 27 - 44). The thread is waiting for at most 4 seconds (line 30) before it continues with its work. This waiting period is not long enough to get the result from the promise.
*   **consumerThread2**: executes the function `consumer` (lines 27 - 44). The thread is waiting at most 20 seconds before it continues with its work.
*   **consumerThread3**: executes the function `consumePeriodically` (lines 46 - 67). It sleeps for 700 milliseconds (line 50) and asks for the result of the promise (line 60). Because of the `std::chrono::seconds(0)` in line 51, there is no waiting. If the result of the calculation is available, it is displayed in line 60.
*   **consumerThread4**: executes the function `consumeWithBackoff` (lines 69 - 92). It sleeps in the first iteration 1 second and doubles its sleeping period every iteration. Otherwise, its strategy is similar to the strategy of `consumerThread3`.

Now to the synchronisation of the program. Both the clock determining the current time and `std::cout` are shared variables, but no synchronisation is necessary. Firstly, the method call `std::chrono::steady_clock::now()` is thread-safe (for example in lines 30 and 40), secondly, the C++ runtime guarantees that the characters are written *thread-safe* to `std::cout`. I only used a `std::lock_guard` to wrap `std::cout` (for example in lines 32, 37, and 41).

Although the threads write one after the other to `std::cout`, the output is not easy to understand.

![Usage of different waiting strategies](images/time----sleepAndWait.png)

Usage of different waiting strategies

The first output is from the promise. The left outputs are from the futures. At first `consumerThread4` asks for the result. 8 characters indent the output. `consumerThread4` also displays its ID. `consumerThread3` immediately follows. 4 characters indent its output. The output of `consumerThread1` and `consumerThread2` is not indented.

*   **consumeThread1**: waits unsuccessfully 4000.18 ms seconds without getting the result.
*   **consumeThread2**: gets the result after 5000.3 ms although its waiting duration is up to 20 seconds.
*   **consumeThread3**: gets the result after 5601.76 ms. That’s about 5600 milliseconds= 8 * 700 milliseconds.
*   **consumeThread4**: gets the result after 8193.81 ms. To say it differently. It waits 3 seconds too long.

## CppMem - An Overview

[CppMem](http://svr-pes20-cppmem.cl.cam.ac.uk/cppmem/) is an interactive tool for exploring the behaviour of small code snippets using the C++ memory model. It has to be in the toolbox of each programmer who seriously deals with the memory model.

The online version of CppMem - you can also install it on your PC - provides valuable services in a twofold way:

1.  CppMem verifies the behaviour of small code snippets. Based on the chosen variant of the C++ memory model, the tool considers all possible interleavings of threads, visualises each of them in a graph and annotates these graphs with additional details.
2.  The very accurate analysis of CppMem gives you deep insight into the C++ memory model. In short, CppMem is a tool that helps you to get a better understanding of the memory model.

Of course, it’s often the nature of powerful tools that you first have to overcome a few hurdles. The nature of things is that CppMem gives you the very detailed analysis related to this incredibly challenging topic and is highly configurable. Therefore, I plan to present the components of the tool.

### The simplified Overview

My simplified overview of CppMem is based on the default configuration. This overview only provides you with the base for further experiments and should help you to understand my process of ongoing optimisation.

![The default configuration of CppMem](images/CaseStudies----CppMemUeberblickNumbers.png)

The default configuration of CppMem

For the sake of simplicity, I refer to the red numbers in the screenshot.

#### 1\. Model

*   Specifies the C++ memory model. *preferred* is a simplified but equivalent variant of the C++11 memory model.

#### 2\. Program

*   Contains the executable program in a simplified C++11 like syntax. To be precise, you cannot directly copy *C or C++* code programs into CppMem.
*   You can choose between many programs that implement typical multithreading scenarios. To get the details of these programs read the very well written article [Mathematizing C++ Concurrency](http://www.cl.cam.ac.uk/~pes20/cpp/popl085ap-sewell.pdf). Of course, you can also run your code.
*   CppMem is about multithreading; therefore, there are shortcuts for multithreading available.
    *   You can easily define two threads using the expression `{{{ ... ||| ... }}}`. The three dots `(...)` represents the work package of each thread.
    *   If you use the expression `x.readvalue(1)`, CppMem evaluates the interleavings of the threads for which the thread execution gives the value `1` for `x`.

#### 3\. Display Relations

*   Describes the relations between the read, write and read-write modifications on atomic operations, fences and locks.
*   You can explicitly enable the relations in the annotated graph with the checkboxes.
*   There are three classes of relations. The coarser distinction between original and derived relations is the most interesting one. Here are the default values.
    *   Original relations:
        *   **sb**: sequenced-before
        *   **rf**: read from
        *   **mo**: modification order
        *   **sc**: sequentially consistent
        *   **lo**: lock order
    *   Derived relations:
        *   **sw**: synchronises-with
        *   **dob**: dependency-ordered-before
        *   **unsequenced_races**: races in a single thread
        *   **data_races**: inter-thread data races

#### 4\. Display Layout

*   With this switch you can choose, which [Doxygraph](https://sourceforge.net/projects/doxygraph/) graph is used.

#### 5\. Model Predicates

*   With this button, you can set the predicates for the chosen model, that can cause a non-consistent (not data-race-free) execution; therefore, if you get a non-consistent execution, you see exactly the reason for the non-consistent execution. I do not use this buttons in this book.

See the [documentation](http://svr-pes20-cppmem.cl.cam.ac.uk/cppmem/help.html) for more details.

This is sufficient as a starting point for CppMem. Now, it is time to give CppMem a try.

CppMem provides many examples.

#### The Examples

The examples show typical use-case when working with concurrent and in particular with lock-free code. The examples are grouped into categories.

##### Paper

The `examples/Paper` category gives you a few examples which are intensely discussed in the paper [Mathematizing C++ Concurrency](https://www.cl.cam.ac.uk/~pes20/cpp/popl085ap-sewell.pdf).

*   `data_race.c`: data race on x
*   `partial_sb.c`: sequenced-before to the evaluation order in a single-threaded program
*   `unsequenced_race.c`: unsequenced race on x according to the evaluation order
*   `sc_atomics.c`: correct use of atomics
*   `thread_create_and_asw.c`: additional synchronize-with due thread creation

Let’s start with the first example.

###### The Test Run

Choose the program `data_race.c` from the CppMem samples. The run button shows immediately there is a [data race](#chap20.xhtml_chapterXXXDataSSSRaces).

![A data race with CppMem](images/CaseStudies----CppMemUeberblickNumbersRun.png)

A data race with CppMem

For simplicity, I refer to the red numbers in my explanation.

1.  The data race is quite easy to see. A thread writes `x (x = 3)` and another thread reads `x (x==3)` without synchronisation.
2.  Two interleavings of threads are possible due to the C++ memory model. Only one of them is consistent with the chosen model. This is the case if, in the expression `x==3`, the value of x is written by the expression `int x = 2` in the main function. The graph displays this relation in the edge annotated with rf and sw.
3.  Switching between the different interleaving of threads is fascinating.
4.  The graph shows all relations, which you enabled in the Display Relations.

*   `a:Wna x=2` is in the graphic the a-th statement, which is a non-atomic write. `Wna` stands for “Write non-atomic”.
*   The key edge in the graph is the edge between the writing of `x (b:Wna)` and the reading of `x (C:Rna)`. That’s the data race on `x`.

##### Further Categories

The further categories focus on specific aspects of lock-free programming. The example of each category is available in various forms. Each form using different memory orderings. For an additional discussion to the categories, read the already mentioned paper [Mathematizing C++ Concurrency](https://www.cl.cam.ac.uk/~pes20/cpp/popl085ap-sewell.pdf). If possible, I present the program with [sequential consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency).

###### Store Buffering (`examples/SB_store_buffering`)

Two threads write to separate locations and then read from the other location.

```
// SB+sc_sc+sc_sc
// Store Buffering (or Dekker's), with all four accesses SC atomics
// Question: can the two reads both see 0 in the same execution?
int main() {
  atomic_int x=0; atomic_int y=0;
  {{{ { y.store(1,memory_order_seq_cst);
        r1=x.load(memory_order_seq_cst); }
  ||| { x.store(1,memory_order_seq_cst);
        r2=y.load(memory_order_seq_cst); }  }}}
  return 0;
}
```

SB+sc_sc+sc_sc+sc.c

###### Message Passing (`examples/MP_message_passing`)

One thread writes data (non-atomic) and the sets an atomic flag while the second thread waits for the flag an read data (non-atomic).

```
// MP+na_sc+sc_na
// Message Passing, of data held in non-atomic x,
//   with sc atomic stores and loads on y  giving release/acquire synchronisation
// Question: is the read of x required to see the new data value 1
//   rather than the initial state value 0?
int main() {
  int x=0; atomic_int y=0;
  {{{ { x=1;
        y.store(1,memory_order_seq_cst); }
  ||| { r1=y.load(memory_order_seq_cst).readsvalue(1);
        r2=x; }  }}}
  return 0;
}
```

MP+na_sc+sc_na.c

###### Load Buffering (`examples/LB_load_buffering`)

Can two reads see the later write of the other thread?

```
// LB+sc_sc+sc_sc
// Load Buffering, with all four accesses sequentially consistent atomics
// Question: can the two reads both see 1 in the same execution?
int main() {
  atomic_int x=0; atomic_int y=0;
  {{{ { r1=x.load(memory_order_seq_cst); 
        y.store(1,memory_order_seq_cst); }
  ||| { r2=y.load(memory_order_seq_cst);
        x.store(1,memory_order_seq_cst); }  }}}
  return 0;
}
```

Lb+sc_sc+sc_sc.c

###### Write-to-Read Causality (`examples/WRC`)

Does the third thread see the write from the first thread? * The first thread writes to `x`. * The second thread reads from that and the writes to `y`. * The third thread reads from that and then reads `x`.

```
// WRC
// the question is whether the final read is required to see 1
// With two release/acquire pairs, it is
int main() {
  atomic_int x = 0;
  atomic_int y = 0;

  {{{ x.store(1,mo_release);
  ||| { r1=x.load(mo_acquire).readsvalue(1);
        y.store(1,mo_release); }
  ||| { r2=y.load(mo_acquire).readsvalue(1);
        r3=x.load(mo_relaxed); }
  }}}
  return 0;
}
```

WRC+rel+acq_rel+acq_rlx.c

###### Independent Reads of Independent Writes (`examples\IRIW`)

Two threads write to different locations. Can the second thread see those writes in a different order?

```
// IRIW with release/acquire
// the question is whether the reading threads have
// to see the writes to x and y in the same order.
// With release/acquire, they do not.
int main() {
  atomic_int x = 0; atomic_int y = 0;
  {{{ x.store(1, memory_order_release);
  ||| y.store(1, memory_order_release);
  ||| { r1=x.load(memory_order_acquire).readsvalue(1);
        r2=y.load(memory_order_acquire).readsvalue(0); }
  ||| { r3=y.load(memory_order_acquire).readsvalue(1);
        r4=x.load(memory_order_acquire).readsvalue(0); }
  }}};
  return 0; 
}
```

IRIW+rel+rel+acq_acq+acq_acq.c

## Glossary

The idea of this glossary is by no means to be exhaustive but to provide a reference for the essential terms.

### ACID

A transaction is an action that has the properties **A**tomicity, **C**onsistency, **I**solation, and **D**urability (ACID). Except for durability, all properties hold for transactional memory in C++.

*   **Atomicity**: either all or no statement of the block is performed.
*   **Consistency**: the system is always in a consistent state. All transactions build a [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC).
*   **Isolation**: each transaction runs in complete isolation from the other transactions.
*   **Durability** a transaction is recorded.

### CAS

CAS stands for *compare-and_swap* and is an atomic operation. It compares an memory location with a given value and modifies the memory location if the memory location and the given value are the same. The CAS operations in C++ are called [`std::compare_exchange_strong`, and `std::compare_exchange_weak`](#chap05.xhtml_textXXXcompare_exchange_strongZZZcompare_exchange_weakZZZCAS).

### Callable Unit

A callable unit (short callable) is something that behaves like a function. Not only are these named functions but also function objects and lambda functions. If a callable accepts one argument, it’s called unary callable; if taking two arguments, binary callable.

### Complexity

O(i) stands for the complexity (runtime) of an operation. So O(1) means that the runtime of an operation on a container is constant and is independent of the size of the container. Opposite to that, O(n) means, that the runtime depends linear on the number of the elements of the container.

[Predicates](#chap23.xhtml_glossaryXXXPredicate) are special callables that return a boolean as a result.

### Concurrency

Concurrency means that the execution of several tasks overlaps. Concurrency is a superset of [parallelism](#chap23.xhtml_glossaryXXXParallelism).

### Critical Section

A critical section is a section of code which at most one thread can use at a time.

### Eager Evaluation

In case of eager evaluation, the expression is evaluated immediately. This evaluation strategy is orthogonal to [lazy evaluation](#chap23.xhtml_glossaryyXXXLazySSSevaluationSSSBOBOBOGlossaryBCBCBC). Eager evaluation is often called greedy evaluation.

### Executor

An executor is an object associated with a specific execution context. It provides one or more execution functions for creating execution agents from a callable function object.

### Function Objects

First of all, don’t call them [functors](https://en.wikipedia.org/wiki/Functor). That’s a *well-defined* term from a branch of mathematics called [category theory](https://en.wikipedia.org/wiki/Category_theory).

Function objects are objects that behave like functions. They achieve this by implementing the function call operator. As function objects are objects, they can have attributes and, therefore, state.

```
struct Square{
  void operator()(int& i){i= i*i;}
};

std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

std::for_each(myVec.begin(), myVec.end(), Square());

for (auto v: myVec) std::cout << v << " "; // 1 4 9 16 25 36 49 64 81 100
```

### Lambda Functions

Lambda functions provide their functionality in-place. The compiler gets its information right on the spot and has therefore excellent optimisation potential. Lambda functions can receive their arguments by value or by reference. They can capture the variables of their defining environment by value or by reference as well.

```
std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
std::for_each(myVec.begin(), myVec.end(), [](int& i){ i= i*i; });
                                        // 1 4 9 16 25 36 49 64 81 100
```

### Lazy evaluation

In the case of [lazy evaluation](https://en.wikipedia.org/wiki/Lazy_evaluation) the expression is only be evaluated if needed. This evaluation strategy is orthogonal to [eager evaluation](#chap23.xhtml_glossaryyXXXEagerSSSevaluationSSSBOBOBOGlossaryBCBCBC). Lazy evaluation is often called call-by-need.

### Lock-free

A non-blocking algorithm is lock-free if there is guaranteed system-wide progress.

### Lost Wakeup

A lost wakeup is a situation in which a thread misses its wakeup notification due to a [race condition](#chap20.xhtml_chapterXXXRaceSSSCondition).

That may happen if you use a [condition variable without a predicate](#chap20.xhtml_chapterXXXBlockingSSSIssues).

### Math Laws

A binary operation (*) on some set X is

*   **associative** , if it satisfies the associative law for all x, y, z in X: (x * y) * z = x * (y * z)

*   **commutative** , if it satisfies the commutative law for all x, y in X: x * y = y * x

### Memory Location

A memory location is according to [cppreference.com](http://en.cppreference.com/w/cpp/language/memory_model)

*   an object of scalar type (arithmetic type, pointer type, enumeration type, or `std::nullptr_t),
*   or the largest contiguous sequence of bit fields of non-zero length.

### Memory Model

The memory model defines the relation between objects and [memory location](#chap23.xhtml_glossaryXXXMemorySSSLocation) and deals in particular with the question: What happens if two threads access the same memory locations.

### Modification Order

All modifications to a particular atomic object M occur in some particular [total order](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC). This total order is called the modification order of M. Consequently, reads of an atomic object by a particular thread never sees “older” values than those the thread has already observed.

### Monad

Haskell as a pure functional language has only pure functions. A key feature of these pure functions is that they always return the same result when given the same arguments. Thanks to this property called [referential transparency](https://en.wikipedia.org/wiki/Referential_transparency) a Haskell function cannot have side effects; therefore, Haskell has a conceptional issue. The world is full of calculations that have side effects. These are calculations that can fail, that can return an unknown number of results, or that are dependent on the environment. To solve this conceptional issue, Haskell uses monads and embeds them in the pure functional language.

The classical monads encapsulate one side effect:

*   **I/O monad**: Calculations that deal with input and output.
*   **Maybe monad**: Calculations that maybe return a result.
*   **Error monad**: Calculations that can fail.
*   **List monad**: Calculations that can have an arbitrary number of results.
*   **State monad**: Calculations that build a state.
*   **Reader monad**: Calculations that read from the environment.

The concept of the monad is from [category theory](https://en.wikipedia.org/wiki/Category_theory), which is a part of the mathematics that deals with objects and mapping between these objects. Monads are abstract data types (type classes), which transform simple types into enriched types. Values of these enriched type are called monadic values. Once in a monad, a value can only be transformed by a function composition into another monadic value.

This composition respects the unique structure of a monad; therefore, the error monad interrupts its calculation, if an error occurs or the state monad builds its state.

A monad consists of three components:

*   **Type constructor**: The type constructor defines how the simple data type becomes a monadic data type.
*   **Functions**:
    *   **Identity function**: Introduces a simple value into the monad.
    *   **Bind operator**: Defines how a function is applied to a monadic value to get a new monadic value.
*   **Rules for the functions**:
    *   The identity function has to be the left and the right identity element.
    *   The composition of functions has to be associative.

For the error monad to become an instance of the type class monad, the error monad has to support the identity function and the bind operator. Both functions define how the error monad deals with an error in the calculation. If you use an error monad, the error handling is done in the background.

A monad consists of two control flows. The explicit control for calculating the result and the implicit control flow for dealing with the specific side effect.

Of course, you can define monad in fewer words: “A monad is just a monoid in the category of endofunctors.”

Monads are becoming more and more import in C++. With C++17 we get [std::optional](http://en.cppreference.com/w/cpp/utility/optional) which is a kind of a Maybe monad. With C++20/23 we will probably get [extended futures](#chap10.xhtml_chapterXXXExtendedSSSFutures) and the [ranges library](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4128.html) from Eric Niebler. Both are monads.

### Non-blocking

An algorithm is called non-blocking if failure or suspension of any thread cannot cause failure or suspension of another thread. This definition is from the excellent book [Java concurrency in practice](http://jcip.net/).

### Parallelism

Parallelism means that several tasks are performed at the same time. Parallelism is a subset of [Concurrency](#chap23.xhtml_glossaryXXXConcurrency).

### Predicate

Predicates are [callable units](#chap23.xhtml_glossaryXXXCallableSSSUnit) that return a boolean as a result. If a predicate has one argument, it’s called a unary predicate. If a predicate has two arguments, it’s called a binary predicate.

### Pattern

“Each pattern is a three-part rule, which express a relation between a certain context, a problem, and a solution.” [Christopher Alexander](https://en.wikipedia.org/wiki/Christopher_Alexander)

### RAII

**R**esource **A**cquisition **I**s **I**nitialization, in short RAII, stands for a popular technique in C++, in which the resource acquisition and release are bound to the lifetime of an object. This means for a lock that the mutex will be locked in the constructor and unlocked in the destructor. This RAII implementation is also known as [scoped locking](#chap13.xhtml_chapterXXXScopedSSSLockingSSSBOBOBOPatternBCBCBC).

Typical use cases in C++ are [locks](#chap06.xhtml_chapterXXXLocks) that handle the lifetime of its underlying [mutex](#chap06.xhtml_chapterXXXMutexes), smart pointers that handle the lifetime of its resource (memory), or [containers of the standard template library](https://en.cppreference.com/w/cpp/container) that handle the lifetime of its elements.

### Release Sequence

A release sequence headed by a release operation A on an atomic object M is a maximal contiguous sub-sequence of side effects in the modification order of M, where the first operation is A, and every subsequent operation

*   is performed by the same thread that performed A, or
*   is an atomic read-modify-write operation.

### Sequential Consistency

Sequential consistency has two essential characteristics:

1.  The instructions of a program are executed in source code order.
2.  There is a global order of all operations on all threads.

### Sequence Point

A sequence point defines any point in the execution of a program at which it is guaranteed that all effects of previous evaluations have been performed, and no effects from subsequent evaluations have yet been performed.

### Spurious Wakeup

A spurious wakeup is a phenomenon of condition variables. It may happen that the waiting component of the condition variable erroneously gets a notification, although the notification component didn’t notify it.

### Thread

In computer science, a thread of execution is the smallest sequence of programmed instructions that can be managed independently by a scheduler, which is typically a part of the operating system. The implementation of threads and processes differs between operating systems, but in most cases, a thread is a component of a process. Multiple threads can exist within one process, executing concurrently and sharing resources such as memory, while different processes do not share these resources. In particular, the threads of a process share its executable code and the values of its variables at any given time. For the details, read the Wikipedia article about [threads](https://en.wikipedia.org/wiki/Thread_(computing)).

### Total order

A total order is a binary relation (<=) on some set X which is antisymmetric, transitive, and total.

*   **Antisymmetric**: if a <= b and b <= a then a == b
*   **Transitivity**: if a <= b and b <= c then a <= c
*   **Totality**: a <= b or b <= a

Applied to concurrency, the definition of total order becomes quite handy. Actions such as operation on the same atomic variable or transaction build a total order. This mean, all threads see the effects of this actions in the same order.

### TriviallyCopyable

TriviallyCopyable objects can be copied by copying their object representations manually (`std::memmove`). All data types compatible with the C language (POD types) are trivially copyable.

Formally, TriviallyCopyable is a concept that has to fulfil the following requirements:

*   Every copy constructor is trivial or deleted
*   Every move constructor is trivial or deleted
*   Every copy assignment operator is trivial or deleted
*   Every move assignment operator is trivial or deleted
*   at least one copy constructor, move constructor, copy assignment operator, or move assignment operator is non-deleted
*   Trivial non-deleted destructor

This implies that the class has no virtual functions or virtual base classes. Trivial in essence means that non of the specified special methods is user-defined. This includes also all base classes and non-static class types.

### volatile

`volatile` is typically used to denote objects which can change independently of the regular program flow. These are, for example, objects in embedded programming which represent an external device (memory-mapped I/O). Because these objects can change independently of the regular program flow and their value is directly be written into main memory, no optimised storing in caches takes place.

### wait-free

A non-blocking algorithm is wait-free if there is guaranteed per-thread progress.

## Index

Entries in capital letters stand for sections and subsections.

| **A** | [async](#chap06.xhtml_chapterXXXasync) |
| [A Cooperatively Interruptible Joining Thread](#chap08.xhtml_chapterXXXASSSCooperativelySSSInterruptibleSSSJoiningSSSThread) | [Atomic Operations on shared_ptr](#chap05.xhtml_chapterXXXAtomicSSSOperationsSSSonSSSshared_ptr) |
| [A Generator Function](#chap08.xhtml_chapterXXXASSSGeneratorSSSFunction) | [Atomic Smart Pointers](#chap08.xhtml_chapterXXXAtomicSSSSmartSSSPointers) |
| [A Quick Overview](#chap02.xhtml_PartXXXASSSQuickSSSOverview) | [atomic<arithmetic type>](#chap05.xhtml_chapterXXXatomicBBBarithmeticSSStypeEEE) |
| [A Simple Queue](#chap17.xhtml_textXXXASSSSimpleSSSQueueZZZpopCCCSimpleSSSQueueZZZpushCCCSimpleSSSQueue) | [atomic<bool>](#chap05.xhtml_chapterXXXatomicBBBboolEEE) |
| [A thread-safe singly linked list](#chap08.xhtml_chapterXXXASSSthread-safeSSSsinglySSSlinkedSSSlist) | [atomic<shared_ptr<T>>](#chap08.xhtml_textXXXatomic_shared_ptrZZZatomic_weak_ptrZZZatomicBBBshared_ptrBBBTEEEEEEZZZatomicBBBweak_ptrBBBTEEEEEE) |
| [ABA](#chap20.xhtml_chapterXXXABA) | [atomic<T*>](#chap05.xhtml_chapterXXXatomicBBBTIIIEEE) |
| [abi_for_size](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) | [atomic<user-defined typel>](#chap05.xhtml_chapterXXXatomicBBBuserMMMdefinedSSStypelEEE) |
| [abi_for_size_t](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) | [atomic<weak_ptr<T>>](#chap08.xhtml_textXXXatomic_shared_ptrZZZatomic_weak_ptrZZZatomicBBBshared_ptrBBBTEEEEEEZZZatomicBBBweak_ptrBBBTEEEEEE) |
| [accumulate](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) | [atomic_bool](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [Accuracy and Steadiness](#chap21.xhtml_chapterXXXAccuracySSSandSSSSteadiness) | [atomic_cancel](#chap10.xhtml_textXXXatomic_noexceptZZZatomic_commitZZZatomic_cancelZZZtransaction-unsafe) |
| [ACI(D)](#chap10.xhtml_chapterXXXACIBOBOBODBCBCBC) | [atomic_char16_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [ACID (Glossary)](#chap23.xhtml_glossaryXXXACIDSSSBOBOBOGlossaryBCBCBC) | [atomic_char32_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [acquire fence](#chap05.xhtml_textXXXfullSSSfenceZZZacquireSSSfenceZZZreleaseSSSfence) | [atomic_char8_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [Acquire-Release Fences](#chap05.xhtml_chapterXXXAcquireMMMReleaseSSSFences) | [atomic_char](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [Acquire-Release Semantic](#chap05.xhtml_chapterXXXAcquire-ReleaseSSSSemantic) | [atomic_clear](#chap05.xhtml_textXXXatomic_test_and_setZZZatomic_test_and_set_explicitZZZatomic_clearZZZatomic_clear_explicit) |
| [acquire](#chap08.xhtml_textXXXcountingSSSsemaphoresZZZmaxSSSBOBOBOcounting_semaphoreBCBCBCZZZreleaseSSSBOBOBOcounting_semaphoreBCBCBCZZZacquireZZZtry_acquireZZZtry_acquire_forZZZtry_acquire_until) | [atomic_clear_explicit](#chap05.xhtml_textXXXatomic_test_and_setZZZatomic_test_and_set_explicitZZZatomic_clearZZZatomic_clear_explicit) |
| [Active Object](#chap14.xhtml_chapterXXXActiveSSSObject) | [atomic_commit](#chap10.xhtml_textXXXatomic_noexceptZZZatomic_commitZZZatomic_cancelZZZtransaction-unsafe) |
| [adopt_lock](#chap06.xhtml_textXXXdefer_lockZZZadopt_lock) | [atomic_int16_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [All Atomic Operations](#chap05.xhtml_chapterXXXAllSSSAtomicSSSOperations) | [atomic_int32_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [All Atomic Operations](#chap05.xhtml_chapterXXXAllSSSAtomicSSSOperations) | [atomic_int64_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [All Multithreading Numbers with a Shared Variable](#chap09.xhtml_chapterXXXAllSSSMultithreadingSSSNumbersSSSwithSSSaSSSSharedSSSVariable) | [atomic_int8_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [All Single Threaded Numbers](#chap09.xhtml_chapterXXXAllSSSSingleSSSThreadedSSSNumbers) | [atomic_int](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [all_of](#chap10.xhtml_textXXXall_ofZZZany_ofZZZnone_ofZZZsome_ofZZZpopcountZZZfind_first_setZZZfind_last_set) | [atomic_int_fast16_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [An Infinite Data Stream with co_yield](#chap08.xhtml_chapterXXXAnSSSInfiniteSSSDataSSSStreamSSSwithSSSco_yield) | [atomic_int_fast32_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [Anti-Pattern (Pattern)](#chap12.xhtml_chapterXXXAnti-PatternSSSBOBOBOPatternBCBCBC) | [atomic_int_fast64_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [any_of](#chap10.xhtml_textXXXall_ofZZZany_ofZZZnone_ofZZZsome_ofZZZpopcountZZZfind_first_setZZZfind_last_set) | [atomic_int_fast8_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [arrive](#chap08.xhtml_textXXXarriveZZZwaitSSSBOBOBObarrierBCBCBCZZZarrive_and_waitSSSBOBOBObarrierBCBCBCZZZarrive_and_drop) | [atomic_int_least16_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [arrive_and_drop](#chap08.xhtml_textXXXarriveZZZwaitSSSBOBOBObarrierBCBCBCZZZarrive_and_waitSSSBOBOBObarrierBCBCBCZZZarrive_and_drop) | [atomic_int_least32_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [arrive_and_wait (barrier)](#chap08.xhtml_textXXXarriveZZZwaitSSSBOBOBObarrierBCBCBCZZZarrive_and_waitSSSBOBOBObarrierBCBCBCZZZarrive_and_drop) | [atomic_int_least64_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [arrive_and_wait (latch)](#chap08.xhtml_textXXXcount_downZZZtry_waitZZZarrive_and_waitSSSBOBOBOlatchBCBCBCZZZwaitSSSBOBOBOlatchBCBCBC) | [atomic_int_least8_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [asctime](#chap21.xhtml_textXXXto_time_tZZZtime_tZZZgmtimeZZZasctime) | [atomic_intmax_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [Asio](#chap24.xhtml_textXXXAsioZZZBoost.Asio) | [atomic_intptr_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |
| [associative (Glossary)](#chap23.xhtml_glossaryXXXassociativeSSSBOBOBOGlossaryBCBCBC) | [atomic_llong](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) |

| [atomic_long](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [barrier](#chap08.xhtml_chapterXXXbarrier) |
| [atomic_noexcept](#chap10.xhtml_textXXXatomic_noexceptZZZatomic_commitZZZatomic_cancelZZZtransaction-unsafe) | [Basics of the Memory Model](#chap05.xhtml_chapterXXXBasicsSSSofSSStheSSSMemorySSSModel) |
| [atomic_ptrdiff_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Best Practices](#chap15.xhtml_chapterXXXBestSSSPractices) |
| [atomic_schar](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Blocking Issues](#chap20.xhtml_chapterXXXBlockingSSSIssues) |
| [atomic_shared_ptr](#chap08.xhtml_textXXXatomic_shared_ptrZZZatomic_weak_ptrZZZatomicBBBshared_ptrBBBTEEEEEEZZZatomicBBBweak_ptrBBBTEEEEEE) | [Boost.Asio](#chap24.xhtml_textXXXAsioZZZBoost.Asio) |
| [atomic_short](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Breaking of Program Invariants](#chap20.xhtml_chapterXXXBreakingSSSofSSSProgramSSSInvariants) |
| [atomic_signal_fence](#chap05.xhtml_chapterXXXatomic_signal_fence) | [busy waiting](#chap05.xhtml_textXXXbusySSSwaiting) |
| [atomic_signed_lock_free](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | **C** |
| [atomic_size_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Calculating the Sum of a Vector](#chap09.xhtml_chapterXXXCalculatingSSStheSSSSumSSSofSSSaSSSVector) |
| [atomic_test_and_set](#chap05.xhtml_textXXXatomic_test_and_setZZZatomic_test_and_set_explicitZZZatomic_clearZZZatomic_clear_explicit) | [Calculations](#chap21.xhtml_chapterXXXCalculations) |
| [atomic_test_and_set_explicit](#chap05.xhtml_textXXXatomic_test_and_setZZZatomic_test_and_set_explicitZZZatomic_clearZZZatomic_clear_explicit) | [call_once](#chap06.xhtml_chapterXXXcall_onceZZZonce_flag) |
| [atomic_thread_fence](#chap05.xhtml_chapterXXXatomic_thread_fence) | [callable (Glossary)](#chap23.xhtml_glossaryXXXCallableSSSUnitZZZcallableSSSBOBOBOGlossaryBCBCBC) |
| [atomic_uchar](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Callable Unit](#chap23.xhtml_glossaryXXXCallableSSSUnitZZZcallableSSSBOBOBOGlossaryBCBCBC) |
| [atomic_uint16_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [caries-a-dependency](#chap05.xhtml_textXXXcaries-a-dependencyZZZdependency-order-before) |
| [atomic_uint32_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [CAS](#chap23.xhtml_glossaryXXXCAS) |
| [atomic_uint64_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [CAS](#chap05.xhtml_textXXXcompare_exchange_strongZZZcompare_exchange_weakZZZCAS) |
| [atomic_uint8_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Case Studies](#chap09.xhtml_chapterXXXCaseSSSStudies) |
| [atomic_uint](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [catch fire semantic](#chap09.xhtml_textXXXcatchSSSfireSSSsemantic) |
| [atomic_uint_fast16_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Challenges](#chap20.xhtml_chapterXXXChallenges) |
| [atomic_uint_fast32_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [clamp](#chap10.xhtml_textXXXminSSSBOBOBOsimdBCBCBCZZZmaxSSSBOBOBOsimdBCBCBCZZZminmaxZZZclamp) |
| [atomic_uint_fast64_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [clear](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [atomic_uint_fast8_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Clocks](#chap21.xhtml_chapterXXXClocks) |
| [atomic_uint_least16_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [co_await](#chap08.xhtml_chapterXXXco_awaitZZZco_yieldZZZco_return) |
| [atomic_uint_least32_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [co_return](#chap08.xhtml_chapterXXXco_awaitZZZco_yieldZZZco_return) |
| [atomic_uint_least64_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [co_yield](#chap08.xhtml_chapterXXXco_awaitZZZco_yieldZZZco_return) |
| [atomic_uint_least8_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [commutative (Glossary)](#chap23.xhtml_glossaryXXXcommutativeSSSBOBOBOGlossaryBCBCBC) |
| [atomic_uintmax_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [compare_exchange_strong](#chap05.xhtml_textXXXcompare_exchange_strongZZZcompare_exchange_weakZZZCAS) |
| [atomic_uintptr_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [compare_exchange_weak](#chap05.xhtml_textXXXcompare_exchange_strongZZZcompare_exchange_weakZZZCAS) |
| [atomic_ullong](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [compatible](#chap10.xhtml_textXXXscalarZZZfixed_sizeZZZcompatibleZZZnativeZZZmax_fixed_size) |
| [atomic_ulong](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [complexity (Glossary)](#chap23.xhtml_glossaryXXXcomplexitySSSBOBOBOGlossaryBCBCBC) |
| [atomic_unsigned_lock_free](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [concat](#chap10.xhtml_textXXXsimd_castZZZstatic_simd_castZZZto_fixed_sizeZZZto_compatibleZZZto_nativeZZZsplitZZZconcat) |
| [atomic_ushort](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Concurrency (Glossary)](#chap23.xhtml_glossaryXXXConcurrencySSSBOBOBOGlossaryBCBCBC) |
| [atomic_wchar_t](#chap05.xhtml_textXXXatomic_boolZZZatomic_charZZZatomic_scharZZZatomic_ucharZZZatomic_shortZZZatomic_ushortZZZatomic_intZZZatomic_uintZZZatomic_longZZZatomic_ulongZZZatomic_llongZZZatomic_ullongZZZatomic_char16_tZZZatomic_char32_tZZZatomic_wchar_tZZZatomic_int8_tZZZatomic_uint8_tZZZatomic_int16_tZZZatomic_uint16_tZZZatomic_int32_tZZZatomic_uint32_tZZZatomic_int64_tZZZatomic_uint64_tZZZatomic_int_least8_tZZZatomic_uint_least8_tZZZatomic_int_least16_tZZZatomic_uint_least16_tZZZatomic_int_least32_tZZZatomic_uint_least32_tZZZatomic_int_least64_tZZZatomic_uint_least64_tZZZatomic_int_fast8_tZZZatomic_uint_fast8_tZZZatomic_int_fast16_tZZZatomic_uint_fast16_tZZZatomic_int_fast32_tZZZatomic_uint_fast32_tZZZatomic_int_fast64_tZZZatomic_uint_fast64_tZZZatomic_intptr_tZZZatomic_uintptr_tZZZatomic_size_tZZZatomic_ptrdiff_tZZZatomic_intmax_tZZZatomic_uintmax_tZZZatomic_signed_lock_freeZZZatomic_unsigned_lock_freeZZZatomic_char8_t) | [Concurrent Architectur](#chap14.xhtml_chapterXXXConcurrentSSSArchitectur) |
| [atomic_weak_ptr](#chap08.xhtml_textXXXatomic_shared_ptrZZZatomic_weak_ptrZZZatomicBBBshared_ptrBBBTEEEEEEZZZatomicBBBweak_ptrBBBTEEEEEE) | [Concurrent Calcuation](#chap06.xhtml_chaperXXXConcurrentSSSCalcuation) |
| [atomicity](#chap10.xhtml_textXXXatomicityZZZconsistencyZZZisolationZZZdurability) | [Concurrent Object](#chap14.xhtml_textXXXConcurrentSSSObject) |
| [Atomics](#chap05.xhtml_chapterXXXAtomics) | [Concurrent Queue (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXConcurrentSSSQueueSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) |
| [Avoidance of Loopholes (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXAvoidanceSSSofSSSLoopholesSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) | [Concurrent Stack (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXConcurrentSSSStackSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) |
| [await_ready](#chap08.xhtml_textXXXawait_readyZZZawait_suspendZZZawait_resume) | [Condition Variables](#chap06.xhtml_chapterXXXConditionSSSVariablesZZZcondition_variable) |
| [await_resume](#chap08.xhtml_textXXXawait_readyZZZawait_suspendZZZawait_resume) | [condition_variable](#chap06.xhtml_chapterXXXConditionSSSVariablesZZZcondition_variable) |
| [await_suspend](#chap08.xhtml_textXXXawait_readyZZZawait_suspendZZZawait_resume) | [condition_variable_any](#chap06.xhtml_textXXXcondition_variable_any) |
| **B** | [consistency](#chap10.xhtml_textXXXatomicityZZZconsistencyZZZisolationZZZdurability) |
| [back::queue](#chap17.xhtml_textXXXpushCCCqueueZZZpopCCCqueueZZZbackCCCqueueZZZfrontCCCqueue) | [const_where_expression](#chap10.xhtml_textXXXconst_where_expressionZZZwhere_expressionZZZwhere) |

| [Constant Expressions](#chap06.xhtml_chapterXXXConstantSSSExpressions) | [dispatcher notifier](#chap14.xhtml_textXXXdispatcherSSSnotifier) |
| [Contention (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXContentionSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) | [Double-Checked Locking Pattern](#chap09.xhtml_chapterXXXDoubleMMMCheckedSSSLockingSSSPattern) |
| [ContinuableFuture](#chap10.xhtml_textXXXFutureContinuationZZZSemiFutureZZZContinuableFutureZZZSharedFuture) | [durability](#chap10.xhtml_textXXXatomicityZZZconsistencyZZZisolationZZZdurability) |
| [Continuation with then](#chap10.xhtml_chapterXXXContinuationSSSwithSSSthen) | **E** |
| [Conventions](#chap21.xhtml_chapterXXXConventions) | [Eager evaluation (Glossary)](#chap23.xhtml_glossaryyXXXEagerSSSevaluationSSSBOBOBOGlossaryBCBCBC) |
| [Copied Value (Pattern)](#chap13.xhtml_chapterXXXCopiedSSSValueSSSBOBOBOPatternBCBCBC) | [element_aligned](#chap10.xhtml_textXXXelement_aligned_tagZZZelement_alignedZZZvector_aligned_tagZZZvector_alignedZZZoveraligned_tagZZZoveraligned) |
| [coroutine handle](#chap08.xhtml_textXXXpromiseSSSobjectSSSBOBOBOcoroutineBCBCBCZZZcoroutineSSShandleZZZcoroutineSSSstate) | [element_aligned_tag](#chap10.xhtml_textXXXelement_aligned_tagZZZelement_alignedZZZvector_aligned_tagZZZvector_alignedZZZoveraligned_tagZZZoveraligned) |
| [coroutine state](#chap08.xhtml_textXXXpromiseSSSobjectSSSBOBOBOcoroutineBCBCBCZZZcoroutineSSShandleZZZcoroutineSSSstate) | [epoch (time_point)](#chap21.xhtml_textXXXepochSSSBOBOBOtime_pointBCBCBCZZZnowSSSBOBOBOtime_pointBCBCBCZZZminSSSBOBOBOtime_pointBCBCBCZZZmaxSSSBOBOBOtime_pointBCBCBC) |
| [Coroutines](#chap08.xhtml_chapterXXXCoroutines) | [Epoch](#chap21.xhtml_chapterXXXEpoch) |
| [count_down](#chap08.xhtml_textXXXcount_downZZZtry_waitZZZarrive_and_waitSSSBOBOBOlatchBCBCBCZZZwaitSSSBOBOBOlatchBCBCBC) | [Exceptions (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXExceptionsSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) |
| [counting semaphores](#chap08.xhtml_textXXXcountingSSSsemaphoresZZZmaxSSSBOBOBOcounting_semaphoreBCBCBCZZZreleaseSSSBOBOBOcounting_semaphoreBCBCBCZZZacquireZZZtry_acquireZZZtry_acquire_forZZZtry_acquire_until) | [Exceptions](#chap06.xhtml_chapterXXXExceptions) |
| [CppMem: Atomics with Acquire-Release Semantic](#chap09.xhtml_chapterXXXCppMemOOOSSSAtomicsSSSwithSSSAcquireMMMReleaseSSSSemantic) | [exchange (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [CppMem: Atomics with Non-atomics](#chap09.xhtml_chapterXXXCppMemOOOSSSAtomicsSSSwithSSSNonMMMatomics) | [exchange (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) |
| [CppMem: Atomics with Relaxed Semantic](#chap09.xhtml_chapterXXXCppMemOOOSSSAtomicsSSSwithSSSRelaxedSSSSemantic) | [exclusive_scan](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) |
| [CppMem: Atomics with Sequential Consistency](#chap09.xhtml_chapterXXXCppMemOOOSSSAtomicsSSSwithSSSSequentialSSSConsistency) | [execution agent](#chap10.xhtml_textXXXexecutionSSSresourceZZZexecutionSSScontextZZZexecutionSSSagent) |
| [CppMem: Locks](#chap09.xhtml_chapterXXXCppMemOOOSSSLocks) | [execution context](#chap10.xhtml_textXXXexecutionSSSresourceZZZexecutionSSScontextZZZexecutionSSSagent) |
| [CppMem: Non-Atomic Variables](#chap09.xhtml_chapterXXXCppMemOOOSSSNonMMMAtomicSSSVariables) | [execution function](#chap10.xhtml_chapterXXXexecutionSSSfunction) |
| [CppMem](#chap22.xhtml_chapterXXXCppMem) | [Execution Policies](#chap07.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseqZZZexecutionOOOsequenced_policyZZZexecutionOOOparallel_policyZZZexecutionOOOparallel_unsequenced_policy) |
| [CppMem](#chap22.xhtml_textXXXCppMem) | [execution resource](#chap10.xhtml_textXXXexecutionSSSresourceZZZexecutionSSScontextZZZexecutionSSSagent) |
| [Creating new Futures](#chap10.xhtml_chapterXXXCreatingSSSnewSSSFutures) | [execution::require](#chap10.xhtml_chapterXXXexecutionCCCrequire) |
| [Critical Section (Glossary)](#chap23.xhtml_glossaryXXXCriticalSSSSectionSSSBOBOBOGlossaryBCBCBC) | [execution:par](#chap07.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseqZZZexecutionOOOsequenced_policyZZZexecutionOOOparallel_policyZZZexecutionOOOparallel_unsequenced_policy) |
| [Cross the valid Time Range](#chap21.xhtml_chapterXXXCrossSSStheSSSvalidSSSTimeSSSRange) | [execution:par_unseq](#chap07.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseqZZZexecutionOOOsequenced_policyZZZexecutionOOOparallel_policyZZZexecutionOOOparallel_unsequenced_policy) |
| [CRTP](#chap14.xhtml_textXXXCRTPZZZCuriouslySSSRecurringSSSTemplateSSSPattern) | [execution:parallel_policy](#chap07.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseqZZZexecutionOOOsequenced_policyZZZexecutionOOOparallel_policyZZZexecutionOOOparallel_unsequenced_policy) |
| [Curiously Recurring Template Pattern](#chap14.xhtml_textXXXCRTPZZZCuriouslySSSRecurringSSSTemplateSSSPattern) | [execution:parallel_unsequenced_policy](#chap07.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseqZZZexecutionOOOsequenced_policyZZZexecutionOOOparallel_policyZZZexecutionOOOparallel_unsequenced_policy) |
| [current_exception](#chap06.xhtml_textXXXcurrent_exceptionZZZmake_exception_ptr) | [execution:seq](#chap07.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseqZZZexecutionOOOsequenced_policyZZZexecutionOOOparallel_policyZZZexecutionOOOparallel_unsequenced_policy) |
| **D** | [execution:sequenced_policy](#chap07.xhtml_chapterXXXExecutionSSSPoliciesZZZexecutionOOOseqZZZexecutionOOOparZZZexecutionOOOpar_unseqZZZexecutionOOOsequenced_policyZZZexecutionOOOparallel_policyZZZexecutionOOOparallel_unsequenced_policy) |
| [Data Races](#chap20.xhtml_chapterXXXDataSSSRaces) | [Executor (Glossary)](#chap23.xhtml_glossaryXXXExecutorSSSBOBOBOGlossaryBCBCBC) |
| [Data Structures](#chap16.xhtml_PartXXXDataSSSStructures) | [executor propagation](#chap10.xhtml_textXXXexecutorSSSpropagation) |
| [Data-Parallel Vector Library](#chap10.xhtml_chapterXXXData-ParallelSSSVectorSSSLibrary) | [Executors](#chap10.xhtml_chapterXXXExecutors) |
| [Data-Parallel Vectors](#chap10.xhtml_chapterXXXData-ParallelSSSVectors) | [Extended Futures](#chap10.xhtml_chapterXXXExtendedSSSFutures) |
| [Deadlocks](#chap20.xhtml_chapterXXXDeadlocks) | **F** |
| [Deal with Sharing](#chap13.xhtml_chapterXXXDealSSSwithSSSSharing) | [False Sharing](#chap20.xhtml_chapterXXXFalseSSSSharing) |
| [Dealing with Mutation](#chap13.xhtml_chapterXXXDealingSSSwithSSSMutation) | [Fences](#chap05.xhtml_chapterXXXFences) |
| [defer_lock](#chap06.xhtml_textXXXdefer_lockZZZadopt_lock) | [fetch_add (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [deferred (future_status)](#chap06.xhtml_textXXXreadySSSBOBOBOfuture_statusBCBCBCZZZtimeoutSSSBOBOBOfuture_statusBCBCBCZZZdeferredSSSBOBOBOfuture_statusBCBCBC) | [fetch_add (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) |
| [define_task_block](#chap10.xhtml_textXXXdefine_task_blockZZZdefine_task_block_restore_thread) | [fetch_and (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [define_task_block_restore_thread](#chap10.xhtml_textXXXdefine_task_blockZZZdefine_task_block_restore_thread) | [fetch_and (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) |
| [dependency-order-before](#chap05.xhtml_textXXXcaries-a-dependencyZZZdependency-order-before) | [fetch_or (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [Design Goals](#chap08.xhtml_chapterXXXDesignSSSGoals) | [fetch_or (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) |
| [detach](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) | [fetch_sub (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [Details](#chap08.xhtml_chaperXXXDetails) | [fetch_sub (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) |
| [Different Synchronisation and Ordering Constraints](#chap05.xhtml_chapterXXXDifferentSSSSynchronisationSSSandSSSOrderingSSSConstraints) | [fetch_xor (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |

| [fetch_xor (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) | [History (Pattern)](#chap12.xhtml_chapterXXXHistorySSSBOBOBOPatternBCBCBC) |
| [FIFO](#chap17.xhtml_textXXXFIFO) | [hmax](#chap10.xhtml_textXXXreduceSSSBOBOBOsimdBCBCBCZZZhminZZZhmax) |
| [find_first_set](#chap10.xhtml_textXXXall_ofZZZany_ofZZZnone_ofZZZsome_ofZZZpopcountZZZfind_first_setZZZfind_last_set) | [hmin](#chap10.xhtml_textXXXreduceSSSBOBOBOsimdBCBCBCZZZhminZZZhmax) |
| [find_last_set](#chap10.xhtml_textXXXall_ofZZZany_ofZZZnone_ofZZZsome_ofZZZpopcountZZZfind_first_setZZZfind_last_set) | [hours](#chap21.xhtml_textXXXnanosecondsZZZmicrosecondsZZZmillisecondsZZZsecondsZZZminutesZZZhours) |
| [Fire and Forget](#chap06.xhtml_chaperXXXFireSSSandSSSForget) | **I** |
| [fixed_size](#chap10.xhtml_textXXXscalarZZZfixed_sizeZZZcompatibleZZZnativeZZZmax_fixed_size) | [inclusive_scan](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) |
| [foldl1](#chap07.xhtml_texttXXXmapZZZscanlZZZscanl1ZZZfoldlZZZfoldl1) | [inline static data members](#chap13.xhtml_textXXXinlineSSSstaticSSSdataSSSmembers) |
| [foldl](#chap07.xhtml_texttXXXmapZZZscanlZZZscanl1ZZZfoldlZZZfoldl1) | [Invaluable Value (Pattern)](#chap12.xhtml_chapterXXXInvaluableSSSValueSSSBOBOBOPatternBCBCBC) |
| [for_each](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) | [Invariants (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXInvariantsSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) |
| [for_each_n](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) | [is_abi_tag](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [Fork and Join](#chap10.xhtml_chapterXXXForkSSSandSSSJoin) | [is_abi_tag_v](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [Free Atomic Function](#chap05.xhtml_chapterXXXFreeSSSAtomicSSSFunction) | [is_always_lock_free](#chap05.xhtml_textXXXis_always_lock_free) |
| [From Time Point to Calendar Time](#chap21.xhtml_chapterXXXFromSSSTimeSSSPointSSStoSSSCalendarSSSTime) | [is_execution_policy](#chap07.xhtml_textXXXis_execution_policy) |
| [front::queue](#chap17.xhtml_textXXXpushCCCqueueZZZpopCCCqueueZZZbackCCCqueueZZZfrontCCCqueue) | [is_lock_free (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [full fence](#chap05.xhtml_textXXXfullSSSfenceZZZacquireSSSfenceZZZreleaseSSSfence) | [is_lock_free (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) |
| [Function Objects (Glossary)](#chap23.xhtml_glossaryXXXFunctionSSSObjectsSSSBOBOBOGlossaryBCBCBC) | [is_simd](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [Further Information](#chap19.xhtml_PartXXXFurtherSSSInformation) | [is_simd_flag_type](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [Future (Pattern)](#chap13.xhtml_chapterXXXFutureSSSBOBOBOPatternBCBCBC) | [is_simd_flag_type_v](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [future](#chap06.xhtml_chapterXXXfuture) | [is_simd_mask](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [future_errc::broken_promise](#chap06.xhtml_textXXXfuture_errorZZZfuture_errcCCCbroken_promise) | [is_simd_mask_v](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [future_error](#chap06.xhtml_textXXXfuture_errorZZZfuture_errcCCCbroken_promise) | [is_simd_v](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [future_status](#chap06.xhtml_chapterXXXfuture_status) | [isolation](#chap10.xhtml_textXXXatomicityZZZconsistencyZZZisolationZZZdurability) |
| [FutureContinuation](#chap10.xhtml_textXXXFutureContinuationZZZSemiFutureZZZContinuableFutureZZZSharedFuture) | [Issues of Mutexes](#chap06.xhtml_chapterXXXIssuesSSSofSSSMutexes) |
| **G** | **J** |
| [General (Best Practices)](#chap15.xhtml_chapterXXXGeneralSSSBOBOBOBestSSSPracticesBCBCBC) | [join and detach](#chap06.xhtml_chapterXXXjoinSSSandSSSdetach) |
| [General Considerations (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXGeneralSSSConsiderationsSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) | [join](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [get](#chap06.xhtml_textXXXshareZZZgetZZZvalidSSSBOBOBOfutureBCBCBCZZZwaitSSSBOBOBOfutureBCBCBCZZZwait_forSSSBOBOBOfutureBCBCBCZZZwait_untilSSSBOBOBOfutureBCBCBC) | [joinable](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [get_future (parameter_pack)](#chap06.xhtml_textXXXget_futureSSSBOBOBOparameter_packBCBCBCZZZset_valueSSSBOBOBOparameter_packBCBCBCZZZresetZZZmake_ready_future_at_thread_exitZZZvalidSSSBOBOBOparameter_packBCBCBC) | [Joining Threads](#chap08.xhtml_chapterXXXJoiningSSSThreads) |
| [get_future (promise)](#chap06.xhtml_textXXXget_futureSSSBOBOBOpromiseBCBCBCZZZset_valueSSSBOBOBOpromiseBCBCBCZZZset_exceptionZZZset_value_at_thread_exitZZZset_exception_at_thread_exit) | [jthread](#chap08.xhtml_textXXXjthread) |
| [get_id](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) | **K** |
| [get_token (stop_source)](#chap08.xhtml_textXXXstop_possibleSSSBOBOBOstop_sourceBCBCBCZZZstop_requestedSSSBOBOBOstop_sourceBCBCBCZZZget_tokenSSSBOBOBOstop_sourceBCBCBCZZZrequest_stopSSSBOBOBOstop_sourceBCBCBC) | [Kind of Atomic Operations](#chap05.xhtml_chapterXXXKindSSSofSSSAtomicSSSOperations) |
| [Glossary](#chap23.xhtml_chapterXXXGlossary) | **L** |
| [gmtime](#chap21.xhtml_textXXXto_time_tZZZtime_tZZZgmtimeZZZasctime) | [Lambda Functions (Glossary)](#chap23.xhtml_glossaryXXXLambdaSSSFunctionsSSSBOBOBOGlossaryBCBCBC) |
| [Granulariy of the Interace (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXGranulariySSSofSSStheSSSInteraceSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) | [latch](#chap08.xhtml_chapterXXXlatch) |
| [Guard Suspension (Pattern)](#chap13.xhtml_chapterXXXGuardSSSSuspensionSSSBOBOBOPatternBCBCBC) | [Latches and Barriers](#chap08.xhtml_chapterXXXLatchesSSSandSSSBarriers) |
| **H** | [Lazy evaluation (Glossary)](#chap23.xhtml_glossaryyXXXLazySSSevaluationSSSBOBOBOGlossaryBCBCBC) |
| [h (time literal)](#chap21.xhtml_textXXXhSSSBOBOBOtimeSSSliteralBCBCBCZZZminSSSBOBOBOtimeSSSliteralBCBCBCZZZsSSSBOBOBOtimeSSSliteralBCBCBCZZZmsSSSBOBOBOtimeSSSliteralBCBCBCZZZusSSSBOBOBOtimeSSSliteralBCBCBCZZZnsSSSBOBOBOtimeSSSliteralBCBCBC) | [Lifetime Issues of Variables](#chap20.xhtml_chapterXXXLifetimeSSSIssuesSSSofSSSVariables) |
| [Half-Sync/Half-Async](#chap14.xhtml_chapterXXXHalf-SyncSLSLSLHalf-Async) | [LIFO](#chap17.xhtml_textXXXLIFO) |
| [hardware_constructive_interference_size](#chap20.xhtml_textXXXhardware_destructive_interference_sizeZZZhardware_constructive_interference_size) | [load (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [hardware_destructive_interference_size](#chap20.xhtml_textXXXhardware_destructive_interference_sizeZZZhardware_constructive_interference_size) | [load (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) |
| [hazard pointers](#chap20.xhtml_textXXXhazardSSSpointers) | [LoadLoad](#chap05.xhtml_textXXXLoadLoadZZZLoadStoreZZZStoreLoadZZZStoreStore) |
| [high_resulution_clock](#chap21.xhtml_textXXXsystem_clockZZZsteady_clockZZZhigh_resulution_clock) | [LoadStore](#chap05.xhtml_textXXXLoadLoadZZZLoadStoreZZZStoreLoadZZZStoreStore) |

| [lock (unique_lock)](#chap06.xhtml_textXXXlockSSSBOBOBOunique_lockBCBCBCZZZtry_lockZZZtry_lock_forZZZtry_lock_untilZZZreleaseSSSBOBOBOunique_lockBCBCBCZZZowns_lockZZZunlock) | [Modification Order (Glossary)](#chap23.xhtml_glossaryXXXModificationSSSOrderSSSBOBOBOGlossaryBCBCBC) |
| [Lock-Based Data Structures](#chap17.xhtml_chapterXXXLock-BasedSSSDataSSSStructures) | [modification order consistency](#chap05.xhtml_textXXXmodificationSSSorderSSSconsistency) |
| [lock-free (Glossary)](#chap23.xhtml_glossaryXXXlockMMMfreeSSSBOBOBOGlossaryBCBCBC) | [Monad (Glossary)](#chap23.xhtml_glossaryXXXMonadSSSBOBOBOGlossaryBCBCBC) |
| [Lock-Free Data Structures](#chap18.xhtml_chapterXXXLock-FreeSSSDataSSSStructures) | [Monitor Object](#chap14.xhtml_chapterXXXMonitorSSSObject) |
| [lock](#chap06.xhtml_textXXXlock) | [Moving Threads](#chap20.xhtml_chapterXXXMovingSSSThreads) |
| [lock_guard](#chap06.xhtml_chapterXXXlock_guard) | [ms (time literal)](#chap21.xhtml_textXXXhSSSBOBOBOtimeSSSliteralBCBCBCZZZminSSSBOBOBOtimeSSSliteralBCBCBCZZZsSSSBOBOBOtimeSSSliteralBCBCBCZZZmsSSSBOBOBOtimeSSSliteralBCBCBCZZZusSSSBOBOBOtimeSSSliteralBCBCBCZZZnsSSSBOBOBOtimeSSSliteralBCBCBC) |
| [Locking Strategy (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXLockingSSSStrategySSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) | [Multithreaded Summation with a Shared Variable](#chap09.xhtml_chapterXXXMultithreadedSSSSummationSSSwithSSSaSSSSharedSSSVariable) |
| [Locks](#chap06.xhtml_chapterXXXLocks) | [Multithreading (Best Practices)](#chap15.xhtml_chapterXXXMultithreadingSSSBOBOBOBestSSSPracticesBCBCBC) |
| [Lost Wakeup (Glossary)](#chap23.xhtml_glossaryXXXLostSSSWakeupSSSBOBOBOGlossaryBCBCBC) | [Multithreading](#chap06.xhtml_chapterXXXMultithreading) |
| [Lost Wakeup](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) | [mutex](#chap06.xhtml_textXXXmutexZZZrecursive_mutexZZZtimed_mutexZZZrecursive_timed_mutex) |
| **M** | [Mutexes](#chap06.xhtml_chapterXXXMutexes) |
| [make_exception_ptr](#chap06.xhtml_textXXXcurrent_exceptionZZZmake_exception_ptr) | [My Performance Measurement](#chap09.xhtml_chapterXXXMySSSPerformanceSSSMeasurement) |
| [make_exceptional_future](#chap10.xhtml_chapterXXXmake_ready_futureZZZmake_exceptional_future) | **N** |
| [make_ready_future](#chap10.xhtml_chapterXXXmake_ready_futureZZZmake_exceptional_future) | [nanoseconds](#chap21.xhtml_textXXXnanosecondsZZZmicrosecondsZZZmillisecondsZZZsecondsZZZminutesZZZhours) |
| [make_ready_future_at_thread_exit](#chap06.xhtml_textXXXget_futureSSSBOBOBOparameter_packBCBCBCZZZset_valueSSSBOBOBOparameter_packBCBCBCZZZresetZZZmake_ready_future_at_thread_exitZZZvalidSSSBOBOBOparameter_packBCBCBC) | [native](#chap10.xhtml_textXXXscalarZZZfixed_sizeZZZcompatibleZZZnativeZZZmax_fixed_size) |
| [map](#chap07.xhtml_texttXXXmapZZZscanlZZZscanl1ZZZfoldlZZZfoldl1) | [native_handle (condition_variable)](#chap06.xhtml_textXXXnotify_oneSSSBOBOBOcondition_variableBCBCBCZZZnotify_allSSSBOBOBOcondition_variableBCBCBCZZZwaitSSSBOBOBOcondition_variableBCBCBCZZZwait_forSSSBOBOBOcondition_variableBCBCBCZZZwait_untilSSSBOBOBOcondition_variableBCBCBCZZZnative_handleSSSBOBOBOcondition_variableBCBCBC) |
| [Math Laws (Glossary)](#chap23.xhtml_glossaryXXXMathSSSLawsSSSBOBOBOGlossaryBCBCBC) | [native_handle](#chap06.xhtml_textXXXnative_handle) |
| [max (counting_semaphore)](#chap08.xhtml_textXXXcountingSSSsemaphoresZZZmaxSSSBOBOBOcounting_semaphoreBCBCBCZZZreleaseSSSBOBOBOcounting_semaphoreBCBCBCZZZacquireZZZtry_acquireZZZtry_acquire_forZZZtry_acquire_until) | [Non-blocking (Glossary)](#chap23.xhtml_glossaryXXXNonMMMblockingSSSBOBOBOGlossaryBCBCBC) |
| [max (simd)](#chap10.xhtml_textXXXminSSSBOBOBOsimdBCBCBCZZZmaxSSSBOBOBOsimdBCBCBCZZZminmaxZZZclamp) | [none_of](#chap10.xhtml_textXXXall_ofZZZany_ofZZZnone_ofZZZsome_ofZZZpopcountZZZfind_first_setZZZfind_last_set) |
| [max (time_point)](#chap21.xhtml_textXXXepochSSSBOBOBOtime_pointBCBCBCZZZnowSSSBOBOBOtime_pointBCBCBCZZZminSSSBOBOBOtime_pointBCBCBCZZZmaxSSSBOBOBOtime_pointBCBCBC) | [Notifications](#chap06.xhtml_chapterXXXNotifications) |
| [max_fixed_size](#chap10.xhtml_textXXXscalarZZZfixed_sizeZZZcompatibleZZZnativeZZZmax_fixed_size) | [notify_all (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [Memory Barriers](#chap05.xhtml_chapterXXXMemorySSSBarriers) | [notify_all (atomic_flag)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [Memory Location (Glossary)](#chap23.xhtml_glossaryXXXMemorySSSLocationSSSBOBOBOGlossaryBCBCBC) | [notify_all (condition_variable)](#chap06.xhtml_textXXXnotify_oneSSSBOBOBOcondition_variableBCBCBCZZZnotify_allSSSBOBOBOcondition_variableBCBCBCZZZwaitSSSBOBOBOcondition_variableBCBCBCZZZwait_forSSSBOBOBOcondition_variableBCBCBCZZZwait_untilSSSBOBOBOcondition_variableBCBCBCZZZnative_handleSSSBOBOBOcondition_variableBCBCBC) |
| [Memory Model (Best Practices)](#chap15.xhtml_chapterXXXMemorySSSModelSSSBOBOBOBestSSSPracticesBCBCBC) | [notify_one (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [Memory Model (Glossary)](#chap23.xhtml_glossaryXXXMemorySSSModelSSSBOBOBOGlossaryBCBCBC) | [notify_one (atomic_flag)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [Memory Model](#chap05.xhtml_chapterXXXMemorySSSModel) | [notify_one (condition_variable)](#chap06.xhtml_textXXXnotify_oneSSSBOBOBOcondition_variableBCBCBCZZZnotify_allSSSBOBOBOcondition_variableBCBCBCZZZwaitSSSBOBOBOcondition_variableBCBCBCZZZwait_forSSSBOBOBOcondition_variableBCBCBCZZZwait_untilSSSBOBOBOcondition_variableBCBCBCZZZnative_handleSSSBOBOBOcondition_variableBCBCBC) |
| [memory_alignment](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) | [now (time_point)](#chap21.xhtml_textXXXepochSSSBOBOBOtime_pointBCBCBCZZZnowSSSBOBOBOtime_pointBCBCBCZZZminSSSBOBOBOtime_pointBCBCBCZZZmaxSSSBOBOBOtime_pointBCBCBC) |
| [memory_alignment_v](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) | [ns (time literal)](#chap21.xhtml_textXXXhSSSBOBOBOtimeSSSliteralBCBCBCZZZminSSSBOBOBOtimeSSSliteralBCBCBCZZZsSSSBOBOBOtimeSSSliteralBCBCBCZZZmsSSSBOBOBOtimeSSSliteralBCBCBCZZZusSSSBOBOBOtimeSSSliteralBCBCBCZZZnsSSSBOBOBOtimeSSSliteralBCBCBC) |
| [memory_order_acq_rel](#chap05.xhtml_textXXXmemory_order_relaxedZZZmemory_order_consumeZZZmemory_order_acquireZZZmemory_order_releaseZZZmemory_order_acq_relZZZmemory_order_seq_cst) | [Null object](#chap13.xhtml_textXXXNullSSSobject) |
| [memory_order_acquire](#chap05.xhtml_textXXXmemory_order_relaxedZZZmemory_order_consumeZZZmemory_order_acquireZZZmemory_order_releaseZZZmemory_order_acq_relZZZmemory_order_seq_cst) | **O** |
| [memory_order_consume](#chap05.xhtml_textXXXmemory_order_relaxedZZZmemory_order_consumeZZZmemory_order_acquireZZZmemory_order_releaseZZZmemory_order_acq_relZZZmemory_order_seq_cst) | [once_flag](#chap06.xhtml_chapterXXXcall_onceZZZonce_flag) |
| [memory_order_relaxed](#chap05.xhtml_textXXXmemory_order_relaxedZZZmemory_order_consumeZZZmemory_order_acquireZZZmemory_order_releaseZZZmemory_order_acq_relZZZmemory_order_seq_cst) | [Ongoing Optimisation](#chap09.xhtml_chapterXXXOngoingSSSOptimisationXXXWithSSSCppMem) |
| [memory_order_release](#chap05.xhtml_textXXXmemory_order_relaxedZZZmemory_order_consumeZZZmemory_order_acquireZZZmemory_order_releaseZZZmemory_order_acq_relZZZmemory_order_seq_cst) | [Operations](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [memory_order_seq_cst](#chap05.xhtml_textXXXmemory_order_relaxedZZZmemory_order_consumeZZZmemory_order_acquireZZZmemory_order_releaseZZZmemory_order_acq_relZZZmemory_order_seq_cst) | [overaligned](#chap10.xhtml_textXXXelement_aligned_tagZZZelement_alignedZZZvector_aligned_tagZZZvector_alignedZZZoveraligned_tagZZZoveraligned) |
| [Meyers Singleton](#chap09.xhtml_textXXXMeyersSSSSingleton) | [overaligned_tag](#chap10.xhtml_textXXXelement_aligned_tagZZZelement_alignedZZZvector_aligned_tagZZZvector_alignedZZZoveraligned_tagZZZoveraligned) |
| [microseconds](#chap21.xhtml_textXXXnanosecondsZZZmicrosecondsZZZmillisecondsZZZsecondsZZZminutesZZZhours) | [owns_lock](#chap06.xhtml_textXXXlockSSSBOBOBOunique_lockBCBCBCZZZtry_lockZZZtry_lock_forZZZtry_lock_untilZZZreleaseSSSBOBOBOunique_lockBCBCBCZZZowns_lockZZZunlock) |
| [milliseconds](#chap21.xhtml_textXXXnanosecondsZZZmicrosecondsZZZmillisecondsZZZsecondsZZZminutesZZZhours) | **P** |
| [min (simd)](#chap10.xhtml_textXXXminSSSBOBOBOsimdBCBCBCZZZmaxSSSBOBOBOsimdBCBCBCZZZminmaxZZZclamp) | [packaged_task](#chap06.xhtml_chapterXXXpackaged_task) |
| [min (time literal)](#chap21.xhtml_textXXXhSSSBOBOBOtimeSSSliteralBCBCBCZZZminSSSBOBOBOtimeSSSliteralBCBCBCZZZsSSSBOBOBOtimeSSSliteralBCBCBCZZZmsSSSBOBOBOtimeSSSliteralBCBCBCZZZusSSSBOBOBOtimeSSSliteralBCBCBCZZZnsSSSBOBOBOtimeSSSliteralBCBCBC) | [Parallel Algorithms of the STL](#chap07.xhtml_chapterXXXParallelSSSAlgorithmsSSSofSSStheSSSSTL) |
| [min (time_point)](#chap21.xhtml_textXXXepochSSSBOBOBOtime_pointBCBCBCZZZnowSSSBOBOBOtime_pointBCBCBCZZZminSSSBOBOBOtime_pointBCBCBCZZZmaxSSSBOBOBOtime_pointBCBCBC) | [Parallelism (Glossary)](#chap23.xhtml_glossaryXXXParallelismSSSBOBOBOGlossaryBCBCBC) |
| [minmax](#chap10.xhtml_textXXXminSSSBOBOBOsimdBCBCBCZZZmaxSSSBOBOBOsimdBCBCBCZZZminmaxZZZclamp) | [partial_sum](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) |
| [minutes](#chap21.xhtml_textXXXnanosecondsZZZmicrosecondsZZZmillisecondsZZZsecondsZZZminutesZZZhours) | [Pattern (Glossary)](#chap23.xhtml_glossaryXXXPatternSSSBOBOBOGlossaryBCBCBC) |

| [Pattern versus Best Practices (Pattern)](#chap12.xhtml_chapterXXXPatternSSSversusSSSBestSSSPracticesSSSBOBOBOPatternBCBCBC) | [s (time literal)](#chap21.xhtml_textXXXhSSSBOBOBOtimeSSSliteralBCBCBCZZZminSSSBOBOBOtimeSSSliteralBCBCBCZZZsSSSBOBOBOtimeSSSliteralBCBCBCZZZmsSSSBOBOBOtimeSSSliteralBCBCBCZZZusSSSBOBOBOtimeSSSliteralBCBCBCZZZnsSSSBOBOBOtimeSSSliteralBCBCBC) |
| [Patterns and Best Practices](#chap12.xhtml_chapterXXXPatternsSSSandSSSBestSSSPractices) | [Scalability (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXScalabilitySSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) |
| [Patterns](#chap11.xhtml_PartXXXPatterns) | [scalar](#chap10.xhtml_textXXXscalarZZZfixed_sizeZZZcompatibleZZZnativeZZZmax_fixed_size) |
| [Performance Numbers of the various Thread-Safe Singleton Implementations](#chap09.xhtml_chapterXXXPerformanceSSSNumbersSSSofSSStheSSSvariousSSSThreadMMMSafeSSSSingletonSSSImplementations) | [scanl1](#chap07.xhtml_texttXXXmapZZZscanlZZZscanl1ZZZfoldlZZZfoldl1) |
| [Performance of Parallel STL](#chap07.xhtml_chapterXXXPerformanceSSSofSSSParallelSSSSTL) | [scanl](#chap07.xhtml_texttXXXmapZZZscanlZZZscanl1ZZZfoldlZZZfoldl1) |
| [pop::queue](#chap17.xhtml_textXXXpushCCCqueueZZZpopCCCqueueZZZbackCCCqueueZZZfrontCCCqueue) | [Scoped Locking (Pattern)](#chap13.xhtml_chapterXXXScopedSSSLockingSSSBOBOBOPatternBCBCBC) |
| [pop::Simple Queue](#chap17.xhtml_textXXXASSSSimpleSSSQueueZZZpopCCCSimpleSSSQueueZZZpushCCCSimpleSSSQueue) | [scoped_lock](#chap06.xhtml_chapterXXXscoped_lock) |
| [pop::stack](#chap17.xhtml_textXXXpushCCCstackZZZpopCCCstackZZZtopCCCstack) | [scoped_thread](#chap06.xhtml_textXXXscoped_thread) |
| [popcount](#chap10.xhtml_textXXXall_ofZZZany_ofZZZnone_ofZZZsome_ofZZZpopcountZZZfind_first_setZZZfind_last_set) | [seconds](#chap21.xhtml_textXXXnanosecondsZZZmicrosecondsZZZmillisecondsZZZsecondsZZZminutesZZZhours) |
| [Predicate (Glossary)](#chap23.xhtml_glossaryXXXPredicateSSSBOBOBOGlossaryBCBCBC) | [Semaphores](#chap08.xhtml_chapterXXXSemaphores) |
| [Proactor](#chap14.xhtml_chapterXXXProactor) | [SemiFuture](#chap10.xhtml_textXXXFutureContinuationZZZSemiFutureZZZContinuableFutureZZZSharedFuture) |
| [promise and future](#chap06.xhtml_chapterXXXpromiseSSSandSSSfuture) | [Sequence Point (Glossary)](#chap23.xhtml_glossaryXXXSequenceSSSPointSSSBOBOBOGlossaryBCBCBC) |
| [promise object (coroutine)](#chap08.xhtml_textXXXpromiseSSSobjectSSSBOBOBOcoroutineBCBCBCZZZcoroutineSSShandleZZZcoroutineSSSstate) | [Sequential Consistency (Glossary)](#chap23.xhtml_glossaryXXXSequentialSSSConsistencySSSBOBOBOGlossaryBCBCBC) |
| [promise](#chap06.xhtml_chapterXXXpromise) | [Sequential Consistency](#chap05.xhtml_chapterXXXSequentialSSSConsistency) |
| [Proxy](#chap14.xhtml_textXXXProxy) | [set_exception](#chap06.xhtml_textXXXget_futureSSSBOBOBOpromiseBCBCBCZZZset_valueSSSBOBOBOpromiseBCBCBCZZZset_exceptionZZZset_value_at_thread_exitZZZset_exception_at_thread_exit) |
| [push::queue](#chap17.xhtml_textXXXpushCCCqueueZZZpopCCCqueueZZZbackCCCqueueZZZfrontCCCqueue) | [set_exception_at_thread_exit](#chap06.xhtml_textXXXget_futureSSSBOBOBOpromiseBCBCBCZZZset_valueSSSBOBOBOpromiseBCBCBCZZZset_exceptionZZZset_value_at_thread_exitZZZset_exception_at_thread_exit) |
| [push::Simple Queue](#chap17.xhtml_textXXXASSSSimpleSSSQueueZZZpopCCCSimpleSSSQueueZZZpushCCCSimpleSSSQueue) | [set_value (parameter_pack)](#chap06.xhtml_textXXXget_futureSSSBOBOBOparameter_packBCBCBCZZZset_valueSSSBOBOBOparameter_packBCBCBCZZZresetZZZmake_ready_future_at_thread_exitZZZvalidSSSBOBOBOparameter_packBCBCBC) |
| [push::stack](#chap17.xhtml_textXXXpushCCCstackZZZpopCCCstackZZZtopCCCstack) | [set_value (promise)](#chap06.xhtml_textXXXget_futureSSSBOBOBOpromiseBCBCBCZZZset_valueSSSBOBOBOpromiseBCBCBCZZZset_exceptionZZZset_value_at_thread_exitZZZset_exception_at_thread_exit) |
| **Q** | [set_value_at_thread_exit](#chap06.xhtml_textXXXget_futureSSSBOBOBOpromiseBCBCBCZZZset_valueSSSBOBOBOpromiseBCBCBCZZZset_exceptionZZZset_value_at_thread_exitZZZset_exception_at_thread_exit) |
| [Queue (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXQueueSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) | [share](#chap06.xhtml_textXXXshareZZZgetZZZvalidSSSBOBOBOfutureBCBCBCZZZwaitSSSBOBOBOfutureBCBCBCZZZwait_forSSSBOBOBOfutureBCBCBCZZZwait_untilSSSBOBOBOfutureBCBCBC) |
| **R** | [Shared Data](#chap06.xhtml_chapterXXXSharedSSSData) |
| [Race Condition](#chap20.xhtml_chapterXXXRaceSSSCondition) | [shared_future](#chap06.xhtml_chapterXXXshared_future) |
| [RAII (Glossary)](#chap23.xhtml_glossaryXXXRAIISSSBOBOBOGlossaryBCBCBC) | [shared_lock](#chap06.xhtml_chapterXXXshared_lock) |
| [ratio](#chap21.xhtml_textXXXratio) | [shared_mutex](#chap06.xhtml_XXXshared_mutexZZZshared_timed_mutex) |
| [RCU](#chap20.xhtml_textXXXRCU) | [shared_ptr](#chap05.xhtml_chapterXXXshared_ptr) |
| [Reactor](#chap14.xhtml_chapterXXXReactor) | [shared_timed_mutex](#chap06.xhtml_XXXshared_mutexZZZshared_timed_mutex) |
| [ready (future_status)](#chap06.xhtml_textXXXreadySSSBOBOBOfuture_statusBCBCBCZZZtimeoutSSSBOBOBOfuture_statusBCBCBCZZZdeferredSSSBOBOBOfuture_statusBCBCBC) | [SharedFuture](#chap10.xhtml_textXXXFutureContinuationZZZSemiFutureZZZContinuableFutureZZZSharedFuture) |
| [recursive_mutex](#chap06.xhtml_textXXXmutexZZZrecursive_mutexZZZtimed_mutexZZZrecursive_timed_mutex) | [signal](#chap05.xhtml_textXXXsignalZZZSIGTERM) |
| [recursive_timed_mutex](#chap06.xhtml_textXXXmutexZZZrecursive_mutexZZZtimed_mutexZZZrecursive_timed_mutex) | [SIGTERM](#chap05.xhtml_textXXXsignalZZZSIGTERM) |
| [reduce (simd)](#chap10.xhtml_textXXXreduceSSSBOBOBOsimdBCBCBCZZZhminZZZhmax) | [simd](#chap10.xhtml_textXXXsimdZZZsimd_mask) |
| [reduce](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) | [simd_cast](#chap10.xhtml_textXXXsimd_castZZZstatic_simd_castZZZto_fixed_sizeZZZto_compatibleZZZto_nativeZZZsplitZZZconcat) |
| [Reference PCs](#chap09.xhtml_textXXXReferenceSSSPCs) | [simd_mask](#chap10.xhtml_textXXXsimdZZZsimd_mask) |
| [relaxed block](#chap10.xhtml_testXXXrelaxedSSSblock) | [simd_size](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [Relaxed Semantic](#chap05.xhtml_chapterXXXRelaxedSSSSemantic) | [simd_size_v](#chap10.xhtml_textXXXis_abi_tagZZZis_abi_tag_vZZZis_simdZZZis_simd_vZZZis_simd_maskZZZis_simd_mask_vZZZis_simd_flag_typeZZZis_simd_flag_type_vZZZsimd_sizeZZZsimd_size_vZZZmemory_alignmentZZZmemory_alignment_vZZZabi_for_sizeZZZabi_for_size_t) |
| [release (counting_semaphore)](#chap08.xhtml_textXXXcountingSSSsemaphoresZZZmaxSSSBOBOBOcounting_semaphoreBCBCBCZZZreleaseSSSBOBOBOcounting_semaphoreBCBCBCZZZacquireZZZtry_acquireZZZtry_acquire_forZZZtry_acquire_until) | [Single Threaded Addition of a Vector](#chap09.xhtml_chapterXXXSingleSSSThreadedSSSAdditionSSSofSSSaSSSVector) |
| [release (unique_lock)](#chap06.xhtml_textXXXlockSSSBOBOBOunique_lockBCBCBCZZZtry_lockZZZtry_lock_forZZZtry_lock_untilZZZreleaseSSSBOBOBOunique_lockBCBCBCZZZowns_lockZZZunlock) | [singleton](#chap09.xhtml_testXXXsingleton) |
| [release fence](#chap05.xhtml_textXXXfullSSSfenceZZZacquireSSSfenceZZZreleaseSSSfence) | [Sleep and Wait](#chap21.xhtml_chapterXXXSleepSSSandSSSWait) |
| [Release Sequence (Glossary)](#chap23.xhtml_glossaryXXXReleaseSSSSequenceSSSBOBOBOGlossaryBCBCBC) | [some_of](#chap10.xhtml_textXXXall_ofZZZany_ofZZZnone_ofZZZsome_ofZZZpopcountZZZfind_first_setZZZfind_last_set) |
| [request_stop (stop_source)](#chap08.xhtml_textXXXstop_possibleSSSBOBOBOstop_sourceBCBCBCZZZstop_requestedSSSBOBOBOstop_sourceBCBCBCZZZget_tokenSSSBOBOBOstop_sourceBCBCBCZZZrequest_stopSSSBOBOBOstop_sourceBCBCBC) | [Specilisations of std::atomic_ref](#chap05.xhtml_chapterXXXSpecilisationsSSSofSSSstdCCCatomic_ref) |
| [reset](#chap06.xhtml_textXXXget_futureSSSBOBOBOparameter_packBCBCBCZZZset_valueSSSBOBOBOparameter_packBCBCBCZZZresetZZZmake_ready_future_at_thread_exitZZZvalidSSSBOBOBOparameter_packBCBCBC) | [Spinlock versus Mutex](#chap05.xhtml_chapterXXXSpinlockSSSversusSSSMutex) |
| [resumable function](#chap08.xhtml_testXXXresumableSSSfunction) | [spinlock](#chap05.xhtml_textXXXspinlock) |
| **S** | [split](#chap10.xhtml_textXXXsimd_castZZZstatic_simd_castZZZto_fixed_sizeZZZto_compatibleZZZto_nativeZZZsplitZZZconcat) |

| [Spurious wakeup (Glossary)](#chap23.xhtml_glossaryXXXSpuriousSSSwakeupSSSBOBOBOGlossaryBCBCBC) | [The Framework](#chap08.xhtml_chapterXXXTheSSSFramework) |
| [Spurious Wakeup](#chap06.xhtml_chapterXXXLostSSSWakeupZZZSpuriousSSSWakeup) | [The functional Heritage](#chap07.xhtml_chapterXXXTheSSSfunctionalSSSHeritage) |
| [Stack (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXStackSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) | [The Future: C++20](#chap08.xhtml_chapterXXXTheSSSFutureOOOSSSCPPP20) |
| [Static Variables](#chap06.xhtml_chapterXXXStaticSSSVariables) | [The Future: C++23](#chap10.xhtml_chapterXXXTheSSSFutureOOOSSSCPPP23) |
| [static_simd_cast](#chap10.xhtml_textXXXsimd_castZZZstatic_simd_castZZZto_fixed_sizeZZZto_compatibleZZZto_nativeZZZsplitZZZconcat) | [The Interface of Data-Parallel Vectors](#chap10.xhtml_chapterXXXTheSSSInterfaceSSSofSSSData-ParallelSSSVectors) |
| [std::call_once with std::once_flag](#chap09.xhtml_chapterXXXstdCCCcall_onceSSSwithSSSstdCCConce_flag) | [The Interface](#chap10.xhtml_chapterXXXTheSSSInterface) |
| [steady_clock](#chap21.xhtml_textXXXsystem_clockZZZsteady_clockZZZhigh_resulution_clock) | [The Interplay of Time Point, Time Durcation, and Clock](#chap21.xhtml_chapterXXXTheSSSInterplaySSSofSSSTimeSSSPointKKKSSSTimeSSSDurcationKKKSSSandSSSClock) |
| [Stop Tokens](#chap08.xhtml_chapterXXXStopSSSTokens) | [The New Algorithms](#chap07.xhtml_chapterXXXTheSSSNewSSSAlgorithms) |
| [stop_callback](#chap08.xhtml_textXXXstop_tokenZZZstop_callbackZZZstop_source) | [The Scheduler](#chap10.xhtml_chapterXXXTheSSSScheduler) |
| [stop_possible (stop_source)](#chap08.xhtml_textXXXstop_possibleSSSBOBOBOstop_sourceBCBCBCZZZstop_requestedSSSBOBOBOstop_sourceBCBCBCZZZget_tokenSSSBOBOBOstop_sourceBCBCBCZZZrequest_stopSSSBOBOBOstop_sourceBCBCBC) | [The Simplified Workflow](#chap08.xhtml_chapterXXXTheSSSSimplifiedSSSWorkflow) |
| [stop_possible (stop_token)](#chap08.xhtml_textXXXstop_possibleSSSBOBOBOstop_tokenBCBCBCZZZstop_requestedSSSBOBOBOstop_tokenBCBCBC) | [The Six Variants](#chap05.xhtml_chapterXXXTheSSSSixSSSVariants) |
| [stop_requested (stop_source)](#chap08.xhtml_textXXXstop_possibleSSSBOBOBOstop_sourceBCBCBCZZZstop_requestedSSSBOBOBOstop_sourceBCBCBCZZZget_tokenSSSBOBOBOstop_sourceBCBCBCZZZrequest_stopSSSBOBOBOstop_sourceBCBCBC) | [The Start Policy](#chap06.xhtml_chaperXXXTheSSSStartSSSPolicy) |
| [stop_requested (stop_token)](#chap08.xhtml_textXXXstop_possibleSSSBOBOBOstop_tokenBCBCBCZZZstop_requestedSSSBOBOBOstop_tokenBCBCBC) | [The Sychronisation and Ordering Constraints](#chap05.xhtml_chapterXXXTheSSSSychronisationSSSandSSSOrderingSSSConstraints) |
| [stop_source](#chap08.xhtml_textXXXstop_tokenZZZstop_callbackZZZstop_source) | [The Test Run](#chap22.xhtml_chapterXXXTheSSSTestSSSRun) |
| [stop_token](#chap08.xhtml_textXXXstop_tokenZZZstop_callbackZZZstop_source) | [The three Fences](#chap05.xhtml_chapterXXXTheSSSthreeSSSFences) |
| [store (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) | [The Typical Minunderstanding](#chap05.xhtml_chapterXXXTheSSSTypicalSSSMinunderstanding) |
| [store (atomic_ref)](#chap05.xhtml_textXXXis_lock_freeSSSBOBOBOatomic_refBCBCBCZZZloadSSSBOBOBOatomic_refBCBCBCZZZstoreSSSBOBOBOatomic_refBCBCBCZZZexchangeSSSBOBOBOatomic_refBCBCBCZZZfetch_addSSSBOBOBOatomic_refBCBCBCZZZfetch_subSSSBOBOBOatomic_refBCBCBCZZZfetch_orSSSBOBOBOatomic_refBCBCBCZZZfetch_andSSSBOBOBOatomic_refBCBCBCZZZfetch_xorSSSBOBOBOatomic_refBCBCBC) | [The Wait Workflow](#chap06.xhtml_chapterXXXTheSSSWaitSSSWorkflow) |
| [StoreLoad](#chap05.xhtml_textXXXLoadLoadZZZLoadStoreZZZStoreLoadZZZStoreStore) | [this_thread::get_id](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [StoreStore](#chap05.xhtml_textXXXLoadLoadZZZLoadStoreZZZStoreLoadZZZStoreStore) | [this_thread::sleep_for](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [Strategized Locking (Pattern)](#chap13.xhtml_chapterXXXStrategizedSSSLockingSSSBOBOBOPatternBCBCBC) | [this_thread::sleep_until](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [Strong Memory Model](#chap05.xhtml_chapterXXXStrongSSSMemorySSSModel) | [this_thread::yield](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [Strong versus Weak Memory Model](#chap05.xhtml_chapterXXXStrongSSSversusSSSWeakSSSMemorySSSModel) | [Thread (Glossary)](#chap23.xhtml_glossaryXXXThreadSSSBOBOBOGlossaryBCBCBC) |
| [Summation of a Vector: The Conclusion](#chap09.xhtml_chapterXXXSummationSSSofSSSaSSSVectorOOOSSSTheSSSConclusion) | [Thread Arguments](#chap06.xhtml_chapterXXXThreadSSSArguments) |
| [suspend_always](#chap08.xhtml_textXXXsuspend_alwaysZZZsuspend_never) | [Thread Creation](#chap06.xhtml_chapterXXXThreadSSSCreation) |
| [suspend_never](#chap08.xhtml_textXXXsuspend_alwaysZZZsuspend_never) | [Thread Lifetime](#chap06.xhtml_chapterXXXThreadSSSLifetime) |
| [Synchronisation Patterns](#chap13.xhtml_chapterXXXSynchronisationSSSPatterns) | [Thread Safe Initialization](#chap06.xhtml_chaperXXXThreadSSSSafeSSSInitialization) |
| [Synchronisation with Atomic Variables or Fences](#chap05.xhtml_chapterXXXSynchronisationSSSwithSSSAtomicSSSVariablesSSSorSSSFences) | [Thread Synchronisation with co_await](#chap08.xhtml_chapterXXXThreadSSSSynchronisationSSSwithSSSco_await) |
| [Synchronized and Atomic Blocks](#chap10.xhtml_ChapterXXXSynchronizedSSSandSSSAtomicSSSBlocks) | [Thread-Local Data](#chap06.xhtml_chapterXXXThreadMMMLocalSSSData) |
| [system_clock](#chap21.xhtml_textXXXsystem_clockZZZsteady_clockZZZhigh_resulution_clock) | [Thread-Local Summation](#chap09.xhtml_chapterXXXThreadMMMLocalSSSSummation) |
| **T** | [Thread-Safe Initialisation of a Singelton](#chap09.xhtml_chapterXXXThreadMMMSafeSSSInitialisationSSSofSSSaSSSSingelton) |
| [tagged state reference](#chap24.xhtml_textXXXtaggedSSSstateSSSreference) | [Thread-Safe Interface (Pattern)](#chap13.xhtml_chapterXXXThread-SafeSSSInterfaceSSSBOBOBOPatternBCBCBC) |
| [Task Blocks](#chap10.xhtml_chapterXXXTaskSSSBlocks) | [Thread-Safe Meyers Singleton](#chap09.xhtml_chapterXXXThreadMMMSafeSSSMeyersSSSSingleton) |
| [task_cancelled_exception](#chap10.xhtml_textXXXtask_cancelled_exception) | [Thread-Safe Passive Object](#chap14.xhtml_textXXXThread-SafeSSSPassiveSSSObject) |
| [Tasks](#chap06.xhtml_chapterXXXTasks) | [Thread-Specific Storage (Pattern)](#chap13.xhtml_chapterXXXThread-SpecificSSSStorageSSSBOBOBOPatternBCBCBC) |
| [test_and_set](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) | [thread::hardware_concurrency](#chap06.xhtml_chapterXXXOperationsZZZjoinZZZdetachZZZjoinableZZZget_idZZZthis_threadCCCget_idZZZthreadCCChardware_concurrencyZZZthis_threadCCCsleep_untilZZZthis_threadCCCsleep_forZZZthis_threadCCCyield) |
| [The Atomic Flag](#chap05.xhtml_chapterXXXTheSSSAtomicSSSFlag) | [Threads versus Tasks](#chap06.xhtml_chapterXXXThreadsSSSversusSSSTasks) |
| [The Challenges](#chap05.xhtml_chapterXXXTheSSSChallenges) | [Threads](#chap06.xhtml_chapterXXXThreads) |
| [The Class Template std::atomic](#chap05.xhtml_chapterXXXTheSSSClassSSSTemplateSSSstdCCCatomic) | [Time Duration](#chap21.xhtml_chapterXXXTimeSSSDuration) |
| [The Class Template std::atomic_ref](#chap05.xhtml_chapterXXXTheSSSClassSSSTemplateSSSstdCCCatomic_ref) | [Time Library](#chap21.xhtml_chapterXXXTimeSSSLibrary) |
| [The Contract](#chap05.xhtml_chapterXXXTheSSSContract) | [Time Point](#chap21.xhtml_chapterXXXTimeSSSPoint) |
| [The Details](#chap04.xhtml_PartXXXTheSSSDetails) | [time_since_epoch](#chap21.xhtml_textXXXtime_since_epoch) |
| [The Foundation](#chap05.xhtml_chapterXXXTheSSSFoundation) | [time_t](#chap21.xhtml_textXXXto_time_tZZZtime_tZZZgmtimeZZZasctime) |

| [timed_mutex](#chap06.xhtml_textXXXmutexZZZrecursive_mutexZZZtimed_mutexZZZrecursive_timed_mutex) | [wait (atomic)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [timeout (future_status)](#chap06.xhtml_textXXXreadySSSBOBOBOfuture_statusBCBCBCZZZtimeoutSSSBOBOBOfuture_statusBCBCBCZZZdeferredSSSBOBOBOfuture_statusBCBCBC) | [wait (atomic_flag)](#chap05.xhtml_textXXXtest_and_setZZZclearZZZis_lock_freeSSSBOBOBOatomicBCBCBCZZZloadSSSBOBOBOatomicBCBCBCZZZstoreSSSBOBOBOatomicBCBCBCZZZexchangeSSSBOBOBOatomicBCBCBCZZZfetch_addSSSBOBOBOatomicBCBCBCZZZfetch_subSSSBOBOBOatomicBCBCBCZZZfetch_orSSSBOBOBOatomicBCBCBCZZZfetch_andSSSBOBOBOatomicBCBCBCZZZfetch_xorSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomicBCBCBCZZZnotify_allSSSBOBOBOatomicBCBCBCZZZwaitSSSBOBOBOatomicBCBCBCZZZnotify_oneSSSBOBOBOatomic_flagBCBCBCZZZnotify_allSSSBOBOBOatomic_flagBCBCBCZZZwaitSSSBOBOBOatomic_flagBCBCBC) |
| [to_compatible](#chap10.xhtml_textXXXsimd_castZZZstatic_simd_castZZZto_fixed_sizeZZZto_compatibleZZZto_nativeZZZsplitZZZconcat) | [wait (barrier)](#chap08.xhtml_textXXXarriveZZZwaitSSSBOBOBObarrierBCBCBCZZZarrive_and_waitSSSBOBOBObarrierBCBCBCZZZarrive_and_drop) |
| [to_fixed_size](#chap10.xhtml_textXXXsimd_castZZZstatic_simd_castZZZto_fixed_sizeZZZto_compatibleZZZto_nativeZZZsplitZZZconcat) | [wait (condition_variable)](#chap06.xhtml_textXXXnotify_oneSSSBOBOBOcondition_variableBCBCBCZZZnotify_allSSSBOBOBOcondition_variableBCBCBCZZZwaitSSSBOBOBOcondition_variableBCBCBCZZZwait_forSSSBOBOBOcondition_variableBCBCBCZZZwait_untilSSSBOBOBOcondition_variableBCBCBCZZZnative_handleSSSBOBOBOcondition_variableBCBCBC) |
| [to_native](#chap10.xhtml_textXXXsimd_castZZZstatic_simd_castZZZto_fixed_sizeZZZto_compatibleZZZto_nativeZZZsplitZZZconcat) | [wait (future)](#chap06.xhtml_textXXXshareZZZgetZZZvalidSSSBOBOBOfutureBCBCBCZZZwaitSSSBOBOBOfutureBCBCBCZZZwait_forSSSBOBOBOfutureBCBCBCZZZwait_untilSSSBOBOBOfutureBCBCBC) |
| [to_time_t](#chap21.xhtml_textXXXto_time_tZZZtime_tZZZgmtimeZZZasctime) | [wait (latch)](#chap08.xhtml_textXXXcount_downZZZtry_waitZZZarrive_and_waitSSSBOBOBOlatchBCBCBCZZZwaitSSSBOBOBOlatchBCBCBC) |
| [top::stack](#chap17.xhtml_textXXXpushCCCstackZZZpopCCCstackZZZtopCCCstack) | [wait-free (Glossary)](#chap23.xhtml_glossaryXXXwaitMMMfreeSSSBOBOBOGlossaryBCBCBC) |
| [total order (Glossary)](#chap23.xhtml_glossaryXXXtotalSSSorderSSSBOBOBOGlossaryBCBCBC) | [wait_for (condition_variable)](#chap06.xhtml_textXXXnotify_oneSSSBOBOBOcondition_variableBCBCBCZZZnotify_allSSSBOBOBOcondition_variableBCBCBCZZZwaitSSSBOBOBOcondition_variableBCBCBCZZZwait_forSSSBOBOBOcondition_variableBCBCBCZZZwait_untilSSSBOBOBOcondition_variableBCBCBCZZZnative_handleSSSBOBOBOcondition_variableBCBCBC) |
| [transaction-unsafe](#chap10.xhtml_textXXXatomic_noexceptZZZatomic_commitZZZatomic_cancelZZZtransaction-unsafe) | [wait_for (future)](#chap06.xhtml_textXXXshareZZZgetZZZvalidSSSBOBOBOfutureBCBCBCZZZwaitSSSBOBOBOfutureBCBCBCZZZwait_forSSSBOBOBOfutureBCBCBCZZZwait_untilSSSBOBOBOfutureBCBCBC) |
| [transaction_safe versus transaction_unsafe Code](#chap10.xhtml_chapterXXXtransaction_safeSSSversusSSStransaction_unsafeSSSCode) | [wait_until (condition_variable)](#chap06.xhtml_textXXXnotify_oneSSSBOBOBOcondition_variableBCBCBCZZZnotify_allSSSBOBOBOcondition_variableBCBCBCZZZwaitSSSBOBOBOcondition_variableBCBCBCZZZwait_forSSSBOBOBOcondition_variableBCBCBCZZZwait_untilSSSBOBOBOcondition_variableBCBCBCZZZnative_handleSSSBOBOBOcondition_variableBCBCBC) |
| [transaction_safe](#chap10.xhtml_textXXXtransaction_safeZZZtransaction_unsafe) | [wait_until (future)](#chap06.xhtml_textXXXshareZZZgetZZZvalidSSSBOBOBOfutureBCBCBCZZZwaitSSSBOBOBOfutureBCBCBCZZZwait_forSSSBOBOBOfutureBCBCBCZZZwait_untilSSSBOBOBOfutureBCBCBC) |
| [transaction_unsafe](#chap10.xhtml_textXXXtransaction_safeZZZtransaction_unsafe) | [Weak Memory Model](#chap05.xhtml_chapterXXXWeakSSSMemorySSSModel) |
| [Transactional Memory](#chap10.xhtml_chapterXXXTransactionalSSSMemory) | [when_all](#chap10.xhtml_chapterXXXwhen_anyZZZwhen_all) |
| [transform_exclusive_scan](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) | [when_any](#chap10.xhtml_chapterXXXwhen_anyZZZwhen_all) |
| [transform_inclusive_scan](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) | [where](#chap10.xhtml_textXXXconst_where_expressionZZZwhere_expressionZZZwhere) |
| [transform_reduce](#chap07.xhtml_textXXXfor_eachZZZfor_each_nZZZexclusive_scanZZZinclusive_scanZZZtransform_exclusive_scanZZZtransform_inclusive_scanZZZreduceZZZtransform_reduceZZZpartial_sumZZZaccumulate) | [where_expression](#chap10.xhtml_textXXXconst_where_expressionZZZwhere_expressionZZZwhere) |
| [Transitivity](#chap05.xhtml_chapterXXXTransitivity) |   |
| [TriviallyCopyable (Glossary)](#chap23.xhtml_glossaryXXXTriviallyCopyableSSSBOBOBOGlossaryBCBCBC) |   |
| [try_acquire](#chap08.xhtml_textXXXcountingSSSsemaphoresZZZmaxSSSBOBOBOcounting_semaphoreBCBCBCZZZreleaseSSSBOBOBOcounting_semaphoreBCBCBCZZZacquireZZZtry_acquireZZZtry_acquire_forZZZtry_acquire_until) |   |
| [try_acquire_for](#chap08.xhtml_textXXXcountingSSSsemaphoresZZZmaxSSSBOBOBOcounting_semaphoreBCBCBCZZZreleaseSSSBOBOBOcounting_semaphoreBCBCBCZZZacquireZZZtry_acquireZZZtry_acquire_forZZZtry_acquire_until) |   |
| [try_acquire_until](#chap08.xhtml_textXXXcountingSSSsemaphoresZZZmaxSSSBOBOBOcounting_semaphoreBCBCBCZZZreleaseSSSBOBOBOcounting_semaphoreBCBCBCZZZacquireZZZtry_acquireZZZtry_acquire_forZZZtry_acquire_until) |   |
| [try_lock](#chap06.xhtml_textXXXlockSSSBOBOBOunique_lockBCBCBCZZZtry_lockZZZtry_lock_forZZZtry_lock_untilZZZreleaseSSSBOBOBOunique_lockBCBCBCZZZowns_lockZZZunlock) |   |
| [try_lock_for](#chap06.xhtml_textXXXlockSSSBOBOBOunique_lockBCBCBCZZZtry_lockZZZtry_lock_forZZZtry_lock_untilZZZreleaseSSSBOBOBOunique_lockBCBCBCZZZowns_lockZZZunlock) |   |
| [try_lock_until](#chap06.xhtml_textXXXlockSSSBOBOBOunique_lockBCBCBCZZZtry_lockZZZtry_lock_forZZZtry_lock_untilZZZreleaseSSSBOBOBOunique_lockBCBCBCZZZowns_lockZZZunlock) |   |
| [try_wait](#chap08.xhtml_textXXXcount_downZZZtry_waitZZZarrive_and_waitSSSBOBOBOlatchBCBCBCZZZwaitSSSBOBOBOlatchBCBCBC) |   |
| [Typical Usage Pattern (Lock-Based Data Structures)](#chap17.xhtml_chapterXXXTypicalSSSUsageSSSPatternSSSBOBOBOLock-BasedSSSDataSSSStructuresBCBCBC) |   |
| [Typical Use-Cases](#chap08.xhtml_chapterXXXTypicalSSSUseMMMCases) |   |
| **U** |   |
| [Underlying Concepts](#chap08.xhtml_chapterXXXUnderlyingSSSConcepts) |   |
| [Unified Futures](#chap10.xhtml_chapterXXXUnifiedSSSFutures) |   |
| [unique_lock](#chap06.xhtml_chapterXXXunique_lock) |   |
| [unlock](#chap06.xhtml_textXXXlockSSSBOBOBOunique_lockBCBCBCZZZtry_lockZZZtry_lock_forZZZtry_lock_untilZZZreleaseSSSBOBOBOunique_lockBCBCBCZZZowns_lockZZZunlock) |   |
| [us (time literal)](#chap21.xhtml_textXXXhSSSBOBOBOtimeSSSliteralBCBCBCZZZminSSSBOBOBOtimeSSSliteralBCBCBCZZZsSSSBOBOBOtimeSSSliteralBCBCBCZZZmsSSSBOBOBOtimeSSSliteralBCBCBCZZZusSSSBOBOBOtimeSSSliteralBCBCBCZZZnsSSSBOBOBOtimeSSSliteralBCBCBC) |   |
| **V** |   |
| [valid (future)](#chap06.xhtml_textXXXshareZZZgetZZZvalidSSSBOBOBOfutureBCBCBCZZZwaitSSSBOBOBOfutureBCBCBCZZZwait_forSSSBOBOBOfutureBCBCBCZZZwait_untilSSSBOBOBOfutureBCBCBC) |   |
| [valid (parameter_pack)](#chap06.xhtml_textXXXget_futureSSSBOBOBOparameter_packBCBCBCZZZset_valueSSSBOBOBOparameter_packBCBCBCZZZresetZZZmake_ready_future_at_thread_exitZZZvalidSSSBOBOBOparameter_packBCBCBC) |   |
| [value object](#chap13.xhtml_textXXXvalueSSSobject) |   |
| [Various waiting strategies](#chap21.xhtml_chapterXXXVariousSSSwaitingSSSstrategies) |   |
| [vector_aligned](#chap10.xhtml_textXXXelement_aligned_tagZZZelement_alignedZZZvector_aligned_tagZZZvector_alignedZZZoveraligned_tagZZZoveraligned) |   |
| [vector_aligned_tag](#chap10.xhtml_textXXXelement_aligned_tagZZZelement_alignedZZZvector_aligned_tagZZZvector_alignedZZZoveraligned_tagZZZoveraligned) |   |
| [volatile (Glossary)](#chap23.xhtml_chapterXXXvolatileSSSBOBOBOGlossaryBCBCBC) |   |
| **W** |   |