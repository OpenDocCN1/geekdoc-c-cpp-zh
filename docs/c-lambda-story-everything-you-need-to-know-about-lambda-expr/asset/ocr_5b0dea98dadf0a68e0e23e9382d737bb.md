To fix the issue, as regular threading scenarios, we should use some sort of a synchronisation mechanism. For this example, we can use atomics as they seem to be the easiest to use.

Changing atomic value. Live code @Wandbox

```
#include <iostream>
#include <thread>
#include <vector>

int main() {
    std::atomic<int> counter = 0;

    const auto maxThreads = std::thread::hardware_concurrency();
    std::vector<std::thread> threads(maxThreads);
    threads.reserve(maxThreads);
    for (int tCounter=0; tCounter < maxThreads; ++ tCounter) {
        threads.push_back([&counter]() noexcept {
            for (int i = 0; i < 1000; ++ i) {
                counter.fetch_add(1);
                counter.fetch_sub(1);
                counter.fetch_add(1);
                counter.fetch_sub(1);
            }
        });
    }

    for (auto &thread : threads) {
        thread.join();
    }

    std::cout << counter.load() << std::endl;
}
```

The code above works as expected because increment and decrement operations are now atomic. It means that when value cannot interrupt this action. The synchronisation makes code safer but at a price of the performance. This is, however, a topic for a much longer discussion and a separate book.

+   Another option to solve the synchronisation problem is to have a local variable in each thread that is computed. Then, before the thread ends, we could lock and update the global value. It is also worth adding that defining a variable volatile doesn't provide correct synchronisation. In C++20 volatile is deprecated in many places.