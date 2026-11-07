
## 容器类型

容器用于管理给定类型的对象。STL 容器分为以下三类：

- 顺序容器（也称为序列容器）
- 关联容器
- 容器适配器

## 顺序容器

顺序容器中的每个对象都有一个特定位置。三种预定义的顺序容器是：

- vector
- deque
- list

在一般性地讨论容器类型之前，让我们先简要描述顺序容器 vector。我们这样做是因为 vector 容器与数组类似，因此可以像数组一样处理。此外，借助 vector 容器，我们可以描述所有容器共有的一些属性。事实上，所有容器对常见操作使用相同的名称。当然，也有一些操作是特定容器所特有的，这些将在描述特定容器时讨论。

## 顺序容器：vector

vector 容器在动态数组中存储和管理其对象。由于数组是随机访问数据结构，因此可以随机访问 vector 的元素。在数组中间或开头插入元素很耗时，尤其是当数组很大时。但是，在末尾插入元素相当快。

实现 vector 容器的类名是 `vector`。（回忆一下，容器是类模板。）包含类 `vector` 的头文件名是 `vector`。因此，要在程序中使用 `vector` 容器，程序必须包含以下语句：

```cpp
#include <vector>
```

此外，要定义 `vector` 类型的对象，我们必须指定对象的类型，因为类 `vector` 是类模板。例如，语句：

```cpp
vector<int> intList;
```

声明 `intList` 是一个 vector，并且组件类型为 `int`。类似地，语句：

```cpp
vector<string> stringList;
```

声明 `stringList` 是一个 vector 容器，并且组件类型为 `string`。

### 声明 vector 对象

vector 类包含多个构造函数，包括默认构造函数。因此，可以通过多种方式声明和初始化 vector 容器。表 22–1 描述了如何声明和初始化特定类型的 vector 容器。

**表 22-1  声明和初始化 vector 容器的各种方式**

| 语句 | 效果 |
|---|---|
| `vector<elemType> vecList;` | 创建空的 vector 容器 `vecList`。（调用默认构造函数。） |
| `vector<elemType> vecList(otherVecList);` | 创建 vector 容器 `vecList`，并将 `vecList` 初始化为 vector `otherVecList` 的元素。`vecList` 和 `otherVecList` 类型相同。 |
| `vector<elemType> vecList(size);` | 创建大小为 `size` 的 vector 容器 `vecList`。`vecList` 使用默认构造函数初始化。 |
| `vector<elemType> vecList(n, elm);` | 创建大小为 `n` 的 vector 容器 `vecList`。`vecList` 使用元素 `elm` 的 `n` 个副本初始化。 |
| `vector<elemType> vecList(beg, end);` | 创建 vector 容器 `vecList`。`vecList` 初始化为范围 `[beg, end)` 中的元素，即范围 `beg...end-1` 中的所有元素。`beg` 和 `end` 都是指针，在 STL 术语中称为迭代器。（本章后面将解释如何使用迭代器。） |

现在我们已经知道如何声明 vector 顺序容器，接下来讨论如何操作存储在 vector 容器中的数据。为了操作 vector 容器中的数据，我们必须了解以下基本操作：

- 元素插入
- 元素删除
- 遍历 vector 容器的元素

可以使用表 22-2 中给出的操作直接访问 vector 容器中的元素。函数名以粗体显示。

**表 22-2  访问 vector 容器元素的操作**

| 表达式 | 描述 |
|---|---|
| `vecList.at(index)` | 返回由 *索引* 指定的位置处的元素。 |
| `vecList[index]` | 返回由 *索引* 指定的位置处的元素。 |
| `vecList.front()` | 返回第一个元素。（不检查容器是否为空。） |
| `vecList.back()` | 返回最后一个元素。（不检查容器是否为空。） |

从表 22-2 可以看出，vector 中的元素可以像在数组中一样处理。参见例 22-1。（回忆一下，在 C++ 中，数组从位置 0 开始。类似地，vector 容器中的第一个元素位于位置 0。）

### 例 22-1

考虑以下语句，它声明 `intList` 是一个大小为 5、元素类型为 `int` 的 vector 容器。

```cpp
vector<int> intList(5);
```

可以使用如下循环将元素存储到 intList 中。

```cpp
for (int j = 0; j < 5; j++)
    intList[j] = j;
```

类似地，可以使用 for 循环输出 intList 的元素。

**vector 类**还包含成员函数，可用于查找容器中当前元素的数量、可插入容器的最大元素数量等。表 22–3 描述了其中一些操作。函数名以粗体显示。（假设 vecCont 是一个 vector 容器。）

**表 22-3  确定 vector 容器大小的操作**

| 表达式 | 描述 |
|---|---|
| `vecCont.capacity()` | 返回无需重新分配即可插入容器 vecCont 的最大元素数。 |
| `vecCont.empty()` | 如果容器 vecCont 为空，则返回 `true`，否则返回 `false`。 |
| `vecCont.size()` | 返回容器 vecCont 中当前元素的数量。 |
| `vecCont.max_size()` | 返回可插入容器 vecCont 的最大元素数。 |

**vector 类**还包含成员函数，可用于操作 vector 容器中的数据以及插入和删除元素。假设 vecList 是一个 vector 类型的容器。vecList 中的元素插入和删除通过表 22–4 中给出的操作完成。这些操作作为 vector 类的成员函数实现，并以粗体显示。表 22–4 还展示了这些操作的用法。

**表 22-4  vector 容器的各种操作**

| 语句 | 效果 |
|---|---|
| `vecList.clear()` | 从容器中删除所有元素。 |
| `vecList.erase(position)` | 删除由 `position` 指定位置处的元素。 |
| `vecList.erase(beg, end)` | 删除从 `beg` 开始直到 `end-1` 的所有元素。 |
| `vecList.insert(position, elem)` | 在由 `position` 指定的位置插入 `elem` 的一个副本。返回新元素的位置。 |
| `vecList.insert(position, n, elem)` | 在由 `position` 指定的位置插入 `elem` 的 `n` 个副本。 |
| `vecList.insert(position, beg, end)` | 将从 `beg` 开始直到 `end-1` 的元素的副本插入到 `vecList` 中由 `position` 指定的位置。 |
| `vecList.push_back(elem)` | 将 `elem` 的一个副本插入到 `vecList` 的末尾。 |
| `vecList.pop_back()` | 删除最后一个元素。 |
| `vecList.resize(num)` | 将元素数量改为 `num`。如果 size() 增加，则默认构造函数创建新元素。 |
| `vecList.resize(num, elem)` | 将元素数量改为 `num`。如果 size() 增加，则新元素是 `elem` 的副本。 |

**注意** 在表 22-4 中，STL 术语中的标识符 `position`、`beg` 和 `end` 称为迭代器。迭代器就像指针一样。一般来说，迭代器用于遍历容器的元素。换句话说，借助迭代器，我们可以遍历容器的元素并逐个处理它们。由于迭代器是 STL 不可或缺的一部分，因此将在本章后面“迭代器”一节中讨论。
