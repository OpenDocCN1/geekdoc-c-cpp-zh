```
boxes/len1.cpp
```

```
```cpp
// number of elements to a raw array:

template<typename T, unsigned N>
size_t len (T (&)[N])
{
    return N;
}
```
```

Here, we define two function templates len() taking one generic argument and then:

+   1. The first function template declares the parameter as `T (&)[N]`, which means that the parameter has to be an array of N elements of type T.
+   
+   2. The second function template declares the parameter simply as `T`, which places no constraints on the parameter but returns type `T::size_type`, which requires that the passed argument type has a corresponding member `size_type`.

When passing a raw array of string literals, only the first function template `len()` matches:

Click here to view code image

```
```cpp
int a[10];
std::cout << len(a);        // OK: only len() for array matches
std::cout << len("type");   // OK: only len() for array matches
```
```

According to its signature, the second function template also matches when substituting (respectively) `int[]` and `char const (&)[?]`, but those substitutions lead to invalid errors in the return type `T::size_type`. The second template is therefore ignored for these calls.

When passing an `std::vector<>`, only the second function template matches:

Click here to view code image

```
```cpp
std::vector<int> v;
std::cout << len(v);   // OK: only len() for a type with
                      // size_type matches
```
```

When passing a raw pointer, neither of the template match (without a fixed?). As a result, the compiler will complain that no matching `len()` function is found.

Click here to view code image

```
```cpp
int* p;
std::cout << len(p);   // ERROR: no matching len() function found
```
```

Note that this differs from passing an object of a type having a `size_type` member, but no `size()` member function, as, for example, the case for `std::allocator<T>`:

Click here to view code image

```
```cpp
std::allocator<T> x;
std::cout << len(x);   // ERROR: len() function found,
                      // but can't call size()
```
```