

```
private:
    double m_Length;                // Length of a box in inches
    double m_Width;                 // Width of a box in inches
    double m_Height;                // Height of a box in inches
};
```

```
// Operator function for 'greater than' that
// compares volumes of CBox objects.
bool CBox::operator>(const CBox& aBox) const
{
    return this->Volume() > aBox.Volume();
}

int main()
{
    CBox smallBox(4.0, 2.0, 1.0);
    CBox mediumBox(10.0, 4.0, 2.0);
    CBox bigBox(30.0, 20.0, 40.0);

    if(mediumBox > smallBox)
        cout << endl
            << "mediumBox is bigger than smallBox";

    if(mediumBox > bigBox)
        cout << endl
            << "mediumBox is bigger than bigBox";
    else
        cout << endl
            << "mediumBox is not bigger than bigBox";

    cout << endl;
    return 0;
}
```

## 如何工作

operator>() 运算符函数的原型出现在类的 public 部分。由于函数定义在类定义之外，因此它不会默认内联。这相当随意。你完全可以把定义放在类定义中的原型位置。在这种情况下，你就不需要用 CBox:: 来限定函数名。正如你所记得的，当一个成员函数在类定义之外定义时，需要这样做，以告诉编译器该函数是类 CBox 的成员。

函数 main() 有两个使用运算符 > 和类成员的 if 语句。这些会自动调用我们重载的运算符。如果你想确认这一点，可以在运算符函数中添加输出语句。此示例的输出为：

```
Constructor called.
Constructor called.
Constructor called.
mediumBox is bigger than smallBox
mediumBox is not bigger than bigBox
Destructor called.
Destructor called.
Destructor called.
```

输出表明 if 语句与我们的运算符函数配合良好，因此能够直接以 CBox 对象表示 CBox 问题的解决方案开始变得切实可行。

## 实现运算符的完整支持

使用我们的运算符函数 operator>(), 仍然有很多事情做不到。以 CBox 对象表示问题解决方案可能涉及如下语句：

```
if(aBox > 20.0)
    // Do something...
```

我们的函数无法处理这种情况。如果你尝试使用比较 CBox 对象与数值值的表达式，你会收到错误信息。为了支持这种能力，你需要以重载函数的形式编写 operator>() 函数的另一个版本。

你很容易就能支持刚刚看到的那种表达式。类内的成员函数声明为：

```
// Compare a CBox object with a constant
bool operator>(const double& value) const;
```

这将出现在类的定义中，而 > 运算符的右操作数对应于这里的函数参数。左操作数的 CBox 对象作为隐式指针 this 传递。

这个重载运算符的实现也很简单。函数体中只有一个语句：

```
// Function to compare a CBox object with a constant
bool CBox::operator>(const double& value) const
{
  return this->Volume() > value;
}
```

这不能更简单了，对吧？但你仍然在使用 > 运算符与 CBox 对象时遇到问题。你可能希望编写如下语句：

```
if(20.0 > aBox)
    // do something...
```

你可以争辩说这可以通过实现接受右参数为 double 类型的 operator<() 运算符函数并重写上面的语句来使用它，这完全正确。事实上，实现 < 运算符很可能也是比较 CBox 对象的需求，但对对象类型的支持不应人为限制你在表达式中使用对象的方式。对象的使用应尽可能自然。问题是如何做到这一点。

成员运算符函数始终将左参数作为指针 this 提供。由于这里的左参数类型为 double，你无法将其实现为成员函数。这就给你留下了两个选择：普通函数或友元函数。由于你不需要访问类的私有成员，因此它不必是友元函数，所以你可以用普通函数实现左操作数为 double 类型的重载 > 运算符。原型放在类定义之外，当然，因为它不是成员，是：

```
bool operator>(const double& value, const CBox& aBox);
```

实现为：

```
// Function comparing a constant with a CBox object
bool operator>(const double& value, const CBox& aBox)
{
    return value > aBox.Volume();
}
```

正如你已经看到的，普通函数（以及友元函数也是如此）通过使用直接成员选择运算符和对象名来访问对象的成员。当然，普通函数只能访问公共成员。成员函数 Volume() 是公共的，所以在这里使用它没有任何问题。

如果类没有公共函数 Volume()，你可以使用可以访问私有数据成员的友元函数，或者你可以提供一组返回私有数据成员值的成员函数，并在普通函数中使用它们来实现比较。

## 试试看 完全重载 > 运算符

我们可以把这一切放在一个示例中来展示其工作原理：

```
// Ex8_04.cpp
// Implementing a complete overloaded 'greater than' operator
#include <iostream>                    // For stream I/O
using std::cout;
using std::endl;

class CBox                            // Class definition at global scope
{
public:
    // Constructor definition
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv)
    {
        cout << endl << "Constructor called.";
    }

    // Function to calculate the volume of a box
double Volume() const
{
    return m_Length*m_Width*m_Height;
}
```

```
// Operator function for 'greater than' that
// compares volumes of CBox objects.
bool operator>(const CBox& aBox) const
{
    return this->Volume() > aBox.Volume();
}

// Function to compare a CBox object with a constant
bool operator>(const double& value) const
{
    return this->Volume() > value;
}
```

```
// Destructor definition
~CBox()
{ cout << "Destructor called." << endl;}

private:
    double m_Length;            // Length of a box in inches
    double m_Width;             // Width of a box in inches
    double m_Height;            // Height of a box in inches
};
```

```
int operator>(const double& value, const CBox& aBox); // Function prototype
```

```
int main()
{
    CBox smallBox(4.0, 2.0, 1.0);
    CBox mediumBox(10.0, 4.0, 2.0);

    if(mediumBox > smallBox)
        cout << endl
             << "mediumBox is bigger than smallBox";

if(mediumBox > 50.0)
    cout << endl
         << "mediumBox capacity is more than 50";
else
    cout << endl
         << "mediumBox capacity is not more than 50";

if(10.0 > smallBox)
    cout << endl
         << "smallBox capacity is less than 10";
else
    cout << endl
         << "smallBox capacity is not less than 10";

cout << endl;

return 0;
}
```

```
// Function comparing a constant with a CBox object
int operator>(const double& value, const CBox& aBox)
{
    return value > aBox.Volume();
}
```

## 如何工作

注意 operator>() 的普通函数版本原型的放置位置。它需要在类定义之后，因为它在参数列表中引用了 CBox 对象。如果你把它放在类定义之前，示例将无法编译。

有一种方法可以把它放在程序文件开头 #include 语句之后：使用不完整的类声明。这将位于原型之前，看起来像这样：

```
class CBox;                     // Incomplete class declaration
int operator>(const double& value, CBox& aBox);  // Function prototype
```

不完整的类声明将 CBox 标识为类，足以让编译器正确处理函数的原型，因为编译器现在知道 CBox 是稍后指定的用户定义类型。

这种机制在诸如两个类各自将另一个类的对象指针作为成员的情况中也是必不可少的。它们各自需要对方先声明。通过使用不完整的类声明，可以解决这种僵局。

示例的输出为：

```
Constructor called.
Constructor called.
mediumBox is bigger than smallBox
mediumBox capacity is more than 50
smallBox capacity is less than 10
Destructor called.
Destructor called.
```

在由于 smallBox 和 mediumBox 对象的声明而产生的构造函数消息之后，你有来自三个 if 语句的输出行，每个都按预期工作。其中第一个调用的是类成员的运算符函数，处理两个 CBox 对象。第二个调用的是参数类型为 double 的成员函数。第三个 if 语句中的表达式调用的是你作为普通函数实现的运算符函数。

碰巧的是，你本可以将两个是类成员的运算符函数都做成普通函数，因为它们只需要访问公共的成员函数 Volume()。

> 任何比较运算符都可以以与你实现这些运算符相同的方式实现。它们只会在细节上有所不同，实现它们的总体方法完全相同。

