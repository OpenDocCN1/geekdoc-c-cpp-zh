https://wg21.link/p2502
https://en.cppreference.com/w/cpp/header/generator

# ### C++23 Multidimensional Subscript Operator

Section 6.13 introduced multidimensional arrays and showed that one way to access each element is by using separate [] for each dimension—given a two-dimensional array of ints named values, you can access each element with an expression of the form:

```
values[row][column]
```

Unfortunately, the preceding syntax does not work with custom classes, but programmers can overload the function-call operator (), which can take an arbitrary number of parameters. In a class representing two-dimensional data, you could use an expression like the following to invoke the overloaded () operator on an object called values:

```
values(row, column)
```

C++23 enables custom types to overload the [] operator for multiple dimensions by allowing an arbitrary number of comma-separated parameters, like the overloaded () operator. So the preceding expression may be implemented with the notation

```
values[row, column]
```

# ### C++23 std::mdspan

Section 7.10 introduced std::span for creating views of contiguous elements in containers such as arrays, vectors and built-in arrays. C++23 provides **std::mdspan** for creating **multidimensional views of contiguous data**. It also supports selecting subviews of that data, known as **slices**. Class mdspan implements an overloaded multidimensional [] operator for accessing elements in an mdspan's view. The following code snippet uses an mdspan (line 2) to view a one-dimensional, six-element array of ints as a 2-by-3 data and displays the elements by row:

```
1  std::array values{2, 3, 5, 7, 11, 13};
2  auto values2d{std::mdspan(values.data(), 2, 3)};
3
4  for (size_t row{0}; row != values2d.extent(0); ++row) {
5    for (size_t column{0}; column != values2d.extent(1); ++column) {
6      std::print("{:>2d} ", values2d[row, column]);
7    }
8
9    std::println("");
10 }
```

| 2 | 3 | 5 |
|---|---|---|
| 7 | 11| 13|

For more information on mdspan, see:

https://en.cppreference.com/w/cpp/container/mdspan

# ### C++23 Container Enhancements

There are several C++23 container enhancements: