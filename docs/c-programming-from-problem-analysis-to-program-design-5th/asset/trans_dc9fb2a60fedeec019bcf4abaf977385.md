
考虑图 18-50 所示的链表。假设结点采用通常的 info-link 形式。使用该链表回答习题 6 至 12。如有必要，声明额外的变量。（假设 `list`、`p`、`s`、`A` 和 `B` 是 `nodeType` 类型的指针。）

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1145_0.png)

**图 18-50** 用于习题 6 至 12 的链表

**6.** 下列各 C++ 语句的输出是什么？

- a. `cout << list->info;`
- b. `cout << A->info;`
- c. `cout << B->link->info;`
- d. `cout << list->link->link->info;`

**7.** 下列各关系表达式的值是什么？

- a. `list->info >= 18`
- b. `list->link == A`
- c. `A->link->info == 16`
- d. `B->link == NULL`
- e. `list->info == 18`

**8.** 将下列各语句标记为有效或无效。如果语句无效，请解释原因。

- a. `A = B;`
- b. `list->link = A->link;`
- c. `list->link->info = 45;`
- d. `*list = B;`
- e. `*A = *B;`
- f. `B = A->link->info;`
- g. `A->info = B->info;`
- h. `list = B->link->link;`
- i. `B = B->link->link->link;`

**9.** 编写 C++ 语句完成以下操作。

- a. 使 `A` 指向包含信息 23 的结点。
- b. 使 `list` 指向包含 16 的结点。
- c. 使 `B` 指向链表中的最后一个结点。
- d. 使 `list` 指向空链表。
- e. 将包含 25 的结点的值设置为 35。
- f. 创建信息为 10 的结点，并将其插入到 `A` 所指向的结点之后。
- g. 删除信息为 23 的结点。同时释放该结点占用的内存。

**10.** 下列 C++ 代码的输出是什么？

```cpp
p = list;

while (p != NULL)
{
    cout << p->info << " ";
    p = p->link;
}
cout << endl;
```

**11.** 如果下列 C++ 代码有效，请给出输出。如果无效，请解释原因。

```cpp
s = A;
p = B;
s->info = B;
p = p->link;
cout << s->info << " " << p->info << endl;
```

**12.** 如果下列 C++ 代码有效，请给出输出。如果无效，请解释原因。

```cpp
p = A;
p = p->link;
s = p;
p->link = NULL;
s = s->link;
cout << p->info << " " << s->info << endl;
```

**13.** 说明下列 C++ 代码产生的结果。假设结点采用通常的 info-link 形式，且 info 的类型为 int。（`list` 和 `ptr` 是 `nodeType` 类型的指针。）

```cpp
list = new nodeType;
list->info = 10;
ptr = new nodeType;
ptr->info = 13;
ptr->link = NULL;
list->link = ptr;
ptr = new nodeType;
ptr->info = 18;
ptr->link = list->link;
list->link = ptr;
ptr->info = 12;
ptr->link = NULL;
list->link->link = ptr;
```

使用这段代码创建的链表回答下列问题。（这些问题彼此独立。）如果需要，请声明额外的指针。

- a. 哪个指针指向链表的第一个结点？
- b. 确定链表中结点的顺序。
- c. 编写 C++ 代码，创建一个 `info` 为 45 的结点，并将其插入到 `info` 为 16 的结点之后。
- d. 编写 C++ 代码，创建一个 `info` 为 58 的结点，并将其插入到 `info` 为 25 的结点之前。这是否要求你改变原来指向链表第一个结点的指针的值？
- e. 编写 C++ 代码删除 `info` 为 25 的结点。这是否要求你改变原来指向链表第一个结点的指针的值？

**17.** 考虑下列 C++ 语句。（类 `unorderedLinkedList` 如本章所定义。）

```cpp
unorderedLinkedList<int> list;

list.insertFirst(15);
list.insertLast(28);
list.insertFirst(30);
list.insertFirst(2);
list.insertLast(45);
list.insertFirst(38);
list.insertLast(25);
list.deleteNode(30);
list.insertFirst(18);
list.deleteNode(28);
list.deleteNode(12);
list.print();
```

该程序段的输出是什么？

**18.** 假设输入为：

```text
18 30 4 32 45 36 78 19 48 75 -999
```

下列 C++ 代码的输出是什么？（类 `unorderedLinkedList` 如本章所定义。）

```cpp
unorderedLinkedList<int> list;
unorderedLinkedList<int> copyList;
int num;

cin >> num;
while (num != -999)
{
    if (num % 5 == 0 || num % 5 == 3)
        list.insertFirst(num);
    else
        list.insertLast(num);
    cin >> num;
}

list.print();
cout << endl;

copyList = list;

copyList.deleteNode(78);
copyList.deleteNode(35);

cout << "Copy List = ";
copyList.print();
cout << endl;
```

- **19.** 画出本章讨论的类 `doublyLinkedList` 的 UML 图。
- **20.** 画出视频商店编程示例中类 `videoType` 的 UML 图。
- **21.** 画出视频商店编程示例中类 `videoListType` 的 UML 图。

## 编程练习

- **1.**（在线通讯录（再访））第 13 章中的编程练习 6 最多只能处理 500 个条目。使用链表重做该程序，以处理所需数量的条目。向程序中添加以下操作：
  - a. 在通讯录中添加或删除一个新条目。
  - b. 允许用户保存通讯录中的数据。
- **2.** 通过添加以下操作来扩展 `class linkedListType`：
  - a. 查找并删除链表中 info 最小的结点。（只删除第一个出现者，并且只遍历链表一次。）
  - b. 查找并删除链表中给定 info 的所有出现。（只遍历链表一次。）

将这些操作作为抽象函数添加到 `class linkedListType` 中，并在 `class unorderedLinkedList` 中提供这些函数的定义。同时编写一个程序来测试这些函数。

- **3.** 通过添加以下操作来扩展类 `linkedListType`：
  - a. 编写一个函数，返回链表中第 *k* 个元素的 info。如果不存在这样的元素，则终止程序。
  - b. 编写一个函数，删除链表中第 *k* 个元素。如果不存在这样的元素，则终止程序。

在类 `linkedListType` 中提供这些函数的定义。同时编写一个程序来测试这些函数。（使用类 `unorderedLinkedList` 或类 `orderedLinkedList` 来测试你的函数。）

### 4. 反向打印单链表

将本章讨论的函数 `reversePrint` 和 `recursiveReversePrint` 包含在类 `linkedListType` 中。同时编写一个程序函数来反向打印一个（单）链表。（使用类 `unorderedLinkedList` 或类 `orderedLinkedList` 来测试你的函数。）

### 5. 将链表分成两个大小几乎相等的子链表

- a. 按如下方式向类 `linkedListType` 添加操作 `divideMid`：

```cpp
void divideMid(linkedListType<Type> &sublist);

//This operation divides the given list into two sublists
//of (almost) equal sizes.
//Postcondition:  first points to the first node and last
//                points to the last node of the first
//                sublist.
//                sublist.first points to the first node
//                and sublist.last points to the last node
//                of the second sublist.
```

考虑以下语句：

```cpp
unorderedLinkedList<int> myList;
unorderedLinkedList<int> subList;
```

假设 `myList` 指向包含元素 34 65 27 89 12（按此顺序）的链表。语句：

```cpp
myList.divideMid(subList);
```

将 `myList` 分成两个子链表：`myList` 指向包含元素 34 65 27 的链表，而 `subList` 指向包含元素 89 12 的子链表。

- b. 编写函数模板的定义以实现操作 `divideMid`。同时编写一个程序来测试你的函数。

### 6. 在给定结点处将链表分成两个子链表

创建一个新链表，其元素顺序为 2 3 5 6 7 8，并且对象 newList 指向该链表。另外，在前面的语句执行之后，list1 和 list2 为空。

- b. 编写函数模板 `mergeLists` 的定义以实现操作 `mergeLists`。

- **8.** 类 `orderedLinkedList` 的函数 `insert` 不检查要插入的项是否已在链表中；也就是说，它不检查重复项。重写函数 `insert` 的定义，使得在插入项之前，检查要插入的项是否已在链表中。如果要插入的项已在链表中，函数输出适当的错误消息。同时编写一个程序来测试你的函数。

- **9.** 本章中，用于实现链表结点的类被定义为 `struct`。下面重写 `struct nodeType` 的定义，使其声明为类，并且成员变量为 `private`。

```cpp
template <class Type>
class nodeType
{
public:
    const nodeType<Type>& operator=(const nodeType<Type>&);
        //Overload the assignment operator.

    void setInfo(const Type& elem);
        //Function to set the info of the node.
        //Postcondition: info = elem;

    Type getInfo() const;
        //Function to return the info of the node.
        //Postcondition: The value of info is returned.

    void setLink(nodeType<Type> *ptr);
        //Function to set the link of the node.
        //Postcondition: link = ptr;

    nodeType<Type>* getLink() const;
        //Function to return the link of the node.
        //Postcondition: The value of link is returned.

    nodeType();
        //Default constructor
        //Postcondition: link = NULL;

    nodeType(const Type& elem, nodeType<Type> *ptr);
        //Constructor with parameters
        //Sets info to point to the object elem points to, and
        //link is set to point to the object ptr points to.
        //Postcondition: info = elem; link = ptr
```

