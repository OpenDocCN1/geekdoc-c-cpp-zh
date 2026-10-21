# Chapter 6: Lambda Extensions

To find out at compile time whether a lambda is valid for a compile-time context, you can declare it as constexpr:

```
```cpp
auto squared3 = [] (auto val) constexpr {
return val*val;
};
```
```

With specified return types, the syntax looks as follows:

```
```cpp
auto squared3i = [] (int val) constexpr -> int {
return val*val;
};
```
```

The usual rules regarding constexpr for functions apply: if the lambda is used in a runtime context, the corresponding functionality is performed at run time.

However, using features in a constexpr lambda that are not valid in a compile-time context results in a compile-time error:

```
```cpp
auto squared4 = [] (auto val) constexpr {
static int calls=0;
... // ERROR: static variable in compile-time context
return val*val;
};
```
```

For an implicit or explicit constexpr lambda, the function call operator is constexpr. That is, the definition of

```
```cpp
auto squared = [] (auto val) {
return val*val;
};
```
```

converts into the closure type:

```
```cpp
class CompilerSpecificName {
public:
...
template<typename T>
constexpr auto operator() (T val) const {
return val*val;
}
};
```
```

Note that the function call operator of the generated closure type is automatically constexpr. In general, since C++17, the generated function call operator is constexpr if either the lambda is explicitly defined to be constexpr or the lambda is implicitly constexpr (as is the case here).

Note that there is a difference between

```
```cpp
auto squared1 = [] (auto val) constexpr {
return val*val;
};
```
```

> ¹ Features not allowed in compile-time context are, for example, static variables, virtual functions, try and catch, and new and delete.