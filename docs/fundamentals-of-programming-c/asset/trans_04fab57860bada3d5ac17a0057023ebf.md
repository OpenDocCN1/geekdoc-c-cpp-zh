

## 16.4. 链表 (LINKED LISTS)

435

![](img/e326304bd50fbc4f7d5a64c1487eb635_445_0.png)

图 16.1：空终止的链表

## 列表 16.6: intlist.h

```cpp
class IntList {
  * 一个存储链表元素的对象。
  * 此类型局部于 IntList 类，在类外部 
  * 无法访问。
  *
  struct Node {
    int data;        // 列表的数据元素
    Node *next;      // 链表中紧随在该节点之后的节点
    Node(int d);     // 构造函数
  };

  Node *head;      // 指向列表中的第一个项

  // 私有辅助方法

  /*
  * insert(p, n)
  * 将 n 插入到 p 所指向的
  * 列表末尾。
  * p 指向链表中的一个节点
  * n 是要插入的元素。
  * 返回包含 n 的
  * 列表指针。
  */
  Node *insert(Node *p, int n);

  /*
  * print(p)
  * 打印整数链表的内容。
  * p 指向一个节点链表。
  */
  void print(Node *p) const;

  /*
  * 返回 p 所指向的链表的长度。
  */
  int length(Node *p) const;

  /*
  * dispose(p)
  * 释放 p 所指向的列表所持有的内存。
  */
  void dispose(Node *p);

public:
  /*
  * 构造函数创建一个初始空列表
  */
  IntList();

  /*
  * 析构函数释放列表持有的内存
  */
  ~IntList();

  /*
  * insert(n)
  * 将 n 插入到列表末尾。
  * n 是要插入的元素。
  */
  void insert(int n);

  /*
  * print()
  * 打印整数链表的内容。
  */
  void print() const;

  /*
  * 返回链表的长度。
  */
  int length() const;

  /*
  * clear()
  * 移除链表中的所有元素。
  */
  void clear();
};
```

Node 定义在 IntList 类内部。我们称 Node 为一个嵌套类。由于 Node 的声明出现在 IntList 的私有部分，它是一个仅对 IntList 类内部代码可见的类型。Node 类型的完整名称为 IntList::Node。

请注意，IntList 类除了公共方法外，还有几个私有方法。类外部代码无法直接执行这些私有方法。这些私有方法是辅助方法

## 16. 链表 (LINKED LISTS)

公共方法通过调用它们来完成其任务。我们看到公共方法会将工作*委托*给它的私有辅助方法。为什么这种委托是必要的？私有方法使用了递归，需要一个 *IntList::Node* 类型的参数，而该类型在 *IntList* 类外部是未知的。因此，客户端无法直接使用私有方法，即使它们是公开的。公共方法不暴露任何关于类实现的细节；具体来说，它们将 *IntList::Node* head 实例变量隐藏在客户端。

观察到 IntList 类重载的 *print* 和 *length* 方法（包括公共和私有的）都被声明为 *const*。列表或其长度都不应修改 IntList 对象。客户端可以

IntList 类的 *insert* 方法会在向集合中添加元素时使用 *new* 来分配 *Node* 对象。IntList 类的析构函数：

```cpp
~IntList();
```

当 IntList 对象超出作用范围时将释放节点。析构函数将调用 *clear* 来清理列表持有的内存。

为什么不让客户端直接调用 *clear* 来释放列表而不调用析构函数呢？客户端在完成列表后可能会调用 *clear*。产生的内存泄漏可能会导致长时间运行的程序耗内存。有了析构函数，客户端程序员无需担心释放列表，因为析构函数会自动完成工作；例如，考虑以下代码：

```cpp
void f() {
    IntList my_list;           // 此处调用构造函数
    // 向列表添加一些数字
    my_list.insert(22);
    my_list.insert(5);
    my_list.insert(-44);
    // 打印列表
    my_list.print();
} // 函数结束时调用 my_list 的析构函数
```

变量 *my_list* 是函数 *f* 的局部变量。当函数 *f* 执行结束时，my_list 超出作用范围。此时，IntList 的析构函数执行 my_list。析构函数确保了 my_list 分配的内存被释放。在 IntList 指针的上下文中，如

```cpp
void f2() {
    IntList *lptr;           // 指针，尚未调用构造函数
    lptr = new IntList();   // 此处调用构造函数
    // 向列表添加一些数字
    lptr->insert(22);
    lptr->insert(5);
    lptr->insert(-44);
    // 打印列表
    lptr->print();
    // 此处调用析构函数
    delete lptr;
}
```

## 16.4. 链表 (LINKED LISTS)

lptr 不是一个对象；它是一个指向对象的指针。声明 lptr 不会创建对象，因此构造函数不会执行。语句

```cpp
lptr = new IntList;
```

会创建一个对象，因此 IntList 构造函数代表 lptr 指向的对象进行执行。当 lptr 在函数 f2() 执行期间超出作用范围时，栈变量 lptr 消失，但由于它是指针，因此没有执行析构函数。客户端必须显式地释放内存：

```cpp
delete lptr; // 此处调用析构函数
```

除非程序员打算让函数将指针返回给客户端（在这种情况下，客户端负责在完成对象操作后调用 delete）。
列表 16.7 (intlist.cpp) 实现了 16.6 中声明的方法。

## 列表 16.7: intlist.cpp

```cpp
// intlist.cpp

#include "intlist.h"
#include <iostream>

// 私有 IntList 操作

/*
* Node 构造函数
*/
IntList::Node(int n) : data(n), next(nullptr) {}

/*
* insert(p, n)
* 将 n 插入到 p 所指向的
* 列表末尾。
* p 指向链表中的一个节点
* n 是要插入的元素。
* 返回包含 n 的
* 列表指针。
*/
IntList::Node *IntList::insert(IntList::Node *p, int n) {
    if (p != nullptr)
        p->next = insert(p->next, n);
    else
        // 如果 p 为空，则创建一个新节点
        p = new IntList::Node(n);
    return p;
}

/*
* 返回 p 所指向的链表的长度。
*/
int IntList::length(IntList::Node *p) const {
    if (p != nullptr)
        return 1 + length(p->next);
    else
        return 0;
}

/*
* dispose(p)
 * 释放 p 所指向的列表所持有的内存。
 */
void IntList::dispose(IntList::Node *p) {
    if (p != nullptr) {
        dispose(p->next);
        delete p;
    }
}

// 公共 IntList 操作

/*
* 构造函数创建一个初始空列表
 */
IntList::IntList() : head(nullptr) {}

/*
* 析构函数释放列表持有的内存
 */
IntList::~IntList() {
    clear();
}

/*
* insert(n)
* 将 n 插入到列表末尾。
* n 是要插入的元素。
 */
void IntList::insert(int n) {
    head = insert(head, n);
}

/*
* print()
* 打印整数链表的内容。
 */
void IntList::print() const {
    IntList::Node *p = head;
    while (p != nullptr) {
        std::cout << p->data << " ";
        p = p->next;
    }
    std::cout << endl;
}

/*
* 返回链表的长度。
 */
int IntList::length() const {
    return length(head);
}

/*
* clear()
* 移除链表中的所有元素。
 */
void IntList::clear() {
    dispose(head);
    head = nullptr;
}
```

