deduce the return type for the wrapper lambda

LIFT is defined as a macro as otherwise you’d have to write this code every time you’d like to create such lambda and pass it into an algorithm.. In this case, macros are the easiest syntax we can use [8](#8).

Play with the final code @Wandbox

# Recursive Lambdas

If you have a regular function then it’s easy to call it recursively. A common example is the calculation of a factorial:

Recursion with a Regular Function. Live code [@Wandbox](@Wandbox)

```
int factorial(int n) {
    return n > 1 ? factorial(n - 1) : 1;
}
```

```
int main() {
    return factorial(5);
}
```

However it’s not directly possible with lambdas:

Errors with Recursive Lambda. Live code [@Wandbox](@Wandbox)

```
int main() {
    auto factorial = [](int n) {
        return n > 1 ? factorial(n - 1) : 1;
    };
    return factorial(5);
}
```

This code doesn’t compile! Here’s an error from GCC:

error: use of 'factorial' before deduction of 'auto'

This happens because we cannot access factorial inside a body of the lambda, it’s still not fully evaluated. To illustrate this issue we can "expand” the code into a simplified functor:

```
struct fact {
    int operator()(int n) const {
        return n > 1 ? factorial(n - 1) : 1;
    };
};
auto factorial = fact{};
```