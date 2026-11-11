# Equivalent expression for the three overloads

```
```cpp
// wait in lines 1 - 4
while (!token.stop_requested()) {
    if (pred()) return true;
    wait(lock);
}
return pred();

// wait_for in lines 6 - 10
return wait_until(lock,
                  std::chrono::steady_clock::now() + rel_time,
                  std::move(pred)
                  );

// wait_until in lines 12 - 16
while (!token.stop_requested()) {
    if (pred()) return true;
    if (wait_until(lock, timeout_time) == std::cv_status::timeout) return pred();
}
return pred();
```
```

After the wait calls, you can check if a stop request happened.

# Handle interrupts with wait

```
```cpp
cv.wait(lock, stoken, predicate);
if (stoken.stop_requested()){
    // interrupt occurred
}
```
```

The following example shows the use of a condition variable with a stop request.

# Use of condition variable with a stop request

```
```cpp
// conditionalVariableAny.cpp

#include <condition_variable>
#include <thread>
#include <iostream>
#include <chrono>
#include <mutex>
#include <thread>

using namespace std::literals;
```
```