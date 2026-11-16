
```cpp
}
~Widget() {
    std::cout << "Destroying widget " << value << '\n';
}
};

Widget global_w(5);

std::shared_ptr<Widget> get_widget1() {
    // Caller need not deallocate the returned object
    return std::make_shared<Widget>(10);
}

Widget *get_widget2() {
    // Caller must NOT deallocate the returned object
    // as it points to a global variable not dynamically
    // allocated
    return &global_w; // No allocation
}

void process() {
    auto p1 = get_widget1();
    std::cout << p1->value << '\n';
    auto p2 = get_widget2();
    std::cout << p2->value << '\n';
}

int main() {
    std::cout << "Entering main\n";
    process();
    std::cout << "Leaving main\n";
}
```

清单 18.22 (smartdelete.cpp) 的输出显示，程序正确销毁了其创建的 Widget 对象。

```
Creating widget 5
Entering main
Creating widget 10
10
5
Destroying widget 10
Leaving main
Destroying widget 5
```

std::shared_ptr 智能指针如何“知道”何时调用 delete 来释放其对象？

给定以下 Widget 类型：

```
struct Widget {
    int value;
    Widget(int value): value(value) {}
};
```

以下语句：

```
auto p = std::make_shared<Widget>(3);
```

创建一个引用包含值 3 的 Widget 对象的智能指针。当我们重新赋值变量 p 时，与 p 关联的对象会发生什么？以下语句：

```
// p is the Widget object created above
p = nullptr;
```

这会将 p 重定向为不指向任何对象。此时，没有变量引用先前创建的 Widget 对象。这意味着该对象实际上已与程序其余部分的执行隔离。这种被废弃的对象被归类为垃圾。垃圾是计算机科学中的一个技术术语，指的是执行程序分配但程序已无法访问的内存。std::shared_ptr 类型使用一种称为引用计数的技术，以自动回收被废弃对象所占用的空间。

引用计数垃圾回收的工作原理如下。通过 std::shared_ptr 构造函数或 std::make_shared 便捷函数动态创建的所有对象都有一个关联的引用计数。当执行程序创建由 std::shared_ptr 对象管理的新对象时，它会将共享指针对象的引用计数设置为 1。执行以下语句后：

```
auto p = std::make_shared<Widget>(3);
```

p 的引用计数为 1。引用计数为 1 意味着恰好有一个共享指针对象（在此例中为 p）被分配给该对象。创建别名，如下所示：

```
q = p;
```

将 p 的引用计数加一。p 和 q 共享同一对象并共享同一引用计数。如果我们创建另一个别名，如下所示：

```
r = p;
```

赋值语句将对象的引用计数增加到 3。如果重新赋值 p、q 或 r，如下所示：

```
q = std::make_shared<Widget>(22);
```

包含值 3 的小部件的引用计数减一，新小部件对象（包含值 22）的引用计数变为 1。如果我们随后重新赋值 p，例如：

```
p = nullptr;
```

这使得只有变量 r 引用包含值 3 的小部件，因此其引用计数为 1。如果我们最后重新赋值 r：

```
r = nullptr;
```

包含值 3 的小部件的引用计数降至零。std::shared_ptr 类具有一个自定义赋值运算符。赋值过程会更改通过这些智能指针管理的对象的引用计数。当赋值会导致共享指针对某个对象的引用计数变为零时，共享指针可以在附加到正在赋值的对象之前删除该对象。赋值会将正在赋值的对象的引用计数加一。

std::shared_ptr 类具有一个名为 use_count 的方法，用于返回共享指针当前管理的对象的引用计数。清单 18.23 (refcount.cpp) 利用此 use_count 方法来演示引用计数垃圾回收的工作原理。

## 清单 18.23: refcount.cpp

```cpp
#include <iostream>
#include <memory>

class Widget {
public:
    Widget() {
        std::cout << "Creating a widget ("
                  << reinterpret_cast<uintptr_t>(this)
                  << ")\n";
    }
    ~Widget() {
        std::cout << "Destroying a widget ("
                  << reinterpret_cast<uintptr_t>(this)
                  << ")\n";
    }
};

int main() {
    auto p = std::make_shared<Widget>();
    std::cout << p.use_count() << "\n"; // Prints 1
    auto q = p;
    std::cout << p.use_count() << "\n"; // Prints 2
    auto r = p;
    std::cout << p.use_count() << "\n"; // Prints 3
    r = nullptr;
    std::cout << p.use_count() << "\n"; // Prints 2
    q = nullptr;
    std::cout << p.use_count() << "\n"; // Prints 1
    p = nullptr;
    std::cout << p.use_count() << "\n"; // Prints 0
}
```

清单 18.23 (refcount.cpp) 输出：

```
Creating a widget (20338980)
1
2
3
2
1
Destroying a widget (20338980)
0
```

观察对象如何从引用计数 1 过渡到引用计数 0，从而自动删除小部件对象并调用其析构函数。

在清单 18.24 (intlist6.h) 中，我们重构了来自清单 18.18 (intlist5.h) 的链表类，以使用 std::shared_ptr 对象而非原始指针。

## 清单 18.24: intlist6.h

```cpp
// intlist6.h

#include <memory> // For std::shared_ptr

class IntList6 {
// The nested private Node class from before
struct Node {
    int data; // A data element of the list
    std::shared_ptr<Node> next; // The node that follows this one
    Node(int d); // Constructor
    Node(const Node&) = default; // Copy constructor
    Node(Node&&) = default; // Move constructor
    ~Node(); // Destructor
    Node& operator=(const Node&) = default; // Copy assignment
    Node& operator=(Node&&) = default; // Move assignment
};

std::shared_ptr<Node> head; // Points to the first item in the list
std::shared_ptr<Node> tail; // Points to the last item in the list
int len; // Number of elements in the list

public:
// The constructor makes an initially empty list
// IntList6();

// The destructor that reclaims the list's memory
~IntList6();

// Copy constructor
IntList6(const IntList6& other);

// Move constructor
IntList6(IntList6&& other);

// Assignment operator
IntList6& operator=(const IntList6& other);

// Move assignment operator
IntList6& operator=(IntList6&& other);

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

清单 18.25 (intlist6.cpp) 实现了在清单 18.24 (intlist6.h) 中声明的方法。

## 清单 18.25: intlist6.cpp

```cpp
// intlist6.cpp

#include "intlist6.h"
#include <iostream>
#include <utility>

// Private IntList6 operations

// Node constructor
IntList6::Node::Node(int n): data(n), next(nullptr) {
    std::cout << "Creating node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

IntList6::Node::~Node() {
    std::cout << "Destroying node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

// The constructor makes an initially empty list.
// The list is empty when head and tail are null.
IntList6::IntList6(): head(nullptr), tail(nullptr), len(0) {}

// Copy constructor makes a copy of the other object's list
IntList6::IntList6(const IntList6& other): IntList6() {
    // Walk through other's list inserting each of its elements
    // into this list
    for (auto cursor = other.head; cursor; cursor = cursor->next)
        insert(cursor->data);
}

// Move constructor takes possession of the temporary's list
IntList6::IntList6(IntList6&& temp): IntList6() {
    // Swap contents with the temporary
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);
}

// Assignment operator
IntList6& IntList6::operator=(const IntList6& other) {
    // Make a local, temporary copy of other
    IntList6 temp(other);

    // Exchange the head and tail pointers and len from this list
    // with those of the new, temporary list
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);

    // The temporary list now points to this list's original contents,
    // and this list now points to the copy of other's list
    // The temporary list will be destroyed since it is a temporary
    return *this;
}
```
