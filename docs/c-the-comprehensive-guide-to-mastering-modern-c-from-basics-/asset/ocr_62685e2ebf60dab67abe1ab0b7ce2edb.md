For the transform example, you can also use range adapters.

```
// https://godbolt.org/z/j9ozax8qE
#include <ranges> // zip_transform
// -
auto res = std::views::zip_transform(f, a, b); // Range adapter
for(auto s : res) { std::cout << s << " "; };
std::cout << '\\n'; // Output: N1 C7 C0 -1
```

# Listing 25.13 Transforming with range adapters.

Unlike the std::transform and std::ranges::transform algorithms, the range adapter std::views::zip_transform works lazily. It can also handle more than two sequences, which is why the operation f is specified first. zip_transform was introduced in C++23:

+   * copy
  Usage: constant, iterators: in/out
  Copies a range element-wise into a target range.

+   * copy_n
  Usage: frequent, iterators: in/out
  Copies n elements from a position.

+   * copy_if
  Usage: frequent, iterators: in/out
  Copies elements only if they satisfy a predicate.

+   * copy_backward
  Usage: occasional, iterators: bi
  Effectively like copy, but starts from the end; important for overlapping copies.

+   * move
  Usage: frequent, iterators: in/out