The explicit conversion is supported because any string implicitly converts to a std::string_view, which has an explicit conversion to any string type. The former is cheap but the latter needs to allocate memory (provided the small string optimization does not apply).

In our example, this means:

```
std::string s{"Paul Kalkbrenner"};
PmrCustomer c1 = s;                 // ERROR: no implicit conversion
PmrCustomer c2{s};                 // ERROR: no implicit conversion
PmrCustomer c3{std::pmr::string{s}};   // OK (implicitly converts s to string_view)
```

We might want to provide additional constructors but the good thing with not providing them is that programmers are forced to implement the expensive conversion. In addition, if you overload for different string types (std::string and std::pmr::string), you get additional ambiguities (e.g., taking a string_view or a string literal), which means that even more overloads are necessary.

In any case, a getter can return only one type (because we cannot overload on different return types only). Thus, we can provide only one getter, which should usually return the “native” type of the API (here, std::pmr::string). This means that if we return a std::pmr::string and need the name as std::string, again we need an explicit conversion:

```
PmrCustomer c4{"Mr. Paul Kalkbrenner"};     // OK: allocates with default resource
std::string s1 = c4.getName();                // ERROR: no implicit conversion
std::string s2 = std::string{c4.getName()};   // OOPS: two allocations
```

This is not only less convenient, it is also a performance issue, because in the last statement, two allocations happen:

+   - First we allocate memory for the return value
+   - Then the conversion from type std::pmr::string to std::string needs another allocation

Therefore, it might be a good idea to provide an additional getter getNameAsString() that directly creates and returns the requested type:

```
std::string s3 = c4.getNameAsString();      // OK: one allocation
```

# 29.4 Afternotes

Polymorphic allocators were first proposed by Pablo Halpern in http://wg21.link/n3525. This approach was adopted as part of the Library Fundamentals TS as proposed by Pablo Halpern in http://wg21.link/n3916. The approach was adopted with other components for C++17 as proposed by Beman Dawes and Alisdair Meredith in http://wg21.link/p0220r1.