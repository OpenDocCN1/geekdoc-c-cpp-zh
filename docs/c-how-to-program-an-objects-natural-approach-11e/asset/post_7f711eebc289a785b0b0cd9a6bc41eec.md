
By placing operations in a **critical section**, we allow only one thread at a time to acquire the lock and perform the operations. If multiple **critical sections** are synchronized with the same **mutex**, only one can execute at a time. Line 83 defines **mutex** data member `m_mutex`, which we’ll use in conjunction with `m_cv` to protect the **critical sections** of code in `SynchronizedBuffer`’s **put** and **get** functions that access the class’s shared mutable data. For data that requires **mutually exclusive** access, the C++ Core Guidelines recommend defining the data together with the **mutex** used to protect it. For example, we will protect `SynchronizedBuffer`’s data members by using a **mutex** that’s also a data member of `SynchronizedBuffer`.⁵⁴

In **multithreaded programs**, place all accesses to shared mutable data inside **critical sections** that synchronize on the same `std::mutex`. All operations within that critical section represent an **atomic** operation. Promptly release the lock when it’s no longer needed.

## SynchronizedBuffer Member Functions

Functions **put** (lines 16–44) and **get** (lines 47–78) provide synchronized access to the shared data members `m_occupied` and `m_buffer`. Only one thread at a time can enter either of these functions’ critical sections on a particular SynchronizedBuffer object. Variable `m_occupied` is used in **put** and **get** to determine whether it’s the producer’s turn to write or the consumer’s turn to read:

- If `m_occupied` is false, `m_buffer` is empty, so the producer can place a value into `m_buffer`, but the consumer cannot read `m_buffer`’s value.
- If `m_occupied` is true, `m_buffer` is full, so the consumer can read `m_buffer`’s value, but the producer cannot place a value into `m_buffer`.

### Member Function `put` and the Producer Thread

You’ll synchronize access to SynchronizedBuffer’s shared mutable data using the class’s **condition_variable**, **mutex** and a `std::unique_lock`, which among its capabilities can lock a **mutex** that’s used in conjunction with a **condition_variable**. When the producer thread invokes **put**, it must first acquire `m_mutex`’s lock to ensure that it has exclusive access to SynchronizedBuffer’s shared mutable data. You acquire a **mutex**’s lock by creating a **lock** object and initializing it with the **mutex** (line 20). If the **mutex**’s lock is not available, the thread creating the lock object is blocked and must wait until it can acquire the lock. Once the thread acquires the lock, the rest of that block is said to be guarded by the **mutex**.

As you’ll see momentarily, a **unique_lock** can release a **mutex**’s lock when it’s not a given thread’s turn to perform its task, then can reacquire the lock later. This capability is important. Holding a lock on the SynchronizedBuffer’s **mutex** when a thread cannot perform its task could cause **deadlock**.

### Acquiring the Lock and Checking Whether It’s the Producer’s Turn

When the `m_mutex`’s lock is available, line 20 acquires the lock. Then, line 22 checks whether `m_occupied` is true. If so, `m_buffer` is full, and the producer thread must wait until `m_buffer` is empty, so lines 23–25 output a message indicating that

- the producer thread is trying to write a value,
- `m_buffer` is full and
- the producer thread is waiting until there’s space.

### Waiting on the Condition Variable

Condition variables can be used to make a thread wait while a condition is not satisfied then to notify a waiting thread to proceed when a condition is satisfied:

- If the producer thread obtains the **mutex**’s lock, but the buffer is full, the thread calls **condition_variable**’s **wait** function (line 30), passing the **unique_lock** (`dataLock`) as the first argument. This causes `dataLock` to release the **mutex**’s lock, places the producer in **condition_variable**’s waiting state and removes the thread from contention for a processor. This is important because the producer thread cannot currently perform its task. So, the consumer should be allowed to access the **SynchronizedBuffer** to allow the condition (`m_occupied`) to change. Now the consumer can attempt to acquire the lock on `m_mutex`.
- When the consumer thread executing the critical section in the **get** function satisfies the condition on which the producer thread may be waiting—that is, the consumer reads the buffer’s value, so the buffer is empty—the consumer thread calls **notify_one** on `m_cv` (line 75). This allows the producer thread waiting on that condition to transition to the **ready state**.⁵⁵ When the operating system moves the producer thread to the **running state**, it can attempt to reacquire the lock.⁵⁶

Once the producer is notified and implicitly reacquires **m_mutex**’s lock, **put** continues executing with the next statement after the **wait** call.

### Spurious Wakeup

Occasionally, the system could move a waiting thread back into the ready state before that thread can perform its task—this is known as a spurious wakeup.⁵⁷,⁵⁸ The **wait** function’s second argument in line 30 is a no-argument lambda that checks whether it’s the producer thread’s turn to access `m_buffer`. When the producer thread gets the processor, it first reacquires the `m_mutex`’s lock, then calls this lambda. If the lambda returns false, the thread releases the lock and returns to **condition_variable** `m_cv`’s waiting state; otherwise, the producer thread continues executing.

### Updating the SynchronizedBuffer’s State

Line 34 assigns the produced value to `m_buffer`. Line 35 sets `m_occupied` to true to indicate that `m_buffer` now contains a value (i.e., a consumer can read the value, but a producer cannot yet put another value there). Lines 37–39 indicate that the producer is writing a value into the `m_buffer`.

### Releasing a Lock

At this point, execution reaches line 40—the end of the block that defines **put**’s critical section. When a thread finishes using a shared object that’s managed with **unique_lock**, the thread must release the lock by calling the lock’s `unlock` function implicitly or explicitly. Lock objects use RAII (discussed in Section 11.5). If you do not explicitly call `unlock`, class **unique_lock**’s destructor will implicitly call it when the lock goes out of scope at the end of the **critical section**. If the consumer thread was previously **blocked** while attempting to enter **get**’s critical section, which is guarded by the same **mutex**, the consumer thread can now acquire the lock to proceed.

### Notifying the Consumer Thread to Continue

Now that the buffer is full, the producer thread calls `m_cv`’s **notify_one** function (line 43) to indicate that the buffer’s state has changed. If the consumer is waiting on this condition variable, it enters the ready state and becomes eligible to reacquire the lock. Function **notify_one** returns immediately, then **put** returns to its caller (i.e., the producer thread). For performance, you should unlock the **unique_lock** before calling **notify_one** (or **notify_all**) to ensure that the notified waiting thread does not need to wait for the mutex lock to become available.

### Member Function `get` and the Consumer Thread

Functions **get** and **put** are implemented similarly. When the consumer thread invokes **get**, line 53 creates a **unique_lock** and attempts to acquire `m_mutex`’s lock. If the lock is not available (e.g., the producer has not yet released it), the **consumer thread is blocked until the lock becomes available**. If it is available, line 53 acquires it, so the consumer thread now owns the lock. Next, line 55 checks whether `m_occupied` is false. If so, `m_buffer` is empty, so lines 56–58 indicate that

- the consumer thread is trying to read a value,
- the buffer is empty and
- the consumer thread is waiting.

### Waiting on the Condition Variable

Line 63 invokes the `m_cv`’s **wait** function to place the consumer thread in that **condition_variable**’s waiting state. Again, **wait** causes `dataLock` to release `m_mutex`’s lock, so the producer thread can attempt to acquire it and do its work.

The consumer thread remains in the **waiting state** until it’s notified by the producer thread to proceed. At that point, the consumer thread returns to the **ready state**. When the operating system moves the thread to the **running state**, the consumer thread attempts to implicitly reacquire `m_mutex`’s lock. If it’s available, the consumer thread reacquires it and **get** continues executing with the next statement after **wait**. The second argument to `m_cv`’s **wait** function is a lambda that checks whether it’s the consumer thread’s turn. If

54. C++ Core Guidelines, “CP.50: Define a mutex Together with the Data It Guards.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-mutex.

55. From a December 6, 2021, email correspondence with Anthony Williams: “Condition variables do not specify which thread is woken when `notify_one` is called. It is valid for *all* the waiting threads to be woken. … In particular, it is often most efficient from an OS perspective to allow the thread that has been waiting the shortest time to be woken …, as its data might still be in cache.”

56. In some applications, when a thread reacquires the lock, it still might not be able to perform its task—in which case, it will reenter the condition variable’s waiting state and implicitly release the lock.

57. Marius Bancila, *Modern C++ Programming Cookbook*, 2/e, p. 422. Birmingham, UK: Packt Publishing, 2020.

58. “Spurious Wakeup.” Accessed April 18, 2023. https://en.wikipedia.org/wiki/Spurious_wakeup.
