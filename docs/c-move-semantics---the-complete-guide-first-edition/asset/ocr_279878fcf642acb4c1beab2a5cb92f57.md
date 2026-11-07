That means:

```
    MyType v;
    const MyType c;
```

```
    f(v);    // T is deduced as MyType& and arg has this type
    f(c);    // T is deduced as const MyType& and arg has this type
```

Now consider how std::forward<> is defined in contrast to std::move():

+   - `std::move()` always converts any type to an rvalue reference:
+   
+         static_cast<remove_reference_t<T>&&>(t)
+   
+     It removes any references and converts to the corresponding rvalue reference type (removes any & and adds &&).

+   - `std::forward<>` only adds rvalue referenceness to the passed type parameter:
+   
+         static_cast<T&&>(t)

Here, the reference collapsing rules apply again:

+   - If type T is an lvalue reference, T&& is still an lvalue reference (&& has no effect). Therefore, we cast arg to an lvalue reference, which means that arg has no move semantics.
+   - However, if T is an rvalue reference (or not a reference at all), T&& is (still) an rvalue reference. Therefore, we cast arg to an rvalue reference and that way we change the value category to an xvalue, which is the effect of std::move().

In total, therefore, we get:

```
    template<typename T>
    void f(T&& arg)              // arg is a universal/forwarding reference
    {
        g(std::forward<T>(arg));  // perfectly forward (move() only for passed rvalues)
    }
```

```
    MyType v;
    const MyType c;

    f(v);             // T and arg are MyType&, forward() has no effect in this case
    f(c);             // T and arg are const MyType&, forward() has no effect in this case
    f(MyType{});      // T is MyType, arg is MyType&&, forward() is equivalent to move()
    f(std::move(v));  // T is MyType, arg is MyType&&, forward() is equivalent to move()
```

Note that string literals are lvalues so that we deduce T and arg for them as follows:

```
    f("hi");              // lvalue passed, so T and arg have type const char (&)[3]
    f(std::move("hi"));   // rvalue passed, so T is deduced as const char [3]
                           //              and arg has type const char (&&)[3]
```