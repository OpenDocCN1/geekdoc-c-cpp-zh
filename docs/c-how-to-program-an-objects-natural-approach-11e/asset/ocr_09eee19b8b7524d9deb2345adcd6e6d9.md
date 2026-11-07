# any_of Algorithm

The C++20 `std::ranges::any_of` algorithm (line 75) performs an *O(n)* linear search to determine whether the unary predicate function in its second argument (in this case, the lambda `isGreaterThan10`) returns true for at least one element in its `input_range` argument (values). If so, `any_of` returns true; otherwise, it returns false.

```
```cpp
// determine whether any of values' elements are greater than 10
if (std::ranges::any_of(values, isGreaterThan10)) {
    std::cout << "\n\nSome values elements are greater than 10";
}
else {
    std::cout << "\n\nNo values elements are greater than 10";
}
```
```

```
```text
Some values elements are greater than 10
```
```

# none_of Algorithm

The C++20 `std::ranges::none_of` algorithm (line 83) performs an *O(n)* linear search to determine whether the unary predicate function in its second argument (in this case, the lambda `isGreaterThan10`) returns false for all of the elements in its `input_range` argument (values). If so, `none_of` returns true; otherwise, it returns false.

```
```cpp
// determine whether none of values' elements are greater than 10
if (std::ranges::none_of(values, isGreaterThan10)) {
    std::cout << "\n\nNo values elements are greater than 10";
}
else {
    std::cout << "\n\nSome values elements are greater than 10";
}
```
```

```
```text
Some values elements are greater than 10
```
```

# find_if_not Algorithm

The C++20 `std::ranges::find_if_not` algorithm (line 91) performs an *O(n)* linear search to locate the first value in its `input_range` argument (values) for which a unary predicate function (the lambda `isGreaterThan10`) returns false. The algorithm returns an iterator that’s positioned at the first element containing a value for which the predicate function returns false; otherwise, it returns the range’s sentinel.