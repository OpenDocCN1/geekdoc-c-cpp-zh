![](bbox=[0.21, 0.13, 0.8, 0.35])

# Terminating a joinable std::thread

Both executions of std::thread terminate. In the second run, the thread thr has enough time to display its message: "Joinable std::thread".

In the following example, I use std::jthread from the current C++20 standard.

# Terminating a still joinable std::jthread

```
```cpp
// jthreadJoinable.cpp

#include <iostream>
#include <thread>

int main() {

    std::cout << '\n';
    std::cout << std::boolalpha;

    std::jthread thr([]{ std::cout << "Joinable std::thread" << '\n'; });

    std::cout << "thr.joinable(): " << thr.joinable() << '\n';

    std::cout << '\n';

}
```
```

Now, the thread thr automatically joins in its destructor such if it's still joinable.