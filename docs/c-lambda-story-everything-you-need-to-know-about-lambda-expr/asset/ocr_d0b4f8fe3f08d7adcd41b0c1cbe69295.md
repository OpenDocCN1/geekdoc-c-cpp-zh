As we can see, it's quite handy to create a thread with a lambda expression. It's local to your executing thread, and you can do everything like with a regular function or functor object.

Let's now try another technique that is available in C++.

# Lambdas with std::async

A second way that you can leverage multithreading is through std::async . We got that functionality together with threads in C++11. This is a high-level API that you set up and call computations lazily or fully asynchronously.

Let's convert our example with iota into the async call:

```
Invoking code asynchronously with std::async . Live code @Coloru
#include <iostream>
#include <future> // for async and future
#include <vector>
#include <numeric> // for std::iota

int main () {
    const auto printThreadID = [](const char * str) {
        std::cout << str << " " << std::this_thread::get_id() << " thread id \n " << ";
    };

    std::vector<int> numbers(100);

    std::future<void> iotaFuture = std::async(std::launch::async,
        [&numbers, startArg=10, &printThreadID](){
        std::iota(numbers.begin(), numbers.end(), startArg);
        printThreadID("iota in");
    });

    iotaFuture.get(); // make sure we get the results...
    printThreadID("printing numbers in");
    for (const auto &num : numbers)
        std::cout << num << " ";

}
```

This time after threads, we rely on the mechanism of std::future. This is an object that handles the synchronisation and guarantees that the results of the invocation are available when we ask it through .get().

In our case we schedule the execution of the lambda through std::async, and then we need to call .get() to finish the computations. .get()