
| `v=iota_view(x,y)` | `v` 是包含 `n` 个元素的范围：`x`, `x+1`, ..., `y-1` 使用 `++` 进行递增 |
| `v=istream_view<T>(is)` | `v` 是通过对 `is` 调用 `>>` 到 `T` 获取的范围 |

`Iota` 视图用于生成简单的序列非常有用。例如：

点击此处查看代码图像

```cpp
for (int x : iota_view<int>(42)) 
  cout << x;
```

`istream_view` 提供了一个在范围循环中使用 `istream` 的简单示例：

点击此处查看代码图像

```cpp
for (auto x : istream_view<double>(cin))
  cout << x;
```

和其他视图一样，`istream_view` 可以与其他视图组合在一起：

点击此处查看代码图像

```cpp
auto cpx = istream_view<double>(cin);
for (auto x : transform_view(cpx, [](auto z){ return z; }))
  cout << x;
```

## 14.4 管道

对于每个标准视图，标准库都提供一个产生过滤器的函数；即一个可以作为过滤器适配器参数的对象。例如，`filter_view` 允许按序列组合过滤器，而不是将它们作为一组嵌套调用的形式呈现。管道样式（使用管道适配器）被认为比嵌套调用更具可读性。管道从左到右工作；即 `f` 的结果传递给 `g`，因此初始 `r` 必须是一个范围或生成器。这些过滤函数位于 `views::views` 命名空间中：

```cpp
void user(forward_range auto r)
{
  auto odd = [](int x) { return x % 2; };
  for (int x : r | views::filter(odd) | views::take(3))
    cout << x;
}
```

视图和管道的实现涉及一些令人头疼的元编程，如果你担心性能，请确保测量你的实现是否提供了你所需。如果不是，总有一种传统的变通方法：

点击此处查看代码图像

```cpp
void user(forward_range auto r)
{
  int count = 0;
  for (int x : r) {
    cout << x;
    if (++count == 3) return;
  }
}
```

然而，其运行逻辑被模糊了。

## 14.5 概念概述

标准库提供了许多实用的概念：

- 定义类型属性的概念（§14.5.1）
- 定义迭代器的概念（§14.5.2）
- 定义范围的概念（§14.5.3）

### 14.5.1 类型概念

概念涉及类型的属性，并且它们之间的关系反映了类型的多样性。这些概念有助于简化模板。

| 核心语言概念 `<concepts>` | `T` 和 `U` 是类型 |
| `same_as<T,U>` | `T` 与 `U` 相同 |
| `derived_from<T,U>` | `T` 继承自 `U` |
| `convertible_to<T,U>` | 一个 `T` 可以转换为 `U` |
| `common_reference_with<T,U>` | `T` 和 `U` 共享一个共同引用类型 |
| `common_with<T,U>` | `T` 和 `U` 共享一个共同类型 |
| `integral<T>` | `T` 是整数类型 |
| `signed_integral<T>` | `T` 是有符号整数类型 |
| `unsigned_integral<T>` | `T` 是无符号整数类型 |
| `floating_point<T>` | `T` 是浮点类型 |
| `assignable_from<T,U>` | 一个 `U` 可以赋值给 `T` |
| `swappable<T,U>` | 一个 `T` 可以与 `U` 交换 |
| `swappable_with<T,T>` |  |

许多算法与相关类型的组合工作，例如混合了整数和浮点数的表达式。我们使用 `common_with` 来说明这种混合在数学上是合理的。如果 `common_with<X,Y>` 为真，我们使用 `common_type_t<X,Y>` 通过首先转换为 `common_type_t<X,Y>` 来比较 `X` 和 `Y`。例如：

点击此处查看代码图像

```cpp
common_type<string, const char> s1 = some_fct();
common_type<string, const char> s2 = some_other_fct();
```

```cpp
if (s1<s2) {
  ...
}
```

为了为一对类型指定共同类型，我们特化在 `common` 定义中使用的 `common_type_t`。例如：

点击此处查看代码图像

```cpp
using common_type_t<Bigint,long> = Bigint; // 适用于合适的 Bigint 定义
```

```cpp
{ x != };
{ x = (x = y) };
```

在编写模板时，我们需要对类型进行分类。

| 对象概念 `<concepts>` |  |
| --- | --- |
| `destructible<T>` | `T` 可以被销毁，并可以使用一元运算符 `&` 获取其地址 |
| `constructible_from<T,Args>` | `T` 可以从类型为 `Args` 的参数列表构造 |
| `default_initializable<T>` | `T` 可以被默认构造 |
| `move_constructible<T>` | `T` 可以被移动构造 |
| `copy_constructible<T>` | `T` 可以被拷贝构造和移动构造 |
| `movable<T>` | 符合 `move_constructible<T>`, `assignable<T&>` 和 `swapable<T>` |
| `copyable<T>` | 符合 `copy_constructible<T>`, `movable<T>` 和 `assignable<T, const T&>` |
| `semiregular<T>` | 符合 `copyable<T>` 和 `default_constructible<T>` |
| `regular<T>` | 符合 `semiregular<T>` 和 `equality_comparable<T>` |

类型的理想状态是 `regular`。普通类型的工作方式类似于 `int`，并简化了我们关于如何使用类型的大部分思考。尽管大多数类刚开始都是 `semiregular` 且缺乏默认的 `==`，但大多数类可以并且应该是 `regular`。

当我们作为受约束的模板模板执行操作时，我们需要指定它是如何调用的，以及我们对其语义提出了哪些其他假设。

| 可调用概念 `<concepts>` |  |
| --- | --- |
| `invocable<F,Args>` | `F` 可以用类型为 `Args` 的参数列表进行调用 |
| `regular_invocable<F,Args>` | 符合 `invocable<F,Args>` 且保持等价性 |
| `predicate<F,T>` | 返回 `bool` 的 `regular_invocable<F,Args>` |
| `relation<F,T,U>` | 提供等价关系的 `relation<F,T,U>` |
| `strict_weak_order<F,T,U>` | 提供严格弱序的 `relation<F,T,U>` |

如果 `$x==y$` 意味着 `$f(x)==f(y)$`，则函数 `$f$` 是保持等价的。`Invocable` 和 `regular_invocable` 仅在语义上不同。我们（目前）无法仅表达我们的意图。

同样，`relation` 和 `equivalence_relation` 仅在语义上不同。等价关系具有自反性、对称性和传递性。

`relation` 和 `strict_weak_order` 仅在语义上不同。严格弱序是标准库比较时假设的，例如 `<`。

### 14.5.2 迭代器概念

传统的标准算法通过迭代器访问数据，因此我们需要概念来对迭代器类型的属性进行分类。

|  |  |
| --- | --- |
| `input_or_output_iterator` | `I` 可以被增加 (`++`) 和解引用 (`*`) |
| `sentinel_for<S,I>` | `S` 是某类迭代器类型的哨兵（sentinel）；也就是说，`S` 是在 `I` 的值类型上的谓词 |
| `sized_sentinel_for<S,I>` | 一种哨兵 `S`，其中 `-` 运算符可以应用于 `I` |
| `input_iterator<I>` | `I` 是输入迭代器；`*` 仅用于读取 |
| `output_iterator<I>` | `I` 是输出迭代器；仅用于写入 |
| `forward_iterator<I>` | `I` 是前向迭代器，支持多次访问和 `==` |
| `bidirectional_iterator<I>` | 支持 `--` 的双向迭代器 |
| `random_access_iterator<I>` | 支持 `+`, `+=`, `-`, 和 `[]` 的双向迭代器 |
| `contiguous_iterator<I>` | 针对连续内存中元素的随机迭代器 |
| `permutable_iterator<I>` | 支持移动和交换的前向迭代器 |
| `mergeable<I,I2,R,O>` | 可以合并由 `I` 和 `I2` 定义的序列 |
| `sortable<I>` | 可以对 `I` 定义序列排序 |
| `sortable<I,R>` | 可以对 `I` 定义序列排序 |

对于 `S` 哨兵（sentinel），其中 `-` 运算符可以应用于 `I`。

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

### 14.5.3 范围概念

范围（range）概念定义了范围的属性。

| 范围概念 |  |
|--- | --- |
| `range<R>` | `R` 是迭代器和哨兵的范围 |
| `sized_range<R>` | `R` 是知道大小的范围 |
| `view<R>` | `R` 是具有常数时间移动和赋值的范围 |
| `common_range<R>` | `R` 是迭代器和哨兵类型相同的范围 |
| `input_range<R>` | `R` 是迭代器和哨兵的范围 |
| `output_range<R>` | `R` 是迭代器和哨兵的范围 |
| `forward_range<R>` | `R` 是支持多次访问的范围 |
| `bidirectional_range<R>` | `R` 是支持双向遍历的范围 |
| `random_access_range<R>` | `R` 是支持随机访问的范围 |
| `contiguous_range<R>` | `R` 是在连续内存中的范围 |

在 `<ranges>` 中有一些概念，但这是一个很好的开始。

# 15 指针与容器

> 教育是关于做什么、何时做以及为什么做。
>
> 培训是关于如何做。
>
> – Richard Hamming

- 引言
- 指针
    - `unique_ptr` 和 `shared_ptr`; `span`
- 容器
    - `array`; `bitset`; `pair`; `tuple`
- 替代方案
    - `variant`; `optional`; `any`
- 建议

## 15.1 引言

C++ 提供了简单的内置底层类型来持有和引用数据：对象和数组持有数据；指针和数组引用此类数据。然而，我们需要支持更专门和更通用的数据持有和使用方式。例如，标准库容器（第12章）和迭代器（$13.3）是为了通用算法设计的。

容器和指针抽象的共同点在于，要正确且高效地使用它们，需要封装数据以及一组访问和操作它们的函数。例如，指针是非常通用且高效的机器地址抽象，但正确地使用它们表示所有权已被证明是

非常困难。因此，标准库提供了资源管理指针；即封装了指针并提供了简化其正确使用的操作的类。

这些标准库抽象封装了内置类型，并要求在时间和空间上的表现与正确使用这些类型时一样优异。

这些类型并没有什么“魔法”之处。我们可以根据需要，使用与标准库中相同的技术，设计并实现我们自己的“智能指针”和特化容器。

## 15.2 指针

指针的通用概念是它引用一个对象并根据其类型对其进行访问。内置类型（如 `int*`）是一个例子，但还有许多其他类型。

| 指针 | 描述 |
| :--- | :--- |
| `T*` | 内置指针：指向类型为 `T` 的对象，或指向连续分配的类型为 `T` 的元素序列 |
| `T&` | 内置引用：引用类型为 `T` 的对象；带有隐式解引用（§1.7）的指针 |
| `unique_ptr<T>` | 对 `T` 的唯一所有权指针 |
| `shared_ptr<T>` | 指向 `T` 对象的指针；所有指向该 `T` 指针的 `shared_ptr` 共享所有权 |
| `weak_ptr<T>` | 指向由 `shared_ptr` 拥有的对象的指针；必须转换为 `shared_ptr` 访问对象 |
| `span<T>` | 指向 `T` 连续序列的指针 (§15.2.2) |
| `string_view<T>` | 指向常量元素序列的指针 (§10.3) |
| `X_iterator<C>` | 来自于 `C` 的元素序列；名称中的 `X` 表示迭代器的类型（§13.3） |

一个对象可以有多个指针。所有权指针是负责最终删除其引用的对象的指针。非所有权指针（例如 `T*` 或 `span`）可能会悬空（dangle）；即指向一个对象已被删除或已超出作用域的位置。

通过悬空指针进行读取或写入是最糟糕的 bug 之一。这样做的结果在技术上是未定义行为。在实践中，它通常意味着访问一个恰好占据该位置的对象。读取意味着获取数组值，而写入则会破坏一个无关的结构。我们能期待的最好就是程序崩溃；这通常比得到错误的结果要好。

C++ 核心指南 [CG] 提供了避免此类问题以及静态检查其永不发生的规则。然而，这里有几种避免指针问题的方法：

- 在对象超出作用域后，不要保留指向该局部对象的指针。特别是，永远不要从函数返回局部对象的指针，或在长生命周期的数据结构中存储来源不确定的指针。系统地使用容器和算法（第 12 章、第 13 章）通常可以让我们避免采用难以避免问题的编程技术。
- 使用所有权指针指向在自由存储（free store）分配的对象。
- 指向静态对象的指针（例如全局变量）不会悬空。
- 将指针算术交给资源句柄的实现（如 `vectors` 和 `unordered_maps`）。
- 记住 `string_views` 和 `span` 是非所有权指针。

### 15.2.1 unique_ptr 和 shared_ptr

任何非平凡程序的关键任务之一都是管理资源。资源必须获取并在以后（显式或隐式）释放的东西。例如内存、套接字、线程和文件句柄。对于长时间运行程序，未能及时释放资源（“泄漏”）会导致严重的性能下降 (§12.7)，甚至可能导致灾难性的崩溃。即使对于短程序，泄漏也可能导致尴尬，引起资源短缺并将运行时间增加几个数量级。

标准库组件的设计是为了不泄漏资源。为了做到这一点，它们依赖语言的基础资源管理支持，使用构造函数/析构函数对来确保资源不会超过负责它的对象的寿命。在 `Vector` 中使用构造函数/析构函数对来管理元素的生命周期就是一个例子 (§5.2.2)，所有标准库容器都以类似的方式实现。重要的是，这种方法能与错误异常正确交互。例如，这种技术被用于标准库的锁类：

点击此处查看代码图像

```cpp
mutex m; // 用于保护对共享数据的访问
void f()
{
    scoped_lock lock(m); // 获取互斥锁
    // ...
}
```

线程不会解锁，直到 `lock()` 的构造函数已获取了互斥锁 (§18.3)。相应的析构函数会释放互斥锁。在这个示例中，`scoped_lock` 通过返回或运行到末尾释放互斥锁。这是 RAII（“资源获取初始化”）的一个例子 (§5.2.2)。RAII 是 C++ 中处理资源的惯用方法。容器（如 `vector`、`map` 和 `ostream`）管理它们的资源（如文件句柄和缓冲区），并处理好作用范围内的对象，但分配在自由存储上的对象呢？在 `<memory>` 中，标准库提供了两个“智能指针”来帮助管理存储上的对象：

- `unique_ptr` 表示唯一所有权（它的析构函数销毁对象）
- `shared_ptr` 表示共享所有权（最后一个指针销毁对象）

“智能指针”最基本的用法是通过严谨的编程来防止内存泄漏。例如：

点击此处查看代码图像
