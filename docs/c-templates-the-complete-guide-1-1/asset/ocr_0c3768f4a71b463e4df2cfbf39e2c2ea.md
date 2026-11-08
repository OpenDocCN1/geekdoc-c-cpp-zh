template. They may even refer to previous template parameters.

For example, if you want to combine the approaches to define the return type with the ability to have multiple parameter types (as discussed in the section before), you can introduce a template parameter `T` for the return type with the common type of the two arguments as default. Again, we have multiple options:

+   1. We can use `operator<` directly. However, because we have to apply `operator<` before the call parameters `a` and `b` are declared, we can only use their types:

**Click here to view code image**

boost/??/maxdefault2.cpp

```
```cpp
#include <type_traits>

template<typename T1, typename T2,
         typename RT = std::common_type_t<T1, T2>>
RT max (T1 t1, T2 t2)
{
    return t1 < t2 ? t2 : t1;
}
```
```

Note again the usage of `std::decay_t<>` to ensure that no reference can be returned.

Note also that this implementation requires that we are able to call function operators for the passed types. There is another solution, using `std::declval<>`, which, however, makes the declaration even more complicated:

**Click here to view code image**

boost/??/maxdefault2.cpp

```
```cpp
#include <type_traits>

template<typename T1, typename T2,
         typename RT = std::common_type_t<T1,T2>>
RT max (T1 t1, T2 t2)
{
    return t1 < t2 ? t2 : t1;
}
```
```

Again, note that `std::common_type_t<>` decays so that the return value can't become a reference.

In all cases, as a caller, you can now omit the default value for the return type:

**Click here to view code image**

`auto a = max(1, 7.2);`

or specify the return type after all other argument types explicitly:

**Click here to view code image**

`auto b = max<double>(2, 4);`

However, again we have the problem that we have to specify three types to be able to specify the return type only. Instead, we would need the ability to have the return type as the first template parameter, while still being able to define it from the argument types. In principle, it is possible to default arguments for finding function template parameters even if parameters without default arguments follow:

**Click here to view code image**

```
```cpp
template<typename RT = long, typename T1, typename T2>
RT max (T1 t1, T2 t2)
{
    return t1 < t2 ? t2 : t1;
}
```
```

With this definition, for example, you can call:

**Click here to view code image**