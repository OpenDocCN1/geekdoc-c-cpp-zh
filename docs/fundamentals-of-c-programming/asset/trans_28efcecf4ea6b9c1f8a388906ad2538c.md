

```
Widget *p1 = new Widget(10);
Widget *p2 = new Widget(20);
Widget *p3 = new Widget(30);
Widget *p4 = new Widget(40);
delete p2;
delete p1;
delete p4;
// Not deleting p3, introducing a memory leak
std::cout << "Leaving test_widget_pointers" << '\n';
}
```

```
int main() {
  std::cout << "Entering main" << '\n';
  test_widget_objects();
  test_widget_pointers();
  std::cout << "Leaving main" << '\n';
}
```

清单 18.12 (testdestructors.cpp) 打印如下内容：

```
Creating widget 100 (2707068)
Creating widget 200 (2707064)
Entering main
Entering test_widget_objects
Creating widget 1 (14024180)
Creating widget 2 (14024184)
Creating widget 3 (14024188)
Creating widget 4 (14024192)
Entering test_widget_objects
Destroying widget 4 (14024192)
Destroying widget 3 (14024188)
Destroying widget 2 (14024184)
Destroying widget 1 (14024180)
Entering test_widget_pointers
Creating widget 10 (14790752)
Creating widget 20 (14790816)
Creating widget 30 (14790832)
Creating widget 40 (14791760)
Destroying widget 20 (14790816)
Destroying widget 10 (14790752)
Destroying widget 40 (14791760)
Leaving test_widget_pointers
Leaving main
Destroying widget 200 (2707064)
Destroying widget 100 (2707068)
```

为 IntList1 类添加析构函数是纠正其缺陷的重要一步，但其后继类 IntList2 和 IntList3 仍不适合正式发布。请考虑清单 18.13 (listassign.cpp)，它使用了能够正确自动清理内存的 IntList3 类。

## 清单 18.13: listassign.cpp

```
#include "intlist3.h"
#include <iostream>

void f() {
    IntList3 seq1, seq2; // Create two empty integer linked lists

    seq1.insert(10); // Build the list [10]-->[-2]-->[8]
    seq1.insert(-2);
    seq1.insert(8);
    seq1.print();

    seq2.insert(5); // Build the list [5]-->[4]
    seq2.insert(4);
    seq2.print();

    std::cout << "\n--------------\n";

    seq1 = seq2; // What does this do?
    seq1.print();
}

int main() {
    f();
    std::cout << "All done\n";
}
```

清单 18.13 (listassign.cpp) 构建两个独立的链表，然后将一个链表赋值给另一个。在某个系统上，程序打印

```
Creating node 10 (14457304)
Creating node -2 (14457592)
Creating node 8 (14456152)
10 -> -2 -> 8
Creating node 5 (14456200)
Creating node 4 (14456248)
5 4
---------------
5 4
Destroying node 4 (14456248)
Destroying node 5 (14456200)
Destroying node 4 (14456248)
Destroying node 5 (14456200)
All done
```

在此次特定运行中，程序运行至完成；然而，有时程序会在打印 All done 之前崩溃。在某些系统上，程序会在打印最后三行输出之前崩溃。

在此次清单 18.13 (listassign.cpp) 的运行中，输出显示程序从未销毁包含 10、-2 和 8 的节点。此外，程序销毁了包含 4 和 5 的节点两次！我们可以通过比较括号中的内存地址，看到程序删除了同一内存两次。这种双重删除的未定义行为正是导致程序有时崩溃的原因。

问题出在这条语句：

```
seq1 = seq2;
```

这条语句究竟做了什么？

## 图 18.4 IntList3 赋值的概念视图。赋值后，两个链表对象别名同一组节点，seq1 的原始列表变得不可达。

![](img/e84ad11adb18201d71595b31ce6c9eff_580_0.png)

在没有程序员额外指导的情况下，程序员定义类型的赋值运算符只是将赋值运算符右侧对象所占内存中的比特位复制到赋值运算符左侧对象保留的内存中。例如，在 Visual C++ 生成 32 位可执行文件时，IntList3 对象占用 12 字节内存——head 指针占 4 字节，tail 指针占 4 字节，len 占 4 字节。IntList3 对象的实际大小因系统而异，在 64 位计算机上会更大。你可以通过在清单 18.13 (listassign.cpp) 中添加以下语句来验证系统上 IntList3 对象的实际大小：

```
std::cout << sizeof seq1 << '\n'; // Prints 12 or 24 under Visual C++
```

赋值

```
seq1 = seq2;
```

只是将 seq2.head 复制到 seq1.head，将 seq2.tail 复制到 seq1.tail，并将 seq2.len 复制到 seq1.len。这会产生三种不良结果：

- 别名。赋值后，对象 seq1 和 seq2 引用同一组节点。有关赋值过程的示意图，请参见图 18.4。

这意味着任何对 seq1 管理的列表的修改都会以相同方式修改 seq2。赋值运算符不会复制 seq2 的内容。这意味着我们的链表对象在赋值方面与 std::vector 对象的行为不同：将一个向量赋值给另一个向量会复制所包含的元素。客户端会期望我们的链表对象表现得类似。然而，这个别名问题虽然不受欢迎，却导致了我们当前 IntList3 实现中的两个严重缺陷：

- **内存泄漏。** 只需将 `seq1` 的 `head` 和 `tail` 指针重定向到 `seq2` 的列表，`seq1` 原始列表中的节点就无法从程序中的任何变量访问到。程序无法 `delete` `seq1` 原始列表中的节点。这构成了内存泄漏。

- **内存损坏。** `seq1` 和 `seq2` 都是 `main` 函数的局部对象。根据声明顺序，`seq1` 的构造函数在 `seq2` 的构造函数之前执行。这意味着当 `main` 执行完毕时，`seq2` 的析构函数会在 `seq1` 的析构函数之前执行。对于局部对象，对象销毁的顺序与对象构造顺序相反。`seq2` 的析构函数将释放 `seq2` 列表中的所有节点。接下来，`seq1` 的析构函数将尝试 `delete` 其列表所占用的内存。不幸的是，这涉及引用和删除之前由 `seq2` 删除的动态内存。任何尝试 `delete` 已删除内存的行为都会导致 `undefined behavior`，这通常会导致内存损坏。这就是为什么清单 18.13 (listassign.cpp) 在某些运行中会崩溃。

幸运的是，C++ 为程序员提供了一种自定义自定义类型赋值行为的方法。在处理赋值本身之前，我们必须区分 _初始化_ 和 _赋值_。请考虑以下语句：

```
int x = 3;
```

这条语句定义并 _初始化_ 变量 `x` 为 3。这条语句与以下两条语句根本不同：

```
int x;
x = 3;
```

对于整数、浮点数和字符等简单类型，这两条语句在表面上与上面的单条语句行为相同。事实上，这两条语句涉及声明后跟赋值。初始化和赋值不是同一回事。回顾第 3.2 节中的初始化替代语法：

```
int x{3};
```

对编译器而言，这条语句与上面的初始化语句等效。然而，请注意，以下代码序列是不合法的：

```
int x;
x{3};   // Illegal
```

C++ 赋予程序员对自定义类型初始化和赋值的完全控制权。我们已经看到如何通过构造函数指定初始化。为了使我们的链表类合法化并使其对客户端使用安全，我们需要提供一个额外的构造函数，称为 _拷贝构造函数_，并为类定义赋值运算符。

名为 `X` 的类的拷贝构造函数具有以下形式：

```
class X {
  // Other stuff for class X
  X::X(const X& other);
};
```

参数是同一类型对象的引用。

要指定赋值，我们提供形式如下的 `operator=` 方法：

```
class X {
    // Other stuff for class X
    X& operator=(const X& other);
};
```

请注意，赋值运算符接受类类型的常量引用参数，并返回类类型的引用。

清单 18.14 (intlist4.h) 扩展了清单 18.9 (intlist3.h)，提供拷贝构造和赋值。

## 清单 18.14: intlist4.h

```
// intlist4.h

class IntList4 {
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
    IntList4();

    // The destructor that reclaims the list's memory
    ~IntList4();

    // Copy constructor
    IntList4(const IntList4& other);

    // Assignment operator
    IntList4 operator=(const IntList4& other);

    // Inserts n onto the back of the list.
    void insert(int n);

    // Prints the contents of the linked list of integers.
    void print() const;

    // Returns the length of the linked list.
    int length() const;

    // Removes all the elements in the linked list.
    void clear();
};

