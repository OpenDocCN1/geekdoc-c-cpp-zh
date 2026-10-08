
We can fix the synchronisation problem by having a mutex and locking it before each call of push_back. But is that code still efficient? If the filter condition is straightforward and fast to execute, then you might even get slower performance than the serial version (seq).

Not to mention that by running it in parallel, you don’t know the order of the copied elements in the output vector.

This section shows only a basic overview of the parallel algorithms, and if you like to see more, please have a look at the following article: Bartek’s coding blog: The Amazing Performance of C++17 Parallel Algorithms, is it Possible?

## Lambdas And Async - Wrap Upon

To wrap up: Lambda expressions are convenient when you want to start a thread, invoke asynchronous code through std::async or use with parallel algorithms. However, it’s essential to keep in mind that closure objects aren’t unique regarding the concurrency and all challenges apply here as well.

## Summary

In this chapter, you’ve seen that C++17 joined two essential elements of C++: constexpr with lambdas. This is a necessary step towards improved metaprogramming support in the language. We’ll see that more in the next chapter about C++20. What’s more, the C++17 Standard also addressed the capturing this problem. In the new standard, you can capture this by value so that the code can be much safer.

We also had a look at some use cases for lambdas: IIFE technique, fold expressions and variadic generic lambdas, deriving from lambda expressions and asynchronous code execution. Thanks to the various features enabled in C++17, we now have much nicer syntax and more straightforward ways to write efficient code.

## 5. Lambdas in C++20

During the meeting in Prague, in February 2020, the ISO Committee finally approved the C++20 Standard and pushed it to the official publication (probably at the end of 2020). The new specification brings a lot of substantial improvements to the language and the Standard Library! Lambda expressions also got a few upgrades.

In this chapter, you'll see:

- What changes in C++20.
- New options to capture this pointer.
- Template lambdas.
- How to improve generic lambdas with concepts.
- How to use lambdas with constexpr algorithms.
- How to make the overloaded pattern even shorter.

You can see the specification related to lambdas in N4861 (the current C++20 draft, post Prague version) and the lambda section: [expr.prim.lambda].

## Lambda Syntax Update

With C++20, we have more changes regarding the syntax of lambda expressions:

- You can now add consteval after the parameter list.
- There's an option to specify the template tail.
- And after the trailing return you can put requires declaration.

```
<params> () specifiers exception attr - -> requires { /code; /* */
  ^       ^       ^
  |       | |
  |       optional: trailing return type
  |  optional: mutable, constexpr, consteval, noexcept, attributes
  | parameter list (optional when no specifiers added)
  |
optional: template parameter list
|
lambda introducer with an optional capture list
```

You can read about new modifications in the next sections.

## A Quick Overview of the Changes

With C++20 we'll get the following features related to lambda expressions:

- Allow [=, this] as a lambda capture - P049R2 and deprecate implicit capture of this via []] - P0806.
- Pack expansion in lambda init-capture: ...args = std::move(args) {} - P0780.
- static, thread_local, and lambda capture for structured bindings - P1091.
- template lambdas (with concepts) - P0428R2.
- Simplifying implicit lambda capture - P0588R1.
- Default constructible and assignable static lambdas - P0624R2.
- Lambdas in unevaluated contexts - P0315R4.
- constexpr Algorithms - most importantly P2022, P0879 and P1645.

If you'd like to know more about C++20, you can have a look at the paper that summarises all the changes: Changes between C++17 and C++20 DIS - P2131.

You can also see my Reference Card with all language and the library features: Bartek’s coding blog: C++20 Reference Card.

Let's now have a quick look at some of the changes.

In most of the cases the newly added features "clean-up" lambda syntax. Plus, C++20 adds enhancements that allow us to use lambdas in advanced scenarios.

For example, with P1091 you can capture a structured binding:

> Some compilers supported structured binding even in C++17 (for GCC), but it was not mandated by the Standard back.

C++20 also brings clarifications related to *this capture. You'll get a warning if you capture [-=] in a method:

About implicit *this capture. Live code @Wandbox

```
struct Baz {
    auto foo() {
        return [=]() { cout << s << '\n'; };
    }
    std::string s;
};
```

Compiling with GCC 9 yields the following warning:

warning: implicit capture of 'this' ['=] is deprecated in C++20

The warning appears, because even with [=] you'll capture this as a pointer. It's better to write what you want explicitly: [=, this], or [=, *this].

After a quick review, let's have a look at more prominent features in C++20 related to lambdas.

## consteval Lambdas

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

Above, you can see that we applied consteval after the argument list. This is very similar to constexpr. The critical difference is that if you remove const from x, the lambda can work (at runtime), while the immediate lambda won't.

By default, if a lambda follows the rules of a constexpr function, the compiler marks the call as implicitly. This is not the case with consteval. You can find the full specification for the new feature in this proposal: P1073R3.

## Capturing a Parameter Pack

One improvement we got in C++20 is pack expansion in lambda capture:

```
template < typename...Args> void call(Args&&... args) {
    auto ret = [...capturedArgs] = std::move(args)]();
}
```

Previously before C++20, the code wouldn't compile (see the C11 section on that) and to work around this issue, you had to wrap arguments into a separate tuple. You can read about in P0780.

To sum, capturing a variadic pack, we can take the example that we got from the C11 chapter and experiment with it, adding the latest feature. For instance, we can leverage fold expression to do a print of each captured object:

Capturing a Variadic Pack. Live code @Wandbox

```
#include <iostream>
#include <memory>

template < class First, class... Args>
void captureTest(First& first, Args&... args) {
    const auto printer = [first = std::move(first),
        ...capturedArgs = std::move(args)]() {
        ((std::cout << ", ") << capturedArgs, ...));
        std::cout << '\n';
    };
    printer();
}

int main() {
    auto ptr = std::make_unique<int>(10);
    captureTest(std::move(ptr), 2, 3, 4);
    captureTest(std::move(ptr), 'a', 'b');
}
```

The output:

0xf06cb20, 2, 3, 4
a, b

In the example, we used a printer object which is similar to the code that we wrote in the C11 chapter, but this time we capture variables rather than forward them as lambda arguments.

## Template Lambdas

With C++14, we got generic lambdas which means that parameters declared
