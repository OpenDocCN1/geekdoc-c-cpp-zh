```
}
while (choice!=0);    // Exit if 0 was chosen

return 0;
}
```

The added value of class `CallableClass` is that it can be used as an *exemplar* for more complicated code that you create and that will run in multithreaded mode. It can function as a reminder and refresher on precise syntax details.

# 28.3.1  Detaching a Thread

We have seen from the above examples that the calling thread must wait on its child thread by invoking a `join()` member function. There is an option, however, whereby a child thread can be detached from the calling thread. It separates the thread of execution from the thread object, allowing execution to continue independently of the parent. Any allocated resources will be freed once the thread exits. An example of use is:

```
```cpp
// Detached thread; independent execution
std::size_t n = 100;
std::vector<double> v(n);
std::iota(std::begin(v), std::end(v), 1);

{
    auto EvenOdd = [&]()
    {
        auto Even = [&](int n) { return n % 2 == 0; };
        auto Odd = [&](int n) { return !Even(n); };
        std::cout << "Number of even values: "
                  << std::count_if(std::begin(v), std::end(v), Even);
        std::cout << "Number of odd values: "
                  << std::count_if(std::begin(v), std::end(v), Odd);
    };
    std::thread t3(EvenOdd); t3.detach();

    // Put a break in order to view output
    std::cout << "Press a key ...";
    int t; std::cin >> t;
}
```
```

In a sense, we ‘fire and forget’ detached threads. The calling thread does not have to wait on detached threads. The usage is similar to a command being executed on an object.

# 28.3.2  Cooperative Tasking with Threads

Multithreading is *pre-emptive* in the sense that the scheduler allocates a fixed amount of time (a *quantum*) to each thread, after which time the thread reverts to *sleep* or *wait-to-join* mode. For example, a thread can sleep for some random time, for example: