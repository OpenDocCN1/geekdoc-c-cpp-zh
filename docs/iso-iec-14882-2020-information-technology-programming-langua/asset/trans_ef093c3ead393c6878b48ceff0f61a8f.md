

(4.2) — 它建模 contiguous_iterator。

(4.3) — 如果 extent 不等于 dynamic_extent，则 count 等于 extent。

5 效果：使用 to_address(first) 初始化 data_，并使用 count 初始化 size_。

6 抛出：无。

```
template<class It, class End>
    constexpr explicit(extent != dynamic_extent) span(It first, End last);
```

7 约束：令 U 为 remove_reference_t<iter_reference_t<It>>。

+   (7.1) — is_convertible_v<U(*)[], element_type(*)[ ]> 为 true。
+   [Note 2: 其意图是仅允许迭代器引用类型到 element_type 的限定转换。
+   — end note]

(7.2) — 它满足 contiguous_iterator。

(7.3) — End 满足 sized_sentinel_for<It>。

(7.4) — is_convertible_v<End, size_t> 为 false。

8 前提条件：

+   (8.1) — 如果 extent 不等于 dynamic_extent，则 last - first 等于 extent。
+   (8.2) — [first, last) 是一个有效范围。
+   (8.3) — 它建模 contiguous_iterator。
+   (8.4) — End 建模 sized_sentinel_for<It>。

9 效果：使用 to_address(first) 初始化 data_，并使用 last - first 初始化 size_。

10 抛出：当且仅当 last - first 抛出时抛出。

```
template<size_t N> constexpr span(type_identity_t<element_type> (&arr)[N]) noexcept;
template<class T, size_t N> constexpr span(array<T, N>& arr) noexcept;
template<class T, size_t N> constexpr span(const array<T, N>& arr) noexcept;
```

11 约束：令 U 为 remove_pointer_t<decltype(data(arr))>。

+   (11.1) — extent == dynamic_extent || N == extent 为 true，且
+   (11.2) — is_convertible_v<U(*)[], element_type(*)[ ]> 为 true。
+   [Note 3: 其意图是仅允许数组元素类型到 element_type 的限定转换。
+   — end note]

12 效果：构造一个对所提供数组的视图的 span。

[Note 4: type_identity_t 影响类模板参数推导。 — end note]

13 后置条件：size() == N && data() == data(arr) 为 true。

```
template<class R> constexpr explicit(extent != dynamic_extent) span(R&& r);
```

14 约束：令 U 为 remove_reference_t<ranges::range_reference_t<R>>。

+   (14.1) — R 满足 ranges::contiguous_range 和 ranges::sized_range。
+   (14.2) — 要么 R 满足 ranges::borrowed_range 要么 is_const_v<element_type> 为 true。
+   (14.3) — remove_cvref_t<R> 不是 span 的特化。
+   (14.4) — remove_cvref_t<R> 不是 array 的特化。
+   (14.5) — is_array_v<remove_cvref_t<R>> 为 false。
+   (14.6) — is_convertible_v<U(*)[], element_type(*)[ ]> 为 true。
+   [Note 5: 其意图是仅允许范围引用类型到 element_type 的限定转换。
+   — end note]

15 前提条件：

+   (15.1) — 如果 extent 不等于 dynamic_extent，则 ranges::size(r) 等于 extent。
+   (15.2) — R 建模 ranges::contiguous_range 和 ranges::sized_range。
+   (15.3) — 如果 is_const_v<element_type> 为 false，则 R 建模 ranges::borrowed_range。

// 23.3.4.13, concept random_access_iterator
template<class I>
    concept random_access_iterator = see below;

// 23.3.4.14, concept contiguous_iterator
template<class I>
    concept contiguous_iterator = see below;

// 23.3.6, indirect callable requirements
// 23.3.6.2, indirect callables
template<class F, class I>
    concept indirectly_unary_invocable = see below;

template<class F, class I>
    concept indirectly_regular_unary_invocable = see below;

template<class F, class I>
    concept indirect_unary_predicate = see below;

template<class F, class I1, class I2>
    concept indirect_binary_predicate = see below;

template<class F, class I1, class I2 = I1>
    concept indirect_equivalence_relation = see below;

template<class F, class I1, class I2 = I1>
    concept indirect_strict_weak_order = see below;

template<class F, class... Is>
    requires (indirectly_readable<Is> && ...) && invocable<F, iter_reference_t<Is>...>
    using indirect_result_t = invoke_result_t<F, iter_reference_t<Is>...>;

// 23.3.6.3, projected
template<indirectly_readable I, indirectly_regular_unary_invocable<I> Proj>
    struct projected;

template<weakly_incrementable I, class Proj>
    struct incrementable_traits<projected<I, Proj>>;

// 23.3.7, common algorithm requirements
// 23.3.7.2, concept indirectly_movable
template<class In, class Out>
    concept indirectly_movable = see below;

template<class In, class Out>
    concept indirectly_movable_storable = see below;

// 23.3.7.3, concept indirectly_copyable
template<class In, class Out>
    concept indirectly_copyable = see below;

template<class In, class Out>
    concept indirectly_copyable_storable = see below;

// 23.3.7.4, concept indirectly_swappable
template<class I1, class I2 = I1>
    concept indirectly_swappable = see below;

// 23.3.7.5, concept indirectly_comparable
template<class I1, class I2, class R, class P1 = identity, class P2 = identity>
    concept indirectly_comparable = see below;

template<class I>
    struct incrementable_traits<counted_iterator<I>>;

template<input_iterator I>
    struct iterator_traits<counted_iterator<I>>;

// 23.5.7, unreachable sentinel
struct unreachable_sentinel_t;
inline constexpr unreachable_sentinel_t unreachable_sentinel{};

// 23.6, stream iterators
template<class T, class charT = char, class traits = char_traits<charT>,
        class Distance = ptrdiff_t>
class istream_iterator;
template<class T, class charT, class traits, class Distance>
    bool operator==(const istream_iterator<T,charT,traits,Distance>& x,
                    const istream_iterator<T,charT,traits,Distance>& y);

template<class T, class charT = char, class traits = char_traits<charT>>
    class ostream_iterator;

template<class charT, class traits = char_traits<charT>>
    class istreambuf_iterator;
template<class charT, class traits>
    bool operator==(const istreambuf_iterator<charT,traits>& a,
                    const istreambuf_iterator<charT,traits>& b);

template<class charT, class traits = char_traits<charT>>
    class ostreambuf_iterator;

// 23.7, range access
template<class C> constexpr auto begin(C& c) -> decltype(c.begin());
template<class C> constexpr auto begin(const C& c) -> decltype(c.begin());
template<class C> constexpr auto end(C& c) -> decltype(c.end());
template<class C> constexpr auto end(const C& c) -> decltype(c.end());
template<class T, size_t N> constexpr T* begin(T (&array)[N]) noexcept;
template<class T, size_t N> constexpr T* end(T (&array)[N]) noexcept;
template<class C> constexpr auto cbegin(const C& c) noexcept(noexcept(std::begin(c)))
    -> decltype(std::begin(c));
template<class C> constexpr auto cend(const C& c) noexcept(noexcept(std::end(c)))
    -> decltype(std::end(c));

template<class C> constexpr auto rbegin(C& c) -> decltype(c.rbegin());
template<class C> constexpr auto rbegin(const C& c) -> decltype(c.rbegin());
template<class C> constexpr auto rend(C& c) -> decltype(c.rend());
template<class C> constexpr auto rend(const C& c) -> decltype(c.rend());
template<class T, size_t N> constexpr reverse_iterator<T*> rbegin(T (&array)[N]);
template<class T, size_t N> constexpr reverse_iterator<T*> rend(T (&array)[N]);
template<class E> constexpr reverse_iterator<const E*> rbegin(initializer_list<E> il);
template<class E> constexpr reverse_iterator<const E*> rend(initializer_list<E> il);
template<class C> constexpr auto crbegin(const C& c) -> decltype(std::rbegin(c));
template<class C> constexpr auto crend(const C& c) -> decltype(std::rend(c));

template<class C> constexpr auto size(const C& c) -> decltype(c.size());
template<class T, size_t N> constexpr size_t size(const T (&array)[N]) noexcept;
template<class C> constexpr auto ssize(const C& c)
    -> common_type_t<ptrdiff_t, make_signed_t<decltype(c.size())>>;
template<class T, ptrdiff_t N> constexpr ptrdiff_t ssize(const T (&array)[N]) noexcept;

template<class C> [[nodiscard]] constexpr auto empty(const C& c) -> decltype(c.empty());
template<class T, size_t N> [[nodiscard]] constexpr bool empty(const T (&array)[N]) noexcept;
template<class E> [[nodiscard]] constexpr bool empty(initializer_list<E> il) noexcept;

