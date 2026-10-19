

constexpr iterator& operator--(difference_type n)
    requires random_access_range<Base>;

13      效果：等价于：
        current_ -= n;
        return *this;

friend constexpr bool operator==(const iterator& x, const iterator& y)
    requires equality_comparable<iterator_t<Base>>;

14      效果：等价于：return x.current_ == y.current_;

friend constexpr bool operator<(const iterator& x, const iterator& y)
    requires random_access_range<Base>;

15      效果：等价于：return x.current_ < y.current_;

friend constexpr bool operator>(const iterator& x, const iterator& y)
    requires random_access_range<Base>;

16      效果：等价于：return y < x;

friend constexpr bool operator<=(const iterator& x, const iterator& y)
    requires random_access_range<Base>;

17      效果：等价于：return !(y < x);

friend constexpr bool operator>=(const iterator& x, const iterator& y)
    requires random_access_range<Base>;

18      效果：等价于：return !(x < y);

friend constexpr auto operator<=>(const iterator& x, const iterator& y)
    requires random_access_range<Base> && three_way_comparable<iterator_t<Base>>;

19      效果：等价于：return x.current_ <=> y.current_;

friend constexpr iterator operator+(iterator i, difference_type n)
    requires random_access_range<Base>;
friend constexpr iterator operator+(difference_type n, iterator i)
    requires random_access_range<Base>;

20      效果：等价于：return iterator{i.parent_, i.current_ + n};

friend constexpr iterator operator-(iterator i, difference_type n)
    requires random_access_range<Base>;

21      效果：等价于：return iterator{i.parent_, i.current_ - n};

friend constexpr difference_type operator-(const iterator& x, const iterator& y)
    requires random_access_range<Base>;

22      效果：等价于：return x.current_ - y.current_;

friend constexpr void iter_swap(const iterator& x, const iterator& y)
    noexcept(noexcept(ranges::iter_swap(x.current_, y.current_)))
    requires indirectly_swappable<iterator_t<Base>>;

23      效果：等价于 ranges::iter_swap(x.current_, y.current_)。

## 24.7.6.4 类模板 transform_view::sentinel [range.transform.sentinel]
namespace std::ranges {
template<input_range V, copy_constructible F>
    requires view<V> && is_object_v<F> &&
            regular_invocable<F&, range_reference_t<V>> &&
            can-reference<invoke_result_t<F&, range_reference_t<V>>>
template<bool Const>
class transform_view<V, F>::sentinel {
private:
    using Parent =
        conditional_t<Const, const transform_view, transform_view>; // exposition only
    conditional_t<Const, const transform_view, transform_view>;
```

## 24.7.6.4 类模板 transform_view::sentinel

using Base = conditional_t<Const, const V, V>;    // exposition only
sentinel_t<Base> end_ = sentinel_t<Base>();    // exposition only
public:
  sentinel() = default;
  constexpr explicit sentinel(sentinel_t<Base> end);
  constexpr sentinel(sentinel<!Const> i)
    requires Const && convertible_to<sentinel_t<V>, sentinel_t<Base>>;

  constexpr sentinel_t<Base> base() const;

  friend constexpr bool operator==(const iterator<Const>& x, const sentinel& y);

  friend constexpr range_difference_t<Base>
    operator-(const iterator<Const>& x, const sentinel& y)
    requires sized_sentinel_for<sentinel_t<Base>, iterator_t<Base>>;
  friend constexpr range_difference_t<Base>
    operator-(const sentinel& y, const iterator<Const>& x)
    requires sized_sentinel_for<sentinel_t<Base>, iterator_t<Base>>;
};
}

constexpr explicit sentinel(sentinel_t<Base> end);

效果：使用 end 初始化 end_。

constexpr sentinel(sentinel<!Const> i)
  requires Const && convertible_to<sentinel_t<V>, sentinel_t<Base>>;

效果：使用 std::move(i.end_) 初始化 end_。

constexpr sentinel_t<Base> base() const;

效果：等价于：return end_;

friend constexpr bool operator==(const iterator<Const>& x, const sentinel& y);

效果：等价于：return x.current_ == y.end_;

friend constexpr range_difference_t<Base>
  operator-(const iterator<Const>& x, const sentinel& y)
  requires sized_sentinel_for<sentinel_t<Base>, iterator_t<Base>>;

效果：等价于：return x.current_ - y.end_;

friend constexpr range_difference_t<Base>
  operator-(const sentinel& y, const iterator<Const>& x)
  requires sized_sentinel_for<sentinel_t<Base>, iterator_t<Base>>;

效果：等价于：return y.end_ - x.current_;

## 24.7.7 Take view [range.take]

### 24.7.7.1 概述 [range.take.overview]

1 take_view 产生另一个 view 的前 N 个元素的视图，如果适配的 view 包含的元素少于 N，则产生所有元素。

2 名称 views::take 表示一个范围适配器对象（24.7.2）。设 E 和 F 为表达式，设 T 为 remove_cvref_t<decltype((E))>，设 D 为 range_difference_t<decltype((E))>。如果 decltype((F)) 不建模 convertible_to<D>，则表达式 views::take(E, F) 为 ill-formed。否则，表达式 views::take(E, F) 与以下表达式等价：

- (2.1) — 如果 T 是 ranges::empty_view（24.6.2.2）的特化，则 ((void) F, decay-copy(E))。
- (2.2) — 否则，如果 T 建模 random_access_range 且 sized_range 且是
  - (2.2.1) — span（22.7.3）的特化，其中 T::extent == dynamic_extent，
  - (2.2.2) — basic_string_view（21.4）的特化，
  - (2.2.3) — ranges::iota_view（24.6.4.2）的特化，或
  - (2.2.4) — ranges::subrange（24.5.4）的特化，

则 T{ranges::begin(E), ranges::begin(E) + min<D>(ranges::size(E), F)}，除非 E 仅被求值一次。
(2.3) — 否则，ranges::take_view{E, F}。

3 [示例 1：

```
vector<int> is{0,1,2,3,4,5,6,7,8,9};
take_view few{is, 5};
for (int i : few)
    cout << i << ' '; // prints: 0 1 2 3 4
— end example
```

## 24.7.7.2 类模板 take_view [range.take.view]

```
namespace std::ranges {
template<view V>
class take_view : public view_interface<take_view<V>> {
private:
    V base_ = V();                                 // exposition only
    range_difference_t<V> count_ = 0;              // exposition only
    // 24.7.7.3, class template take_view::sentinel
    template<bool> struct sentinel;                // exposition only
public:
    take_view() = default;
    constexpr take_view(V base, range_difference_t<V> count);

    constexpr V base() const& requires copy_constructible<V> { return base_; }
    constexpr V base() && { return std::move(base_); }

    constexpr auto begin() requires (!simple-view<V>) {
        if constexpr (sized_range<V>) {
            if constexpr (random_access_range<V>)
                return ranges::begin(base_);
            else {
                auto sz = size();
                return counted_iterator{ranges::begin(base_), sz};
            }
        } else
            return counted_iterator{ranges::begin(base_), count_};
    }

    constexpr auto begin() const requires range<const V> {
        if constexpr (sized_range<const V>) {
            if constexpr (random_access_range<const V>)
                return ranges::begin(base_);
            else {
                auto sz = size();
                return counted_iterator{ranges::begin(base_), sz};
            }
        } else
            return counted_iterator{ranges::begin(base_), count_};
    }

    constexpr auto end() requires (!simple-view<V>) {
        if constexpr (sized_range<V>) {
            if constexpr (random_access_range<V>)
                return ranges::begin(base_) + size();
            else
                return default_sentinel;
        } else
            return sentinel<false>{ranges::end(base_)};
    }
}
```

## 24.7.8 Take while view [range.take.while]

### 24.7.8.1 概述 [range.take.while.overview]

1 给定一元谓词 pred 和一个 view r，take_while_view 产生范围 [begin(r), ranges::find_if_not(r, pred)) 的视图。

2 名称 views::take_while 表示一个范围适配器对象（24.7.2）。给定子表达式 E 和 F，表达式 views::take_while(E, F) 与 take_while_view<E, F> 表达式等价。

3 [示例 1：

```
auto input = istringstream{"0 1 2 3 4 5 6 7 8 9"};
auto small = [](const auto x) noexcept { return x < 5; };
auto small_ints = istream_view<int>(input) | views::take_while(small);
for (const auto i : small_ints) {
    cout << i << ' ';
}
auto i = 0;
input >> i;
cout << i;
// prints 0 1 2 3 4
// prints 6
```

— end example]

## 24.7.8.2 类模板 take_while_view [range.take.while.view]

```
namespace std::ranges {
template<view V, class Pred>
    requires input_range<V> && is_object_v<Pred> &&
            indirect_unary_predicate<const Pred, iterator_t<V>>
class take_while_view : public view_interface<take_while_view<V, Pred>> {
    // 24.7.8.3, class template take_while_view::sentinel
    template<bool> class sentinel; // exposition only
    V base_(); // exposition only
    semiregular-box<Pred> pred_; // exposition only
public:
    take_while_view() = default;
    constexpr take_while_view(V base, Pred pred);
    constexpr V base() const& requires copy_constructible<V> { return base_; }
    constexpr V base() && { return std::move(base_); }
    constexpr const Pred& pred() const;
    constexpr auto begin() requires (!simple-view<V>)
    { return ranges::begin(base_); }
    constexpr auto begin() const requires range<const V>
    { return ranges::begin(base_); }
    constexpr auto end() requires (!simple-view<V>)
    { return sentinel<false>(ranges::end(base_), addressof(*pred_)); }
    constexpr auto end() const requires range<const V>
    { return sentinel<true>(ranges::end(base_), addressof(*pred_)); }
};
template<class R, class Pred>
    take_while_view(R&&, Pred) -> take_while_view<views::all_t<R>, Pred>;
constexpr take_while_view(V base, Pred pred);
```

1 效果：使用 std::move(base) 初始化 base_，并使用 std::move(pred) 初始化 pred_。

constexpr const Pred& pred() const;

2 效果：等价于：return *pred_;

