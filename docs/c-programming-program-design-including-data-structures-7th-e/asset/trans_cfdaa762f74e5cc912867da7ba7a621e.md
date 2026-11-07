
`class fullTimeEmployee` 的定义如下：

```cpp
#include "employeeType.h"

class fullTimeEmployee: public employeeType
{
public:
    void set(string first, string last, long id,
             double salary, double bonus);
        //Function to set the first name, last name,
        //id, and salary according to the parameters.
        //Postcondition: firstName = first; lastName = last;
        //               personId = id; empSalary = salary;
        //               empBonus = bonus;

    void setSalary(double salary);
        //Function to set the salary.
        //Postcondition: empSalary = salary;

    double getSalary();
        //Function to retrieve the salary.
        //Postcondition: returns empSalary

    void setBonus(double bonus);
        //Function to set the bonus.
        //Postcondition: empBonus = bonus;

    double getBonus();
        //Function to retrieve the bonus.
        //Postcondition: returns empBonus;

    void print() const;
        //Function to output the first name, last name,
        //and the wages.
        //Postcondition: Outputs
        //              Id:
        //              Name: firstName lastName
        //              Wages: $$$$.$$

    double calculatePay() const;
        //Function to calculate and return the wages.
        //Postcondition: Pay is calculated and returned

    fullTimeEmployee(string first = "", string last = "",
                     long id = 0, double salary = 0,
                     double bonus = 0);
        //Constructor with default parameters.
        //Sets the first name, last name, id, salary, and
        //bonus according to the parameters. If
        //no value is specified the default values are
        //assumed.
        //Postcondition: firstName = first; lastName = last;
        //               personId = id; empSalary = salary;
        //               empBonus = bonus;

private:
    double empSalary;
    double empBonus;
};
```

类 `fullTimeEmployee` 的构造函数和函数的定义如下：

```cpp
void fullTimeEmployee::set(string first, string last,
                           long id,
                           double salary, double bonus)
{
    setName(first, last);
    setId(id);
    empSalary = salary;
    empBonus = bonus;
}

void fullTimeEmployee::setSalary(double salary)
{
    empSalary = salary;
}

double fullTimeEmployee::getSalary()
{
    return empSalary;
}

void fullTimeEmployee::setBonus(double bonus)
{
    empBonus = bonus;
}

double fullTimeEmployee::getBonus()
{
    return empBonus;
}

void fullTimeEmployee::print() const
{
    cout << "Id: " << getId() << endl;
    cout << "Name: ";
    personType::print();
    cout << endl;
    cout << "Wages: $" << calculatePay() << endl;
}

double fullTimeEmployee::calculatePay() const
{
    return empSalary + empBonus;
}

fullTimeEmployee::fullTimeEmployee(string first, string last,
                                   long id, double salary,
                                   double bonus)
                                 : employeeType(first, last, id)
{
    empSalary = salary;
    empBonus = bonus;
}
```

类 partTimeEmployee 的定义如下：

```cpp
#include "employeeType.h"

class partTimeEmployee: public employeeType
{
public:
    void set(string first, string last, long id, double rate,
             double hours);
        //Function to set the first name, last name, id,
        //payRate, and hoursWorked according to the
        //parameters.
        //Postcondition: firstName = first; lastName = last;
        //                personId = id;
        //                payRate = rate; hoursWorked = hours

    double calculatePay() const;
        //Function to calculate and return the wages.
        //Postcondition: Pay is calculated and returned.

    void setPayRate(double rate);
        //Function to set the salary.
        //Postcondition: payRate = rate;

    double getPayRate();
        //Function to retrieve the salary.
        //Postcondition: returns payRate;

    void setHoursWorked(double hours);
        //Function to set the bonus.
        //Postcondition: hoursWorked = hours

    double getHoursWorked();
        //Function to retrieve the bonus.
        //Postcondition: returns empBonus;

    void print() const;
        //Function to output the id, first name, last name,
        //and the wages.
        //Postcondition: Outputs
        //              Id:
        //              Name: firstName lastName
        //              Wages: $$$$.$$

    partTimeEmployee(string first = "", string last = "",
                     long id = 0,
                     double rate = 0, double hours = 0);
        //Constructor with parameters
        //Sets the first name, last name, payRate, and
        //hoursWorked according to the parameters. If
        //no value is specified, the default values are
        //assumed.
        //Postcondition: firstName = first; lastName = last;
        //               personId = id, payRate = rate;
        //               hoursWorked = hours;

private:
    double payRate;     //stores the pay rate
    double hoursWorked; //stores the hours worked
};
```

类 partTimeEmployee 的构造函数和函数的定义如下：

```cpp
void partTimeEmployee::set(string first, string last, long id,
                          double rate, double hours)
{
    setName(first, last);
    setId(id);
    payRate = rate;
    hoursWorked = hours;
}

void partTimeEmployee::setPayRate(double rate)
{
    payRate = rate;
}

double partTimeEmployee::getPayRate()
{
    return payRate;
}

void partTimeEmployee::setHoursWorked(double hours)
{
    hoursWorked = hours;
}

double partTimeEmployee::getHoursWorked()
{
    return hoursWorked;
}

void partTimeEmployee::print() const
{
    cout << "Id: " << getId() << endl;
    cout << "Name: ";
    personType::print();
    cout << endl;
    cout << "Wages: $" << calculatePay() << endl;
}

double partTimeEmployee::calculatePay() const
{
    return (payRate * hoursWorked);
}

//constructor
partTimeEmployee::partTimeEmployee(string first, string last,
                                   long id,
                                   double rate, double hours)
                                   : employeeType(first, last, id)
{
    payRate = rate;
    hoursWorked = hours;
}
```

以下函数 main 测试这些类：

```cpp
#include <iostream>
#include "partTimeEmployee.h"
#include "fullTimeEmployee.h"

int main()
{
    fullTimeEmployee newEmp("John", "Smith", 75, 56000, 5700);
    partTimeEmployee tempEmp("Bill", "Nielson", 275, 15.50, 57);

    newEmp.print();
    cout << endl;
    tempEmp.print();

    return 0;
}
```

## 示例运行：

```text
Id: 75
Name: John Smith
Wages: $61700

Id: 275
Name: Bill Nielson
Wages: $883.5
```

前面的输出不言自明。我们将细节留作练习。

![](img/d0be7fc6d804b63484835c6c8bc67a07_917_0.png)

## 基于数组的列表

本章前面的一节讨论了如何使用指针创建动态数组。第8章简要说明了如何使用循环处理存储在数组中的元素。此外，本章前面几节讨论了抽象类。利用这些特性，本节讨论如何使用数组来操作列表。让我们首先给出以下定义。

**列表：** 一组相同类型的元素。

列表的**长度**是列表中元素的数量。对列表执行的一些操作如下：

- 1. 创建列表。列表被初始化为空状态。
- 2. 判断列表是否为空。
- 3. 判断列表是否已满。
- 4. 求列表的大小。
- 5. 销毁或清空列表。
- 6. 判断某项是否与给定的列表元素相同。
- 7. 在列表的指定位置插入一项。
- 8. 从列表的指定位置删除一项。
- 9. 用另一项替换指定位置的项。
- 10. 从列表的指定位置检索一项。
- 11. 在列表中搜索给定项。

我们创建的列表可以是有序的或无序的。然而，无论列表是有序还是无序，实现某些操作的算法是相同的。例如，无论列表是有序还是无序，如果列表的长度为空，则列表为空。然而，有序列表和无序列表的搜索算法通常是不同的。因此，接下来我们创建实现其中一些操作的抽象类。我们将分别描述用于创建有序列表和无序列表的类。然而，我们必须首先决定如何将列表存储在计算机内存中。

因为列表的所有元素类型相同，处理列表的一种有效、方便且常见的方法是将其存储在数组中。最初，保存列表元素的数组大小通常大于列表中的元素数量，以便在后续阶段列表可以增长到特定大小。因此，我们必须知道数组有多满，也就是说，我们必须跟踪存储在数组中的列表元素数量。现在，C++ 允许程序员创建动态数组。因此，我们将让用户指定数组的大小。数组的大小可以在声明列表对象时指定。由此可知，为了在数组中维护和处理列表，我们需要以下三个变量：
