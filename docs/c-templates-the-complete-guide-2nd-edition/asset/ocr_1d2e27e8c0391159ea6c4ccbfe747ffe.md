```
```cpp
template<typename List>
using LargestType = typename LargestTypeT<List>::Type;
```
```

The **LargestType** algorithm will return the first, largest type within the typelist. For example, if given the typelist `Typelist<bool, int, long, short>`, this algorithm will return the first type that is the same size as `long`, which is likely to be either `int` or `long`, depending on your platform.[^1]

The primary template for `LargestTypeT` doubles as the recursive case for the algorithm. It employs the common *first/rest* idiom, which has three steps. In the first step, it computes a partial result based on just the first element, which in this case is the front element of the list, and places it in `First`. Next, it recurses to compute the result for the rest of the elements in the list, and places that result in `Rest`. For example, in the first step of recursion for the typelist `Typelist<bool, int, long, short>`, `First` is `bool`, while `Rest` is the result of applying the algorithm to `Typelist<int, long, short>`. Finally, the third step combines the `First` and `Rest` results to produce the solution. Here, the `IfThenElse` picks the larger of either the first element in the list (`First`) or the best candidate so far (`Rest`), and returns the winner.[^2] The `>=` breaks ties in favor of the element that comes earlier in the list.

The recursion terminates when the list is empty. By default, we use `char` as a sentinel type to initialize the algorithm, because every type is as large as `char`.

Note that the basis case explicitly mentions the empty typelist `Typelist<>`. This is somewhat unfortunate, because it precludes the use of other forms of typelists, which we’ll return to in later sections (including Section 24.3 on page 566, Section 24.5 on page 571, and Chapter 25). To address this problem, we introduce an `IsEmpty` metafunction that determines whether the given typelist has no elements: [Click here to view code image](#).

# *typelist/typelistisempty.hpp*

```
```cpp
template<typename List>
class IsEmpty
{
public:
  static constexpr bool value = false;
};

template<>
class IsEmpty<Typelist<>> {
public:
  static constexpr bool value = true;
};
```
```