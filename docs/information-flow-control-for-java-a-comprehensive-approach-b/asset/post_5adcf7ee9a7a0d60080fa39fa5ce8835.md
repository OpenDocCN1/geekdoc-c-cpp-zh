
## Chapter 3
## Concurrency

Both standard Java (JSE) and Java for embedded devices (J2ME) support several threads of execution at the same time, either virtually dispatched to a single processor or running concurrently on multiple multicore architectures. These threads share main memory, whereas the heap objects themselves. Threads in Java are integrated into the programming language itself, whereas languages need to include a multi-threading library that accesses native operating system routines. Therefore, threads in Java are much more system-independent than in other languages.

As Java is an object-oriented language, each thread running in the Java VM is an object of the Thread class. There is no other way for a user to create a thread via a `Thread object` whose `start` method is invoked. In such a case, a new thread is spawned and the run method of this thread is executed. All threads share a single heap for objects of threads and their interactions consist of synchronous communication via shared variables (i.e., at least two threads share the reference to a heap memory).²

Making threads independent of the base operating system required the definition of semantics for thread operations. Apart from that, the Java designers wanted to give compilers the ability to apply aggressive optimizations while at the same time giving programmers a kind of security. As a result, the `Java Memory Model (JMM)` was released on JSR-133 and incorporated into Java 1.5 [GSJB05].

### 3.1 The New Java Memory Model

A memory model answers the question on which conditions the value of a shared variable that has been previously (re)defined in another thread. With multicore having separate caches, it is no longer the case that one thread might ever, let alone immediately, see the result of an operation in another thread. 

> ¹In analogy to previous work, the term thread will mean a thread of execution in the operating system, an instance of the thread class will be called a thread object.\²If one thread *t1* calls a (non-synchronization) method of the thread object *t2* (where *t2* corresponds to a thread executing in parallel to *t1*), this is nevertheless executed in *t1*'s thread of execution, thus will only interact with *t2*'s thread in terms of shared memory.

## CHAPTER 3. CONCURRENCY

Defining a precise memory model has several advantages:
First, describing the behaviors that multithreaded programs are allowed to exhibit all kinds of compiler optimizations, even if such an optimization is not known or implemented by the time the memory model is defined. To remain consistent, the Java Language Specification requires an as-if semantics within thread boundaries that programmers are used from sequential programming. And, the specification committee wanted to guarantee a certain level of security, even if the program is insufficiently synchronized: The result of an unsynchronized field access is not defined in traditional programming languages, which might lead to reading an arbitrary value from memory (e.g. a stale value). The JMM defines a value to that in this thread before the read instruction may even be seen, in the case of race conditions.³

Requiring that every processor in a shared-memory multiprocessor environment immediately sees what all the processors are doing is expensive in contemporary architectures, which only appear to adhere to the Von Neumann model. In practice, this requirement would abandon nearly all recent achievements in speeding up processors, like pipelining, caches or speculative execution. Therefore, all architectures use more or less relaxed notion of memory-coherence and require the operating system, compilers and sometimes even to insert special instructions (fences) to guarantee safe sharing of data. Java’s write once, run everywhere philosophy thus the definition of a common memory model, which is enforced by the JVM in terms of the program’s memory.

The JMM describes, based on a program and a corresponding execution trace, whether the trace is a legal execution of the program. To this end, it validates for each read, the observed value follows certain rules. Implementations of the JMM need only make sure that the execution produces a result that can be derived from the rules in the JMM, but are free in all other details. In particular, all present and future compiler optimizations are legal, if they adhere to those rules.

The actions of each thread in isolation must obey an as-if-serial semantics i.e all actions must execute in the same order as the thread’s statements are ordered in the program, with the additional restriction that the observed values of shared variables must adhere to the rest of the memory model. As-if-serial semantics does, however, not restrict optimizations that change a thread’s semantics but preserve that appearance (e.g. loop invariant code motion).

In Java, all instance and static fields and arrays are stored in shared heap memory and are therefore affected by the memory model. In contrast, local variables in methods of formal method or exception handler parameters are not shared and thus need only adhere to intra-thread semantics. For the rest of the memory model, the term variable will denote a shared variable. Two

> ³An exception to this exists for 64 bit values, where access may be split into two accesses of 32 bit holds, so an inconsistent value might be observed in the case of insufficient synchronization.

### 3.1. THE JAVA MEMORY MODEL

access (reads or writes) to the same variable are said to be *conflicting*, if at least one is a write. (Wait, re-reading for flow): 
access (reads or writes) to the same variable are said to be *conflicting*, if at least one is a write. An *inter-thread action* is an action by one thread, that can be detected or directly influenced by another thread. The inter-thread actions include reads and writes to variables, locks and unlocks of monitors [Hoa74] as short-term scheduling means, and starting and joining of threads. Mid-term scheduling is provided via Bunch-Hansen style [BIH73] signal-and-continue [How76] notify/notifyAll.

The JMM guarantees visibility of results between two inter-thread actions only if they are ordered by a partial ordering called *happens-before*. If two actions are not ordered by happens-before, the JVM may reorder them arbitrarily allows compiler optimizations. Two conflicting accesses are said to form a data race (also, *race condition*), if they are not ordered by happens-before. A correctly synchronized program in Java exhibits no data races.

Happens-before is defined by the rules [GJSB05, GPB06]:

 **Program order** defines that each action in a thread happens-before every action in that thread that follows in the program order.
- **Monitor lock** unlock on a monitor lock happens-before every subsequent lock on the same monitor.⁴
- **Volatile variable** A read to a volatile variable happens-before every subsequent read on that same variable.
- **Thread start** A call to `Thread.start` happens-before every action in the started thread.
- **Thread termination** Any action in a thread happens-before any other thread detects that the thread has terminated through `join` or `isAlive` of class Thread.
- **Interruption** A thread calling `interrupt` on another thread happens-before the interrupted thread detects the interrupt through an `InterruptedException` or `isInterrupted` or interrupted.
- **Finalizer** The end of a constructor happens-before the start of a finalizer for that object.
- **Transitivity** Happens-before is transitive.

The transitive rule with program order makes synchronization on the same variable possible a fence instruction, all actions in one thread before a lock release are visible in the other thread after its subsequent acquisition. The same holds for a write and a read of a volatile variable. However, if two threads synchronize on different locks, there is no happens-before relation and therefore no ordering required.

> ⁴This rule includes wait/notify synchronization, due to the implicit unlocking of wait.
