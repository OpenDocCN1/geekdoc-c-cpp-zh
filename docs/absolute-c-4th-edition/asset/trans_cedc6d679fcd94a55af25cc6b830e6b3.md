

## 显示 14.3 — 派生类 HourlyEmployee 的接口

```cpp
//This is the header file hourlyemployee.h.
//This is the interface for the class HourlyEmployee.
#ifndef HOURLYEMPLOYEE_H
#define HOURLYEMPLOYEE_H

#include <string>
#include "employee.h"

using std::string;

namespace SavitchEmployees
{

    class HourlyEmployee : public Employee
    {
    public:
        HourlyEmployee( );
        HourlyEmployee(string theName, string theSsn,
                       double theWageRate, double theHours);
        void setRate(double newWageRate);
        double getRate( ) const;
        void setHours(double hoursWorked);
        double getHours( ) const;
        void printCheck( );
    private:
        double wageRate;
        double hours;
    };

}//SavitchEmployees

#endif //HOURLYEMPLOYEE_H
```

> 请注意，派生类的定义与任何其他类定义开始方式相同，但在类定义的第五行添加了冒号、保留字 public 以及基类的名称，如下所示（来自显示 14.3）：

```cpp
class HourlyEmployee : public Employee
{
```
派生类（如 HourlyEmployee）会自动获得基类（如 Employee）的所有成员变量和成员函数，并可以添加额外的成员变量和成员函数。

## 显示 14.4 派生类 SalariedEmployee 的接口

```
//This is the header file salariedemployee.h.
//This is the interface for the class SalariedEmployee.
#ifndef SALARIEDEMPLOYEE_H
#define SALARIEDEMPLOYEE_H

#include <string>
#include "employee.h"

using std::string;

namespace SavitchEmployees
{

class SalariedEmployee : public Employee
{
public:
    SalariedEmployee();
    SalariedEmployee(string theName, string theSsn, double theWeeklySalary);
    double getSalary() const;
    void setSalary(double newSalary);
    void printCheck();
private:
    double salary;//weekly
};

}//SavitchEmployees

#endif //SALARIEDEMPLOYEE_H
```

类 HourlyEmployee 的定义没有提到成员变量 name、ssn 和 netPay，但 HourlyEmployee 类的每个对象都有名为 name、ssn 和 netPay 的成员变量。成员变量 name、ssn 和 netPay 是从类 Employee 继承而来的。类 HourlyEmployee 声明了两个额外的成员变量 wageRate 和 hours。因此，HourlyEmployee 类的每个对象都有五个成员变量，名为 ssn、netPay、wageRate 和 hours。请注意，派生类（如 HourlyEmployee）的定义只列出新增的成员变量。基类中定义的成员变量不会被提及。它们会自动提供给派生类。

正如它继承了类 Employee 的成员变量一样，类 HourlyEmployee 也继承了类 Employee 的所有成员函数。因此，类 HourlyEmployee 从类 Employee 继承了成员函数 getName、getSsn、getNetPay、setName、setSsn、setNetPay 和 printCheck。

## 继承的成员

派生类自动拥有基类的所有成员变量和所有普通成员函数。 （正如本章后面所讨论的，有一些特殊的成员函数，如构造函数，并不会自动继承。）这些来自基类的成员被称为继承。 这些继承的成员函数和继承的成员变量，除一个例外外，都不会在派生类的定义中提及，但它们会自动成为派生类的成员。如文中所述，如果你想更改继承成员函数的定义，则会在派生类的定义中提及该继承成员函数。

除了继承的成员变量和成员函数外，派生类还可以添加新的成员变量和新的成员函数。新的成员变量和新的成员函数的声明列在类定义中。例如，派生类 HourlyEmployee 添加了两个成员变量 wageRate 和 hours，并添加了新的成员函数 setRate、getRate、setHours 和 getHours。这在显示 14.3 中有所展示。请注意，除非你想更改继承成员函数的定义，否则不会给出继承成员函数的声明，我们稍后会讨论这一点。现在，不要担心派生类构造函数定义的细节。我们将在下一小节讨论构造函数。

在派生类的实现文件中，例如显示 14.5 中 HourlyEmployee 的实现，你给出所有新增成员函数的定义。请注意，除非在派生类中更改了成员函数的定义，否则不会给出继承成员函数的定义，我们接下来会讨论这一点。

## 父类和子类

在讨论派生类时，通常使用源自家庭关系的术语。基类通常被称为父类。派生类则被称为子类。这使得继承的语言非常流畅。例如，我们可以说子类从其父类继承其成员变量和成员函数。这个类比通常会再进一步。一个类的父类的父类（或其他任意数量的“父类的”迭代）通常被称为祖先类。如果类 A 是类 B 的祖先，则类 B 通常被称为类 A 的后代。

派生类定义中可以更改继承成员函数的定义，使其在派生类中的含义与在基类中的含义不同。这称为重新定义继承的成员函数。例如，

成员函数 printCheck( ) 在派生类 HourlyEmployee 的定义中被重新定义。要重新定义成员函数定义，只需将其列在类定义中并为其提供新的定义，就像你对在派生类中添加的成员函数所做的那样。这通过类 HourlyEmployee 的重新定义函数 printCheck( ) 进行了说明（显示 14.3 和 14.5）。

## 显示 14.5 派生类 HourlyEmployee 的实现（第 1 部分，共 2 部分）

```cpp
1 //This is the file hourlyemployee.cpp.
2 //This is the implementation for the class HourlyEmployee.
3 //The interface for the class HourlyEmployee is in
4 //the header file hourlyemployee.h.
5 #include <string>
6 #include <iostream>
7 #include "hourlyemployee.h"
8 using std::string;
9 using std::cout;
10 using std::endl;
11 
12 namespace SavitchEmployees
13 {
14     HourlyEmployee::HourlyEmployee() : Employee(), wageRate(0), hours(0)
15     {
16         //deliberately empty
17     }
18     
19     HourlyEmployee::HourlyEmployee(string theName, string theNumber,
20                                    double theWageRate, double theHours)
21         : Employee(theName, theNumber), wageRate(theWageRate), hours(theHours)
22     {
23         //deliberately empty
24     }
25     
26     void HourlyEmployee::setRate(double newWageRate)
27     {
28         wageRate = newWageRate;
29     }
30     
31     double HourlyEmployee::getRate() const
32     {
33         return wageRate;
34     }
35     
36     void HourlyEmployee::setHours(double hoursWorked)
37     {
38         hours = hoursWorked;
39     }
```

### 3.2 基于深度学习的文本检测与识别

传统的文本检测与识别方法依赖于手工设计的特征，如边缘检测、连通域分析等，这些方法在复杂场景下鲁棒性较差。近年来，随着深度学习技术的快速发展，基于深度学习的文本检测与识别方法逐渐成为主流，并在自然场景、文档图像、视频帧等多种应用中取得了显著的性能提升。

在文本检测方面，主流方法可分为基于回归的方法和基于分割的方法。基于回归的方法（如EAST、DBNet）直接预测文本区域的边界框或多边形，具有较高的推理速度；基于分割的方法（如PSENet、PANet）则通过像素级分割来定位文本区域，能够更好地处理任意形状的文本。

在文本识别方面，基于CTC（Connectionist Temporal Classification）的方法和基于注意力机制的方法是目前的两大主流框架。CTC方法（如CRNN）通过引入时序分类损失，能够有效处理不定长序列的识别问题；注意力方法（如ASTER、SAR）则通过编码器-解码器结构，结合注意力机制实现更精准的字符对齐与识别。

此外，端到端的文本检测与识别方法（如FOTS、Mask TextSpotter）将检测和识别任务统一到一个网络框架中，通过共享特征提取层，不仅简化了训练流程，还提升了整体性能。这些方法在车牌识别、票据识别、场景文字翻译等实际应用中展现了巨大的潜力。

尽管基于深度学习的文本检测与识别方法已取得显著进展，但在复杂背景、多语言混合、低分辨率等场景下仍面临挑战。未来的研究将更加注重模型的轻量化、跨域泛化能力以及多模态信息的融合。

