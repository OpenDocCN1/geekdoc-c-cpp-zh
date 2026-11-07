
**表 21-14** 双向迭代器的附加操作

| 表达式 | 效果 |
| --- | --- |
| `--biDirectionalIterator` | 向后移动，返回新位置（前置递减）。 |
| `biDirectionalIterator--` | 向后移动，返回旧位置（后置递减）。 |

> **注意**
> 双向迭代器可用于 `vector`、`deque`、`list`、`set`、`multiset`、`map` 和 `multimap` 类型的容器。

## 随机访问迭代器

随机访问迭代器是能够随机处理容器元素的双向迭代器。这些迭代器可用于 `vector`、`deque` 和 `string` 类型的容器，以及数组。为双向迭代器定义的操作（例如表 21-13 和表 21-14）也适用于随机访问迭代器。表 21-15 描述了为随机访问迭代器定义的附加操作。假设 `rAccessIterator` 是一个随机访问迭代器。

**表 21-15** 随机访问迭代器的附加操作

| 表达式 | 效果 |
| --- | --- |
| `rAccessIterator[n]` | 访问第 n 个元素。 |
| `rAccessIterator += n` | 如果 n >= 0，则将 `rAccessIterator` 向前移动 n 个元素；如果 n < 0，则向后移动。 |
| `rAccessIterator -= n` | 如果 n >= 0，则将 `rAccessIterator` 向后移动 n 个元素；如果 n < 0，则向前移动。 |
| `rAccessIterator + n` | 返回其后第 n 个元素的迭代器。 |
| `n + rAccessIterator` | 返回其后第 n 个元素的迭代器。 |
| `rAccessIterator - n` | 返回其前第 n 个元素的迭代器。 |
| `rAccessIt1 - rAccessIt2` | 返回迭代器 `rAccessIt1` 和 `rAccessIt2` 之间的距离。 |
| `rAccessIt1 < rAccessIt2` | 如果 `rAccessIt1` 位于 `rAccessIt2` 之前，则返回 `true`，否则返回 `false`。 |
| `rAccessIt1 <= rAccessIt2` | 如果 `rAccessIt1` 位于 `rAccessIt2` 之前或与之相等，则返回 `true`，否则返回 `false`。 |
| `rAccessIt1 > rAccessIt2` | 如果 `rAccessIt1` 位于 `rAccessIt2` 之后，则返回 `true`，否则返回 `false`。 |
| `rAccessIt1 >= rAccessIt2` | 如果 `rAccessIt1` 位于 `rAccessIt2` 之后或与之相等，则返回 `true`，否则返回 `false`。 |

图 21-1 展示了迭代器层次结构。

![](img/b217c421655b51e7494cf3b89bb5432d_1540_0.png)

**图 21-1** 迭代器层次结构

现在你已经了解了不同类型的迭代器，接下来我们描述如何为容器声明迭代器。

## typedef iterator

每个容器（序列容器或关联容器）都包含一个 `typedef` iterator。因此，容器迭代器是使用 `typedef` iterator 声明的。例如，语句

```cpp
vector<int>::iterator intVector;
```

将 `intVector` 声明为 `int` 类型 vector 容器的一个迭代器。

因为 `iterator` 是在容器（即类）如 `vector` 内部定义的 `typedef`，所以我们必须使用合适的容器名、容器元素类型和作用域解析运算符来使用 `typedef` iterator。

## typedef const_iterator

因为迭代器的工作方式类似指针，借助容器迭代器和解引用运算符 `*`，我们可以修改容器中的元素。然而，如果容器被声明为 `const`，那么我们必须防止迭代器修改容器中的元素，尤其是意外修改。为了处理这种情况，每个容器还包含另一个 `typedef const_iterator`。例如，语句

```cpp
vector<int>::const_iterator intConstVecIt;
```

将 `intConstVecIt` 声明为 `vector` 容器的一个迭代器，该容器的元素类型为 `int`。迭代器 `intConstVecIt` 用于处理那些被声明为 `vector<int>` 类型常量 vector 容器的元素。

`const_iterator` 类型的迭代器是只读迭代器。

## typedef reverse_iterator

每个容器还包含 `typedef reverse_iterator`。这种类型的迭代器用于反向遍历容器中的元素。

## typedef const_reverse_iterator

这种类型的迭代器是只读迭代器，用于反向遍历容器中的元素。如果容器被声明为 `const`，并且我们需要反向遍历容器中的元素，则需要这种迭代器。

除了前面的四个 `typedef` 之外，还有其他几个所有容器共有的 `typedef`，表 21-16 对它们进行了描述。

**表 21-16** 所有容器共有的各种 typedef

| typedef | 效果 |
|---|---|
| `difference_type` | 两个指向同一容器的迭代器相减所得结果的类型。 |
| `pointer` | 指向容器中所存储元素类型的指针。 |
| `reference` | 对容器中所存储元素类型的引用。 |
| `const_reference` | 对容器中所存储元素类型的常量引用。const 引用是只读的。 |
| `size_type` | 用于对容器中的元素进行计数的类型。此类型也用于通过序列容器进行索引，但 `list` 容器除外。 |
| `value_type` | 容器元素的类型。 |

## 流迭代器

另一组有用的迭代器是*流迭代器——istream 迭代器和 ostream 迭代器。*本节介绍这两种迭代器。

## istream_iterator

`istream` 迭代器用于从输入流将数据输入到程序中。类 `istream_iterator` 包含输入流迭代器的定义。使用 `istream` 迭代器的一般语法是：

```cpp
istream_iterator<Type> isIdentifier(istream&);
```

其中 `Type` 是内置类型或用户定义的类类型，并且为其定义了输入迭代器。标识符 `isIdentifier` 使用构造函数初始化，该构造函数的参数是 `istream` 类对象（如 `cin`）或任何公开定义的 `istream` 子类型（如 `ifstream`）。

## ostream_iterator

`ostream` 迭代器用于将程序中的数据输出到输出流。这些迭代器在本章前面已经定义过。为完整起见，我们在此回顾它们。

类 `ostream_iterator` 包含输出流迭代器的定义。使用 `ostream` 迭代器的一般语法是

```cpp
ostream_iterator<Type> osIdentifier(ostream&);
```

或

```cpp
ostream_iterator<Type> osIdentifier(ostream&, char* deLimit);
```

其中 `Type` 是内置类型或用户定义的类类型，并且为其定义了输出迭代器。标识符 `osIdentifier` 使用构造函数初始化，该构造函数的参数是 `ostream` 类对象（如 `cout`）或任何公开定义的 `ostream` 子类型（如 `ofstream`）。在用于声明 `ostream` 迭代器的第二种形式中，通过使用初始化构造函数的第二个参数（`deLimit`），我们可以指定一个用于分隔输出的字符。

## 关联容器

本节讨论关联容器。关联容器中的元素会根据某种排序准则自动排序。默认排序准则是关系运算符 <（小于）。用户还可以选择指定自己的排序准则。

由于关联容器中的元素会自动排序，因此当新元素插入容器时，它会被插入到适当的位置。实现这类数据结构的一种方便而快速的方法是使用二叉搜索树。事实上，关联容器就是这样实现的。因此，容器中的每个元素都有一个父节点（根节点除外），并且最多有两个子节点。对于每个元素，父节点中的键大于左子节点中的键，且小于右子节点中的键。

STL 中预定义的关联容器如下：

- 集合
- 多重集合
- 映射
- 多重映射

本书只讨论关联容器 `set` 和 `multiset`。

## 关联容器：set 和 multiset

如前所述，容器 set 和 multiset 都根据某种排序准则自动对其元素排序。默认排序准则是关系运算符 <（小于）；也就是说，元素按升序排列。用户也可以指定其他排序准则。对于用户定义的数据类型（如类），必须正确重载关系运算符。

容器 set 和 multiset 之间的唯一区别是：容器 multiset 允许重复元素，而容器 set 不允许。

定义容器 set 的类名是 set；定义容器 multiset 的类名是 multiset。包含类 set 和 multiset 的定义以及用于实现这些容器各种操作的函数定义的头文件名是 set。因此，要使用这些容器中的任何一个，程序必须包含以下语句：

```cpp
#include <set>
```

## 声明 set 或 multiset 关联容器

类 set 和 multiset 包含多个构造函数，用于声明和初始化这些类型的容器。本节讨论声明和初始化这些类型关联容器的各种方式。表 21-17 描述了如何声明和初始化特定类型的 set/multiset 容器。
