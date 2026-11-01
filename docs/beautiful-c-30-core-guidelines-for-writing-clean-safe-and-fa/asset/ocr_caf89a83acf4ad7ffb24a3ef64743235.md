We are sure you are familiar with this. You may also be familiar with the keyword mutable that qualifies nonstatic member data as immune from const restrictions, par-ticularly if you have read Chapter 3.4, ES.50: “Don’t cast away const.” This is part of the const machinery insofar as it applies to const-qualified member functions.

New to C++11 was the keyword constexpr. The idea behind this was to improve compile-time programming by allowing a very limited set of functions to be executed at compile time. Engineers were already doing this in an unpleasant way using pre-processor macros. With the arrival of constexpr these macros could be eliminated and replaced with proper, type-safe functions. It was a nice feeling being able to elim-inate another use case from the preprocessor.

It was not without constraints, though. You were allowed only one expression per function, which led to a resurgence in recursion and a lot of ternary operator use. The standard example, as for template metaprogramming, was generating factorials and Fibonacci numbers, but a lot of math functions were available, such as trigono-metric expansions. A single expression was very limiting but sharpened everyone’s thoughts about functional programming.

Here is a factorial example:

Click here to view code image

```
```cpp
constexpr int factorial(int n) {
    return n <= 1 ? 1 // Base case
        : (n * factorial(n - 1)); //
Recurse case
}
```
```

Of course, all this recursion highlighted to everyone what the limits of the compiler were; 12! is the largest factorial to fit in a 32-bit representation.

It was fantastically popular, and C++14 broadened the scope still further. The single-expression restriction was lifted and constexpr libraries started to appear. Particularly, decent compile-time hashing became possible. The genie was well and truly out of the bottle and nothing was going to stop the expansion of constexpr throughout the language, and the relaxing of constraints.