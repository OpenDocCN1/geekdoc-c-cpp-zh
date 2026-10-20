```
auto&& r3{retByValue()};      // std::string&&
auto&& r4{retByRef()};         // std::string&
auto&& r5{retByRefRef()};      // std::string&&
auto&& r6{retByConstRef()};    // const std::string&
auto&& r7{retByConstRefRef()}; // const std::string&&
```

Whenever we use an rvalue (prvalue or xvalue) to initialize a reference declared with auto&&, we declare an rvalue reference. For example, this is the case when we bind the reference to an object marked with std::move() or to a returned plain value or rvalue reference.

However, when we use an lvalue to initialize a reference declared with auto&&, we declare an lvalue reference. For example, this is the case when we bind the reference to an object that has a name or to the return value of a function returning an lvalue reference.

Because string literals are lvalues (with a character array as type) we also get an lvalue reference when we bind the universal reference to a string literal:

```
auto&& r8{"hello"};           // const char(&)[6]
```

Because references to functions are always lvalues we also get an lvalue reference when we bind the universal reference to a function:

```
std::string foo(int);          // forward declaration
```

```
auto&& r9{foo};                // lvalue of type std::string(&)(int)
```

# 11.2.2 Perfectly Forwarding an auto&& Reference

The same way we can perfectly forward the value passed to a universal reference as a function template parameter:

```
template<typename T>
void callFoo(T&& ref) {
    foo(std::forward<T>(ref));    // becomes foo(std::move(ref)) for passed rvalues
}
```

we can perfectly forward the universal reference declared with auto&&:

```
auto&& ref{...};

foo(std::forward<decltype(ref)>(ref));  // becomes foo(std::move(ref)) for rvalues
```

Remember that the expression std::forward<decltype(ref)>(ref) is essentially implemented as follows:

+   - If the passed type decltype(ref) is an lvalue reference, which it is if ref was initialized with a returned lvalue reference, the expression casts ref to an lvalue reference, which means that ref is passed without move semantics.
+   - If the passed type decltype(ref) is an rvalue reference, which it is if ref was initialized with a returned plain value or rvalue reference, the expression casts ref to an rvalue reference, which is the effect of std::move(ref).