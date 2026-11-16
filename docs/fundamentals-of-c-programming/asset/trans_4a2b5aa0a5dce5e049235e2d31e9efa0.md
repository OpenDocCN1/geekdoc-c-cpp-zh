

```cpp
class X2 {
public:
    int data;
    X2(int n) : data(n) {}
};
```

这里程序员提供了一个显式构造函数，因此编译器不会生成默认构造函数。这意味着以下语句是非法的：

```
X2 my_x2; // Illegal; the client must provide an integer
```

如果我们确实希望客户端能够有或没有整数参数地创建对象，我们可以重载构造函数（提供我们自己的默认构造函数），或者使用 `default` 标签强制编译器为我们生成一个，如下所示：

```
class X3 {
public:
    int data;
    X3() = default; // Allow compiler to generate default constructor
    X3(int n) : data(n) {} // and provide our own
};
```

这使得以下两个语句都成为可能：

```
X3 my_x3a;
X3 my_x3b(4);
```

我们可以通过将编译器通常会提供的默认构造函数标记为 `delete` 标签，来阻止编译器生成其默认构造函数，如下所示：

```
class X4 {
public:
    int data;
    X4() = delete;
};
```

你是否注意到，我们在链表示例中使用的 Node 嵌套结构体中违反了三法则？我们添加了析构函数，但没有提供拷贝构造函数，也没有定义拷贝赋值运算符。我们如何为这一决定辩护？

实际上，Node 结构体不需要析构函数。链表类即使使用没有析构函数的 Node 内部结构，也能完美运行。Node 结构体内部没有任何代码分配资源。外部链表类负责分配和释放内存资源。链表方法将 Node 对象作为被动数据来操作。我们添加析构函数仅是为了能够准确看到程序何时销毁了一个 Node 对象。这使我们能够检测内存泄漏和多次删除，并将我们的链表类改进为一个健壮的实用工具。Node 析构函数既不清理任何资源，也不做任何会影响编译器生成的拷贝构造函数或编译器生成的拷贝赋值运算符所要完成的工作的事情。请记住，除非你有非常充分的理由不这样做，否则应当遵循三法则。在我们的情况中，充分的理由是我们的析构函数不做任何会促使我们编写自己的拷贝构造函数和拷贝赋值运算符以便与析构函数正确协调的事情。

为了强调我们违反三法则的有意决定，我们可以将 Node 结构体重写为

```
struct Node {
    int data;        // A data element of the list
    Node* next;      // The node that follows this one
    Node(int d);     // Constructor
    Node(const Node&) = default; // Copy constructor
    Node(Node&&) = default;      // Move constructor
    ~Node();         // Destructor
    Node& operator=(const Node&) = default; // Copy assignment
    Node& operator=(Node&&) = default;      // Move assignment
};
```

通过显式默认拷贝构造函数和拷贝赋值运算符，我们表明我们并非偶然遗漏了它们。包含析构函数会阻止编译器自动生成移动构造函数和移动赋值运算符。通过将这两个方法声明为 default，编译器会为我们生成它们。

由于我们的 Node 对象仅包含简单类型（一个 int 和一个指针），我们可以省略上述声明中的所有显式默认方法，而不会有任何不同。这是因为 C++ 仅仅通过复制来“移动”一个整数。一个简单的整数没有我们需要从临时对象中窃取的资源；只需简单的赋值即可。同样，一个指针可能指向某个复杂的对象，但指针本身仅仅是一个地址。复制和移动构造是相同的，复制和移动赋值的处理方式也相同。

## 18.6 智能指针

使用 new 和 delete 手动管理动态内存的 C++ 程序员遵循的是直接从 C 语言继承的风格。许多现代编程语言（如 Python、Java 和 C#）通过一种称为垃圾回收的技术来管理动态内存。垃圾回收负责处理避免多次删除和内存泄漏所需的记账工作。在垃圾回收语言中，程序员只需调用相当于 new 的操作；当执行中的程序不再使用动态分配的对象时，垃圾回收器会负责稍后释放空间。垃圾回收效果不错，但它确实会给执行中的程序增加一些开销。这种开销会消耗一些额外内存，并可能影响程序的运行时效率。C++ 致力于尽可能高效，因此不提供自动垃圾回收器。垃圾回收语言通常将所有对象都分配在堆上，从而以统一的方式管理对象。C++ 支持静态分配和栈分配的对象，以及堆分配的对象。堆分配稍慢，且堆碎片化会进一步降低程序性能。C++ 遵循“你只为所用付费”的格言，意味着不需要堆的程序不会承担使用堆的运行时成本。

C++ 提供了非垃圾回收语言的效率优势，并在需要时具备垃圾回收的便利性。C++ 通过多种方式实现这一点。我们已经见过并享受其益处一段时间的一种方式是：std::vector 类在幕后使用 new 和 delete 来管理动态数组。软件工程师仔细实现了 std::vector，以做正确的事情，避免别名、内存泄漏和多次删除。

现代 C++ 使得编写不直接使用 new 或 delete 来管理动态内存的程序成为可能。这种风格使用智能指针；也就是说，指针“知道”确切何时释放它们引用的内存。

C++ 智能指针消除了程序员进行此类手动干预的需要。智能指针会在适当的时间自动删除其关联的内存。std::shared_ptr 类型是标准 C++ 智能指针的一个示例。

假设我们有以下 Widget 类型：

```
struct Widget {
    int data;
    Widget(int n) : data(n) { }
};
```

以下代码在堆上创建一个 Widget 对象，并将其赋值给名为 p 的 std::shared_ptr 对象：

```
std::shared_ptr<Widget> p(new Widget(12));
```

泛型 std::make_shared 函数提供了一种更方便的方式来创建 std::shared_ptr 对象：

```
std::shared_ptr<Widget> p = std::make_shared<Widget>(12);
```

std::make_shared 函数消除了对 new 运算符的需求。它在幕后使用 new 来为其创建的对象分配必要的内存，但程序员看不到 new。在对象生命周期的另一端，使用智能指针时程序员永远不会调用 delete；智能指针会在适当的时间自动调用 delete。使用 std::make_shared 函数使程序员能够处理动态分配的内存，而无需直接使用 new 和 delete。这消除了困扰手动内存管理的内存泄漏和多次删除的可能性。

我们可以使用 auto 的类型推断能力，以更简单的方式表达智能指针的创建：

```
auto p = std::make_shared<Widget>(12);
```

在表达式 std::make_shared<Widget>(12) 中，尖括号内的名称是要创建的对象的类型，括号内的值是要传递给该类型构造函数的参数。编译器知道该函数将返回 std::shared_ptr<Widget> 类型，因此无需在左侧明确写出 p 的精确类型。

一旦以这些方式之一定义了 p，我们就可以在语法上将其视为原始指针；例如：

```
// Make p point to a dynamically created a Widget object
auto p = std::make_shared<Widget>(12);
std::cout << p->data << '\n'; // Prints 12
p->data = 5;
std::cout << p->data << '\n'; // Prints 5
```

清单 18.21 (simplesharedptrtest.cpp) 提供了一个使用 std::shared_ptr 对象进行一些简单测试的程序。

## 清单 18.21: simplesharedptrtest.cpp

```
#include <iostream>
#include <string>
#include <memory>

struct Widget {
    static unsigned id_source; // Source of unique IDs
```

