![](bbox=[0.271, 0.103, 0.744, 0.224])

Summation with a thread-local variable on Linux

![](bbox=[0.271, 0.256, 0.744, 0.367])

Summation with a thread-local variable on Windows

In the last scenario, I use tasks.

# ### 6.1.3.3 Using Tasks

Using tasks, we can do the whole job without explicit synchronization. Each partial summation is performed in a separate thread, and the final summation takes place in the main thread.

Here is the program:

Summation of a vector with minimal synchronization using tasks

```
```cpp
// tasksSummation.cpp

#include <chrono>
#include <future>
#include <iostream>
#include <random>
#include <thread>
#include <utility>
#include <vector>

constexpr long long size = 100000000;

constexpr long long fir =  25000000;
constexpr long long sec =  50000000;
constexpr long long thi =  75000000;
constexpr long long fou = 100000000;
```
```