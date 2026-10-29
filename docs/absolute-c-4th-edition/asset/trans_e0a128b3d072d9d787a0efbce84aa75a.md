

继承，因此一旦一个类拥有虚函数表，那么它的所有派生类也都有虚函数表。）

每当创建一个具有一个或多个虚函数的类的对象时，存储在内存中的对象描述中会额外增加一个指针。这个指针指向该类的虚函数表。当你使用指向对象的指针（没错，又是一个指针）调用成员函数时，运行时系统使用虚函数表来决定使用哪个成员函数的定义；它不会使用指针的类型。

当然，这一切都是自动发生的，所以你不必担心它。编译器编写者甚至可以以其他方式实现虚函数，只要它能正确工作即可（尽管实际上从未以不同方式实现）。

## 自测练习

8. 为什么下面的是非法的？

```
Pet vpet;
Dog vdog; //Dog is a derived class with base class Pet.
...
vdog = static_cast<Dog>(vpet); //ILLEGAL!
```

## 章节总结

- 晚绑定意味着哪个版本的成员函数是合适的这一决定是在运行时做出的。在 C++ 中，使用晚绑定的成员函数称为虚函数。*多态*是晚绑定的另一个词。
- 纯虚函数是一个没有定义的成员函数。纯虚函数用关键字 *virtual* 和成员函数声明中的记号 = 0 表示。有一个或多个纯虚函数的类称为 *抽象类*。
- 抽象类是一种类型，可以用作基类来派生其他类。然而，你不能创建抽象类类型的对象（除非它是某个派生类的对象）。
- 你可以将派生类对象赋给其基类的变量（或任何祖先类），但不在基类中的成员变量会丢失。这被称为 *切片问题*。
- 如果指针 pAncestor 的域类型是指针 pDescendant 的域类型的基类，则允许以下指针赋值：

```
pAncestor = pDescendant;
```

而且，被 pDescendant 指向的动态变量的数据成员或成员函数都不会丢失。尽管动态变量的所有额外字段都在那里，但你需要虚成员函数来访问它们。

将析构函数设为虚函数是一个良好的编程实践。

## 自测练习答案

- 1. 本质上这三个术语之间没有区别。它们都指的是同一个主题。它们的使用上只有细微差别。（虚函数是一种成员函数，晚绑定是指当函数是虚函数时用于决定使用哪个函数定义所使用的机制，而多态是晚绑定的另一个名称。）
- 2. 输出将更改为以下内容：
  
  Discounted item is not cheaper.
- 3. 是的，拥有全部成员函数都是纯虚函数的抽象类是合法的。
- 4. a. 非法，因为 Employee 是一个抽象类。
  b. 合法。
  c. 合法，因为抽象类是一种类型。
- 5. 没有成员可以赋给派生类新增的成员。
- 6. 尽管将派生类对象赋给基类变量是合法的，但这会丢弃派生类对象中不是基类成员的部分。这种情况被称为切片问题。
- 7. 如果基类函数带有 virtual 修饰符，则调用派生类成员函数。如果基类成员函数没有 virtual 修饰符，则调用基类成员函数。
- 8. 由于 Dog 可能比 Pet 有更多的成员变量，对象 vpet 可能没有足够的数据来容纳所有类型为 Dog 的成员变量。

## 编程项目

- 1. 考虑一个图形系统，它有各种图形的类，比如矩形、正方形、三角形、圆形等等。例如，矩形可能有数据成员高度、宽度和中心点，而正方形和圆形可能只有中心点和边长或半径，分别。在一个设计良好的系统中，这些将派生自一个公共类 Figure。你需要实现这样一个系统。
  
  类 Figure 是基类。你应该仅添加派生自 Figure 的 Rectangle 和 Triangle 类。每个类都有成员函数 erase 和 draw 的存根。每个这些成员函数输出一条消息，说明哪个函数被调用以及调用对象的类是什么。由于这些只是存根，它们除了输出此消息之外什么也不做。成员函数 center 调用 erase 和 draw 以擦除并重绘图形的中心。由于你只有 erase 和 draw 的存根，center 不会做任何“居中”操作，但会调用成员函数 erase 和 draw。另请在成员函数 center 中添加一条输出消息，宣布 center 正在被调用。成员函数不应接受任何参数。该项目有三个部分：
  
  a. 使用不带虚函数的类定义。编译并测试。
  b. 使基类成员函数变为虚函数。编译并测试。
  c. 解释结果的差异。

对于真实的例子，你必须用实际绘图代码替换这些成员函数的定义。你将在编程项目 2 中被要求这样做。

对所有测试使用以下 main 函数：

```
//This program tests Programming Problem 1.

#include <iostream>
#include "figure.h"
#include "rectangle.h"
#include "triangle.h"
using std::cout;
int main()
{
    Triangle tri;
    tri.draw();
    cout << "\nDerived class Triangle object calling center().\n";
    tri.center(); //Calls draw and center

    Rectangle rect;
    rect.draw();
    cout << "\nDerived class Rectangle object calling center().\n";
    rect.center(); //Calls draw and center
    return 0;
}
```

2. 完善编程问题 1。为各种构造函数和成员函数 Figure::center, Figure::draw, Figure::erase, Triangle::draw, Triangle::erase, Rectangle::draw 和 Rectangle::erase 提供新的定义，以便 draw 函数通过在屏幕上的合适位置放置字符 '*' 实际在屏幕上绘制图形。对于 erase 函数，你可以简单地清除屏幕（通过输出空白行或做更复杂的操作）。其中有很多细节，你必须自行决定其中的一些。

如需更多在线编程项目，请点击下方的 CodeMate 图标。

# 16 CHAPTER Templates

![](img/9505fd46e120aa9c1406715936ff6251_646_0.png)

- 16.1 FUNCTION TEMPLATES 654
- Syntax for Function Templates 656
- Pitfall: Compiler Complications 659
- Example: A Generic Sorting Function 661
- Tip: How to Define Templates 665
- Pitfall: Using a Template with an Inappropriate Type 665
  
- 16.2 CLASS TEMPLATES 667
- Syntax for Class Templates 667
- Example: An Array Template Class 671
- The vector and basic_string Templates 677
  
- 16.3 TEMPLATES AND INHERITANCE 678
- Example: Template Class for a Partially filled Array with Backup 678
- CHAPTER SUMMARY 684
- ANSWERS TO SELF-TEST EXERCISES 684
- PROGRAMMING PROJECTS 688

```
temp = variable1;
variable1 = variable2;
variable2 = temp;
}
```

请注意，函数 swapValues 仅适用于类型为 int 的变量。然而，函数体中给出的算法同样可以用来交换两个类型为 char 的变量的值。如果我们还想用函数 swapValues 来交换类型为 char 的变量，我们可以通过添加以下定义来重载函数名 swapValues：

```
void swapValues(char& variable1, char& variable2)
{
    char temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

但这两种 swapValues 函数定义显得低效且不令人满意：它们几乎完全相同。唯一的区别是一个定义在三个地方使用类型 int，另一个在相同三个地方使用类型 char。以这种方式继续，如果我们希望函数 swapValues 适用于类型为 double 的变量对，我们就必须编写第三个几乎相同的函数定义。如果我们希望 swapValues 适用于更多类型，几乎相同的函数定义的数目会更大。这需要大量的输入，并且会让我们的代码充斥着看起来完全相同的许多定义。我们应该能够说以下函数定义适用于任何类型的变量：

```
void swapValues(Type_Of_The_Variables& variable1,
                Type_Of_The_Variables& variable2)
{
    Type_Of_The_Variables temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

正如我们将看到的，类似这样的操作是可能的。我们可以定义一个适用于所有类型变量的函数，尽管语法比上面所示的要复杂一些。正确的语法在下一小节中描述。

