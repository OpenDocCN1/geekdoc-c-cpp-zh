

## 小结

- *类*是一种用户自定义数据类型，其中方法和数据作为成员组合在一起。
- *构造函数*的主要作用是初始化类，并为所有数据成员构造值。
- 三种类型的构造函数是：默认构造函数、参数化构造函数和拷贝构造函数。
- 析构函数有助于释放未使用对象的内存。
- 构造函数和析构函数都与类同名。
- C++ 中的 `this` 指针存储对象或类实例的地址，使成员函数能够更新相应对象的值。
- 类函数既可以在类定义内部定义，也可以在类定义外部定义。
- 调用类函数是通过类的对象并使用点运算符或选择运算符来完成的。
- 在 C++ 中，`static` 关键字可将任何变量、数据成员或函数声明为一种常量类型。这些值不能被修改。
- `::` 是 C++ 中的作用域解析运算符，其主要作用是访问类的静态成员或为其赋值。
- `new` 和 `delete` 运算符用于 C++ 中的内存分配和释放。

## 练习

### 理论题

- 1. 什么是类？请用示例描述声明类的语法。
- 2. 讨论 C++ 中类的创建和声明？
- 3. 在类主体内部定义的成员函数与在类主体外部定义的成员函数有什么区别？
- 4. 解释传递对象参数的不同方法。
- 5. 使用示例讨论 C++ 中的构造函数和析构函数。
- 6. C++ 中如何动态进行内存分配？
- 7. `static` 关键字在 C++ 中可以以几种方式使用？请使用代码示例讨论这一点。

### 实践题

- 1. 编写一个程序，创建一个名为 `Student` 的类，其中包含一个字符串变量 name 和一个整型变量 `roll_no`。通过创建 `Student` 类的对象，将 `roll_no` 的值赋为 2，将 name 的值赋为 John。
- 2. 编写一个 C++ 程序，演示类的声明和定义以及类成员的访问。
- 3. 编写一个 C++ 程序，演示类的构造函数的调用。
- 4. 编写一个 C++ 程序，演示类的析构函数的调用。
- 5. 编写一个 C++ 程序，使用类的概念实现一个带菜单的简单计算器。
- 6. 编写一个 C++ 程序，演示 `static` 关键字的使用方式。
- 7. 编写一个 C++ 程序，使用 `static` 关键字统计并显示对象被创建的次数。
- 8. 编写一个 C++ 程序，演示 `new` 和 `delete` 运算符的使用。
- 9. 编写一个 C++ 程序，仅使用指针变量实现一个带菜单的简单计算器。

### 选择题

- 1. 关于类，以下哪个语句是正确的？
  - a. 对象是它所属类的一个实例。
  - b. 类是它所属对象的一个实例。
  - c. 对象是该类的数据类型的一个实例。
  - d. A 和 C 都正确。
- 2. 如果在函数中定义了一个局部类，那么对于该类的对象，下列说法正确的是？
  - a. 该对象可以在该函数中局部地访问、声明和使用。
  - b. 该对象必须在任何其他函数中声明。
  - c. 该对象在函数外部可以临时访问。
  - d. 该对象可以在程序中的任何位置调用该类的所有其他成员。
- 3. 以下哪项指的是将数据及其功能封装到单个独立实体中？
  - a. 模块化
  - b. 抽象
  - c. 封装
  - d. 以上都不是
- 4. 当使用 `struct` 而不是关键字 `class` 时，程序中会发生什么？
  - a. 默认访问权限是公有的
  - b. 默认访问权限是私有的
  - c. 默认访问权限是保护的
  - d. 访问被拒绝
- 5. 以下哪个用于在类外部定义类的成员？
  - a. `:`
  - b. `::`
  - c. `#`
  - d. `!!$`
- 6. C++ 中的类包含什么？
  - a. 数据
  - b. 函数
  - c. 数据和函数
  - d. 数组
- 7. 在类中，数据成员也被称为 ________
  - a. 抽象
  - b. 属性
  - c. 特性
  - d. 维度
- 8. C++ 中的一个类中有多少个访问说明符？
  - a. 2
  - b. 1
  - c. 4
  - d. 3

### 选择题答案

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| (a) | (a) | (c) | (a) | (b) | (c) | (b) | (d) |

## 参考资料

### 书籍

- B. Stroustrup，*C++ 程序设计语言*（第 4 版）（Addison-Wesley Professional，2013 年）。
- K. R. Venugopal，*精通 C++*（第 2 版）（McGraw Hill Education，2017 年 7 月）。
- Y. Kanetkar，*让我们学 C++*（BPB Publications，2020 年 9 月）。
- Y. Kanetkar，*测试你的 C++ 技能*（BPB Publications，2003 年 3 月）。

### 网站

- Learn CPP，访问于 2022 年 7 月，*https://www.learncpp.com*
- Codes Cracker，访问于 2022 年 7 月，*https://codescracker.com*
- Geeks For Geeks，访问于 2022 年 7 月，*https://www.geeksforgeeks.org*
- Udacity，访问于 2022 年 7 月，*https://www.udacity.com*
- Scaler，访问于 2022 年 7 月，*https://www.scaler.com*
- C Plus Plus，访问于 2022 年 7 月，*https://cplusplus.com*

## 继承

### 6.1 引言

我们在第一章中简要讨论了面向对象编程的概念。现在，让我们深入学习其中几个概念。我们熟悉类的创建，以及对象如何访问类以使用某个特定类的成员。在 C++ 中，我们可以在一个程序中创建多个类（并在这些类之间建立联系），使它们能够共享对其各自数据成员的访问。这种在类之间建立联系并共享某些属性的概念被称为*继承*。本章将探讨继承及其类型，以及如何充分利用这一面向对象编程概念。所有讨论的主题都附有代码示例，我们鼓励读者全部尝试一遍，以提高对这一主题的理解。

### 6.2 继承

正如孩子不仅会继承父母的资产，还会继承一些独特的特征，如眼睛或头发的颜色，C++ 中的继承被定义为“子”类继承其“父”类特征的能力。在继续之前，让我们进一步了解这些术语。

- *父类*：也称为*基类*或*超类*。你可以把它看作是在其子类之前已存在的实体。它的所有子类都从它继承属性。

### 代码：使用访问说明符（公有、私有、保护）

```cpp
#include <iostream>
using namespace std;
class Parent {

    public:
    int p1=60;
    void showP()
    {
        cout<<"\nParent age is public " <<p1<< endl;
        cout<<"\nParent age is private " <<p2<< endl;
        cout<<"\nParent age is protected " <<p3<< endl;
    }
    private:
    int p2=12;
    protected:
    int p3=16;
};

class Child : public Parent
{

    public:
    int c1=20;
    void showC() {
        cout<< "\nChild age is public " <<c1<< endl;
        cout<< "\nChild age is private " <<c2<< endl;
        cout<< "\nChild age is protected " <<c3<< endl;
    }
    private:
    int c2;
    protected:
    int c3;
};

int main() {
    Child c;
    c.p2=36;
    c.p3=56;
    c.showP();
    c.showC();
    return 0;
}
```

### 输出：

```text
inherit.cpp:37:7: error: 'p2' is a private member of 'Parent'
    c.p2= 36;
      ^

inherit.cpp:14:9: note: declared private here
    int p2;
        ^

inherit.cpp:38:7: error: 'p3' is a protected member of 'Parent'
    c.p3=56;
      ^

inherit.cpp:16:9: note: declared protected here
    int p3;
        ^
```

请仔细研究给出的代码片段，以及当我们尝试在派生类调用中访问声明为私有（private）和保护（protected）的数据成员时所产生的错误。

### 6.2.2 继承方式

- 1. **公有：** 如果一个类以公有方式继承，那么基类中为数据成员定义的访问权限在派生类中也会保持不变。也就是说，公有成员具有公有访问权限，私有成员具有私有访问权限，保护成员具有保护访问权限。这是一种常用的继承访问方式。

### 代码：提供对数据的访问

```cpp
#include <iostream>
using namespace std;
class parentc
{
    public :
        int age=52;
    protected :
        int avgSal= 43000;
    private :
        int adharDigit=876;

};
class PublicChild : public parentc
{
    public:
    int pro()
    {
        return avgSal;
    }
};
```

