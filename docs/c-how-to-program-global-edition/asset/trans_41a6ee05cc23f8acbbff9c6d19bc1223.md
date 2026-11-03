

![](img/bf54db922e6fa8319cba11069e785521_827_0.png)

## 虚函数调用 baseClassPtr->print() 的流程

当 baseClassPtr 指向 commissionEmployee 对象时

## 图20.18 | 虚函数调用如何工作

## CommissionEmployee 类的 vtable

CommissionEmployee 类的 vtable 中的 earnings 函数指针指向 CommissionEmployee 的 earnings 函数，该函数返回员工的销售额乘以佣金率。print 函数指针指向 CommissionEmployee 版本的函数，该函数打印员工类型、姓名、社会保险号、佣金率和总销售额。与 HourlyEmployee 类一样，这两个函数都覆盖了 Employee 类中的函数。

### BasePlusCommissionEmployee 类的 *vtable*

BasePlusCommissionEmployee 类的 *vtable* 中的 earnings 函数指针指向 BasePlusCommissionEmployee 的 earnings 函数，该函数返回员工的基本工资加上销售额乘以佣金率。print 函数指针指向 BasePlusCommissionEmployee 版本的函数，该函数打印员工的基本工资以及类型、姓名、社会保险号、佣金率和总销售额。两个函数都覆盖了 CommissionEmployee 类中的函数。

### 继承具体的 *虚* 函数

在我们的 Employee 案例研究中，每个具体类都提供了自己的虚函数 earnings 和 print 实现。你已经了解到，每个直接继承抽象基类 Employee 的类都必须实现 earnings 才能成为具体类，因为 earnings 是一个纯虚函数。然而，这些类不需要为了实现 print 函数而被视为具体类——print 不是纯虚函数，派生类可以继承 Employee 类对 print 的实现。此外，BasePlusCommissionEmployee 类不必实现 print 或 earnings 函数——这两个函数实现都可以从具体类 CommissionEmployee 继承。如果我们的层次结构中的某个类以这种方式继承函数实现，那么这些函数的 vtable 指针将简单地指向被继承的函数实现。例如，如果 BasePlusCommissionEmployee 没有覆盖 earnings，那么 BasePlusCommissionEmployee 类的 vtable 中的 earnings 函数指针将指向与 CommissionEmployee 类的 vtable 所指向的相同的 earnings 函数。

### 实现多态性的三级指针

多态性是通过一个优雅的数据结构实现的，该结构涉及*三级指针*。我们已经讨论了一级——*vtable* 中的函数指针。这些指针指向执行*虚*函数调用时实际执行的函数。

现在我们来考虑第二级指针。每当实例化一个具有一个或多个*虚*函数的类的对象时，编译器会向该对象附加一个指向该类的*vtable*的指针。这个指针通常位于对象的前面，但并不是必须这样实现。在图20.18中，这些指针与在图20.17中创建的对象相关联（SalariedEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 类型各一个对象）。该图显示了每个对象的数据成员值。例如，salariedEmployee 对象包含一个指向 SalariedEmployee vtable 的指针；该对象还包含 John Smith、111-11-1111 和 $800.00 这些值。

第三级指针仅仅包含接收*虚*函数调用的对象的句柄。这一级的句柄也可以是*引用*。图20.18描绘了包含 Employee 指针的 *vector* employees。

现在让我们看看典型的*虚*函数调用是如何执行的。考虑函数 virtualViaPointer 中的调用 baseClassPtr->print()（图20.17中的第69行）。假设 baseClassPtr 包含 employees[1]（即 employees 中 commissionEmployee 对象的地址）。当编译器编译这条语句时，它确定该调用确实是通过*基类指针*进行的，并且 print 是一个*虚*函数。

编译器确定 print 是每个 *vtable* 中的第二个条目。为了定位这个条目，编译器注意到它需要跳过第一个条目。因此，编译器编译一个偏移量或位移量到机器语言对象代码指针表中，以找到执行虚函数调用的代码。偏移量的字节大小取决于特定平台上表示函数指针所用的字节数。例如，在32位平台上，指针通常存储为4字节，而在64位平台上，指针通常存储为8字节。这里我们假设4字节。

编译器生成执行以下操作的代码 [注意：列表中的数字对应于图20.18中带圆圈的数字]：

1. 选择 employees 的第4个条目（本例中为 commissionEmployee 对象的地址），并将其作为参数传递给函数 virtualViaPointer。这将参数 baseClassPtr 设置为指向 commissionEmployee。
2. 解引用该指针以到达 commissionEmployee 对象——正如你回忆的，该对象以一个指向 commissionEmployee vtable 的指针开头。
3. 解引用 commissionEmployee 的 vtable 指针以到达 CommissionEmployee vtable。
4. 跳过四个字节的偏移量以选择 print 函数指针。
5. 解引用 print 函数指针以形成要执行的实际函数的“名称”，并使用函数调用运算符 () 执行适当的 print 函数，在本例中该函数打印员工类型、姓名、社会保险号、总销售额和佣金率。

图20.18的数据结构可能看起来复杂，但这种复杂性由编译器管理，对你隐藏，使多态编程变得简单。每次虚函数调用时发生的指针解引用操作和内存访问需要一些额外的执行时间。添加到对象上的 vtable 和 vtable 指针需要一些额外的内存。

> > **性能提示 20.1**
> >
> > 多态性（通常通过 C++ 中的虚函数和动态绑定实现）是高效的。您可以使用这些功能，而对性能的影响很小。

> > **性能提示 20.2**
> >
> > 虚函数和动态绑定实现了多态编程，作为 switch 逻辑编程的替代方案。优化编译器通常会生成与手工编写的基于 switch 的逻辑几乎一样高效的多态代码。多态性的开销对于大多数应用来说是可以接受的。在某些情况下——例如对性能要求严格的实时应用——多态性的开销可能过高。

## 20.8 案例研究：使用多态和运行时类型信息的工资系统，结合向下转换、dynamic_cast、typeid 和 type_info

回顾 20.6 节开头的问题陈述，在当前工资周期中，我们虚构的公司决定通过将 BasePlusCommissionEmployee 的基本工资增加10%来奖励他们。在 20.6.5 节中多态地处理 Employee 对象时，我们不需要担心“具体情况”。但现在，为了调整 BasePlusCommissionEmployee 的基本工资，我们必须在执行时确定每个 Employee 对象的具体类型，然后采取相应的行动。本节演示了运行时类型信息（RTTI）和动态转换的强大功能，它们使程序能够在执行时确定对象的类型并相应地对该对象进行操作。^1

图20.19 使用了 20.6 节开发的 Employee 层次结构，并将每个 BasePlusCommissionEmployee 的基本工资增加了10%。第21行声明了包含三个元素的 vector employees，它存储指向 Employee 对象的指针。第24-29行用 SalariedEmployee（图20.11-20.12）、CommissionEmployee（图20.13-20.14）和 BasePlusCommissionEmployee（图20.15-20.16）类的动态分配对象的地址填充 vector。第32-52行遍历 employees vector，并通过调用成员函数 print（第34行）显示每个 Employee 的信息。回想一下，由于 print 在基类 Employee 中声明为虚函数，系统会调用适当的派生类对象的 print 函数。

```cpp
1 // Fig. 20.19: fig20_19.cpp
2 // Demonstrating downcasting and runtime type information.
3 // NOTE: You may need to enable RTTI on your compiler
4 // before you can compile this application.
5 #include <iostream>
6 #include <iomanip>
7 #include <vector>
8 #include <typeinfo>
9 #include "Employee.h"
10 #include "SalariedEmployee.h"
11 #include "CommissionEmployee.h"
12 #include "BasePlusCommissionEmployee.h"
13 using namespace std;
14
15 int main()
16 {
17   // set floating-point output formatting
18   cout << fixed << setprecision( 2 );
19
20   // create vector of three base-class pointers
21   vector < Employee * > employees( 3 );
22
23   // initialize vector with various kinds of Employees
24   employees[ 0 ] = new SalariedEmployee(
25      "John", "Smith", "111-11-1111", 800 );
26   employees[ 1 ] = new CommissionEmployee(
27      "Sue", "Jones", "333-33-3333", 10000, .06 );
28   employees[ 2 ] = new BasePlusCommissionEmployee(
29      "Bob", "Lewis", "444-44-4444", 5000, .04, 300 );
30 }
```

图20.19 | 演示向下转换和运行时类型信息。（第1部分，共2部分。）

1. 有些编译器要求在使用 RTTI 之前先启用它。我们用于测试本书 C++ 示例的编译器——GNU C++、Visual C++ 和 Xcode LLVM——都默认启用 RTTI。

