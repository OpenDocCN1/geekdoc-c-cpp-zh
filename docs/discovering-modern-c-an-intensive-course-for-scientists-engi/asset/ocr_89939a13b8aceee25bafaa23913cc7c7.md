implementation that only switches the pointers. This can be achieved with a small change in a generic manner:

```
```cpp
template <typename T, typename U>
inline void some_function(T& x, T& y, const U& z, int i)
{
    using std::swap;
    ...
    swap(x, y); // involves ADL
    ...
}
```
```

With this implementation, both swap overloads are candidates but the one in our class is prioritized by overload resolution as its argument type is more specific than that of the standard implementation. More generally, any implementation for a user type is more specific than std::swap. In fact, std::swap is already overloaded for standard containers for the same reason. This is a general pattern:

# Use using

Do not qualify namespaces of function templates for which user-type overloads might exist. Make the name visible instead and call the function unqualified.

As an addendum to the default swap implementation: Since C++11, the default is to move the values between the two arguments and the temporary: C++11

```
```cpp
template <typename T>
inline void swap(T& x, T& y)
{
    T tmp(move(x));
    x = move(y);
    y = move(tmp);
}
```
```

As a result, types without user-defined swap can be swapped efficiently when they provide a fast move constructor and assignment. Only types without user implementation and move support are finally copied.

# 3.3 Class Templates

In the previous section, we described the use of templates to create generic functions. Templates can also be used to create generic classes. Analogous to generic functions, class template is the correct term to the standard whereas template class (or templated class) is more frequently used in daily life. In these classes, the types of data members can be parameterized.

This is in particular useful for general-purpose container classes like vectors, matrices, and lists. We could also extend the complex class with a parametric value type. However, we have already spent so much time with this class that it seems more entertaining to look at something else.