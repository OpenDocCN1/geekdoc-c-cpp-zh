

```
constexpr explicit sentinel(Parent& parent);

1    *Effects:* Initializes `end_` with ranges::end(parent.base_).

constexpr sentinel(sentinel<!Const> s)
  requires Const && convertible_to<sentinel_t<V>, sentinel_t<Base>>;

2    *Effects:* Initializes `end_` with std::move(s.end_).

friend constexpr bool operator==(const_iterator<Const>& x, const sentinel& y);

3    *Effects:* Equivalent to: `return x.outer_ == y.end_;`
```

## 24.7.12 分割视图 [range.split]

### 24.7.12.1 概述 [range.split.overview]

split_view 接受一个视图和一个分隔符，并根据分隔符将视图拆分为子范围。分隔符可以是单个元素或元素的视图。

名称 views::split 表示一个范围适配器对象（24.7.2）。给定子表达式 E 和 F，表达式 views::split(E, F) 与 split_view{E, F} 表达式等价。

```
[*Example 1:*]

string str{"the quick brown fox"};
split_view sentence{str, ' '};
for (auto word : sentence) {
  for (char ch : word)
    cout << ch;
  cout << '*';
}
// The above prints: the*quick*brown*fox*
--- end example]
```

### 24.7.12.2 类模板 split_view [range.split.view]

```
namespace std::ranges {
  template<auto>
    struct require-constant;        // exposition only

  template<class R>
    concept tiny-range =             // exposition only
      sized_range<R> &&
      requires { typename require-constant<remove_reference_t<R>::size()>; } &&
      (remove_reference_t<R>::size() <= 1);

  template<input_range V, forward_range Pattern>
    requires view<V> && view<Pattern> &&
      indirectly_comparable<iterator_t<V>, iterator_t<Pattern>, ranges::equal_to> &&
      (forward_range<V> || tiny-range<Pattern>)
  class split_view : public view_interface<split_view<V, Pattern>> {
  private:
    V base_ = V();                         // exposition only
    Pattern pattern_ = Pattern();         // exposition only
    iterator_t<V> current_ = iterator_t<V>(); // exposition only, present only if !forward_range<V>
    // 24.7.12.3, class template split_view::outer-iterator
    template<bool> struct outer-iterator; // exposition only
    // 24.7.12.5, class template split_view::inner-iterator
    template<bool> struct inner-iterator; // exposition only
  public:
    split_view() = default;
    constexpr split_view(V base, Pattern pattern);

    template<input_range R>
      requires constructible_from<V, views::all_t<R>> &&
               constructible_from<Pattern, single_view<range_value_t<R>>>
    constexpr split_view(R&& r, range_value_t<R> e);
```

### 24.7.12.3 类模板 split_view::outer-iterator [range.split.outer]

```
constexpr V base() const& requires copy_constructible<V> { return base_; }
constexpr V base() && { return std::move(base_); }

constexpr auto begin() {
    if constexpr (forward_range<V>)
        return outer-iterator<simple-view<V>>{*this, ranges::begin(base_)};
    else {
        current_ = ranges::begin(base_);
        return outer-iterator<false>{*this};
    }
}

constexpr auto begin() const requires forward_range<V> && forward_range<const V> {
    return outer-iterator<true>{*this, ranges::begin(base_)};
}

constexpr auto end() requires forward_range<V> && common_range<V> {
    return outer-iterator<simple-view<V>>{*this, ranges::end(base_)};
}

constexpr auto end() const {
    if constexpr (forward_range<V> && forward_range<const V> && common_range<const V>)
        return outer-iterator<true>{*this, ranges::end(base_)};
    else
        return default_sentinel;
};

template<class R, class P>
    split_view(R&&, P&&) -> split_view<views::all_t<R>, views::all_t<P>>;

template<input_range R>
    split_view(R&&, range_value_t<R>)
    -> split_view<views::all_t<R>, single_view<range_value_t<R>>>;
}

constexpr split_view(V base, Pattern pattern);

template<input_range R>
    requires constructible_from<V, views::all_t<R>> &&
            constructible_from<Pattern, single_view<range_value_t<R>>>
constexpr split_view(R&& r, range_value_t<R> e);

namespace std::ranges {
    template<input_range V, forward_range Pattern>
        requires view<V> && view<Pattern> &&
                indirectly_comparable<iterator_t<V>, iterator_t<Pattern>, ranges::equal_to> &&
                (forward_range<V> || tiny-range<Pattern>)
    template<bool Const>
    struct split_view<V, Pattern>::outer-iterator {
    private:
        using Parent =
            conditional_t<Const, const split_view, split_view>;
        using Base =
            conditional_t<Const, const V, V>;
        Parent* parent_ = nullptr;
        iterator_t<Base> current_ =
            iterator_t<Base>();
```

1 Effects: Initializes base_ with std::move(base), and pattern_ with std::move(pattern).

2 Effects: Initializes base_ with views::all(std::forward<R>(r)), and pattern_ with single_view{ std::move(e) }.

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

```
auto end = ranges::end(x.i_.parent_->base_);
if constexpr (tiny-range<Pattern>) {
    const auto & cur = x.i_.current;
    if (cur == end) return true;
    if (pcur == pend) return x.incremented_;
    return *cur == *pcur;
} else {
    auto cur = x.i_.current;
    if (cur == end) return true;
    if (pcur == pend) return x.incremented_;
    do {
        if (*cur != *pcur) return false;
        if (++pcur == pend) return true;
    } while (++cur != end);
    return false;
}
```

```
friend constexpr void iter_swap(const inner-iterator& x, const inner-iterator& y)
    noexcept(noexcept(ranges::iter_swap(x.i_.current, y.i_.current)))
    requires indirectly_swappable<iterator_t<Base>>;
```

Effects: Equivalent to ranges::iter_swap(x.i_.current, y.i_.current).

## 24.7.13 计数视图 [range.counted]

1 一个计数视图呈现了计数范围（23.3.1）的元素的视图 i + [0, n) 对于迭代器 i 和非负整数 n。

2 名称 views::counted 表示一个定制点对象（16.3.3.3.6）。设 E 和 F 为表达式，设 T 为 decay_t<decltype((E))>，设 D 为 iter_difference_t<T>。如果 decltype((F)) 不建模 convertible_to<D>，则 views::counted(E, F) 为 ill-formed。

[Note 1: 此情况可在 views::counted(E, F) 出现在模板实例化的直接上下文中时导致替换失败。 — 结束说明]

否则，views::counted(E, F) 与以下表达式等价：

- (2.1) — 如果 T 建模 contiguous_iterator，则 span{to_address(E), static_cast<D>(F)}。
- (2.2) — 否则，如果 T 建模 random_access_iterator，则 subrange{E, E + static_cast<D>(F)}，除非 E 仅被求值一次。
- (2.3) — 否则，subrange{counted_iterator{E, F}, default_sentinel}。

## 24.7.14 共同视图 [range.common]

### 24.7.14.1 概述 [range.common.overview]

1 common_view 接受一个其迭代器和哨兵类型不同的视图，并将其转换为具有相同类型迭代器和哨兵的视图。

2 [Note 1: common_view 对于调用期望范围的迭代器和哨兵类型相同的遗留算法很有用。 — 结束说明]

3 名称 views::common 表示一个范围适配器对象（24.7.2）。给定子表达式 E，表达式 views::common(E) 与以下表达式等价：

- (3.1) — views::all(E)，如果 decltype((E)) 建模 common_range 且 views::all(E) 为良构表达式。
- (3.2) — 否则，common_view{E}。

4 [Example 1:

```
// Legacy algorithm:
template<class ForwardIterator>
size_t count(ForwardIterator first, ForwardIterator last);

template<forward_range R>
void my_algo(R&& r) {
    auto&& common = common_view{r};
    auto cnt = count(common.begin(), common.end());
```

