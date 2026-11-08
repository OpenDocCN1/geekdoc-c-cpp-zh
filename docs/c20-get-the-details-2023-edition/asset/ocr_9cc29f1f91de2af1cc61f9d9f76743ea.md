# co_await has a time duration

```
```cpp
// suspendsNeverWithSleepAwaitTransform.cpp

...

Job prepareJob() {
    using namespace std::chrono_literals;
    co_await 0.1ms;
}
```
```

Second, the promise type supports a member function `await_transform` that gets the time duration and returns the Awaitable.

# **The promise with a member function await_transform**

```
```cpp
// suspendsNeverWithSleepAwaitTransform.cpp

...

struct promise_type {
    ...
    auto await_transform(std::chrono::duration<double, std::milli> sleepDuration) {
        return MySuspendNever(sleepDuration);
    }
    ...
};
```
```

The `co_await` operator needs an Awaitable as an argument. Typically, the Awaitable becomes the Awaiter.

# ### 6.1.4.2 Awaiter

The concept Awaiter requires three member functions `await_ready`, `await_suspend`, and `await_resume`.