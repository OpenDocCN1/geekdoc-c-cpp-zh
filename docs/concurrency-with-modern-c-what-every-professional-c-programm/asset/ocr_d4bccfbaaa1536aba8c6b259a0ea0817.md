![](bbox=[0.3, 0.14, 0.7, 0.31])

Usage of the Simple Queue with a Dummy Node

Now, I'm done with my refactoring. The crucial observation for the queue with a dummy node is that the `pop` member function and the `push` member function work almost entirely on different ends. This separation allows it to use a mutex for each end. Only the check (`head.get() == tail`) (line 20) in the `pop` member function requires both mutexes. This is not so bad because this critical region is short-lived.

With this knowledge in mind, let me put the pieces together and finally come to the concurrent queue with fine-grained locking.

# 13.1.3.4 The Implementation

The synchronization of the queue is based on two mutexes. One mutex protects the head, and one mutex protects the tail of the queue. The final question is: Where to put the two mutexes? To get maximum performance, the critical regions should be as short-lived as possible. This means for the member function `pop` that the entire member function has to be protected, but for the member function `push` only the instructions that use the queue's tail. The other operations are local and, therefore, thread-safe.

A Fine-Grained Concurrent Queue

```
```cpp
// concurrentQueueFineLocking.cpp

#include <future>
#include <iostream>
#include <memory>
#include <mutex>
#include <utility>

template <typename T>
class ConcurrentQueue{
private:
    struct Node{
```
```