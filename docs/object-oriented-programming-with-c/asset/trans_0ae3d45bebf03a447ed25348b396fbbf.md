

```cpp
constructor (arglist) : initialization-section
{ assignment-section
}
```

_赋值部分_ 只是构造函数函数的主体，用于为其数据成员赋初始值。冒号后面紧跟的部分称为 _初始化部分_。我们可以使用此部分为基构造函数提供初始值，并初始化其自身的类成员。这意味着我们可以使用任一节来初始化构造函数类的成员数据。初始化部分基本上包含由逗号分隔的初始化列表。此列表称为 _初始化列表_。考虑一个简单示例：

```cpp
class XYZ
{
int a;
int b;
public:
XYZ(int i, int j) : a(i), b(2 * j) { }
};
main()
{
XYZ x(2, 3);
}
```

此程序将把 **a** 初始化为 2，**b** 初始化为 6。注意数据成员是如何初始化的，只需使用变量名后跟用括号括起的初始化值（像函数调用一样）。参数列表中的任何参数都可作为初始化值使用，且列表中的项目可以按任意顺序排列。例如，构造函数 **XYZ** 也可以写成：

```cpp
XYZ(int i, int j) : b(i), a(i + j) { }
```

在这种情况下，**a** 将被初始化为 5，**b** 为 2。记住，数据成员是按照声明的顺序进行初始化的，与初始化列表中的顺序无关。这使我们能够有如下语句

```cpp
XYZ(int i, int j) : a(i), b(a * j) { }
```

这里 a 被初始化为 2，b 为 6。记住，先声明的 a 先被初始化，然后其值被用来初始化 b。然而，以下写法将不起作用：

```cpp
XYZ(int i, int j) : b(i), a(b * j) { }
```

因为 b 的值在需要先初始化的 a 中不可用。

以下语句也是有效的：

```cpp
XYZ(int i, int j) : a(i) { b = j; }
XYZ(int i, int j) { a = i; b = j; }
```

如果不需要，我们可以省略任一节。程序 8.8 说明了在基类和派生类构造函数中使用初始化列表。

## Program 8.8 Initialization List in Constructors

```cpp
#include <iostream>
using namespace std;
class alpha
{
int x;
public:
alpha(int i)
{
x = i;
cout << "\n alpha constructed";

g.show_beta();
g.show_gamma();
return 0;
};
```

程序 8.8 的输出为：

```
beta constructed
alpha constructed
gamma constructed
Display member values
x = 4
p = 2.5
q = 5
u = 2
v = 4
```

> **NOTE:** *派生构造函数 **gamma** 的参数列表仅包含三个参数 **a**、**b** 和 **c**，它们用于初始化三个类中包含的五个数据成员。*

## 8.12 Member Classes: Nesting of Classes

继承是将一个类的某些属性派生到另一个类的机制。我们已经详细了解了如何使用派生类的概念来实现这一点。C++ 还支持另一种将一个类的属性继承到另一个类的方式。这种方法认为一个对象可以是许多其他对象的集合。也就是说，一个类可以包含其他类的对象作为其成员，如下所示：

```cpp
class alpha {...};
class beta {...};
```

```cpp
class gamma
{
alpha a; // a 是 alpha 类的对象
beta b; // b 是 beta 类的对象
....
};
```

**gamma** 类的所有对象都将包含对象 **a** 和 **b**。这种关系称为 *包含关系* 或 *嵌套*。创建包含另一个对象的对象与创建独立对象非常不同。独立对象在声明时带参数时由其构造函数创建。另一方面，嵌套对象是分两阶段创建的。首先，使用各自的构造函数创建成员对象，然后创建其他成员。这意味着，所有成员对象的构造函数都应在自身构造函数体执行之前被调用。这是通过在嵌套类的构造函数中使用初始化列表来实现的。

示例：

```cpp
class gamma
{
....
alpha a; // a 是 alpha 的对象
beta b; // b 是 beta 的对象
public:
gamma(arglist): a(arglist1), b(arglist2)
{
// 构造函数体
}
};
```

*arglist* 是在定义 **gamma** 对象时要提供的参数列表。这些参数用于初始化 **gamma** 的成员。*arglist1* 是 **a** 的构造函数的参数列表，*arglist2* 是 **b** 的构造函数的参数列表。*arglist1* 和 *arglist2* 可能使用也可能不使用来自 *arglist* 的参数。

记住，_a_(_arglist1_) 和 _b_(_arglist2_) 是函数调用，因此参数不包含数据类型。它们只是变量或常量。

```cpp
gamma(int x, int y, float z) : a(x), b(x,z)
{
赋值部分（用于普通其他成员）
}
```

我们可以在一个类中使用任意多个成员对象。对于每个成员对象，我们在初始化列表中添加一个构造函数调用。成员对象的构造函数是按照它们在嵌套类中声明的顺序调用的。

## Summary

- 将新类从旧类派生出来的机制称为继承。继承提供了可重用性的概念。C++ 类可以通过继承被重用。
- 派生类继承基类的部分或全部属性。
- 只有一个基类的派生类称为单继承。
- 一个类可以从多个类继承属性，这称为多继承。
- 一个类可以从另一个派生类派生，这称为多级继承。
- 当一个类的属性被多个类继承时，这称为层次继承。
- 类的私有成员无论在公有模式还是私有模式下都不能被继承。
- 在公有模式下继承的受保护成员变为受保护，而在私有模式下继承则在派生类中变为私有。
- 在公有模式下继承的公有成员变为公有，而在私有模式下继承则在派生类中变为私有。
- 友元函数和友元类的成员函数可以直接访问私有和受保护的数据。
- 派生类的成员函数只能直接访问受保护和公有数据。然而，它们可以通过基类的成员函数访问私有数据。
- 多路径继承可能导致从“祖父”基类继承的成员重复。这可以通过将公共基类设为虚基类来避免。
- 在多继承中，基类是按照它们在派生类声明中出现的顺序构造的。
- 在多级继承中，构造函数是按照继承顺序执行的。
- 一个类可以包含其他类的对象。这称为包含关系或嵌套。

## Key Terms

- abstract class
- access control
- access mechanism
- ancestor class
- assignment section
- base class
- base constructor
- child class
- common base class
- containership
- derivation
- derived class
- derived constructor
- direct base class
- dot operator
- duplicate members
- father class
- **friend**
- grandfather class
- grandparent class
- hierarchical inheritance
- hybrid inheritance
- indirect base class
- inheritance
- inheritance path
- initialization list
- initialization section
- intermediate base
- member classes
- multilevel inheritance
- multiple inheritance
- nesting
- **private**
- private derivation
- private members
- privately derived
- **protected**
- protected members
- **public**
- public derivation
- public members
- publicly derived
- reusability
- single inheritance
- subclass
- virtual base class
- visibility mode
- visibility modifier

## Review Questions

- 8.1 C++ 中的继承是什么意思？
- 8.2 继承有哪些不同形式？请为每种形式举例。
- 8.3 描述 C++ 中单继承的语法。
- 8.4 我们知道基类的私有成员不可继承。是否以任何方式可能让派生类的对象访问基类的私有成员？如果可以，如何实现？记住，基类不能被修改。
- 8.5 以下两个派生类的属性有何不同？

  - (a) `class D1: private B{//...};`
  - (b) `class D2: public B{//....};`

- 8.6 我们在何时对类成员使用受保护的可见性说明符？

