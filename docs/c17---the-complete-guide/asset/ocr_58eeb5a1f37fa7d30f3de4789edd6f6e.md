# 33.2 std::bool_constant<>


Also note that calling a function template requires explicit instantiation. If print() were a template:

```
```cpp
template<typename T>
void print(const T &coll)
{
    std::cout << "elems: ";
    for (const auto& elem : coll) {
        std::cout << elem << ' ';
    }
    std::cout << '\n';
}
```
```

then you would have to pass a call to it with explicitly specified template parameters:

> // ERROR: can't deduce template parameter T
> call(print, vals);

```
call(print<std::vector<int>>, vals); // OK
```

Finally, note that according to the rules of move semantics, returning the result of an invocation requires decltype(auto) to perfectly return the return value to the caller:

```
```cpp
template<typename Callable, typename... Args>
decttype(auto) call(Callable&& op, Args&&... args)
{
    return std::invoke(std::forward<Callable>(op),   // call passed callable with
        std::forward<Args>(args)...); // all additional passed args
}
```
```

# 33.2 std::bool_constant<>


If traits yield Boolean values, they now use the alias template bool_constant<>:

```
```cpp
namespace std {
    template<bool B>
    using bool_constant = integral_constant<bool, B>; // since C++17
    using true_type = bool_constant<true>;
    using false_type = bool_constant<false>;
}
```
```

Before C++17, you had to use integral_constant<> directly, which meant that true_type and false_type were defined as follows:

```
```cpp
namespace std {
    using true_type = integral_constant<bool, true>;
    using false_type = integral_constant<bool, false>;
}
```
```

Still, Boolean traits should usually inherit from std::true_type if a specific property applies and from std::false_type if this is not the case. For example: