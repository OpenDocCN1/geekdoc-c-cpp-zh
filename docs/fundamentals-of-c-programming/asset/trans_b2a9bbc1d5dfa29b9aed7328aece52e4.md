

f();
}

我们可以通过为内部 Node 结构体添加析构函数来验证我们修改后的链表类是否正确释放其动态内存，如下所示：

```
// This is the modified nested, private Node class
struct Node {
    int data;    // A data element of the list
    Node *next;  // The node that follows this one in the list
    Node(int d); // Constructor
    ~Node();     // Destructor
};
};
```

我们还修改了构造函数实现并添加了析构函数实现，如下所示：

```
// Node constructor
IntList2::Node::Node(int n): data(n), next(nullptr) {
    std::cout << "Creating node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

// Node destructor
IntList2::Node::~Node() {
    std::cout << "Destroying node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}
}
```

清单 18.9（intlist3.h）提供了使用此修改后的 Node 嵌套类更新的头文件，清单 18.10（intlist3.cpp）包含实现。

## 清单 18.9：intlist3.h

```
// intlist3.h

class IntList3 {
    // The nested private Node class from before
    struct Node {
        int data;    // A data element of the list
        Node *next;  // The node that follows this one in the list
        Node(int d); // Constructor
        ~Node();     // Destructor
    };

    Node *head;   // Points to the first item in the list
    Node *tail;   // Points to the last item in the list

    int len;      // Number of elements in the list

public:
    // The constructor makes an initially empty list
    IntList3();

    // The destructor that reclaims the list's memory
~IntList3();
// Inserts n onto the back of the list.
void insert(int n);
// Prints the contents of the linked list of integers.
void print() const;
// Returns the length of the linked list.
int length() const;
// Removes all the elements in the linked list.
void clear();
};
```

## 清单 18.10：intlist3.cpp

```
// intlist3.cpp

#include "intlist3.h"
#include <iostream>

// Private IntList3 operations

// Node constructor
IntList3::Node::Node(int n): data(n), next(nullptr) {
  std::cout << "Creating node " << data
    << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

IntList3::Node::~Node() {
  std::cout << "Destroying node " << data
    << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

// The constructor makes an initially empty list.
// The list is empty when head and tail are null.
// The list's length is initially zero.
IntList3::IntList3(): head(nullptr), tail(nullptr), len(0) {}

// The destructor deallocates the memory held by the list
IntList3::~IntList3() {
  clear();
}

// Inserts n onto the back of the list.
// n is the element to insert.
void IntList3::insert(int n) {
  // Make a node for the new element n
  IntList3::Node *new_node = new Node(n);
  if (tail) { // Is tail non-null?
    tail->next = new_node; // Link the new node onto the back
    tail = new_node; // The new node is the new tail of the list
  }
  else // List is empty, so make head and tail point to new node
head = tail = new_node;
    len++; // List now has one more element
}

// Prints the contents of the linked list of integers.
void IntList3::print() const {
    for (auto cursor = head; cursor; cursor = cursor->next)
        std::cout << cursor->data << ' ';
    std::cout << '\n';
}

// Returns the length of the linked list.
int IntList3::length() const {
    return len;
}

// Removes all the elements in the linked list.
void IntList3::clear() {
    auto cursor = head;
    while (cursor) {
        auto temp = cursor;
        cursor = cursor->next;
        delete temp;
    }
    head = tail = nullptr; // Null head signifies list is empty
    len = 0;
}
```

这里，Node 构造函数通过打印其数据字段和驻留内存中的地址来标识它正在创建的元素。C++ 对指针类型与非指针类型之间的转换非常严格——很容易意外进行转换，且几乎从未有意这样做——因此简单的 `static_cast` 在这里无效。`reinterpret_cast` 移除了保护措施，并将构成指针的位视为 `uintptr_t`，这是一种保证能表示与指针相同值范围的整数类型。析构函数指示 Node 对象何时被销毁。清单 18.11（test2.cpp）与清单 18.8（test1.cpp）是同一程序，只是它使用 IntList3 对象而不是 IntList2 对象。

## 清单 18.11：test2.cpp

```
#include <iostream>
#include "intlist3.h"

void f() {
    IntList3 my_list; // Constructor called here
    // Add some numbers to the list
    my_list.insert(22);
    my_list.insert(5);
    my_list.insert(44);
    // Print the list
    my_list.print();
} // my_list goes out of scope; destructor automatically frees its memory

int main() {
    f();
}
```

如果从 IntList3 类中移除析构函数，实际上使其成为没有增强 Node 结构体的 IntList1 类，清单 18.11（test2.cpp）将打印以下内容：

```
Creating node 22 (16846704)
Creating node 5 (16823408)
Creating node -44 (16822992)
22 5 -44
```

（实际内存地址每次运行都会不同，但 Node 数据值将相同。）

该函数创建了三个节点但没有删除任何一个。当此函数返回时，my_list 不再存在，因此我们无法再访问它分配的节点。如果保持 IntList3 不变，清单 18.11（test2.cpp）将打印以下内容：

```
Creating node 22 (19337072)
Creating node 5 (19313328)
Creating node -44 (19313696)
22 5 -44
Destroying node -44 (19313696)
Destroying node 5 (19313328)
Destroying node 22 (19337072)
```

这表明 IntList3 析构函数正确释放了链表对象持有的动态内存。在声明 Node 对象或使用 new 创建 Node 对象以赋值给 Node 指针时，Node 构造函数会执行。insert 方法使用 new 创建 Node 对象，因此会调用构造函数。当对象超出作用域或 delete 释放动态分配的对象时，Node 析构函数会执行。IntList3 析构函数调用 clear 方法，该方法使用 delete 释放列表中的每个节点。

考虑动态分配链表本身（而不仅仅是其节点）的情况：

```
void f2() {
    IntList3 *lptr;    // Pointer, constructor NOT called yet
    lptr = new IntList3;  // Constructor called here
    // Add some numbers to the list
    lptr->insert(22);
    lptr->insert(5);
    lptr->insert(-44);
    // Print the list
    lptr->print();
    delete lptr;    // Destructor called here
}
```

在此 f2 函数中，lptr 不是对象；它是指向对象的指针。声明 lptr 不会创建对象，因此 IntList3 构造函数不会执行。语句

```
lptr = new IntList3;
```

会创建一个对象，因此 IntList3 构造函数会代表 lptr 指向的对象执行。当 lptr 在函数 f2 执行结束时超出作用域，栈变量 lptr 会消失，但由于它是指针而非对象，不会执行任何析构函数代码。客户端必须使用 delete 显式释放内存：

```
delete lptr;    // Destructor called here
```

除非程序员打算让函数将指针返回给客户端（在这种情况下，客户端负责在使用完对象后调用 `delete`）。

如您所见，动态分配列表本身（存储其元素的节点除外）使我们回到了之前的情况。我们必须记住在使用完对象后做些什么。在此情况下，我们必须记住 `delete` 列表本身。析构函数在此无法帮助我们。这是一个很好的示例，表明虽然动态内存使我们能够做许多有趣的事情，但除非绝对必要以实现所需行为，否则最好避免使用它。

析构函数执行与构造函数相反的角色。构造函数确保新对象以明确定义的状态开始其生命周期，而析构函数负责执行对象生命周期结束时所需的操作。对于大多数类，析构函数是不必要的。然而，对于链表对象，析构函数是必不可少的，因为构成链表的节点是使用 `new` 运算符动态分配的。任何使用 `new` 分配的内存在不再使用时都需要相应的 `delete` 调用。clear 方法将处理内存释放，但如果没有析构函数，程序员必须记住在使用完链表对象时有意调用 `clear`。析构函数使程序员免于此责任并消除了内存泄漏的可能性。析构函数只是调用 `clear` 来清理列表持有的资源。

清单 18.12（testdestructors.cpp）演示了执行中的程序如何按创建顺序的逆序销毁局部和全局对象。对于通过 `new` 运算符分配的对象，如在函数 `test_widget_pointers` 中，析构函数仅在对相关指针应用 `delete` 时才执行。

## 清单 18.12：testdestructors.cpp

```
#include <iostream>

class Widget {
public:
  int data;
  Widget(int n): data(n) {
    std::cout << "Creating widget " << data
              << " " << reinterpret_cast<uintptr_t>(this) << "\n";
  }
  ~Widget() {
    std::cout << "Destroying widget " << data
              << " " << reinterpret_cast<uintptr_t>(this) << "\n";
  }
};

// Global widgets
Widget global1(100);
Widget global2(200);

void test_widget_objects() {
  std::cout << "Entering test_widget_objects" << '\n';
  Widget w1(1);
  Widget w2(2);
  Widget w3(3);
  Widget w4(4);
  std::cout << "Leaving test_widget_objects" << '\n';
}

void test_widget_pointers() {
  std::cout << "Entering test_widget_pointers" << '\n';
```
