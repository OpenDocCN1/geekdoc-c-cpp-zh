

## ISO/IEC 14882:2020(E)

Effects: 使用 std::move(i) 初始化 begin_，使用 s 初始化 end_。如果 StoreSize 为 true，则使用 n 初始化 size_。

> [Note 1: 接受范围的长度并将其存储以便稍后从 size() 返回，使得 subrange 即使存储的迭代器和哨兵不建模 sized_sentinel_for 时也能建模 sized_range。—— end note]

```cpp
template<not-same-as<subrange> R>
    requires borrowed_range<R> &&
        convertible-to-non-slicing<iterator_t<R>, I> &&
        convertible_to<sentinel_t<R>, S>
constexpr subrange(R&& r) requires (!StoreSize || sized_range<R>);
```

Effects: 等价于：

- — 如果 StoreSize 为 true，则 subrange{r, ranges::size(r)}。
- — 否则，subrange{ranges::begin(r), ranges::end(r)}。

```cpp
template<not-same-as<subrange> PairLike>
    requires pair-like-convertible-from<PairLike, const I&, const S&>
constexpr operator PairLike() const;
```

Effects: 等价于：return PairLike(begin_, end_);

### 24.5.4.3 Accessors [range.subrange.access]

```cpp
constexpr I begin() const requires copyable<I>;
```

Effects: 等价于：return begin_;

```cpp
[[nodiscard]] constexpr I begin() requires (!copyable<I>);
```

Effects: 等价于：return std::move(begin_);

```cpp
constexpr S end() const;
```

```cpp
constexpr explicit single_view(const T& t);
```

1  **Effects:** 使用 t 初始化 *value_*。

```cpp
constexpr explicit single_view(T&& t);
```

2  **Effects:** 使用 std::move(t) 初始化 *value_*。

```cpp
template<class... Args>
  requires constructible_from<T, Args...>
constexpr single_view(in_place_t, Args&&... args);
```

3  **Effects:** 按如下方式初始化 *value_*：*value_{in_place, std::forward<Args>(args)...}*。

```cpp
constexpr T* begin() noexcept;
constexpr const T* begin() const noexcept;
```

4  **Effects:** 等价于：`return data();`

```cpp
constexpr T* end() noexcept;
constexpr const T* end() const noexcept;
```

5  **Effects:** 等价于：`return data() + 1;`

```cpp
static constexpr size_t size() noexcept;
```

6  **Effects:** 等价于：`return 1;`

```cpp
constexpr T* data() noexcept;
constexpr const T* data() const noexcept;
```

7  **Effects:** 等价于：`return value_.operator->();`

### 24.6.4 Iota view [range.iota]

### 24.6.4.1 Overview [range.iota.overview]

1  `iota_view` 通过反复递增初始值来生成元素序列。

2  名称 `views::iota` 表示一个定制点对象（16.3.3.3.6）。给定子表达式 E 和 F，表达式 `views::iota(E)` 和 `views::iota(E, F)` 分别与 `iota_view{E}` 和 `iota_view{E, F}` 表达式等价。

> 3  [Example 1:
> 
> ```cpp
> for (int i : iota_view{1, 10})
>   cout << i << ' ';  // prints: 1 2 3 4 5 6 7 8 9
> ```
> 
> — end example]

### 24.6.4.2 Class template iota_view [range.iota.view]

```cpp
namespace std::ranges {
  template<class I>
    concept decrementable =      // exposition only
      see below;
  template<class I>
    concept advanceable =        // exposition only
      see below;

  template<weakly_incrementable W, semiregular Bound = unreachable_sentinel_t>
    requires weakly-equality-comparable-with<W, Bound> && semiregular<W>
  class iota_view : public view_interface<iota_view<W, Bound>> {
  private:
    // 24.6.4.3, class iota_view::iterator
    struct iterator;              // exposition only
    // 24.6.4.4, class iota_view::sentinel
    struct sentinel;              // exposition only
    W value_ = W();               // exposition only
    Bound bound_ = Bound();       // exposition only
  public:
    iota_view() = default;
    constexpr explicit iota_view(W value);
```

- (5.2) — addressof(a += n) 等于 addressof(a)。
- (5.3) — I(a + n) 等于 (a += n)。
- (5.4) — 对于类型为 D 的任意两个正值 x 和 y，如果 I(a + D(x + y)) 是良定义的，则 I(a + D(x + y)) 等于 I(I(a + x) + y)。
- (5.5) — I(a + D(0)) 等于 a。
- (5.6) — 如果 I(a + D(n - 1)) 是良定义的，则 I(a + n) 等于 [](I c) { return ++c; }(I(a + D(n - 1)))。
- (5.7) — (b += -n) 等于 a。
- (5.8) — (b -= n) 等于 a。
- (5.9) — addressof(b -= n) 等于 addressof(b)。
- (5.10) — I(b - n) 等于 (b -= n)。
- (5.11) — D(b - a) 等于 n。
- (5.12) — D(a - b) 等于 D(-n)。
- (5.13) — bool(a <= b) 为 true。

```cpp
constexpr explicit iota_view(W value);
```

6 Preconditions: Bound 表示 unreachable_sentinel_t 或 Bound() 可从 value 到达。

7 Effects: 使用 value 初始化 value_。

```cpp
constexpr iota_view(type_identity_t<W> value, type_identity_t<Bound> bound);
```

8 Preconditions: Bound 表示 unreachable_sentinel_t 或 bound 可从 value 到达。当 W 和 Bound 建模 totally_ordered_with 时，则 bool(value <= bound) 为 true。

9 Effects: 使用 value 初始化 value_，使用 bound 初始化 bound_。

```cpp
constexpr iterator begin() const;
```

10 Effects: 等价于：return iterator{value_};

```cpp
constexpr auto end() const;
```

11 Effects: 等价于：

```cpp
if constexpr (same_as<Bound, unreachable_sentinel_t>)
  return unreachable_sentinel;
else
  return sentinel{bound_};
```

```cpp
constexpr iterator end() const requires same_as<W, Bound>;
```

12 Effects: 等价于：return iterator{bound_};

```cpp
constexpr auto size() const requires see below;
```

13 Effects: 等价于：

```cpp
if constexpr (is-integer-like<W> && is-integer-like<Bound>)
  return (value_ < 0)
    ? ((bound_ < 0)
      ? to-unsigned-like(-value_) - to-unsigned-like(-bound_)
      : to-unsigned-like(bound_) + to-unsigned-like(-value_))
    : to-unsigned-like(bound_) - to-unsigned-like(value_);
else
  return to-unsigned-like(bound_ - value_);
```

14 Remarks: requires-clause 中的表达式等价于 (same_as<W, Bound> && advanceable<W>) || (integral<W> && integral<Bound>) || sized_sentinel_for<Bound, W>

### 24.6.4.3 Class iota_view::iterator [range.iota.iterator]

```cpp
namespace std::ranges {
  template<weakly_incrementable W, semiregular Bound>
```

```cpp
constexpr explicit iterator(W value);
```

Effects: 使用 value 初始化 value_。

```cpp
constexpr W operator*() const noexcept(is_nothrow_copy_constructible_v<W>);
```

Effects: 等价于：return value_;

[Note 2: noexcept 子句由默认的 iter_move 实现所需要。—— end note]

```cpp
constexpr iterator& operator++();
```

Effects: 等价于：

```cpp
++value_;
return *this;
```

```cpp
constexpr void operator++(int);
```

Effects: 等价于 ++*this.

```cpp
constexpr iterator operator++(int) requires incrementable<W>;
```

Effects: 等价于：

```cpp
auto tmp = *this;
++*this;
return tmp;
```

```cpp
constexpr iterator& operator--() requires decrementable<W>;
```

Effects: 等价于：

```cpp
--value_;
return *this;
```

```cpp
constexpr iterator operator--(int) requires decrementable<W>;
```

Effects: 等价于：

```cpp
auto tmp = *this;
--*this;
return tmp;
```

```cpp
constexpr iterator& operator+=(difference_type n)
requires advanceable<W>;
```

Effects: 等价于：

```cpp
if constexpr (is-integer-like<W> && !is-signed-integer-like<W>) {
  if (n >= difference_type(0))
    value_ += static_cast<W>(n);
  else
    value_ -= static_cast<W>(-n);
} else {
  value_ += n;
}
return *this;
```

```cpp
constexpr iterator& operator-=(difference_type n)
requires advanceable<W>;
```

Effects: 等价于：

```cpp
if constexpr (is-integer-like<W> && !is-signed-integer-like<W>) {
  if (n >= difference_type(0))
    value_ -= static_cast<W>(n);
  else
    value_ += static_cast<W>(-n);
} else {
  value_ -= n;
}
return *this;
```

```cpp
constexpr W operator[](difference_type n) const
    requires advanceable<W>;
```

Effects: 等价于：return W(value_ + n);

```cpp
friend constexpr bool operator==(const iterator& x, const iterator& y)
    requires equality_comparable<W>;
```

Effects: 等价于：return x.value_ == y.value_;

```cpp
friend constexpr bool operator<(const iterator& x, const iterator& y)
    requires totally_ordered<W>;
```

Effects: 等价于：return x.value_ < y.value_;

```cpp
friend constexpr bool operator>(const iterator& x, const iterator& y)
    requires totally_ordered<W>;
```

Effects: 等价于：return y < x;

```cpp
friend constexpr bool operator<=(const iterator& x, const iterator& y)
    requires totally_ordered<W>;
```

Effects: 等价于：return !(y < x);

```cpp
friend constexpr bool operator>=(const iterator& x, const iterator& y)
    requires totally_ordered<W>;
```

Effects: 等价于：return !(x < y);

```cpp
friend constexpr auto operator<=>(const iterator& x, const iterator& y)
    requires totally_ordered<W> && three_way_comparable<W>;
```

Effects: 等价于：return x.value_ <=> y.value_;

```cpp
friend constexpr iterator operator+(iterator i, difference_type n)
    requires advanceable<W>;
```

Effects: 等价于：return i += n;

```cpp
friend constexpr iterator operator+(difference_type n, iterator i)
    requires advanceable<W>;
```

Effects: 等价于：return i + n;

```cpp
friend constexpr iterator operator-(iterator i, difference_type n)
    requires advanceable<W>;
```

Effects: 等价于：return i -= n;

```cpp
friend constexpr difference_type operator-(const iterator& x, const iterator& y)
    requires advanceable<W>;
```

Effects: 等价于：

```cpp
using D = difference_type;
if constexpr (is-integer-like<W>) {
    if constexpr (is-signed-integer-like<W>)
        return D(D(x.value_) - D(y.value_));
    else
        return (y.value_ > x.value_)
            ? D(-D(y.value_ - x.value_))
            : D(x.value_ - y.value_);
} else {
    return x.value_ - y.value_;
}
```

### 24.6.4.4 Class iota_view::sentinel [range.iota.sentinel]

```cpp
namespace std::ranges {
    template<weakly_incrementable W, semiregular Bound>
        requires weakly-equality-comparable-with<W, Bound>
    struct iota_view<W, Bound>::sentinel {
```

