# 6.1.4 Awaitables and Awaiters

The three functions of a promise object `promise.yield_value`, `initial_suspend`, and `final_suspend` return Awaitables.

# 6.1.4.1 Awaitables

An Awaitable is something you can await on. It is the argument of `co_await`: `co_await` Awaitable. The Awaitable determines if the coroutine pauses or not.

Essentially, the compiler generates the following function calls using the promise prom and the `co_await` operator.

| Call | Compiler generated call |
|---|---|
| Start coroutine execution | `co_await prom.initial_suspend()` |
| `co_yield` value | `co_await prom.yield_value(value)` |
| `co_return` value | `co_await prom.return_value(value)` |
| End coroutine execution | `co_await prom.final_suspend()` |

Thanks to the member function `await_transform`, the promise becomes the Awaitable.

# 6.1.4.1.1 `await_transform`

The following Awaitable suspends never. This example also shows how the Awaitable can get an argument.

# A special Awaitable

```
```cpp
// suspendsNeverWithSleep.cpp

#include <coroutine>
#include <chrono>
#include <format>
#include <iostream>
#include <thread>

struct MySuspendNever {
    MySuspendNever(std::chrono::duration<double, std::milli> sleep): sleepDuration(sleep) {}
    std::chrono::duration<double, std::milli> sleepDuration;
```
```