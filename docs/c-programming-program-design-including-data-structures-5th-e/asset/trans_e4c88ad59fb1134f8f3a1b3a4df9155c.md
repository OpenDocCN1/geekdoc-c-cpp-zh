
接下来，我们定义 `class listType`，将列表实现为一个 ADT。通常，在列表中，我们不仅存储元素，还要记录列表中元素的数量。因此，我们的 `class listType` 有两个成员变量：一个用于存储元素，另一个用于记录列表中元素的数量。下面的 `class listType` 将列表定义为 ADT。

```cpp
class listType
{
public:
    bool isEmptyList() const;
    bool isFullList() const;
    int search(int searchItem) const;
    void insert(int newElement);
    void remove(int removeElement);
    void destroyList();
    void printList() const;
    listType(); //constructor

private:
    int list[1000];
    int length;
};
```

图 11-10 显示了类 `listType` 的 UML 类图。

![](img/f97f778697507bb6fdd80c5991210cba_673_0.png)

**图 11-10** 类 `listType` 的 UML 类图

## 结构体与类

第 10 章将 `struct` 定义为组件的固定集合，其中组件可以具有不同的类型。`struct` 中组件的这一定义仅包含成员变量。然而，C++ 的 `struct` 与 C++ 的 `class` 非常相似。与类一样，`struct` 的成员也可以是函数，包括构造函数和析构函数。`struct` 与 `class` 的唯一区别在于，默认情况下，`struct` 的所有成员都是 `public`，而 `class` 的所有成员都是 `private`。你可以在 `struct` 中使用成员访问说明符 `private` 将某个成员设为 `private`。

在 C 中，`struct` 的定义与第 10 章给出的 C++ 中 `struct` 的定义相似。由于 C++ 由 C 演变而来，标准的 C 结构体在 C++ 中完全可以使用。然而，C++ 中 `struct` 的定义已被扩展，以包含成员函数、构造函数和析构函数。将来，由于 `class` 是一个语法上独立的实体，专门设计用于处理 ADT，`class` 的定义可能会以与类 C 的 `struct` 的定义完全不同的方式演变。

C++ 的 `classes` 和 `structs` 具有相同的能力。然而，大多数程序员限制结构体的使用，以遵循其类 C 的结构体形式，因此不使用它们来包含成员函数。换句话说，如果 `class` 的所有成员变量都是 `public`，并且该 `class` 没有成员函数，你通常会使用 `struct` 来对这些成员进行分组。事实上，本书就是这样做的。

## 信息隐藏

上一节定义了 `class` `clockType` 来实现程序中的时间。然后我们编写了一个使用 `class` `clockType` 的程序。事实上，我们将 `class` `clockType` 与函数定义结合起来，以实现操作和函数 main，从而完成程序。也就是说，`class` `clockType` 的规格说明和实现细节被直接纳入程序中。

将类的规格说明和实现细节包含在程序中是一种好做法吗？绝对不是。不这样做有几个原因。假设 `class` 的定义和成员函数的定义被直接包含在用户程序中。那么用户就可以直接访问类的定义和成员函数的定义。因此，用户可以随意修改操作。用户也可以随意修改对象的成员变量。因此，从这个意义上说，对象的 `private` 成员变量对该对象而言不再是 `private`。

如果多个程序员在项目中使用同一个对象，并且他们可以直接访问该对象的内部部分，那么就无法保证每个程序员都会以完全相同的方式使用同一个对象。因此，我们必须隐藏实现细节。用户只应知道对象做什么，而不是它如何做。隐藏实现细节使用户不必在程序中加入这段额外的代码。此外，通过隐藏细节，我们可以确保在整个项目中以完全相同的方式使用对象。此外，一旦对象被编写、调试并经过正确测试，它就会变得（并保持）无错误。

![](img/f97f778697507bb6fdd80c5991210cba_674_0.png)

本节讨论如何隐藏对象的实现细节。为便于说明，我们将使用类 **clockType**。

要在程序中实现 **clockType**，用户必须声明 **clockType** 类型的对象，并知道允许哪些操作以及这些操作做什么。因此，用户必须能够访问规格说明细节。由于用户不关心实现细节，我们必须将这些细节放在一个单独的文件中，称为**实现文件**。此外，由于规格说明细节可能太长，我们必须使用户不必将它们直接包含在程序中。然而，用户必须能够查看规格说明细节，以便正确调用函数等。因此，我们必须将规格说明细节放在一个单独的文件中。包含规格说明细节的文件称为**头文件**（或**接口文件**）。

实现文件包含用于实现对象操作的函数定义。该文件包含 C++ 语句以及其他内容（例如预处理指令）。由于 C++ 程序只能有一个函数 main，实现文件不包含函数 main。只有用户程序包含函数 main。由于实现文件不包含函数 main，我们无法从该文件生成可执行代码。事实上，我们从实现文件生成所谓的目标代码。然后，用户将实现文件生成的目标代码与使用该类的程序的目标代码链接起来，以创建最终的可执行代码。

最后，头文件的扩展名为 h，而实现文件的扩展名为 cpp。假设类 clockType 的规格说明细节位于名为 clockType 的文件中。那么该文件的完整名称应为 clockType.h。如果类 clockType 的实现细节位于某个文件中——例如 clockTypeImp——则该文件的名称必须是 clockTypeImp.cpp。

文件 clockTypeImp.cpp 只包含函数的定义，不包含类的定义。因此，为了解决未声明标识符（例如函数名和变量名）的问题，我们借助 include 语句将头文件 clockType.h 包含在文件 clockTypeImp.cpp 中。任何使用类 clockType 的程序，以及定义类 clockType 操作的实现文件，都需要以下 include 语句：

```cpp
#include "clockType.h"
```

请注意，头文件 clockType.h 用双引号括起来，而不是尖括号。头文件 clockType.h 称为用户定义的头文件。通常，所有用户定义的头文件都用双引号括起来，而系统提供的头文件（例如 iostream）则括在尖括号之间。

实现部分包含函数的定义，而这些定义对用户是隐藏的，因为通常*仅*向用户提供目标代码。

然而，类的用户应了解特定函数做什么以及如何使用它。因此，在包含函数原型的规格说明文件中，我们加入注释，简要描述函数，并说明任何前置条件和/或后置条件。

**前置条件：** 一条说明在调用函数之前必须为真的条件的语句。

**后置条件：** 一条说明在函数调用完成后为真的语句。

以下是类 clockType 的规格说明文件和实现文件：

```cpp
//clockType.h, the specification file for the class clockType

class clockType
{
public:
    void setTime(int hours, int minutes, int seconds);
        //Function to set the time.
        //The time is set according to the parameters.
        //Postcondition: hr = hours; min = minutes;
        //               sec = seconds;
        //               The function checks whether the
        //               values of hours, minutes, and seconds
        //               are valid. If a value is invalid, the
        //               default value 0 is assigned.

    void getTime(int& hours, int& minutes, int& seconds) const;
        //Function to return the time.
        //Postcondition: hours = hr; minutes = min;
        //               seconds = sec;

    void printTime() const;
        //Function to print the time.
        //Postcondition: The time is printed in the form
        //               hh:mm:ss.

    void incrementSeconds();
        //Function to increment the time by one second.
        //Postcondition: The time is incremented by one second.
        //               If the before-increment time is
        //               23:59:59, the time is reset to 00:00:00.

    void incrementMinutes();
        //Function to increment the time by one minute.
        //Postcondition: The time is incremented by one minute.
        //               If the before-increment time is
        //               23:59:53, the time is reset to 00:00:53.

    void incrementHours();
        //Function to increment the time by one hour.
        //Postcondition: The time is incremented by one hour.
        //               If the before-increment time is
        //               23:59:53, the time is reset to 00:59:53.
```
