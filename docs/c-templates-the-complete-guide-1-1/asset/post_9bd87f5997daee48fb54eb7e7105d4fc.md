
```cpp
throw NotEqualityComparable();
}

});
```

Finally, by using `TypeEqualityWithin` in our implementation of `SpecificFunctionProvider`, we are able to provide support for `==` within `Function<>` where the stored function object and the function object support ...

[Click here to view code image](#)

```cpp
virtual bool equals(FunctionType& f, Arg... const& fb)
const override {
  if (auto spec = dynamic_cast<SpecificFunction<Foo...>&>(
      ...)) {
    return TypeEqualityFunction::equals(function,
      specificFunction);
  }
}

// Functions with different types are never equal:
return false;
```

### 22.6 PERFORMANCE CONSIDERATIONS

Type erasure provides some of the advantages of both static polymorphism and dynamic polymorphism, but not all. In particular, the performance of generated code using type erasure tends to be less than that of dynamic polymorphism, because both rely on dynamic dispatch via virtual functions. Thus, some of the traditional advantages of static polymorphism—speed, such as the ability of the compiler to inline calls, may be lost. Whether this loss of performance will be perceptible is application-dependent, but it’s often easy to tell by considering how much work is performed in the function being called relative to the cost of a virtual function call: If the two are close (e.g., using `Function<>` to simply add two integers), type erasure is likely to execute far more slowly than a static-polymorphic version. If, on the other hand, the function call performs a significant amount of work—querying a database, sorting a large input, or updating a user interface—the overhead of type erasure is unlikely to be measurable.

### 22.7 AFTERNOTES

Kevlin Henney popularized type erasure in C++ with the introduction of the `Any` type (`Boost.Any`/`boost::any`), which later became a popular Boost library (`Boost.Any`) and part of the C++ standard library with C++17. The technique was refined somewhat in the Boost.Function library, which applied virtual functions and type-erasure operations and eventually became `std::function`. However, each of the early libraries addressed only a single set of operations: `any` was a simple value type with only copy and a set of operations limited to invocation.

Later efforts, such as the Boost.TypeErasure library (`Boost.TypeErasure`) and Adobe’s Poly library (`AdobePoly`), apply template metaprogramming techniques to allow users to form a type-safe value with some specified list of capabilities. For example, the following type constructed using the Boost.TypeErasure library handles any construction, a type-erased-like criterion, and output streaming for printing:

[Click here to view code image](#)

```cpp
using AnyIterable = any<
  boost::type_erasure::copy_constructible<>,
  typeid_<>,
  ostreamable
>;
```

- 1. Making `invoke()` const is a safety belt against invoking non-const `operator()` overloads through `const`.
- 2. Although the type could be copied with dynamic cast from one element to another, the `Function<>` class makes the `bridge` pointer private, so clients of `Function<>` have no access to the type itself.
- 3. Mechanically, the code for the call to `operator()` is instantiated because it is the virtual functions of a class template (in this case, the `SpecificFunction<>`), so typically instantiating the class template itself is instantiated.

## Chapter 23

## Metaprogramming

Metaprogramming consists of "programming a program." In other words, we lay out code that the programming system executes to generate new code that implements the functionality we really want. Usually, the term metaprogramming implies a reflexive attribute: The metaprogramming component is part of the program for which it generates a bit of code (i.e., an additional or different bit of the program).

Why would metaprogramming be desirable? As with most other programming techniques, the goal is to achieve more functionality with less effort, where effort can be measured as code size, maintenance cost, and so forth. What characterizes metaprogramming is that some user-defined computation happens at translation time. The underlying motivation is often performance (things computed at translation time can frequently be optimized away) or interface simplicity (metaprogramming is generally easier to adapt than a runtime approach).

Metaprogramming often relies on the concepts of traits and type functions as described in Chapter 19. We therefore recommend becoming familiar with that chapter prior to delving into this one.

### 23.1 The State of Modern C++ Metaprogramming

C++ metaprogramming techniques evolved over time (the Afternotes at the end of this chapter survey this evolution in detail). Let's discuss and categorize the various approaches to metaprogramming that are in common use in modern C++.

### 23.1.1 Value Metaprogramming

In the first edition of this book, we were limited to the features introduced in the original C++ standard (published in 1998, with minor corrections in 2003). In that world, composing simple compile-time ("meta-") computations was a minor challenge. We therefore devoted a good chunk of this chapter to doing just that; one fairly advanced example computed the square root of an integer value at compile time using recursive template instantiations. As introduced in Section 1.2.4 on page 22, C++11 and, especially, C++14 removed most of that challenge with the introduction of constexpr functions. For example, since C++14, a compile-time function to compute a square root is easily written as follows:

Click here to view code image

```cpp
meta/sqrtconstexpr.hpp

template<typename T>
constexpr T sqrt(T x)
{
    // handle cases where x and its square root are equal as a special case to simplify
    // the iteration criterion for larger x:
    if (x <= 1) {
        return x;
    }

    // repeatedly determine in which half of a [lo, hi] interval the square root of x is located,
    // until the interval is reduced to just one value:
    T lo = 0, hi = x;
    for (;;) {
        auto mid = (hi+lo)/2, midSquared = mid*mid;
        if (midSquared <= x && (mid+1)*(mid+1) > x) {
            return mid;
        }
        // continue with the bigger half of the interval:
        if (midSquared < x) {
            lo = mid;
        } else {
            hi = mid;
        }
    }
}
```

This algorithm searches for the answer by repeatedly halving an interval known to contain the square root of x (the roots of 0 and 1 are treated as special cases to keep the convergence criterion simple). This sqrt() function can be evaluated at compile or run time.

Click here to view code image

```cpp
static_assert(sqrt(25) == 5, "");       // evaluated at compile time
static_assert(sqrt(4) == 2, "");        // evaluated at compile time

std::array<int, sqrt(40)> arr;           // declares array of 6 elements (compile time)
```

Click here to view code image

```cpp
long long t = 53478;
std::cout << sqrt(t) << '\n';             // prints 231
```

This function's implementation may not be the most efficient at compile time (where exploiting peculiarities of the machine often pays off), but because it is meant to perform compile-time computations, absolute efficiency is less important than portability. Note that no advice about template magic is in sight in that square root example, only the usual template argument deduction for a function template. The code is "plain C++" and is not particularly challenging to write.

Value metaprogramming (i.e. programming the computation of compile-time values) as we did above is occasionally quite useful, but there are two additional kinds of metaprogramming that can be performed with modern C++ (say, C++14 and C++17): type metaprogramming and hybrid metaprogramming.

### 23.1.2 Type Metaprogramming

We already encountered a form of type computation in our discussion of traits in Chapter 19. In Chapter 5, those traits take a type and produce a new type from it. For example, our RemoveReference trait from the previous chapter will remove a reference type. However, the examples we developed in Chapter 5 consisted only of fairly elementary type operations. By relying on recursive template instantiation—a mainstay of template-based metaprogramming—we can perform type computations of a more considerable complexity.

Consider the following small example:

Click here to view code image

```cpp
src/meta/removeallextents.hpp

// primary template: in general we yield the given type

template<typename T>
struct RemoveAllExtent {
    using Type = T;
};

// partial specializations for array types (with and without size)
template<typename T, std::size_t SZ>
struct RemoveAllExtent<T[SZ]> {
    using Type = typename RemoveAllExtent<T>::Type;
};

template<typename T>
struct RemoveAllExtent<T[]> {
    using Type = typename RemoveAllExtent<T>::Type;
};

template<typename T>
using RemoveAllExtents = typename RemoveAllExtent<T>::Type;
```
