# ISO/IEC 14882:2020(E)

```
constexpr decltype(auto) operator[](iter_difference_t<I> n) const
    requires random_access_iterator<I>;
```

```
template<common_with<I> I2>
    friend constexpr bool operator==(
        const counted_iterator& x, const counted_iterator<I2>& y);
    friend constexpr bool operator==(
        const counted_iterator& x, default_sentinel_t);
```

```
template<common_with<I> I2>
    friend constexpr strong_ordering operator<=>( 
        const counted_iterator& x, const counted_iterator<I2>& y);
```

```
friend constexpr iter_rvalue_reference_t<I> iter_move(const counted_iterator& i)
    noexcept(noexcept(ranges::iter_move(i.current)))
    requires input_iterator<I>;
```

```
template<indirectly_swappable<I> I2>
    friend constexpr void iter_swap(const counted_iterator& x, const counted_iterator<I2>& y)
    noexcept(noexcept(ranges::iter_swap(x.current, y.current)));
```

```
private:
    I current = I();                // exposition only
    iter_difference_t<I> length = 0;    // exposition only
};
```

```
template<class I>
struct incrementable_traits<counted_iterator<I>> {
    using difference_type = iter_difference_t<I>;
};
```

```
template<input_iterator I>
struct iterator_traits<counted_iterator<I>> : iterator_traits<I> {
    using pointer = void;
};
}
```

# 23.5.6.2 Constructors and conversions [counted.iter.const]

```
constexpr counted_iterator(I i, iter_difference_t<I> n);
```

1 Preconditions: n >= 0.

2 Effects: Initializes current with std::move(i) and length with n.

```
template<class I2>
    requires convertible_to<const I2&, I>
    constexpr counted_iterator(const counted_iterator<I2>& x);
```

3 Effects: Initializes current with x.current and length with x.length.

```
template<class I2>
    requires assignable_from<I&, const I2&>
    constexpr counted_iterator& operator=(const counted_iterator<I2>& x);
```

4 Effects: Assigns x.current to current and x.length to length.

5 Returns: *this.

# 23.5.6.3 Accessors [counted.iter.access]

```
constexpr I base() const & requires copy_constructible<I>;
```

1 Effects: Equivalent to: return current;

```
constexpr I base() &&;
```

2 Returns: std::move(current).