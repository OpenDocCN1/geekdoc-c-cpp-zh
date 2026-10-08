

```cpp
bool operator()(const pair<string,int&>& r) const { return r.second > val; }
```

或者，且等价地，我们可以使用 lambda 表达式 (§7.3.2)：

点击此处查看代码图像

```cpp
auto p = find_if(m, [](const auto& r) { return r.second > 42; });
```

谓词不应修改其应用的元素。

## 13.5 算法概述

算法的通用定义是“一组有限的规则，它为解决一组特定问题提供了一系列操作[并且]具有五个重要特征：有限性 ... 确定性 ... 输入 ... 输出 ... 有效性” [Knuth,1968§1.1]。在 C++ 标准库的上下文中，算法是一个作用在元素序列上的函数句模板。

标准库提供了数十种算法。这些算法定义在 `<algorithm>` 和 `<numeric>` 头文件中。这些标准库算法都以序列作为输入。从 b 到 e 的半开区间称为 [b:e)。以下是几个示例：

## 标准算法 <algorithm>

| f=for_each(b,e,f) | 对 [b:e) 中的每个元素 x 执行 f(x) |
| p=find(b,e,x) | p 是 [b:e) 中第一个满足 "p==x" 的 p |
| p=find_if(b,e,f) | p 是 [b:e) 中第一个满足 'f'(p) 的 p |
| n=count(b,e) | n 是 [b:e) 中满足 "q==x" 的元素 'q' 的数量 |
| n=count_if(b,e,f) | n 是 [b:e) 中满足 'f'(q)' 的元素 'q' 的数量 |
| replace(b,e,v) | 将 [b:e) 中满足 "q==v" 的元素 'q' 替换为 v |
| replace_if(b,e,f) | 将 [b:e) 中满足 'f'(q)' 的元素 'q' 替换为 v |
| p=copy(b,out) | 将 [b:e) 复制到 [out) |
| p=copy_if(b,out) | 将 [b:e) 中满足 'f'(q) 的元素复制到 [out) |
| p=move(b,out) | 将 [b:e) 移动到 [out) |
| p=unique_copy(b,out) | 将 [b:e) 复制到 [out)；不复制相邻重复元素 |
| sort(b,e) | 使用排序准则排序 [b:e) 中的元素 |
| sort(b,e,f) | 使用 f 作为排序准则排序 [b:e) 中的元素 |
| (p1,p2)=equal_range(b,e,v) | [p1,p2) 是排序后序列 [b:e) 中值为 v 的子序列；作为对 v 的二分查找 |
| p=merge(b,e,b2,e2,out) | 将两个有序序列 [b:e) 和 [b:e2) 合并到 [out) |
| p=merge(b,e,b2,e2,out,f) | 使用 f 作为比较标准将两个有序序列 [b:e) 和 [b:e2) 合并到 [out) |

对于每个接受 [b:e) 范围的算法，`<ranges>` 都提供了一个接受范围的版本。请记住 (§9.3.2) 同时使用标准库算法的传统迭代器版本及其 ranges 对应版本，你需要对调用进行限定或使用 using 声明。

这些算法以及许多其他算法（例如 §17.3）可以应用于容器、字符串和内置数组的元素。

某些算法（如 `replace()` 和 `sort()`）会修改值元素，但没有哪个算法会添加或删除容器的元素。原因是序列并不标识持有该序列元素的容器。要添加或删除元素，你需要一个了解容器的对象（例如 `back_inserter()`；§13.1）或直接引用容器本身（例如 `push_back()` 或 `erase()`；§12.2）。

Lambda 是作为参数传递的非常常见的的操作。例如：

点击此处查看代码图像

```cpp
vector<int> v={0,1,2,3,4,5};
for_each(v.begin(),v.end(),[](int &x){x*=x;});
for_each(v.begin(),v.end(),[](int &x){x=sqrt(x);});
```

标准库算法需要比手工编写的循环更细致的设计和实现。了解它们，并优于原生语言使用它们。

## 13.6 并行算法

当同一个任务需要处理许多数据项时，只要通信是独立的，我们就可以每个数据项上执行它：

- 并行执行：任务在多个线程上执行（通常运行在处理器核心上）
- 向量化执行：任务在单线程上使用向量化执行，也称为 SIMD（单指令，多数据）。

标准库对这两者都提供了支持，我们可以明确指定想要顺序执行；在 `<execution>` 命名空间中：

- seq：顺序执行（可行）
- par：并行执行（可行）
- unseq：无序执行（向量化）
- par_unseq：并行和/或无序执行（可行）。考虑 `std::sort()`：

```cpp
sort(v.begin(),v.end());           // 顺序
sort(seq,v.begin(),v.end());      // 顺序（默认）
sort(par,v.begin(),v.end());        // 并行
sort(par_unseq,v.begin(),v.end()); // 并行和/或无序
```

是否值得并行/向量化取决于算法、序列中的元素以及程序对硬件的利用。因此，执行策略只是提示。编译器或运行时调度程序将决定使用多少并发。这是平凡的，在这里关于效率的规则非常重要。

遗憾的是，并行算法尚未进入标准库，但如果我们需要它们，它们很容易定义：

点击此处查看代码

```cpp
void sort(auto pol, random_access_range& r)
{
  sort(pol.begin(),r.end());
}
```

大多数标准库算法（除 `equal_range` 外的所有算法）都可以请求使用 `par` 和 `unseq` 进行并行和向量化。数值数据参见 §17.3。

## 13.7 建议

- STL 算法作用于一个或多个序列；§13.1。
- 输入序列是半开的，由一对迭代器定义；§13.1。
- 你可以定义迭代器来满足特殊需求；§13.1。
- 许多算法可以应用于 I/O 流；§3.3。
- 搜索时，算法通常返回输入序列的结尾表示“未找到”；§3.2。
- 算法不会直接从其参数中添加或删除元素；§3.2。
- 编写循环时，考虑是否可以表示为通用算法；§3.2。
- 使用类型别名来清理复杂的符号；§3.2。
- 使用谓词和其他函数对象为标准算法提供更广泛的含义；§3.4, §3.5。
- 谓词不应修改其参数；§3.4。
- 了解你的标准库算法，并优于手工编写的循环；§3.5。

## 14 Ranges

> 如果没有经验验证结论，强大的论据毫无意义。 — Roger Bacon

- 引言
- Views
- 流水线
- Concepts 概述
  - 类型 Concepts；迭代器 Concepts；范围 Concepts
- 建议

## 14.1 引言

标准库在 `<ranges>` 命名空间中提供了受限概念（第 8 章）和未受限（为了兼容性）的版本。自然，我更倾向于使用概念。范围是 `{begin(), end()}` 对定义的序列的泛化；它指定元素序列。范围可以通过以下方式定义：

- 一对 (begin, end)
- 一对 (begin, n)，其中 begin 是迭代器，n 是元素数量
- 一对 (begin, pred)，其中 begin 是迭代器，pred 是谓词；如果 pred(p) 对迭代器 p 为真，则我们到达范围的结尾。这允许我们拥有无限范围和“按需”生成的范围 (§14.3)。

这种范围概念允许我们说 `sort(v)` 而不是 `sort(v.begin(),v.end())`，因为自 1994 年以来我们一直使用 STL。我们对自己的算法也可以这样做：

点击此处查看 forward_range R

```cpp
template<forward_range R>
    requires sortable<iterator<R>>
void my_sort(R& r) // 受概念限制的 my_sort
{
    return my_sort(r.begin(),r.end()); // 使用 1994 风格的 sort
}
```

Ranges 允许我们更直接地表达算法 99% 的常用场景。除了显著优势外，ranges 还提供了优化和消除一类“愚错误”的机会，例如 `sort(v1.begin(),v2.end())` 和 `sort(v2.end(),v1.begin())`。这类错误在世界上可见的。

自然，对应不同类型迭代器的不同类型范围。特别是 `input_range`、`forward_range`、`bidirectional_range`、`random_access_range` 和 `contiguous_range` 被表示为概念 (§14.5)。

## 14.2 Views

View 是查看范围的一种。例如：

点击此处查看 forward_range auto& r

```cpp
void user(forward_range auto& r)
{
    filter_view v { r, [](int x) { return x%2; } }; // 来自 r 的奇数
    cout << "odd numbers: ";
    for (int x : v)
        cout << x << ' ';
}
```

从 `filter_view` 读取时，我们从范围中读取。如果值匹配谓词，则返回；否则，`filter_view` 尝试使用范围中的元素重试。许多范围是无限的。我们通常只找到几个值。因此，有视图从范围中提取少数值：

点击此处查看 forward_range auto& r

```cpp
void user(forward_range auto& r)
{
    filter_view v(r, [](int x) { return x%2; } }); // r 中的奇数
    take_view tv (v, 100); // 从 v 中查看最多 100 个元素
    cout << "odd numbers: ";
    for (int x : tv)
        cout << x << ' ';
}
```

我们可以通过直接使用 `take_view` 来避免命名它：

for (int x : take_view(v, 3))

