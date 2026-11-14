doesn't make it obvious what this exactly means in a programmer's daily life. Furthermore, no compiler supported this feature² at the time of writing so we can only try it in the future.

+   2. More specifically, trying to compile c++20/contexpr_vector_string.cpp failed with clang++-13, gccc++-11, and VS19.

The language standard tried to define conditions under which a type is usable in a constexpr function. It turned out that this is not definable as a type property because it depends on how the type is used—more precisely which constructor is called in the considered constexpr function. Accordingly, the respective type trait is_literal_type was doomed to be useless and declared deprecated since C++14.³

+   3. Nonetheless, attention was paid that the useless result is well defined.

A really nice feature of constexpr functions is their usability at compile time and run time:

Click here to view code image

```
long n = atoi(argv[1]);
cout << "fibonacci(" << n << ") = " << fibonacci(n) << '\n';
```

Here we passed the first argument from the command line (which is definitely not known during compilation). Thus, whenever one or more arguments are only known at run time, the function cannot be evaluated at compile time. Only when all function arguments are available at compile time can the function be computed during compilation.

The hybrid applicability of constexpr functions implies in turn that their parameters can only be passed to constexpr functions. Passing a parameter to a regular function would impede the usage at compile time. Conversely, we cannot pass a function parameter to a compile-time evaluation like static_assert as it prevents run-time calls. As a consequence, we cannot express assertions within constexpr functions in C++11.

The language standard regulates which functions from the standard library must be realized as constexpr. Some library implementations realize additional functions as constexpr. For instance, the following function:

Click here to view code image