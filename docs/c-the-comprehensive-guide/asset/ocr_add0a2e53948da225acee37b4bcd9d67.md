There are exactly two launch policies of type `std::launch`:

+   - `launch::async`  
+     Start a separate thread for the background computation.
+   - `launch::deferred`  
+     Wait with the computation until the result is retrieved with `get`. This does not necessarily have to happen in a separate thread.

`launch` is an enum, whose values you can combine with the `|` operator (or for) if you want to leave the choice to the standard library. `launch::deferred | launch::async` is the default behavior.

An example of deferred execution looks like the following listing.

```
```cpp
// https://godbolt.org/z/P9MjGe6Mn
#include <iostream>
#include <future>   // async
#include <vector>
using std::cout; using std::endl;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
int main() {
    // Prepare tasks
    std::vector<std::future<long>> fibs;
    for(int n=0; n<50; ++n) {
        auto fut = std::async(std::launch::deferred, fib, n);
        fibs.push_back( std::move(fut) );
    }
    // only retrieve the required result
    cout << "fib(42): " << fibs[42].get() << endl; // Output: fib(42): 267914296
}
```
```

**Listing 29.32** How to enforce deferred execution.

By the way, you don't have to wait for the result with `get` and retrieve it at the same time. You can also just wait first with `wait()`. A subsequent `get()` will then deliver the result immediately.

# 29.6.2  Wait Until a Certain Time

Instead of using `wait`, you can also wait for a certain time with `wait_for` or `wait_until`:

+   - `wait()`  
+     Waits until the result is ready.
+   - `wait_for(std::chrono::duration)`  
+     Waits until the result is ready or a duration has elapsed.