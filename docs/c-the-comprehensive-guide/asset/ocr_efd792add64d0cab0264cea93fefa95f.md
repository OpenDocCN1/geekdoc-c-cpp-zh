+   - **`wait_for(std::chrono::time_point)`**
+     Waits until the result is ready or a time point is reached.

The last two do not return void, but a future_status, which you can use to check if the result is already there or if the timeout has occurred.

```
```cpp
// https://godbolt.org/z/o9oYrvMcj
#include <iostream>
#include <future>  // async
#include <chrono>
using std::cout; using std::endl; using namespace std::chrono;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
int main() {
    auto f43 = std::async(async, 43);
    while(true) {
        auto ready = f43.wait_for(500ms);
        if(ready==std::future_status::timeout) {
            std::cout << "not yet..." << std::endl;
        } else {
            break;
        }
    }
    // pick up, is immediately there
    cout << "fib(43): " << f43.get() << endl; // Output: fib(43): 701408733
}
```
```

**Listing 29.33** Waiting for a certain time with “async”.

The output for me is this:

```
```
not yet...
not yet...
not yet...
not yet...
not yet...
not yet...
fib(43): 433494437
```
```

So it was checked six times, and the result was not yet there. On the seventh time, the result was present. The following get() then immediately delivers the result.

# Waiting Forever or For a Certain Time

If you block in the thread area of the standard library with a function like wait() and can wait forever for the function to return, there are always functions that allow you to