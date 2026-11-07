
- c. 将 `first` 前进到指向下一个节点。
- d. 使 `trail` 指向 `current` 之前的节点。
- e. 使 `p` 指向一个空链表。
- f. 将 `last` 之前的节点的值设置为 `54`。
- g. 编写一个 `while` 循环，使 `first` 指向 `info` 为 `5` 的节点。

10. 将下列每个语句标记为有效或无效。如果语句无效，请解释原因。(3, 4)

- a. `p = list->link;`
- b. `first = list;`
- c. `temp->link = nullptr;`
- d. `current->link = temp->info;`
- e. `p = *last;`
- f. `first = 90;`
- g. `p->link->info = current->info;`
- h. `current->info = temp->link;`
- i. `*list = *temp;`
- j. `temp->link = last->link->link;`
- k. `cout << trail->link->link->info;`

11. 编写 C++ 语句完成以下操作。(3, 4)

- a. 编写一段 C++ 代码，使 `first` 遍历整个链表。
- b. 创建 `info` 为 `17` 的节点，并将其插入到 `current` 之后。
- c. 删除链表的最后一个节点，并释放该节点占用的内存。删除该节点后，使 `last` 指向链表的最后一个节点，且最后一个节点的链接必须为 `nullptr`。
- d. 删除 `info` 为 `92` 的节点。同时，释放该节点占用的内存。
- e. 编写一段 C++ 代码，通过调整链表中节点的链接，将 `info` 为 `46` 的节点移动到 `current` 之后。

12. 以下 C++ 代码的输出是什么？(3, 4)

- a.
```cpp
while (first != last)
{
    cout << first->info << " ";
    first = first->link;
}
cout << last->info << endl;
```

- b.
```cpp
while (current->link != nullptr)
    current = current->link;
    cout << current->info << " ";
cout << endl;
```

- c.
```cpp
while (p != nullptr)
    cout << p->info << " ";
    p = p->link;
cout << endl;
```

13. 如果以下 C++ 代码有效，请给出输出。如果无效，请解释原因。(3, 4)

```cpp
q = current;
current = current->link;
current->link = temp->link;
trail = current->link;
current = trail;
cout << q->info << " " << trail->info
     << " " << current->info << endl;
```

14. 如果以下 C++ 代码有效，请给出输出。如果无效，请解释原因。(3, 4)

```cpp
trail = temp->link;             //Line 1
temp = temp->link->link;         //Line 2
current = temp;                  //Line 3
current = current->link;         //Line 4
trail->link = last->link;        //Line 5
cout << current->info << " "
     << last->info << endl;       //Line 6
```

15. 给出以下 C++ 代码产生的结果。假设节点采用通常的 info-link 形式，且 info 的类型为 int。（first、temp 和 p 是 nodeType 类型的指针。）(3, 4)

```cpp
first = new nodeType;
first->info = 78;
p = new nodeType;
p->info = 26;
first->link = p;
p->link = nullptr;
temp = new nodeType;
temp->info = 39;
temp->link = first;
p = first;
first = temp;
temp = p->link;
cout << first->info << " " << temp->info << " "
     << p->info << endl;
```

16. 给出以下 C++ 代码产生的结果。假设节点采用通常的 info-link 形式，且 info 的类型为 int。（list、trail 和 current 是 nodeType 类型的指针。）(3, 4)

```cpp
current = new nodeType;
current->info = 72;
current->link = nullptr;
trail = current;
current = new nodeType;
current->info = 46;
current->link = trail;
list = current;
current = new nodeType;
current->info = 52;
list->link = current;
current->link = trail;
trail = current;
current = new nodeType;
current->info = 91;
current->link = trail->link;
trail->link = current;
current = list;
while (current != nullptr)
{
    cout << current->info << " ";
    current = current->link;
}
cout << endl;
```

17. 假设链表的节点采用通常的 `info-link` 形式，且 `info` 的类型为 `int`。如下文 (a) 到 (d) 部分所述，以下数据将被插入到一个初始为空的链表中：72、43、8、12。假设 head 是 `nodeType` 类型的指针。创建链表后，head 应指向链表的第一个节点。根据需要声明其他变量。编写 C++ 代码创建该链表。创建链表后，编写代码打印该链表。你的代码的输出是什么？(3, 4)

- a. 将 72 插入空链表。
- b. 在 72 之前插入 43。
- c. 在链表末尾插入 8。
- d. 在 43 之后插入 12。

18. 假设链表的节点采用通常的 `info-link` 形式，且 info 的类型为 `int`。（`list` 和 `ptr` 是 `nodeType` 类型的指针。）以下代码创建一个链表。(3, 4)

```cpp
ptr = new nodeType;
ptr->info = 16;
list = new nodeType;
list->info = 25;
list->link = ptr;
ptr = new nodeType;
ptr->info = 12;
ptr->link = nullptr;
list->link->link = ptr;
```

使用这段代码创建的链表回答以下问题。（这些问题彼此独立。）如果需要，请声明其他指针。

- a. 哪个指针指向链表的第一个节点？
- b. 确定链表中节点的顺序。
- c. 编写 C++ 代码，创建一个 `info 45` 的节点，并将其插入到 `info 16` 的节点之后。
- d. 编写 C++ 代码，创建一个 `info 58` 的节点，并将其插入到 `info 25` 的节点之前。这是否需要你更改原本指向链表第一个节点的指针的值？
- e. 编写 C++ 代码，删除 `info 25` 的节点。这是否需要你更改原本指向链表第一个节点的指针的值？

19.
- a. `class linkedListType` 的函数 begin 做什么？(5, 6)
- b. `class linkedListType` 的函数 end 做什么？(5, 6)

20. `unorderedLinkedList` 类的函数 `insertFirst` 与 `orderedLinkedList` 类的函数 `insertFirst` 有何不同？(7, 8)

21. 考虑以下 C++ 语句。（`unorderedLinkedList` 类如本章所定义。）(6, 8)

```cpp
unorderedLinkedList<int> list;

list.insertFirst(36);
list.insertLast(10);
list.insertFirst(65);
list.insertLast(30);
list.insertFirst(44);
list.deleteNode(10);
list.insertLast(27);
list.insertFirst(15);
list.insertFirst(5);
list.deleteNode(44);
list.deleteNode(87);

linkedListIterator<int> it;

for (it = list.begin(); it != list.end(); ++it)
    cout << *it << " ";
cout << endl;
```

这段程序段的输出是什么？

22. 假设输入为

**45 35 12 83 40 23 11 98 64 120 16 -999**

以下 C++ 代码的输出是什么？（`unorderedLinkedList` 类如本章所定义。）(8)

```cpp
unorderedLinkedList<int> list;
unorderedLinkedList<int> copyList;
int num;

cin >> num;
while (num != -999)
{
    if (num % 4 == 0 || num % 3 == 0)
        list.insertFirst(num);
    else
        list.insertLast(num);
    cin >> num;
}

cout << "list = ";
list.print();
cout << endl;

copyList = list;

copyList.deleteNode(33);
copyList.deleteNode(58);

cout << "copyList = ";
copyList.print();
cout << endl;
```

23. 绘制本章讨论的 `doublyLinkedList` 类的 UML 图。(10)

24. 绘制编程示例 DVD Store 中 `dvdType` 类的 UML 图。

25. 绘制编程示例 DVD Store 中 `dvdListType` 类的 UML 图。

## 编程练习

### 1. **（在线通讯录再探）** 第11章中的编程练习5最多只能处理500条记录。使用链表重做该程序，以处理所需数量的记录。向你的程序添加以下操作：

- a. 向通讯录添加或删除新条目。
- b. 允许用户保存通讯录中的数据。

### 2. 通过添加以下操作扩展 `class linkedListType`：

- a. 查找并删除链表中 `info` 最小的节点。（仅删除第一次出现的节点，并且只遍历链表一次。）
- b. 从链表中查找并删除给定 `info` 的所有出现。（只遍历链表一次。）

将这些函数作为抽象函数添加到 `class linkedListType` 中，并在 `class unorderedLinkedList` 中提供这些函数的定义。同时，编写一个程序测试这些函数。

### 3. 通过添加以下操作扩展 `class linkedListType`：

- a. 编写一个函数，返回链表中第 *k* 个元素的 `info`。如果不存在这样的元素，则终止程序。
- b. 编写一个函数，删除链表中第 *k* 个元素。如果不存在这样的元素，则终止程序。

在 `class linkedListType` 中提供这些函数的定义。同时，编写一个程序测试这些函数。（使用 `class unorderedLinkedList` 或 `class orderedLinkedList` 测试你的函数。）

### 4. （反向打印单链表）

将本章讨论的函数 `reversePrint` 和 `recursiveReversePrint` 包含到 `class linkedListType` 中。同时，编写一个程序函数以反向打印一个（单）链表。（使用 `class unorderedLinkedList` 或 `class orderedLinkedList` 测试你的函数。）

### 5. （将链表分成两个大小几乎相等的子链表）

- a. 按如下方式向 `class linkedListType` 添加操作 `divideMid`：

```cpp
void divideMid(linkedListType<Type>& sublist);
//This operation divides the given list into two sublists
//of (almost) equal sizes.
//Postcondition: first points to the first node and last
//              points to the last node of the first
//              sublist.
//              sublist.first points to the first node
//              and sublist.last points to the last node
//              of the second sublist.
```

考虑以下语句。

```cpp
unorderedLinkedList<int> myList;
unorderedLinkedList<int> subList;
```

假设 myList 指向包含元素 34 65 27 89 12（按此顺序）的链表。语句：

```cpp
myList.divideMid(subList);
```
