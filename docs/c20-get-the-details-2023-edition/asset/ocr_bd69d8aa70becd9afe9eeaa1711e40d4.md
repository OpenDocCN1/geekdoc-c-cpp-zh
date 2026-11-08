![](bbox=[0.263, 0.111, 0.737, 0.38])

Multiple time synchronizations with condition variables

The average execution time is 0.52 seconds.

Porting this workflow to `std::atomic_flag` in C++20 is straightforward.

# ## 7.5.2 `std::atomic_flag`

Here is the same workflow using two atomic flags and then one.

# ### 7.5.2.1 Two Atomic Flags

In the following program, I replace the waiting on the condition variable with the waiting on the atomic flag and the condition variable’s notification with the atomic-flag setting followed by the notification.

Multiple time synchronizations with two atomic flags

```
```cpp
// PingPongAtomicFlags.cpp

#include <iostream>
#include <atomic>
#include <thread>

std::atomic_flag condAtomicFlag1{};
std::atomic_flag condAtomicFlag2{};

std::atomic<int> counter{};
constexpr int countLimit = 1'000'000;
```
```