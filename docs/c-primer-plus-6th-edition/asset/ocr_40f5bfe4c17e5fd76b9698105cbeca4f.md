requires that result not in the range [first, last)—that is, the target, can can't overlap
the source.

# move_backward() (C++11)

```
template<class BidirectionalIterator1,
class BidirectionalIterator2
BidirectionalIterator2 copy_backward(BidirectionalIterator1 first,

BidirectionalIterator1 last, BidirectionalIterator2 result);
```

The move_backward() function uses std::move() to move the elements in the range
[first, last] into the range [result - (last - first), result). Copying begins with
the element at last -1 being copied to location result - 1 and proceeds backward
from there to first. result - (last - first)—that is, an iterator pointing
one past the last copied-to-location. The function requires result not be in the
range [first, last). However, because copying is done backward, it is possible for the
target and source to overlap.

# swap()

```
template<class T> void swap(T& a, T& b);
```

The swap() function exchanges values stored at two locations specified by references.
(C++ most moves this function to the utility header file.)

# swap_ranges()

```
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 swap_ranges(

ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result);
```

The swap_ranges() function exchanges values in the range [first, last) with the cor-
responding values in the range beginning at first2.Two ranges should not overlap.

# iter_swap()

```
template<class ForwardIterator1, class ForwardIterator2>
void iter_swap(ForwardIterator1 a, ForwardIterator2 b);
```

The iter_swap() function exchanges values stored at two locations specified by iterators.

# transform()

```
template<class InputIterator, class OutputIterator, class UnaryOperation>
OutputIterator transform(InputIterator first, InputIterator last,
OutputIterator result, UnaryOperation op);
```