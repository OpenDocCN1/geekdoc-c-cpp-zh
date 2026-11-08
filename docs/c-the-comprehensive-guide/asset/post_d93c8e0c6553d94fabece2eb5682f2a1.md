
The beginning of the second range is passed with `s.rbegin()`. `rbegin()` returns an iterator that, when incremented with ++, moves one element backward. So the same sequence is traversed backward here. In the end, the first letter is compared with the last, then the second with the second-to-last, and so on.

We don't necessarily have to restrict `isPalindrome` to `string_view`. We could also allow `input_range auto&&` as a parameter, and the function would work with any range and container that supports `rbegin()`. If I were more careful, I wouldn't traverse the entire sequence from start to finish, but only up to the halfway point, because `==` should be symmetric. I could achieve this by writing the following instead of `s.end()`:
`s.begin()+(s.end()-s.begin())/2`.

In the case of `for_each`, information is not the goal; rather, a unary function without a return value is called on each element. Actually, these functions are intended to be read-only. However, if you provide an (in)appropriate functor or predicate, you can indeed modify the elements of the range. Doing so is not forbidden but probably confusing. With `for_each`, you see an example in Listing 25.11. Instead, you should use `transform` here.

```cpp
// https://godbolt.org/z/jz1GqQ7d9
#include <iostream>
#include <vector>
#include <algorithm>
int main() {
    std::vector<int> c{ 1,2,3,4 };
    std::ranges::for_each(c, [](auto &n) { n *= n; }); // modifying
    std::cout << c[3] << '\n'; // Output: 16
}
```

**Listing 25.11** Even “read-only” algorithms like `for_each` can modify elements.

That is why I want to emphasize one thing: do not use `for_each` to solve every problem. There are often other algorithms that are better at solving certain problems. And if you look at the list of algorithms from time to time, you will become more comfortable with them over time, your code will become more compact and—I claim—better. A few examples:

- If you want to determine how often an element is contained in a sequence, use `count`, not `for_each`.
- If you want to check a predicate for all elements, use `all_of`.
- If you want to know if at least one element satisfies a predicate, use `any_of`.
- If a sequence contains the same elements as another, just in a different order, by no means use `for_each`; instead, use `is_permutation`.

These are the available nonmodifying algorithms:

- **all_of**  
  Usage: frequent; iterators: in  
  Checks if a predicate is true for all elements.

- **any_of**  
  Usage: frequent; iterators: in  
  Checks if at least one element satisfies the predicate.

- **none_of**  
  Usage: frequent; iterators: in  
  Checks if none of the elements satisfy a predicate.

- **for_each**  
  Usage: constant; iterators: in  
  Applies a unary function to each element, see Listing 25.11.

- **for_each_n**  
  Usage: rare; iterators: in  
  Applies a unary function to the first *n* elements of a range.

- **find**  
  Usage: constant; iterators: in  
  Finds by a sample value.

- **find_if**  
  Usage: constant; iterators: in  
  Finds by a predicate, see Listing 25.9.

- **find_if_not**  
  Usage: frequent; iterators: in  
  Finds by the negation of a predicate.

- **find_end**  
  Usage: rare; iterators: fw  
  Finds the end of a matching subsequence.

- **find_first_of**  
  Usage: frequent; iterators: in/fw  
  Finds one of several sample values.

- **`ranges::find_last`, `ranges::find_last_if`, `ranges::find_last_if_not`**  
  Usage: occasional (C++23); iterators: in/fw  
  Finds the last element or the element matching the predicate.

- **adjacent_find**  
  Usage: occasional; iterators: fw  
  Finds the first position where two adjacent elements both satisfy a predicate.

- **count**  
  Usage: constant; iterators: in  
  Counts the number of occurrences of a sample value.

- **count_if**  
  Usage: constant; iterators: in  
  Counts how often a predicate matches.

- **mismatch**  
  Usage: frequent; iterators: in  
  Finds the first difference between two sequences.

- **equal**  
  Usage: constant; iterators: in  
  Checks if all elements are pairwise equal, see Listing 25.10.

- **is_permutation**  
  Usage: occasional; iterators: in  
  Is one sequence just a permutation of another?

- **search**  
  Usage: frequent; iterators: fw  
  Finds the position where a subsequence is hidden within a larger sequence.

- **search_n**  
  Usage: occasional; iterators: fw  
  Finds the position with *n* consecutive values equal to the sought value.

- **`ranges::contains`, `ranges::contains_subrange`**  
  Usage: frequent (C++23); iterators: fw  
  Checks whether a single element or an entire range is contained within another range. `contains` is like `find(...) != end()`, `contains_subrange` is like `search(...)`, but more expressive.

- **`ranges::starts_with`**  
  Usage: frequent (C++23); iterators: fw  
  Checks if one range starts with another.

- **`ranges::ends_with`**  
  Usage: frequent (C++23); iterators: fw  
  Checks if one range ends with another.

`std::search` optionally takes an additional Searcher parameter, which specifies the algorithm to be used for searching a subsequence in a container (e.g., string):

```cpp
template<forward_iterator It, class Searcher>
ForwardIterator std::search(It first, It last, const Searcher& searcher);
```

At least the well-known Boyer-Moore algorithms like `boyer_moore_searcher` and Boyer-Moore-Horspool algorithms like `boyer_moore_horspool_searcher` are available. These can significantly speed up the search, especially when the search text is long and consists of many different characters. Do not expect a significant speedup when searching for "aaaaaa" or "ababab". You can also let the implementation decide by using `default_searcher`. The `std::ranges::search` variant does not support the Searcher parameter.

## 25.6.4 Inherently Modifying Algorithms

The functions in this section write a result to an output range. For some of the algorithms, it is allowed for the output range and input range to overlap. This is not always the case, so be careful and check the documentation to see if overlapping is allowed. Some algorithms like `unique` modify the sequence in place.

Let me highlight a small group of functions that are related but do not appear directly next to each other due to alphabetical sorting—or even in a different list. The following functions all work in some form on input and/or output sequences and apply a function `f` defined by you to the elements:

- `for_each` applies `f` to each element of an input sequence; `f` returns void and is unary.
- `generate` applies `f` to each element of the output sequence; `f` returns an element and is nullary.
- `transform` applies `f` to each element of the input sequence and writes the result to an output sequence; `f` returns an element and is unary.
- `transform` can also apply `f` to two input sequences and write the result to an output sequence; in this case, `f` returns an element and is binary.

By its nature, `for_each` usually triggers a side effect, such as output or changing an internal state. Similarly, `generate` will likely change an internal state as a side effect; otherwise the generated sequences would be quite boring.

Especially `transform` is extremely powerful. `f` can indeed accept arguments of a completely different type than it returns. The elements of the containers underlying the iterators only need to match. In Listing 25.12, I transform a sequence of char and int to a sequence of string.

```cpp
// https://godbolt.org/z/7r4b8jdGr
#include <algorithm>
#include <iostream>
#include <vector>
#include <string>

using std::to_string; using std::string; using std::vector;
struct Squares {
    mutable int n = 1;
    int operator()() const { return n*n++; }
};
```
