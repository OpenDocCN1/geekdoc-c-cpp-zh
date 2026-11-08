Note that all these cases may cause trouble if used improperly. For example:

Click here to view code image

```
```cpp
std::string s = "hello";
auto a = [](std::string& s) -> decltype(auto) {
    return s[0];
};
// call a
std::cout << a(s) << '\n'; // prints "h"
```
```

Here, we introduced a reference to an element of a string, but by the time we use the reference, the underlying string no longer exists. In other words, we created a dangling reference, and we have undefined behavior. This cannot happen with a plain auto, because the lambda internally is likely to return by value, but things can easily become less obvious. For example:

Click here to view code image

```
```cpp
auto a = [](std::string& s) {
    return s[0];
};
// call a
std::cout << a(s) << '\n'; // prints "h"
```
```

We should therefore ensure that the lambda returns return by value. However, as discussed in this chapter, using a template parameter T is guaranteed that it is not a reference, because return might sometimes implicitly be declared as a reference.

Click here to view code image

```
```cpp
template<typename T>
T add(T x, T y) // T is a template parameter
{
    return x + y; // 0002: return by value when called for int
}
```
```

Even when a template parameter is declared from a call-by-value call, it might become a reference type when explicitly specifying the template parameter to be a reference:

Click here to view code image

```
```cpp
template<typename T>
T add(T x, T y) // T might become a reference
{
    return x + y; // 0002: returns a reference if T is a reference
}
```
```

Let us:

```
```cpp
int x = 42;
std::string s = "hello"; // call??
```
```

To be safe, we have two options:

+   - Use the type trait std::decay<> (see Section D.4 on page 408) to ensure the return type is not a reference:

Click here to view code image

```
```cpp
template<typename T>
typename std::decay<T>::type add(T x, T y)
{
    return x + y; // always returns by value
}
```
```

Other traits, such as std::decay<> (see Section D.4 on page 408), may also be useful but become too lengthy to use. To avoid that, we can specify the return type in a different way:

Click here to view code image

```
```cpp
template<typename T>
auto add(T x, T y) -> typename std::decay<T>::type
{
    return x + y; // always returns by value
}
```
```

Let the compiler deduce the return type but by declaring the return type to be `auto` (C++14; see Section 1.3.2 on page 11), because auto always decays:

Click here to view code image

```
```cpp
template<typename T>
auto add(T x, T y) // by-value return type deduced by compiler
{
    return x + y; // always returns by value
}
```
```

# 7.6 RECOMMENDED TEMPLATE PARAMETER DECLARATIONS

As explained in the previous section, we have very different ways to declare parameters that depend on template parameters:

+   - **Declare the parameter by value:** This approach is simple, but it does not preserve the best performance for large objects. Still the caller can decide to pass by reference using std::cref() and std::ref(), but the callee must be careful about doing so.
+   - **Declare the parameter by reference:** This approach often provides better performance for somewhat large objects, especially when passing
+     - existing objects (lvalues) to lvalue references,
+     - temporary objects (prvalues) or objects marked as movable (xvalues) to rvalue references,
+     - or both to forwarding references.

Because in all these cases the argument doesn't decay, you may need special care when passing string literals and other raw arrays. For forwarding