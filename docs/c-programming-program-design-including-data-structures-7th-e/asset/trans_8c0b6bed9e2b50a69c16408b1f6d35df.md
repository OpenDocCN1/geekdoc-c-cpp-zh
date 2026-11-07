

## 声明 vector 对象

类 vector 包含多个构造函数，包括默认构造函数。因此，可以用多种方式声明和初始化 vector 容器。表 21-1 描述了如何声明和初始化特定类型的 vector 容器。

**表 21-1** 声明和初始化 vector 容器的多种方式

| 语句 | 作用 |
|---|---|
| `vector<elemType> vecList;` | 创建空的 vector 容器 `vecList`。（调用默认构造函数。） |
| `vector<elemType> vecList(otherVecList);` | 创建 vector 容器 `vecList`，并将 `vecList` 初始化为 vector `otherVecList` 的元素。`vecList` 和 `otherVecList` 类型相同。 |
| `vector<elemType> vecList(size);` | 创建大小为 `size` 的 vector 容器 `vecList`。`vecList` 使用默认构造函数初始化。 |
| `vector<elemType> vecList(n, elm);` | 创建大小为 `n` 的 vector 容器 `vecList`。`vecList` 使用元素 `elm` 的 `n` 个副本初始化。 |
| `vector<elemType> vecList(beg, end);` | 创建 vector 容器 `vecList`。`vecList` 初始化为范围 [beg, end) 中的元素，即范围 `beg, ..., end-1` 中的所有元素。`beg` 和 `end` 都是指针，在 STL 术语中称为迭代器。（本章后面将解释迭代器的用法。） |

现在我们已经知道如何声明 vector 序列容器，接下来讨论如何操作存储在 vector 容器中的数据。为了操作 vector 容器中的数据，我们必须了解以下基本操作：

- 项插入
- 项删除
- 遍历 vector 容器的元素

使用表 21-2 给出的操作可以直接访问 vector 容器中的元素。函数名以粗体显示。

**表 21-2** 访问 vector 容器元素的操作

| 表达式 | 描述 |
|---|---|
| `vecList.at(index)` | 返回由 `index` 指定位置处的元素。 |
| `vecList[index]` | 返回由 `index` 指定位置处的元素。 |
| `vecList.front()` | 返回第一个元素。（不检查容器是否为空。） |
| `vecList.back()` | 返回最后一个元素。（不检查容器是否为空。） |

从表 21-2 可以看出，vector 中的元素可以像在数组中一样进行处理。参见例 21-1。（回想一下，在 C++ 中，数组从位置 0 开始。类似地，vector 容器中的第一个元素位于位置 0。）

### 例 21-1

考虑以下语句，它声明 `intList` 为一个大小为 5、元素类型为 `int` 的 vector 容器：

```cpp
vector<int> intList(5);
```

可以使用如下循环将元素存储到 `intList` 中：

```cpp
for (int j = 0; j < 5; j++)
    intList[j] = j;
```

类似地，可以使用 `for` 循环输出 `intList` 的元素。

类 vector 还包含成员函数，可用于查找容器中当前元素的数量、可插入容器的最大元素数量等。表 21-3 描述了其中一些操作。函数名以粗体显示。（假设 `vecCont` 是一个 vector 容器。）

**表 21-3** 确定 vector 容器大小的操作

| 表达式 | 描述 |
|---|---|
| `vecCont.capacity()` | 返回在不重新分配内存的情况下，可插入容器 `vecCont` 的最大元素数。 |
| `vecCont.empty()` | 如果容器 `vecCont` 为空，则返回 true；否则返回 false。 |
| `vecCont.size()` | 返回容器 `vecCont` 中当前元素的数量。 |
| `vecCont.max_size()` | 返回可插入容器 `vecCont` 的最大元素数。 |

类 vector 还包含成员函数，这些函数可用于操作 vector 容器中的数据，以及插入和删除项。假设 `vecList` 是 vector 类型的容器。`vecList` 中的项插入和删除通过表 21-4 给出的操作完成。这些操作实现为类 vector 的成员函数，并以粗体显示。表 21-4 还展示了如何使用这些操作。

**表 21-4** vector 容器的各种操作

| 语句 | 作用 |
|---|---|
| `vecList.clear()` | 删除容器中的所有元素。 |
| `vecList.erase(position)` | 删除由 position 指定位置处的元素。 |
| `vecList.erase(beg, end)` | 删除从 beg 开始直到 end-1 的所有元素。 |
| `vecList.insert(position, elem)` | 在由 position 指定的位置插入 elem 的一个副本。返回新元素的位置。 |
| `vecList.insert(position, n, elem)` | 在由 position 指定的位置插入 elem 的 n 个副本。 |
| `vecList.insert(position, beg, end)` | 将从 beg 开始直到 end-1 的元素的副本插入到 `vecList` 中由 position 指定的位置。 |
| `vecList.push_back(elem)` | 将 elem 的一个副本插入到 `vecList` 的末尾。 |
| `vecList.pop_back()` | 删除最后一个元素。 |
| `vecList.resize(num)` | 将元素数量改为 num。如果 `size()` 增加，则默认构造函数创建新元素。 |
| `vecList.resize(num, elem)` | 将元素数量改为 num。如果 `size()` 增加，则新元素是 elem 的副本。 |

> **注意**
>
> 在表 21-4 中，STL 术语中的标识符 `position`、`beg` 和 `end` 称为迭代器。迭代器就像指针。通常，迭代器用于遍历容器中的元素。换言之，借助迭代器，我们可以遍历容器中的元素并逐个处理它们。由于迭代器是 STL 的组成部分，本章后面“迭代器”一节将讨论它们。

例 21-1 使用 `for` 循环和数组下标运算符 `[]` 来访问 `intList` 的元素。我们声明 `intList` 为一个大小为 5 的 vector 对象。这是否意味着我们只能在 `intList` 中存储五个元素？答案是否定的。事实上，我们可以向 `intList` 添加更多元素。然而，因为声明 `intList` 时指定其大小为 5，为了添加位置 4 之后的元素，我们使用函数 `push_back`。此外，如果我们最初声明一个 vector 对象并且不指定其大小，那么要向该 vector 对象添加元素，我们使用函数 `push_back`。例 21-2 说明了如何使用函数 `push_back`。

### 例 21-2

以下语句声明 `intList` 为一个大小为 0 的 vector 对象：

```cpp
vector<int> intList;
```

要向 `intList` 添加元素，可以按如下方式使用函数 `push_back`：

```cpp
intList.push_back(34);
intList.push_back(55);
```

这些语句执行后，`intList` 的大小为 2，并且：

```cpp
intList = {34, 55}
```

在例 21-2 中，因为 `intList` 被声明为大小为 0，所以我们使用函数 `push_back` 向 `intList` 添加元素。然而，我们也可以使用 `resize` 函数增大 `intList` 的大小，然后使用数组下标运算符。例如，假设 `intList` 如例 21-2 中那样声明。那么，以下语句将 `intList` 的大小设置为 10：

```cpp
intList.resize(10);
```

类似地，以下语句将 `intList` 的大小增加 10：

```cpp
intList.resize(intList.size() + 10);
```

然而，有时 `push_back` 函数更方便，因为它不需要知道 vector 的大小；它只是将元素添加到末尾。

接下来，我们描述如何在 vector 容器中声明迭代器。

## 声明指向 vector 容器的迭代器

`class vector` 包含一个 `typedef iterator`，它被声明为 `public` 成员。指向 vector 容器的迭代器使用 `typedef iterator` 声明。例如，以下语句：

```cpp
vector<int>::iterator intVecIter;
```

声明 `intVecIter` 为 `int` 类型 vector 容器中的迭代器。

