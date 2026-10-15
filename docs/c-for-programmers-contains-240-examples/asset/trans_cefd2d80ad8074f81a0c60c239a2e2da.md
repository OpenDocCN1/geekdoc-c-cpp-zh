

word explicit 到第 15 行的单参数构造函数的声明。包含类 Array 成员函数定义的源代码文件无需修改。

图 11.18 展示了图 11.16 中程序的略微修改版本。编译此程序时，编译器会产生错误消息，指出第 15 行传递给 outputArray 的整数值无法转换为 const Array &。编译器错误消息显示在输出窗口中。第 16 行演示了如何使用 explicit 构造函数创建一个包含 3 个元素的临时 Array 并将其传递给函数 outputArray。

## Common Programming Error 11.10

> 尝试为隐式转换调用 explicit 构造函数是编译错误。

## Common Programming Error 11.11

> 对除单参数构造函数之外的其他数据成员或成员函数使用 explicit 关键字是编译错误。

```
// Fig. 11.18: Fig11_18.cpp
// Driver for simple class Array.
#include <iostream>
using std::cout;
using std::endl;

#include "Array.h"

void outputArray( const Array & ); // prototype

int main()
{
    Array integers1( 7 ); // 7-element array
    outputArray( integers1 ); // output Array integers1
    outputArray( 3 ); // convert 3 to an Array and output Array's contents
    outputArray( Array( 3 ) ); // explicit single-argument constructor call
    return 0;
} // end main

// print array contents
void outputArray( const Array &arrayToOutput )
{
    cout << "The Array received has " << arrayToOutput.getSize()
        << " elements. The contents are:\n" << arrayToOutput << endl;
} // end outputArray
```

```
c:\cppfp_examples\ch11\Fig11_17_18\Fig11_18.cpp(15) : error C2664:
    'outputArray' : cannot convert parameter 1 from 'int' to 'const Array &'
    Reason: cannot convert from 'int' to 'const Array'
    Constructor for class 'Array' is declared 'explicit'
```

Fig. 11.18 | Demonstrating an explicit constructor.

## Error-Prevention Tip 11.3

在不应由编译器用于执行隐式转换的单参数构造函数上使用 explicit 关键字。

## 11.15 Wrap-Up

在本章中，你学习了如何通过定义重载运算符来构建更健壮的类，从而使程序员能够将你的类的对象视为 C++ 基本数据类型一样处理。我们介绍了基本的运算符重载概念，以及 C++ 标准对重载运算符施加的若干限制。你学习了实现重载运算符作为成员函数或作为全局函数的理由。我们讨论了将一元和二元运算符作为成员函数和全局函数重载之间的差异。对于全局函数，我们展示了如何使用重载的流提取和流插入运算符分别输入和输出我们类的对象。我们展示了区分前缀和后缀自增 (++) 运算符版本所需的特殊语法。我们还演示了标准 C++ 类 string，该类大量使用重载运算符来创建一个健壮、可重用的类，可以替代基于 C 风格指针的字符串。最后，你学习了如何使用关键字 explicit 防止编译器使用单参数构造函数执行隐式转换。在下一章中，我们将继续讨论类，介绍一种称为继承的软件重用形式。我们将看到，当类共享共同的属性和行为时，可以将这些属性和行为定义在共同的“基”类中，并将这些能力“继承”到新的类定义中。

## 12

## Object-Oriented
Programming:
Inheritance

## OBJECTIVES

在本章中你将学习：

- 通过从现有类继承来创建类。
- 继承如何促进软件重用。
- 基类和派生类之间的概念及其关系。
- 受保护的成员访问说明符。
- 继承层次结构中使用构造函数和析构函数。
- 继承层次结构中构造函数和析构函数的调用顺序。
- public、protected 和 private 继承之间的差异。
- 使用继承来自定义现有软件。

> 说你完全了解另一个人之前，不要与他分割继承。
> —Johann Kasper Lavater

> 此方法是把一个类的数目定义为与给定类相似的所有类的类。
> —Bertrand Russell

> 继承一个图书馆固然好，但收集一个图书馆更好。
> —Augustine Birrell

> 拯救基权威免受他人书籍的影响。
> —William Shakespeare

- 12.1 Introduction
- 12.2 Base Classes and Derived Classes
- 12.3 protected Members
- 12.4 Relationship between Base Classes and Derived Classes
    - 12.4.1 Creating and Using a CommissionEmployee Class
    - 12.4.2 Creating a BasePlusCommissionEmployee Class Without Using Inheritance
    - 12.4.3 Creating a CommissionEmployee–BasePlusCommissionEmployee Inheritance Hierarchy
    - 12.4.4 CommissionEmployee–BasePlusCommissionEmployee Inheritance Hierarchy Using protected Data
    - 12.4.5 CommissionEmployee–BasePlusCommissionEmployee Inheritance Hierarchy Using private Data
- 12.5 Constructors and Destructors in Derived Classes
- 12.6 public, protected and private Inheritance
- 12.7 Software Engineering with Inheritance
- 12.8 Wrap-Up

## 12.1 Introduction

本章通过介绍其另一个关键特性——*继承*，继续我们对面向对象编程 (OOP) 的讨论。继承是一种软件重用形式，你创建一个类吸收现有类的数据和行为并以新功能增强它们。软件可重用性在程序开发期间节省时间。它还鼓励重用经过验证、调试过的、高质量的软件，从而提高系统有效实现的机会。

创建类时，而不是编写全新的数据成员和成员函数，你可以指定新类应 *继承* 现有类的成员。此现有类称为 *基类*，新类称为 *派生类*。 （其他编程语言，如 Java，将基类称为 *超类*，将派生类称为 *子类*。）派生类代表更专门化的对象组。通常，派生类包含从其基类继承的行为加上额外的行为。正如我们将看到的，派生类还可以自定义从基类继承的行为。 *直接基类* 是派生类显式继承的基类。 *间接基类* 是在 *类层次结构* 中从两级或更多级向上继承的基类。在 *单继承* 的情况下，一个类派生自一个基类。C++ 还支持 *多继承*，其中派生类继承自多个（可能不相关）基类。单继承很直接——我们展示了几个示例，应该能让你迅速熟练掌握。多继承可能复杂且容易出错。我们在第 22 章 Other Topics 中讨论多继承。

C++ 提供 public、protected 和 private 继承。在本章中，我们集中于 public 继承并简要解释其他两种。private 继承和 protected 继承形式很少使用。通过 public 继承，派生类的每个对象也是该派生类基类的对象。然而，基类对象不是其派生类的对象。例如，如果我们有 vehicle 作为基类，car 作为派生类，那么所有汽车都是车辆，但并非所有车辆都是汽车。随着我们在本章和第 13 章继续研究面向对象编程，我们利用这种关系执行一些有趣的操作。

构建软件系统的经验表明，大量代码处理密切相关的特殊情况。当你忙于处理特殊情况时，细节可能会掩盖大局。通过面向对象编程，你关注系统对象之间的共同点而不是特殊情况。

我们区分 *is-a 关系* 和 *has-a 关系*。 *is-a* 关系代表继承。在 *is-a* 关系中，派生类的对象也可以被视为其基类的对象——例如，一辆汽车 *is a* 车辆，因此车辆的任何属性和行为也是汽车的属性和行为。相比之下， *has-a* 关系代表组合。 （组合在第 10 章中讨论。）在 *has-a* 关系中，一个对象包含一个或多个其他类的对象作为成员。例如，一辆汽车包含许多组件——它 *has a* 方向盘， *has a* 刹车踏板， *has a* 变速箱并 *has* 许多其他组件。

派生类成员函数可能需要访问基类数据成员和成员函数。派生类可以访问其基类的非私有成员。基类成员不应可供派生类的成员函数访问，应在基类中声明为 private。派生类可以通过基类中提供的非私有成员函数并继承到派生类中来影响私有基类成员的状态。

> **Software Engineering Observation 12.1**
> 
> *派生类的成员函数不能直接访问基类的私有成员。*

> **Software Engineering Observation 12.2**
> 
> *如果派生类可以访问其基类的私有成员，则从该派生类继承的类也可以访问该数据。这将传播对本应私有数据的访问，信息隐藏的好处将丧失。*

继承的一个问题是派生类可能继承它不需要或不应拥有的成员和成员函数。类设计者的责任是确保类提供的功能适合未来的派生类。即使基类成员函数对派生类是合适的，派生类通常也要求成员函数以特定于派生类的方式表现。在这种情况下，基类成员函数可以在派生类中重新定义并提供适当的实现。

## 12.2 Base Classes and Derived Classes

通常，一个类的对象 *is an* 另一个类的对象。例如，在几何中，矩形 *is a* 四边形（正方形、平行四边形和梯形也是如此）。因此，在 C++ 中，类 Rectangle 可以说 *继承* 自类 Quadrilateral。在此上下文中，类 Quadrilateral 是基类，类 Rectangle 是派生类。矩形是四边形的一种特定类型，但声称四边形 *is a* 矩形是不正确的——

