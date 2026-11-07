# ### 17.6.1 Class SynchronizedBuffer: Mutexes, Locks and Condition Variables

Figures 17.7–17.8 demonstrate a producer thread and a consumer thread correctly accessing a synchronized shared mutable buffer. In this example:

+   - the producer always produces a value first,
+   - the consumer correctly consumes only after the producer produces a value and
+   - the producer correctly produces the next value only after the consumer consumes the previous (or first) value.

As you'll see, SynchronizedBuffer's put and get functions (Fig. 17.7) handle the synchronization. We output messages from these functions for demonstration purposes only. I/O is slow compared to processor operations. So, I/O should not be performed in critical sections because it's crucial to minimize the amount of time that an object is "locked."

```
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
      std::unique_lock dataLock{m_mutex};

      if (m_occupied) {
         std::cout << std::format(
            "Producer tries to write.\n{:40}{}\t{}\n",
            "Buffer full. Producer waits.", m_buffer, m_occupied);

         // wait on condition variable m_cv; the lambda in the second
         // argument ensures that if the thread gets the processor
         // before m_occupied is false, the thread continues waiting
         m_cv.wait(dataLock, [&]() {return !m_occupied;});
      }

   }
```
```

**Fig. 17.7** | SynchronizedBuffer maintains synchronized access to a shared mutable integer that is accessed by a producer thread and a consumer thread. (Part 1 of 2.)