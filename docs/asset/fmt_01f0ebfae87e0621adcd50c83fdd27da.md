
| gradeBook1 created for: CS101 Introduction to C++ Programming |
| gradeBook2 created for: CS102 Data Structures in C++ |

**图 16.7** | 实例化 `GradeBook` 类的多个对象并使用 `GradeBook` 构造函数在创建每个 `GradeBook` 对象时指定课程名称。（2 部分，共 2 部分）

## 定义构造函数

图 16.7 的第 14–18 行定义了 `GradeBook` 类的构造函数。构造函数的名称与其类名相同，都为 `GradeBook`。构造函数在参数列表中指定了执行其任务所需的数据。当你创建一个新对象时，将这些数据放在对象名称后的括号中（正如我们在第 47–48 行中所所示的那样）。第 14 行表示 `GradeBook` 类的构造函数有一个名为 `name` 的字符串参数。我们声明此构造函数为 `explicit`（显式的），因为它接受单个参数——这对于你将在第 18.13 节中将学习的排序非常重要。目前，只需将所有单参数构造函数声明为 `explicit`。后期构造函数不能声明为 `const`（甚至不能是 `void`）。

构造函数使用成员初始化列表（第 15 行）用构造函数参数 `name` 的值来初始化数据成员 `courseName`。成员初始化器出现在构造函数参数列表与开始结构体体的的左括号之间。

## 16.5 使用构造函数初始化对象

`struct` 之后。成员初始化列表通过冒号 (`:`) 与参数列表隔开。一个成员初始化器由数据成员的变量名后跟包含初始值的括号组成。在这个示例中，`courseName` 使用参数 `name` 的值进行初始化。如果一个类包含多个数据成员，则数据成员初始化器与下一个之间用逗号隔开。成员初始化列表在构造函数执行之前执行。你可以在构造函数体内进行初始化，但你会发现使用成员初始化器效率更高，而且某些类型的数据成员必须被初始化。

注意，构造函数（第 14 行）和 `setCourseName` 函数（第 21 行）都使用了参数名。你可以在不同函数中使用相同的参数名，因为参数是每个函数的局部变量——它们之间不会相互干扰。

## 测试 GradeBook

图 16.7 的第 44–54 行定义了 `main` 函数，用于测试 `GradeBook` 类并使用构造函数初始化 `GradeBook` 对象。第 47 行创建并初始化了 `gradeBook1`。当执行此处时，会调用 `GradeBook` 构造函数（第 14–18 行），传入参数 `"CS103 Introduction to C++ Programming"` 以初始化 `gradebook1` 的课程。第 48 行对 `gradebook2` 重复此过程，这次传递参数 `"CS102 Data Structures in C++"` 以初始化 `gradebook2` 的课程名称。第 51–52 行使用每个 `getCourseName` 成员获取课程名称，并证明它们在对象创建时已通过初始化。输出确认了每个 `GradeBook` 对象都维护着自己的成员 `courseName`。

## 为类提供默认构造函数的方法

任何不接受参数的构造函数都称为默认构造函数。类可以通过以下几种方式获得默认构造函数：

- 1. 编译器在每个没有用户定义构造函数的类中隐式创建一个默认构造函数。默认构造函数不初始化类的数据成员，但会为每个作为另一个类对象的数据成员调用默认构造函数。未初始化的变量包含未定义的（“垃圾”）值。
- 2. 你显式定义一个不接受参数的构造函数。这样的默认构造函数将调用每个作为另一个类对象的数据成员的默认构造函数，并执行额外的初始化。
- 3. 如果你定义了任何带参数的构造函数，C++ 将不会为该类隐式创建一个默认构造函数。我们将展示 C++11 如何强制编译器创建默认构造函数，即使你定义了非默认构造函数。

对于图 16.1、图 16.3 和图 16.5 中的每个版本的 `GradeBook` 类，编译器都显式定义了一个默认构造函数。

![](img/fa81e30d8bce030c9060826ba9997d7b_637_0.png)

> 预防技巧 16.2
> 不需要对类的数据成员进行初始化（几乎不需要），提供构造函数以确保你的类的数据成员用有意义的值进行初始化。

# 606 第 16 章 类、对象与字符串

## 软件工程观察 16.2

数据成员可以在构造函数中初始化（几乎不需要），也可以在对象创建后设置其值。然而，良好的软件工程实践是在客户端代码调用对象的成员函数之前确保对象已完全初始化。

### 为 GradeBook 类添加构造函数
图 16.8 的 UML 类图表示了图 16.7 中的 `GradeBook` 类，该类具有一个类型为 `String` 的构造函数。与操作一样，UML 在类图第三部分中建模构造函数。为了区分构造函数和类的操作，UML 在构造函数名称前使用书名（« 和 »）放置“constructor”。按照惯例，我们将构造函数列在类的第三部分中。

![](img/fa81e30d8bce030c9060826ba9997d7b_638_0.png)

| GradeBook |
| :--- |
| courseName : String |
| <<constructor>> + GradeBook(name : String) |
| setCourseName(name : String) |
| getCourseName() : String |
| displayMessage() |

**图 16.8** | 表示 `GradeBook` 具有一个类型为 `String` 的构造函数的 UML 类图。

## 16.6 将类放在单独的文件中以便于重用

创建类定义的好处之一是，当正确封装后，可以被其他程序员重用。例如，通过包含头文件 `<string>` 在任何 C++ 程序中重用 C++ 标准库类型 `string`（正如你看到的，通过链接到库对象）。

想要使用我们 `GradeBook` 类的程序员不能简单地将图 16.7 中的文件包含另一个文件中。正如你所知，`main` 开始每个程序的执行，如果其他包含图 16.7，他们将得到“行李”—我们的 `main` 函数，并且程序将有两个 `main` 函数。编译带有两个 `main` 函数的程序会导致错误。因此，将 `main` 放在类定义的同一个文件中会防止类被其他程序重用。在本节中，我们将演示如何通过将其分离到另一个文件中来使其可重用。

### 头文件

本章之前的每个示例都由单个 `.cpp` 文件组成，也称为源文件，包含 `GradeBook` 类定义和 `main` 函数。在构建面向对象的 C++ 程序时，习惯是将可重用的源码（如类）定义在具有 `.h` 扩展的文件中——称为头文件。程序使用 `#include` 预处理指令来包含头文件并利用

## 16.6 将类置于单独的文件以实现重用

可重用的软件组件，例如 C++ 标准库提供的 `string` 类型以及用户定义的类型，如 `GradeBook` 类。

我们的下一个示例将图 17 中的代码分成了两个文件——`GradeBook.h`（图 16.9）和 `fig16_10.cpp`（图 16.10）。查看图 16.9 中的头文件时，请注意它只包含了 `GradeBook` 类的定义（第 7–38 行）以及类所依赖的头文件。使用 `GradeBook` 的 `main` 函数定义在源文件 `fig16_10.cpp`（图 16.10）的第 8–18 行。为了帮助你准备书中和工业中更大的程序，我们使用一个包含 `main` 函数的单独源文件来测试我们的类（这是一个驱动程序）。你将学习带有 `main` 函数的源文件如何使用头文件中的类定义来创建类对象。

```cpp
// Fig.16.9: GradeBook.h

// 在与 main 分离的文件中定义 GradeBook 类

#include <iostream>

#include <string> // class GradeBook 使用 C++ 标准 string 类

// GradeBook 类定义

class GradeBook {

public:

    // 构造函数用提供的字符串参数初始化 courseName
    explicit GradeBook(std::string courseName)
        : courseName(courseName) // 成员初始化 courseName
    {
        // 空体
    } // GradeBook 构造函数
    // 设置课程名的函数
    void setCourseName(std::string courseName)
    {
        // 在对象中存储课程名
    } //  setCourseName 函数
    // 获取课程名的函数
    std::string getCourseName() const {
        return courseName; // 返回对象的 courseName
    } // getCourseName 函数
    // 向 GradeBook 显示欢迎消息
    void displayMessage() const {
        // 调用 getCourseName 获取课程名
        cout << "! Welcome to the book\n" << getCourseName();
    } // displayMessage 函数
private:
    std::string courseName; // 此 GradeBook 的课程名
};

// 结束 GradeBook 类
```

图 16.9 | 在与 `main` 分离的文件中定义 `GradeBook` 类

```cpp
// Fig. 10: fig16_10.cpp
// 在 main 中包含 GradeBook.h
#include <iostream>
#include "GradeBook.h" // 包含 GradeBook 类的定义
using namespace std;

// 程序执行开始
int main() {
    // 创建 GradeBook 对象
    GradeBook gradeBook1("CS101 Introduction to C++");
    GradeBook gradeBook2("CS102 Data Structures in C++");
    // 显示每个 GradeBook 的 courseName 值
    cout << "gradeBook1 created for course: " << gradeBook1.getCourseName();
    cout << "\radeBook2 created for course: " << gradeBook2.getCourseName();
    return 0;
}
```

gradeBook1 created for course: CS101 Introduction to C++
gradeBook2 created for course: CS102 Data Structures in C++

**图 16.10** 在 `main` 中包含 `GradeBook.h` 以包含 `GradeBook` 类

**在头文件中使用 std::**
在整个头文件（图 16.9）中，我们在引用 `string`（第 11、18、24 行）、`cout`（第 33 行）和 `endl`（第 34 行）时使用了 `std::`。由于后续章节将解释的微妙原因，头文件永远不应该包含指令或 `using` 声明。

**包含用户定义类的头文件**
作为 `GradeBook.h` 的头文件（图 16.9）不能作为一个完整的程序使用，因为它不包含 `main` 函数。要使用它，必须编写一个包含 `main` 函数的单独源文件（如图 16.10 所示）来实例化并使用类。

编译器不知道 `GradeBook` 是什么，因为它是一个用户定义的类型。事实上，编译器甚至不知道 C++ 标准库中的类。为了帮助理解如何使用，我们必须显式地包含类的定义——例如，为了使用 `string` 类型，程序必须包含 `<string>` 头文件。这允许编译器确定为每个 `string` 对象预留的内存，并确保程序正确调用 `string` 的成员函数。

要创建图 16.10 中第 11–12 行的 `gradeBook1` 和 `gradeBook2` 对象，编译器必须知道 `GradeBook` 对象的大小。虽然概念上对象包含成员变量和成员函数，但 C++ 对象只包含数据。编译器只为类的成员函数创建一个副本并在所有对象之间共享它。当然，每个对象都需要自己的成员变量，因为它们的内容在对象之间可能会变化（例如两个 `BankAccount` 对象有两个不同的余额）。然而，成员函数代码是不可修改的，因此可以在所有对象之间共享。因此，对象的大小取决于存储类成员变量所需的内存量。通过在第 4 行包含 `GradeBook.h`，我们为编译器提供了它所需的信息（图 16.9，第 37 行），以确定 `GradeBook` 对象的大小并判断类对象是否被正确使用（在图 16.10 的第 11-12 行和 15-16 行）。

第 4 行指示 C++ 处理器在程序编译之前将 `#include` 指令替换为 `GradeBook` 内容的副本（即类定义）。当编译源文件 `fig16_10.cpp` 时，它现在包含了 `GradeBook` 类定义，编译器能够确定如何创建对象，并看到它们的成员函数被正确调用。现在类定义位于头文件中（没有 `main` 函数），我们可以将其包含在任何需要重用我们类的程序中。

为了确保预处理器能够正确找到头文件，`#include` 指令应将用户定义的头文件放在引号中（例如 `"GradeBook.h"`），并将 C++ 标准库头文件放在角括号中（`<iostream>`）。

### 额外的软件工程问题
现在 `GradeBook` 定义在头文件中，该类是可重用的。遗憾的是，像图 16.9 所示将类定义置于头文件中会向客户端泄露类的完整实现——`GradeBook.h` 是一个任何人都可以打开并阅读的简单文本。传统的软件工程认为，为了使用类的对象，客户端代码需要知道调用哪些成员函数、为每个成员函数提供什么参数以及期望从每个成员函数获得什么返回类型。如果客户端代码知道类的实现，它可能基于类的实现来编写代码。理想情况下，如果实现发生变化，类代码就不需要改变。隐藏类的实现使得改变类变得更容易。

在 16.7 节中，我们展示了如何将 `GradeBook` 类分成两个文件，以便：
- 类是可重用的
- 客户端知道类提供了哪些函数、如何调用它们以及期望的返回类型
- 客户端不知道类的实现

## 16.7 分离接口与实现

在前节中，我们展示了如何通过将类定义与客户端代码（例如 `main` 函数）分离来提高重用性。我们现在引入另一个良好的软件工程原则——分离接口与实现。

### 类的接口
接口定义了人与系统相互交互的方式。例如，控件是用户与其内部组件之间的接口。接口允许用户执行一组操作（如切换电台、调节音量和在 AM 和 FM 之间切换）。接口指定了这些允许的操作，但没有指定如何实现。同样，类的接口描述了客户端可以使用什么以及如何请求这些服务，但没有指定类如何实现这些。类的公共接口由类的公共成员组成（称为类的公共服务）。例如，`GradeBook` 的接口（图 16.9）包含了构造函数以及成员函数 `setCourseName`、`getCourseName` 和 `displayName`。`GradeBook` 的客户端（例如图 16.10 中的 `main`）使用这些函数来请求这些服务。

## 16.7 接口与实现的分离

`public interface` 在不泄露类成员函数实现的情况下定义类。函数原型是函数的声明，它告诉编译器函数的返回类型以及其各个参数的类型。此外，头文件仍然指定了类的私有数据成员（第 16 行）。编译器必须知道类的数据成员，以便确定为该类的每个对象预留多少内存。在客户端中包含头文件 `GradeBook.h` 以确保（16.13 的第 5 行），为编译器提供了所需的信息，以确保客户端正确地调用 `GradeBook` 的成员函数。

```cpp
// 图 16.11: GradeBook.h
// GradeBook 类定义。此文件展示了 GradeBook 的公共
// 接口，而不暴露 GradeBook 公共函数的实现，
// 这些函数定义在 GradeBook.cpp 中。

// <string> //类 GradeBook 使用 C++ 标准字符串类
// GradeBook 类定义
class GradeBook {
public:
    explicit GradeBook(std::string); // 构造函数初始化 courseName
    void setCourseName(std::string name); // 设置课程名称
    std::string getCourseName() const; // 获取课程名称
    void displayMessage() const; // 显示欢迎消息
private:
    std::string courseName; // 此 GradeBook 的课程名称
};
```
