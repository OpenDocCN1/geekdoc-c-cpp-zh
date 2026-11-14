

## 5.4.6.3 在嵌套类对象上进行归约

=> c++03/reduction_unroll_nesting_example.cpp

为避免使用数组，我们可以为 n 个临时变量定义一个类，其中 n 是模板参数。这样，类的设计更符合函子的递归方案：

```cpp
template <unsigned BSize, typename Value>
struct multi_tmp
{
  typedef multi_tmp<BSize-1, Value> sub_type;

  multi_tmp(const Value& v) : value(v), sub(v) {}

  Value value;
  sub_type sub;
};
```

```cpp
template <typename Value>
struct multi_tmp<0, Value>
{
  multi_tmp(const Value& v) {}
};
```

此类对象可以递归初始化，因此不需要像数组那样使用循环。函子可以操作 value 成员，并将 sub 成员的引用传递给其后继者。这引出了我们函子的实现：

```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
  template <typename S, typename V>
  void operator()(S& sum, const V& v, unsigned i)
  {
    using std::abs;
    sum.value += abs(v(i + Offset));
    one_norm_ftor<Offset + 1, Max>()(sum.sub, v, i);
  }
};

template <unsigned Max>
struct one_norm_ftor<Max, Max>
{
  template <typename S, typename V>
  void operator()(S& sum, const V& v, unsigned i) {}
};
```

使用此函子的展开函数如下：

```cpp
template <unsigned BSize, typename Value>
typename Vector::value_type
inline one_norm(const Vector& v)
{
    using std::abs;
    typedef typename Vector::value_type value_type;
    multi_tmp<BSize, value_type> multi_sum(0);
    unsigned s = size(v), sb = s / BSize * BSize;
    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>()(multi_sum, v, i);
    value_type sum = multi_sum.sum();
    for (unsigned i = sb; i < s; ++i)
        sum += abs(v[i]);
    return sum;
}
```

还缺少一部分：我们必须在最后对 `multi_sum` 中的部分和进行归约。不幸的是，我们无法对 `multi_sum` 的成员编写循环。因此，我们需要一个递归函数来深入 `multi_sum`，最简单的方法是将其实现为带有相应特化的成员函数：

```cpp
template <unsigned BSize, typename Value>
struct multi_tmp
{
    Value sum() const { return value + sub.sum(); }
};
```

请注意，我们是从空的 `multi_tmp` 开始求和，而不是从最内层的 value 成员开始。否则，我们需要为 `multi_tmp<1, Value>` 额外编写一个特化。同样，我们可以像 `accumulate` 那样实现一般归约，但这需要存在一个初始元素：

```cpp
template <unsigned BSize, typename Value>
struct multi_tmp
{
    template <typename Op>
    Value reduce(Op op, const Value& init) const
    { return op(value, sub.reduce(op, init)); }
};

template <typename Value>
struct multi_tmp<0, Value>
{
    template <typename Op>
    Value reduce(Op op, const Value& init) const { return init; }
};
```

此版本的计算时间如下

| 实现 | 时间 |
|---|---|
| one_norm<1>(v) | 0.786668 µs |
| one_norm<2>(v) | 0.442476 µs |
| one_norm<4>(v) | 0.441455 µs |
| one_norm<6>(v) | 0.410978 µs |
| one_norm<8>(v) | 0.426368 µs |

因此，在我们的测试环境中，不同实现的性能相似。

## 5.4.6.4 应对抽象惩罚

=> c++03/reduction_unroll_registers_example.cpp

在前面的章节中，我们引入了临时变量以实现更多独立操作。然而，这些临时变量只有在被分配到寄存器时才有益处。否则，由于额外的内存流量和缓存失效信号，它们甚至可能减慢整个执行速度。在某些旧编译器中，数组和嵌套类位于主内存中，展开代码的运行时间甚至比顺序代码更长。

这是抽象惩罚的典型示例：语义等价的程序由于采用更抽象的表述而运行得更慢。为了量化抽象惩罚，Alex Stepanov 在 20 世纪 90 年代初编写了一个基准测试，用于测量包装类对 accumulate 函数性能的影响 [40]。其思想是，能够以相同速度运行所有测试版本的编译器应该能够在不产生额外开销的情况下执行 STL 算法。

当时，可以观察到更抽象代码存在显著开销，而现代编译器可以轻松处理该基准测试中的抽象。但这并不意味着它们能处理每一层抽象，我们始终需要检查性能关键型内核是否可以通过不那么抽象的实现来运行得更快。例如，在 MTL4 中，矩阵向量积以迭代器风格为所有矩阵类型和视图进行泛型实现。该操作针对重要的矩阵类进行了特化，并针对这些数据结构进行了调优，部分使用了原始指针。泛型高性能软件需要在泛型可重用性和针对性调优之间取得良好平衡，一方面避免可感知的开销，另一方面避免组合式代码爆炸。

在我们特殊的寄存器使用情况中，我们可以尝试通过将复杂性从数据结构中转移出来来帮助编译器优化。我们最好的机会是将它们存储在寄存器中，方法是将其声明为函数局部变量：

```cpp
inline one_norm(const Vector& v)
{
    typename Vector::value_type s0(0), s1(0), s2(0), ...
}
```

现在的问题是我们应该声明多少个。数量不能依赖于模板参数，而必须对所有块大小固定。此外，临时变量的数量限制了我们展开循环的能力。

## 5.4 元调优：编写你自己的编译器优化

迭代块中实际使用的临时变量数量取决于模板参数 BSize。不幸的是，我们无法根据模板参数更改函数调用中的参数数量，即，对于较小的 BSize 值传递更少的参数。因此，我们必须将所有变量传递给迭代块函子：

```cpp
for (unsigned i = 0; i < sb; i += BSize)
    one_norm_ftor<0, BSize>()(s0, s1, s2, s3, s4, s5, s6, s7, v, i);
```

每个块中的第一个计算在 s0 上累积，第二个在 s1 上累积，依此类推。不幸的是，我们无法根据参数选择临时变量（除非为每个值进行特化）。

或者，每个计算都在其第一个函数参数上执行，后续函子在不带第一个参数的情况下被调用：

```cpp
one_norm_ftor<1, BSize>()(s1, s2, s3, s4, s5, s6, s7, v, i);
one_norm_ftor<2, BSize>()(s2, s3, s4, s5, s6, s7, v, i);
one_norm_ftor<3, BSize>()(s3, s4, s5, s6, s7, v, i);
```

这也无法通过模板实现。

解决方案是旋转引用：

```cpp
one_norm_ftor<1, BSize>()(s1, s2, s3, s4, s5, s6, s7, s0, v, i);
one_norm_ftor<2, BSize>()(s2, s3, s4, s5, s6, s7, s0, s1, v, i);
one_norm_ftor<3, BSize>()(s3, s4, s5, s6, s7, s0, s1, s2, v, i);
```

此旋转通过以下函子实现来完成：

```cpp
template <unsigned Offset, unsigned Max>
struct one_norm_ftor
{
    template <typename S, typename V>
    void operator()(S& s0, S& s1, S& s2, S& s3, S& s4, S& s5, S& s6,
                    S& s7, const V& v, unsigned i)
    {
        using std::abs;
        s0 += abs(v[i + Offset]);
        one_norm_ftor<Offset + 1, Max>()(s1, s2, s3, s4, s5, s6, s7,
                                        s0, v, i);
    }
};

template <unsigned Max>
struct one_norm_ftor<Max, Max>
{
    template <typename S, typename V>
    void operator()(S& s0, S& s1, S& s2, S& s3, S& s4, S& s5, S& s6,
                    S& s7, const V& v, unsigned i) {}
};
```

基于此函子的相应 one_norm 函数很简单：

```cpp
template <unsigned BSize, typename Vector>
typename Vector::value_type
inline one_norm(const Vector& v)
{
    using std::abs;
    typename Vector::value_type s0(0), s1(0), s2(0), s3(0), s4(0),
        s5(0), s6(0), s7(0);
    unsigned s = size(v), sb = s / BSize * BSize;
    for (unsigned i = 0; i < sb; i += BSize)
        one_norm_ftor<0, BSize>()(s0, s1, s2, s3, s4, s5, s6, s7, v, i);
    s0 += s1 + s2 + s3 + s4 + s5 + s6 + s7;
    for (unsigned i = sb; i < s; ++i)
        s0 += abs(v[i]);
    return s0;
}
```

一个小缺点是对于非常小的向量存在开销：即使没有块迭代，所有寄存器也必须在块迭代后累积。另一方面，一个巨大的优势是，旋转允许块大小大于临时变量的数量。它们被重复使用而不会损坏结果。尽管如此，实际并发性不会更大。

此实现的执行在测试机上耗时如下

| 实现 | 时间 |
|---|---|
| one_norm<1>(vs) | 0.793497 µs |
| one_norm<2>(vs) | 0.508242 µs |
| one_norm<4>(vs) | 0.443954 µs |
| one_norm<6>(vs) | 0.441819 µs |
| one_norm<8>(vs) | 0.438749 µs |

这种性能与嵌套类实现相当，适用于能够正确处理后者（即，数据成员在寄存器中）的编译器；否则，旋转代码明显更快。

## 5.4.7 调优嵌套循环

=> c++11/matrix_unroll_example.cpp

性能讨论中最常用（也最被滥用）的示例是稠密矩阵乘法。我们不声称能与手工调优的汇编代码竞争，但我们展示了元编程的强大之处，即从单一实现生成代码变体。作为起点，我们使用第 A.4.3 节中的矩阵模板实现。在以下内容中，我们使用这个简单的测试用例：

```cpp
const unsigned s = 128; // s = 4 in testing, 128 in timing
matrix<float> A(s, s), B(s, s), C(s, s);
for (unsigned i = 0; i < s; ++i)
    for (unsigned j = 0; j < s; j++) {
        A(i, j) = 100.0 * i + j;
        B(i, j) = 200.0 * i + j;
    }
mult(A, B, C);
```

