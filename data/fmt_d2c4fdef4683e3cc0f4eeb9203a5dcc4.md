
`44` (`front = NULL`) 而不是 (`isEmpty()`).

`45` `template<class T>` // 使用 `cstdlib` 和 `iostream`:

`46` `Queue<T>::remove()`

`47` {

`48` if (`isEmpty()`)

`49` `cout` << "Error: Removing an item from empty queue.\n"

`50` `exit(1);`

`51` }

```

```cpp
`53` `T` `result` = `front-data`;

`54` `Node<T>` *`discard`;

`55` `discard` = `front`;

`56` `front` = `front-link`;

`57` if (`front` = `NULL`) // 如果你删除了最后一个节点

`58` `back` = `NULL`;

`59` `delete` `discard`;

`60` `return` `result`;

`61` }

`62` //`QueueSavitch`
```

当一个类是另一个类的友时，通常会在类定义中包含一个前向声明。这要求你第二个定义类或模板，如显示 `17.22` 所示。注意前向声明只是类或模板定义的头部后跟一个分号。使用友元的完整示例见第 `17.4` 节（参见编程示例“树模板类”）。

# 示例：使用链法的哈希表

哈希表或哈希映射是一种高效存储和检索数据的数据结构。构建哈希表有许多方法；在本节中，我们将使用数组结合链表。对象通过键关联存储在哈希表中。给定键，我们就可以检索到对象。理想情况下，键对于每个对象是唯一的。如果对象具有内在唯一的键，我们可以使用哈希函数来计算一个。例如，让我们使用哈希表来存储单词字典。这样的哈希表可能用于制作拼写检查器——哈希表中缺失的单词可能无法得到正确的纠正。我们将使用固定数组构建哈希表，每个数组元素引用一个链表。哈希函数计算的键将映射到数组的索引。实际数据将存储在哈希值索引处的链表中。显示 `17.23` 使用具有十个条目的固定数组说明了这一思想。最初，数组 `hasharray` 的每个条目包含指向空链表的引用。首先，我们添加单词“cat”，它被分配了键或哈希值为`2`（稍后我们将显示如何计算它）。接下来，我们添加“dog”和“bird”，它们分别被分配了哈希值`4`和`7`。这些字符串中的每一个都使用哈希值作为数组中的索引插入到链表的头部。最后，我们添加“turtle”，它的哈希值也是 `2`。由于“cat”已经存储在索引 `2`，我们现在发生了冲突。使用现有的链表，索引 `2` 现在有两个节点：“turtle”和“cat”。

要从哈希表中检索值，我们首先计算目标的哈希值。接下来，我们顺序搜索存储在 `hasharray[hashvalue]` 中的链表以目标。如果在该链表中没有找到目标，则目标未存储在哈希表中。如果链表的大小较小，检索过程将很快。

# 第 17 章 链式数据结构

示例：（续）

## 字符串的哈希函数

计算字符串的数值哈希值的一种简单方法是将字符串中每个字符的 ASCII 值相加，然后根据数组的大小对总和进行模运算。附录 `3` 给出了一部分 ASCII 码的子集。计算哈希值的代码在函数 `computeHash` 所示。

```cpp
int computeHash(string s) {
    int hash = 0;
    for (int i = 0; i < s.length(); i++) {
        hash = hash + s[i];
    }
    return hash % SIZE; // 示例中 SIZE = 10
}
```

例如，字符串 `"dog"` 的 ASCII 码：

- d -> 100
- g -> 111
- g -> 103

哈希函数的计算方式为：

```
Sum = 100 + 111 + 103 = 314
Hash = Sum % 10 = 314 % 10 = 4
```

在这个示例中，我们计算了一个无界值，即字符串中 ASCII 值的总和。然而，数组被定义为包含有限数量的元素。为了将总和缩放到数组的大小，我们计算总和对于数组大小的模（在示例中为 `10`）。在实践中，数组的大小通常大于可以进入哈希表的元素数量¹。对于字符串 `"dog"`，其他字符串也可能映射到相同的值。例如，我们可以验证 `"cat"` 映射到 (`99` + `97` + `116`) % `10` = `2`，而 `"turtle"` 映射到 (`116` + `117` + `114` + `116` + `101`) % `10` = `2`。

哈希表的完整代码列表在显示 `17.24` 和 `17.25` 中给出。显示 `17.26` 展示了一个演示。哈希表的定义使用了一个数组，其中每个元素都是在显示 `17.14` 中定义的 `Node` 类。链表使用显示 `17.14` 和 `17.15` 中的通用链表库实现。

> ¹ 质数可以避免导致冲突的常见模数因子。

## 链表应用

### 17.23 构建哈希表

#### 具有 10 个空链表的哈希表

```cpp
Node<string> *hashArray[10];
for (int i=0; i<10; i++) hashArray[i] = NULL;
```

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| hashArray | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL |

在添加哈希值为 `2` 的 `"cat"` 后

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| hashArray | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL |

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_808_0.png)

在添加哈希值为 `4` 的 `"dog"` 和哈希值为 `7` 的 `"bird"` 后

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| hashArray | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL |

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_808_1.png)

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| hashArray | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL | NULL |

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_808_2.png)

### 显示 17.24 HashTable 类的接口文件

```cpp
// 这是头文件 hashtable.h。这是 HashTable 类的
// 接口，它是一个用于字符串哈希表的类。
#ifndef HASHTABLE_H
#define HASHTABLE_H
#include <string>
#include "listtools.h"
using LinkedListSavitch::Node;
using std::string;
namespace HashTableSavitch
{
    const int SIZE = 10; // 哈希表数组的最大尺寸
    class HashTable {
    public:
        HashTable(); // 初始化哈希表。
        // 通常拷贝构造函数和赋值
        //运算符被省略以节省空间。
        ~HashTable(); // 析构销哈希表。
        bool containsString(string target) const; // 如果 target 在哈希表中则返回真
        否则返回 false。
        void put(string s); // 将字符串添加到哈希表。
    private:
        Node<string>* hashArray[SIZE]; 真正的哈希表
        static int computeHash(string s);// 计算哈希值
    }; //HashTable
} //HashTableSavitch
#endif //
```

### HashTable 类的实现（部分 1）

```cpp
// 这是实现文件 hashtable.cpp。这是 HashTable
// 类的实现。
#include <string>
#include "listtools.h"
using LinkedListSavitch::Node;
using std::string;
namespace HashTableSavitch
{
    HashTable::HashTable() {
        for (int i = 0; i < SIZE; i++)
            hashArray[i] = NULL;
    }
    HashTable::~HashTable() {
        for (int i = 0; i < SIZE; i++) {
            while (hashArray[i] != NULL) {
                Node<string>* temp = hashArray[i];
                hashArray[i] = hashArray[i]->next;
                delete temp;
            }
        }
    }
    int HashTable::computeHash(string s) {
        int hash = 0;
        for (int i = 0; i < s.length(); i++) {
            hash = hash + s[i];
        }
        return hash % SIZE;
    }
    bool HashTable::containsString(string target) const {
        int hash = computeHash(target);
        Node<string>* current = hashArray[hash];
        while (current != NULL) {
            if (current->data == target)
                return true;
            current = current->next;
        }
        return false;
    }
    void HashTable::put(string s) {
        int hash = computeHash(s);
        Node<string>* newNode = new Node<string>(s);
        newNode->next = hashArray[hash];
        hashArray[hash] = newNode;
    }
}
```

### 显示 17.26 演示（部分 1）

```cpp
// 程序演示 HashTable 的使用
#include <iostream>
#include "hashtable.h"
using std::string;
using std::cout;
using HashTableSavitch;
int main() {
    HashTable h;
    cout << "Adding dog, cat, turtle, bird" << endl;
    h.put("dog");
    h.put("cat");
    h.put("turtle");
    h.put("bird");
    cout << "Contains dog? " << (h.containsString("dog") ? 1 : 0) << endl;
    cout << "Contains cat? " << (h.containsString("cat") ? 1 : 0) << endl;
    cout << "Contains turtle? " << (h.containsString("turtle") ? 1 : 0) << endl;
    cout << "Contains bird? " << (h.containsString("bird") ? 1 : 0) << endl;
    cout << "Contains fish? " << (h.containsString("fish") ? 1 : 0) << endl;
    cout << "Contains cow? " << (h.containsString("cow") ? 1 : 0) << endl;
    return 0;
}
```

### 显示 17.26 演示（部分 2）

示例输出

```
Adding dog, cat, turtle, bird
Contains dog? 1
Contains cat? 1
Contains turtle? 1
Contains bird? 1
Contains fish? 0
Contains cow? 0
```

## 哈希表的效率

我们哈希表的效率取决于多个因素。首先，让我们检查极端情况。最坏的运行时性能发生在插入表的每个元素都具有相同键时。所有元素将存储在单个链表中，查找操作可能需要搜索列表中的每个元素。幸运的是，如果我们插入的元素是随机的，它们具有相同键的可能性极低。

我们可以通过使用更好的哈希函数来减少冲突。例如，示例字符串字母的哈希函数忽略了字母的顺序。`"rat"` 和 `"tar"` 将具有相同的值。对于字符串，更好的哈希函数是根据字母在单词中的位置乘以递增的权重：

```cpp
int hash = 0;
for (int i = 0; i < s.length(); i++) {
  hash = 31 * hash + s[i];
}
```

减少冲突的另一种方法是使哈希表更大。例如，如果哈希表数组容量为 `10000`，但我们只插入 `1000` 个元素，那么冲突的概率将远小于哈希表数组只能存储 `1000` 个条目。然而，仅插入 `1000` 个

# 第 17 章 链数据结构

在一个包含 `10,000` 条条目的哈希表中，意味着将 `9000` 个内存位置未被使用，这是内存的浪费。这说明了时间空间权衡。通常可以以内存空间为代价来提高运行性能，反之亦然。

时间空间权衡

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_813_0.png)

### 自测练习

- 1. 假设你大学的每位学生都分配了一个唯一的九位数字 ID 编号。你想创建一个哈希表，将 ID 编号索引到代表学生的对象。哈希表的大小为 `N`，其中 `N` 小于九位数。请描述一个你可以使用的简单哈希函数，将 ID 编号映射到哈希索引。

- 2. 为 `HashTable` 编写一个 `outputHashTable()` 函数，输出哈希表中存储的每一个项。

# 示例：Set 模板类

集合（Set）是一个元素集合，其中没有元素出现超过一次。计算机科学中的许多问题都可以借助集合数据结构来解决。链表的变体是实现集合的一种直接方法。在此实现中，每个集合都使用单向链表存储。每个节点的数据仅包含集合中的一个项。

显示 `17.27` 展示了使用这种数据结构存储的两个示例集合。`round` 集合包含 `"peas"`、`ball"` 和 `"pie"`，而 `green` 集合包含 `"peas"` 和 `"grass"`。字符串 `"peas"` 同时存在于两个集合中，因为它既是圆的又是绿的。请注意，如果用于填充 `Node` 模板的数据类型是指对象的指针，则多个列表将引用同一个对象，而不是在每个列表中创建该对象的多个副本。

# 基础集合操作

我们的集合类应该支持的一些基础操作

```
add element. 向集合中添加新项。
contains. 确定目标项是否为集合的成员。
union. 返回一个与两个集合并集的集合。
intersection. 返回一个与两个集合交集的集合。
```

我们还应该包含一种遍历集合中每个元素的方法。其他实用的集合操作包括获取集合基数（cardinality）的函数以及从集合中移除项的函数。这些操作的实现在编程项目 `17.7` 的练习给出。

# 链表应用 785

示例：（继续）

实现通用元素集合的代码出现在显示 `17.28` 和 `17.29` 中。`Set` 类使用了显示 `17.14` 中的链表工具。`add` 函数简单地将节点添加到链表的头部，但仅当该项不在集合中时才添加。`contains` 函数使用链表库中的搜索函数。我们只需遍历列表中的每一个项来寻找目标。

`union` 函数将调用对象中的元素与输入参数 `otherSet` 中的元素结合。为了对这些集合取并集，我们创建了一个新的空集合对象。接下来，我们遍历调用对象的集合和 `otherSet` 的集合。所有元素都被添加到新集合中。`add` 函数强制了唯一性检查，因此我们不需要在 `union` 函数中检查重复元素。
