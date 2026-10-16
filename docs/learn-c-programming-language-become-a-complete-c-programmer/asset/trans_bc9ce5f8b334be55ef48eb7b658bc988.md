

`priority_queue` 很可能使用 `heap` 实现 (§32.6.4)。

## 31.6 Advice

+   [1] 一个 STL 容器定义了一个序列；§31.2。
+   [2] 将 `vector` 作为你的默认容器使用；§31.2, §31.4。
+   [3] 插入操作符，例如 `insert()` 和 `push_back()` 在 `vector` 上通常比在 `list` 上更高效；§31.2, §31.4.1.1。
+   [4] 对于通常为空的序列，使用 `forward_list`；§31.2, §31.4.2。
+   [5] 在性能方面，不要相信你的直觉：要测量；§31.3。
+   [6] 不要盲目相信渐近复杂度度量；有些序列很短，单个操作的成本可能差异巨大；§31.3。
+   [7] STL 容器是资源句柄；§31.2.1。
+   [8] 一个 `map` 通常实现为红黑树；§31.2.1, §31.4.3。
+   [9] 一个 `unordered_map` 是一个哈希表；§31.2.1, §31.4.3.2。
+   [10] 要成为 STL 容器的元素类型，一个类型必须提供拷贝或移动操作；§31.2.2。
+   [11] 当你需要保留多态行为时，使用指针或智能指针的容器；§31.2.2。
+   [12] 比较操作应实现严格弱序；§31.2.2.1。
+   [13] 按引用传递容器，按值返回容器；§31.3.2。
+   [14] 对于容器，使用 `()`-初始化语法指定大小，使用 `{}`-初始化语法指定元素列表；§31.3.2。
+   [15] 对于容器的简单遍历，使用 `rangefor` 循环或 begin/end 一对迭代器；§31.3.4。
+   [16] 当你不需要修改容器的元素时，使用 `const` 迭代器；§31.3.4。
+   [17] 使用 `auto` 避免使用迭代器时的冗长和拼写错误；§31.3.4。
+   [18] 使用 `reserve()` 避免使指向元素的指针和迭代器失效；§31.3.3, §31.4.1。
+   [19] 不要在没有测量的情况下假设 `reserve()` 的性能优势；§31.3.3。
+   [20] 在容器上使用 `push_back()` 或 `resize()` 而不是在数组上使用 `realloc()`；§31.3.3, §31.4.1.1。
+   [21] 不要使用已调整大小的 `vector` 或 `deque` 的迭代器；§31.3.3。
+   [22] 在必要时，使用 `reserve()` 使性能可预测；§31.3.3。
+   [23] 不要假设 `[]` 会进行范围检查；§31.2.2。
+   [24] 当你需要保证范围检查时，使用 `at()`；§31.2.2。
+   [25] 使用 `emplace()` 以获得记法上的便利；§31.3.7。

Section 31.6 Advice 925

+   [26] 优先使用紧凑且连续的数据结构；§31.4.1.2。
+   [27] 使用 `emplace()` 以避免必须预先初始化元素；§31.4.1.3。
+   [28] `list` 遍历相对昂贵；§31.4.2。
+   [29] 一个列表通常有每个元素四字长的内存开销；§31.4.2。
+   [30] 有序容器的序列由其比较对象定义（默认 <）；§31.4.3.1。
+   [31] 无序容器（哈希容器）的序列不是可预测的有序；§31.4.3.2。
+   [32] 如果你需要对大量数据进行快速查找，使用无序容器；§31.3。
+   [33] 对于没有自然顺序的元素类型（例如，没有合理的 <）使用无序容器；§31.4.3。
+   [34] 如果你需要按顺序遍历其元素，使用有序关联容器（例如 map 和 set）；§31.4.3.2。
+   [35] 实验以检查你是否拥有可接受的哈希函数；§31.4.3.4。
+   [36] 通过使用异或组合标准哈希函数得到的哈希函数通常是好的；§31.4.3.4。
+   [37] 0.7 通常是一个合理的负载因子；§31.4.3.5。
+   [38] 你可以为容器提供替代接口；§31.5。
+   [39] STL 适配器不提供对其底层容器的直接访问；§31.5。

# This page intentionally left blank

+   - Introduction
+   - Algorithms
+     Sequences; Policy Arguments; Complexity
+   - Nonmodifying Sequence Algorithms for_each(); Sequence Predicates; count(); find(); equal() and mismatch(); search()
+   - Modifying Sequence Algorithms
+     copy(); unique(); remove() and replace(); rotate(), random_shuffle(), and partition();
+     Permutations; fill(); swap()
+   - Sorting and Searching
+     Binary Search; merge(); Set Algorithms; Heaps; lexicographical_compare()
+   - Min and Max
+   - Advice

## 32

## STL Algorithms

> *Form is liberating.*
> — Engineer’s proverb

## 32.1 Introduction

本章介绍 STL 算法。STL 由标准库的迭代器、容器、算法和函数对象部分组成。STL 的其余部分在第 31 章和第 33 章中介绍。

## 32.2 Algorithms

在 <algorithm> 中定义了约 80 个标准算法。它们操作由一对迭代器定义的 *序列*（用于输入）或单个迭代器（用于输出）。在拷贝、比较等两个序列时，第一个序列由一对迭代器 [b:e) 表示，但第二个序列仅由单个迭代器 b2 表示，该迭代器被视为持有足够元素以供算法使用的序列的开始，例如，与第一个序列一样多的元素：[b2:b2+(e−b))。某些算法，例如 sort()，需要随机访问迭代器，而许多算法，例如 find()，仅按顺序读取其元素，因此可以使用前向迭代器即可。许多算法遵循通常的约定，返回序列的末尾以表示“未找到”（§4.5）。我不会为每个算法提及这一点。

算法，无论是标准库算法还是用户自己的算法都很重要：

+   • 每个算法命名一个特定操作，记录接口并指定语义。
+   • 每个算法可以被广泛使用并为许多程序员所知。

对于正确性、可维护性和性能而言，与“随机代码”相比，这些可以是巨大的优势，后者具有功能和依赖性定义较差的代码。如果你发现自己编写了一段包含多个循环、似乎彼此无关的局部变量或复杂控制结构的代码，请考虑是否可以通过将其中一部分做成具有描述性名称、明确目的、明确接口和明确依赖性的函数/算法来简化代码。

STL 算法风格的数值算法在 §40.6 中介绍。

### 32.2.1 Sequences

标准库算法的理想是为可以实现最优的东西提供最通用和灵活的接口。基于迭代器的接口是对该理想的良好但不完美的近似（§33.1.1）。例如，基于迭代器的接口不能直接表示序列的概念，导致可能出现混淆和检测某些范围错误方面的困难：

```
void user(vector<int>& v1, vector<int>& v2)
{
copy(v1.begin(),v1.end(),v2.begin()); // mayoverflowv2
sort(v1.begin(),v2.end()); // oops!
}
```

许多此类问题可以通过提供标准库算法的容器版本来缓解。例如：

```
template<typename Cont>
void sort(Cont& c)
{
static_assert(Range<Cont>(), "sort(): Cont argument not a Range");
static_assert(Sortable<Iterator<Cont>>(), "sort(): Cont argument not Sortable");
std::sort(begin(c),end(c)); }
```

```
template<typename Cont1, typename Cont2> void copy(const Cont1& source , Cont2& target) {
static_assert(Range<Cont1>(), "copy(): Cont1 argument not a Range");
static_assert(Range<Cont2>(), "copy(): Cont2 argument not a Range");
```

Section 32.2.1 Sequences 929

```
if (target.size()<source.size()) throw out_of_range{"copy target too small"};
std::copy(source.begin(),source.end(),target.begin());
}
```

这将简化 user() 的定义，使第二个错误不可能表达，并在运行时捕获第一个错误：

```
void user(vector<int>& v1, vector<int>& v2)
{
copy(v1,v2); // overflows will be caught
sort(v1);
}
```

然而，容器版本也比直接使用迭代器的版本更不通用。特别是，你不能使用容器 sort() 对容器的一半进行排序，也不能使用容器 copy() 写入输出流。

一种互补的方法是定义一个“范围”或“序列”抽象，允许我们在需要时定义序列。我使用概念 Range 来表示任何具有 begin() 和 end() 迭代器的东西（§24.4.4）。也就是说，没有持有数据的 Range 类——正如 STL 中没有 Iterator 类或 Container 类一样。因此，在“容器 sort()”和“容器 copy()”示例中，我将模板参数称为 Cont（表示“容器”），但它们将接受任何具有 begin() 和 end() 且满足算法其余要求的序列。

标准库容器大多返回迭代器。特别是，它们不返回结果容器（除了少数罕见的例子，例如 pair）。一个原因是在设计 STL 时，没有直接支持移动语义。所以，有

