
## `typedef CONST_ITERATOR`

因为迭代器的工作方式类似指针，借助指向容器的迭代器和解引用运算符 `*`，我们可以修改容器中的元素。然而，如果容器被声明为 const，那么我们必须防止迭代器修改容器中的元素，尤其是意外修改。为了处理这种情况，每个容器都包含另一个 `typedef const_iterator`。例如，以下语句：

```cpp
vector<int>::const_iterator intConstVecIt;
```

声明 intConstVecIt 为一个指向 vector 容器的迭代器，该容器的元素类型为 int。迭代器 intConstVecIt 用于处理那些被声明为 `vector<int>` 类型的常量 vector 容器的元素。

`const_iterator` 类型的迭代器是只读迭代器。

## `typedef REVERSE_ITERATOR`

每个容器还包含 typedef reverse_iterator。这种类型的迭代器用于反向遍历容器中的元素。

## `typedef CONST_REVERSE_ITERATOR`

这种类型的迭代器是只读迭代器，用于反向遍历容器中的元素。如果容器被声明为 const，并且我们需要反向遍历容器中的元素，就需要使用它。

除了前面的四个 typedef 之外，还有几个其他 typedef 是所有容器共有的，表 21-16 对它们进行了说明。

### 表 21-16 所有容器共有的各种 typedef

| typedef | 作用 |
|---|---|
| `difference_type` | 两个指向同一容器的迭代器相减所得结果的类型。 |
| `pointer` | 指向容器中所存储元素类型的指针。 |
| `reference` | 对容器中所存储元素类型的引用。 |
| `const_reference` | 对容器中所存储元素类型的常量引用。常量引用是只读的。 |
| `size_type` | 用于对容器中元素进行计数的类型。该类型也用于对序列容器（list 容器除外）进行索引。 |
| `value_type` | 容器元素的类型。 |

## 流迭代器

另一组有用的迭代器是流迭代器——istream 迭代器和 ostream 迭代器。本节介绍这两种迭代器。

### istream_iterator

istream 迭代器用于从输入流向程序输入数据。类 istream_iterator 包含输入流迭代器的定义。使用 istream 迭代器的一般语法是：

```cpp
istream_iterator<Type> isIdentifier(istream&);
```

其中 Type 是内置类型或用户定义的类类型，并且为其定义了输入迭代器。标识符 isIdentifier 使用构造函数进行初始化，该构造函数的参数是 istream 类对象（例如 cin）或任何公开定义的 istream 子类型（例如 ifstream）。

### ostream_iterator

ostream 迭代器用于将程序中的数据输出到输出流。这些迭代器在本章前面已经定义过。为了完整性，我们在这里回顾它们。

类 ostream_iterator 包含输出流迭代器的定义。使用 ostream 迭代器的一般语法是：

```cpp
ostream_iterator<Type> osIdentifier(ostream&);
```

或者：

```cpp
ostream_iterator<Type> osIdentifier(ostream&, char* deLimit);
```

其中 Type 是内置类型或用户定义的类类型，并且为其定义了输出迭代器。标识符 osIdentifier 使用构造函数进行初始化，该构造函数的参数是 ostream 类对象（例如 cout）或任何公开定义的 ostream 子类型（例如 ofstream）。在用于声明 ostream 迭代器的第二种形式中，通过使用初始化构造函数的第二个参数（分隔符），我们可以指定一个用于分隔输出的字符。

## 关联容器

本节讨论关联容器。关联容器中的元素会根据某种排序准则自动排序。默认的排序准则是关系运算符 <（小于）。用户也可以选择指定自己的排序准则。

由于关联容器中的元素会自动排序，因此当向容器中插入新元素时，它会插入到合适的位置。实现这类数据结构的一种方便而快速的方法是使用二叉搜索树。事实上，关联容器就是这样实现的。因此，容器中的每个元素都有一个父节点（根节点除外），并且至多有两个子节点。对于每个元素，父节点中的键大于左子节点中的键，并且小于右子节点中的键。

STL 中预定义的关联容器有：

- 集合（set）
- 多重集合（multiset）
- 映射（map）
- 多重映射（multimap）

本书只讨论关联容器 set 和 multiset。

### 关联容器：set 和 multiset

如前所述，容器 set 和 multiset 都会根据某种排序准则自动对其元素排序。默认的排序准则是关系运算符 <（小于）；也就是说，元素按升序排列。用户也可以指定其他排序准则。对于用户定义的数据类型（例如类），必须正确重载关系运算符。

容器 set 和 multiset 之间的唯一区别是：容器 multiset 允许重复元素，而容器 set 不允许。

定义容器 set 的类名是 set；定义容器 multiset 的类名是 multiset。包含类 set 和 multiset 的定义，以及用于实现这些容器各种操作的函数定义的头文件名是 set。因此，要使用这些容器中的任意一个，程序必须包含以下语句：

```cpp
#include <set>
```

### 声明 set 或 multiset 关联容器

类 set 和 multiset 包含多个构造函数，用于声明并初始化这些类型的容器。本节讨论声明和初始化这些类型关联容器的各种方式。表 21-17 说明了如何声明和初始化特定类型的 set/multiset 容器。

```cpp
set<int> intSet;                                      //Line 1
set<int, greater<int> > otherIntSet;                  //Line 2
multiset<string> multiStringMultiSet;                 //Line 3
multiset<string, greater<string> > otherStringMultiSet; //Line 4
```

第 1 行语句将 intSet 声明为一个空 set 容器，元素类型为 int，排序准则为默认排序准则。第 2 行语句将 otherIntSet 声明为一个空 set 容器，元素类型为 int，排序准则为大于。也就是说，容器 otherIntSet 中的元素将按降序排列。第 3 行和第 4 行语句具有类似的约定。

函数 greater 定义在头文件 functional 中。该头文件中的其他函数及其用途将在本章后面的“函数对象”一节中讨论。

第 2 行和第 4 行语句说明了如何指定降序排序准则。

> **注意**
>
> 在第 2 行和第 4 行语句中，请注意两个 > 符号之间的空格——即 `greater<int>` 和 `>` 之间的空格。如果使用的是旧编译器，那么这个空格很重要，因为 `>>` 在 C++ 中也是移位运算符。不过，C++11 中已经取消了这一限制，并且本书编写程序所使用的编译器已经实现了该特性。因此，在 C++11 中，第 2 行和第 4 行语句可以写成：
>
> ```cpp
> set<int, greater<int>> otherIntSet;                    //Line 2
> multiset<string, greater<string>> otherStringMultiSet; //Line 4
> ```

### 从 `set/multiset` 插入和删除元素

假设 `ct` 的类型为 `set` 或 `multiset`。表 21-18 描述了可用于从 set 中插入或删除元素的操作，还说明了如何使用这些操作。函数名以粗体显示。

### 表 21-18 — 从 Set 插入或删除元素的操作

| 表达式 | 作用 |
|---|---|
| `ct.insert(elem)` | 将 `elem` 的副本插入 `ct`。对于 set，它还返回插入操作是否成功。 |
| `ct.insert(position, elem)` | 将 `elem` 的副本插入 `ct`。返回插入 `elem` 的位置。第一个参数 `position` 提示从何处开始搜索插入位置。参数 `position` 是一个迭代器。 |
| `ct.insert(beg, end);` | 将从位置 `beg` 开始直到 `end-1` 的所有元素的副本插入 `ct`。`beg` 和 `end` 都是迭代器。 |
