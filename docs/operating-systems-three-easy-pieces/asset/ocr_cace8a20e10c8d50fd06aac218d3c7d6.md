# INTERLUDE: MEMORY API

> ASIDE: Why NO Memory Is Leaked ONCE Your PROCESS EXITS

When you write a short-lived program, you might allocate some space using malloc(). The program runs and is about to complete: is there need to call free() a bunch of times before exiting? While it seems wrong not to do it, no memory will be "lost" in any real sense. The reason is simple: there are two levels of memory management in the system.
The first level of memory management is performed by the OS, which hands memory to processes when they run, and takes it back when processes exit (or otherwise die). The second level of management is within each process, for example the heap when you call malloc() and free(). Even if you fail to call free() (and thus leak memory in the heap), the operating system will reclaim all the memory of heap (including those pages for code, stack, and, as relevant, heap) when the process is finished. No matter what the state of your heap is in address space, the OS takes back all of those pages when the process dies, ensuring that no memory is lost despite the fact you didn't!

Thus, for short-lived programs, leaking memory often does not cause any operational problems (though it may be considered poor form). When you write a long-running server (such as a web server or database management system, which never exits), leaked memory is a much bigger issue, and will eventually lead to a crash when the application runs out of memory. And of course, leaking memory is an even larger issue inside one particular program: the operating system itself. Showing us out those: whose the kernel code has the toughest job of all...

# Calling free() Incorrectly

One last problem is the call of free() incorrectly. After all, free() expects you to pass to it one of the pointers you received from malloc() earlier. When you pass in some other value, bad things can (and do) happen. Thus, invalid frees are dangerous and of course should be avoided.

# Summary

As you can see, there are lots of ways to abuse memory. Because of frequent errors with memory, a whole ecosystem of tools have developed to help find problems in your code. Check both purport [HJ92] and valgrind [SN05]; both are excellent at helping you locate the source of your memory-related problems. Once you become accustomed to using these powerful tools, you will wonder how you survived without them.