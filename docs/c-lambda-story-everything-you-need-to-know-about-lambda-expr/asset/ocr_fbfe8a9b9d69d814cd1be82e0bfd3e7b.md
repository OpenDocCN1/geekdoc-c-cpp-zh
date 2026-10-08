As you can see, inside operator () there’s no way we can access a variable of the functor type.

If you need to call lambda recursively, there are at least two tricks that you can leverage:

+   - With std::function and capturing it.
- With internal lambda and passing it as a generic parameter.

Let’s see the first option:

# With std::function

The main idea is that we assign a lambda to std::function 9 and then we can capture this into the lambda body.

> Recursive Lambda with std::function . Live code @Wandbox

```
#include <functional>
int main() {
    const std::function<int(int)> factorial = [&factorial](int n) {
        return n > 1 ? factorial(n - 1) : 1;
    };
    return factorial(5);
}
```

In the previous code sample, inside is a captured std::function object. This object is fully defined, and that’s why the compiler has no issues when accessing and calling it.

If you want to use only stateless lambdas, then you might even try with a function pointer rather than std::function as it should cost much less memory.

But there’s one more trick:

# Internal Lambda and a Generic Parameter

With C++14 we can use the following alternative:

> Recursive Lambda with internal implementation. Live code @Wandbox

```
int main() {
    const auto factorial = [](int n) noexcept {
```