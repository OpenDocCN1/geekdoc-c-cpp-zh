When the value of a customer is moved away, both name and values are guaranteed to have a valid state so that the destructor for them (called by the destructor of Customer) works fine:

```
~~~cpp
void foo()
{
    Customer c{"Michael Spencer"};
    ...
    process(std::move(c));
    // both name and values have valid but unspecified states
    ...
} // destructor of c will clean up name and values (whatever their state is)
~~~
```

Also, assigning a new value to c will work because we assign both the name and the values.

# 6.2.2 Non-Destructible Moved-From Objects

However, in rare cases problems might occur. In these cases, we have usually implemented an assignment operator or a destructor to do more than just assign or destroy the members.<sup>3</sup>

Consider the following class, where we use a fixed-size array of a variable number of thread objects, for which we explicitly call join() in the destructor to wait for their end:

*basics/tasks.hpp*

```
~~~cpp
#include <array>
#include <thread>

class Tasks {
private:
    std::array<std::thread,10> threads; // array of threads for up to 10 tasks
    int numThreads{0};                  // current number of threads/tasks
public:
    Tasks() = default;

    // pass a new thread:
    template <typename T>
    void start(T op) {
        threads[numThreads] = std::thread(std::move(op));
        ++numThreads;
    }
    ...

    // at the end wait for all started threads:
    ~Tasks() {
        for (int i = 0; i < numThreads; ++i) {
            threads[i].join();
        }
    }
};
~~~
```

3 We see here one reason why move semantics is disabled by default when a destructor is implemented.