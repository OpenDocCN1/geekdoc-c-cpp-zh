
- 关联 (association)
- 基类 (base class)
- 组合 (composition)
- 依赖 (dependency)
- 派生类 (derived class)
- 继承 (inheritance)
- 实例树 (instance tree)
- 里氏替换原则 (Liskov substitution principle)
- 多重性 (multiplicity)
- 私有继承 (private inheritance)
- 保护继承 (protected inheritance)
- 保护成员 (protected member)
- 公有继承 (public inheritance)
- 子类 (subclass)
- 超类 (superclass)

## 总结

面向对象编程中的继承从通用概念推导出更具体的概念。更通用的类称为基类，更具体的称为派生类。派生类继承基类的所有成员，参数除外。

546 第 11 章 类之间的关系

面向对象编程中的继承从通用概念推导出更具体的概念。更通用的类称为基类，更具体的称为派生类。派生类继承基类的所有成员，参数除外。

面向对象编程中的继承从通用概念推导出更具体的概念。更通用的类称为基类，更具体的称为派生类。派生类继承基类的所有成员，参数除外。

面向对象编程中的继承从通用概念推导出更具体的概念。更通用的类称为基类，更具体的称为派生类。派生类继承基类的所有成员，参数除外。

565 第 11 章 类之间的关系

...第二个。依赖是。

# 第11章

PR-9. 为程序 11.6 中 `main` 与 `Person` 和 `Student` 对象的交互画一张序列图。

PR-10. 为程序 11.6 中 `main` 与 `Person` 和 `Date` 对象的交互画一张序列图。注意我们有两个 `Person` 类实例和两个 `Date` 类实例。

PR-11. 为程序 11.21 中对象的交互画一张序列图。

# 程序

+   PRG-1. 设计一个名为 `Square` 的类来定义正方形几何形状。该类必须有一个名为 `side` 的数据成员来定义每边的长度。定义两个成员函数 `getPeri` 和 `getArea` 来计算正方形的周长和面积。现在定义一个 `Cube` 来定义立方体并继承自 `Square` 类。`Cube` 不需要新的数据成员，但需要 `getArea` 和 `getVolume` 成员函数。为这两个类提供适当构造函数和析构函数。

+   PRG-2. 设计一个 `Rectangle` 类，包含两个数据成员：`length` 和 `width`。为该类定义构造函数和析构函数，并编写计算矩形周长和面积的成员函数。然后定义一个继承自 `Rectangle` 的 `Cuboid` 类，增加一个成员 `height`。然后为 `Cuboid` 编写构造函数，并编写计算 `Cuboid` 对象表面积和体积的成员函数。

+   PRG-3. 创建一个继承自 `Circle` `Sphere`。我们知道可以通过绕直径旋转圆来创建一个球对象。

    a. 为 `circle` 类设计接口，包含一个数据成员：`radius`。为该类定义参数化构造函数和析构函数，并使用以下关系编写计算圆周长和面积的成员函数。

    b. 为 `Sphere` 类定义接口文件。为该类定义参数化构造函数和析构函数，并编写计算球表面积和体积的成员函数。

    c. 为 `Sphere` 类定义实现文件，使用以下公式计算球的表面积和体积；在公式中，`perimeter` 是 (b) 中定义的圆周，`area` 是 (b) 中定义的圆面积。

| perimeter = 2 * π radius | area = π * radius * radius |

| surface = 2 * radius * perimeter | volume = (4 / 3) * π * radius * radius |

+   PRG-4. 创建一个继承自 `Circle` 的 `Cylinder`。我们知道可以通过给圆对象添加高度来创建一个圆柱对象。

    a. 按照 PRG-3 所示为名为 `circle` 的类设计接口。

    b. 为名为 `Cylinder` 的类定义接口文件。同样为该类定义参数化构造函数和析构函数，并编写计算体积的成员函数。

    c. 为 `Cylinder` 类定义实现文件，使用以下公式计算圆柱的表面积和体积；在这些公式中，`perimeter` 是圆柱的周长，`area` 是 (b) 中定义的类面积。

| surface = height * perimeter | volume = height * area |

    d. 编写应用文件来测试 `Circle` 和 `Cylinder` 类。创建一个简单的员工类，支持两种类型的员工：月薪制（salaried）和计时制（hourly）。所有员工都有四个数据成员：`name`、`employee number`、`birth date` 和 `date hired`。月薪制员工有月薪和年奖金（比例在 0% 到 10% 之间）。计时制员工有时薪和加班费（范围在 50% 到 100% 之间）。

**PRG-5.**

**PRG-6.** 设计一个 `Student` 类，包含两个数据成员：`name` 和 `gpa`。定义一个 `Course` 类，其数据成员持有课程中的学生人数和一个在堆内存中创建的学生数组。`Student` 类必须有一个打印学生对象信息的函数。`Course` 类必须包含关于学生选修课程的信息，并打印所有已课学生的信息。

**PRG-7.** 设计一个 `Course` 类，包含两个数据成员：`name` 和 `units`。设计一个 `Student` 类，包含三个数据成员：`name`、`gpa` 和在内存中实现的课程列表。为 `Course` 和 `Student` 类的操作创建构造函数、析构函数和所有必要的成员函数。在应用程序中测试这两个类。

**PRG-8.** 编写一个程序来模拟下面所示定义的三个类：

![](img/ce9c99d45f71111839bc062830bd19fd_569_0.png)

+   a. 使用 `name` 作为 `Person` 类的唯一数据成员。

    b. 使用 `name` 和 `gpa` 作为 `Student` 类的数据成员。

    c. 使用 `name` 和 `salary` 作为 `Employee` 类的数据成员。

**PRG-9.** 编写程序模拟下面所示定义的七个类。前三个类（`Person`、`Student` 和 `Employee`）已 PRG-8 中定义。编写代码定义其他四个类。

![](img/ce9c99d45f71111839bc062830bd19fd_569_1.png)

# 第11章 类之间的关系

+   a. 为 *Undergraduate*（本科）类使用 **year** (1, 2, 3, 4)。

    b. 为 *Graduate*（研究生）类使用 **goal** (master, phd)。

    c. 为 *Staff*（员工）类使用 **status** (manager, nonmanager)。

    d. 为 *Professor*（教授）类使用 **status** (part-time, full-time)。

我们建议使用 *enum*。

**PRG-10.** 设计一个 `Point` 类，包含两个数据成员：`x` 和 `y`。为该类定义构造函数和析构函数，并编写计算两点间距离的成员函数。然后定义一个继承自 `Point` 的 `Rectangle` 类，增加一个成员 `length`。然后为 `Rectangle` 编写构造函数，并编写计算 `Rectangle` 对象周长和面积的成员函数。

**PRG-11.** 创建一个继承自 `Rational` 的 `Fraction`。我们知道可以通过对两个分数进行加、减、乘、除来创建一个分数对象。

## 示例 12.1

程序 12.1 显示了一个仅使用前两个条件的不完全多态程序。我们定义了两个类。然后我们创建一个指针（模拟套接字），它可以在不同时间接受每个类的一个对象（插拔兼容对象）。为了简单起见，我们为每个类只定义了一个公共成员函数，并让系统添加析构函数。

程序 12.1 一个不完全的多态程序

```cpp
/***************************************************/
 * 一个显示多态前两个条件的简单程序 |
 * 态 |
/**************************************************/
#include <iostream>
#include <string>
using namespace std;
// 基类的定义和内联打印函数
class Base {
public:
    void print() const { cout << "In the Base" << endl; }
};
// 派生类的定义和内联打印函数
class Derived : public Base {
public:
    void print() const { cout << "In the Derive" << endl; }
};
int main () {
    // 创建指向基类的指针（模拟套接字）
    Base* ptr;
    // 让 ptr 指向基类对象
    ptr = new Base();
    ptr->print();
    delete ptr;
    // 让 ptr 指向派生类对象
    ptr = new Derived();
    ptr->print();
    delete ptr;
    return 0;
}
```

运行：

In the Base

In the Base

# 第 12 章 多态性与其他问题

在第 27 行，*ptr* 指向一个 *Base* 类的对象，在第 28 行，我们调用了在 *Base* 类中定义的函数。在第 31 行，我们让同一个指针指向一个 *Derived* 类的对象，在第 32 行，我们尝试调用在 *Derived* 类中定义的函数，但结果显示调用的是为 *Base* 类定义的函数。多态的前两个条件在程序中实现了，但第三个条件（虚）没有满足。该函数不是一个*virtual*函数。

这个结果是预之中的，因为变量 *ptr* 被定义为指向 *Base* 的指针。它可以接受指向一个 *Derived* 类型对象，因为派生对象是一个 *Base* 对象（继承定义了“is-”关系）。然而，当它想要调用函数时，它仍然是一个 *Base* 指针，所以它调用了在 *Base* 类中定义的 *print* 函数。我们没有更改指针的类型；只是强制它指向了 *Derived* 类。

## 示例 12.2

我们重复了之前的示例，但我们将 print 函数设为虚函数。结果是在每次调用时都激活正确的函数，如程序 12.2 所示。在第 13 行和第 19 行，我们为 *print* 函数添加了 *virtual* 修饰符。第 28 行调用了适用于基类的相应 *print* 函数，第 32 行调用了适用于派生类的相应 *print* 函数。

程序 12.2 使用所有三个条件的有效多态程序

```cpp
****************************************************************
* 一个简单的程序，证明如果满足了所有三个必要的
* 条件，我们就拥有多态性。
****************************************************************/
#include <iostream>
#include <string>
using namespace std;
// 基类的定义和 print 函数的内联定义
class Base
{
public:
    virtual void print() const { cout << "In the Base" << endl; }
};
// 派生类的定义和 print 函数的内联定义
class Derived : public Base
{
public:
    virtual void print() const { cout << "In the Derive" << endl; }
};
int main () {
    // 创建指向基类的指针（模拟对象）
    Base* ptr;
}
```

（续）

# 程序 12.2 使用所有三个条件的有效多态程序（续）

```cpp
// 让 ptr 指向一个基类对象
ptr = new Base();
ptr->print();
delete ptr;
// 让 ptr 指向一个派生类对象
ptr = new Derived();
ptr->print();
delete ptr;
return 0;
}
```

运行：

In the Base

In the Derived

# 虚函数修饰符并非必要

尽管我们向 print 函数添加了虚修饰符，但并不是需要的。当一个函数被定义为虚函数时，类层次结构中所有相同签名的函数都会自动成为虚函数。

# 机制

为了理解虚函数如何参与多态行为，我们必须理解虚函数表（*vtables*）。在多态中，系统为类层次结构中的每个类创建一个虚函数表。vtable 中的每个条目都有指向对应虚函数的指针。应用程序中创建的每个对象都将有一个额外的数据成员，该成员指向相应的 vtable。在我们这个简单程序中，有两个对象和两个虚表，每个虚表有一个条目，如图 12.2 所示。

当 ptr 指向基类对象时，到达对象添加的 VPTR 指针，它指向基类的虚表。在这种情况下，虚表只有一个条目，调用了基类中唯一的虚函数。当 ptr 指向派生类对象时，到达派生类对象的虚表，并调用了派生类中定义的 print 函数。

![](img/ce9c99d45f71111839bc062830bd19fd_575.png)

图 12.2 基类和派生类的虚表

## 12.1.2 构造函数和析构函数

类层次结构中的构造函数和析构函数也是成员函数，尽管是特殊的。它们需要声明为虚函数吗？我们分别讨论构造函数和析构函数。

# 构造函数不能是虚的

构造函数不能是虚的，因为构造函数是成员函数，基类和派生类的名称不同。

# 虚析构函数

尽管我们向 print 函数添加了虚修饰符，但并不是需要的。当一个函数被定义为虚函数时，类层次结构中所有相同签名的函数都会自动成为虚函数。为了回答这个问题，让我们看看两种情况：

情况1：多态

假设析构函数不是虚的。图 12.3 显示了一个没有使用多态的程序。

| 名称 | 堆内存 |

| --- | --- |

| 基对象 | 字符 |

| 派生对象 | |

在第一种，指针 ptr 指向基类型，delete 可以删除基对象。当基对象被删除时，会调用它的析构函数，从而调用字符串类的析构函数。堆中的字符被释放了。没有内存泄漏。

在第二种情况下，指针 ptr 仍然指向基类型，这意味着它可以删除一个 Student 类对象（它不存在，所以什么都不会发生），当 Student 对象没有被删除时，它的析构函数没有被调用，这意味着字符串类的析构函数没有被调用，堆中的字符没有被释放。我们有了内存泄漏。Student 对象占用的内会在离开作用范围时最终会被释放，但指向字符的指针变成了悬空指针，系统永远无法删除字符串中的内存位置。

情况2：多态

现在析构函数是虚的。图 12.4 显示了一个使用了多态的程序。

| 名称 | 堆内存 |

| --- | --- |

| 基对象 | 字符 |

| 派生对象 | 字符 |

解决方案是将基类的析构函数设为虚函数，这会自动使派生类的析构函数成为虚函数。系统还允许不同名称的成员函数为虚，它们都会被添加到虚函数表中。表 12.5 显示虚函数表中有两个条目，当堆中的对象被删除时，程序知道应该调用哪个析构函数

```cpp
C++ 建议我们在多态中始终为基类定义显式的析 并将其设为虚。使用虚析构函数可以防止多态中可能的内存泄漏。
```

## 第 12 章 多态与其他问题

图 12.5 使用虚析构函数时的虚表

示例 12.3

我们展示了如何通过指向 Person 类的指针利用多态来打印 Student 类中的信息。

程序 12.3 显示了 Person 类的接口文件。

### 程序 12.3 文件 Person.h

```cpp
****************************************/
* Person 类的接口文件 *
****************************************/
#ifndef PERSON_H
#define PERSON_H
#include <iostream>
#include <string>
using namespace std;

class Person
{
private:
    string name;
public:
    Person (string name);
    virtual ~Person ()
    virtual void print () const;
};
#endif
```

### 程序 12.4 文件 person.cpp

```cpp
************************************************
* Person 类的实现文件
************************************************/
#include "Person.h"

// Person 构造函数的定义
Person :: Person (string nm)
: name (nm)
{
    // Person 析构函数的定义（虚函数）
}

Person :: ~Person ()
{
}

// print 函数的定义（虚函数）
void Person :: print () const
{
    cout << "Name: " << name << endl;
}
```

（注）
