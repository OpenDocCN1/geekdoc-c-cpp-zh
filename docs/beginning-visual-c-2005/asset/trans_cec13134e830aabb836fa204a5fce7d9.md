
这里我要谈的是一剂极其强大的“良药”，它会使你编程的方式发生重大改变。你不再根据本质上与计算机相关的数据类型（整数、浮点数等）来分解问题，然后编写程序，而是根据与问题相关的数据类型来编程，也就是类。这些类可能命名为 CEmployee、CCowboy、CCheese 或 CChutney，每个类都针对你想要解决的那类问题专门定义，并且带有操作你新类型实例所需的函数和运算符。

如今，程序设计的第一步是确定需要哪些新的、与应用相关的数据类型来解决手头的问题，然后围绕问题所涉及的具体对象（无论是 CCoffins 还是 CCowpokes）上的操作来编写程序。

## 术语

我先总结一下在讨论 C++ 类时会用到的一些术语：

- **类**是一种用户自定义的数据类型。
- **面向对象编程**（OOP）是一种编程风格，其基本思想是将自己的数据类型定义为类。
- 声明类类型的对象有时称为**实例化**，因为你在创建类的一个**实例**。
- 类的实例称为**对象**。
- 对象包含其定义中隐含的数据，以及操作这些数据的函数，这种思想称为**封装**。

当我深入探讨面向对象编程的细节时，有些地方可能看起来有点复杂，但回到你所做事情的基本原理，往往有助于让事情更清晰，所以请始终牢记对象的真正意义。对象的意义在于：围绕你的问题领域所特有的对象来编写程序。C++ 中围绕类的各种设施，都是为了让这种编程方式尽可能全面而灵活。现在让我们开始理解类吧。

## 理解类

类是你定义的一种数据类型的规范。它可以包含数据元素，这些数据元素既可以是 C++ 基本类型的变量，也可以是其他用户自定义类型的变量。类的数据元素可以是单个数据元素、数组、指针、几乎任何类型的指针数组，或其他类的对象，因此你在数据类型中可以包含的内容非常灵活。类还可以包含函数，这些函数通过访问对象所包含的数据元素来操作该类的对象。因此，类既定义构成对象的基本数据，也定义操作属于该类的各个对象的数据的手段。

类中的数据和函数称为类的**成员**。有趣的是，类中作为数据项的成员称为**数据成员**，而作为函数的成员称为**函数成员**或**成员函数**。类的成员函数有时也称为**方法（methods）**；本书不使用这个术语，但请记住，你在其他地方可能会看到它。

数据成员也称为**字段（fields）**，这个术语用于 C++/CLI，因此我会不时使用这个术语。

当你定义一个类时，你是在为一种数据类型定义蓝图。这实际上并不定义任何数据，而是定义类名的含义，即类的对象将由什么构成，以及可以对这样的对象执行哪些操作。这很像你为基本类型`double`编写一份说明。那不会是一个实际的`double`类型变量，而是关于它如何构成、如何运作的定义。要创建基本数据类型的变量，需要使用声明语句。类也是如此，稍后你会看到。

## 定义类

再看一下前面提到的类示例——一个盒子的类。你使用关键字`class`定义了 CBox 数据类型，如下所示：

```
class CBox
{
    public:
        double m_Length;        // Length of a box in inches
        double m_Width;         // Width of a box in inches
        double m_Height;        // Height of a box in inches
};
```

类名出现在`class`关键字之后，三个数据成员定义在花括号之间。类中的数据成员是使用你已经熟悉并喜爱的声明语句定义的，整个类定义以分号结束。类的所有成员名称都局限于该类。因此，你可以在程序的其他地方使用相同的名称而不会引起任何问题。

## 类中的访问控制

`public`关键字看起来有点像标签，但实际上不止如此。它决定了其后类成员的访问属性。将数据成员指定为`public`，意味着类的对象的这些成员可以在它们所属的类对象作用域内的任何地方被访问。你也可以将类的成员指定为`private`或`protected`。事实上，如果完全省略访问说明，成员将具有默认属性`private`。（这是 C++ 中类与结构体的唯一区别——结构体的默认访问说明符是`public`。）稍后你将进一步了解这些关键字在类定义中的作用。

请记住，到目前为止你定义的一切只是一个类，即一种数据类型。你还没有声明任何类类型的对象。当我谈到访问类成员（比如 m_Height）时，我指的是访问某个特定对象的数据成员，而该对象需要在某处声明。

## 声明类的对象

声明类的对象所使用的声明语句，与你用来声明基本类型对象的声明完全相同。因此，你可以用下列语句声明 CBox 类类型的对象：

```
CBox box1;    // Declare box1 of type CBox
CBox box2;    // Declare box2 of type CBox
```

当然，box1 和 box2 这两个对象都拥有各自的数据成员。如图 7-4 所示。

![](img/2359b0c604600c58fba3539c738a356e_378_0.png)

对象名 box1 代表整个对象，包括它的三个数据成员。不过，它们没有被初始化为任何值——每个对象的数据成员只是包含垃圾值，因此我们需要研究如何访问它们，以便将它们设置为特定值。

## 访问类的数据成员

你可以使用访问结构体成员时所用的直接成员选择运算符来引用类对象的数据成员。因此，要把对象 box2 的数据成员 m_Height 设置为 18.0，可以编写如下赋值语句：

```
box2.m_Height = 18.0;    // Setting the value of a data member
```

你只能在类外部的函数中以这种方式访问该数据成员，因为 m_Height 成员被指定为具有 public 访问权限。如果它没有定义为 public，这条语句将无法编译。稍后你会对此有更多了解。

## 试一试　　首次使用类

验证你能否像使用结构体一样使用类。请在下面的控制台应用程序中试一试：

```
// Ex7_02.cpp
// Creating and using boxes
#include <iostream>
using std::cout;
using std::endl;

class CBox                        // Class definition at global scope
{
public:
    double m_Length;              // Length of a box in inches
    double m_Width;               // Width of a box in inches
    double m_Height;              // Height of a box in inches
};

int main()
{
    CBox box1;                    // Declare box1 of type CBox
```

```
CBox box2;                          // Declare box2 of type CBox

double boxVolume = 0.0;               // Stores the volume of a box

box1.m_Height = 18.0;                 // Define the values
box1.m_Length = 78.0;                 // of the members of
box1.m_Width = 24.0;                  // the object box1

box2.m_Height = box1.m_Height - 10;   // Define box2
box2.m_Length = box1.m_Length/2.0;    // members in
box2.m_Width = 0.25*box1.m_Length;    // terms of box1

// Calculate volume of box1
boxVolume = box1.m_Height*box1.m_Length*box1.m_Width;

cout << endl
    << "Volume of box1 = " << boxVolume;

cout << endl
    << "box2 has sides which total "
    << box2.m_Height+ box2.m_Length+ box2.m_Width
    << " inches.";

cout << endl                         // Display the size of a box in memory
    << "A CBox object occupies "
    << sizeof box1 << " bytes.";

cout <<endl;
return 0;
}
```

当你在 main() 中键入代码时，每当在类对象名后面输入成员选择运算符，编辑器都会提示一个成员名称列表。你可以双击从列表中选择所需的成员。将鼠标光标悬停在代码中的任何变量上片刻，就会显示其类型。

## 工作原理

这里我们暂时回到控制台应用程序示例，因此项目应相应定义。这里的一切都会像你从结构体的使用经验中预期的那样运作。类的定义出现在 main() 函数之外，因此具有全局作用域。这样，你就可以在程序中的任何函数里声明对象，并且程序编译后，该类会出现在“类视图（Class View）”选项卡中。

你在 main() 函数中声明了两个 CBox 类型的对象 box1 和 box2。当然，与基本类型的变量一样，box1 和 box2 是 main() 的局部对象。类类型的对象在作用域方面遵循与基本类型变量（例如本例中使用的 boxVolume 变量）相同的规则。

前三条赋值语句设置了 box1 的数据成员的值。接下来的三条赋值语句根据 box1 的数据成员定义了 box2 的数据成员的值。

