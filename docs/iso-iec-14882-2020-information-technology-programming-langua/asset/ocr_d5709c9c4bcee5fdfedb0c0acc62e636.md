# 23.5.6.4 Element access [counted.iter.elem]

```
constexpr iter_difference_t<I> count() const noexcept;
```

Effects: Equivalent to: return length;

```
constexpr decltype(auto) operator*();
constexpr decltype(auto) operator*() const
    requires dereferenceable<const I>;
```

Effects: Equivalent to: return *current;

```
constexpr decltype(auto) operator[](iter_difference_t<I> n) const
    requires random_access_iterator<I>;
```

Preconditions: n < length.

Effects: Equivalent to: return current[n];

# 23.5.6.5 Navigation [counted.iter.nav]

```
constexpr counted_iterator& operator++();
```

Preconditions: length > 0.

Effects: Equivalent to:

```
++current;
--length;
return *this;
```

```
decltype(auto) operator++(int);
```

Preconditions: length > 0.

Effects: Equivalent to:

```
--length;
try { return current++; } catch(...) { ++length; throw; }
```

```
constexpr counted_iterator operator++(int)
    requires forward_iterator<I>;
```

Effects: Equivalent to:

```
counted_iterator tmp = *this;
++*this;
return tmp;
```

```
constexpr counted_iterator& operator--()
    requires bidirectional_iterator<I>;
```

Effects: Equivalent to:

```
--current;
++length;
return *this;
```

```
constexpr counted_iterator operator--(int)
    requires bidirectional_iterator<I>;
```

Effects: Equivalent to:

```
counted_iterator tmp = *this;
--*this;
return tmp;
```

```
constexpr counted_iterator operator+(iter_difference_t<I> n) const
    requires random_access_iterator<I>;
```

Effects: Equivalent to: return counted_iterator(current + n, length - n);