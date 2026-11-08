```
```cpp
std::cout << '\n';
}
```
```

The main program starts two threads, nonInterruptible and interruptible (lines 5 and 14). Only thread interruptible gets a `std::stop_token`, which it uses in line 18 to check if it is interrupted. The lambda immediately returns in case of an interruption. The call to `interruptible.request_stop()` triggers the cancellation of the thread. Calling `nonInterruptible.request_stop()` has no effect.

![](bbox=[0.263, 0.284, 0.737, 0.775])

# 3.4.5 `std::jthread`

`std::jthread` stands for joining thread. `std::jthread` extends `std::thread` by automatically joining the started thread. `std::jthread` can also be interrupted.

[^10]: https://en.cppreference.com/w/cpp/thread/jthread