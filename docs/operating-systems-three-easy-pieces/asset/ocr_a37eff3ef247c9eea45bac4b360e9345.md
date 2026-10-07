382

CONDITION VARIABLES

# TIP: USE WHILE (NOT IF) FOR CONDITIONS

When checking for a condition in a multi-threaded program, using a `while` loop is always correct; using an `if` statement might only be, depending on the semantics of signaling. Thus, always use `while` and your code will be as expected.

Using loops around conditional checks also handles the case where spurious wakeups occur. In some thread packages, to details of the implementation, it is possible that two threads get woken up just a single signal has taken place [L11]. Spurious wakeups are further reason to re-check the thread is waiting on.

# The Correct Producer/Consumer Solution

We have a working producer/consumer solution, albeit not a fully general one. The last change we make is enable more concurrency and efficiency; specifically, we add more buffer slots, so that multiple values can be consumed before sleeping. With a single producer and consumer, this approach is more efficient as it reduces context switches; with multiple producers or consumers (or both), it even allows producing or consuming to take place, increasing concurrency. Fortunately, it is a small change from our current solution.

The first change for this solution is within the buffer itself and the `put()` and `get()` (Figure 30.13). We also slightly change the conditions that producers and consumers check in order to determine whether to sleep or not. We also show the wait and signaling logic (Figure 30.14). A producer only sleeps if all buffers are filled (p2); similarly, a consumer only sleeps if all buffers are currently empty (c2). Thus we solve the producer/consumer problem, time to sit back and drink a cold one.

# 30.3 Covering Conditions

We'll look at one more example of how condition variables can be used. This code is drawn from Lampson and Redell's paper on Pilot [LR80], the same group who first implemented the Mesa semantics described above (the language they used Mesa, hence the name).

The problem they ran into is shown via this simple example, in this case in a multi-threaded memory allocation library. Figure 30.15 shows a snippet which demonstrates the issue.

As you see in the code, when a thread calls into the memory allocation code, it might have to wait in order for more memory to come free. Conversely, when a thread frees memory, it signals that memory is free. However, our code above has a problem: waiting thread (there can be more than one) should be woken?

OPERATING SYSTEMSn[Version 1.01]

WWW.OSTEP.ORG