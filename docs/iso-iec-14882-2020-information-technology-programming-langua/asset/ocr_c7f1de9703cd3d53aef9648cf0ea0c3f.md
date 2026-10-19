# 23.5.6.7 Customizations [counted.iter.cust]

```
friend constexpr iter_rvalue_reference_t<I>
iter_move(const counted_iterator& i)
    noexcept(noexcept(ranges::iter_move(i.current)))
    requires input_iterator<I>;

Effects: Equivalent to: return ranges::iter_move(i.current);
```

```
template<indirectly_swappable<I> I2>
friend constexpr void
iter_swap(const counted_iterator& x, const counted_iterator<I2>& y)
    noexcept(noexcept(ranges::iter_swap(x.current, y.current)));

Effects: Equivalent to ranges::iter_swap(x.current, y.current).
```

# 23.5.7 Unreachable sentinel [unreachable.sentinel]

1 Class unreachable_sentinel_t can be used with any weakly_incrementable type to denote the “upper bound” of an unbounded interval.

2 [Example 1:
char* p;
// set p to point to a character buffer containing newlines
char* nl = find(p, unreachable_sentinel, '\n');
Provided a newline character really exists in the buffer, the use of unreachable_sentinel above potentially makes the call to find more efficient since the loop test against the sentinel does not require a conditional branch. — end example]

```
namespace std {
struct unreachable_sentinel_t {
template<weakly_incrementable I>
friend constexpr bool operator==(unreachable_sentinel_t, const I&) noexcept
{ return false; }
};
}
```

# 23.6 Stream iterators [stream.iterators]

# 23.6.1 General [stream.iterators.general]

1 To make it possible for algorithmic templates to work directly with input/output streams, appropriate iterator-like class templates are provided.

[Example 1:
partial_sum(istream_iterator<double, char>(cin),
istream_iterator<double, char>(),
ostream_iterator<double, char>(cout, "\n"));
reads a file containing floating-point numbers from cin, and prints the partial sums onto cout. — end example]

# 23.6.2 Class template istream_iterator [istream.iterator]

# 23.6.2.1 General [istream.iterator.general]

1 The class template istream_iterator is an input iterator (23.3.5.3) that reads successive elements from the input stream for which it was constructed.

```
namespace std {
template<class T, class charT = char, class traits = char_traits<charT>,
class Distance = ptrdiff_t>
class istream_iterator {
public:
using iterator_category = input_iterator_tag;
using value_type = T;
using difference_type = Distance;
using pointer = const T*;
using reference = const T&;
using char_type = charT;
using traits_type = traits;
```