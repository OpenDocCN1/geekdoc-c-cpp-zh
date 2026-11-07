
- c. 使用以下公式为 *Cylinder* 类定义一个实现文件，以求出圆柱体的表面积和体积；在这些公式中，*perimeter* 是圆的周长，*area* 是 (b) 部分中定义的圆的面积。

  | 表面积 = 高度 * 周长 | 体积 = 高度 * 面积 |
  | --- | --- |
- d. 编写一个应用程序文件来测试 *Circle* 和 *Cylinder* 类。

- **PRG-5.** 创建一个简单的员工类，支持两类员工：受薪员工和小时工。所有员工都有四个数据成员：*姓名*、*员工编号*、*出生日期* 和 *受雇日期*。受薪员工有月薪和年度奖金，奖金以 0% 到 10% 之间的百分比表示。小时工有小时工资和加班费率，加班费率范围为 50% 到 100%。

- **PRG-6.** 设计一个名为 *Student* 的类，具有两个数据成员：*姓名* 和 *平均绩点*。然后定义一个名为 *Course* 的类，其数据成员 *容量* 保存课程中的学生人数，以及一个在堆内存中创建的学生数组。*Student* 类必须有一个成员函数来打印学生对象的信息。*Course* 类必须具有注册学生到课程中的信息，并且必须打印所有已注册学生的信息。

- **PRG-7.** 设计一个名为 *Course* 的类，具有两个数据成员：*名称* 和 *学分*。然后设计一个名为 *Student* 的类，具有三个数据成员：*姓名*、*平均绩点* 和已修课程列表。该列表必须在堆内存中实现为数组。为 *Course* 和 *Student* 类的操作创建构造函数、析构函数和所有必要的成员函数。在应用程序中测试这两个类。

- **PRG-8.** 编写一个程序，模拟如下所示的三个类：

  ![](img/d68f6199646ca63591a6d8419e0ed4ba_569_0.png)

  - a. 使用 *姓名* 作为 *Person* 类的唯一数据成员。
  - b. 使用 *姓名* 和 *平均绩点* 作为 *Student* 类的数据成员。
  - c. 使用 *姓名* 和 *薪水* 作为 *Employee* 类的数据成员。

- **PRG-9.** 编写一个程序，模拟如下所示的七个类。前三个类（*Person*、*Student* 和 *Employee*）已在 PRG-8 中定义。编写代码定义其他四个类。

  ![](img/d68f6199646ca63591a6d8419e0ed4ba_569_1.png)

## 12 多态性及其他问题

在本章中，我们讨论多态性以及与面向对象编程相关的其他问题。多态性使我们能够在一个函数的不同类中编写多个版本。我们还将讨论与多态性相关的另外两个问题：抽象类和多重继承。

### 目标

阅读并学习本章后，您应该能够：

- 定义多态性并描述实现它所需的三个必要条件。
- 定义虚表以及它们如何帮助系统在运行时决定使用哪个虚函数。
- 讨论虚析构函数以及为什么正确使用多态性需要它们。
- 区分继承中的静态绑定和动态绑定。
- 讨论运行时类型信息 (RTTI) 及其使用方式。
- 讨论抽象类及其用途。
- 讨论接口类及其用途。
- 讨论多重继承及其相关问题。
- 展示如何使用虚基继承和类混合来消除多重继承中重复数据成员的问题。

### 12.1 | 多态性

在前面的章节中，我们提到面向对象编程的主要支柱之一是**多态性**。多态性使我们能够编写一个函数的多个版本，每个版本位于不同的类中。然后，当我们调用该函数时，会执行与被引用对象相适应的版本。我们在日常语言中也能看到相同的概念。我们用一个动词（*函数*）表示不同的含义。例如，我们说“打开”，意思是打开门、罐子或书；具体打开哪个由上下文决定。类似地，在 C++ 中，我们可以调用一个名为 *printArea* 的函数来打印三角形的面积或矩形的面积。

为了更好地理解多态性的概念，我们必须首先理解插接兼容对象的概念。与电气设备的类比可能会有帮助，如图 12.1 所示。

![](img/d68f6199646ca63591a6d8419e0ed4ba_572_0.png)

假设我们有两个电气设备（例如台灯和电视机）。我们只有一个插座，一次只能为其中一个设备供电。每个设备都有一个插头，可以插入这个唯一的插座。在时刻 t1，我们将台灯插入插座。在时刻 t2，我们拔下台灯，将电视机插入插座。我们可以这样做，因为这两个设备是插接兼容的；它们的插头遵循相同的标准。插接兼容设备的有趣之处在于，它们都从插座获得相同的东西（电力），但各自执行不同的任务。

**12.1.1 多态的条件**

我们通过将多态性与插头进行比较，来定义继承中多态的条件。

**指针或引用**

为了进行比较，我们需要某种东西扮演插座的角色，一旦创建，就可以接受插接兼容对象。在 C++ 中，指针或引用可以扮演这个角色。我们可以定义一个指针（或引用），它可以指向基类；然后我们可以让该指针指向层次结构中的任何对象。因此，指针和引用变量有时被称为多态变量。

**可交换对象**

我们需要扮演设备角色的插接兼容对象。继承层次结构中的对象扮演这个角色。

**虚函数**

我们需要某种东西扮演提供给执行不同任务的不同设备的电力角色。在 C++ 中，这是通过虚函数完成的，虚函数由关键字 virtual 修饰。例如，我们可以在所有类中都有一个 print 函数，名称都相同，但每个函数打印的内容不同。

> **对于多态，我们需要指针（或引用），需要可交换对象，并且需要虚函数。**

**示例 12.1**

程序 12.1 展示了一个不完整的多态程序，仅使用了前两个条件。我们定义了两个类。然后我们创建一个指针（模拟插座），它可以在不同时间接受每个类的对象（插接兼容对象）。为简单起见，我们只为每个类定义一个公有成员函数，并让系统添加默认构造函数。

**程序 12.1** 一个不完整的多态程序

```cpp
/**************************************************************
 * A simple program to show the first two conditions for       *
 * polymorphism                                                *
 **************************************************************/
#include <iostream>
#include <string>
using namespace std;

// Definition of Base class and in-line print function
class Base
{
    public:
        void print () const {cout << "In the Base" << endl;}
};
// Definition of Derived class and in-line print function
class Derived : public Base
{
    public:
        void print () const {cout << "In the Derived" << endl;}
};

int main ()
{
    // Creation of a pointer to the Base class (simulating socket)
    Base* ptr;
    // Let ptr point to an object of the Base class
    ptr = new Base ();
    ptr -> print();
    delete ptr;
    // Let ptr point to an object of the Derived class
    ptr = new Derived();
    ptr -> print();
    delete ptr;
    return 0;
}

Run:
In the Base
In the Base
```

在第 27 行，*ptr* 指向 *Base* 类的一个对象，在第 28 行，我们调用 *Base* 类中定义的函数。在第 31 行，我们让同一个指针指向 *Derived* 类的一个对象，在第 32 行，我们试图调用 *Derived* 类中定义的函数，但结果显示调用的是为 *Base* 类定义的函数。程序中完成了多态的前两个条件，但第三个条件（虚函数）未满足。print 函数不是*虚*函数。

这个结果应该是意料之中的，因为变量 *ptr* 被定义为指向 *Base* 的指针。它可以接受指向 *Derived* 类型对象的指针，因为派生对象是 *Base* 对象（继承定义了一种 *is-a* 关系）。然而，当它想调用 print 函数时，它仍然是指向 *Base* 的指针，因此它调用 *Base* 类中定义的 *print* 函数。我们没有改变指针的类型；我们只是强制它指向 *Derived* 类。

**示例 12.2**

我们重复上一个示例，但将 print 函数设为*虚*函数。结果是每次调用时都会激活正确的函数，如程序 12.2 所示。在第 13 行和第 19 行，我们为 *print* 函数添加了修饰符 *virtual*。第 28 行调用 *Base* 类合适的 *print* 函数，第 32 行调用 *Derived* 类合适的 *print* 函数。

**程序 12.2** 一个使用全部三个条件的有效多态程序

```cpp
/***********************************************************************
 * A simple program to show that if all three necessary               *
 * conditions are fulfilled, we have polymorphism.                    *
 ***********************************************************************/

#include <iostream>
#include <string>
using namespace std;

// Definition of Base class and in-line definition for print function
class Base
{
public:
    virtual void print () const {cout << "In the Base" << endl;}
};

// Definition of Derived class and in-line definition for print function
class Derived : public Base
{
public:
    virtual void print () const {cout << "In the Derived" << endl;}
};

int main ( )
{
    // Creation of a pointer to the Base class (simulating socket)
    Base* ptr;
```
