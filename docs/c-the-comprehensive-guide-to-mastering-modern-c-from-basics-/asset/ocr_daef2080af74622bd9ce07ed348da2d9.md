conveniently a range adapter (view), so you can use it,
for example, with loops or combine it with operator|

```
// https://godbolt.org/z/Gfazq6GE7
#include <generator>
#include <iostream>
#include <vector>

std::generator<int> fib(int n) { // generates int values
    int a = 0, b = 1;
    while (----) {
        co_yield a; // makes this function a coroutine
        auto tmp = a;
        a = b;
        b++;
    }
}
int main() {
    for (auto i : fib(10)) std::cout << i << '\n'; // Output: 1 1 2 3 5 8 13 21 34 55
}
```

# 29.42 Your coroutine returns a "generator".

Because fib contains a co_yield, the function becomes
coroutine. The return type is std::generator<int>, and all
the magic is contained within. There you will find the
promise_type, a coroutine_handle, an iterator, and much
.

With fib(10), you enter the coroutine. It starts
immediately because the promise_type of generator is
configured that way. As soon as the compiler reaches
co_yield, the coroutine is paused and the value b is
stored in generator. Control is returned to the caller.
The for loop retrieves the int from the generator and
outputs it.

The for loop now increments the iterator, causing the
coroutine to resume. The same process occurs at the