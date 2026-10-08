

```cpp
{ x != };
{ x = (x = y) };
```

在编写模板时，我们需要对类型进行分类。

| 对象概念 <concepts> | |
| --- | --- |
| destructible<T> | T 可以被销毁，并可以使用一元运算符 & 获取其地址 |
| constructible_from<T,Args> | T 可以从类型为 Args 的参数列表构造 |
| default_initializable<T> | T 可以被默认构造 |
| move_constructible<T> | T 可以被移动构造 |
| copy_constructible<T> | T 可以被拷贝构造和移动构造 |
| movable<T> | 符合 move_constructible<T>, assignable<T&> 和 swapable<T> |
| copyable<T> | 符合 copy_constructible<T>, movable<T> 和 assignable<T, const T&> |
| semiregular<T> | 符合 copyable<T> 和 default_constructible<T> |
| regular<T> | 符合 semiregular<T> 和 equality_comparable<T> |

类型的理想状态是 `regular`。普通类型的工作方式类似于 `int`，并简化了我们关于如何使用类型的大部分思考。尽管大多数类刚开始都是 `semiregular` 且缺乏默认的 `==`，但大多数类可以并且应该是 `regular`。

当我们作为受约束的模板模板执行操作时，我们需要指定它是如何调用的，以及我们对其语义提出了哪些其他假设。

| 可调用概念 <concepts> | |
| --- | --- |
| invocable<F,Args> | F 可以用类型为 Args 的参数列表进行调用 |
| regular_invocable<F,Args> | 符合 invocable<F,Args> 且保持等价性 |
| predicate<F,T> | 返回 bool 的 regular_invocable<F,Args> |
| relation<F,T,U> | 提供等价关系的 relation<F,T,U> |
| strict_weak_order<F,T,U> | 提供严格弱序的 relation<F,T,U> |

如果 $x==y$ 意味着 $f(x)==f(y)$，则函数 $f$ 是保持等价的。`Invocable` 和 `regular_invocable` 仅在语义上不同。我们（目前）无法仅表达我们的意图。

同样，`relation` 和 `equivalence_relation` 仅在语义上不同。等价关系具有自反性、对称性和传递性。

`relation` 和 `strict_weak_order` 仅在语义上不同。严格弱序是标准库比较时假设的，例如 `<`。

## 14.5.2 迭代器概念

传统的标准算法通过迭代器访问数据，因此我们需要概念来对迭代器类型的属性进行分类。

| | |
| --- | --- |
| input_or_output_iterator | I 可以被增加 (++) 和解引用 (*) |
| sentinel_for<S,I> | S 是某类迭代器类型的哨兵（sentinel）；也就是说，S 是在 I 的值类型上的谓词 |
| sized_sentinel_for<S,I> | 一种哨兵 S，其中 - 运算符可以应用于 I |
| input_iterator<I> | I 是输入迭代器；* 仅用于读取 |
| output_iterator<I> | I 是输出迭代器；仅用于写入 |
| forward_iterator<I> | I 是前向迭代器，支持多次访问和 == |
| bidirectional_iterator<I> | 支持 -- 的双向迭代器 |
| random_access_iterator<I> | 支持 +, +=, -, 和 [] 的双向迭代器 |
| contiguous_iterator<I> | 针对连续内存中元素的随机迭代器 |
| permutable_iterator<I> | 支持移动和交换的前向迭代器 |
| mergeable<I,I2,R,O> | 可以合并由 I 和 I2 定义的序列 |
| sortable<I> | 可以对 I 定义序列排序 |
| sortable<I,R> | 可以对 I 定义序列排序 |

对于 S 哨兵（sentinel），其中 - 运算符可以应用于 I。

最后，我们可以尝试编写一个关于 `Sentinel` 的类来满足 `Sentinel` 概念。这里有一个一个 `Sentinel` 类的示例：

```cpp
template<class Iter>
class Sentinel {
public:
    Sentinel(int ee) : end(ee) {}
    Sentinel() {}
    friend bool operator==(const Iter& p, const Sentinel& s) { return p == s.end; }
    friend bool operator!=(const Iter& p, const Sentinel& s) { return !(p == s.end); }
private:
    Iter end;
};
```

是的，我们可以写出“Hello, World!”的程序：

```cpp
const char aa[] = "Hello, World!\n";
ranges::for_each(aa, [](const char x) { cout << x; });
```

是的，这会输出 Hello, World! 并不换行。

## 14.5.3 范围概念

范围（range）概念定义了范围的属性。

| 范围概念 | |
|--- | --- |
| range<R> | R 是迭代器和哨兵的范围 |
| sized_range<R> | R 是知道大小的范围 |
| view<R> | R 是具有常数时间移动和赋值的范围 |
| common_range<R> | R 是迭代器和哨兵类型相同的范围 |
| input_range<R> | R 是迭代器和哨兵的范围 |
| output_range<R> | R 是迭代器和哨兵的范围 |
| forward_range<R> | R 是支持多次访问的范围 |
| bidirectional_range<R> | R 是支持双向遍历的范围 |
| random_access_range<R> | R 是支持随机访问的范围 |
| contiguous_range<R> | R 是在连续内存中的范围 |

在 `<ranges>` 中有一些概念，但这是一个很好的开始。

# 15 指针与容器

> 教育是关于做什么、何时做以及为什么做。
> 培训是关于如何做。
– Richard Hamming

- 引言
- 指针
    - unique_ptr 和 shared_ptr; span
- 容器
    - array; bitset; pair; tuple
- 替代方案
    - variant; optional; any
- 建议

## 15.1 引言

C++ 提供了简单的内置底层类型来持有和引用数据：对象和数组持有数据；指针和数组引用此类数据。然而，我们需要支持更专门和更通用的数据持有和使用方式。例如，标准库容器（第12章）和迭代器（$13.3）是为了通用算法设计的。
容器和指针抽象的共同点在于，要正确且高效地使用它们，需要封装数据以及一组访问和操作它们的函数。例如，指针是非常通用且高效的机器地址抽象，但正确地使用它们表示所有权已被证明是

