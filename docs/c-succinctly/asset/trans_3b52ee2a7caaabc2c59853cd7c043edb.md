

还有一种定义内联成员函数的方法。如果你希望类定义保持整洁，不在其中包含成员函数定义，但仍想拥有一些内联成员函数，可以改为类似下面的做法：

### 示例：SimpleClassSample\Vehicle.h（备用代码在文件底部被注释掉）

```cpp
#pragma once
#include <string>

namespace Inventory
{
    enum class VehicleCondition;

    class Vehicle
    {
    public:
        Vehicle(
            VehicleCondition condition,
            double pricePaid
        );

        ~Vehicle(void);

        inline VehicleCondition GetVehicleCondition(void);

        void SetVehicleCondition(VehicleCondition condition);

        inline double GetBasis(void);

    private:
        VehicleCondition                 m_condition;
        double                           m_basis;
    };

    VehicleCondition Vehicle::GetVehicleCondition(void)
    {
        return m_condition;
    }

    double Vehicle::GetBasis(void)
    {
        return m_basis;
    }
}
```

如你所见，在类声明之后，我们定义了希望内联的成员函数，就像它们在源文件中一样。关键区别在于，类中的函数声明前有 `inline` 关键字，而函数定义位于头文件本身。如果省略该关键字，就会得到如图 1 所示的链接器错误。

![](img/e4d68f5a79326a8404dad75080806b64_36_0.png)

*图 1：省略 `Vehicle::GetVehicleCondition` 成员函数上的 `inline` 关键字后的结果。*

顺便说一句，链接器错误看起来总是很糟糕。原因是链接器不再知道你的变量和函数在源文件中的名称。它只知道编译器为了确保所有名称唯一而将这些名称转换成了什么。这包括重载方法，它们在链接阶段需要唯一名称，以便链接器能将重载成员函数的调用连接到该函数的正确重载版本。

图 1 中的错误只是告诉我们，我们多次定义了 `Inventory::Vehicle::GetVehicleCondition(void)`。现在，我们知道只定义了一次，而且就在头文件中，但我们在 **SimpleClassSample** 项目的 **Vehicle.cpp** 和 **Main.cpp** 中都包含了该头文件。

由于我们有意忘记在 `Vehicle::GetVehicleCondition` 函数声明中添加 `inline` 关键字，编译器不会将代码内联。相反，它会在 **Main.cpp** 和 **Vehicle.cpp** 中都将其编译为一个函数。

当然，编译器对此没有问题，因为它将每个源文件视为独立的编译单元。编译器无法知道更多，因为当代码到达它那里时，代码已经由预处理阶段插入。只有当链接器获得所有已编译代码并尝试匹配所有内容时，我们才会进入构建过程说“嘿，我已经有这个函数的另一个版本了！”然后失败的阶段。

如你所见，有两种使成员函数内联的方法。两种方法都必须在头文件中完成，因为编译器会按照头文件被包含的次数多次评估头文件代码，而源文件只会被运行一次。如果使用第二种方法却忘记 `inline` 关键字，就会遇到可怕的链接器错误。如果使用第二种方法且记得 `inline` 关键字，但在源文件中定义函数，也会遇到可怕的链接器错误——这次会提示没有定义。

> **提示：** 不要试图把所有东西都内联。否则最终只会导致编译时间变慢，扼杀你的生产力。只内联有意义的东西，比如成员变量的简单 getter 和 setter 函数。和其他任何事情一样，先进行性能分析，然后再根据需要优化。

## 保护级别和访问说明符

成员函数和成员数据有三种可能的访问说明符：

- `public`
- `protected`
- `private`

这些访问说明符表示成员具有的可访问性级别。在 **SampleClass\Vehicle.h** 中，你可以看到两个使用示例。请注意，与 C# 不同，你不需要在每个成员前重复访问说明符。相反，你声明访问说明符，后跟一个冒号（例如 `public:`），然后其后的每个声明和定义都会获得该可访问性级别，直到遇到另一个访问说明符。

默认情况下，类成员是私有的。这意味着如果类声明开头没有访问说明符，那么所有声明的成员都将是私有的，直到遇到访问说明符。如果一直没遇到，你就会得到一个完全私有的类，这会非常奇怪。

结构体成员默认为公有，因此偶尔你会看到没有任何访问说明符的结构体。不过，如果你希望在结构体中使用它们，其工作方式与类中相同。

最后，你可以多次使用同一个访问说明符；如果你希望组织类，先定义成员函数，再定义成员变量（或相反），可以轻松地这样做：

*注意：此代码仅用于说明；未包含在任何示例中。*

```cpp
#include <string>

class SomeClass
{
public:
    SomeClass(void);
    virtual ~SomeClass(void);
    int AddTwoInts(int, int);
    void StoreAString(const wchar_t*);

private:
    bool CheckForIntAdditionOverflow(int, int);

public:
    int SomePublicInteger;

protected:
    std::wstring m_storedString;
};
```

前面的类定义并没有定义任何特别有用的东西。不过，它确实展示了所有三种访问说明符的用法。它还表明你可以多次使用说明符，例如上一个示例中的 public。

## 继承

在 C++ 中指定类所派生的类时，你也应指定访问说明符。如果不指定，就会得到默认访问级别：类为 private，结构体为 public。注意，我说的是类。C++ 支持多重继承。这意味着一个类或结构体可以有多个直接基类或基结构体，而不像 C# 中一个类只能有一个父类。

C++ 没有单独的接口类型。一般来说，应避免多重继承，除非是作为缺少单独接口的变通方法。换句话说，一个类应当只有零个或一个真正的基类，以及零个或多个纯抽象类（接口）。不过，这只是个人风格建议。

对于多重继承，也有一些很好的理由。例如，假设你有三组功能。每一组都由函数和数据组成。再假设每组彼此无关——它们之间没有联系，但也不是互斥的。在这种情况下，你可能希望将每个功能组放入自己的类中。然后，如果你遇到需要创建同时需要其中两组甚至全部三组功能的类的情况，只需创建一个继承自全部三者的类即可。

或者，只要你的公有和受保护成员函数及变量中没有命名冲突，你就完成了。例如，如果三个功能组都有一个成员函数 `void PrintDiagnostics(void);` 会怎样？你完蛋了，对吧？嗯，事实证明并非如此，你（通常）不会完蛋。你需要使用一些奇怪的语法来指定你想要哪个基类的 `PrintDiagnostics` 函数。即便如此，你也没有完全搞定。

C++ 允许你指定希望一个类是普通基类还是虚基类。方法是在基类说明符中，在类名之前放置或不放置关键字 `virtual`。我们很快就会看一个处理所有这些内容的示例，但在那之前，重要的是要理解：如果你至少两次继承一个类，并且其中两个或更多继承不是虚继承，你最终会得到该类数据成员的多个副本。

当试图指定你想使用其中哪一个副本时，这会引发一大堆问题。表面上看，解决方案是从所有类虚继承，但由于 C++ 实现解析虚成员的方式，这会带来运行时性能损失。更好的做法是尽量避免这种情况发生，但由于这并不总是可能，所以一定要记住虚继承。

现在来看一个有助于理解这一切的示例：

### 示例：InheritanceSample\InheritanceSample.cpp

```cpp
#include <iostream>
#include <ostream>
#include <string>
#include <typeinfo>
#include "../pchar.h"

using namespace std;

class A
{
public:
    A(void) : SomeInt(0) { }
    virtual ~A(void) { }

    const wchar_t* Id(void) const { return L"A"; }

    virtual const wchar_t* VirtId(void) const { return L"A"; }

    int GetSomeInt(void) const { return SomeInt; }
    int                 SomeInt;
};

class B1 : virtual public A
```

