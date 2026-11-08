
与任何其他数据类型一样，ADT 也关联三样东西：ADT 的名称，称为**类型名**；属于该 ADT 的值的集合，称为**域**；以及作用于这些数据的操作集合。遵循这些约定，我们可以如下定义 clockType ADT：

```
dataTypeName
    clockType
domain
    Each clockType value is a time of day in the form of hours,
        minutes, and seconds.
operations
    Set the time.
    Return the time.
    Print the time.
    Increment the time by one second.
    Increment the time by one minute.
    Increment the time by one hour.
    Compare the two times to see whether they are equal.
```

### 示例 10-7

列表定义为同一类型的值的集合。因为列表中的所有值都属于同一类型，所以表示和处理列表的一种便捷方式是使用数组。你可以如下将列表定义为 ADT：

```
dataTypeName
    listType
domain
    Every listType value is an array of, say, 1000 numbers.
operations
    Check to see whether the list is empty.
    Check to see whether the list is full.
    Search the list for a given item.
    Delete an item from the list.
    Insert an item in the list.
    Sort the list.
    Destroy the list.
    Print the list.
```

下一个显而易见的问题是：如何在程序中实现 ADT。要实现 ADT，必须表示数据并编写算法来执行操作。

上一节使用类将数据和函数组合在一起。此外，我们对类的定义只包含操作的规格说明；实现这些操作的函数是单独编写的。因此，我们看到类是实现 ADT 的一种便捷方式。事实上，在 C++ 中，类就是专门为处理 ADT 而设计的。

接下来，我们定义类 `listType`，以将列表实现为 ADT。通常在列表中，我们不仅存储元素，还要记录列表中元素的数量。因此，我们的类 `listType` 有两个成员变量：一个用于存储元素，另一个用于记录列表中元素的数量。下面的类 `listType` 将列表定义为 ADT。

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
    listType(); // constructor

private:
    int list[1000];
    int length;
};
```

图 10-10 展示了类 `listType` 的 UML 类图。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_703_0.png)

**图 10-10** 类 `listType` 的 UML 类图

## 结构体与类

第 9 章将结构体定义为组件的固定集合，其中组件可以具有不同类型。结构体中组件的这一定义只包含成员变量。然而，C++ 结构体与 C++ 类非常相似。与类一样，结构体的成员也可以是函数，包括构造函数和析构函数。结构体与类唯一的区别是：默认情况下，结构体的所有成员都是 public，而类的所有成员都是 private。你可以在结构体中使用成员访问说明符 private 使某个成员成为 private。

在 C 中，结构体的定义与第 9 章给出的 C++ 中结构体的定义相似。由于 C++ 是从 C 演变而来的，标准的 C 结构体在 C++ 中完全可以接受。然而，C++ 中结构体的定义被扩展为包含成员函数、构造函数和析构函数。将来，由于类是语法上独立的实体，是专门为处理 ADT 而设计的，因此类的定义可能会以与类 C 结构体的定义完全不同的方式演变。

C++ 类和结构体具有相同的能力。然而，大多数程序员限制结构体的使用，以遵循其类 C 结构体的形式，因此不使用结构体来包含成员函数。换句话说，如果一个类的所有成员变量都是 public，并且该类没有成员函数，那么通常使用结构体来组合这些成员。事实上，本书就是这样做的。

## 信息隐藏

上一节定义了类 clockType 以在程序中实现时间。然后我们编写了一个使用类 clockType 的程序。事实上，我们将类 clockType 与函数定义结合起来实现操作，并与函数 main 结合起来完成程序。也就是说，类 clockType 的规格说明和实现细节被直接合并到程序中。

将类的规格说明和实现细节包含在程序中是一种好做法吗？绝对不是。不这样做有几个原因。假设类的定义和成员函数的定义被直接包含在用户程序中。那么用户就可以直接访问类的定义和成员函数的定义。因此，用户可以随意修改操作。用户也可以随意修改对象的成员变量。因此，在这个意义上，对象的私有成员变量对该对象而言不再是私有的。

如果多个程序员在一个项目中使用同一个对象，并且他们可以直接访问该对象的内部部分，那么就无法保证每个程序员都会以完全相同的方式使用同一个对象。因此，我们必须隐藏实现细节。用户应该只知道对象做什么，而不知道它是如何做的。隐藏实现细节使用户不必将这段额外的代码放入程序中。此外，通过隐藏细节，我们可以确保对象在整个项目中以完全相同的方式使用。而且，一旦对象编写、调试并经过适当测试，它就会变得（并保持）无错误。

本节讨论如何隐藏对象的实现细节。为便于说明，我们将使用类 `clockType`。

要在程序中实现类 `clockType`，用户必须声明 `clockType` 类型的对象，并知道允许哪些操作以及这些操作做什么。因此，用户必须能够访问规格说明细节。由于用户不关心实现细节，我们必须将这些细节放在一个单独的文件中，称为**实现文件**。此外，由于规格说明细节可能太长，我们必须使用户不必将它们直接包含在程序中。然而，用户必须能够查看规格说明细节，以便正确调用函数等。因此，我们必须将规格说明细节放在一个单独的文件中。包含规格说明细节的文件称为**头文件**（或**接口文件**）。

实现文件包含用于实现对象操作的函数定义。该文件除其他内容（如预处理器指令）外，还包含 C++ 语句。由于一个 C++ 程序只能有一个函数 `main`，所以实现文件不包含函数 `main`。只有用户程序包含函数 `main`。由于实现文件不包含函数 `main`，我们无法从该文件生成可执行代码。事实上，我们从实现文件生成所谓的目标代码。然后，用户将实现文件生成的目标代码与使用该类的程序的目标代码链接起来，以创建最终的可执行代码。

最后，头文件的扩展名为 h，而实现文件的扩展名为 cpp。假设类 `clockType` 的规格说明细节位于名为 `clockType` 的文件中。该文件的完整名称应为 `clockType.h`。如果类 `clockType` 的实现细节位于一个文件中——比如 `clockTypeImp`——则该文件的名称必须是 `clockTypeImp.cpp`。

文件 `clockTypeImp.cpp` 只包含函数的定义，而不包含类的定义。因此，为了解决未声明标识符（如函数名和变量名）的问题，我们借助 `#include` 语句将头文件 `clockType.h` 包含到文件 `clockTypeImp.cpp` 中。任何使用类 `clockType` 的程序，以及定义类 `clockType` 函数的实现文件，都需要下面这条语句：

```cpp
#include "clockType.h"
```

注意，头文件 `clockType.h` 是用双引号括起来的，而不是尖括号。头文件 `clockType.h` 称为用户定义的头文件。通常，所有用户定义的头文件都用双引号括起来，而系统提供的头文件（如 `iostream`）则括在尖括号之间。

实现文件包含函数的定义，而这些定义对用户是隐藏的，因为通常只向用户提供目标代码。
