Count of a2 elements greater than 9: 3

# ### min_element Algorithm

Line 35 calls the C++20 `std::ranges::min_element` algorithm to locate the smallest element in its **forward_range** argument `a2`. Such a range supports **forward_iterators**, which allow `min_element` to read the range's elements. The algorithm returns an iterator located at the first occurrence of the range's smallest element or its sentinel if the range is empty. As with many algorithms that compare elements, you can provide a custom binary predicate function that specifies how to compare two elements and returns true if the first should be considered less than the second. Before dereferencing an iterator that might represent a range's sentinel, you should check that it does not match the sentinel, as in line 35.

Concepts C

Err X

```
```cpp
34      // locate minimum element in a2
35      if (auto result{std::ranges::min_element(a2)}; result != a2.end()) {
36          std::cout << "\na2 minimum element: " << *result;
37      }
38
```
```

a2 minimum element: 1

# ### max_element Algorithm

Line 40 calls the C++20 `std::ranges::max_element` algorithm to locate the largest element in its **forward_range** argument `a2`. Such a range supports **forward_iterators**, which allow `max_element` to read the range's elements. The algorithm returns an iterator located at the first occurrence of the range's largest element or its sentinel if the range is empty. Again, you can provide a custom binary predicate function specifying how to compare the elements.

Concepts C

```
```cpp
39      // locate maximum element in a2
40      if (auto result{std::ranges::max_element(a2)}; result != a2.end()) {
41          std::cout << "\na2 maximum element: " << *result;
42      }
43
```
```

a2 maximum element: 100

# ### minmax_element Algorithm

Line 45 calls the C++20 `std::ranges::minmax_element` algorithm to locate the smallest and largest elements in its **forward_range** argument `a2`. The algorithm returns a `std::ranges::minmax_element_result` containing iterators named `min` and `max` aimed at the smallest and largest elements, respectively:

Concepts C

+   - If there are duplicate smallest elements, the first iterator is located at the first of the smallest values.
+   - If there are duplicate largest elements, the second iterator is located at the last of the largest values—note that this is different from how `max_element` works.

You can provide a custom binary predicate function specifying how to compare elements.