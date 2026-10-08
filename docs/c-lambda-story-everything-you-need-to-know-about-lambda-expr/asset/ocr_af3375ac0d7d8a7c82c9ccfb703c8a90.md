After a quick review, let's have a look at more prominent features in C++20 related to lambdas.

# constevalval Lambdas

While constexpr from C++11 allows function execution at the compilation phase, it's also possible to run those functions at runtime. It appears that in some cases, it might be best to limit the functionality only to compile-time. That's why in C++20, we have a new keyword that creates functions which conform to the rules of a constexpr function but can only be evaluated at compile-time. Such functions are also called "immediate functions".

This new keyword can also be applied to lambdas. Let's review a simple example:

A Simple Immediate Lambda. Live code @Wandbox

```
int main() {
    const int x = 10;
    auto lam = [int x] consteval { return x + x; };
    return lam(x);
}
```

Above, you can see that we applied consteval after the argument list of the lambda. This is very similar to the application of constexpr. The critical difference is that if you remove const from x_n, then the constexpr lambda can work (at runtime), while the immediate lambda won't compile.

By default, if a lambda follows the rules of a constexpr function, the compiler marks the call as const implicitly. This is not the case with consteval as it forms a stronger restriction on such code. And you cannot use both of these keywords at the same time. You can find the full specification for the new feature in this proposal: P1073R3.

# Capturing a Parameter Pack

One improvement we got in C++20 is pack expansion in lambda capture-

```
template < typename...Args> void call(Args&& ... args) {
    auto ret = [...capturedArgs] = std::move(args)]();
}
```