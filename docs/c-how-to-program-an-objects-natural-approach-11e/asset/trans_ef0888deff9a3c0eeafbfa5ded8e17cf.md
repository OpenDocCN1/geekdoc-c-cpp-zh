
## SalariedCommissionEmployee 成员函数 earnings

SalariedCommissionEmployee 的 earnings 函数（第 49–52 行）重定义了类 SalariedEmployee（图 10.2 第 34 行）的 earnings，以计算 SalariedCommissionEmployee 的收益。SalariedCommissionEmployee 版本中的第 50 行使用表达式 `SalariedEmployee::earnings()` 获取基于工资的那部分收益，然后将该值加到佣金上以计算总收益。

要从派生类调用重定义的基类成员函数，请将基类名称和作用域解析运算符（`::`）放在基类成员函数名之前。此处需要 `SalariedEmployee::` 以避免无限递归。此外，我们通过从 SalariedCommissionEmployee 的 earnings 函数调用 SalariedEmployee 的 earnings 函数来避免重复代码。

## SalariedCommissionEmployee 成员函数 toString

类似地，SalariedCommissionEmployee 的 toString 函数（图 10.5 第 55–59 行）重定义了 SalariedEmployee 的 toString 函数（图 10.2 第 37–40 行）。新版本返回一个字符串，其中包含

- 调用 `SalariedEmployee::toString()` 的结果（图 10.5 第 58 行）
- SalariedCommissionEmployee 的总销售额和佣金率。

## 测试类 SalariedCommissionEmployee

图 10.6 创建了 SalariedCommissionEmployee 对象 employee（第 9 行）。第 12–16 行通过调用其 get 函数获取对象的数据成员值来输出 employee 的数据。第 18–19 行分别使用 setGrossSales 和 setCommissionRate 更改 employee 的 m_grossSales 和 m_commissionRate 值。然后，第 20–21 行调用 employee 的 toString 成员函数以显示 employee 的更新信息。最后，第 24 行显示 employee 更新后的收益。

```cpp
// Fig10_06.cpp
// SalariedCommissionEmployee class test program.
#include <format>
#include <iostream>
#include "SalariedCommissionEmployee.h"

int main() {
   // instantiate SalariedCommissionEmployee object
   SalariedCommissionEmployee employee{"Ivano Lal", 300.0, 5000.0, .04};

   // get SalariedCommissionEmployee object data
   std::cout << "Employee information obtained by get functions:\n"
             << std::format("{:}: {:}\n{:}: {:}\n{:}: {:}\n{:}: {:}\n",
                            "name", employee.getName(), "salary", employee.getSalary(),
                            "gross sales", employee.getGrossSales(),
                            "commission", employee.getCommissionRate());
```

**图 10.6** | SalariedCommissionEmployee 类测试程序。（第 1 部分，共 2 部分。）

- 6. 避免代码重复是优点。缺点是这会在基类和派生类之间产生耦合，从而使大规模系统难以修改。

```cpp
   employee.setGrossSales(8000.0); // change gross sales
   employee.setCommissionRate(0.1); // change commission rate
   std::cout << "\nUpdated employee information from function toString:\n"
             << employee.toString();

   // display the employee's earnings
   std::cout << std::format("earnings: ${:.2f}\n", employee.earnings());
}
```

```text
Employee information obtained by get functions:
name: Ivano Lal
salary: $300.00
gross sales: $5000.00
commission: 0.04

Updated employee information from function toString:
name: Ivano Lal
salary: $300.00
gross sales: $8000.00
commission rate: 0.10

earnings: $1100.00
```

**图 10.6** | SalariedCommissionEmployee 类测试程序。（第 2 部分，共 2 部分。）

### 派生类构造函数必须调用其基类的构造函数

如果 SalariedCommissionEmployee 的构造函数没有显式调用 SalariedEmployee 的构造函数，编译器将报错。在这种情况下，编译器会尝试调用 SalariedEmployee 的默认构造函数，但该构造函数不存在，因为基类显式定义了构造函数。如果基类提供默认构造函数，则派生类构造函数可以隐式调用基类构造函数。

### 关于派生类中构造函数的说明

派生类构造函数必须使用任何必需的参数调用其基类的构造函数；否则会发生编译错误。这确保继承的私有基类成员（派生类无法直接访问）得到初始化。派生类的数据成员初始化器通常放在成员初始化列表中的基类初始化器之后。

### 基类的 private 成员在派生类中不可直接访问

C++ 严格执行对访问 private 数据成员的限制。即使是与其基类关系密切的派生类，也不能直接访问其基类的 private 数据。例如，类 SalariedEmployee 的 private 数据成员 m_salary 虽然是每个 SalariedCommissionEmployee 对象的一部分，但不能由类 SalariedCommissionEmployee 的成员函数直接访问。如果它们尝试这样做，编译器会产生错误消息，例如 GNU g++ 的以下消息：

> 'double SalariedEmployee::m_salary' 在此上下文中是 private

然而，正如你在图 10.5 中看到的，SalariedCommissionEmployee 的成员函数可以访问从 SalariedEmployee 继承的公有成员。

## 在派生类头文件中包含基类头文件

注意，我们在派生类的头文件中 #include 基类的头文件（图 10.4 第 6 行）。这有几个必要原因：

- 为了使派生类在第 8 行（图 10.4）从基类继承，编译器需要来自 `SalariedEmployee.h` 的基类定义。
- **编译器根据类的定义确定对象的大小**，因此它必须知道类定义，以便为新对象保留适当数量的内存。**派生类对象的大小取决于其类定义中显式声明的数据成员以及从直接和间接基类继承的数据成员。**⁷ 包含基类的定义使编译器能够确定为构成派生类对象总大小的所有数据成员的完整内存需求。
- 基类定义还使编译器能够确定派生类是否正确使用基类继承的成员。例如，**编译器使用基类的函数原型来验证派生类对继承的基类函数的函数调用。**

## 通过实现继承消除重复代码

使用实现继承时，基类声明层次结构中所有类的共同数据成员和成员函数。当这些共同特征需要更改时，只需在基类中进行更改。派生类随后继承这些更改，并且必须重新编译。如果没有继承，则需要对所有包含相关代码副本的源代码文件进行更改。⁸

![](img/7b5e2088e71c7f78681d4ddbcf104c06_601_0.png)

## 检查点

- 1. *（填空）* 派生类构造函数可以通过一个 ______——即向基类构造函数传递参数的成员初始化器——来调用其基类的构造函数。**答案：** 基类初始化器。
- 2. *（代码）* 假设类 `SalariedEmployee` 有一个不接受参数的 `print` 成员函数。同时，假设类 `SalariedCommissionEmployee` 继承自 `SalariedEmployee` 并重定义 `print`。编写一个表达式，从 `SalariedCommissionEmployee` 的 `print` 函数中调用 `SalariedEmployee` 的 `print` 函数。**答案：** `SalariedEmployee::print()`
- 3. *（判断正误）* C++ 严格执行对访问私有数据成员的限制。即使是与其基类关系密切的派生类，也不能直接访问其基类的私有数据。**答案：** 正确。

- 7. 一个类的所有对象共享该类成员函数的一份副本，这些函数与对象分开存储，并且不属于对象大小的一部分。
- 8. 同样，实现继承的缺点（尤其是在深层继承层次结构中）是它在层次结构的类之间造成紧密耦合，使其难以修改。

