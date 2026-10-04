# CHAPTER 30

# Hybrid Thread Synchronization
Constructs

In this chapter:

+   * A Simple Hybrid Lock ............................................................................ 790
* Spinning, Thread Ownership, and Recursion ................................................ 791
* Hybrid Constructs in the Framework Class Library ................................ 793
* The Famous Double-Check Locking Technique ............................................ 807
* The Condition Variable Pattern ................................................................... 811
* Asynchronous Synchronization. ................................................................ 814
* The Concurrent Collection Classes. ....................................................... 818

In 29, "Primitive Thread Synchronization Constructs," I discussed the primitive user-mode and kernel-mode thread synchronization constructs. From these primitive constructs, all other thread synchronization constructs can be built. Typically, other thread synchronization constructs are built by comining the user-mode and kernel-mode constructs, and I call these *hybrid thread synchronization constructs*. Hybrid constructs provide the performance benefit of the primitive user-mode constructs when there is no thread contention. Hybrid constructs also use the primitive kernel-mode constructs to provide the benefit of not spinning (wasting CPU time) when multiple threads are contending for the construct at the same time. Because, in most applications, threads are rarely contending for a construct at the same time, the performance improvements can help your application greatly.

In this chapter, I show how hybrid constructs are built from the primitive constructs. Then, I will introduce you to many of the hybrid constructs that ship with the Framework Class Library (FCL), describe their behavior, and give some insight as how to use these constructs correctly. I will also mention constructs that I have created and made available for Winlett's Power Threading library, which can be downloaded from http://Wintellect.com/PowerThreading.aspx.

Toward the end of the chapter, I show how to minimize resource usage and improve performance by using the FCL's concurrent collection classes instead of some of the hybrid constructs. And finally, I discuss asynchronous synchronization constructs, which allow you to synchronize access to a resource without blocking any threads, thereby reducing resource consumption while improving scalability.