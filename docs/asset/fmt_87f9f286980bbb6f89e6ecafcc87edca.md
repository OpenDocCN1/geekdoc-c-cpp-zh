
`socialSecurityNumber = ssn; // 应该验证`

`setGrossSales(sales); // 验证并存储总销售额`

`setCommissionRate(rate); // 验证并存储佣金率`

`setBaseSalary(salary); // 验证并存储基本工资`

}

// 设置名字

`void BasePlusCommissionEmployee::setFirstName(const string& first) {`

`firstName = first; // 应该验证`

}

// 返回名字

`string BasePlusCommissionEmployee::getFirstName() const {`

`return firstName;`

}

// 设置姓

`void BasePlusCommissionEmployee::setLastName(const string& last) {`

`lastName = last; // 应该验证`

}

// 返回姓

`string BasePlusCommissionEmployee::getLastName() const {`

`return lastName;`

}

// 设置社会安全号

`void BasePlusCommissionEmployee::setSocialSecurityNumber(const string& ssn) {`

`socialSecurityNumber = ssn; // 应该验证`

}

// 返回社会安全号

`string BasePlusCommissionEmployee::getSocialSecurityNumber() const {`

`return socialSecurityNumber;`

}

图 11.8 | `BasePlusCommissionEmployee` 类表示一个除了佣金外还领取基本工资的员工。（3/3 部分）

```cpp
50 // 设置总销售额金额
51 void BasePlusCommissionEmployee::setGrossSales(double sales) {
52   if (sales < 0.0) {
53     throw invalid_argument("Gross sales must be >= 0.0");
54   }
55 }
56
57 grossSales = sales;
```

```cpp
59 // 返回总销售额金额
60 double BasePlusCommissionEmployee::getGrossSales() const {
61   return grossSales;
62 }
```

```cpp
63 // 设置佣金率
64 void BasePlusCommissionEmployee::setCommissionRate(double rate) {
65   if (rate < 0.0 || rate > 1.0) {
66     throw invalid_argument("Commission rate must be between 0.0 and 1.0");
67   }
68   commissionRate = rate;
69 }
```

```cpp
70 // 返回佣金率
71 double BasePlusCommissionEmployee::getCommissionRate() const {
72   return commissionRate;
73 }
```

```cpp
74 // 设置基本工资
75 void BasePlusCommissionEmployee::setBaseSalary(double salary) {
76   if (salary < 0.0) {
77     throw invalid_argument("Salary must be >= 0.0");
78   }
79   baseSalary = salary;
80 }
```

```cpp
81 // 返回基本工资
82 double BasePlusCommissionEmployee::getBaseSalary() const {
83   return baseSalary;
84 }
```

```cpp
85 // 计算收入
86 double BasePlusCommissionEmployee::earnings() const {
87   return baseSalary + (commissionRate * grossSales);
88 }
```

```cpp
89 // 返回字符串表示
90 string BasePlusCommissionEmployee::toString() const {
91   ostringstream output;
92   output << "commission employee: " << firstName << " " << lastName << "\n";
93   output << "social security number: " << socialSecurityNumber << "\n";
94   output << "gross sales: " << fixed << setprecision(2) << grossSales << "\n";
95   output << "commission rate: " << setprecision(2) << commissionRate << "\n";
96   output << "base salary: " << setprecision(2) << baseSalary << "\n";
97   return output.str();
98 }
```

# 550 第二章 面向对象编程：继承

```cpp
int main() {
    // 实例化 BasePlusCommissionEmployee 对象
    BasePlusCommissionEmployee employee("Bob", "Lewis", "333-33-3333", 5000, .04, 300);
    // 获取佣金员工数据
    cout << fixed << setprecision(2); // 设置浮点数格式
    cout << "Employee information obtained by get functions: \n";
    cout << "First name is " << employee.getFirstName();
    cout << "\nLast name is " << employee.LastName();
    cout << "\nSocial security number is " << employee.getSecurityNumber();
    cout << "Gross sales is " << employee.getGrossSales();
    cout << "\nCommission rate is " << employee.getCommissionRate();
    cout << "\nBase salary is " << employee.getBaseSalary() << endl;
    employee.setBaseSalary(1000); // 设置基础工资
    cout << "\nUpdated employee information from function toString: \n\n";
    cout << employee.toString();
    // 显示员工薪资
    cout << "\nEmployee's earnings: $" << employee.earnings() << endl;
}
```

通过 get 函数获取的员工信息：
First name is Bob
Last name is Lewis
Social security number is 333-33-3333
Gross sales is 5000.00
Commission rate is 0.04
Base salary is 300.00

通过 toString 函数更新的员工信息：
base salary commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 1000.00

Employee's earnings: $1200.00

图 11.9 | `BasePlusCommissionEmployee`：在类 `BasePlusCommissionEmployee` 与类 `CommissionEmployee` 之间

探索 `BasePlusCommissionEmployee` 类与 `CommissionEmployee` 类之间的相似之处

`BasePlusCommissionEmployee` 的大部分代码（图 11.7–18）与 `CommissionEmployee` 类代码（图 11.4–5）相似，甚至完全相同。例如，在 `BasePlusCommissionEmployee` 类中，私有数据成员 `firstName` 和 `lastName` 以及成员函数 `setFirstName`、`setLastName` 和 `getLastName` 与 `CommissionEmployee` 类完全相同。`CommissionEmployee` 类和 `BasePlusCommissionEmployee` 类还包含私有数据成员 `socialSecurityNumber`、`commissionRate` 和 `grossSales`，以及操作成员的 set 函数。

## 11.3 基类与派生类之间的关系

此外，`BasePlusCommissionEmployee` 的构造函数与 `CommissionEmployee` 类的构造函数几乎相同，由于 `BasePlusCommissionEmployee` 的构造函数还设置了 `baseSalary`。`BasePlusCommissionEmployee` 类的其他添加是私有数据 `baseSalary` 以及成员函数 `setBaseSalary` 和 `getBaseSalary`。`BasePlusCommissionEmployee` 的 `toString` 函数与 `CommissionEmployee` 类的几乎相同，但 `BasePlusCommissionEmployee` 的 `toString` 重写了数据 `baseSalary` 的值。

我们直接从 `CommissionEmployee` 类中复制代码并粘贴到 `BasePlusCommissionEmployee` 类中，然后修改 `BasePlusCommissionEmployee` 类以包含基础工资以及操作基础工资的成员函数。这种复制-粘贴的方法容易出错且耗时。

![](img/09cee61886647f0b1e06dc44c0065a38_551_0.png)

# 软件工程观察 11.1

从一个类复制和粘贴代码会导致同份代码产生多个物理副本，并在整个系统中传播错误，造成代码维护的噩梦。通过避免代码重复（以及可能产生的错误重复），在想要“吸收”另一个类的数据成员和成员函数时，请使用**继承**，而不是“复制-粘贴”的方法。

![](img/09cee61886647f0b1e06dc44c0065a38_551_1.png)

# 软件工程观察 11.2

通过继承，层级结构中所有类的公共数据成员和成员函数都声明在基类中。当这些公共特性需要进行更改时，你只需要在基类中进行更改——派生类会继承这些更改。如果没有继承，则需要对包含相关代码副本的所有源文件进行修改。

## 11.3 创建佣金员工——BasePlusCommissionEmployee 继承层次结构

现在我们创建并测试新的 `BasePlusCommissionEmployee` 类（图 11.10–11.11），它派生自 `CommissionEmployee` 类（图 11.4–11.5）。一个 `BasePlusCommissionEmployee` 对象是一个 `CommissionEmployee`（因为继承传递了 `CommissionEmployee` 类的能力），但 `BasePlusCommissionEmployee` 类还拥有数据成员 `baseSalary`（图 11.10, 21）。类中第 10 行的冒号（:）定义了继承的类型。作为一个派生类（使用公共继承），`BasePlusCommissionEmployee` 继承了 `CommissionEmployee` 的所有的成员，构造函数除外——每个类都包含特定于该类的构造函数。（析构函数也不被继承。）因此，`BasePlusCommissionEmployee` 的公有服务包含了继承自 `CommissionEmployee` 的部分——尽管我们无法在 `BasePlusCommissionEmployee` 的源代码中使用继承的成员函数，但它们仍然是派生类 `BasePlusCommissionEmployee` 的一部分。派生类的公有服务还包括成员函数 `setBaseSalary`、`getBaseSalary` 和 `earnings`（第 15–19 行）。

图 11.11 显示了 `BasePlusCommissionEmployee` 的成员函数实现。构造函数（第 10–16 行）引入了基类语法（第 14 行），将参数传递给基类（`CommissionEmployee`）。

```cpp
// 图 11.10: BasePlusCommissionEmployee.h
// 派自 CommissionEmployee 的 BasePlusCommissionEmployee 类
#include <string>
#include "CommissionEmployee.h"
class BasePlusCommissionEmployee : public CommissionEmployee {
public:
    BasePlusCommissionEmployee(const std::string&, const std::string&,
                               const std::string&, double = 0.0, double = 0.0);
    void setBaseSalary(double salary);
    double getBaseSalary() const;
    double earnings() const;
    std::string toString() const;
private:
    double baseSalary;
};
```

图 11.10 | 显示继承的 `BasePlusCommissionEmployee` 类定义

```cpp
// 图 11.11: BasePlusCommissionEmployee.cpp
// BasePlusCommissionEmployee 成员函数定义
#include <iostream>
#include <sstream>
#include <stdexcept>
#include "BasePlusCommissionEmployee.h"
using namespace std;
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
    const std::string& first, const std::string& last,
    const std::string& ssn, double sales, double rate)
    : CommissionEmployee(first, last, ssn, sales, rate) {
    setBaseSalary(salary);
}
void BasePlusCommissionEmployee::setBaseSalary(double salary) {
    if (salary < 0.0) {
        throw invalid_argument("Salary must be >= 0.0");
    }
    baseSalary = salary;
}
double BasePlusCommissionEmployee::getBaseSalary() const {
    return baseSalary;
}
double BasePlusCommissionEmployee::earnings() const {
    return baseSalary + (commissionRate * grossSales);
}
string BasePlusCommissionEmployee::toString() const {
    ostringstream output;
    output << setprecision(2);
    output << "base-salaried commission employee: " << firstName << " '"
           << lastName << " '" << socialSecurityNumber
           << "\ngross sales: " << grossSales
           << "\ncommission rate: " << commissionRate
```

