

# 通用编程 1023

与本章中的大多数示例一样，列表 16.13 中的代码在处理 `std` 命名空间时采用了偷懒的方法：

```
using namespace std;
```

这样做是为了简化演示。示例使用了大量的指令或作用域解析运算符的 `std` 命名空间元素，这会让代码看起来有些繁琐：

```
std::set<std::string> B(s2, s2 + N);
std::ostream_iterator<std::cout, char> out(std::cout, " ");
std::cout << "Set A";
std::copy(A.begin(), A.end(), out);
```

# multimap 示例

与 `set` 来说，`multimap` 是可逆的、排序的关联容器。然而，对于 `multimap`，键类型不同于值类型，一个 `multimap` 对象可以与特定的键关联多个值。

基础的 `multimap` 通过模板参数指定键类型和值的类型。例如，以下声明创建了一个使用 `int` 作为键类型、使用 `string` 作为存储的值类型的 `multimap` 对象：

```
multimap<int, string> codes;
```

可以使用可选的模板参数来指定比较函数或用于排序的键对象。默认情况下使用 `less<>` 模板（稍后会讨论），并将键类型作为其参数。较旧的 C++ 实现可能需要显式地指定此模板参数。

为了将信息整合在一起，实际的值类型将键类型和数据封装进单个 `pair` 中。为了实现这一点，STL 使用 `pair<class T, U>` 模板类在单个对象中存储两种值。`keytype` 是键类型，`datatype` 是存储数据的类型，而值类型是 `pair<const keytype, datatype>`。例如，之前声明的 `codes` 对象的值类型为 `pair<const int, string>`。

假设你想存储城市名称，并使用区号作为键。这恰好符合该声明，该声明使用 `int` 作为键，使用 `string` 作为数据类型。一种方法是创建一个 `pair` 并将其插入到 `multimap` 对象中：

```cpp
pair<const int, string> item(213, "Los Angeles");
codes.insert(item);
```

或者你也可以创建一个匿名 `pair` 对象并在一条语句中插入它：
```
codes.insert(pair<const int, string> (213, "Los Angeles"));
```

由于项是按键排序的，因此不需要标识插入位置。

# 第 16 章字符串类与标准模板库

给定一个 `pair` 对象，你可以通过 `first` 和 `second` 成员访问其两个组件：

```cpp
pair<const int, string> item(213, "Los Angeles");
cout << item.first << ' ' << item.second << endl;
```

获取 `multimap` 对象的信息该怎么办？`count()` 成员函数接受键作为参数并返回该键拥有的项数。`lower_bound()` 和 `upper_bound()` 成员函数接受键作为工作，作用与 `set` 相同。`equal_range()` 成员函数接受键作为参数并返回表示匹配该范围的迭代器。为了返回两个值，该方法将它们封装成一个 `pair` 对象，此时两个模板参数都是迭代器类型。例如，以下代码将打印 `codes` 中区号为 718 的城市列表：

```cpp
pair<multimap<KeyType, string>::iterator,
multimap<KeyType, string>::iterator>
range = codes.equal_range(718);
cout << "Cities with area code 718:\n";
std::multimap<KeyType, std::string>::iterator it;
for (auto it = range.first; it != range.second; ++it)
cout << (*it).second << endl;
```

像这样的声明有助于 C++11 自动类型推导功能的产生，允许你如下所示简化代码：

```cpp
auto range = codes.equal_range(718);
cout << "Cities with area code 718:\n";
for (auto it = range.first; it != range.second; ++it)
cout << (*it).second << endl;
```

列表 16.14 展示了大部分这些技术。它还使用了 `typedef` 来简化部分代码编写。

# 列表 16.14 multimap.cpp

```cpp
// multimap.cpp -- use a multimap
#include <iostream>
#include <string>
#include <map>
#include <algorithm>

typedef int KeyType; typedef std::pair<const KeyType, std::string> Pair;
typedef std::multimap<KeyType, std::string> MapCode;

int main()
{
```

# 通用编程 1025

```cpp
using namespace std;
MapCode codes;

```cpp
codes.insert(Pair(415, "San Francisco"));
codes.insert(Pair(510, "Oakland"));
codes.insert(Pair(718, "Brooklyn"));
codes.insert(Pair(718, "Staten Island"));
codes.insert(Pair(415, "San Rafael"));
codes.insert(Pair(510, "Berkeley"));

cout << "Number of cities with area code 415: "
<< codes.count(415) << endl;
cout << "Number of cities with area code 718: "
<< codes.count(718) << endl;
cout << "Number of cities with area code 510: "
<< codes.count(510) << endl;
cout << "Area Code City\n";
MapCode::iterator it;
for (it = codes.begin(); it != codes.end(); ++it)
cout << " " << (*it).first << " "
<< (*it).second << endl;
```

```cpp
pair<MapCode, MapCode::iterator> range
 = codes.equal_range(718);
cout << "Cities with area code 718:\n";
for (it = range.first; it != range.second; ++it)
cout << " " << (*it).second << endl;
```

```cpp
return 0;
}
```

这是列表 16.14 的输出：

```
Number of cities with area code 415: 2
Number of cities with area code 718: 2
Number of cities with area code 510: 2
Area Code City
415 San Francisco
415 San Rafael
510 Oakland
510 Berkeley
718 Brooklyn
718 Staten Island
Cities with area code 718:
```

# 无序关联容器

关联容器按其键排序。然而，对于 `multimap`，键类型不同于值类型，一个 `multimap` 对象可以与特定的键关联多个值。

基础的 `multimap` 通过模板参数指定键类型和值的类型。例如，以下声明创建了一个使用 `int` 作为键类型、使用 `string` 作为存储的值类型的 `multimap` 对象：

```cpp
multimap<int, string> codes;
```

可以使用可选的模板参数来指定比较函数或用于排序的键对象。默认情况下使用 `less<>` 模板（稍后会讨论），并将键类型作为其参数。较旧的 C++ 实现可能需要显式地指定此模板参数。

为了将信息整合在一起，实际的值类型将键类型和数据封装进单个 `pair` 中。为了实现这一点，STL 使用 `pair<class T, U>` 模板类在单个对象中存储两种值。`keytype` 是键类型，`datatype` 是存储数据的类型，而值类型是 `pair<const keytype, datatype>`。例如，之前声明的 `codes` 对象的值类型为 `pair<const int, string>`。

假设你想存储城市名称，并使用区号作为键。这恰好符合该声明，该声明使用 `int` 作为键，使用 `string` 作为数据类型。一种方法是创建一个 `pair` 并将其插入到 `multimap` 对象中：

```cpp
pair<const int, string> item(213, "Los Angeles");
codes.insert(item);
```

或者你也可以创建一个匿名 `pair` 对象并在一条语句中插入它：
```
codes.insert(pair<const int, string> (213, "Los Angeles"));
```

由于项是按键排序的，因此不需要标识插入位置。

给定一个 `pair` 对象，你可以通过 `first` 和 `second` 成员访问其两个组件：

```cpp
pair<const int, string> item(213, "Los Angeles");
cout << item.first << ' ' << item.second << endl;
```

获取 `multimap` 对象的信息该怎么办？`count()` 成员函数接受键作为参数并返回该键拥有的项数。`lower_bound()` 和 `upper_bound()` 成员函数接受键作为工作，作用与 `set` 相同。`equal_range()` 成员函数接受键作为参数并返回表示匹配该范围的迭代器。为了返回两个值，该方法将它们封装成一个 `pair` 对象，此时两个模板参数都是迭代器类型。例如，以下代码将打印 `codes` 中区号为 718 的城市列表：

```cpp
pair<multimap<KeyType, string>::iterator,
multimap<KeyType, string>::iterator>
range = codes.equal_range(718);
cout << "Cities with area code 718:\n";
std::multimap<KeyType, std::string>::iterator it;
for (auto it = range.first; it != range.second; ++it)
cout << (*it).second << endl;
```

像这样的声明有助于 C++11 自动类型推导功能的产生，允许你如下所示简化代码：

```cpp
auto range = codes.equal_range(718);
cout << "Cities with area code 718:\n";
for (auto it = range.first; it != range.second; ++it)
cout << (*it).second << endl;
```

列表 16.14 展示了大部分这些技术。它还使用了 `typedef` 来简化部分代码编写。

# 列表 16.14 multimap.cpp

```cpp
// multimap.cpp -- use a multimap
#include <iostream>
#include <string>
#include <map>
#include <algorithm>

typedef int KeyType; typedef std::pair<const KeyType, std::string> Pair;
typedef std::multimap<KeyType, std::string> MapCode;

int main()
{
```

```cpp
codes.insert(Pair(415, "San Francisco"));
codes.insert(Pair(510, "Oakland"));
codes.insert(Pair(718, "Brooklyn"));
codes.insert(Pair(718, "Staten Island"));
codes.insert(Pair(415, "San Rafael"));
codes.insert(Pair(510, "Berkeley"));

cout << "Number of cities with area code 415: "
<< codes.count(415) << endl;
cout << "Number of cities with area code 718: "
<< codes.count(718) << endl;
cout << "Number of cities with area code 510: "
<< codes.count(510) << endl;
cout << "Area Code City\n";
MapCode::iterator it;
for (it = codes.begin(); it != codes.end(); ++it)
cout << " " << (*it).first << " "
<< (*it).second << endl;
```

```cpp
pair<MapCode, MapCode::iterator> range
 = codes.equal_range(718);
cout << "Cities with area code 718:\n";
for (it = range.first; it != range.second; ++it)
cout << " " << (*it).second << endl;
```

```cpp
return 0;
}
```

# 无序关联容器

关联容器不是按键排序的。相反，它们使用哈希函数将键映射到一个整数，该整数用于在桶数组中找到相应的索引。C++11 引入了 `unordered_map`、`unordered_multimap`、`unordered_set` 和 `unordered_multiset`。如果多个键哈希到同一个索引，就会发生冲突，容器使用链地址或开放寻址法来处理这种情况。无序容器在接口上与有序容器相似，但不维护元素的排序顺序。元素的顺序是不可预测的，并会随着插入和删除而改变。

# 函数对象（仿函数）

关联容器按键排序。然而，对于 `multimap`，键类型不同于值类型，一个 `multimap` 对象可以与特定的键关联多个值。

基础的 `multimap` 通过模板参数指定键类型和值的类型。例如，以下声明创建了一个使用 `int` 作为键类型、使用 `string` 作为存储的值类型的 `multimap` 对象：

```cpp
multimap<int, string> codes;
```

可以使用可选的模板参数来指定比较函数或用于排序的键对象。默认情况下使用 `less<>` 模板（稍后会讨论），并将键类型作为其参数。较旧的 C++ 实现可能需要显式地指定此模板参数。

为了将信息整合在一起，实际的值类型将键类型和数据封装进单个 `pair` 中。为了实现这一点，STL 使用 `pair<class T, U>` 模板类在单个对象中存储两种值。`keytype` 是键类型，`datatype` 是存储数据的类型，而值类型是 `pair<const keytype, datatype>`。例如，之前声明的 `codes` 对象的值类型为 `pair<const int, string>`。

假设你想存储城市名称，并使用区号作为键。这恰好符合该声明，该声明使用 `int` 作为键，使用 `string` 作为数据类型。一种方法是创建一个 `pair` 并将其插入到 `multimap` 对象中：

```cpp
pair<const int, string> item(213, "Los Angeles");
codes.insert(item);
```

或者你也可以创建一个匿名 `pair` 对象并在一条语句中插入它：
```
codes.insert(pair<const int, string> (213, "Los Angeles"));
```

由于项是按键排序的，因此不需要标识插入位置。

给定一个 `pair` 对象，你可以通过 `first` 和 `second` 成员访问其两个组件：

```cpp
pair<const int, string> item(213, "Los Angeles");
cout << item.first << ' ' << item.second << endl;
```

获取 `multimap` 对象的信息该怎么办？`count()` 成员函数接受键作为参数并返回该键拥有的项数。`lower_bound()` 和 `upper_bound()` 成员函数接受键作为工作，作用与 `set` 相同。`equal_range()` 成员函数接受键作为参数并返回表示匹配该范围的迭代器。为了返回两个值，该方法将它们封装成一个 `pair` 对象，此时两个模板参数都是迭代器类型。例如，以下代码将打印 `codes` 中区号为 718 的城市列表：

```cpp
pair<multimap<KeyType, string>::iterator,
multimap<KeyType, string>::iterator>
range = codes.equal_range(718);
cout << "Cities with area code 718:\n";
std::multimap<KeyType, std::string>::iterator it;
for (auto it = range.first; it != range.second; ++it)
cout << (*it).second << endl;
```

像这样的声明有助于 C++11 自动类型推导功能的产生，允许你如下所示简化代码：

```cpp
auto range = codes.equal_range(718);
cout << "Cities with area code 718:\n";
for (auto it = range.first; it != range.second; ++it)
cout << (*it).second << endl;
```

列表 16.14 展示了大部分这些技术。它还使用了 `typedef` 来简化部分代码编写。

# 列表 16.14 multimap.cpp

```cpp
// multimap.cpp -- use a multimap
#include <iostream>
#include <string>
#include <map>
#include <algorithm>

typedef int KeyType; typedef std::pair<const KeyType, std::string> Pair;
typedef std::multimap<KeyType, std::string> MapCode;

int main()
{
```

```cpp
codes.insert(Pair(415, "San Francisco"));
codes.insert(Pair(510, "Oakland"));
codes.insert(Pair(718, "Brooklyn"));
codes.insert(Pair(718, "Staten Island"));
codes.insert(Pair(415, "San Rafael"));
codes.insert(Pair(510, "Berkeley"));

cout << "Number of cities with area code 415: "
<< codes.count(415) << endl;
cout << "Number of cities with area code 718: "
<< codes.count(718) << endl;
cout << "Number of cities with area code 510: "
<< codes.count(510) << endl;
cout << "Area Code City\n";
MapCode::iterator it;
for (it = codes.begin(); it != codes.end(); ++it)
cout << " " << (*it).first << " "
<< (*it).second << endl;
```

```cpp
pair<MapCode, MapCode::iterator> range
 = codes.equal_range(718);
cout << "Cities with area code 718:\n";
for (it = range.first; it != range.second; ++it)
cout << " " << (*it).second << endl;
```

```cpp
return 0;
}
```

