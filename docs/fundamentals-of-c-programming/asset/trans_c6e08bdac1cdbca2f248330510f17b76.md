
空列表)。

清单 18.4 (intlist.cpp) 实现了清单 18.3 (intlist.h) 中声明的方法。

```cpp
// intlist.cpp

#include "intlist1.h"
#include <iostream>

// Private IntList1 operations

/*
 * Node constructor
 */
IntList1::Node::Node(int n): data(n), next(nullptr) {}

/*
 * Returns the length of the linked list pointed to by p.
 */
int IntList1::length(IntList1::Node *p) const {
    if (p)
        return 1 + length(p->next);  // 1 + length of rest of list
    else
        return 0;    // Empty list has length zero
}

/*
 * dispose(p)
 * Deallocate the memory held by the list pointed to by p.
 */
void IntList1::dispose(IntList1::Node *p) {
    if (p) {
        dispose(p->next);   // Free up the rest of the list
        delete p;   // Deallocate this node
    }
}

// Public IntList1 operations

/*
 * The constructor makes an initially empty list.
 * The list is empty when head and tail are null.
 */
IntList1::IntList1(): head(nullptr), tail(nullptr) {}

/*
 * insert(n)
 * Inserts n onto the back of the list.
 * n is the element to insert.
 */
void IntList1::insert(int n) {
    // Make a node for the new element n
    IntList1::Node *new_node = new Node(n);
    if (tail) {   // Is tail non-null?
        tail->next = new_node; // Link the new node onto the back
        tail = new_node; // The new node is the new tail of the list
    }
    else // List is empty, so make head and tail point to new node
        head = tail = new_node;
}

/**
 * print()
 * Prints the contents of the linked list of integers.
 */
void IntList1::print() const {
   for (auto cursor = head; cursor; cursor = cursor->next)
      std::cout << cursor->data << ' ';
   std::cout << '\n';
}

/**
 * Returns the length of the linked list.
 */
int IntList1::length() const {
   return length(head); // Delegate work to private helper method
}

/**
 * clear()
 * Removes all the elements in the linked list.
 */
void IntList1::clear() {
   dispose(head); // Deallocate space for all the nodes
   head = tail = nullptr; // Null head signifies list is empty
}
```

由于清单 18.4 (intlist.cpp) 中的代码出现在类声明之外，任何使用 Node 类型的地方都需要使用其全名：IntList1::Node。请注意 Node 构造函数中 :: 的用法：

```
IntList1::Node::Node(int n): data(n), next(nullptr) {}
```

清单 18.4 (intlist.cpp) 中的两个私有方法（Length 和 Dispose）是递归的。IntList1 类的 insert 方法在向集合添加元素时使用 new 动态分配 Node 对象。clear 方法负责释放列表节点，从而清理列表所持有的内存。

清单 18.5 (listmain.cpp) 提供了一些示例客户端代码，用于操作链表。

## 清单 18.5: listmain.cpp

```cpp
// list_main.cpp

#include "intlist1.h"
#include <iostream>

int main() {
   bool done = false;
   char command;
   int value;
   IntList1 list;

   while (!done) {
       std::cout << "I)nsert <item> P)rint L)ength E)rase Q)uit >>";
       std::cin >> command;
       switch (command) {
       case 'I': // Insert a new element into the list
       case 'i':
           if (std::cin >> value)
               list.insert(value);
           else
               done = true;
           break;
       case 'P': // Print the contents of the list
       case 'p':
           list.print();
           break;
       case 'L': // Print the list's length
       case 'l':
           std::cout << "Number of elements: " << list.length() << '\n';
           break;
       case 'E': // Erase the list
       case 'e':
           list.clear();
           break;
       case 'Q': // Exit the loop (and the program)
       case 'q':
           done = true;
           break;
       }
   }
   list.clear(); // Free up the space held by the linked list
}
```

清单 18.5 (listmain.cpp) 中的客户端代码允许用户交互式地向列表添加项目、打印列表、确定列表大小并清空列表。以下是示例运行：

| 示例运行 |
|------------|
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>p |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>i 90 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>i 23 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>i 10 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>i -4 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>p |
| 90 23 10 -4 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>i 22 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>p |
| 90 23 10 -4 22 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>l |
| 元素数量: 5 |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>e |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>p |
| I)插入 <item> P)打印 L)长度 E)擦除 Q)退出 >>q |

## 图 18.3 典型 IntList1 对象的概念视图。此处的链表对象名为 list。

![](img/e84ad11adb18201d71595b31ce6c9eff_567_0.png)

图 18.3 可视化了示例运行中途链表的概念状态。

请注意，客户端代码根本不使用指针。所有指针操作都隐藏在 IntList1 类内部。指针编程可能很棘手，很容易引入微妙且难以查找的错误；因此，封装再次带来了更轻松、更健壮的应用程序开发。Node 结构体本身在 IntList1 内部是私有的，使用这些链表的程序员无法访问。

如 IntList1::dispose 方法所示，指针变量本身可以用作条件语句或循环中的条件。空指针被解释为 false，任何非空指针都为 true。这意味着如果 p 是指针，语句

```
if (p)
/* Do something */
```

等同于

```
if (p != nullptr)
/* Do something */
```

而语句

```
if (!p)
/* Do something */
```

等同于

```
if (p == nullptr)
/* Do something */
```

大多数 C++ 程序员使用较短的语法。

为了更好地理解递归方法的工作原理，请按以下解释思考 Node 对象的结构：Node 对象持有一个数据项和一个指向其后列表其余部分的指针。指向 Node 的指针要么是空的，要么是非空的。空指针表示空列表。非空指针表示非空列表，由两部分组成：列表中的第一个元素和列表的其余部分。如果 Node 对象的 next 字段为空，则列表的其余部分为空。

有了这种对列表的看法，我们现在可以更详细地考察递归链表方法的行为：

- length— 列表要么为空，要么非空。空列表的长度为零。非空列表的长度至少为一，因为非空列表至少包含一个元素。从符号上讲（不是 C++），我们可以让 ∅ 表示空列表，让 x → ∅ 表示仅包含元素 x 的列表。

编写递归列表长度方法简单如下：

- 如果列表为空，其长度为零。从符号上讲，我们可以写 Length(∅) = 0。
- 如果列表非空，其长度为一（计算其第一个元素）加上列表其余部分的 Length。

从符号上讲，我们可以写 length(x→rest) = 1 + length(rest)。

我们可以将确定 2→10→7→∅ 长度的递归过程可视化为：

```
length(2→10→7→∅) = 1 + length(10→7→∅)
= 1 + 1 + length(7→∅)
= 1 + 1 + 1 + length(∅)
= 1 + 1 + 1 + 0
= 3
```

- dispose— dispose 方法的行为与 length 类似。不过请注意，它在删除当前节点*之前*递归调用以删除列表其余部分的节点。在使用 delete 释放数据后，尝试通过指针访问数据会导致未定义行为；因此，尝试这样做是逻辑错误。这意味着 dispose 中的代码不应写成

```
if (p) { // Logic error! Do not do it this way!
    delete p; // Deallocate this node first
    dispose(p->next); // Then free up the rest of the list
}
```

在这里，我们在删除 p 的内存后，试图使用 p→next，而 p→next 本身也使用了 p。

虽然递归方法对递归进行了良好的回顾，但递归对这些函数并非严格必要。我们可以改用以下代码片段所示的公共 length 和 clear 函数：

// length 和 clear 的迭代版本

```cpp
int IntList1::length() const {
    int len = 0;
    for (auto cursor = head; cursor; cursor = cursor->next)
        len++;
    return len;
}
```

```cpp
void IntList1::clear() {
    auto cursor = head;
    while (cursor) {
        auto temp = cursor;
        cursor = cursor->next;
        delete temp;
    }
    head = tail = nullptr; // Null head signifies list is empty
}
```
