If you carefully follow my explanation such as the one in the subsection *Challenges*, you probably expect *Relaxed Semantic* to come next; however I’ll look first at the memory model `std::memory_order_consume` which is quite similar to `std::memory_order_acquire`.

# ## 2.4.4 `std::memory_order_consume`

`std::memory_order_consume` is the most legendary of the six memory orderings. For two reasons: first, `std::memory_order_consume` is extremely hard to understand, and second - and this may change in the future - no compiler supports it currently. With C++17 the situation gets even worse. Here is the official wording: “The specification of release-consume ordering is being revised, and the use of memory_order_consume is temporarily discouraged.”

How can it be that a compiler that implements the C++11 standard doesn’t support the memory model `std::memory_order_consume`? The answer is that the compiler maps `std::memory_order_consume` to `std::memory_order_acquire`. This mapping is acceptable because both are load or acquire operations. `std::memory_order_consume` requires weaker synchronization and ordering constraints than `std::memory_order_acquire`. Therefore, the release-acquire ordering is potentially slower than the release-consume ordering but - and this is the key point - *well-defined*.

To understand the release-consume ordering, it is a good idea to compare it with the release-acquire ordering. I speak in the following subsection explicitly about the release-acquire ordering and not about the acquire-release semantic to emphasize the strong relationship of `std::memory_order_consume` and `std::memory_order_acquire`.

# ### 2.4.4.1 Release-acquire ordering

As a starting point, let us use the following program with two threads t1 and t2. t1 plays the producer’s role, t2 the consumer’s role. The atomic variable ptr helps to synchronize the producer and consumer.

Release-acquire ordering

```
```cpp
// acquireRelease.cpp

#include <atomic>
#include <thread>
#include <iostream>
#include <string>

using namespace std;

atomic<string*> ptr;
int data;
atomic<int> atoData;

void producer(){
    string* p = new string("C++11");
```
```