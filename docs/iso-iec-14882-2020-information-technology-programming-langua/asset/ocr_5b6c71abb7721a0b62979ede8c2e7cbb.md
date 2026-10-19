# 23.5.1.9 Non-member functions [reverse.iter.nonmember]

```
template<class Iterator1, class Iterator2>
constexpr bool operator<=(
    const reverse_iterator<Iterator1>& x,
    const reverse_iterator<Iterator2>& y);
```

Constraints: x.base() >= y.base() is well-formed and convertible to bool.

Returns: x.base() >= y.base().

```
template<class Iterator1, class Iterator2>
constexpr bool operator>=(
    const reverse_iterator<Iterator1>& x,
    const reverse_iterator<Iterator2>& y);
```

Constraints: x.base() <= y.base() is well-formed and convertible to bool.

Returns: x.base() <= y.base().

```
template<class Iterator1, three_way_comparable_with<Iterator1> Iterator2>
constexpr compare_three_way_result_t<Iterator1, Iterator2>
operator<=>(const reverse_iterator<Iterator1>& x,
    const reverse_iterator<Iterator2>& y);
```

Returns: y.base() <=> x.base().

[Note 1: The argument order in the Returns: element is reversed because this is a reverse iterator. — end note]

```
template<class Iterator1, class Iterator2>
constexpr auto operator-(
    const reverse_iterator<Iterator1>& x,
    const reverse_iterator<Iterator2>& y) -> decltype(y.base() - x.base());
```

Returns: y.base() - x.base().

```
template<class Iterator>
constexpr reverse_iterator<Iterator> operator+(
    typename reverse_iterator<Iterator>::difference_type n,
    const reverse_iterator<Iterator>& x);
```

Returns: reverse_iterator<Iterator>(x.base() - n).

```
friend constexpr iter_rvalue_reference_t<Iterator>
iter_move(const reverse_iterator& i) noexcept(see below);
```

Effects: Equivalent to:
    auto tmp = i.base();
    return ranges::iter_move(--tmp);

Remarks: The expression in noexcept is equivalent to:
    is_nothrow_copy_constructible_v<Iterator> &&
    noexcept(ranges::iter_move(--declval<Iterator&>()))

```
template<indirectly_swappable<Iterator> Iterator2>
friend constexpr void
iter_swap(const reverse_iterator& x,
    const reverse_iterator<Iterator2>& y) noexcept(see below);
```

Effects: Equivalent to:
    auto xtmp = x.base();
    auto ytmp = y.base();
    ranges::iter_swap(--xtmp, --ytmp);

Remarks: The expression in noexcept is equivalent to:
    is_nothrow_copy_constructible_v<Iterator> &&
    is_nothrow_copy_constructible_v<Iterator2> &&
    noexcept(ranges::iter_swap(--declval<Iterator&>(), --declval<Iterator2&>()))