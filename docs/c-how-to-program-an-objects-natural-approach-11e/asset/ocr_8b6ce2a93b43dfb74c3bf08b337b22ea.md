```
```
array a1 contains: 1 3 5 7 9
array a2 contains: 2 4 5 7 9
```
```

**Fig. 14.9** | Algorithms copy_backward, merge, unique, reverse, copy_if and copy_n. (Part 2 of 2.)

# ### copy_backward Algorithm

The C++20 `std::ranges::copy_backward` algorithm (line 21) copies its first argument’s *bidirectional_range* (`a1`) into the range specified by the *output iterator* in its second argument—in this case, the end of the target container (`results.end()`). The algorithm copies the elements in reverse order, placing each into the target container starting from the element before `results.end()` and working toward the beginning of the container. The algorithm returns a `std::ranges::copy_backward_result` containing two iterators:

+   - The first is positioned at `a1.end()`.
+   - The second is positioned at the last element copied into the target range—that is, the beginning of `results` because the copy is performed backward.

Though the elements are copied in reverse order, they’re placed in `results` in the same order as `a1`. One difference between `copy` and `copy_backward` is that

+   - the iterator returned from `copy` is positioned after the last element copied and
+   - the one returned from `copy_backward` is positioned at the last element copied, which is the first element in the range.

```
```cpp
19 // place elements of a1 into results in reverse order
20 std::array<int, a1.size()> results{};
21 std::ranges::copy_backward(a1, results.end());
22 std::cout << "\nAfter copy_backward, results contains: ";
23 std::ranges::copy(results, output);
24
```
```

```
```
After copy_backward, results contains: 1 3 5 7 9
```
```

# ### move and move_backward Algorithm

You can use move semantics with ranges. The C++20 `std::ranges` algorithms `move` and `move_backward` (from header `<algorithm>`) work like the `copy` and `copy_backward` algorithms but move the elements in the specified ranges rather than copying them.

# ### merge Algorithm

The C++20 `std::ranges::merge` algorithm (line 27) combines two *input_ranges* that are each sorted in ascending order and writes the results to the target container specified by the third argument’s *output iterator*. After this operation, `results2` contains both ranges’ values in sorted order. A second version of `merge` takes iterator/sentinel pairs representing the two ranges. Both versions allow you to provide a *binary predicate function* that specifies the sorting order by comparing its two arguments and returning `true` if the first should be considered less than the second for ordering purposes.