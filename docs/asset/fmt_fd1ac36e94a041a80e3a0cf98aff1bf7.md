
```cpp
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main() {
    // 定义一个电话簿 multimap
    multimap<string, string> phonebook = {
        {"Will", "555-1212"}, {"Will", "555-0123"},
        {"Faye", "555-0707"}, {"Faye", "555-1234"},
        {"Sarah", "555-8787"}, {"Sarah", "555-5678"}
    };

    // 定义一个对变量来接收
    // 从 equal_range 成员函数返回的对象
    pair<multimap<string, string>::iterator, multimap<string, string>::iterator> range;

    // 定义一个 multimap 的迭代器
    multimap<string, string>::iterator iter;

    // 获取匹配 "Faye" 的元素范围
    range = phonebook.equal_range("Faye");

    // 显示所有匹配 "Faye" 的元素
    for (iter = range.first; iter != range.second; iter++) {
        cout << iter->first << "\t" << iter->second << endl;
    }

    return 0;
}
```

| 程序输出 |
| :--- | :--- |
| Faye | 555-0707 |
| Faye | 555-1234 |

# 从 multimap 中删除元素

你可以使用 `erase()` 函数从 multimap 中删除或擦除元素。你可以调用 `erase()` 函数，并传递与要删除的元素关联的键。所有匹配指定键的元素都将从 multimap 中擦除。`erase()` 函数返回被删除的元素个数。以下代码展示了一个示例：

```cpp
// 定义一个电话簿。
multimap<string, string> phonebook = {
    {"Will", "555-0122"}, {"Will", "555-0123"},
    {"Faye", "555-0707"}, {"Faye", "555-1234"},
    {"Sarah", "555-8787"}, {"Sarah", "555-5678"}
};
```

```cpp
// 从 multimap 中删除 Will 的电话号码。
phonebook.erase("Will");
```

这段代码创建了一个包含六个元素的 multimap 容器。然后，它删除了所有键为 "Will" 的元素（删除了两个元素）。此时，multimap 只剩下四个元素。

# unordered_multimap 类

从 C++ 开始，STL 提供了一个名为 `unordered_multimap` 的类模板，它与 multimap 类相似，但有两个不同之处：(1) `unordered_multimap` 中的键不是按特定顺序排序的，(2) `unordered_multimap` 类具有更好的性能。如果你对大量元素进行大量搜索，并且不在意按键的顺序检索它们，那么你应该使用 `unordered_multimap` 类而不是 multimap 类。

要使用 `unordered_multimap` 类，你必须在程序中编写 `#include <unordered_multimap>` 指令。`unordered_multimap` 类拥有与 multimap 类类似的成员函数集，在大多数情况下，操作 `unordered_multimap` 就和操作 multimap 一样。

> 注意：`unordered_multimap` 类之间的差异在于每个类在内部存储元素的方式。`multimap` 类使用名为二叉树的数据结构，而 `unordered_multimap` 类使用哈希表。

# 检查点

- 17.20 存储在 map 中的每个元素都包含两个部分。它们是什么？
- 17.21 写出一条语句定义一个名为 `myMap` 的 map。`myMap` 中的键应该是 `int` 类型，值应该是 `string` 类型。
- 17.22 假设已经创建了一个名为 `employee` 的空 map。以下语句的作用是什么？
  `employee[543] = "Joanne Manchester";`
- 17.23 描述在 map 中通过特定键检索元素的两种方法。

# 17.5 set、multiset 和 unordered_set 类

- 17.24 如果你想将自己编写的类对象作为值存储在 map 中，你是否必须确保该类具有？
- 17.25 如果你想将自己编写的类对象作为键存储在 map 中，你是否必须确保该类具有？
- 17.26 `map` 和 `unordered_map` 之间的区别是什么？
- 17.27 `map` 和 `multimap` 之间的区别是什么？

# set、multiset 和 unordered_set 类

概念：set（集合）包含一个唯一值的集合。

set 是一种关联容器，它以类似于数学集合的方式存储一组唯一值。你使用 STL 模板 `set` 在 C++ 中实现 set 容器。关于 STL set 容器，有两点需要知道：

- set 中的所有元素必须是唯一的。任意两个元素不能具有相同的值。
- set 中的元素会自动按升序排序。

要使用 `set` 类，你需要在程序中包含 `<set>` 头文件。然后，你可以使用 `set` 类的其中一个构造函数来定义 `set` 对象。表 17-12 显示了使用每个构造函数定义 set 语句的通用格式。表 17-13 显示了 `set` 的许多（但不是所有）成员函数。

## 表 17-12 set 定义语句

| 构造函数类型 | 说明 |
| :--- | :--- |
| 默认构造函数 | `set<dataType> name;` 创建一个空的 set 对象。在通用格式中，`dataType` 是每个元素的数据类型，`name` 是 set 的名称。 |
| 范围构造函数 | `set<dataType> name(iterator1, iterator2);` 创建一个初始包含两个迭代器指定的值范围的 set 对象。在此通用格式中，`dataType` 是每个元素的数据类型，`iterator1` 和 `iterator2` 参数标记了将存储在 set 中的值范围的开始和结束（`iterator2` 标记的由 `iterator2` 指向的元素不会包含在范围内）。范围内的任何重复值将只添加到 set 中一次。 |
| 拷贝构造函数 | `set<dataType> name(set2);` 创建一个作为 `set2` 拷贝的 set 对象。 |

## 表 17-13 set 的成员函数

| 成员函数 | 描述 |
| :--- | :--- |
| `begin()` | 返回指向第一个元素的迭代器。 |
| `cbegin()` | 返回指向第一个元素的 const 迭代器。 |
| `end()` | 返回指向结束元素的容器。 |
| `clear()` | 擦除容器中的所有元素。 |
| `count(value)` | 返回指定 `value` 的个数。 |
| `crbegin()` | 返回指向最后一个元素的 const 迭代器。 |
| `crend()` | 返回指向结束元素的 const 迭代器。 |
| `emplace(args...)` | 在容器中构造新元素。 |
| `empty()` | 如果容器为空则返回 true，否则返回 false。 |
| `end()` | 返回指向结束元素的迭代器。 |
| `equal_range(value)` | 返回一对迭代器。 |
| `erase(value)` | 擦除指定 `value` 的元素。 |
| `find(value)` | 搜索元素，如果找到则返回迭代器。 |
| `insert(value)` | 将 `value` 插入 set。 |
| `lower_bound(value)` | 返回第一个不小于 `value` 的元素的迭代器。 |
| `max_size()` | 返回容器的最大容量。 |
| `rbegin()` | 返回指向最后一个元素的反向迭代器。 |
| `rend()` | 返回指向结束元素的反向迭代器。 |
| `size()` | 返回容器中元素的数量。 |
| `swap(second)` | 交换两个 set 的内容。 |
| `upper_bound(value)` | 返回第一个大于 `value` 的元素的迭代器。 |

# 第17章 标准模板库

## 17.5 set、multiset 和 unordered_set 类

这里是定义一个包含整数的 set 的示例：

```cpp
set<int> numbers;
```

该语句定义了一个容器。在尖括号 `<>` 中，数据类型 `int` 是每个元素的类型。你可以提供初始化列表来初始化 set，如下：

```cpp
set<int> numbers = {1, 2, 3, 4, 5};
```

这里是定义一个包含字符串的 set 的示例：

```cpp
set<string> names = {"Joe", "Karen", "Jackie"};
```

set 不能包含重复项，因此如果相同的值在初始化列表中出现多次，它会被添加到 set 中一次。例如，以下 set 将包含值 1, 2, 3, 4, 5：

```cpp
set<int> numbers = {1, 1, 2, 3, 3, 3, 4, 5};
```

# 向现有 set 添加元素

`set` 类提供了一个 `insert()` 成员函数向容器添加新元素。你可以简单地调用该成员函数，并将新元素的值作为参数。以下代码展示了一个示例：

```cpp
set<int> numbers;
numbers.insert(10);
numbers.insert(20);
numbers.insert(30);
```

第一个语句创建一个名为 `numbers` 的空 set 容器。后续语句将值 10、20 和 30 添加到 set 中。如果你插入的值已经于 set 中，`insert()` 成员函数将什么都不做（不会插入新元素）。

# 使用范围循环遍历 set

范围循环是遍历 set 中所有元素的一种方便方法。以下代码展示了如何显示 set 中的所有元素的示例：

```cpp
// 创建一个包含名字的 set。
set<string> names = {"Joe", "Karen", "Jackie"};

// 显示每个元素。
for (string element : names)
{
    cout << element << endl;
}
```

# 第 17 章 标准模板库

## 在 set 中使用迭代器

你可以使用双向迭代器来访问 set 中的元素。`set` 类提供了 `begin()` 和 `cbegin()` 成员函数，它们返回指向 set 中第一个元素的迭代器；以及 `end()` 和 `cend()` 成员函数，它们返回指向 set 末尾（最后一个元素之后）的迭代器。下面的代码展示了使用迭代器显示 set 中所有元素的示例：

```cpp
// 创建一个包含名称的 set。
set<string> names = {"Joe", "Karen", "Lisa", "Jackie"};

// 创建迭代器。
set<string>::iterator iter;

// 使用迭代器显示 set 中的每个元素。
for (iter = names.begin(); iter != names.end(); iter++) {
    cout << *iter;
}
```

> 注意：`end()` 和 `cend()` 成员函数返回的是指向 set 末尾的迭代器，并不指向实际元素。如果存在额外的元素，它指向所在的位置。

## 确定值是否存在于 set 中

你可以使用 `count()` 成员函数或 `find()` 成员函数来确定一个值是否存在于 set 中。`count()` 成员函数接受一个值作为参数，如果该值在 set 中则返回 1，否则返回 0。`find()` 函数接受一个值作为参数，如果在 set 中找到了，则返回指向该元素的迭代器；如果没有找到，则返回指向 set 末尾的迭代器。下面的代码是一个示例：

```cpp
// 创建包含名称的 set。
set<string> names = {"Joe", "Karen", "Lisa", "Jackie"};

// 创建迭代器。
set<string>::iterator iter;

// 查找 "Karen"。
iter = names.find("Karen");

// 显示结果。
if (iter != names.end())
{
    cout << *iter << " was found.\n";
}
else {
    cout << "Karen was not found.\n";
}
```

![](img/191adf328469956e6a7b1008ce9bdb5)

## 在 set 中存储自定义类对象

只要类重载了 `<` 运算符，你就可以在 set 中存储你编写的类对象。`set` 类使用 `<` 运算符来确定存储元素的顺序并检测重复项。（假设我们正在比较两个值 `value1` 和 `value2`。如果 `value1` 不小于 `value2` 且 `value2` 不小于 `value1`，则这两个值相等。）

例如，回本章较早讨论过的 `Customer` 类（参见 `Customer.h` 的内容）。`Customer` 类持有两个数据：客户编号和姓名。该类还重载了比较客户编号的运算符。如果在 set 容器中存储 `Customer` 对象，对象将按客户编号排序，容器不允许存储相同客户编号的对象。程序 17-22 演示了这一点。

## 程序 17-22

```cpp
#include <iostream>
#include <set>
#include "Customer.h"
using namespace std;

int main() {
  // 创建 Customer 对象的 set。
  set<Customer> customerset = {
    Customer(1003, "Megan Cruz"),
    Customer(1002, "Austin Hill"),
    Customer(1001, "Sarah Scott")
  };
  // 插入插入一个重复的客户编号。
  customerset.emplace(1001, "Evan Smith");
  // 显示 set 元素
  cout << "List of customers:\n";
  for (auto element : customerset) {
    cout << element.getCustomerNumber() << " " << element.getName() << endl;
  }
}
```

（程序继续）

## 程序 17-22（续）

### 程序输出

```text
List of customers:
1001 Sarah Scott
1002 Austin Hill
1003 Megan Cruz
```

查找客户编号 1002：

找到：Austin Hill

![](img/191adf328469956e6a7b1008ce9bdb5)

让我们仔细观察一下这个程序：

- 第 9 行到第 13 行定义了一个 set 容器 `customerset`。该容器初始化了三个 `Customer` 对象。
- 第 16 行调用 `emplace()` 成员函数向 set 添加一个 `Customer` 对象。然而，传递给 `emplace()` 函数的客户编号已经存在于 set 中。因此，该对象不会被添加到 set 中。
- 第 20 行到第 24 行的循环显示 set 容器的所有元素。在程序输出中，元素按客户编号的顺序被提取。
- 接下来，程序在 set 容器中查找客户编号为 1002 的对象。第 28 行的语句定义了一个迭代器，并将 `find()` 函数返回的值赋值。

仔细观察传递给 `find()` 成员函数的参数。表达式 `Customer(1002, "")` 构造了一个临时的无名 `Customer` 对象，其客户编号为 1002，姓名为 ""。（因为我们只是用它来查找编号为 1002 的元素，所以不需要为姓名提供有效值。）`find` 成员函数将接受此 `Customer` 对象作为参数，并在容器中搜索具有匹配编号的元素。（记住，set 容器使用 `Customer` 类重载的 `<` 运算符来判断两个对象是否相等。）如果找到了匹配的元素，函数返回指向该元素的迭代器。否则，它返回指向容器末尾的迭代器。

- 第 30 行到第 33 行的 `if/else` 语句确定迭代器是否指向匹配元素，还是容器的末尾，并显示搜索结果。

## multiset 类

`multiset` 类允许创建一个可以存储重复元素的集合。要使用 `multiset` 类，你需要在程序中包含 `<set>` 头文件。它提供了与 `set` 类相同的成员函数，但有两点不同：

- 在 `set` 类中，`count()` 成员函数返回 0 或 1。在 `multiset` 类中，`count()` 可以返回大于 1 的值。
- 在 `set` 类中，`equal_range()` 成员函数最多返回一个元素。在 `multiset` 类中，`equal_range()` 可以返回多个元素。

## unordered_set 和 unordered_multiset
