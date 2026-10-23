```
```cpp
// Non-reference type
std::cout << std::boolalpha << "Check value ref: "
          << std::is_reference<decltype(y)>::value << "\n";
std::cout << std::boolalpha << "Check l-value ref: "
          << std::is_lvalue_reference<decltype(y)>::value << "\n";
std::cout << std::boolalpha << "Check r-value ref: "
          << std::is_rvalue_reference<decltype(y)>::value << "\n";

// Reference type
std::cout << std::boolalpha << "Check value ref: "
          << std::is_reference<decltype(z)>::value << "\n"; // true
std::cout << std::boolalpha << "Check l-value ref: "
          << std::is_lvalue_reference<decltype(z)>::value << "\n";
std::cout << std::boolalpha << "Check r-value ref: "
          << std::is_rvalue_reference<decltype(z)>::value << "\n";
}
```
```

You can run this code and check the output.

# 4.4 LIFE BEFORE AND AFTER `decltype`

Many applications use heterogeneous data types that are combined and manipulated in various ways. In particular, we are interested in defining what the conversion rules are in mixed-mode floating-point operations and conversions. This discussion is of interest when developing libraries. It promotes the robustness of the code.

Some examples are:

+   - Matrix linear algebra operations on vectors and matrices and BLAS (*Basic Linear Algebra Subprograms*). The underlying data types can be a mixture of integers, floating-point types and complex numbers.
+   - Common types for *durations* and common type manipulation in the C++ *chrono* library.
+   - *Boost Units*, a C++ library for *dimensional analysis* that is an important technique in many branches of science and engineering (Hughes and Brighton, 1967; Wildi, 1995).

We begin with a simple example and define an operation (in this case multiplication) that accepts two generic input arguments, combines them in some way and then produces a generic return type. To this end, we consider the following alternatives:

+   - S1: Function object with one template parameter.
+   - S2: Function object with different template parameters for input arguments and return type.
+   - S3: Function object using `decltype` to *deduce* the return type.
+   - S4: Using `std::common_type<>`.

The corresponding code is easy to understand; we provide four different function objects to multiply generic types. It is recommended to read the corresponding code comments:

```
```cpp
// S1: Function object class using only one template parameter for
// operator().
```
```