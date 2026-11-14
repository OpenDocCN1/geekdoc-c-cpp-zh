# 6.5 Conversion

For several casts, the compiler just looks differently on the bits in memory: either with another interpretation of the bits or with other access rights (e.g., const versus non-const). Other casts actually create new objects.

In C++, there are four different cast operators:

+   * static_cast
+   * dynamic_cast
+   * const_cast
+   * reinterpret_cast

C as its linguistic root knows only one casting operator: ( _type_ ) _expr_. This single operator is difficult to understand because it can trigger a cascade of transformations to create an object of the target type: for instance, converting a const pointer to int into a non-const pointer to char.

In contrast, the C++ casts only change one aspect of the type at a time. Another disadvantage of C-style casts is that they are hard to find in code (see also [45, Chapter 95]), whereas the C++ casts are easy to discover: just search for _cast. C++ still allows this old-style casting but all C++ experts agree on discouraging its use.

> **C Casts**
> Do not use C-style casts.

In this section, we will show the different cast operators and discuss the pros and cons of different casts in different contexts.

# 6.5.1 Casting between Base and Derived Classes

C++ offers a static and a dynamic cast between classes of a hierarchy.

# 6.5.1.1 Casting Up

```
=> c++03/up_down_cast_example.cpp
```

Casting up, i.e., from a derived to a base class, is always possible when there are no ambiguities. It can even be performed implicitly like we did in the function spy_on:

```
void spy_on(const person& p);
spy_on(tom); // Upcast student -> person
```

spy_on accepts all sub-classes of person without the need for explicit conversion. Thus, we can pass student tom as an argument. To discuss conversions between classes in a diamond-shaped hierarchy, we introduce some single-letter class names for brevity: