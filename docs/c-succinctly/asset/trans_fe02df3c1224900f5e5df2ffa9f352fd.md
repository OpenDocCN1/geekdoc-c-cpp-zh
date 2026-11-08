
```cpp
double pricePaid
};

~Vehicle(void);

VehicleCondition GetVehicleCondition(void)
{
    return m_condition;
};

void SetVehicleCondition(VehicleCondition condition);

double GetBasis(void) { return m_basis; };

private:
    VehicleCondition        m_condition;
    double                  m_basis;
};
}
```

## 示例：SimpleClassSample\\Vehicle.cpp

```cpp
#include "Vehicle.h"
#include "VehicleCondition.h"

using namespace Inventory;
using namespace std;

Vehicle::Vehicle(VehicleCondition condition, double pricePaid) :
        m_condition(condition),
        m_basis(pricePaid)
{
}

Vehicle::~Vehicle(void)
{
}

void Vehicle::SetVehicleCondition(VehicleCondition condition)
{
        m_condition = condition;
}
```

## 示例：SimpleClassSample\\SimpleClassSample.cpp

```cpp
#include <iostream>
#include <ostream>
#include <string>
#include <iomanip>
#include "Vehicle.h"
#include "VehicleCondition.h"
#include "../pch.h"

using namespace Inventory;
using namespace std;

int _tmain(int /*argc*/, wchar_t* /*argv*/[])
{
        auto vehicle = Vehicle(Vehicle::Excellent, 325844942.65);
        auto condition = vehicle.GetVehicleCondition();
        wcout << L"The vehicle is in " <<
                GetVehicleConditionString(condition).c_str() <<
                L" condition. Its basis is $" << setw(10) <<
                setprecision(2) << setiosflags(ios::fixed) <<
                vehicle.GetBasis() << L"." << endl;

        return 0;
}
```

在 **Vehicle.h** 中，我们首先对 **VehicleCondition** 枚举类进行前向声明。我们将在本章末尾进一步讨论这项技术。目前的关键点是：（1）我们可以使用这个前向声明，也可以包含 **VehicleCondition.h** 头文件；（2）**VehicleCondition** 的声明必须位于 **Vehicle** 的类定义之前。

为了让编译器为 **Vehicle** 的实例分配足够的空间，它需要知道 **Vehicle** 的每个数据成员有多大。我们可以通过包含相应的头文件来让它知道，或者在某些情况下使用前向声明。如果 **VehicleCondition** 的声明出现在 **Vehicle** 的定义之后，那么编译器将拒绝编译代码，因为编译器不知道 **VehicleCondition** 有多大，甚至不知道它是什么数据类型。

在这种情况下，一个简单的声明就足以告诉编译器 **VehicleCondition** 是什么（一个枚举类）以及它有多大。除非另有指定，枚举类默认使用 int 作为其底层字段。如果我们让底层字段留空，但随后又在其他地方说使用 short、long 或其他底层字段类型，编译器将生成不同的错误消息，告诉我们存在多个相互冲突的声明。

然后我们继续定义 **Vehicle** 类。该定义包括其成员函数和成员变量的声明。大多数情况下，我们不定义成员函数。例外是 **GetVehicleCondition** 成员函数和 **GetBasis** 成员函数，我们将在“[内联成员函数](#)”一节中讨论它们。

我们在 **Vehicle.cpp** 中定义 **Vehicle** 的其他成员函数。在这种情况下，成员函数是构造函数、析构函数和 **SetVehicleCondition**。通常，像 **SetVehicleCondition** 这样的函数会是内联的，**Vehicle** 类中简单的构造函数和析构函数也会如此。这里单独定义它们，是为了说明当这些类型的成员函数不是内联函数时如何定义它们。我们将在专门讨论构造函数的章节中讨论那种看起来奇怪的构造函数语法。**Vehicle** 类的其余代码应该很清楚。

> **注意：** 虽然不要求你采用 **ClassName.h** 或 **ClassName.cpp** 的文件命名约定，但你几乎到处都会看到它被使用，因为它使代码的使用和维护更容易。

**VehicleCondition.h** 中的 **GetVehicleConditionString** 内联函数返回的是该函数中创建的 **std::wstring** 的副本，而不是局部值本身。如果你来自 C#，可能会觉得这有点奇怪，因为没有使用 new 关键字。我们将在讨论存储持续时间的章节中讨论自动持续时间类型时探讨这一点。

入口点函数使用了 C++ 标准库的一些 I/O 格式化功能。

### 成员函数

如前所述，成员函数是类、结构体或联合体的一部分。简单来说，从这里开始，我将把它们作为类成员来讨论。

静态成员函数可以调用其他静态类成员函数，无论保护级别如何。静态成员函数还可以显式（即 `SomeClass::SomeFloat = 20.0f;`）或隐式（即 `SomeFloat = 20.0f;`）访问静态类成员数据，无论保护级别如何。

如果有一个与类成员同名的参数，显式形式会很有帮助。为成员数据添加 `m_` 前缀，例如 `m_SomeFloat`，可以消除这个问题，并清楚表明你正在处理的是类成员数据而不是局部变量或参数。这只是一种风格选择，不是要求。

实例（即非静态）成员函数会自动获得一个 `this` 指针，指向调用它们的实例的实例数据。实例成员函数可以调用其他类成员函数，并访问所有类成员数据，无论是显式地——与静态成员使用 `this->m_count++;` 访问实例数据一样——还是隐式地——与静态和实例数据一样（例如 `m_data++`），无论保护级别如何。

### 内联成员函数

在 `SimpleClassSample\Vehicle.h` 中，`GetVehicleCondition` 和 `GetBasis` 成员函数都同时被声明和定义。这种声明与定义的组合在 C++ 中称为内联成员函数。由于这类似于在 C# 中编写方法，可能也会诱使你在 C++ 中这样做。除了一些例外情况，你不应该这样做。

正如我们之前讨论的，当你构建 C++ 项目时，编译器只会遍历每个源文件一次。它可能会对相同的源文件进行多遍处理以优化它们，但在完成后不会再回来。

相比之下，每当头文件被包含到另一个文件中时，编译器都会重新处理你的头文件，无论该文件是源文件还是另一个头文件。这意味着在一次构建过程中，编译器最终可能会多次遍历头文件中的代码。

在 `SimpleClassSample\Vehicle.h` 头文件的开头，你会看到 `#pragma once` 指令。这是一行有用且重要的代码。如果你在某个源文件中包含头文件 `A.h`，然后又包含另一个包含 `A.h` 的头文件，`#pragma once` 指令会告诉预处理器不要再次包含 `A.h` 的内容。这可以防止预处理器在两个相互包含的头文件之间无限地来回跳转。它还可以防止编译器错误。如果 `A.h` 被多次包含，编译器在遇到第二次包含 `A.h` 时的类型定义时会失败。

即使有了该指令，对于每个包含该头文件的源文件，编译器仍然需要包含并解析该头文件代码。你放入头文件的内容越多，构建每个源文件所需的时间就越长。这会增加编译时间；正如你将发现的，与 C# 相比，C++ 项目的编译时间可能相当长。

当你确实在头文件中内联包含成员函数的定义时，C++ 编译器可以在任何使用该函数的源文件中将该代码内联。这通常会使程序执行更快，因为程序可以直接就地运行代码，而不需要进行函数调用。

编译器会保留作用域，因此你无需担心内联函数中定义的变量与其使用位置所在函数中的变量之间发生命名冲突。对于像前面示例那样只是检索成员变量值的代码，内联定义可以提高速度，尤其是在代码在循环中执行时。

