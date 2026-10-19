```
constexpr auto size() const requires sized_range<const V> {
    return ranges::size(base_);
}
};

template<class R>
    reverse_view(R&&) -> reverse_view<views::all_t<R>>;
}
```

```
constexpr explicit reverse_view(V base);
```

Effects: Initializes base_ with std::move(base).

```
constexpr reverse_iterator<iterator_t<V>> begin();
```

Returns:
    make_reverse_iterator(ranges::next(ranges::begin(base_), ranges::end(base_)))

Remarks: In order to provide the amortized constant time complexity required by the range concept, this function caches the result within the reverse_view for use on subsequent calls.

```
constexpr reverse_iterator<iterator_t<V>> begin() requires common_range<V>;
constexpr auto begin() const requires common_range<const V>;
```

Effects: Equivalent to: return make_reverse_iterator(ranges::end(base_));

```
constexpr reverse_iterator<iterator_t<V>> end();
constexpr auto end() const requires common_range<const V>;
```

Effects: Equivalent to: return make_reverse_iterator(ranges::begin(base_));

# 24.7.16 Elements view [range.elements]

# 24.7.16.1 Overview [range.elements.overview]

1 elements_view takes a view of tuple-like values and a size_t, and produces a view with a value-type of the Nth element of the adapted view’s value-type.

2 The name views::elements<N> denotes a range adaptor object (24.7.2). Given a subexpression E and constant expression N, the expression views::elements<N>(E) is expression-equivalent to elements_view<views::all_t<decltype((E))>, N>{E}.

```
[Example 1:

auto historical_figures = map{
    {"Lovelace"sv, 1815},
    {"Turing"sv, 1912},
    {"Babbage"sv, 1791},
    {"Hamilton"sv, 1936}
};

auto names = historical_figures | views::elements<0>;
for (auto&& name : names) {
    cout << name << ' ';
    // prints Babbage Hamilton Lovelace Turing
}

auto birth_years = historical_figures | views::elements<1>;
for (auto&& born : birth_years) {
    cout << born << ' ';
    // prints 1791 1936 1815 1912
}
— end example]
```

3 keys_view is an alias for elements_view<views::all_t<R>, 0>, and is useful for extracting keys from associative containers.