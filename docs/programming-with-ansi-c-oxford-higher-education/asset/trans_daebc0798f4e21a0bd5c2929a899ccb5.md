
学生指针转换为指向计算机科学学生的指针，并看到现在它可以访问计算机科学部分。

5. 使用练习3中给出的同一个类，现在定义一个虚函数 Display()，使用同一个基类指针（指向学生的指针）在各个类中显示所有类的详细信息。现在，使用该虚函数访问计算机科学对象。可以看出，无需任何指针类型转换，基类指针就可以通过虚函数访问派生类对象。

6. 在练习3的类中，提供一个虚函数 Registration()，为相应的学生注册考试。最后，显示有多少学生注册了哪场考试。

7. 在练习2的类中，提供一个虚函数 Push()，将对象压入相应的堆栈。

8. 在练习1中，提供一个虚函数 Display()，显示给定表示形式的时间。

9. 定义一个 Faculty 类。它包含以下属性：
(a) 教师的姓名
(b) 教师的资历
(c) 教师能够教授的科目

10. 将练习9中的 Faculty 类继承为正式教师，其特点是：
(a) 全职工作（不指定咨询时间）
(b) 至少教授三门科目
(c) 仅属于该学院

11. 将练习9中的 Faculty 类继承为客座教师，其特点是：
(a) 仅在两到三天内有空（还需指定咨询时间）
(b) 只教授一门科目
(c) 隶属于其他机构

12. 为练习10和11中给出的类的对象读写提供虚函数。

13. 定义一个 Vehicle 类。将该类继承为两轮车和四轮车。将两轮车继承为自行车和摩托车，将四轮车继承为柴油车和汽油车。提供一个虚函数来计算车辆的里程（行驶距离（公里）/ 燃料消耗量）。

14. 对于练习1，为所有类提供虚析构函数。

15. 定义一个 Employee 类。同时定义继承自 Employee 类的 MaleEmp 和 FemaleEmp 类。再定义继承自 Employee 类的 Officers、Clerks 和 Peons 类。定义一个包含10种不同类型员工的数组。在所有类中定义一个 ReadDetails() 函数。无论类型如何，所有数组元素都应在同一个例程中可访问。

# 第11章

# 运行时类型信息与类型转换运算符

## 学习目标

- 运行时类型信息简介
- typeinfo 对象与 typeid 运算符
- 多态对象
- 动态类型转换简介
- 使用 const_cast、static_cast 和 reinterpret_cast 进行类型转换
- 在模板中使用 typeid 和 dynamic_cast
- 交叉转换和向下转换

## 11.1 引言

运行时类型信息（RTTI）是 C++ 中一个非常强大的工具，用于在运行时查找对象的类型。由于是在运行时运行，RTTI 也会对系统性能产生显著影响。因此，大多数编译器都提供 RTTI，但默认情况下将其禁用。如果要使用 RTTI，需要启用该选项（同时也要接受性能下降）。虽然性能是一个重要问题，但对于某些应用来说并不是最重要的。在这种情况下，RTTI 所提供的灵活性和强大功能胜过了性能问题。

ANSI C++ 标准化委员会新增了两个用于 RTTI 的关键字，即 typeid 和 dynamic_cast。typeid 是一个运算符，它以特定形式（typeinfo 对象）返回对象的类型。dynamic_cast 是一种新类型的运算符，它使我们能够以安全的方式对多态对象进行类型转换。只有在转换有效的情况下，它才会将源类型转换为目标类型。类似的运算符还有 const_cast、reinterpret_cast 和 static_cast。这些运算符将在本章讨论。这里还引入了一个内置类 typeinfo。typeinfo 对象保存传递给 typeid 运算符的参数类型信息。

> typeid 和 dynamic_cast 是用于 RTTI 的新运算符。

> 大多数编译器提供 RTTI，但由于性能问题默认将其禁用。

> 多态对象可以使用虚函数进行操作。

> 请注意，dynamic_cast、const_cast、reinterpret_cast 和 static_cast 是 C++ 中定义的新运算符，与 C 中提供的普通类型转换相比，它们提供了更好的转换功能。

## 11.1.1 多态对象

使用虚函数，可以借助基类指针指向任何派生类对象。这种可以使用虚函数进行操作的对象称为多态对象。一个带有虚函数的对象以及从该对象派生的所有对象，或层次结构中的任何后续对象，都称为多态对象。它们可以被基类指针指向，并在运行时进行操作。

考虑一个 Employee 类，ProductionEmployee、SalesEmployee 和 OtherEmployee 都继承自它。另外，考虑 Employee 类的函数 ListLeaves()，它显示员工迄今已使用的休假天数。因此，结构如下：

```
class Employee
{
    ...
public:
    virtual void ListLeaves()
    {...}
}
```

```
class ProductionEmployee : public Employee
{
    void ListLeaves()
    {...}
}
```

```
class SalesEmployee : public Employee
{
    void ListLeaves()
    {...}
}
```

```
class OtherEmployee : public Employee
{
    void ListLeaves()
    {...}
}
```

```
main()
{
    Employee *ptrEmp;
    switch(int EmpType)
    {
        ...
        case 1: // Production employee
        ptrEmp = new ProductionEmployee; // Polymorphic object
        ...
    }
    ...
    ptrEmp->ListLeaves()
    ...
}
```

> 如果对象在运行时可以改变其形态，即当指针在运行时改变指向的对象，并且指针表达式根据指针指向的位置产生不同的对象，则这样的对象称为多态对象。

本例中创建的对象是一个多态对象，因为它在运行时可以采用任何派生员工类型的形式。

## 11.1.2 RTTI 的必要性

> RTTI 会在运行时降低处理速度，因此只在需要时使用。编译器默认将其关闭。使用虚函数的替代方案通常更好。

RTTI 是一个强大的工具，如果使用虚函数可以解决问题，则应避免使用 RTTI。然而，有时使用 RTTI 是必要的。让我们考虑程序11.1中所示的一个简单示例，以更好地理解这一点。

假设一个应用程序有在线传入的新闻。新闻可以是不同类型。为简单起见，我们只考虑两种类型，即纯文本新闻和带图片的新闻。该应用程序要求只在屏幕上显示所有新闻的标题。用户可以点击任意新闻进行查看。也可以右键点击新闻以启用一些附加操作。右键选项可能包括以下内容：

- 1. 将此新闻作为电子邮件发送。
- 2. 将此新闻复制到特定文件夹。
- 3. 使用打印机打印此新闻。

假设用户不希望带图片的新闻被打印，因为它们会消耗大量打印机墨粉。为了解决这个问题，可以定义一个 News 类作为基类。PlainTextNews 和 NewsWithImages 是派生自它的两个类。News 类将是一个抽象类，因为所有可用的新闻要么是纯文本，要么带图片。为简单起见，不考虑其他新闻类型。

在 News 类中定义了三个函数：SendNews()、StoreNews() 和 PrintNews()。这种设计会使 NewsWithImages 继承这三个函数。然而，我们不希望 NewsWithImages 继承 PrintNews()，因此应将其从 News 类中移除。那还能放在哪里呢？下一个显而易见的选择是 PlainTextNews 类。

SendNews() 和 StoreNews() 函数对两种类型的新闻都是必需的，因此需要在 News 类中定义为虚函数。如程序11.1所示：

```
PROGRAM 11.1 A solution using virtual functions

//NewsHierarchy.cpp
#include <iostream>
#include <typeinfo>
#include <string>
using namespace std;

#define SENDNEWS 1
#define STORENEWS 2
#define PRINTNEWS 3

// Base class
class News
{
public:
	virtual void SendNews(string Address){};
	virtual void StoreNews(){};
	virtual ~News() = 0;
};

News::~News()
{
	// Empty body
}
```
