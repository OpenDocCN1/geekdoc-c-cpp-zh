
- 21. 画出本章讨论的类 `doublyLinkedList` 的 UML 图。
- 22. 画出 DVD 商店编程示例中类 `dvdType` 的 UML 图。
- 23. 画出 DVD 商店编程示例中类 `dvdListType` 的 UML 图。

## 编程练习

- 1. **（在线通讯录（修订版））** 第 11 章中的编程练习 5 最多只能处理 500 个条目。使用链表重做该程序，以处理所需数量的条目。向程序中添加以下操作：
  - a. 向通讯录中添加或删除新条目。
  - b. 允许用户保存通讯录中的数据。

- 2. 通过添加以下操作来扩展类 `linkedListType`：
  - a. 查找并删除链表中 `info` 最小的结点。（只删除第一个出现的结点，并且只遍历链表一次。）
  - b. 查找并删除链表中给定 `info` 的所有出现。（只遍历链表一次。）

  在类 `linkedListType` 中将它们添加为抽象函数，并在类 `unorderedLinkedList` 中提供这些函数的定义。另外，编写一个程序来测试这些函数。

- 3. 通过添加以下操作来扩展类 `linkedListType`：
  - a. 编写一个函数，返回链表中第 k<sup>个</sup>元素的 `info`。如果不存在这样的元素，则终止程序。
  - b. 编写一个函数，返回链表中第 k<sup>个</sup>元素。如果不存在这样的元素，则终止程序。

  在类 `linkedListType` 中提供这些函数的定义。另外，编写一个程序来测试这些函数。（使用类 `unorderedLinkedList` 或类 `orderedLinkedList` 来测试你的函数。）

- 4. **（反向打印单链表）** 将本章讨论的函数 `reversePrint` 和 `recursiveReversePrint` 包含到类 `linkedListType` 中。另外，编写一个程序函数来反向打印（单）链表。（使用类 `unorderedLinkedList` 或类 `orderedLinkedList` 来测试你的函数。）

- 5. **（将链表划分为两个大小几乎相等的子链表）**
  - a. 按如下方式向类 `linkedListType` 添加操作 `divideMid`：

```
void divideMid(linkedListType<Type> &sublist);
//This operation divides the given list into two sublists
//of (almost) equal sizes.
//Postcondition: first points to the first node and last
//              points to the last node of the first
//              sublist.
//              sublist.first points to the first node
//              and sublist.last points to the last node
//              of the second sublist.
```

考虑以下语句：

```
unorderedLinkedList<int> myList;
unorderedLinkedList<int> subList;
```

假设 `myList` 指向包含元素 34 65 27 89 12（按此顺序）的链表。语句：

```
myList.divideMid(subList);
```

将 myList 划分为两个子链表：myList 指向包含元素 34 65 27 的链表，而 subList 指向包含元素 89 12 的子链表。

  - b. 编写函数模板的定义以实现操作 `divideMid`。另外，编写一个程序来测试你的函数。

- 6. **（在给定结点处将链表拆分为两个子链表）**
  - a. 向类 `linkedListType` 添加以下操作：

```
void divideAt(linkedListType<Type> &secondList,
              const Type& item);
//Divide the list at the node with the info item into two
//sublists.
//Postcondition: first and last point to the first and
//              last nodes of the first sublist.
//              secondList.first and secondList.last
//              point to the first and last nodes of the
//              second sublist.
```

考虑以下语句：

```
unorderedLinkedList<int> myList;
unorderedLinkedList<int> otherList;
```

假设 `myList` 指向包含元素 34 65 18 39 27 89 12（按此顺序）的链表。语句：

```cpp
myList.divideAt(otherList, 18);
```

将 `myList` 划分为两个子链表：`myList` 指向包含元素 34 65 的链表，而 `otherList` 指向包含元素 18 39 27 89 12 的子链表。

  - b. 编写函数模板的定义以实现操作 `divideAt`。另外，编写一个程序来测试你的函数。

- 7.
  - a. 向类 `orderedLinkedList` 添加以下操作：

```
void mergeLists(orderedLinkedList<Type>& list1,
                orderedLinkedList<Type>& list2);
//This function creates a new list by merging the
//elements of list1 and list2.
//Postcondition: first points to the merged list
//              list1 and list2 are empty
```

考虑以下语句：

```
orderedLinkedList<int> newList;
orderedLinkedList<int> list1;
orderedLinkedList<int> list2;
```

假设 `list1` 指向包含元素 2 6 7 的链表，`list2` 指向包含元素 3 5 8 的链表。语句：

```
newList.mergeLists(list1, list2);
```

创建一个新链表，其中元素顺序为 2 3 5 6 7 8，并且对象 `newList` 指向该链表。此外，在前面的语句执行后，`list1` 和 `list2` 为空。

  - b. 编写函数模板 `mergeLists` 的定义以实现操作 `mergeLists`。

- 8. 类 `orderedLinkedList` 的函数 `insert` 不检查要插入的项是否已经在链表中；也就是说，它不检查重复项。重写函数 `insert` 的定义，使其在插入该项之前检查要插入的项是否已经在链表中。如果要插入的项已经在链表中，该函数输出适当的错误消息。另外，编写一个程序来测试你的函数。

- 9. 在本章中，用于实现链表结点的类被定义为 `struct`。下面重写了 `struct nodeType` 的定义，使其声明为类，并且成员变量为私有：

```
template <class Type>
class nodeType
{
```

类 nodeType 的成员函数用于访问结点的 info 和 link 字段。另外，编写程序来测试类 unorderedLinkedList 和 orderedLinkedList 的各种操作。

- 11. 为类 `doublyLinkedList` 编写函数 `copyList`、复制构造函数以及重载赋值运算符的函数的定义。

- 12. 编写一个程序来测试类 `doublyLinkedList` 的各种操作。

- 13. **（循环链表）** 本章定义并识别了循环链表上的各种操作。
  - a. 编写类 `circularLinkedList` 及其成员函数的定义。（你可以假设循环链表的元素按升序排列。）
  - b. 编写一个程序来测试 (a) 中定义的类的各种操作。

- 14. **（DVD 商店编程示例）**
  - a. 完成 DVD 商店编程示例中定义的类 `customerType` 的设计与实现。
  - b. 设计并实现类 `customerListType`，以创建和维护 DVD 商店的客户列表。

- 15. **（DVD 商店编程示例）** 完成 DVD 商店程序的设计与实现。换句话说，编写一个程序，使用 DVD 商店编程示例和编程练习 14 中设计的类，使 DVD 商店能够运行。

- 16. 通过添加以下函数来扩展类 `linkedListType`：

```
void rotate();
//Function to remove the first node of a linked list and put it
//at the end of the linked list.
```

另外编写一个程序来测试你的函数。使用类 `unorderedLinkedList` 创建一个链表。

- 17. 编写一个程序，提示用户输入一个字符串，然后以 pig Latin 形式输出该字符串。将字符串转换为 pig Latin 形式的规则在第 7 章的编程示例：Pig Latin 字符串中描述。你的程序必须将字符串的字符存储到链表中，并使用编程练习 16 中描述的函数 `rotate` 来旋转该字符串。

