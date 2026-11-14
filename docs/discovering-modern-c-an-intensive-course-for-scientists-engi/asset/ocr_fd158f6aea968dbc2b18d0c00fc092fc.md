Here we defined the function divide twice: with int and double parameters. When we call divide, the compiler performs an Overload Resolution:

+   1. Is there an overload that matches the argument type(s) exactly? Take it; otherwise:

+   2. Are there overloads that match after conversion? How many?

+   • 0: Error: No matching function found.
+   • 1: Take it.
+   • > 1: Error: ambiguous call.

How does this apply to our example? The calls divide(x, y) and divide(n, n) are exact matches. For divide(x, n), no overload matches exactly and both by Implicit Conversion so that it's ambiguous.

The term "implicit conversion" requires some explanation. We have already seen that the numeric types can be converted one to another. These are implicit conversions as demonstrated in the example. When we later define our own types, we can implement a conversion from another type to it or conversely from our new type to an existing one. These conversions can be declared explicit and are then only applied when a conversion is explicitly requested but not for matching function arguments.

```
=> c++11/overload_testing.cpp
```

More formally phrased, function overloads must differ in their Signature. The signature consists in C++ of

+   • The function name;
+   • The number of arguments, called Arity; and
+   • The types of the arguments (in their respective order).

In contrast, overloads varying only in the return type or the argument names have the same signature and are considered as (forbidden) redefinitions:

```
void f(int x) {}
void f(int y) {} // Redefinition: only argument name different
long f(int x) {} // Redefinition: only return type different
```

That functions with different names or arity are distinct goes without saying. The presence of a reference symbol turns the argument type into another argument type (thus, f(int) and f(int&) can coexist). The following three overloads have different signatures:

```
void f(int x) {}
void f(int& x) {}
void f(const int& x) {}
```