

## 重载加法运算符

让我们研究一下为 CBox 类重载加法运算符。这很有趣，因为它涉及创建并返回一个新对象。新对象是其两个操作数 CBox 对象之和（无论你如何定义这个“和”的含义）。

那么我们希望两个盒子的和表示什么呢？嗯，有很多合理的可能性，但这里我们保持简单。我们将两个 CBox 对象的和定义为一个足够大的 CBox 对象，能够容纳另外两个盒子叠放在一起。可以采用这样的方式：新对象的 m_Length 成员取所相加的两个对象中较大的 m_Length 成员，m_Width 成员以类似方式得到。m_Height 成员是两个操作数对象的 m_Height 成员之和，这样生成的 CBox 对象可以容纳另外两个 CBox 对象。这不一定是较优的解决方案，但足以满足我们的目的。通过修改构造函数，我们还将使 CBox 对象的 m_Length 成员始终大于或等于 m_Width 成员。

我们为盒子定义的加法运算用图形解释起来更容易，因此如图 8-4 所示。

![](img/2359b0c604600c58fba3539c738a356e_464_0.png)

## 第 8 章

因为需要直接访问对象的成员，所以将 `operator+()` 设为成员函数。类定义中该函数成员的声明如下：

```
CBox operator+(const CBox& aBox) const;  // Function adding two CBox objects
```

将参数定义为引用是为了避免在调用函数时不必要的复制右参数，同时将其设为 const 引用，因为该函数不会修改参数。如果不将参数声明为 const 引用，编译器将不允许向函数传递 const 对象，这样 + 的右操作数就不可能是 const CBox 对象。还应将函数声明为 const，因为它不会改变调用它的对象。否则，+ 的左操作数就不能是 const CBox 对象。

现在，`operator+()` 函数的定义如下：

```
// Function to add two CBox objects
CBox CBox::operator+(const CBox& aBox) const
{
    // New object has larger length and width, and sum of heights
    return CBox(m_Length > aBox.m_Length ? m_Length:aBox.m_Length,
                m_Width > aBox.m_Width ? m_Width:aBox.m_Width,
                m_Height + aBox.m_Height);
}
```

你可以从当前对象（`*this`）和作为参数传入的对象 aBox 构造一个局部 CBox 对象。请记住，返回过程会生成该局部对象的临时副本，并将该副本传回调用函数，而不是在函数返回时丢弃的局部对象。

## 试一试 —— 练习我们的加法

在这个示例中，你将能够看到 CBox 类中重载的加法运算符是如何工作的：

```
// Ex8_06.cpp
// Adding CBox objects
#include <iostream>                    // For stream I/O
using std::cout;
using std::endl;

class CBox                              // Class definition at global scope
{
public:
    // Constructor definition
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0): m_Height(hv)
    {
        m_Length = lv > wv? lv: wv;     // Ensure that
        m_Width = wv < lv? wv: lv;      // length >= width
    }

    // Function to calculate the volume of a box
    double Volume() const
    {
        return m_Length*m_Width*m_Height;
    }

    // Operator function for 'greater than' which
```

## 关于类的更多内容

```
// compares volumes of CBox objects.
int CBox::operator>(const CBox& aBox) const
{
    return this->Volume() > aBox.Volume();
}

// Function to compare a CBox object with a constant
int operator>(const double& value) const
{
    return Volume() > value;
}
```

```
// Function to add two CBox objects
CBox operator+(const CBox& aBox) const
{
    // New object has larger length & width, and sum of heights
    return CBox(m_Length > aBox.m_Length? m_Length:aBox.m_Length,
                m_Width > aBox.m_Width? m_Width:aBox.m_Width,
                m_Height + aBox.m_Height);
}

// Function to show the dimensions of a box
void ShowBox() const
{
    cout << m_Length << " "
         << m_Width << " "
         << m_Height << endl;
}
```

```
private:
    double m_Length;                    // Length of a box in inches
    double m_Width;                     // Width of a box in inches
    double m_Height;                    // Height of a box in inches
};

int operator>(const double& value, const CBox& aBox); // Function prototype

int main()
{
    CBox smallBox(4.0, 2.0, 1.0);
    CBox mediumBox(10.0, 4.0, 2.0);
    CBox aBox;
    CBox bBox;

    aBox = smallBox + mediumBox;
    cout << "aBox dimensions are ";
    aBox.ShowBox();

    bBox = aBox + smallBox + mediumBox;
    cout << "bBox dimensions are ";
    bBox.ShowBox();

    return 0;
}

// Function comparing a constant with a CBox object
```

## 关于类的更多内容

```
const Length operator++(int); // Postfix increment operator
Length& operator--(); // Prefix decrement operator
const Length operator--(int); // Postfix decrement operator
// rest of the class...
```

这个简单的类假定长度仅以 double 类型的值存储。在实际中，你可能会让 length 类比这里更复杂，但它足以说明如何重载自增和自减运算符。

重载运算符的前缀形式和后缀形式主要通过参数列表来区分；前缀形式没有参数，后缀形式有一个 int 类型的参数。后缀运算符函数中的参数仅用于与前缀形式区分，在函数实现中不再使用。

前缀自增和自减运算符会在操作数的值用于表达式之前递增该操作数，因此你只需在自增或自减后返回对当前对象的引用。对于后缀形式，操作数是在其当前值用于表达式之后才递增。实现方式是：在递增当前对象之前，创建一个当前对象的副本，然后在当前对象被修改后返回该副本。

## 类模板

在第 6 章中你已经看到，可以定义函数模板，它会自动生成在接受的参数类型或返回值类型上有所不同的函数。C++ 也有类似的机制用于类。类模板本身并不是一个类；它更像是类的“配方”，由编译器用来生成类的代码。正如你在图 8-5 中看到的，它类似于函数模板——通过指定模板中的尖括号之间出现的参数（这里为 T）的类型选择，你确定要生成的类。这样做会生成一个特定的类，称为类模板的实例。从模板创建类的过程称为实例化模板。

当为特定类型实例化模板类的对象时，会生成相应的类定义，这样你就可以从一个类模板生成任意数量的不同类。通过查看一个示例，你将很好地了解这在实践中是如何工作的。

## 定义类模板

我会选择一个简单的例子来说明如何定义和使用类模板，并且我不会因为担心误用可能引发的错误而把事情复杂化。假设你想定义一个可以存储某种数据样本的类，并且每个类都要提供一个 Max() 函数来确定所存储样本的最大值。这个函数类似于你在第 6 章函数模板讨论中看到的那个。你可以定义一个类模板，它会生成一个 CSamples 类，用于存储你想要的任何类型的样本。

图 8-5

![](img/2359b0c604600c58fba3539c738a356e_469_0.png)

```
template <class T>
class CSamples
{
    public:
        // Constructor definition to accept an array of samples
        CSamples(const T values[], int count)
        {
            m_Free = count < 100? count:100; // Don't exceed the array
            for(int i = 0; i < m_Free; i++)
                m_Values[i] = values[i];      // Store count number of samples
        }

        // Constructor to accept a single sample
        CSamples(const T& value)
        {
            m_Values[0] = value;            // Store the sample
```

