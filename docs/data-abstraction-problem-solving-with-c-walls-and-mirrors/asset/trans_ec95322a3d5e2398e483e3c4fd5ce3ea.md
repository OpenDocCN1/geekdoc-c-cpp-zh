

# 摘要

- 1. ADT 列表通过位置维护其数据。列表中的每个条目通过其位置标识，位置是一个从 1 开始的整数。因此，列表中的数据是有顺序的，但该顺序由列表客户端决定，而不是列表本身。
- 2. 你可以在从 1 到当前列表长度加 1 范围内的位置向列表插入新条目。因此，你可以在第一个条目之前、最后一个条目之后或两个当前条目之间插入新条目。
- 3. 在列表中插入新条目会对列表中紧跟在被插入条目之后的所有现有条目重新编号。
- 4. 你可以移除当前位于从 1 到当前列表长度范围内位置的条目。因此，你可以移除第一个条目、最后一个条目或任何中间条目。
- 5. 从列表中移除条目会对列表中紧跟在删除条目之后的所有现有条目重新编号。

# 练习题

- 1. 考虑一个整数类型的 ADT 列表。编写一个伪代码函数，计算列表 `alist` 中整数之和。你的函数定义应该独立于列表的实现。
- 2. 实现类似于 Checkpoint 3 中的 `swap` 函数，但删除对列表中第 $i^{th}$ 个和第 $j^{th}$ 个项存在的假设。返回一个指示交换是否成功的值。
- 3. 使用你在练习 2 中编写的 `swap` 函数，编写一个反转列表 `alist` 中项顺序的函数。
- 4. 第 8.2 节描述了 `displayList` 和 `replace` 函数。它们的定义是基于 ADT 列表操作编写的。
  - a. `displayList` 和 `replace` 的实现方式有什么优点和缺点？
  - b. 将 `displayList` 和 `replace` 定义为 ADT 列表的操作有什么优点和缺点？
- 5. 假设 ADT 列表有一个方法 `get`，可以返回给定条目在列表中的位置。为该方法编写规格说明（Specifications）。
- 6. 在客户端级别编写一个伪代码函数 `getPosition`，返回给定条目在给定列表中的位置。
- 7. 假设 ADT 列表有一个方法 `contains`，可以判断列表是否包含给定条目。为该方法编写规格说明。
- 8. 在客户端级别编写一个伪代码函数 `contains`，测试列表是否包含给定条目。
- 9. ADT 列表的 `remove` 方法从列表中删除给定位置的条目。假设 ADT 列表有另一个方法 `remove`，可以从列表中删除指定的条目。为该方法编写规格说明。如果列表包含重复条目，你的方法会做什么？
- 10. 在客户端级别编写一个伪代码函数 `remove`，从给定列表中删除指定的条目。
- 11. 使用本章第 8.1 节“公理”中提供的 ADT 列表公理，证明操作序列：
  - 在位置 2 插入 A
  - 在位置 2 插入 B
  - 在位置 2 插入 C
  对非空字符列表产生的效果与以下序列相同：
  - 在位置 2 插入 C
  - 在位置 3 插入 B
  - 在位置 4 插入 A
- 12. 重复第 2 章的练习 20，使用 ADT 列表实现函数 `f(n)`。

# 编程问题

- 1. 使用 ADT 列表操作，编写第 1 章练习 9 中定义的 ADT 多项式操作的伪代码实现。
- 2. 圣诞老人维护着坏孩子列表和乖孩子列表。坏孩子列表上是那些会在袜子里得到煤炭的人的名字。乖孩子列表上是那些将收到礼物的人。列表中的每个对象都包含一个名字（字符串）和一个该人的礼物列表（ADT 列表的实例）。为乖孩子列表中的对象设计一个 ADT。通过说明每个 ADT 操作的用途、描述其参数，并编写前置条件、后置条件和其头定义的伪代码版本。然后为该 ADT 编写一个包含 javadoc 风格注释的模板接口。

# 第 9 章 列表实现

## 目录
- 9.1 基于数组的 ADT 列表实现 266
  - 9.1.1 头文件 266
  - 9.1.2 实现文件 268
- 9.2 基于链接的 ADT 列表实现 272
  - 9.2.1 头文件 272
  - 9.2.2 实现文件 274
  - 9.2.3 在 LinkedList 方法中使用递归 281
- 9.3 实现方案对比 285
- 总结 286
- 练习题 286
- 编程问题 286

- 前提条件
- 第 3 章 基于数组的实现
- C++ 间歇 2 指针、多态与内存分配
- 第 4 章 基于链接的实现
- C++ 间歇 3 异常
- 第 8 章 列表

上一节明确指定了 ADT 列表的操作，我们现在考虑实现它的数据结构。本章探索了列表的两种实现并比较了它们的优缺点。

# 9.1 基于数组的 ADT 列表实现

当你设计抽象数据类型时，你关注的是它的操作，但忽略了将如何用 C++ 实现它。当你设计一个抽象数据类型时，你关注的是它的操作。现在我们已经明确指定了 ADT 列表的操作，我们可以实现它。回顾如下列表操作：

```
+isEmpty(): boolean
+getLength(): integer
+insert(position: integer, newEntry: ItemType): boolean
+remove(position: integer): boolean
+clear(): void
+getEntry(position: integer): ItemType
+setEntry(position: integer, newEntry: ItemType): void
```

当你需要表示列表项时，首要任务是使用数组。事实上，你可能认为“列表”只是数组的一个华丽说法。这种想法并不完全正确。基于数组的实现是一个自然选择，因为它可以通过索引来标识项。然而，数组的大小是固定的。这种方法的的一个明显优点是实现列表操作很容易。那么，可以使用以下语句：

```
static const DEFAULT_CAPACITY = 100;
ItemType items[DEFAULT_CAPACITY]; // 列表项
int itemCount; // 当前条目计数
int maxItems; // 列表容量
```

### 9.1.1 头文件

现在我们已经确定了类的成员，就可以编写它的头文件，如 9-1 所示。我们派生自上一节开发的模板接口。编译器生成的析构函数和拷贝构造函数将足够。ListInterface 未指定的只有给定越界位置的行为。我们可以在这种情况抛出异常，为此我们使用第 7 章列表 7-5 和 7-6 中定义的 PreconditionViolated 类。

> 注意：通过为 ArrayList 定义数据成员 maxItems，该类能够动态分配数组而不是静态。因此，程序员可以轻松定义一个允许客户端选择数组大小的构造函数。

#  9-1 类的头文件

```
/** ADT 列表：基于数组的实现。
@file ArrayList.h */

#ifndef _ARRAY_LIST
#define _ARRAY_LIST

#include "ListInterface.h"
#include "PreconditionViolated.h"

template<class ItemType>
class ArrayList : public ListInterface<ItemType>{
private:
    static const int DEFAULT_CAPACITY = 100;
    ItemType items[DEFAULT_CAPACITY]; // 列表项
    int itemCount; // 当前条目计数
    int maxItems; // 列表容量
public:
    ArrayList();
    // 拷贝构造函数和析构函数由编译器提供
    bool isEmpty() const;
    int getLength() const;
    bool insert(int newPosition, const ItemType& newEntry);
    bool remove(int position);
    void clear();
    /** @throw PreconditionViolatedExcep if position < 1 or
       position > getLength(). */
    ItemType getEntry(int position) const throw(PreconditionViolatedExcep);
    /** @throw PreconditionViolatedExcep if position < 1 or
       position > getLength(). */
    void setEntry(int position, const ItemType& newEntry)
        throw(PreconditionViolatedExcep);
}; // end ArrayList

#include "ArrayList.cpp"
#endif
```

