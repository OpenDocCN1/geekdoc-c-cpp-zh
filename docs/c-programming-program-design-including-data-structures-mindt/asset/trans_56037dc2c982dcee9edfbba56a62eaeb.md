
假设构造函数的定义如下：

```cpp
rectangleType::rectangleType(double l, double w)
{
    setDimension(l, w);
}
```

现在假设类 boxType 的定义如下：

```cpp
class boxType: public rectangleType
{
public:
    void setDimension(double l, double w, double h);
    double getHeight() const;
    double area() const;
    double volume() const;
    void print() const;
    boxType(double l = 0, double w = 0, double h = 0);
    //Constructor with default parameters

private:
    double height;
};
```

可以如下编写类 boxType 的构造函数的定义：

```cpp
boxType::boxType(double l, double w, double h)
    : rectangleType(l, w)
{
    if (h >= 0)
        height = h;
    else
        height = 0;
}
```

注意，这个定义也处理了类 boxType 的默认构造函数。

> **注意**
>
> 假设基类 baseClass 具有私有成员变量和构造函数。进一步假设类 derivedClass 派生自 baseClass，并且 derivedClass 没有成员变量。因此，derivedClass 的成员变量是从 baseClass 继承而来的那些成员变量。构造函数不能像其他函数那样被调用，并且 derivedClass 的成员函数不能直接访问 baseClass 的成员变量。为了保证 derivedClass 类型对象的继承成员变量被初始化，即使 derivedClass 没有成员变量，它也必须具有适当的构造函数。derivedClass 的（带参数的）构造函数仅仅发出对 baseClass 的（带参数的）构造函数的调用。因此，当你编写 derivedClass 的（带参数的）构造函数的定义时，构造函数定义的首部包含对 baseClass 的适当（带参数的）构造函数的调用，而构造函数体为空——也就是说，它只包含左花括号和右花括号。

### 示例 11-3

假设你想定义一个类来归组员工的属性。员工既有全职的，也有兼职的。兼职员工根据工作小时数和小时薪资率获得报酬。假设你想定义一个类来跟踪兼职员工的信息，例如**姓名**、**薪资率**和**工作时长**。然后你可以打印员工姓名及其工资。因为每个员工都是一个人，并且示例 10-10（第 10 章）定义了 `class personType` 来存储名字和姓氏以及对 `name` 的必要操作，所以我们可以基于 `class personType` 定义 `class partTimeEmployee`。你还可以重新定义 `print` 函数以打印适当的信息。

```cpp
class partTimeEmployee: public personType
{
public:
    void print() const;
        //Function to output the first name, last name, and
        //the wages.
        //Postcondition: Outputs
        //               firstName lastName wages are $$$$.$$

    double calculatePay() const;
        //Function to calculate and return the wages.
        //Postcondition: Pay is calculated and returned.

    void setNameRateHours(string first, string last,
                          double rate, double hours);
        //Function to set the first name, last name, payRate,
        //and hoursWorked according to the parameters.
        //Postcondition: firstName = first; lastName = last;
        //               payRate = rate; hoursWorked = hours;

    partTimeEmployee(string first = "", string last = "",
                     double rate = 0, double hours = 0);
        //Constructor with parameters
        //Sets the first name, last name, payRate, and hoursWorked
        //according to the parameters. If no value is specified,
        //the default values are assumed.
        //Postcondition: firstName = first; lastName = last;
        //               payRate = rate; hoursWorked = hours;

private:
    double payRate;      //variable to store the pay rate
    double hoursWorked;  //variable to store the hours worked
};
```

图 11-5 展示了 `class partTimeEmployee` 的 UML 类图和继承层次结构。

![](img/b217c421655b51e7494cf3b89bb5432d_811_0.png)

图 11-5 类 partTimeEmployee 的 UML 类图和继承层次结构

类 partTimeEmployee 的成员函数定义如下：

```cpp
void partTimeEmployee::print() const
{
    personType::print();  //print the name of the employee
    cout << "'s wages are: $" << calculatePay() << endl;
}

double partTimeEmployee::calculatePay() const
{
    return (payRate * hoursWorked);
}

void partTimeEmployee::setNameRateHours(string first,
    string last, double rate, double hours)
{
    personType::setName(first, last);
    payRate = rate;
    hoursWorked = hours;
}

//Constructor
partTimeEmployee::partTimeEmployee(string first, string last,
    double rate, double hours)
    : personType(first, last)
{
    if (rate >= 0)
        payRate = rate;
    else
        payRate = 0;

    if (hours >= 0)
        hoursWorked = hours;
    else
        hoursWorked = 0;
}
```

## 派生类中的析构函数

回顾第 10 章，类可以有析构函数。正如我们将在下一章看到的，析构函数通常用于释放分配给类对象的动态内存。（在执行期间分配的内存空间称为动态内存空间。下一章解释如何创建和使用动态内存。）假设一个基类及其派生类都有析构函数。当派生类对象离开作用域时，它会自动调用其析构函数。当派生类的析构函数执行时，它会自动调用基类的析构函数。因此，在编写派生类的析构函数的定义时，不需要显式调用基类的析构函数。此外，当派生类的析构函数执行时，它先执行自己的代码，然后调用基类的析构函数。例如，假设类 three 派生自类 two，类 two 派生自类 one，并且这些类都有析构函数。当类 three 的对象离开作用域时，首先执行类 three 的析构函数，然后执行类 two 的析构函数，最后执行类 one 的析构函数。也就是说，析构函数按相反顺序执行。

## 派生类的头文件

上一节解释了如何从先前定义的类派生新类。要定义新类，需要创建新的头文件。基类已经定义，头文件包含它们的定义。因此，要基于先前定义的类创建新类，新类的头文件包含告诉计算机在哪里查找基类定义的命令。回顾一下，要在用户程序中包含系统提供的头文件（例如 `iostream`），需将头文件括在尖括号中；要在程序中包含用户定义的头文件，需将头文件括在双引号中。

假设类 `personType` 的定义放在头文件 `personType.h` 中。要创建类 `partTimeEmployee` 的定义，头文件——比如 `partTimeEmployee.h`——必须包含以下预处理指令：

```cpp
#include "personType.h"
```

位于类 `partTimeEmployee` 的定义之前。具体来说，头文件 `partTimeEmployee.h` 如下所示。

```cpp
//Header file partTimeEmployee

#include "personType.h"

class partTimeEmployee: public personType
{
public:
    void print() const;
    //Function to output the first name, last name, and
    //the wages.
    //Postcondition: Outputs
    //              firstName lastName wages are $$$$.$$
