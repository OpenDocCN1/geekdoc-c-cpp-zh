```
// ...
}
template <typename T>
void rvalue_only(T&&) = delete;
```

When we call this function with an rvalue only the first overload matches and the function is executed as expected. For any lvalue argument— including const lvalues—the second overload is the better match and a compiler error is issued.

Alternatively, we could refrain from overloading and add a static_assert that our parameter is indeed an rvalue reference:

Click here to view code image

```
template <typename T>
void rvalue_only2 (T&& arg)
{
    static_assert (is_rvalue_reference<decltype (arg)>::value
        ,
        "This function is only allowed for
        rvalues!");
    // ...
}
```

is_rvalue_reference is a so-called type trait that we will discuss in more detail in Section 5.2.1. This version has the advantage that we can choose the error message. Furthermore, when we have multiple rvalue parameters we can test them in subsequent static assertions whereby the first approach needs an overload for each rvalue parameter (and all combinations thereof if we don’t want confusing error messages about ambiguities).

# 3.1.3 Dealing with Errors in Templates

Back to our max example that works for all numeric types. But what happens with types that provide no operator>, for instance, std::complex<T>? Let us try to compile the following snippet:³

Click here to view code image

```
std::complex<float> z(3, 2), c(4, 8);
std::cout << "The maximum of c and z is " << ::max(c, z) <<
'\n';
```