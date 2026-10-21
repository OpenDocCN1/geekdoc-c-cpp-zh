

现在你已经定义了尺寸为 3x5x8 的标准盒子，你不想让它被随意修改。特别是，你不想允许其数据成员中存储的值被更改。你怎么能确定它们不会被更改呢？

好吧，你已经可以确定了。如果你将一个类的对象声明为 const，编译器将不允许调用任何可能修改它的成员函数。你可以通过修改前一个示例中对象 cigar 的声明来很容易地证明这一点，改为：

```
const CBox cigar(8.0, 5.0,1.0);      // Declare cigar box
```

如果你尝试用此更改重新编译程序，它将无法编译。你会看到错误信息：

```
error C2662: 'compare' : cannot convert 'this' pointer from 'const class CBox' to 'class CBox &'      Conversion loses qualifiers
```

这是对调用 cigar 的 Compare() 成员的 if 语句产生的。你声明为 const 的对象将始终具有 const 的 this 指针，因此编译器不会允许调用任何不假设传递给它的 this 指针为 const 的成员函数。你需要找出如何使成员函数中的 this 指针为 const。

## 类的 const 成员函数

要使成员函数中的 this 指针为 const，你必须在类定义内将该函数声明为 const。看看你如何用 CBox 的 Compare() 成员来做到这一点。类定义需要修改为以下内容：

```
class CBox                                 // Class definition at global scope
{
public:
    // Constructor definition
    CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0)
    {
        cout << endl << "Constructor called.";
        m_Length = lv;                      // Set values of
        m_Width = bv;                       // data members
        m_Height = hv;
    }

    // Function to calculate the volume of a box
    double Volume()
    {
        return m_Length*m_Width*m_Height;
    }

    // Function to compare two boxes which returns true (1)
    // if the first is greater than the second, and false (0) otherwise
    int Compare(CBox xBox) const
    {
        return this->Volume() > xBox.Volume();
    }

private:
```

```
double m_Length;              // Length of a box in inches
double m_Width;               // Width of a box in inches
double m_Height;              // Height of a box in inches
};
```

要指定一个成员函数为 const，你只需在函数头后附加 const 关键字。请注意，你只能对类成员函数这样做，而不能对普通的全局函数这样做。将函数声明为 const 只有在该函数是类的成员时才有意义。其效果是使函数中的 this 指针为 const，这反过来意味着你不能在函数定义内将类的一个数据成员写在赋值号的左侧；它将被编译器标记为错误。const 成员函数不能调用同一类的非 const 成员函数，因为这可能会修改对象。

当你将一个对象声明为 const 时，你为其调用的成员函数必须声明为 const；否则程序将无法编译。

## 类外部的成员函数定义

当 const 成员函数的定义出现在类外部时，定义的头必须添加 const 关键字，就像类内的声明一样。事实上，你应该始终将所有不修改其被调用的类对象的成员函数声明为 const。考虑到这一点，CBox 类可以定义为：

```
class CBox                     // Class definition at global scope
{
public:
    // Constructor
    CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0);

    double Volume() const;       // Calculate the volume of a box
    int Compare(CBox xBox) const; // Compare two boxes

private:
    double m_Length;             // Length of a box in inches
    double m_Width;              // Width of a box in inches
    double m_Height;             // Height of a box in inches
};
```

这假设所有成员函数都是单独定义的，包括构造函数。Volume() 和 Compare() 成员都已声明为 const。Volume() 函数现在在类外定义为：

```
double CBox::Volume() const
{
    return m_Length*m_Width*m_Height;
}
```

Compare() 函数的定义是：

```
int CBox::Compare(CBox xBox) const
{
    return this->Volume() > xBox.Volume();
}
```

正如你所见，const 修饰符出现在两个定义中。如果你省略它，代码将无法编译。带有 const 修饰符的函数与不带 const 修饰符的函数是不同的，即使名称和参数完全相同。事实上，你可以在一个类中同时拥有 const 和非 const 版本的函数，有时这非常有用。

按所示声明类时，构造函数也需要单独定义，像这样：

```
CBox::CBox(double lv, double bv, double hv):
    m_Length(lv), m_Width(bv), m_Height(hv)
{
    cout << endl << "Constructor called.";
}
```

## 类对象的数组

你可以以声明普通数组的方式声明类对象的数组，其中元素是内置类型之一。类对象数组的每个元素都会导致调用默认构造函数。

### 试试看 类对象的数组

我们可以使用上一个示例中的 CBox 类定义，但修改为包含特定的默认构造函数：

```
// Ex7_11.cpp
// Using an array of class objects
#include <iostream>
using std::cout;
using std::endl;

class CBox                         // Class definition at global scope
{
public:
    // Constructor definition
    CBox(double lv, double bv = 1.0, double hv = 1.0)
    {
        cout << endl << "Constructor called.";
        m_Length = lv;                 // Set values of
        m_Width = bv;                  // data members
        m_Height = hv;
    }

    CBox()                           // Default constructor
    {
        cout << endl
             << "Default constructor called.";
        m_Length = m_Width = m_Height = 1.0;
    }

    // Function to calculate the volume of a box
    double Volume() const
    {
```

```
return m_Length*m_Width*m_Height;
}

private:
    double m_Length;                // Length of a box in inches
    double m_Width;                 // Width of a box in inches
    double m_Height;                // Height of a box in inches

};

int main()
{
```

```
CBox boxes[5];                    // Array of CBox objects declared
CBox cigar(8.0, 5.0, 1.0);         // Declare cigar box

cout << endl
    << "Volume of boxes[3] = " << boxes[3].Volume()
    << endl
    << "Volume of cigar = " << cigar.Volume();

cout << endl;
return 0;
```

该程序产生以下输出：

```
Default constructor called.
Default constructor called.
Default constructor called.
Default constructor called.
Default constructor called.
Constructor called.
Volume of boxes[3] = 1
Volume of cigar = 40
```

## 它是如何工作的

你已修改了接受参数的构造函数，使其只提供两个默认值，并添加了一个默认构造函数，在显示已调用的消息后将数据成员初始化为 1。你现在可以看到何时调用了哪个构造函数。构造函数现在具有相当不同的参数列表，因此编译器不可能混淆它们。

从输出可以看出，默认构造函数被调用了五次，每次对应 boxes 数组的一个元素。另一个构造函数被调用来创建 cigar 对象。从输出可以清楚地看出，默认构造函数初始化工作正常，因为数组元素的体积为 1。

## 类的静态成员

类的成员数据和成员函数都可以声明为 static。由于上下文是类定义，其效果比类外部的 static 关键字要复杂一些，所以让我们先看看静态数据成员。

