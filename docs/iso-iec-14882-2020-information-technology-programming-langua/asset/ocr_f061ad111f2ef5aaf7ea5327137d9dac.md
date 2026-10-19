```
public:
    using iterator_concept =
        conditional_t<forward_range<Base>, forward_iterator_tag, input_iterator_tag>;
    using iterator_category = input_iterator_tag;
    // 24.7.12.4, class split_view::outer-iterator::value_type
    struct value_type;
    using difference_type  = range_difference_t<Base>;

    outer-iterator() = default;
    constexpr explicit outer-iterator(Parent& parent)
        requires (!forward_range<Base>);
    constexpr outer-iterator(Parent& parent, iterator_t<Base> current)
        requires forward_range<Base>;
    constexpr outer-iterator(outer-iterator<!Const> i)
        requires Const && convertible_to<iterator_t<V>, iterator_t<Base>>;

    constexpr value_type operator*() const;

    constexpr outer-iterator& operator++();
    constexpr decltype(auto) operator++(int) {
        if constexpr (forward_range<Base>) {
            auto tmp = *this;
            ++*this;
            return tmp;
        } else
            ++*this;
    }

    friend constexpr bool operator==(const outer-iterator& x, const outer-iterator& y)
        requires forward_range<Base>;

    friend constexpr bool operator==(const outer-iterator& x, default_sentinel_t);
};
}
```

1 Many of the following specifications refer to the notional member current of outer-iterator. current is equivalent to current_ if V models forward_range, and parent_->current_ otherwise.

```
constexpr explicit outer-iterator(Parent& parent)
    requires (!forward_range<Base>);
2     Effects: Initializes parent_ with addressof(parent).

constexpr outer-iterator(Parent& parent, iterator_t<Base> current)
    requires forward_range<Base>;
3     Effects: Initializes parent_ with addressof(parent) and current_ with std::move(current).

constexpr outer-iterator(outer-iterator<!Const> i)
    requires Const && convertible_to<iterator_t<V>, iterator_t<Base>>;
4     Effects: Initializes parent_ with i.parent_ and current_ with std::move(i.current_).

constexpr value_type operator*() const;
5     Effects: Equivalent to: return value_type{*this};

constexpr outer-iterator& operator++();
6     Effects: Equivalent to:
        const auto end = ranges::end(parent_->base_);
        if (current == end) return *this;
        const auto [pbegin, pend] = subrange{parent_->pattern_};
        if (pbegin == pend) ++current;
        else {
            do {
                auto [b, p] = ranges::mismatch(std::move(current), end, pbegin, pend);
```