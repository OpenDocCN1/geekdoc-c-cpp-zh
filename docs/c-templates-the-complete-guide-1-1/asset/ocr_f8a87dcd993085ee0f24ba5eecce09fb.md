![](bbox=[0.04, 0.0, 0.96, 0.012])

```
```cpp
template<typename T> struct X { T const m; };
struct Y {
    using T = int;
    Y() : m(7) { }
    Y(int) : m(0) { }
    auto get() const { return m; } // OK? see text
    T m;
};
```
```

There are no exceptional reasons why C++ could not support all the uses in this example, but the C++ committee felt that the benefits were outweighed by the additional implementation cost and the potential for abuse.

In order to avoid confusing both programmers and compilers, the old use of auto as a "storage class specifier" is no longer permitted in C++11 (and later standards).

![](bbox=[0.04, 0.162, 0.96, 0.174])

```
```cpp
auto i = 42; // i has type int
auto i = 42; // error: i has type int
auto i = 42; // i has type int
```
```

This old use of auto (inherited from C) is always redundant. Most compilers can usually diagnose that use from the use as a placeholder (even though they don't have to), offering a transition path from older C++ code to newer C++ code. The old use of auto is simply no longer in the language, however.

# ## DEDUCED RETURN TYPES

C++11 added another situation where a decltype placeholder type can appear: function return types. For example:

![](bbox=[0.04, 0.352, 0.96, 0.364])

```
```cpp
auto f(int x) -> decltype(x) { return x; }
```
```

defines a function with return type int (the type of x). This can be expressed by using a trailing return type syntax also:

![](bbox=[0.04, 0.432, 0.96, 0.444])

```
```cpp
auto f(int x) -> int { return x; }
```
```

The next mechanism exists to handle no return type: if no return type is specified explicitly, the lambda's return type is deduced as if it were `auto`.

![](bbox=[0.04, 0.517, 0.96, 0.529])

```
```cpp
auto l = [] (int i) { return i; }; // OK
```
```

Functions can be declared separately from their definition. This is true with functions whose return type is deduced also:

![](bbox=[0.04, 0.617, 0.96, 0.629])

```
```cpp
auto f(); // forward declaration
auto f() { return 42; }
```
```

However, the forward declaration is of very limited use in a case like this. The function can only be called after it has been defined. Perhaps surprisingly, it is not even possible to forward declare a function with a 'deduced' return type. For example:

![](bbox=[0.04, 0.727, 0.96, 0.739])

```
```cpp
auto known();
auto known() { return 42; } // ERROR: incompatible return type
```
```

Mostly, the ability to forward declare a function with a deduced return type is only useful to make a more function definition available without the full definition because of syntax preferences.

![](bbox=[0.04, 0.822, 0.96, 0.834])

```
```cpp
struct S {
    auto f(); // the definition will follow the class definition
};
auto S::f() { return 42; }
```
```

# ## DEDUCIBLE NONTYPE PARAMETERS

Prior to C++17, a nontype template argument had to be declared with a specific type. However, that type could be a template parameter type. For example:

![](bbox=[0.04, 0.932, 0.96, 0.944])

```
```cpp
template<typename T, T v> struct X {
    static constexpr T value = v;
};
```
```

In this example, having to specify the type of the nontype template argument—that is, specifying T in addition to v—can be tedious. C++17 therefore adds the ability to deduce nontype template parameters whose actual types are deduced from the corresponding template arguments.