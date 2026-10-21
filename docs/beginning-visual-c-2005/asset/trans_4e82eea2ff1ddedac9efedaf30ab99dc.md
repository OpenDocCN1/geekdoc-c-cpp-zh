

## 类继承与虚函数

```cpp
// 调用基类构造函数
CCandyBox(double lv, double wv, double hv, char* str = "Candy"):
CBox(lv, wv, hv)
{
    ...
}
```

这与您在此处所做的事情完全一致，因为您本质上是在初始化派生类对象中的一个 CBox 子对象。在第一种情况下，您是在初始化列表中显式调用 double 型成员 m_Length、m_Width 和 m_Height 的默认构造函数。在第二种情况下，您是在调用 CBox 的构造函数。这将导致在 CCandyBox 构造函数执行之前，调用您所选择的那个特定的 CBox 构造函数。

如果您构建并运行此示例，它将产生如下所示的输出：

```
CBox constructor called
CBox constructor called
CBox constructor1 called
CBox constructor called
CBox constructor2 called
myBox occupies 24 bytes
myCandyBox occupies 32 bytes
myMintBox occupies 32 bytes
myMintBox volume is 6
```

| 屏幕输出 | 正在构造的对象 |
|---------------|-------------------------|
| CBox constructor called | MyBox |
| CBox constructor called | MyCandyBox |
| CBox constructor1 called | MyCandyBox |
| CBox constructor called | MyMintBox |
| CBox constructor2 called | MyMintBox |

输出的第一行源于 CBox 类构造函数的调用，该调用来自 CBox 对象 myBox 的声明。第二行输出来自于 CCandyBox 对象 myCandyBox 的声明所引发的基类构造函数的自动调用。

> *请注意，基类构造函数总是在派生类构造函数之前被调用。*

下面一行是由于您为 myCandyBox 对象调用了自定义的默认派生类构造函数。由于该对象未被初始化，所以调用了这个构造函数。第四行输出源于我们在新的 CCandyBox 对象构造函数中显式指定要调用的 CBox 类构造函数。为 CCandyBox 对象指定的尺寸参数值会被传递给基类构造函数。接下来是新的派生类构造函数自身的输出，因此同样是先调用基类构造函数，然后再调用派生类构造函数。

从您目前所看到的内容中应该能清楚地了解到：当派生类构造函数执行时，总是会调用基类构造函数来构造派生类对象中的基类部分。如果您未指定要使用的基类构造函数，编译器会安排调用默认的基类构造函数。

表格中的最后一行表明，myMintBox 对象基类部分的初始化工作正常，私有成员已由 CBox 类构造函数初始化完毕。

基类的私有成员只能由基类的函数成员访问，这有时并不方便。在很多情况下，您希望基类的某些私有成员能够从派生类内部进行访问。正如您可能已经预料到的，C++ 提供了一种实现方式。

## 声明类成员为 protected

除了类的 public 和 private 访问说明符之外，您还可以将类的成员声明为 protected。在类内部，protected 关键字与 private 关键字具有相同的效果：类的 protected 成员只能由该类的成员函数以及该类的友元函数访问（也可以由声明为该类友元的类的成员函数访问——您将在本章后面了解友元类）。使用 protected 关键字，您可以按如下方式重新定义 CBox 类：

```cpp
// Box.h in Ex9_04
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox
{
public:
    // 基类构造函数
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv)
    { cout << endl << "CBox constructor called"; }
```

```cpp
// CBox 析构函数——仅用于跟踪调用
~CBox()
{ cout << "CBox destructor called" << endl; }
```

```cpp
protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

现在，这些数据成员实际上仍然是私有的，因为普通全局函数无法访问它们，但它们仍然可以被派生类的成员函数访问。

## 试一试  使用 protected 成员

您可以通过使用这个版本的 CBox 类来演示 protected 数据成员的用法，派生一个新版本的 CCandyBox 类，该类通过自己的成员函数 Volume() 访问基类的成员：

```cpp
// CandyBox.h in Ex9_04
#pragma once
#include "Box.h"
#include <iostream>
using std::cout;
using std::endl;

class CCandyBox: public CBox
{
public:
    char* m_Contents;

    // 派生类函数，用于计算体积
    double Volume() const
    { return m_Length*m_Width*m_Height; }

    // 构造函数，设置尺寸和内容
    // 显式调用 CBox 构造函数
    CCandyBox(double lv, double wv, double hv, char* str = "Candy")
        :CBox(lv, wv, hv)  // 构造函数
    {
        cout << endl <<"CCandyBox constructor2 called";
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    // 构造函数，设置内容
    // 自动调用默认的 CBox 构造函数
    CCandyBox(char* str = "Candy")                 // 构造函数
    {
        cout << endl << "CCandyBox constructor1 called";
        m_Contents = new char[ strlen(str) + 1 ];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    ~CCandyBox()                                 // 析构函数
    {
        cout << "CCandyBox destructor called" << endl;
        delete[] m_Contents;
    }
};
```

Ex9_04.cpp 中 main() 的代码如下：

```cpp
// Ex9_04.cpp
// 使用 protected 访问说明符
#include <iostream>                 // 用于流式 I/O
```

```cpp
error C2248: 'm_Length' : cannot access protected member declared in class 'CBox'
```

这非常清楚地表明成员 m_Length 是不可访问的。

## 继承类成员的访问级别

您已经知道，如果在派生类的定义中没有为基类指定访问说明符，则默认的说明符是 private。这会导致基类中被继承的 public 和 protected 成员在派生类中变成 private。基类的 private 成员仍然保持对基类私有，因此派生类的成员函数无法访问它们。实际上，无论基类在派生类定义中如何指定，它们都保持对基类私有。

您还曾经使用过 public 作为基类的说明符。这会使基类的成员在派生类中的访问级别与在基类中的访问级别相同，因此 public 成员保持 public，protected 成员保持 protected。

最后一种可能性是将基类声明为 protected。这会使基类中被继承的 public 成员在派生类中变为 protected。protected（以及 private）继承成员在派生类中保持其原有的访问级别。图 9-3 对此进行了总结。

![](img/2359b0c604600c58fba3539c738a356e_530_0.png)

图 9-3

这可能看起来有点复杂，但您可以将其归结为关于派生类继承成员的以下三点：

- 在基类中声明为 `private` 的成员在派生类中永远不可访问。
- 将基类定义为 `public` 不会改变其成员在派生类中的访问级别。
- 将基类定义为 `protected` 会使其 `public` 成员在派生类中变为 `protected`。

能够在派生类中更改继承成员的访问级别给您带来了一定程度的灵活性，但请不要忘记，您不能放宽在基类中指定的访问级别；您只能使访问级别更加严格。这提示我们，如果您希望在派生类中能够改变访问级别，您的基类需要包含 `public` 成员。这似乎与将数据封装在类中以保护其免受未授权访问的想法相悖，但正如您将看到的，我们通常会将基类定义成这样的方式：它们的唯一目的是作为其他类的基类，而不打算用它们自身来实例化对象。

## 派生类中的复制构造函数

请记住，当您声明一个用同类的另一个对象来初始化的对象时，复制构造函数会被自动调用。请看下面的语句：

```cpp
CBox myBox(2.0, 3.0, 4.0);          // 调用构造函数
CBox copyBox(myBox);                // 调用复制构造函数
```

第一条语句调用接受三个 `double` 类型参数的构造函数，第二条语句调用复制构造函数。如果您不提供自己的复制构造函数，编译器会提供一个，它将初始化对象的成员逐个复制到新对象的对应成员中。为了在程序执行期间能够看到发生了什么，您可以为 CBox 类添加一个自己的复制构造函数版本。然后，您可以将此类作为基类来定义 CCandyBox 类。

```cpp
// Box.h in Ex9_05
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox                         // 基类定义
{
public:
    // 基类构造函数
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv)
    { cout << endl << "CBox constructor called"; }

    // 复制构造函数
    CBox(const CBox& initB)
    {
```

