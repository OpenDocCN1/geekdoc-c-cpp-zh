# Move Semantics

Move semantics is supported following the rules just introduced. In the following declarations:

```
MyStruct ms = { 42, "Jim" };
auto&& [v,n] = std::move(ms);            // entity is rvalue reference to ms
```

the structured bindings v and n refer to an anonymous entity being an rvalue reference to ms, while ms still holds its value:

```
std::cout << "ms.s: " << ms.s << '\n';  // prints "Jim"
```

However, you can move assign n, which refers to ms.s:

```
std::string s = std::move(n);           // moves ms.s to s
std::cout << "ms.s: " << ms.s << '\n';   // prints unspecified value
std::cout << "n:    " << n << '\n';      // prints unspecified value
std::cout << "s:    " << s << '\n';      // prints "Jim"
```

As usual, moved-from objects are in a valid state with an unspecified value. Thus, it is fine to print the value but not to make any assumptions about what is printed.

This is slightly different to initializing the new entity with the moved values of ms:

```
MyStruct ms = { 42, "Jim" };
auto [v,n] = std::move(ms);              // new entity with moved-from values from ms
```

Here, the initialized anonymous entity is a new object initialized with the moved values from ms. Therefore, ms has already lost its value:

```
std::cout << "ms.s: " << ms.s << '\n';  // prints unspecified value
std::cout << "n:    " << n << '\n';      // prints "Jim"
```

You can still move assign the value of n or assign a new value there, but this does not affect ms.s:

```
std::string s = std::move(n);           // moves n to s
n = "Lara";
std::cout << "ms.s: " << ms.s << '\n';  // prints unspecified value
std::cout << "n:    " << n << '\n';      // prints "Lara"
std::cout << "s:    " << s << '\n';      // prints "Jim"
```

# 1.2 Where Structured Bindings Can Be Used

In principle, structured bindings can be used for structures with public data members, raw C-style arrays, and "tuple-like objects:"

+   - For **structures and classes** where all non-static data members are public, you can bind each non-static data member to exactly one name.
+   - For **raw arrays**, you can bind a name to each element of the array.
+   - For any type, you can use a **tuple-like API** to bind names to whatever the API defines as "elements." The API roughly requires the following components for a type *type*: