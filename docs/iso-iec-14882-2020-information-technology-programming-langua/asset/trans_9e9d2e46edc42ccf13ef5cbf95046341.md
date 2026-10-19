

```
template<class Iterator>
    constexpr reverse_iterator<Iterator> make_reverse_iterator(Iterator i);
```

*Returns:* reverse_iterator<Iterator>(i).

## 23.5.2 Insert iterators

### 23.5.2.1 General

为了使插入操作能够像写入数组一样处理，库中提供了一种特殊的迭代器适配器，称为*插入迭代器*。使用常规迭代器类，

```
while (first != last) *result++ = *first++;
```

会将范围 [first, last) 复制到以 result 开始的范围。同样使用 result 为插入迭代器的代码会将相应元素插入到容器中。此设备允许库中的所有复制算法以*插入模式*而非*常规覆盖模式*工作。

插入迭代器由容器以及可能指向容器中插入位置的迭代器构造，如果该位置既不在开头也不在末尾。插入迭代器满足输出迭代器的要求。`operator*` 返回插入迭代器本身。赋值 `operator=(const T& x)` 在插入迭代器上定义，以允许写入它，它会在插入迭代器所指向的位置之前插入 x。换句话说，插入迭代器就像一个指向容器中插入发生位置的光标。`back_insert_iterator` 在容器末尾插入元素，`front_insert_iterator` 在容器开头插入元素，而 `insert_iterator` 在容器中迭代器所指的位置插入元素。`back_inserter`、`front_inserter` 和 `inserter` 是三个将容器转换为插入迭代器的函数。

### 23.5.2.2 Class template back_insert_iterator

```
namespace std {
    template<class Container>
    class back_insert_iterator {
    protected:
        Container* container = nullptr;

    public:
        using iterator_category = output_iterator_tag;
        using value_type        = void;
        using difference_type   = ptrdiff_t;
        using pointer           = void;
        using reference         = void;
        using container_type    = Container;

        constexpr back_insert_iterator() noexcept = default;
        constexpr explicit back_insert_iterator(Container& x);
        constexpr back_insert_iterator& operator=(const typename Container::value_type& value);
        constexpr back_insert_iterator& operator=(typename Container::value_type&& value);

        constexpr back_insert_iterator& operator*();
        constexpr back_insert_iterator& operator++();
        constexpr back_insert_iterator  operator++(int);
    };
}
```

### 23.5.2.2.1 Operations

```
constexpr explicit back_insert_iterator(Container& x);
```

*Effects:* Initializes container with address of(x).

```
constexpr back_insert_iterator& operator=(const typename Container::value_type& value);
```

*Effects:* As if by: `container->push_back(value);`

*Returns:* *this.

```
template<sized_sentinel_for<Iterator> S>
    friend constexpr iter_difference_t<Iterator>
        operator-(const move_iterator& x, const move_sentinel<S>& y);
    friend constexpr iter_rvalue_reference_t<Iterator>
        iter_move(const move_iterator& i)
            noexcept(noexcept(ranges::iter_move(i.current)));
    template<indirectly_swappable<Iterator> Iterator2>
        friend constexpr void
            iter_swap(const move_iterator& x, const move_iterator<Iterator2>& y)
            noexcept(noexcept(ranges::iter_swap(x.current, y.current)));
```

```
private:
    Iterator current;  // exposition only
};
}
```

1 The member typedef-name iterator_category denotes

- (1.1) — random_access_iterator_tag if the type iterator_traits<Iterator>::iterator_category models derived_from<random_access_iterator_tag>, and
- (1.2) — iterator_traits<Iterator>::iterator_category otherwise.

## 23.5.3.3 Requirements [move.iter.requirements]

1 The template parameter Iterator shall either meet the Cpp17InputIterator requirements (23.3.5.3) or model input_iterator (23.3.4.9). Additionally, if any of the bidirectional traversal functions are instantiated, the template parameter shall either meet the Cpp17BidirectionalIterator requirements (23.3.5.6) or model bidirectional_iterator (23.3.4.12). If any of the random access traversal functions are instantiated, the template parameter shall either meet the Cpp17RandomAccessIterator requirements (23.3.5.7) or model random_access_iterator (23.3.4.13).

## 23.5.3.4 Construction and assignment [move.iter.cons]

```
constexpr move_iterator();
```

1 Effects: Constructs a move_iterator, value-initializing current. Iterator operations applied to the resulting iterator have defined behavior if and only if the corresponding operations are defined on a value-initialized iterator of type Iterator.

```
constexpr explicit move_iterator(Iterator i);
```

2 Effects: Constructs a move_iterator, initializing current with std::move(i).

```
template<class U> constexpr move_iterator(const move_iterator<U>& u);
```

3 Mandates: U is convertible to Iterator.
4 Effects: Constructs a move_iterator, initializing current with u.base().

```
template<class U> constexpr move_iterator& operator=(const move_iterator<U>& u);
```

5 Mandates: U is convertible to Iterator.
6 Effects: Assigns u.base() to current.

## 23.5.3.5 Conversion [move.iter.op.conv]

```
constexpr Iterator base() const &;
```

1 Constraints: Iterator satisfies copy_constructible.
2 Preconditions: Iterator models copy_constructible.
3 Returns: current.

```
constexpr Iterator base() &&;
```

4 Returns: std::move(current).

## 23.5.3.6 Element access

constexpr reference operator*() const;

**Effects:** Equivalent to: `return ranges::iter_move(current);`

constexpr reference operator[](difference_type n) const;

**Effects:** Equivalent to: `ranges::iter_move(current + n);`

## 23.5.3.7 Navigation

constexpr move_iterator& operator++();

**Effects:** As if by `++current`.

**Returns:** `*this`.

constexpr auto operator++(int);

**Effects:** If Iterator models `forward_iterator`, equivalent to:

```cpp
move_iterator tmp = *this;
++current;
return tmp;
```

Otherwise, equivalent to `++current`.

constexpr move_iterator& operator--();

**Effects:** As if by `--current`.

**Returns:** `*this`.

constexpr move_iterator operator--(int);

**Effects:** As if by:

```cpp
move_iterator tmp = *this;
--current;
return tmp;
```

constexpr move_iterator operator+(difference_type n) const;

**Returns:** `move_iterator(current + n)`.

constexpr move_iterator& operator+=(difference_type n);

**Effects:** As if by: `current += n;`

**Returns:** `*this`.

constexpr move_iterator operator-(difference_type n) const;

**Returns:** `move_iterator(current - n)`.

constexpr move_iterator& operator-=(difference_type n);

**Effects:** As if by: `current -= n;`

**Returns:** `*this`.

## 23.5.3.8 Comparisons

```
template<class Iterator1, class Iterator2>
  constexpr bool operator==(const move_iterator<Iterator1>& x,
                            const move_iterator<Iterator2>& y);
template<sentinel_for<Iterator> S>
  friend constexpr bool operator==(const move_iterator& x,
                                   const move_sentinel<S>& y);
```

**Constraints:** `x.base() == y.base()` is well-formed and convertible to bool.

**Returns:** `x.base() == y.base()`.

```
template<class Iterator1, class Iterator2>
constexpr bool operator<(const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
```

Constraints: x.base() < y.base() is well-formed and convertible to bool.
Returns: x.base() < y.base().

```
template<class Iterator1, class Iterator2>
constexpr bool operator<(const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
```

Constraints: y.base() < x.base() is well-formed and convertible to bool.
Returns: y < x.

```
template<class Iterator1, class Iterator2>
constexpr bool operator<=(const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
```

Constraints: y.base() < x.base() is well-formed and convertible to bool.
Returns: !(y < x).

```
template<class Iterator1, class Iterator2>
constexpr bool operator>=(const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
```

Constraints: x.base() < y.base() is well-formed and convertible to bool.
Returns: !(x < y).

```
template<class Iterator1, three_way_comparable_with<Iterator1> Iterator2>
constexpr compare_three_way_result_t<Iterator1, Iterator2>
operator<=>(const move_iterator<Iterator1>& x,
             const move_iterator<Iterator2>& y);
```

Returns: x.base() <=> y.base().

## 23.5.3.9 Non-member functions

```
template<class Iterator1, class Iterator2>
  constexpr auto operator-(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y)
      -> decltype(x.base() - y.base());

template<sized_sentinel_for<Iterator> S>
  friend constexpr iter_difference_t<Iterator>
    operator-(const move_sentinel<S>& x, const move_iterator<Iterator>& y);

template<sized_sentinel_for<Iterator> S>
  friend constexpr iter_difference_t<Iterator>
    operator-(const move_iterator<Iterator>& x, const move_sentinel<S>& y);
```

Returns: x.base() − y.base().

```
template<class Iterator>
  constexpr move_iterator<Iterator>
    operator+(iter_difference_t<Iterator> n, const move_iterator<Iterator>& x);
```

Constraints: x + n is well-formed and has type Iterator.
Returns: x + n.

```
friend constexpr iter_value_reference_t<Iterator>
  iter_move(const move_iterator& i)
    noexcept(noexcept(ranges::iter_move(i.current)));
```

Effects: Equivalent to: return ranges::iter_move(i.current);

```
template<indirectly_swappable<Iterator> Iterator2>
  friend constexpr void
    iter_swap(const move_iterator& x, const move_iterator<Iterator2>& y)
      noexcept(noexcept(ranges::iter_swap(x.current, y.current)));
```

Effects: Equivalent to: ranges::iter_swap(x.current, y.current).

