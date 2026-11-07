# Constexpr Functions

Constexpr functions are executed at compile time when called with constexpr arguments, enabling compile-time computations and ensuring the results are available during compilation. This is incredibly useful for defining constants that are computed but remain constant throughout the application's execution.

An example of a constexpr function might look like this:

```
```cpp
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : (n * factorial(n - 1));
}

int main() {
    constexpr int result = factorial(5); // Compute at compile time
    std::cout << "The factorial of 5 is: " << result << std::endl;
}
```
```