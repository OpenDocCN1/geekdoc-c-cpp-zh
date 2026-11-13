
除了在类定义中声明静态成员常量外，程序还必须在实现文件中重复声明该常量。在我们的示例中，以下单行必须出现在实现文件中：const bag::size_type bag::CAPACITY;

我们已经描述了静态成员常量的一般格式，但需要注意一些陷阱：

- 关键字 static 在实现文件中不重复，因为 static 在类定义之外具有不同的含义。
- 在实现文件中声明常量时，必须使用完整的类型名称（例如 bag::size_type），而不是简写版本（例如 size_type），因为简写版本只能在类定义或成员函数的实现中使用。
- 在实现文件中，还必须使用常量的完整名称（例如 bag::CAPACITY），而不是简写版本（例如 CAPACITY），否则编译器不会知道这是类的成员。

为便于日后参考，以下是静态成员常量的摘要，包括关于不同类型常量的初始值必须出现在何处的说明。

## 澄清 const 关键字 第 4 部分：静态成员常量

静态成员常量在类中的声明前有两个关键字 static 和 const。例如，在我们的 bag 类定义中：

```
static const size_type CAPACITY = 30;
```

关键字 static 表示整个类只有一个该成员的副本，关键字 const 表示程序不能更改该值（这与普通声明的常量类似）。

除了在类定义中声明静态成员常量外，还必须在实现文件中不带关键字 static 地重新声明该常量。例如：

```
const bag::size_type bag::CAPACITY;
```

请注意，初始值（例如 30）仅在头文件中给出，而不是在实现文件中。但是，在头文件中定义值的技术仅允许用于整数类型，例如 int 和 size_t。非整数类型必须采用相反的方式，即将值留在头文件之外，并在实现文件中定义该值。造成这种差异的原因是，整数值通常在类定义中用于定义诸如数组大小之类的内容。

## 较旧的编译器不支持静态成员常量的初始化

在类定义中初始化和使用静态成员常量的功能是一个相对较新的特性。如果你有一个不支持静态常量成员的旧编译器，那么附录 E“处理旧编译器”为你的编程提供了一种替代方案。

## Bag 类—文档

我们现在对 bag 类了解足够多，可以编写头文件的文档，如图 3.1 所示。我们为这个头文件使用了名称 bag1.h，因为它是我们计划实现的几种不同 bag 的第一个。

文档包括关于两个 typedef 语句（value_type 和 size_type）和静态成员常量（CAPACITY）的信息。特别是，请注意，我们对 value_type 所需的数据类型进行了非常具体的说明。value_type 可以是 C++ 内置数据类型中的任何一种（例如 int 或 char），也可以是带有默认构造函数、赋值运算符以及用于测试相等性（x == y）和不等性（x != y）的运算符的类。

花点时间阅读并理解图 3.1 中的所有前置条件，例如 += 运算符的这个前置条件：

> 前置条件：size() + addend.size() <= CAPACITY.

在这个前置条件中，size() 指的是激活该函数的 bag 的大小，CAPACITY 指的是激活该函数的 bag 的容量。另一方面，addend.size() 指的是 addend 的大小，addend 是该函数的一个参数。

## 图 3.1 Bag 头文件文档

## 头文件文档

```
// FILE: bag1.h
// CLASS PROVIDED: bag (part of the namespace main_savitch_3)
// TYPEDEFS and MEMBER CONSTANTS for the bag class:
//   typedef ____ value_type
//     bag::value_type is the data type of the items in the bag. It may be any of the C++
//     built-in types (int, char, etc.), or a class with a default constructor, an assignment
//     operator, and operators to test for equality (x == y) and non-equality (x != y).
// typedef __ size_type
// bag::size_type is the data type of any variable that keeps track of how many items
// are in a bag.
// static const size_type CAPACITY = __
// bag::CAPACITY is the maximum number of items that a bag can hold.
// CONSTRUCTOR for the bag class:
// bag( )
// Postcondition: The bag has been initialized as an empty bag.
// MODIFICATION MEMBER FUNCTIONS for the bag class:
// size_type erase(const value_type& target)
// Postcondition: All copies of target have been removed from the bag.
// The return value is the number of copies removed (which could be zero).
// bool erase_one(const value_type& target)
// Postcondition: If target was in the bag, then one copy has been removed;
// otherwise the bag is unchanged. A true return value indicates that one
// copy was removed; false indicates that nothing was removed.
// void insert(const value_type& entry)
// Precondition: size( ) < CAPACITY.
// Postcondition: A new copy of entry has been added to the bag.
// void operator +=(const bag& addend)
// Precondition: size( ) + addend.size( ) <= CAPACITY.
// Postcondition: Each item in addend has been added to this bag.
// CONSTANT MEMBER FUNCTIONS for the bag class:
// size_type size( ) const
// Postcondition: The return value is the total number of items in the bag.
// size_type count(const value_type& target) const
// Postcondition: The return value is number of times target is in the bag.
// NONMEMBER FUNCTIONS for the bag class:
// bag operator +(const bag& b1, const bag& b2)
// Precondition: b1.size( ) + b2.size( ) <= bag::CAPACITY.
// Postcondition: The bag returned is the union of b1 and b2.
// VALUE SEMANTICS for the bag class:
// Assignments and the copy constructor may be used with bag objects.
```

## 记录值语义

value_type 的一个要求可能看起来很奇怪——为什么我们要求 value_type“必须有赋值运算符”？难道每种数据类型都允许诸如 x = y 这样的赋值吗？难道总会有一个自动赋值运算符吗？不！例如，当 x 和 y 是数组时，x = y 是被禁止的。稍后我们将看到其他需要小心定义赋值运算符实际含义的数据类型。

## Bag 类—演示程序

有了文档，我们可以编写一个使用 bag 的程序。我们不需要知道函数是如何实现的。例如，图 3.2 中出现了一个演示程序。该程序询问用户家庭成员的年龄。用户输入年龄，后跟一个负数以表示输入结束，这些年龄被放入一个 bag 中。然后程序要求用户再次输入年龄，作为一个简单的测试。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_134_0.png)

## 一个程序

```
// FILE: bag.demo.cxx
// This is a small demonstration program showing how the bag class is used.
#include <iostream> // Provides cout and cin
#include <cstddef> // Provides EXIT_SUCCESS
#include "bag1.h" // With value_type defined as an int
using namespace std;
using namespace main_savitch_3;

// PROTOTYPES for functions used by this demonstration program:
void get_ages(bag& ages);
// Postcondition: The user has been prompted to type in the ages of family members. These
// ages have been read and placed in the ages bag, stopping when the bag is full or when the
// user types a negative number.

void check_ages(bag& ages);
// Postcondition: The user has been prompted to type in the ages of family members again.
// Each age is removed from the ages bag when it is typed, stopping when the bag is empty.

int main( )
{
    bag ages;

    get_ages(ages);
    check_ages(ages);
    cout << "May your family live long and prosper." << endl;
    return EXIT_SUCCESS;
}
```
