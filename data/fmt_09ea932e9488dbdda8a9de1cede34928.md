
![](img/9d4e3b4f2864cf2e0756eefc7e2e4b3e_117_0.png)

**图 6-3** 双向链表包含 `next`（后继）和 `previous`（前驱）成员，而单向链表仅包含一个 `next`（后继）成员。

## LinkedList 类

程序员使用 `LinkedList` 类来创建和管理链表。C++ 程序员定义自己的 `LinkedList` 类，而 Java 程序员则使用 `LinkedList` 集合类。你将在本章的“使用 Java 列表”部分学习 `LinkedList` 集合类。现在，我们将重点关注在 C++ 中定义 `LinkedList` 类。

`LinkedList` 类定义由两个数据成员和六个函数组成，如本节中的示例所示。这两个数据成员是指向在本章之前定义的 `Node` 结构实例的指针。第一个指针 `front` 指向链表的第一个节点。第二个指针 `back` 指向链表的最后一个节点。

这六个成员操作着链表。第一个成员函数是类的构造函数，在声明实例时被调用。紧随构造函数之后析构函数。当你使用 `delete` 运算符向操作系统归内存时，会调用析构函数。如果你不调用 `delete` 运算符，析构函数永远不会被调用，应用程序会导致内存泄漏。

`appendNode()` 成员函数将新节点放在链表的末尾。`appendNode()` 需要一个表示节点当前数据的整数。接下来两个成员函数按自然顺序（从第一个到最后一个）显示链表的内容。`displayReverse()` 成员函数按反序显示链表。最后一个成员函数 `destroyList()` 被调用以从内存中移除 `LinkedList` 实例。

`LinkedList` 类规范定义在头文件中，实现定义在源文件中。我们将在接下来的几个章节中详细查看这些成员函数的实现。

```cpp
class LinkedList
{
  private:
    NODE* front;
    NODE* back;

  public:
    LinkedList();
    ~LinkedList();
    void appendNode(int);
    void displayNodes();
    void displayReverse();
    void destroyList();
};
```

## LinkedList 构造函数

`LinkedList` 构造函数在创建节点实例时初始化元素。正如你在接下来的章节中看到的，当你创建一个新节点时，为结构提供当前数据。此数据被分配给参数列表。`data` 的值被分配给结构的 `data` 元素。此外，指向前驱和后继节点的引用被初始化为 `NULL`，这告诉程序链表中没有其他元素。当添加新节点时，`NULL` 会被替换为指向新节点的引用。

```cpp
class LinkedList
{
  private:
    NODE* front;
    NODE* back;

  public:
    LinkedList()
    {
      front = NULL;
      back = NULL;
    }
};
```

## 析构函数

析构函数在你使用 `delete` 运算符向操作系统归内存时被调用。如果你不调用 `delete` 运算符，析构函数永远不会被调用，应用程序会导致内存泄漏。

```cpp
~LinkedList()
{
  // 释放内存逻辑
}
```

## appendNode() 函数

`appendNode()` 成员函数将新节点放在链表的末尾。`appendNode()` 需要一个表示节点当前数据的整数。

```cpp
void appendNode(int data)
{
  NODE* n = new NODE(data);
  if (back == NULL)
  {
    back = n;
    front = n;
  }
  else
  {
    back->next = n;
    n->previous = back;
    back = n;
  }
}
```

## displayNodes() 函数

`displayNodes()` 成员函数首先在屏幕上显示“Nodes”一词，并声明一个指向节点的指针，该指针初始化为链表头部的节点。

在尝试显示分配给节点的数据之前，`displayNodes()` 会确定链表头部是否存在节点。它通过判断 `temp` 指针所指向的节点是否为 `NULL` 来确定。如果是，则链表为空，无内容可显示。如果不是，该成员函数继续执行并显示分配给链表头部节点的数据。

随后会显示一个空格，然后是该节点的数据。`displayNodes()` 成员函数使用节点的 `next` 成员将指向下一个节点的指针赋值给 `temp` 指针。该过程持续，在显示分配给节点的数据之前，首先判断节点是否为 `NULL`。

在显示完链表末尾节点后，该过程结束，因为末尾节点的 `next` 成员为 `NULL`。

```cpp
NODE* temp = front;
while(temp != NULL) {
    cout << " " << temp->data;
    temp = temp->next;
}
```

## displayReverse() 函数

`displayReverse()` 成员函数按反序显示链表。

```cpp
void displayReverse()
{
  NODE* current = back;
  while (current != NULL)
  {
    cout << current->data << " ";
    current = current->previous;
  }
  cout << endl;
}
```

## destroyList() 函数

最后一个成员函数 `destroyList()` 被调用以从内存中移除 `LinkedList` 实例。

```cpp
void destroyList()
{
  NODE* current = front;
  while (current != NULL)
  {
    NODE* next = current->next;
    delete current;
    current = next;
  }
  front = NULL;
  back = NULL;
}
```

## 遍历链表

`displayNodesReverse()` 成员函数按反序显示链表的内容，从链表的末尾节点开始，一直显示到第一个节点。以下示例展示了如何实现这一点：

```cpp
void displayNodesReverse()
{
    cout << "Nodes in reverse order:";
    NODE* temp = back;
    while (temp != NULL) {
        cout << " " << temp->data;
        temp = temp->prev;
    }
}
```

你会发现 `displayNodesReverse()` 成员函数与上一节描述的 `displayNodes()` 成员函数几乎相同。这两个成员函数之间有两个重要的区别。`displayNodesReverse()` 成员函数将指向链表末尾节点的指针赋值为第一个显示。`displayNodes()` 成员函数将 `front` 指针赋值给 `temp` 指针，导致链表的第一个节点被显示。

`displayNodesReverse()` 成员函数与 `displayNodes()` 成员函数的另一个区别是，在 `displayNodesReverse()` 中用于确定下一个显示的节点。这使得节点能够按反序显示。图 6-5 展示了链表是如何遍历的。

## 数据结构解密

| 节点 1 | 节点 2 | 节点 3 | 节点 4 |
| --- | --- | --- | --- |
| 24 | 1 34 | 2 34 | 3 44 |

这里按遍历顺序显示节点。从这里开始

图 6-5 每个节点的 `previous` 成员遍历了链表。

## 销毁链表

`destroyList()` 成员函数从链表中移除节点并同时移除链表本身，如下所示。正如你之前在这里中学的，每个节点都是使用 `new` 运算符动态声明的。这允许你使用 `delete` 运算符移除节点。

```cpp
void destroyList()
{
    NODE* temp = back;
    while(temp != NULL)
    {
        NODE* temp2 = temp;
        temp = temp->previous;
        delete temp2;
    }
    back = NULL;
    front = NULL;
}
```

`destroyList()` 成员函数首先声明指向链表末尾节点的临时指针。然而，在移除节点之前，成员函数通过测试 `temp` 指针是否为 `NULL` 来确定链表末尾是否存在节点。

## 声明节点

| 前置指针 | NULL | 24 | 2 | 1 | 34 | NULL | 后置指针 |

步骤 1 `back->next=n;`

| 节点 1 NULL | 24 | 2 | 1 | 34 | NULL | NULL 节点 3 |

步骤 2 `n->previous=back;`

| 节点 1 NULL | 24 | 2 | 1 | 34 | 2 | 44 | NULL 节点 3 |

步骤 3 `back=n` back=3

**图 6-4** `appendNode()` 成员函数改变了链表中指针指向的节点。

## 数据结构深度解密

```cpp
while(temp != NULL)
{
    cout << " " << temp->data;
    temp = temp->next;
}
```

```cpp
void LinkedList::displayNodesReverse()
{
    cout << "反序排列的节点：";
    NODE* temp = back;
    while(temp != NULL)
    {
        cout << " " << temp->data;
        temp = temp->previous;
    }
}
```

```cpp
void LinkedList::destroyList()
{
    NODE* temp = back;
    while(temp != NULL)
    {
        NODE* temp2 = temp;
        temp = temp->previous;
        delete temp2;
    }
    back = NULL;
    front = NULL;
}
```

最后是使用链表的 C++ 应用程序。我们将该文件命名为 `LinkedListDemo.cpp`，如下所示。令人惊讶的是，与定义 `NODE` 结构和 `LinkedList` 类所使用的所有代码相比，该应用程序本身非常小。

```cpp
// LinkedListDemo.cpp
#include <iostream>
using namespace std;

void main() {
    LinkedList* list = new LinkedList();
    list->appendNode(10);
    list->appendNode(20);
    list->appendNode(30);
    list->displayNodes();
    list->displayNodesReverse();
    delete list;
}
```

应用程序通过声明 `LinkedList` 类的实例开始。正如你在本章早些时候回顾的那样，构造函数初始化了头指针（`front`）和尾指针（`back`）。

该实例使用 `new` 运算符声明。`new` 运算符返回实例内存位置的引用。同一条语句声明了一个指向 `LinkedList` 列表的指针，并将其赋值为 `LinkedList` 类实例的引用。

接下来，调用了三次 `appendNode()` 成员函数。`appendNode()` 成员函数在链表的末尾添加一个新节点，并将传递给 `appendNode()` 成员函数的赋值赋值给节点的数据成员。

示例中的最后两个句子显示了链表中每个节点的数据。首先，调用 `displayNodes()` 成员函数按自然顺序显示节点，从链表的头部开始到链表末尾的节点结束。

接下来，调用 `displayNodesReverse()` 成员函数，其操作与 `displayNodes()` 成员函数相同，但它从尾节点开始，到头节点结束。然后调用 `delete` 运算符从内存中删除 `LinkedList` 类的实例。

以下是代码示例的输出：

```
10
20
30
20
10
```

## 使用 Java 使用链表

链表在 Java 中的实现方式与 C++ 不同，因为 Java 定义了一个 `LinkedList` 类，它作为 Java 集合框架的一部分，位于 `java.util` 包中。

## 数据结构深度解密

Java 的 `LinkedList` 执行与我们在 C++ `LinkedList` 类中定义的相同基本操作。此外，Java `LinkedList` 类还有其他用于操作链表的特性。你将在接下来的两个章节中学习这些内容，其中 `LinkedList` 类将用于实现其他类型的数据结构。现在，我们将为你展示如何使用 Java 实现链表。

使用 `LinkedList` 类的用处是，你只需要创建一个 `LinkedList` 类实例，并根据程序需要调用成员方法来操作链表。

本节的代码示例是本章之前描述的 C++ 应用程序的 Java 版本。你会注意到两个程序非常相似，尽管 Java 应用程序有一些细微差别。

Java 程序中的第一条语句与 C++ 程序中的语句相同。接下来的三条语句声明了 `LinkedList` 类的一个实例。`LinkedList` 类的 `add()` 成员方法在链表的末尾创建一个新节点。

`add()` 成员方法类似于 C++ 程序中的 `appendNode()` 方法。

链表通过 `size()` 成员方法确定链表的节点数量。节点的数据是可以通过调用 `LinkedList` 类的 `get()` 方法获取的。

以下是代码示例的输出：

```
10
20
30
20
10
```

```java
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        for (Integer i : list) {
            System.out.println(i);
        }
        for (int i = list.size()-1; i>=0; i--) {
            System.out.println(list.get(i));
        }
    }
}
```
