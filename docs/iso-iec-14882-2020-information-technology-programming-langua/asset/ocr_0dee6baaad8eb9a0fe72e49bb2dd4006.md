```
```cpp
friend constexpr bool operator<=(const iterator& x, const iterator& y)
  requires random_access_range<Base>;
friend constexpr bool operator>=(const iterator& x, const iterator& y)
  requires random_access_range<Base>;
friend constexpr auto operator<=>(const iterator& x, const iterator& y)
  requires random_access_range<Base> && three_way_comparable<iterator_t<Base>>;

friend constexpr iterator operator+(const iterator& x, difference_type y)
  requires random_access_range<Base>;
friend constexpr iterator operator+(difference_type x, const iterator& y)
  requires random_access_range<Base>;
friend constexpr iterator operator-(const iterator& x, difference_type y)
  requires random_access_range<Base>;
friend constexpr difference_type operator-(const iterator& x, const iterator& y)
  requires random_access_range<Base>;
};
}

constexpr explicit iterator(iterator_t<Base> current);
```

*Effects:* Initializes `current_` with `std::move(current)`.

```cpp
constexpr iterator(iterator<!Const> i)
  requires convertible_to<iterator_t<!Const>, iterator_t<Base>>;
```

*Effects:* Initializes `current_` with `std::move(i.current_)`.

```cpp
constexpr iterator_t<Base> base() const&
  requires copyable<iterator_t<Base>>;
```

*Effects:* Equivalent to: `return current_;`

```cpp
constexpr iterator_t<Base> base() &&;
```

*Effects:* Equivalent to: `return std::move(current_);`

```cpp
constexpr iterator& operator++();
```

*Effects:* Equivalent to:

```cpp
++current_;
return *this;
```

```cpp
constexpr void operator++(int) requires (!forward_range<Base>);
```

*Effects:* Equivalent to: `++current_`.

```cpp
constexpr iterator operator++(int) requires forward_range<Base>;
```

*Effects:* Equivalent to:

```cpp
auto temp = *this;
++current_;
return temp;
```

```cpp
constexpr iterator& operator--() requires bidirectional_range<Base>;
```

*Effects:* Equivalent to:

```cpp
--current_;
return *this;
```

```cpp
constexpr iterator operator--(int) requires bidirectional_range<Base>;
```

*Effects:* Equivalent to:

```cpp
auto temp = *this;
--current_;
return temp;
```
```