
## 前向迭代器

前向迭代器结合了输入迭代器的全部功能以及输出迭代器的几乎所有功能。假设 `forwardIterator` 是一个前向迭代器。表21-13描述了作用于 `forwardIterator` 的操作。

表21-13 前向迭代器上的操作

| 表达式 | 效果 |
|---|---|
| `*forwardIterator` | 访问 `forwardIterator` 所指向的元素。 |
| `forwardIterator->member` | 访问该元素的成员。 |
| `++forwardIterator` | 向前移动，返回新位置（前置递增）。 |
| `forwardIterator++` | 向前移动，返回旧位置（后置递增）。 |
| `forwardIt1 == forwardIt2` | 如果两个迭代器相同则返回 `true`，否则返回 `false`。 |
| `forwardIt1 != forwardIt2` | 如果两个迭代器不相同则返回 `true`，否则返回 `false`。 |
| `forwardIt1 = forwardIt2` | 赋值 |

> 前向迭代器可以指向同一集合中的同一元素，并多次处理同一元素。

## 双向迭代器

双向迭代器是前向迭代器，也可以反向遍历元素。假设 `bidirectionalIterator` 是一个双向迭代器。为前向迭代器定义的操作（表21-13）也适用于双向迭代器。为了向后步进，还为 `bidirectionalIterator` 定义了递减操作。表21-14展示了双向迭代器上的附加操作。

**表21-14** 双向迭代器上的附加操作

| 表达式 | 效果 |
|---|---|
| `--bidirectionalIterator` | 向后移动，返回新位置（前置递减）。 |
| `bidirectionalIterator--` | 向后移动，返回旧位置（后置递减）。 |

> 双向迭代器可用于 `vector`、`deque`、`list`、`set`、`multiset`、`map` 和 `multimap` 类型的容器。

## 随机访问迭代器

随机访问迭代器是双向迭代器，可以随机处理容器中的元素。这些迭代器可用于 `vector`、`deque` 和 `string` 类型的容器以及数组。为双向迭代器定义的操作（例如表21-13和表21-14）也适用于随机访问迭代器。表21-15描述了为随机访问迭代器定义的附加操作。假设 `rAccessIterator` 是一个随机访问迭代器。

**表21-15** 随机访问迭代器上的附加操作

| 表达式 | 效果 |
|---|---|
| `rAccessIterator[n]` | 访问第 n 个元素。 |
| `rAccessIterator += n` | 如果 n >= 0，则将 `rAccessIterator` 向前移动 n 个元素；如果 n < 0，则向后移动。 |
| `rAccessIterator -= n` | 如果 n >= 0，则将 `rAccessIterator` 向后移动 n 个元素；如果 n < 0，则向前移动。 |
| `rAccessIterator + n` | 返回后第 n 个元素的迭代器。 |
| `n + rAccessIterator` | 返回后第 n 个元素的迭代器。 |
| `rAccessIterator - n` | 返回前第 n 个元素的迭代器。 |
| `rAccessIt1 - rAccessIt2` | 返回迭代器 `rAccessIt1` 和 `rAccessIt2` 之间的距离。 |
| `rAccessIt1 < rAccessIt2` | 如果 rAccessIt1 位于 rAccessIt2 之前，则返回 true，否则返回 false。 |
| `rAccessIt1 <= rAccessIt2` | 如果 rAccessIt1 位于 rAccessIt2 之前或与之相等，则返回 true，否则返回 false。 |
| `rAccessIt1 > rAccessIt2` | 如果 rAccessIt1 位于 rAccessIt2 之后，则返回 true，否则返回 false。 |
| `rAccessIt1 >= rAccessIt2` | 如果 rAccessIt1 位于 rAccessIt2 之后或与之相等，则返回 true，否则返回 false。 |

图21-1展示了迭代器层次结构。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1475_0.png)

现在你已经了解了不同类型的迭代器，接下来我们描述如何声明容器中的迭代器。

## typedef ITERATOR

每个容器（序列容器或关联容器）都包含一个 typedef iterator。因此，容器中的迭代器使用 typedef iterator 来声明。例如，语句：

```
vector<int>::iterator intVecIter;
```

将 intVecIter 声明为 int 类型的 vector 容器中的迭代器。

因为 iterator 是在容器（即类）如 vector 内部定义的 typedef，所以我们必须使用适当的容器名、容器元素类型和作用域解析运算符来使用 typedef iterator。

### typedef CONST_ITERATOR

因为迭代器的工作方式类似于指针，借助容器中的迭代器和解引用运算符，我们可以修改容器中的元素。然而，如果容器被声明为 const，那么我们必须防止迭代器修改容器中的元素，尤其是意外修改。为了处理这种情况，每个容器还包含另一个 typedef const_iterator。例如，语句：

```
vector<int>::const_iterator intConstVect;
```

将 intConstVect 声明为元素类型为 int 的 vector 容器中的迭代器。迭代器 intConstVect 用于处理那些被声明为 vector<int> 类型的常量 vector 容器的元素。

const_iterator 类型的迭代器是只读迭代器。

### typedef REVERSE_ITERATOR

每个容器还包含 typedef reverse_iterator。此类型的迭代器用于反向遍历容器中的元素。

### typedef CONST_REVERSE_ITERATOR

此类型的迭代器是只读迭代器，用于反向遍历容器中的元素。如果容器被声明为 const，并且我们需要反向遍历容器中的元素，则需要此迭代器。

除了前面的四个 typedef 之外，还有几个 typedef 是所有容器共有的，表21-16对此进行了描述。

**表21-16** 所有容器共有的各种 typedef

| 类型 | 效果 |
|---|---|
| `difference_type` | 两个指向同一容器的迭代器相减所得结果的类型。 |
| `pointer` | 指向容器中存储元素类型的指针。 |
| `reference` | 对容器中存储元素类型的引用。 |
| `const_reference` | 对容器中存储元素类型的常量引用。常量引用是只读的。 |
| `size_type` | 用于对容器中元素进行计数的类型。此类型也用于对序列容器进行索引，但 list 容器除外。 |
| `value_type` | 容器元素的类型。 |

## 流迭代器

另一组有用的迭代器是流迭代器——istream 迭代器和 ostream 迭代器。本节介绍这两种迭代器。

### `istream_iterator`

istream 迭代器用于从输入流向程序输入数据。类 istream_iterator 包含输入流迭代器的定义。使用 istream 迭代器的一般语法是：

```
istream_iterator<Type> isIdentifier(istream&);
```

其中 Type 是内置类型或用户定义的类类型，并且为其定义了输入迭代器。标识符 isIdentifier 使用构造函数初始化，该构造函数的参数是 istream 类对象（例如 cin）或任何公开定义的 istream 子类型（例如 ifstream）。

### `ostream_iterator`

ostream 迭代器用于将程序中的数据输出到输出流。这些迭代器在本章前面已经定义过。为完整起见，我们在这里回顾它们。

类 ostream_iterator 包含输出流迭代器的定义。使用 ostream 迭代器的一般语法是：

```
ostream_iterator<Type> osIdentifier(ostream&);
```

或：

```
ostream_iterator<Type> osIdentifier(ostream&, char* deLimit);
```

其中 Type 是内置类型或用户定义的类类型，并且为其定义了输出迭代器。标识符 osIdentifier 使用构造函数初始化，该构造函数的参数是 ostream 类对象（例如 cout）或任何公开定义的 ostream 子类型（例如 ofstream）。在用于声明 ostream 迭代器的第二种形式中，通过使用初始化构造函数的第二个参数（deLimit），我们可以指定分隔输出的字符。

## 关联容器

本节讨论关联容器。关联容器中的元素会根据某种排序准则自动排序。默认排序准则是关系运算符 <（小于）。用户还可以选择指定自己的排序准则。
