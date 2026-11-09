# Chapter 29
# Hybrid Thread Synchronization Constructs

+   In this chapter:
+   - A Simple Hybrid Lock ........................................................ 826
+   - Spinning, Thread Ownership, and Recursion ................................. 827
+   - A Potpourri of Hybrid Constructs ............................................ 829
+   - The Famous Double-Check Locking Technique ................................. 844
+   - The Condition Variable Pattern .............................................. 848
+   - Using Collections to Avoid Holding a Lock for a Long Time .................. 851
+   - The Concurrent Collection Classes ........................................... 856

In Chapter 28, “Primitive Thread Synchronization Constructs,” I discussed the primitive user-mode and kernel-mode thread synchronization constructs. From these primitive constructs, all other thread synchronization constructs can be built. Typically, other thread synchronization constructs are built by combining the user-mode and kernel-mode constructs, and I call these hybrid thread synchronization constructs. Hybrid constructs provide the performance benefit of the primitive user-mode constructs when there is no thread contention. Hybrid constructs also use the primitive kernel-mode constructs to provide the benefit of not spinning (wasting CPU time) when multiple threads are contending for the construct at the same time. Since, in most applications, threads are rarely contending for a construct at the same time, the performance improvements can help your application greatly.

In this chapter, I will first show how hybrid constructs are built from the various primitive constructs. Then, I will introduce you to many of the hybrid constructs that ship with the Framework Class Library (FCL), describe their behavior, and give some insight as to how to use these constructs correctly. I will also mention some constructs that I have created and make available for free in Wintellect’s Power Threading library, which can be downloaded from http://Wintellect.com/.

Toward the end of the chapter, I show how to minimize resource usage and improve performance by using the FCL’s concurrent collection classes instead of using some of the hybrid constructs. And finally, I discuss the Power Threading library’s ReaderWriterGate and SyncGate classes which offer reader-writer semantics without blocking any threads, thereby also reducing resource consumption and improving performance.