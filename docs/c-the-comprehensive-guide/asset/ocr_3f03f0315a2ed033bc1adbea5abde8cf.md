# ## 29.2  Shared Data

Each thread has its own stack. This means local variables and function parameters belong to it and it only. Another thread does not get to see them and, above all, cannot change them.

Global variables and heap memory are shared among all threads. If one thread changes a global variable, then another thread will notice—but when is hard to say.

Within a thread, it is guaranteed that one statement happens *after* the next. This may sound trivial, but it is not. I want to remind you of Chapter 4, because what applies to statements does not apply to expressions: In `func(a(), b())` it is not specified that `a()` is executed before `b()` (or vice versa). Only from statement to statement is there a guarantee that operations between them appear to be completed. I emphasize the latter because the system promises to make it look to you as if the operations are completed. If the operations do not affect each other, the compiler or hardware is free to reorder them strategically. And not only that: Even if the statements refer to each other, they may be reordered if the same result is guaranteed. And believe me, current hardware and software make extensive use of this possibilities!

However, the guarantee only applies within a single thread! When multiple threads come into play, the well-intentioned reordering of instructions in one thread can lead to another thread, which relies on the sequence of instructions in the source code, encountering a completely different state. If it uses values based on its assumptions, it can be wrong, and the calculation yields an incorrect result.

The second point is that with true parallelism, instructions are indeed executed simultaneously. Even the simplest instructions like `i += 1` become problematic. Imagine that `i += 1` is executed exactly in parallel on two cores. Then `i` will not be incremented by 2, because for that to happen, each core would need to know at all times what each of the other cores is doing.

Therefore, when accessing shared data, it is important that it is *synchronized*:

+   - First, synchronization ensures that a computation in one thread is visible to another thread. In C++, you can use atomics—that is, atomic types.
+   - Second, you synchronize write accesses so that no other thread can write or read something incomplete at that moment. For this, you use mutexes and locks—for example, mutex and lock_guard.

# ### 29.2.1  Data Races

*A data race* occurs when a variable is simultaneously used (read or written) by multiple threads and at least one of them writes. The result of the operation is then undefined.

There is no data race if all involved threads only read.