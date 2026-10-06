
## 获取值

你可以通过调用 `get()` 成员函数来获取哈希表中存储的值，如下代码段所示。`get()` 函数需要两个参数。第一个参数是引用条目键的 `char` 指针。第二个参数是引用条目值的 `char` 指针。如果在哈希表中找到了键，`get()` 函数会将条目的值从哈希表复制到 `value` 参数中。如果找到了键，则返回布尔值 `true`；否则返回布尔值 `false`。

`get()` 函数通过调用 `find()` 函数并将作为 `get()` 函数第一个参数的键传递给它来搜索哈希表。`find()` 函数在哈希表中搜索键之前会对键进行哈希处理。然后 `find()` 函数返回包含该键的元数据结构引用或 `NULL`。

`get()` 函数将 `find()` 函数的返回值赋值给 `temp` 的指针，这是一个元数据结构指针。`get()` 函数判断 `temp` 指针是否为 `NULL`。如果是，则将 `value` 的第一个数组元素赋值为空字符（设为空字符串），`get()` 函数返回布尔 `false`，表示该键不在哈希表中。

如果 `temp` 不是 `NULL`，说明 `find()` 函数在哈希表中找到了该键，并返回包含该条目的元数据引用。然后将条目的值复制到 `value` 参数中，`get()` 函数返回布尔值 `true`。

```cpp
bool get(char* key, char* value)
{
    METADATA* temp = find(key);
    if (temp == NULL)
    {
        value[0] = '\0';
        return false;
    }
    strcpy(value, temp->value);
    return true;
}
```

## 第 11 章 什么是哈希表？

```cpp
bool get(char* key, char* value)
{
    METADATA* temp = find(key);
    if(temp == NULL)
    {
        value[0] = '\0';
        return false;
    }
    else
    {
        strcpy(value, temp->value);
        return true;
    }
}
```

## find()

你在其他成员函数中多次调用了 `find()` 成员函数。现在让我们来看一下 `find()` 成员函数是如何工作的。正如你记得的，`find()` 函数的目的是在哈希表中搜索键。如果找到了键，`find()` 函数将返回一个包含该键和对应值的元数据结构的引用。如果没有找到键，`find()` 则返回 `NULL`。

`find()` 函数需要一个参数，即键的引用。该键被传递给 `hashString()`，该函数对键进行哈希处理并返回与该键对应的哈希值。这是因为存储在哈希表中的键是实际键的哈希值。因此，`find()` 函数必须将键转换为对应的哈希值，以便在指针数组中定位条目。

`hashString()` 函数返回的哈希值被赋值给桶索引（bucket index），该索引被用作识别表数组（即哈希表）中条目的索引。表元素是一个元数据结构的引用，然后被赋值给元数据结构的 `temp` 指针。

只要 `temp` 指针不为 `NULL`，`find()` 函数就会使用 `strcmp()` 来比较传递给 `find()` 函数的键所指向的元数据结构中的键元素。此时，`temp` 变量被用于遍历列表。如果匹配成功，则返回 `temp` 指针指向的元数据结构。如果没有匹配，则将元数据结构的下一个成员赋值给 `temp` 指针，`find()` 函数通过进行下一次比较继续执行。

### 数据结构解密

如果 `find()` 函数在检查了哈希索引中的所有条目后仍没有匹配，则 `find()` 函数将返回 `NULL`。

```cpp
METADATA* find(char* key)
{
    int bucket = hashString(key);
    METADATA* temp = table[bucket];
    while (temp != NULL) {
        if (strcmp(key, temp->key) == 0) {
            return temp;
        }
        temp = temp->next;
    }
    return NULL;
}
```

## contains()

`contains()` 成员函数的目的是确定键是否存在于哈希表中。正如接下来的定义所示，`contains()` 函数的构造简单，但它在处理哈希表时起着至关重要的作用。

正如在本章之前的部分学到的，哈希表的每个键必须是唯一的。`contains()` 函数通过确定键是否已经存在于哈希表中，使你的应用程序确保键的唯一性。

`contains()` 函数需要一个参数，即你想要在哈希表中查询的键的引用。如果键存在，`contains()` 函数返回布尔值 `true`；如果未找到键，则返回布尔值 `false`。

`contains()` 函数通过调用 `find()` 函数并传递键来确定键是否存在。在本章的上一节中，你已经学过 `find()` 函数返回键的元数据引用或 `NULL`。`contains()` 函数决定返回的是其中哪一个。

如果 `find()` 函数返回 `NULL`，则 `contains()` 函数返回布尔值 `false`；否则，如果 `find()` 函数返回包含键的元数据引用，则返回布尔值 `true`。

```cpp
bool contains(char* key)
{
    if(find(key) == NULL) {
        return false;
    }
    else {
        return true;
    }
}
```

## 删除条目

当你的应用程序需要从哈希表中删除条目时，你需要调用 `remove()` 函数。如后续代码所示，`remove()` 函数需要一个参数，即要从哈希表中删除的条目的键的引用。如果找到了键并完全删除，`remove()` 函数返回布尔值 `false`；否则……（注：原文此处存在重复与断裂，已按技术逻辑完成翻译）。

### 数据结构解密

```c
}
size = 0;
}
```

## getSize()

`getSize()` 成员函数是 Hashtable 类中最简单的函数；它读取 Hashtable 类的 `size` 数据成员，将其值返回给调用 `getSize()` 函数的语句。`getSize()` 函数的定义在下一个代码段中。

为什么要使用 `getSize()` 函数而不是直接让应用程序访问 `size` 数据成员呢？为了保护数据的完整性。如果你让应用程序直接访问 `size` 数据成员，应用程序中的语句可能会给 `size` 赋错误的值。通过只允许 hashtable 的成员函数对 `size` 进行访问，你可以保护数据的完整性。

```c
int getSize()
{
    return size;
}
```

## hashString()

`hashString()` 成员函数是另一个由 Hashtable 类其他成员函数调用的函数，每当函数需要将键转换为哈希值时调用。`hashString()` 函数需要一个参数，即指向要哈希键的字符指针。哈希值与键对应，并由 `hashString()` 作为 `long` 类型返回。

`hashString()` 函数的定义在下一个代码段中。哈希过程首先通过调用 `strlen()` 函数来确定键的长度。长度被赋值给一个整数 `n`。你会声明一个 `long` `h` 并将其初始化为零，以存储哈希过程中哈希键的中间值。

哈希过程在键的位级别上运行，实际上随机化了破坏键的位。`hashString` 函数通过 `for` 循环遍历键的每个字符。在每次迭代中，组成变量 `h` 值的位会被左移（`h << 2`），键字符的位会被加到左移后的位上。结果被赋值给变量 `h`。这个过程一直持续到键的最后一个字符被哈希为止。

### 第 11 章 什么是哈希表？

`hashString()` 随后计算模值、最终的哈希值 (`h`) 和表格大小 (`h % tablesize`)。模值可以是正值，也可以是负值。然而，哈希键必须是一个正值。因此，`hashString()` 函数返回哈希键的绝对值 `abs(h % tablesize)`。

```c
long hashString(char* key)
{
    int n = strlen(key);
    long h = 0;
    for(int i=0; i<n; i++) {
        h = (h << 2) + key[i];
    }
    return abs(h % tablesize);
}
```

> **注意**：哈希的目标是获取一组键，并产生一个分布良好的索引序列。尽管程序员们认为哈希表的大小应该是素数，但存在多种哈希算法。然而，所有的哈希算法都有一个共同点：它们都使用了位移。
>
> 不存在一种“完美的哈希函数”。某些哈希函数在给定数据集上的效果比其他函数好。程序员通常在为哈希表设置最佳哈希函数之前，先在数据集上测试多种哈希函数。

## initIterator()

当被调用时，`initIterator()` 函数为 Hashtable 类的两个数据成员赋值。`current_entry` 数据成员被赋值为 `tablesize` 数据成员的值。

接下来，`for` 循环寻找哈希表中的第一个条目。在每次循环中，表格数组的当前元素与 `NULL` 进行比较。如果元素是 `NULL`，则继续查找表格数组中不为 `NULL` 的元素。第一个不为 `NULL` 的元素就是哈希表中的第一个条目。

### 数据结构解密

一旦找到了第一个条目，表格数组对应元素的值就会赋值给 `current_entry`。该值是对元数据结构的引用，该结构包含了该条目的键和值。然后，将元素的索引赋值给 `current_index` 数据成员。`initIterator()` 函数返回。

`initIterator()` 函数被 `displayAll()` 函数用于在调用 `hasNext()` 和 `getNextKey()` 成员函数之前，确定哈希表中的条目。这两个函数都直接访问 Hashtable 类的 `current_entry` 和 `current_index` 数据成员。这些将在在本章的下一节中详细讨论。

```c
void initIterator() {
  current_entry = NULL;
  current_index = tablesize;
  for(int i=0; i<tablesize; i++) {
    if(table[i] == NULL) {
      continue;
    }
    current_entry = table[i];
    current_index = i;
    break;
  }
}
```

## hasNext() 和 getNextKey()

`hasNext()` 和 `getNextKey()` 成员函数与 `initIterator()` 配合使用，用于判断哈希表中是否存在另一个条目。`hasNext()` 函数通过将 `current_entry` 与 `NULL` 比较来判断是否存在。如果 `current_entry` 为 `NULL`，则 `hasNext()` 函数返回 `false`；否则返回 `true`。

`getNextKey()` 函数获取条目的键。

```c
bool hasNext() {
  if(current_entry == NULL) {
    return false;
  } else {
    return true;
  }
}
```

等一下，如果表格的剩余元素都是 `NULL`，则哈希表中没有更多条目了。`getNextKey()` 函数为 `current_entry` 赋一个 `NULL` 值，并将 `tablesize` 数据成员的值赋给 `current_index` 数据成员。这些键和值是无特定顺序从哈希表中提取的；通常，哈希表不支持数据的排序。

## 使用 C++ 实现哈希表

现在你已经理解了 Hashtable 类各个组件的工作原理，是时候将它们组合成一个可以运行的 C++ 应用程序了。我将应用程序分为三个文件：包含应用程序的 `HashtableDemo.cpp` 文件；包含元数据结构定义和 Hashtable 类定义的 `HashTable.h` 文件；以及包含成员函数实现的 `Hashtable.cpp` 文件。在本节中，我们将关注如何在应用程序中使用 Hashtable 类。你已经学习了 Hashtable 类的成员函数和数据成员是如何工作的。

应用程序从声明 Hashtable 类的一个实例并将引用赋值给 `hashtable` 指针开始。你使用定义的 `SIZE_KEY` 和 `SIZE_VALUE` 宏声明两个 `char` 数组，以设置数组的大小。这些数组存储了你将输入哈希表的数据的键和值字符串。

接下来，调用 `strcpy()` 函数来复制键和值。在将这些内容插入哈希表之前，你必须通过调用 `contains()` 成员函数来确定键是否已经存在于哈希表中；如果键已存在则返回 `true`；否则返回布尔值 `false`。注意，非操作符 `!` 反转了返回值的逻辑。你这样做是为了执行语句中包含的方法。

如果键在哈希表中不存在，应用程序会在屏幕上显示一条消息，告知正在插入键和值。实际的插入操作通过调用 Hashtable 类的 `put()` 成员函数完成。`put()` 函数要求将键和值作为参数传递。

重复此过程以向哈希表插入另外两个键/值对。这些中的每一个也会显示在此处所示的屏幕上。图 11-5 展示了该哈希表。

- 添加节点 - 键: 389 值: Mary
- 添加节点 - 键: 415 值: Henry
- 添加节点 - 键: 999 值: Joe

一旦所有三个新条目都插入到哈希表中，应用程序就会调用 `displayAll()` 函数。`displayAll()` 函数是一个独立函数，而不是 Hashtable 类的成员。它的唯一目的是显示哈希表的内容。在本示例中，`displayAll()` 函数定义在 `main()` 函数下方。

### 数据结构揭秘

| table[0] | key = "999", value = "Joe", Next = NULL |
| :--- | :--- |
| table[1] | key = "415", value = "Henry", Next = NULL |
| table[2] | key = "389", value = "Mary", Next = NULL |

**图 11-5** 最后一次调用 `put()` 函数后创建的哈希表。

当调用此函数时，屏幕上显示：

哈希表中的当前节点：
key: 415 value: Henry
key: 999 value: Joe
key: 389 value: Mary

应用程序调用 Hashtable 类的 `remove()` 成员函数来删除以 415 为键的条目。再次调用 `displayAll()` 函数以证明该条目已已从哈希表中删除。

删除 415 后：

哈希表中的当前节点：
key: 999 value: Joe
key: 389 value: Mary

在最后一步中，应用程序使用 `delete` 操作符销毁哈希表。析构函数在哈希表销毁之前被自动调用。析构函数调用 Hashtable 类的 `remove()` 成员函数，该函数在从哈希表中删除条目之前会显示每个条目。当所有条目都被删除时，屏幕上显示如下：

销毁哈希表：
正在移除节点 - key:999 Joe
正在移除节点 - key:389 Mary

```cpp
//HashtableDemo.cpp
#include <iostream.h>
#include <time.h>
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include "Hashtable.h"

void displayAll(Hashtable* hashtable);

void main() {
    Hashtable* hashtable = new Hashtable();
    char key[SIZE_KEY];
    char value[SIZE_VALUE];
    strcpy(key, "389");
    strcpy(value, "Mary");
    if(!hashtable->contains(key)) {
        cout << "Adding node - key: " << key << " << value: " << value << endl;
        hashtable->put(key, value);
    }
    strcpy(key, "415");
    strcpy(value, "Henry");
    if(!hashtable->contains(key)) {
        cout << "Adding node - key: " << key << " << value: " << value << endl;
        hashtable->put(key, value);
    }
    strcpy(key, "999");
    strcpy(value, "Joe");
    if(!hashtable->contains(key)) {
