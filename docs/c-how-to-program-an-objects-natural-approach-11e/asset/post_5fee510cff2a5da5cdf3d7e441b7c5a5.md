
- the consumer reads invalid data (–1) before the producer has produced its first legitimate value or
- the consumer reads stale values it read previously.

The C++ standard emphasizes that “a memory location cannot be safely accessed by two threads without some form of locking unless they are both read accesses.”49

## Thread Synchronization, Mutual Exclusion and Critical Sections

The problems from the last example can be solved by giving only one thread at a time exclusive access to code that manipulates the shared mutable data. During that time, the other thread must wait. When the thread with exclusive access finishes accessing the shared mutable data, the waiting thread can proceed. This thread synchronization process coordinates access to shared mutable data by concurrent threads. Each thread accessing a shared object excludes the other thread from doing so simultaneously. This is called mutual exclusion. The code sections that we protect using mutual exclusion are called critical sections.

## Executing a Set of Operations As If They Are One Operation

To make our shared buffer thread safe, we must ensure that only one thread at a time can store a value in the buffer or read a value from the buffer. We must also ensure that these operations cannot be divided into smaller suboperations—known as making the operations atomic. We do this by allowing only one thread to execute `put` or `get` at a time.

- If the producer is executing `put` when the consumer tries to execute `get`, the consumer must wait until the producer finishes its `put` call.
- Similarly, if the consumer is executing `get` when the producer tries to execute `put`, the producer must wait until the consumer finishes its `get` call.

## Immutable Data Does Not Require Synchronization

The synchronization we demonstrate in the next example is required only for shared mutable data, which might change during its lifetime. Immutable data does not change, so any number of concurrent threads can access the data. The C++ Core Guidelines say, “You can’t have a race condition on a constant,” and for this reason, indicate that you should

- “use const to define objects with values that do not change after construction” and
- “use constexpr for values that can be computed at compile time.”50

Doing so indicates the variables’ values will not change after they’re initialized, preventing accidental modification that could compromise thread safety. The C++ Core Guidelines also recommend minimizing the use of shared mutable data to avoid data races.51

- 49. “C++11 Language Extensions—Concurrency.” Accessed April 18, 2023. https://isocpp.org/wiki/faq/cpp11-language-concurrency.
- 50. C++ Core Guidelines, “Const, Constants and Immutability.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#S-const.
- 51. C++ Core Guidelines, “CP.3: Minimize Explicit Sharing of Writable Data.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-data.

## 17.6.1 Class SynchronizedBuffer: Mutexes, Locks and Condition Variables

Figures 17.7–17.8 demonstrate a producer thread and a consumer thread correctly accessing a synchronized shared mutable buffer. In this example:

- the producer always produces a value first,
- the consumer correctly consumes only after the producer produces a value and
- the producer correctly produces the next value only after the consumer consumes the previous (or first) value.

As you'll see, SynchronizedBuffer's put and get functions (Fig. 17.7) handle the synchronization. We output messages from these functions for demonstration purposes only. I/O is slow compared to processor operations. So, I/O should not be performed in critical sections because it's crucial to minimize the amount of time that an object is "locked."

```cpp
// Fig. 17.7: SynchronizedBuffer.h
// SynchronizedBuffer maintains synchronized access to a shared mutable
// integer that is accessed by a producer thread and a consumer thread.
#pragma once
#include <condition_variable>
#include <format>
#include <mutex>
#include <iostream>
#include <string>

using namespace std::string_literals;

class SynchronizedBuffer {
public:
   // place value into m_buffer
   void put(int value) {
      // critical section that requires a lock to modify shared data
      // lock on m_mutex to be able to write to m_buffer
      {
         std::unique_lock dataLock{m_mutex};

         if (m_occupied) {
            std::cout << std::format(
               "Producer tries to write.\n{:<40}{}\t{}\n",
               "Buffer full. Producer waits.", m_buffer, m_occupied);

            // wait on condition variable m_cv; the lambda in the second
            // argument ensures that if the thread gets the processor
            // before m_occupied is false, the thread continues waiting
            m_cv.wait(dataLock, [&]() {return !m_occupied;});
         }

         // write to m_buffer
         m_buffer = value;
         m_occupied = true;

         std::cout << std::format("{:<40}{}\t{}\n\n",
             "Producer writes "s + std::to_string(value),
             m_buffer, m_occupied);
      } // dataLock's destructor releases the lock on m_mutex

      // if consumer is waiting, notify it that it can now read
      m_cv.notify_one();
   }

   // return value from m_buffer
   int get() {
      int value; // will store the value returned by get

      // critical section that requires a lock to modify shared data
      {
         // lock on m_mutex to be able to read from m_buffer
         std::unique_lock dataLock(m_mutex);

         if (!m_occupied) {
            std::cout << std::format("{:<40}{}\t\t{}\n\n",
                "Consumer tries to read.\nBuffer empty. Consumer waits.",
                m_buffer, m_occupied);

            // wait on condition variable m_cv; the lambda in the second
            // argument ensures that if the thread gets the processor
            // before m_occupied is true, the thread continues waiting
            m_cv.wait(dataLock, [&]() {return m_occupied;});
         }

         value = m_buffer;
         m_occupied = false;

         std::cout << std::format("{:<40}{}\t\t{}\n\n",
             "Consumer reads "s + std::to_string(m_buffer),
             m_buffer, m_occupied, std::string(34, '-'));
      } // dataLock's destructor releases the lock on m_mutex

      // if producer is waiting, notify it that it can now write
      m_cv.notify_one();

      return value;
   }
private:
   int m_buffer{-1}; // shared by producer and consumer threads
   bool m_occupied{false};
   std::condition_variable m_cv;
   std::mutex m_mutex;
};
```

**Fig. 17.7** | SynchronizedBuffer maintains synchronized access to a shared mutable integer that is accessed by a producer thread and a consumer thread. (Part 1 of 2.)

**Fig. 17.7** | SynchronizedBuffer maintains synchronized access to a shared mutable integer that is accessed by a producer thread and a consumer thread. (Part 2 of 2.)

### SynchronizedBuffer’s m_buffer and m_occupied Data Members

Line 80 defines the int data member m_buffer into which a producer thread will write data and from which a consumer thread will read data. The bool data member m_occupied (line 81) indicates whether m_buffer currently contains data. We’ll use this to help keep track of the shared buffer’s state for thread synchronization purposes. Variables m_occupied and m_buffer are both part of a SynchronizedBuffer’s state information, so you must synchronize access to both to ensure that the buffer is thread-safe.

### SynchronizedBuffer’s std::condition_variable Data Member

As part of synchronizing access to the buffer, we must ensure that the producer and consumer threads each do their work only when the buffer is in an appropriate state. We need a way to allow the threads to **wait, depending on certain conditions**, which we maintain via m_occupied:

- The producer can place a new item in the buffer only if the **buffer is not full**—that is, m_occupied is false.
- The consumer can read an item from the buffer only if the **buffer is not empty**—that is, m_occupied is true.

If a given condition is true, the corresponding thread may proceed. If it’s false, the corresponding thread must wait until it becomes true.

We also need a way to let a **waiting thread know when conditions have changed** so it can proceed:

- If the consumer is waiting to read and the producer writes a new value into the buffer, the **buffer is now full**, so the producer should **notify the waiting consumer** that it can read that value.
- If the producer is waiting to write and the consumer reads the buffer’s current value, the **buffer is now empty**, so the consumer should **notify the waiting producer** that it can write into the buffer.

These wait and notify capabilities are provided by a **std::condition_variable**⁵² (from header **<condition_variable>**). Line 82 defines the m_cv data member of this type.

### SynchronizedBuffer’s std::mutex Data Member

A common way to implement mutually exclusive access to shared mutable resources is by creating **critical sections**. These **synchronized blocks of code** execute atomically using features from the **<mutex>** header. A **std::mutex** can be owned by only one thread at a time. A thread that requires exclusive access to a resource must first acquire a lock on a **mutex**—typically at the beginning of a block of code. Other threads attempting to perform operations that require the same **mutex** will be blocked until the first thread releases the lock—typically at the end of a block of code. At that point, the blocked threads may attempt to acquire the lock and proceed with the operation.⁵³

- 52. “std::condition_variable.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/thread/condition_variable.
- 53. From a December 6, 2021, email correspondence with Anthony Williams: “There is no requirement on which thread gets the mutex lock when a mutex is unlocked. … it is often most efficient from an OS perspective to allow the thread that has been waiting the shortest time to … acquire the mutex lock, as its data still might be in cache.”
