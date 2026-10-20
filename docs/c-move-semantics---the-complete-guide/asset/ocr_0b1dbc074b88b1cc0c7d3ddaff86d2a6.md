```
std::chrono::duration<double, std::milli> d{t1 - t0};
std::cout << d.count() << "ms\n";
}
```

We provide a class that wraps a string of significant length (to avoid the small string optimization). Note that we have to initialize the value with parentheses because braces would interpret the 100 as the initial character with the value 100.

In the class we mark the move constructor with NOEXCEPT, which the preprocessor can replace with nothing or noexcept (e.g., compile with -DNOEXCEPT=noexcept). We then measure how long it takes to reallocate 1 million of these objects in a vector.

On almost all platforms, declaring the move constructor with noexcept makes the reallocation faster by a factor of up to 10 (make sure a significant level of optimization is activated). That is, a reallocation (typically forced by inserting a new element) might take about 20 instead of 200 milliseconds. This means 180 milliseconds less in which we cannot use the vector for anything. This can be a huge benefit.²

# 7.2 Details of noexcept Declarations

As seen, noexcept was introduced to allow specification of conditional guarantees not to throw. In general, knowing at compile time that a function cannot throw can improve code and optimizations because you do not have to deal with possible clean-ups due to exceptions raised. Note that if the noexcept guarantee is violated, the program calls std::terminate(), which usually calls std::abort() to cause an “abnormal program termination” (e.g., a core dump).

# 7.2.1 Rules for Declaring Functions with noexcept

A couple of rules apply when declaring noexcept conditions:

+   - The noexcept condition must be a compile-time expression that yields a value convertible to bool.
+   - You cannot overload functions that have only different noexcept conditions.
+   - In class hierarchies, a noexcept condition is part of the specified interface. Overwriting a base class function that is noexcept in a derived class with a function that is not noexcept is an error (but not the other way around).

For example:

```
class Base {
public:
...
virtual void foo(int) noexcept;
virtual void foo(int);    // ERROR: overload on different noexcept clause only
virtual void bar(int);

```

² Note that there is a bug in Visual C++ 2015 that means that move is always used on reallocation and we do not see a difference. This bug is fixed with Visual C++ 2017 (which might slow down the reallocation if a move constructor does not guarantee not to throw).