

# ISO/IEC 14882:2020(E)

(2.2) — 否则，如果 T 是数组类型（6.8.3）且 remove_all_extents_t<T> 是不完整类型，则 ranges::rend(E) 是格式错误，无需诊断。

(2.3) — 否则，如果 decay-copy(t.rend()) 是有效表达式，其类型建模 sentinel_for<decltype(ranges::rbegin(E))>，则 ranges::rend(E) 与 decay-copy(t.rend()) 表达式等价。

(2.4) — 否则，如果 T 是类或枚举类型，且 decay-copy(rend(t)) 是有效表达式，其类型建模 sentinel_for<decltype(ranges::rbegin(E))>，重载决议在仅找到以下声明的无限定查找上下文中进行
void rend(auto&) = delete;
void rend(const auto&) = delete;
则 ranges::rend(E) 与在上述上下文中进行重载决议的 decay-copy(rend(t)) 表达式等价。

(2.5) — 否则，如果 ranges::begin(t) 和 ranges::end(t) 都是相同类型的有效表达式，且该类型建模 bidirectional_iterator（23.3.4.12），则 ranges::rend(E) 与 make_reverse_iterator(ranges::begin(t)) 表达式等价。

(2.6) — 否则，ranges::rend(E) 是格式错误的。

3 [注 1：上述可诊断的格式错误情况在 ranges::rend(E) 出现在模板实例化的直接上下文中时会导致替换失败。——注结束]

4 [注 2：每当 ranges::rend(E) 是有效表达式时，表达式 ranges::rend(E) 和 ranges::rbegin(E) 的类型 S 和 I 建模 sentinel_for<S, I>。——注结束]

# 24.3.8 ranges::crbegin [range.access.crbegin]

1 名称 ranges::crbegin 表示一个定制点对象（16.3.3.3.6）。对于类型为 T 的子表达式 E，表达式 ranges::crbegin(E) 表达式等价于：

+   (1.1) — 如果 E 是左值，则 ranges::rbegin(static_cast<const T&>(E))。
+   (1.2) — 否则，ranges::rbegin(static_cast<const T&&>(E))。

2 [注 1：每当 ranges::crbegin(E) 是有效表达式时，其类型建模 input_or_output_iterator。——注结束]

# 24.3.9 ranges::crend [range.access.crend]

1 名称 ranges::crend 表示一个定制点对象（16.3.3.3.6）。对于类型为 T 的子表达式 E，表达式 ranges::crend(E) 表达式等价于：

+   (1.1) — 如果 E 是左值，则 ranges::rend(static_cast<const T&>(E))。
+   (1.2) — 否则，ranges::rend(static_cast<const T&&>(E))。

2 [注 1：每当 ranges::crend(E) 是有效表达式时，表达式 ranges::crend(E) 和 ranges::crbegin(E) 的类型 S 和 I 建模 sentinel_for<S, I>。——注结束]

# 24.3.10 ranges::size [range.prim.size]

1 名称 ranges::size 表示一个定制点对象（16.3.3.3.6）。

2 给定类型为 T 的子表达式 E，令 t 为表示 E 的实化对象的左值。则：

+   (2.1) — 如果 T 是未知界限的数组（9.3.4.5），则 ranges::size(E) 是格式错误的。
+   (2.2) — 否则，如果 T 是数组类型，则 ranges::size(E) 表达式等价于 decay-copy(extent_v<T>)。
+   (2.3) — 否则，如果 disable_sized_range<remove_cv_t<T>>（24.4.3）为 false 且 decay-copy(t.size()) 是整数型（23.3.4.4）的有效表达式，则 ranges::size(E) 表达式等价于 decay-copy(t.size())。
+   (2.4) — 否则，如果 T 是类或枚举类型，disable_sized_range<remove_cv_t<T>> 为 false 且 decay-copy(size(t)) 是整数型的有效表达式，重载决议在仅找到以下声明的无限定查找上下文中进行
+   void size(auto&) = delete;
+   void size(const auto&) = delete;

# 24.3.14 ranges::cdata [range.prim.cdata]

1 名称 ranges::cdata 表示一个定制点对象（16.3.3.3.6）。对于类型为 T 的子表达式 E，表达式 ranges::cdata(E) 表达式等价于：

+   - 如果 E 是左值，则 ranges::data(static_cast<const T&>(E))。
+   - 否则，ranges::data(static_cast<const T&&>(E))。

2 [注 1：每当 ranges::cdata(E) 是有效表达式时，它具有指向对象的指针类型。——注结束]

# 24.4 Range requirements [range.req]

# 24.4.1 General [range.req.general]

1 范围是一个抽象，允许 C++ 程序以统一的方式对数据结构的元素进行操作。对范围调用 ranges::begin 返回一个其类型建模 input_or_output_iterator（23.3.4.6）的对象。对范围调用 ranges::end 返回一个其类型为 S 的对象，该类型与 ranges::begin 返回的对象类型 I 一起建模 sentinel_for<S, I>。库将范围的接口、语义和复杂度形式化，以便算法和范围适配器能够高效地在不同类型的序列上工作。

2 range 概念要求 ranges::begin 和 ranges::end 分别返回迭代器和哨兵。sized_range 概念以 ranges::size 为摊销 O(1) 的要求细化 range。view 概念指定了具有常数时间析构和移动操作的范围类型的要求。

3 若干 range 的细化在概念和算法中经常出现。常见范围是指 ranges::begin 和 ranges::end 返回相同类型对象的范围。随机访问范围是指 ranges::begin 返回建模 random_access_iterator（23.3.4.13）的类型的范围。（连续、双向、前向、输入和输出范围类似定义。）可视图范围可以转换为视图。

# 24.4.2 Ranges [range.range]

1 range 概念定义了允许通过提供迭代器和哨兵来遍历其元素的类型的要求。

```
template<class T>
  concept range =
    requires(T& t) {
      ranges::begin(t);
      ranges::end(t);
    };
// sometimes equality-preserving (see below)
```

2 range 概念的必需表达式 ranges::begin(t) 和 ranges::end(t) 不要求隐式表达式变体（18.2）。

3 给定表达式 t 使得 decltype((t)) 为 T&，仅当

+   (3.1) — [ranges::begin(t), ranges::end(t)) 表示一个范围（23.3.1），
+   (3.2) — ranges::begin(t) 和 ranges::end(t) 均为摊销常数时间和非修改的，且
+   (3.3) — 如果 ranges::begin(t) 的类型建模 forward_iterator，则 ranges::begin(t) 是相等保持的。

T 才建模 range。

4 [注 1：ranges::begin 和 ranges::end 的相等保持性使得可以将迭代器类型建模 forward_iterator 的范围传递给多个算法，并通过对 ranges::begin 和 ranges::end 的重复调用对范围进行多次遍历。由于当返回类型不建模 forward_iterator 时 ranges::begin 不要求相等保持，因此重复调用可能不返回相等的值或不被定义。——注结束]

```
template<class T>
  concept borrowed_range =
    range<T> &&
    (is_lvalue_reference_v<T> || enable_borrowed_range<remove_cvref_t<T>>);
```

5 给定表达式 E 使得 decltype((E)) 为 T，仅当从 E 所表示的对象获得的迭代器的有效性与该对象的生命周期无关时，T 才建模 borrowed_range。

# ISO/IEC 14882:2020(E)

[注 2：由于从建模 borrowed_range 的类型的对象获得的迭代器的有效性与对象的生命周期无关，因此函数可以按值接受此类类型的参数并返回从中获得的迭代器，而不会有悬空的危险。——注结束]

```
template<class>
    inline constexpr bool enable_borrowed_range = false;
```

说明：根据 16.4.5.2.1，用户可以为 cv 无限定程序定义类型特化 enable_borrowed_range。此类特化应可在常量表达式（7.7）中使用且类型为 const bool。

[示例 1：类模板 subrange（24.5.4）的每个特化 S 都建模 borrowed_range，因为

+   - enable_borrowed_range<S> 被特化为具有值 true，且
+   - S 的迭代器的有效性与 S 对象的生命周期无关，因为它们是从其他范围“借用”的。

——示例结束]

# 24.4.3 Sized ranges [range.sized]

1 sized_range 概念以使用 ranges::size 在摊销常数时间内确定范围中元素数量的要求细化 range。

```
template<class T>
concept sized_range =
    range<T> &&
    requires(T& t) { ranges::size(t); };
```

2 给定类型为 remove_reference_t<T> 的左值 t，仅当

+   (2.1) ranges::size(t) 为摊销 O(1)、不修改 t 且等于 ranges::distance(t)，且
+   (2.2) 如果 iterator_t<T> 建模 forward_iterator，则 ranges::size(t) 在 ranges::begin(t) 的求值与否下均是良定义的。

T 才建模 sized_range。

[注 1：ranges::size(t) 否则不要求在求值 ranges::begin(t) 之后仍是良定义的。例如，对于迭代器类型不建模 forward_iterator 的 sized_range，ranges::size(t) 可能仅在第一次调用 ranges::begin(t) 之前求值时才为良定义。——注结束]

```
template<class>
    inline constexpr bool disable_sized_range = false;
```

3 说明：根据 16.4.5.2.1，用户可以为 cv 无限定程序定义类型特化 disable_sized_range。此类特化应可在常量表达式（7.7）中使用且类型为 const bool。

4 [注 2：disable_sized_range 允许使用满足但实际上不建模 sized_range 的范围类型于库中。——注结束]

# 24.4.4 Views [range.view]

1 view 概念指定了范围类型的要求，该类型具有常数时间移动构造、移动赋值和析构；即这些操作的成本与视图中的元素数量无关。

```
template<class T>
concept view =
    range<T> && movable<T> && default_initializable<T> && enable_view<T>;
```

2 T 仅在以下情况下建模 view：

+   (2.1) T 具有 O(1) 移动构造；且
+   (2.2) T 具有 O(1) 移动赋值；且
+   (2.3) T 具有 O(1) 析构；且
+   (2.4) copy_constructible<T> 为 false，或 T 具有 O(1) 拷贝构造；且
+   (2.5) copyable<T> 为 false，或 T 具有 O(1) 拷贝赋值。

