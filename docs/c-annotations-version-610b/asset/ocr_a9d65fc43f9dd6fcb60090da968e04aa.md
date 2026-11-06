# 20.1. **DEFINING FUNCTION TEMPLATES**

Using `decltype` (cf. section 3.3.5) to define the return type won’t work as `lhs` and `rhs` aren’t known to the compiler by the time `decltype` is used. Thus the next attempt to get rid of the additional template type parameter fails to compile:

```
```cpp
template <typename Lhs, typename Rhs>
decltype(lhs + rhs) add(Lhs lhs, Rhs rhs)
{
    return lhs + rhs;
}
```
```

The `decltype`-based definition of a function’s return type may become fairly complex. To reduce the complexities the C++11 standard provides the *late-specified return type* syntax that does allow use of `decltype` to define a function’s return type. It is primarily used with function templates but it may also be used for ordinary (non-template) functions:

```
```cpp
template <typename Lhs, typename Rhs>
auto add(Lhs lhs, Rhs rhs) -> decltype(lhs + rhs)
{
    return lhs + rhs;
}
```
```

When this function is used in a statement like `cout << add(3, 3.4)` the resulting value will be 6.4, which is most likely the intended result, rather than 6. As an example how a late-specified return type may reduce the complexity of a function’s return type definition consider the following:

```
```cpp
template <class T, class U>
decltype((*(T*)0)+(*(U*)0)) add(T t, U u);
```
```

Using a late-specified return type we get the equivalent:

```
```cpp
template <class T, class U>
auto add(T t, U u) -> decltype(t+u);
```
```

which most people think is easier to read.

The expression specified with `decltype` does not necessarily use the parameters `lhs` and `rhs` themselves. In the next function definition `lhs.length` is used instead of `lhs` itself:

```
```cpp
template <typename Class, typename Rhs>
auto add(Class lhs, Rhs rhs) -> decltype(lhs.length() + rhs)
{
    return lhs.length() + rhs;
}
```
```

*Any* variable visible at the time `decltype` is compiled can be used in the `decltype` expression. However, it is currently not possible to handle member selection through pointers to members. The following code aims at specifying the address of a member function as `add`’s first argument and then use its return value type to determine the function template’s return type:

```
```cpp
std::string global;

template <typename MEMBER, typename RHS>
auto add(MEMBER mem, RHS rhs) -> decltype((global.*mem)() + rhs)
{
    return (global.*mem)() + rhs;
}
```
```