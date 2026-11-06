

如果键的顺序不重要，可以使用`unordered_multimap`（头文件`<unordered_map>`）代替。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1955_0.png)

### 性能提示 15.11

`multimap`的实现可以高效定位与给定键关联的所有值。

```cpp
// Fig. 15.17: fig15_17.cpp
// Standard Library multimap class template.
#include <iostream>
#include <map> // multimap class-template definition
using namespace std;

int main() {
   multimap<int, double, less<int>> pairs; // create multimap

   cout << "There are currently " << pairs.count(15)
      << " pairs with key 15 in the multimap\n";

   // insert two value-type objects in pairs
   pairs.insert(make_pair(15, 99.3));
   pairs.insert(make_pair(15, 2.7));

   cout << "After inserts, there are " << pairs.count(15)
      << " pairs with key 15\n\n";

   // insert five value-type objects in pairs
   pairs.insert(make_pair(30, 111.11));
   pairs.insert(make_pair(10, 22.22));
   pairs.insert(make_pair(25, 33.333));
   pairs.insert(make_pair(20, 9.345));
   pairs.insert(make_pair(5, 77.54));

   cout << "Multimap pairs contains:\nKey\tValue\n";

   // walk through elements of pairs
   for (auto mapItem : pairs)
      cout << mapItem.first << '\t' << mapItem.second << '\n';
}
```

There are currently 0 pairs with key 15 in the multimap  
After inserts, there are 2 pairs with key 15

Multimap pairs contains:

| Key | Value |
| --- | ---: |
| 5 | 77.54 |
| 10 | 22.22 |
| 15 | 99.3 |
| 15 | 2.7 |
| 20 | 9.345 |
| 25 | 33.333 |
| 30 | 111.11 |

图15.17 标准库`multimap`类模板。

第8行创建了一个`multimap`，其键类型是`int`，键关联值的类型是`double`，元素按*升序*排列——模板实参`less<int>`是默认排序；在`multimap`声明中不是必需的。第10行使用函数`count`确定键为`15`的键–值对数量（目前还没有，因为容器当前为空）。

第14行使用函数`insert`向`multimap`添加一个新的键–值对。标准库函数`make_pair`创建一个键–值`pair`对象——在本例中，`first`表示类型为`int`的键（`15`），`second`表示类型为`double`的值（`99.3`）。函数`make_pair`自动使用你在`multimap`声明（第8行）中为键和值指定的类型。第15行插入另一个键为`15`、值为`2.7`的`pair`对象。然后第17–18行输出键为`15`的对数。从C++11起，你可以对`pair`对象使用列表初始化，所以第15行可以简化为

```cpp
pairs.insert({15, 2.7});
```

类似地，你可以使用C++11列表初始化来初始化从函数返回的对象。例如，下面返回一个包含`int`和`double`的pair

```cpp
return {15, 2.7};
```

第21–25行向`multimap`中插入另外五个`pairs`。第30–32行的基于范围的`for`语句输出`multimap`的内容，包括键和值。我们用关键字`auto`推断循环控制变量的类型（一个包含`int`键和`double`值的`pair`）。第31行访问`multimap`每个元素中当前`pair`的成员。注意在输出中，键按*升序*出现。

### C++11：列表初始化键–值对容器

在本例中，我们使用了对成员函数insert的单独调用来将键–值对放入`multimap`。如果事先知道键–值对，可以在创建`multimap`时使用列表初始化。例如，下面的语句用三个键–值对初始化一个`multimap`，这些键–值对由主初始化列表中的子列表表示：

```cpp
multimap<int, double, less<int>> pairs{
    {10, 22.2}, {20, 9.345}, {5, 77.54}};
```

## 15.6.4 `map`关联容器

*map关联容器*（来自头文件`<map>`）可以快速存储和检索*唯一键及关联值*。*不允许*重复键——每个键只能关联一个值。这称为**一对一映射**。例如，一家使用唯一员工编号（如100、200和300）的公司可能有一个`map`，将员工编号与其电话分机号关联——分别为4321、4115和5217。使用`map`，你指定键，就能快速取回关联的数据。在`map`的下标运算符`[]`中提供键，可以定位`map`中与该键关联的值。可以在`map`的*任意位置*进行插入和删除。如果键的顺序不重要，可以使用`unordered_map`（头文件`<unordered_map>`）代替。

**图15.18**演示了一个`map`（在第8行创建），并使用与**图15.17**相同的特性来演示下标运算符。第27–28行使用类`map`的下标运算符。当下标是`map`中已有的键时（第27行），运算符返回关联值的引用。当下标是`map`中*不存在的*键时（第28行），运算符将该键插入`map`，并返回一个可用于将该键与某个值关联的引用。第27行将键`25`的值（在15行中指定为`33.333`）替换为新值`9999.99`。第28行在`map`中插入一个新的键–值对（称为**创建关联**）。注意本例的`map`本可以用`pair`的初始化器列表初始化，正如我们在**15.6.3节**中为`multimap`所示。

```cpp
// Fig. 15.18: fig15_18.cpp
// Standard Library class map class template.
#include <iostream>
#include <map> // map class-template definition
using namespace std;

int main() {
   map<int, double, less<int>> pairs;

   // insert eight value_type objects in pairs
   pairs.insert(make_pair(15, 2.7));
   pairs.insert(make_pair(30, 111.11));
   pairs.insert(make_pair(5, 1010.1));
   pairs.insert(make_pair(10, 22.22));
   pairs.insert(make_pair(25, 33.333));
   pairs.insert(make_pair(5, 77.54)); // dup ignored
   pairs.insert(make_pair(20, 9.345));
   pairs.insert(make_pair(15, 99.33)); // dup ignored

   cout << "pairs contains:\nKey\tValue\n";

   // walk through elements of pairs
   for (auto mapItem : pairs) {
      cout << mapItem.first << '\t' << mapItem.second << '\n';
   }

   pairs[25] = 9999.99; // use subscripting to change value for key 25
   pairs[40] = 8765.43; // use subscripting to insert value for key 40

   cout << "\nAfter subscript operations, pairs contains:\nKey\tValue\n";

   // use const_iterator to walk through elements of pairs
   for (auto mapItem : pairs) {
      cout << mapItem.first << '\t' << mapItem.second << '\n';
   }

   cout << endl;
}
```

pairs contains:

| Key | Value |
| --- | ---: |
| 5 | 1010.1 |
| 10 | 22.22 |
| 15 | 2.7 |
| 20 | 9.345 |
| 25 | 33.333 |
| 30 | 111.11 |

After subscript operations, pairs contains:

| Key | Value |
| --- | ---: |
| 5 | 1010.1 |
| 10 | 22.22 |
| 15 | 2.7 |
| 20 | 9.345 |
| 25 | 9999.99 |
| 30 | 111.11 |
| 40 | 8765.43 |

图15.18 标准库`map`类模板。

## 15.7 容器适配器

三种**容器适配器**是`stack`、`queue`和`priority_queue`。容器适配器*不是一等容器*，因为它们*不提供*可存储元素的实际数据结构实现，而且*适配器不支持迭代器*。*适配器类*的好处是可以选择合适的基础数据结构。所有三种*适配器类*都提供成员函数`push`和`pop`，分别向每个适配器数据结构正确地插入元素和从每个适配器数据结构正确地删除元素。接下来的几个小节提供适配器类的示例。

### 15.7.1 `stack`适配器

类`stack`（来自头文件`<stack>`）允许在基础容器的一端（称为*栈顶*）进行插入和删除，因此栈通常被称为*后进先出*数据结构。我们在**6.11节**讨论函数调用栈时介绍了栈。`stack`可以用`vector`、`list`或`deque`实现。本例创建三个整数栈，分别使用`vector`、`list`和`deque`作为底层数据结构来表示`stack`。默认情况下，`stack`使用`deque`实现。`stack`的操作包括：`push`在`stack`的*栈顶*插入一个元素（通过调用底层容器的函数`push_back`实现），`pop`删除`stack`的*栈顶*元素（通过调用底层容器的函数`pop_back`实现），`top`获取`stack`栈顶元素的引用（通过调用底层容器的函数`back`实现），`empty`确定`stack`是否为空（通过调用底层容器的函数`empty`实现），以及`size`获取`stack`中的元素个数（通过调用底层容器的函数`size`实现）。在**第19章**中，我们将向你展示如何开发自己的自定义stack类模板。

**图15.19**演示了`stack`适配器类。第17、20和23行实例化了三个整数栈。第17行指定了一个`stack`，其

