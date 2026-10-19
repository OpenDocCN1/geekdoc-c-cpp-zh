

### 24.7.9.2 类模板 drop_view [range.drop.view]

```cpp
namespace std::ranges {
    template<view V>
    class drop_view : public view_interface<drop_view<V>> {
    public:
        drop_view() = default;
        constexpr drop_view(V base, range_difference_t<V> count);

        constexpr V base() const& requires copy_constructible<V> { return base_; }
        constexpr V base() && { return std::move(base_); }

        constexpr auto begin()
            requires (! (simple_view<V> && random_access_range<V>));
        constexpr auto begin() const
            requires random_access_range<const V>;

        constexpr auto end()
            requires (!simple_view<V>)
        { return ranges::end(base_); }

        constexpr auto end() const
            requires range<const V>
        { return ranges::end(base_); }

        constexpr auto size()
            requires sized_range<V>
        {
            const auto s = ranges::size(base_);
            const auto c = static_cast<decltype(s)>(count_);
            return s < c ? 0 : s - c;
        }

        constexpr auto size() const
            requires sized_range<const V>
        {
            const auto s = ranges::size(base_);
            const auto c = static_cast<decltype(s)>(count_);
            return s < c ? 0 : s - c;
        }
    private:
        V base_ = V();                     // exposition only
        range_difference_t<V> count_ = 0;  // exposition only
    };

    template<class R>
        drop_view(R&&, range_difference_t<R>) -> drop_view<views::all_t<R>>;
}
```

```cpp
constexpr drop_view(V base, range_difference_t<V> count);
```

1 前提条件：count >= 0 成立。

2 效果：使用 std::move(base) 初始化 base_，并使用 count 初始化 count_。

3 [示例 1：

```cpp
auto ints = views::iota(0) | views::take(10);
auto latter_half = drop_view{ints, 5};
for (auto i : latter_half) {
    cout << i << ' ';
}
// prints 5 6 7 8 9
```

— 示例结束]

效果：等价于：return *pred_;

返回：ranges::find_if_not(base_, cref(*pred_))。

备注：当 drop_while_view 满足 forward_range 时，为了提供 range 概念所要求的均摊常数时间复杂度，第一次调用会将该结果缓存在 drop_while_view 中，以供后续调用使用。

> [注 1：如果没有这一点，将 reverse_view 应用于 drop_while_view 会产生二次迭代复杂度。— 注结束]

## 24.7.11 连接视图 join_view [range.join]

### 24.7.11.1 概述 [range.join.overview]

1 join_view 将范围的视图展平为一个视图。

2 名称 views::join 表示一个范围适配器对象（24.7.2）。给定子表达式 E，表达式 views::join(E) 与 join_view{E} 表达式等价。

> [示例 1：
> vector<string> ss{"hello", " ", "world", "!"};
> join_view greeting{ss};
> for (char ch : greeting)
>     cout << ch;                         // prints: hello world!
> — 示例结束]

### 24.7.11.2 类模板 join_view [range.join.view]

```cpp
namespace std::ranges {
template<input_range V>
  requires view<V> && input_range<range_reference_t<V>> &&
           (is_reference_v<range_reference_t<V>> ||
            view<range_value_t<V>>)
class join_view : public view_interface<join_view<V>> {
private:
  using InnerRng = range_reference_t<V>;          // exposition only
  // 24.7.11.3, class template join_view::iterator
  template<bool Const>
    struct iterator;                             // exposition only
  // 24.7.11.4, class template join_view::sentinel
  template<bool Const>
    struct sentinel;                             // exposition only
  V base_ = V();                                   // exposition only
  views::all_t<InnerRng> inner_ =                  // exposition only, present only when !is_reference_v<InnerRng>
    views::all_t<InnerRng>();
public:
  join_view() = default;
  constexpr explicit join_view(V base);
  constexpr V base() const& requires copy_constructible<V> { return base_; }
  constexpr V base() && { return std::move(base_); }
  constexpr auto begin() {
    constexpr bool use_const = simple_view<V> &&
                               is_reference_v<range_reference_t<V>>;
    return iterator<use_const>{*this, ranges::begin(base_)};
  }
}
```

### 24.7.11.3 类模板 join_view::iterator [range.join.iterator]

iterator::difference_type 表示以下类型：

```cpp
common_type_t<
    range_difference_t<Base>,
    range_difference_t<range_reference_t<Base>>>
```

join_view 迭代器使用 `satisfy` 函数跳过空的内部范围。

```cpp
constexpr void satisfy();        // exposition only
```

**效果：** 等价于：

```cpp
auto update_inner = [this](range_reference_t<Base> x) -> auto& {
    if constexpr (ref-is-glvalue) // x is a reference
        return x;
    else
        return (parent_->inner_ = views::all(std::move(x)));
};

for (; outer_ != ranges::end(parent_->base_); ++outer_) {
    auto& inner = update_inner(*outer_);
    inner_ = ranges::begin(inner);
    if (inner_ != ranges::end(inner))
        return;
}
if constexpr (ref-is-glvalue)
    inner_ = iterator_t<range_reference_t<Base>>();
```

```cpp
constexpr iterator(Parent& parent, iterator_t<Base> outer);
```

**效果：** 使用 `std::move(outer)` 初始化 `outer_`，使用 `addressof(parent)` 初始化 `parent_`；然后调用 `satisfy()`。

```cpp
constexpr iterator(iterator<!Const> i)
requires Const &&
    convertible_to<iterator_t<V>, iterator_t<Base>> &&
    convertible_to<iterator_t<InnerRng>,
                         iterator_t<range_reference_t<Base>>>;
```

**效果：** 使用 `std::move(i.outer_)` 初始化 `outer_`，使用 `std::move(i.inner_)` 初始化 `inner_`，并使用 `i.parent_` 初始化 `parent_`。

```cpp
constexpr iterator_t<Base> operator->() const
    requires has-arrow<iterator_t<Base>> && copyable<iterator_t<Base>>;
```

**效果：** 等价于 return `inner_;`

```cpp
constexpr iterator& operator++();
```

设 `inner-range` 为：

- (9.1) 如果 `ref-is-glvalue` 为 true，则为 `*outer_`。
- (9.2) 否则，为 `parent_->inner_`。

**效果：** 等价于：

```cpp
auto&& inner_rng = inner-range;
if (++inner_ == ranges::end(inner_rng)) {
    ++outer_;
    satisfy();
}
return *this;
```

```cpp
constexpr void operator++(int);
```

**效果：** 等价于：`++*this`。

```cpp
constexpr iterator operator++(int)
    requires ref-is-glvalue && forward_range<Base> &&
            forward_range<range_reference_t<Base>>;
```

**效果：** 等价于：

```cpp
auto tmp = *this;
++*this;
return tmp;
```

```cpp
constexpr iterator& operator--()
    requires ref-is-glvalue && bidirectional_range<Base> &&
            bidirectional_range<range_reference_t<Base>> &&
            common_range<range_reference_t<Base>>;
```

**效果：** 等价于：

```cpp
if (outer_ == ranges::end(parent_->base_))
    inner_ = ranges::end(*--outer_);
while (inner_ == ranges::begin(*outer_))
    inner_ = ranges::end(*--outer_);
--inner_;
return *this;
```

```cpp
constexpr iterator operator--(int)
    requires ref-is-glvalue && bidirectional_range<Base> &&
            bidirectional_range<range_reference_t<Base>> &&
            common_range<range_reference_t<Base>>;
```

**效果：** 等价于：

```cpp
auto tmp = *this;
--*this;
return tmp;
```

```cpp
friend constexpr bool operator==(const iterator& x, const iterator& y)
    requires ref-is-glvalue && equality_comparable<iterator_t<Base>> &&
            equality_comparable<iterator_t<range_reference_t<Base>>>;
```

**效果：** 等价于：return x.outer_ == y.outer_ && x.inner_ == y.inner_;

```cpp
friend constexpr void iter_swap(const iterator& x, const iterator& y)
    noexcept(noexcept(ranges::iter_swap(x.inner_, y.inner_)));
```

**效果：** 等价于：return ranges::iter_swap(x.inner_, y.inner_);

### 24.7.11.4 类模板 join_view::sentinel [range.join.sentinel]

```cpp
namespace std::ranges {
    template<input_range V>
        requires view<V> && input_range<range_reference_t<V>> &&
                (is_reference_v<range_reference_t<V>> ||
                 view<range_value_t<V>>)
    template<bool Const>
    struct join_view<V>::sentinel {
    private:
        using Parent =
            conditional_t<Const, const join_view, join_view>; // exposition only
        using Base   = conditional_t<Const, const V, V>;      // exposition only
        sentinel_t<Base> end_ = sentinel_t<Base>();           // exposition only
    public:
        sentinel() = default;
        constexpr explicit sentinel(Parent& parent);
        constexpr sentinel(sentinel<!Const> s)
            requires Const && convertible_to<sentinel_t<V>, sentinel_t<Base>>;
        friend constexpr bool operator==(const iterator<Const>& x, const sentinel& y);
    };
}
```

