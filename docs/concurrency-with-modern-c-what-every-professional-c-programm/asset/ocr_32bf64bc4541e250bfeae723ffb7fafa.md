![](bbox=[0.28, 0.123, 0.721, 0.284])

Using a std::jthread that joins automatically

Here is a typical implementation of std::jthreads destructor.

# Typical implementation of std::jthreads destructor

```
```cpp
jthread::~jthread() {
    if(joinable()) {
        request_stop();
        join();
    }
}
```
```

First, the thread checks if it is still joinable (line 2). A thread is still joinable if neither join() or detach() was called on it. If the thread is still joinable, it asks for the stopping of the execution (line 3) and calls join() afterward (line 4). The join call blocks until the thread's execution is done.

# 3.2.2 Cooperative Interruption of a `std::jthread`

To get the general idea, let me present a simple example.

# Interrupt an non-interruptable and interruptable `std::jthread`

```
```cpp
// interruptJthread.cpp

#include <chrono>
#include <iostream>
#include <thread>

using namespace std::literals;

int main() {

    std::cout << '\n';
```
```