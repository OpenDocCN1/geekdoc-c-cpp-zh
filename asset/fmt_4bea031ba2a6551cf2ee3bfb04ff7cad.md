
# 12.4 虚函数与虚析构函数

```cpp
std::string firstName;
std::string lastName;
std::string socialSecurityNumber;
double grossSales; // 总销售额
double commissionRate; // 佣金比例
};
#endif
```

图 12.4 | `CommissionEmployee` 类将 `earnings` 和 `toString` 声明为虚函数。
（第 2 部分，共 2 部分）。

```cpp
// Fig. 12.5: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee 类继承自 CommissionEmployee 类。
#ifndef BASEPLUS_H
#define BASEPLUS_H
#include <string> // C++ 标准字符串类
#include "CommissionEmployee.h" // CommissionEmployee 类
class BasePlusCommissionEmployee : public CommissionEmployee {
public:
    BasePlusCommissionEmployee(const std::string&, const std::string&,
    const std::string&, double = 0.0, double = 0.0, double = 0.0);
    void setBaseSalary(double); // 设置基础工资
    double getBaseSalary() const; // 返回基础工资
    virtual double earnings() const; // 计算佣金
    virtual std::string toString() override; // 字符串表示
private:
    double baseSalary; // 基础工资
};
#endif
```

图 12.5 | `BasePlusCommissionEmployee` 类将 `earnings` 和 `toString` 声明为虚函数并覆盖。

我们修改了 12.1 以创建图 12.6 所示程序。图 12.5 的第 32–44 行表明，指向 `CommissionEmployee` 对象的 `CommissionEmployee` 指针可以调用 `CommissionEmployee` 功能，而指向 `BasePlusCommissionEmployee` 对象的 `BasePlusCommissionEmployee` 指针可以用于调用 `BaseEmployee` 功能。当第 54 行调用基类指针时，会调用派生类 `BasePlusCommissionEmployee` 的 `toString` 函数，因此第 54 行输出的文本与图 12.1 中的第 46 行不同（在当时成员函数未声明为虚函数时）。我们看到，程序是根据对象的类型而不是句柄的类型来决定调用哪个函数的。当 `CommissionEmployeePtr` 指向 `CommissionEmployee` 对象时，调用的是 `CommissionEmployee` 的 `toString` 函数（图 12.6，第 36 行），而当 `CommissionEmployeePtr` 指向 `BasePlusCommissionEmployee` 对象时，调用的是 `BasePlusCommissionEmployee` 的 `toString` 函数（第 54 行）。因此，相同的 `toString` 消息——通过基类指针发送给各种派生类——实现了多态行为。

```cpp
// Fig. 12.6: fig12_06.cpp
// 引入多态性、虚函数和动态绑定。
#include <iostream>
#include <iomanip>
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;
int main() {
    // 创建基类对象
    CommissionEmployee employee("Sue", "Jones", "222-2222", 10000, .06);
    // 创建派生类对象
    BasePlusCommissionEmployee basePlusCommissionEmployee("Bob", "Lewis", "333-3333", 5000, .04, 300);
    cout << setprecision(2); // 设置浮点数格式
    // 使用静态绑定输出对象
    cout << "\nINVOKING TOSTRING ON BASE-CLASS AND DERIVED-CLASS OBJECTS WITH STATIC BINDING\n"
         << employee.toString(); // 静态绑定
         << "\n";
    // 使用动态绑定输出对象
    CommissionEmployee* commissionEmployeePtr = &employee;
    cout << "\nINVOKING TOSTRING ON BASE-CLASS AND DERIVED-CLASS POINTER-TO-OBJECT\n"
         << commissionEmployeePtr->toString(); // 动态绑定
    // 注：此处原文代码块逻辑存在重复，翻译遵循原文结构
}
```

## 12.5 类型字段与 switch 语句

基类的直接和间接派生类。同样地，在 C++11 之前，任何现有的类都可以作为层次结构中的基类。从 C++11 开始，你可以将一个类声明为 `final` 以防止其用作基类，如下：

```cpp
class MyClass final { //此类不能作为基类
  // 类体
};
```

尝试重写 `final` 成员函数或继承自 `final` 基类会导致编译错误。

确定对象类型的一种方法是使用 `switch` 语句来检查字段的值。这允许我们区分不同的对象，然后为特定对象调用适当的操作，类似于通过多态可以实现的功能。例如，在形状层次结构中，如果每个形状都有一个 `shapeType` 属性，`switch` 就可以检查对象的 `shapeType` 来决定调用哪个 `toString` 函数。

使用 `switch` 逻辑会带来各种潜在问题。例如，你可能在需要类型测试时忘记包含它，或者忘记在 `switch` 语句中处理所有可能的情况。在通过添加新类型来修改基于 `switch` 的系统时，你可能会忘记在所有相关的 `switch` 语句中插入新分支。每个类的添加或删除都需要修改系统中的每个相关 `switch` 语句；跟踪这些更改可能非常耗时且容易出错。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_587_0.png)

> 软件工程观察 12.6
多态编程可以消除对 `switch` 逻辑的需求。通过使用多态机制执行等效逻辑，你可以避免通常与 `switch` 逻辑相关的错误。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_587_1.png)

> 软件工程观察 12.7
多态的一个有趣的结果是程序变得外观简洁。它们包含了更分支逻辑和简单的顺序代码。

## 12.6 抽象类与纯虚函数

当我们把类视为一种类型时，我们假设程序将创建该类型的对象。然而，在某些情况下，定义一些从未打算实例化的类是有用的。此类类被称为抽象类。由于这些类通常在继承层次结构中充当基类，我们称它们为抽象基类。这些类不能用于实例化对象，因为正如我们将看到的，抽象类是不完全的——派生类在实例化之前必须定义对象的“缺失部分”。我们将在第 12.7 节中用抽象类构建程序。

抽象类是一个其他类可以继承自的基类。可以用于实例化对象的类被称为具体类。每个具体类都为其定义的每个成员函数定义或继承了实现。一个很好的例子在 11.3 节，它从抽象基类 `Shape` 开始。我们可以有一个抽象基类 `TwoDimensionalShape`，并派生出它的具体类 `Circle`、`Square` 和 `Triangle`。我们也可以有一个抽象类 `ThreeDimensionalShape` 并派生出如 `Cube`、`Sphere` 和 `Tetrahedron` 这样的具体类。抽象类过于通用，无法定义真实的对象；在能够实例化对象之前，我们需要更具体一些。例如，如果有人告诉你要“画一个二维形状”，你会画什么？具体类提供了使实例化对象成为可能的具体细节。

### 12.6.1 纯虚函数

通过将类的一个或多个虚函数声明为“纯”，可以使该类变为抽象类。纯虚函数通过在其声明中放置 `= 0` 来指定，如下：

```cpp
virtual void draw() const = 0; // 纯虚函数
```
