Click here to view code image

```
template <typename T, typename U>
inline void some_function(T& x, T& y, const U& z, int i)
{
    using std::swap;
    ...
    swap(x, y); // involves ADL
    ...
}
```

With this implementation, both swap overloads are candidates but the one in our class is prioritized by overload resolution as its argument type is more specific than that of the standard implementation. More generally, any implementation for a user type is more specific than std::swap. In fact, std::swap is already overloaded for standard containers for the same reason. This is a general pattern:

# Use using

Do not qualify namespaces of function templates for which user-type overloads might exist. Make the name visible instead and call the function unqualified.

> C++11 As an addendum to the default swap implementation: Since C++11, the default is to move the values between the two arguments and the temporary if possible:

```
template <typename T>
inline void swap(T& x, T& y)
{
    T tmp(move(x));
    x= move(y);
    y= move(tmp);
}
```

As a result, types without user-defined swap can be swapped efficiently when they provide a fast move constructor and assignment. Only types without user implementation and move support are finally copied.