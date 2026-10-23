```
```cpp
// Set the data and set the boolean to true (i.e. ready)
data = 3.1415;

ready.store(true);
}

void Consumer(int n)
{
    // Hang around wait waiting for the data to be ready
    while (!ready.load())
    {
        std::cout.put('.').flush();

        // Go back to sleep
        std::this_thread::sleep_for
            (std::chrono::milliseconds(100));
    }

    std::cout << "\nValue of data is from consumer: "
              << n << ", " << data << std::endl;
}
```
```

A test program using threads and C++ tasks (as discussed in Chapter 29) is:

```
```cpp
#include <thread>
#include <future>
#include <atomic>
#include <chrono>
#include <iostream>

int main()
{
    std::thread producer (Producer);
    std::thread consumer1 (Consumer, 1);
    std::thread consumer2(Consumer, 2);

    producer.join();
    consumer1.join();
    consumer2.join();

    std::cout << "\n\nSolution using tasks\n";
    // Same using tasks and async()
    auto p = std::async(std::launch::async, Producer);
    auto c1 = std::async(std::launch::async, Consumer, 1);
    auto c2 = std::async(std::launch::async, Consumer, 2);

    return 0;
}
```
```