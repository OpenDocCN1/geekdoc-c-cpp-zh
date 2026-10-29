

## Display 19.11 The set Template Class
### set TEMPLATE CLASS DETAILS

类型名称：set<T> 或 set<T, Ordering> 表示一个由类型 T 的元素组成的集合。Ordering 用于对元素进行排序以便存储。如果未给出 Ordering，则使用的排序为二元运算符 <。库头文件：<set>，将其定义放在 std 命名空间中。已定义的类型包括 value_type、size_type。迭代器：iterator、const_iterator、reverse_iterator 和 const_reverse_iterator。所有迭代器都是双向的，且不包含 const_ 的迭代器是可变的。begin()、end()、rbegin() 和 rend() 具有预期的行为。添加或删除元素不会影响迭代器，除非迭代器位于被删除的元素处。

### SAMPLE MEMBER FUNCTIONS

| MEMBER FUNCTION (s IS A SET OBJECT) | MEANING |
|---|---|
| s.insert(Element) | 在集合中插入 Element 的副本。如果集合中已存在 Element，则此操作无效。 |
| s.erase(Element) | 从集合中移除 Element。如果集合中不存在 Element，则此操作无效。 |
| s.find(Element) | 返回位于集合中 Element 副本处的迭代器。如果集合中不存在 Element，则返回 s.end()。迭代器是否可变取决于实现。 |
| s.erase(Iterator) | 删除 Iterator 位置处的元素。 |
| s.size() | 返回集合中元素的数量。 |
| s.empty() | 如果集合为空则返回 true；否则返回 false。 |
| s1 == s2 | 如果两个集合包含相同的元素则返回 true；否则返回 false。 |

set 模板类还具有默认构造函数、拷贝构造函数以及此处未提及的其他专用构造函数。它也有析构函数，用于回收所有存储空间，并有一个行为良好的赋值运算符。

## Display 19.12 Program Using the set Template Class (part 1 of 2)

```
//Program to demonstrate use of the set template class.
#include <iostream>
#include <set>
using std::cout;
using std::endl;
using std::set;
```

Display 19.13 中给出了 map 模板类的一些基本细节。为了理解这些细节，你需要先了解一些关于 pair 模板类的知识。

## Display 19.13 The map Template Class
### map TEMPLATE CLASS DETAILS

类型名称：map<KeyType, T> 或 map<KeyType, T, Ordering> 表示一个将 KeyType 类型的元素映射到 T 类型元素的映射。Ordering 用于按键值对元素进行排序以实现高效存储。如果未给出 Ordering，则使用的排序为二元运算符 <。

库头文件：<map>，将其定义放在 std 命名空间中。

已定义的类型：包括 key_type 表示键值的类型，mapped_type 表示映射到的值的类型，以及 size_type。 （因此，已定义的类型 key_type 就是我们上面所说的 KeyType。）

迭代器：iterator、const_iterator、reverse_iterator 和 const_reverse_iterator。所有迭代器都是双向的。不包含 const 的迭代器既不是常量也不是可变的，而是介于两者之间。例如，如果 p 的类型为 iterator，则你可以更改键值但不能更改类型为 T 的值。也许最好，至少一开始，将所有迭代器都当作常量来对待。begin()、end()、rbegin() 和 rend() 具有预期的行为。添加或删除元素不会影响迭代器，除非迭代器位于被删除的元素处。

### SAMPLE MEMBER FUNCTIONS

| MEMBER FUNCTION (m IS A MAP OBJECT) | MEANING |
|---|---|
| m.insert(Element) | 在映射中插入 Element。Element 的类型为 pair<KeyType, T>。返回类型为 pair<iterator, bool> 的值。如果插入成功，则返回的 pair 的第二部分为 true，且迭代器位于插入的元素处。 |
| m.erase(Target_Key) | 删除键为 Target_Key 的元素。 |
| m.find(Target_Key) | 返回位于键值为 Target_Key 的元素处的迭代器。如果不存在此类元素，则返回 m.end()。 |
| m[Target_Key] | 返回与 Target_Key 关联的对象的引用。如果映射中尚不包含此类对象，则会插入一个类型为 T 的默认对象。 |
| m.size() | 返回映射中 pairs 的数量。 |
| m.empty() | 如果映射为空则返回 true；否则返回 false。 |
| m1 == m2 | 如果两个映射包含相同的 pairs 则返回 true；否则返回 false。 |

map 模板类还具有默认构造函数、拷贝构造函数以及此处未提及的其他专用构造函数。它也有析构函数，用于回收所有存储空间，并有一个行为良好的赋值运算符。

STL 模板类 `pair<T1, T2>` 具有值对对象，其中第一个元素为类型 `T1`，第二个为类型 `T2`。如果 `aPair` 是类型为 `pair<T1, T2>` 的对象，则 `aPair.first` 是第一个元素，其类型为 `T1`，而 `aPair.second` 是第二个元素，其类型为 `T2`。成员变量 `first` 和 `second` 是公有成员变量，因此不需要访问器或修改器函数。

pair 模板的头文件为 `<utility>`。因此，要使用 pair 模板类，你需要在文件中包含以下内容（或类似内容）：

```
```cpp
#include <utility>
using std::pair;
```
```

map 模板类使用 pair 模板类来存储键与数据项之间的关联。例如，给定定义

```
```cpp
map<string, int> numberMap;
```
```

如果我们向映射中添加

```
```cpp
numberMap["c++"] = 10;
```
```

那么当我们使用迭代器访问此 pair 时，`iterator->first` 将引用键 "c++"，而 `iterator->second` 将引用数据值 10。

一个简单的示例展示了如何使用 map 模板类的一些成员函数，给出在 Display 19.14 中。

我们将提及另外四个关联容器，但不会给出它们的任何细节。模板类 `multiset` 和 `multimap` 与 `set` 和 `map` 基本相同，只是 `multiset` 允许元素重复，而 `multimap` 允许每个键值关联多个值。一些 STL 实现还包括哈希集合和哈希映射类。这些模板类与 set 和 map 基本相同，只是它们使用哈希表实现。哈希表在第 17 章中描述。set 和 map 类的大多数实现使用平衡二叉树而不是哈希表。在平衡二叉树中，根左侧的节点数大致等于根右侧的节点数。二叉搜索树也在第 17 章中描述，尽管我们没有讨论平衡它们的细节。

### Efficiency

STL 实现力求达到最佳效率。例如，set 和 map 元素以排序顺序存储，因此搜索元素的算法可以更高效。

每个模板类的每个成员函数都有一个保证的最大运行时间。这些最大运行时间使用所谓的 *big-O notation* 表示，我们将在第 19.3 节讨论。 （第 19.3 节还给出了我们已经讨论过的一些容器成员函数的保证运行时间。）它们在标题为“Container Access Running Times”的小节中给出。你将在本章其余部分描述的某些函数中被告知其保证的最大运行时间。

## Display 19.14 Program Using the map Template Class (part 1 of 2)

```
```cpp
//Program to demonstrate use of the map template class.
#include <iostream>
#include <map>
#include <string>
using std::cout;
using std::endl;
using std::map;
using std::string;

int main( )
{
    map<string, string> planets;

    planets["Mercury"] = "Hot planet";
    planets["Venus"] = "Atmosphere of sulfuric acid";
    planets["Earth"] = "Home";
    planets["Mars"] = "The Red Planet";
    planets["Jupiter"] = "Largest planet in our solar system";
    planets["Saturn"] = "Has rings";
    planets["Uranus"] = "Tilts on its side";
    planets["Neptune"] = "1500 mile-per-hour winds";
    planets["Pluto"] = "Dwarf planet";

    cout << "Entry for Mercury - " << planets["Mercury"]
         << endl << endl;

    if (planets.find("Mercury") != planets.end( ) )
        cout << "Mercury is in the map." << endl;
    if (planets.find("Ceres") == planets.end( ) )
        cout << "Ceres is not in the map." << endl << endl;

    cout << "Iterating through all planets:" << endl;
    map<string, string>::const_iterator iter;
    for (iter = planets.begin( ); iter != planets.end( ); iter++)
    {
        cout << iter->first << " - " << iter->second << endl;
    }

    return 0;
}
```

> 迭代器将按键排序输出映射。在此情况下，输出将按行星名称的字母顺序列出。

### Sample Dialogue

```
```
Entry for Mercury - Hot planet

Mercury is in the map.
Ceres is not in the map.
Iterating through all planets:
Earth - Home
Jupiter - Largest planet in our solar system
```
```
