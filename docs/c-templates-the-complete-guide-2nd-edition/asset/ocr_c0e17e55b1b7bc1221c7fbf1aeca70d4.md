This can be used to define a function that calls `print()` for the elements of a `std::array` or `std::tuple` using the compile-time access with `get<>()` for the given indices: Click here to view code image

```
template<typename T, std::size_t... Idx>
void printByIdx(T t, Indices<Idx...>)
{
  print(std::get<Idx>(t)...);
}
```

This template can be used as follows: Click here to view code image

```
std::array<std::string, 5> arr = {"Hello", "my", "new", "!", "World"}; printByIdx(arr, Indices<0, 4, 3>()); or as follows:
```

Click here to view code image

```
auto t = std::make_tuple(12, "monkeys", 2.0);
printByIdx(t, Indices<0, 1, 2>());
```

This is a first step towards meta-programming, which will be discussed in Section 8.1 on page 123 and Chapter 23.

# 4.4.4 Variadic Deduction Guides

Even deduction guides (see Section 2.9 on page 42) can be variadic. For example, the C++ standard library defines the following deduction guide for `std::arrays`: Click here to view code image

```
namespace std {
template<typename T, typename... U> array(T, U...)
-> array<enable_if_t<(is_same_v<T, U> && ...), T>, (1 + sizeof...(U))>;
}
```

An initialization such as `std::array a{42,45,77};` deduces T in the guide to the type of the element, and the various U... types to the types of the subsequent elements. The total number of elements is therefore 1 + sizeof...(U): Click here to view code image

```
std::array<int, 3> a{42,45,77}; The std::enable_if<> expression for the first array parameter is a fold expression that (as introduced as isHomogeneous() in Section 4.4.1 on page 62) expands to: Click here to view code image
```

```
is_same_v<T, U1> && is_same_v<T, U2> && is_same_v<T, U3> …
```