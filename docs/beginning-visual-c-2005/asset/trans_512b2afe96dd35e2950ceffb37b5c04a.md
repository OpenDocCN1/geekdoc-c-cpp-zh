

## 类继承与虚函数

```cpp
cout << endl << "CBox copy constructor called";
m_Length = initB.m_Length;
m_Width = initB.m_Width;
m_Height = initB.m_Height;
}
```

```cpp
// CBox destructor - just to track calls
~CBox()
{ cout << "CBox destructor called" << endl; }

protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

还请记住，拷贝构造函数必须将其参数指定为引用，以避免自身被无限次调用，这本应由按值传递参数所需复制而导致。当我们的示例中的拷贝构造函数被调用时，它会向屏幕输出一条消息，因此你能从输出中看到何时发生了这种情况。

我们将使用来自 Ex9_04.cpp 的 CCandyBox 类版本，如下再次所示：

```cpp
// CandyBox.h in Ex9_05
#pragma once
#include "Box.h"
#include <iostream>
using std::cout;
using std::endl;

class CCandyBox: public CBox
{
public:
    char* m_Contents;

    // Derived class function to calculate volume
    double Volume() const
    { return m_Length*m_Width*m_Height; }

    // Constructor to set dimensions and contents
    // with explicit call of CBox constructor
    CCandyBox(double lv, double wv, double hv, char* str = "Candy")
        :CBox(lv, wv, hv)  // Constructor
    {
        cout << endl <<"CCandyBox constructor2 called";
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    // Constructor to set contents
    // calls default CBox constructor automatically
    CCandyBox(char* str = "Candy")           // Constructor
    {
        cout << endl << "CCandyBox constructor1 called";
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    ~CCandyBox()                         // Destructor
    {
        cout << "CCandyBox destructor called" << endl;
        delete[] m_Contents;
    };
};
```

它还没有添加拷贝构造函数，因此你将依赖编译器生成的版本。

### 试一试    派生类中的拷贝构造函数

你可以用以下示例来测试刚刚定义的拷贝构造函数：

```cpp
// Ex9_05.cpp
// Using a derived class copy constructor
#include <iostream>                // For stream I/O
#include <cstring>                 // For strlen() and strcpy()
#include "CCandyBox.h"             // For CBox and CCandyBox
using std::cout;
using std::endl;

int main()
{
    CCandyBox chocBox(2.0, 3.0, 4.0, "Chockies");  // Declare and initialize
    CCandyBox chocolateBox(chocBox);               // Use copy constructor

    cout << endl
         << "Volume of chocBox is " << chocBox.Volume()
         << endl
         << "Volume of chocolateBox is " << chocolateBox.Volume()
         << endl;

    return 0;
}
```

### 它是如何工作的（或为什么不起作用）

当你运行此示例的 Debug 版本时，除了预期的输出外，你还会看到图 9-4 所示的对话框。

点击 Abort 以清除对话框，你将在控制台窗口中看到你可能期望的输出。输出显示编译器生成的派生类拷贝构造函数自动调用了基类的拷贝构造函数。

![](img/2359b0c604600c58fba3539c738a356e_534_0.png)

图 9-4

然而，正如你可能已经意识到的那样，一切并非如预期。在这种特定情况下，编译器生成的拷贝构造函数导致了问题，因为第二个声明的对象中派生类的 m_Contents 成员指向的内存与第一个对象中的内存相同。当一个对象被销毁（在 main() 结束时超出作用域）时，它会释放文本占用的内存。当第二个对象被销毁时，析构函数尝试释放已被前一个对象的析构函数调用释放的内存——这就是对话框中错误消息的原因。

解决办法是为派生类提供一个拷贝构造函数，为新对象分配额外的内存。

### 试一试   修复拷贝构造函数问题

你可以通过向 Ex9_05 中派生 CCandyBox 类的 public 部分添加以下拷贝构造函数代码来实现：

```cpp
// Derived class copy constructor
CCandyBox(const CCandyBox& initCB)
{
    cout << endl << "CCandyBox copy constructor called";

    // Get new memory
    m_Contents = new char[ strlen(initCB.m_Contents) + 1 ];

    // Copy string
    strcpy_s(m_Contents, strlen(initCB.m_Contents) + 1, initCB.m_Contents);
}
```

现在你可以用相同的 function main() 运行这个新版本的最后一个示例，看看新的拷贝构造函数如何工作。

### 它是如何工作的

现在运行示例时，它表现更好并产生以下输出：

```text
CBox constructor called
CCandyBox constructor2 called
CBox constructor called
CCandyBox copy constructor called
Volume of chocBox is 24
Volume of chocolateBox is 1
CCandyBox destructor called
CBox destructor called
CCandyBox destructor called
CBox destructor called
```

然而，仍然存在问题。输出的第三行显示，chocolateBox 对象的 CBox 部分的默认构造函数被调用，而不是拷贝构造函数。因此，该对象具有默认尺寸而非初始化对象的尺寸，所以体积不正确。其原因是，当你为派生类对象编写构造函数时，你有责任确保派生类对象的成员得到正确初始化。这包括继承的成员。

修复方法是，在 CCandyBox 类的拷贝构造函数的初始化列表中调用基类部分的拷贝构造函数。拷贝构造函数于是变为：

```cpp
// Derived class copy constructor
CCandyBox(const CCandyBox& initCB): CBox(initCB)
{
    cout << endl << "CCandyBox copy constructor called";

    // Get new memory
    m_Contents = new char[ strlen(initCB.m_Contents) + 1 ];

    // Copy string
    strcpy_s(m_Contents, strlen(initCB.m_Contents) + 1, initCB.m_Contents);
}
```

现在 CBox 类的拷贝构造函数会使用 initCB 对象调用。只将其基类部分传递给它，因此一切正常。如果你在最后一个示例中添加基类拷贝构造函数调用，输出如下：

```text
CBox constructor called
CCandyBox constructor2 called
CBox copy constructor called
CCandyBox copy constructor called
Volume of chocBox is 24
Volume of chocolateBox is 24
CCandyBox destructor called
CBox destructor called
CCandyBox destructor called
CBox destructor called
```

输出显示所有构造函数和析构函数都按正确顺序调用，且 chocolateBox 的 CBox 部分的拷贝构造函数在 CCandyBox 拷贝构造函数之前被调用。派生类对象 chocolateBox 的体积现在与其初始化对象相同，这才是应有的结果。

因此，你需要记住另一条黄金法则：

> 如果你为派生类编写任何类型的构造函数，你就有责任初始化派生类对象的所有成员，包括其所有继承的成员。

## 类成员作为友元

你在第 7 章中看到如何将函数声明为类的友元。这赋予友元函数访问任何类成员的特权。当然，没有理由说友元函数不能是另一个类的成员。

假设你定义一个 CBottle 类来表示一个瓶子：

```cpp
class CBottle
{
public:
    CBottle(double height, double diameter)
    {
        m_Height = height;
        m_Diameter = diameter;
    }

private:
    double m_Height;            // Bottle height
    double m_Diameter;          // Bottle diameter
};
```

你现在需要一个类来表示一打瓶子的包装，其尺寸会自动定制以容纳特定种类的瓶子。你可以将其定义为：

```cpp
class CCarton
{
public:
    CCarton(const CBottle& aBottle)
    {
        m_Height = aBottle.m_Height;        // Bottle height
        m_Length = 4.0*aBottle.m_Diameter;  // Four rows of ...
        m_Width = 3.0*aBottle.m_Diameter;   // ...three bottles
    }

private:
    double m_Length;    // Carton length
    double m_Width;     // Carton width
    double m_Height;    // Carton height
};
```

