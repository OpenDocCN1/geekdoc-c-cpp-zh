
## 类的头文件

当你设计并实现一个类时，应该提供一个单独的头文件。

在头文件的顶部，放置程序员使用该类所需的所有文档。

文档之后是该类的类定义。但只出现类定义，而不出现成员函数的实现（内联函数除外）。

将类定义放在命名空间内，并在整个内容周围放置一个“宏保护”。宏保护可防止意外的重复定义。

### 图 2.5 节流器类的头文件

### 一个头文件

```
// FILE: throttle.h
// CLASS PROVIDED: throttle (part of the namespace main_savitch_2A)
// ...
// CONSTRUCTORS for the throttle class:
// throttle()
// Postcondition: The throttle has one position above the shut_off position, and it is currently shut off.
// throttle(int size)
// Precondition: size > 0.
// Postcondition: The throttle has size positions above the shut_off position, and it is currently shut off.
// MODIFICATION MEMBER FUNCTIONS for the throttle class:
// void shut_off( )
// Postcondition: The throttle has been turned off.
// void shift(int amount)
// Postcondition: The throttle's position has been moved by amount (but not below 0 or above the top position).
```

成员函数通常没有前置条件。

### （图 2.5 续）

```
//
// CONSTANT MEMBER FUNCTIONS for the throttle class:
// double flow( ) const;
//     Postcondition: The value returned is the current flow as a
//     proportion of the maximum flow.
//
// bool is_on( ) const;
//     Postcondition: If the throttle's flow is above 0 then
//     the function returns true; otherwise it returns false.
//
// VALUE SEMANTICS for the throttle class (see the discussion on page 56):
//     Assignments and the copy constructor may be used with throttle objects.
#ifndef MAIN_SAVITCH_THROTTLE
#define MAIN_SAVITCH_THROTTLE
namespace main_savitch_2A
{
    class throttle
    {
    public:
        // CONSTRUCTORS
        throttle( );
        throttle(int size);
        // MODIFICATION MEMBER FUNCTIONS
        void shut_off( );
        void shift(int amount);
        // CONSTANT MEMBER FUNCTIONS
        double flow( ) const { return position / double(top_position); }
        bool is_on( ) const { return (position > 0); }
    private:
        int top_position;
        int position;
    };
}
#endif
```

宏保护开始

命名空间分组开始

命名空间分组结束

宏保护结束

## 在头文件中描述类的值语义

类的值语义决定了值如何从一个对象复制到另一个对象。在 C++ 中，值语义包含两个操作：赋值运算符和拷贝构造函数。

**赋值运算符。** 对于两个对象 x 和 y，赋值 y = x 将 x 的值复制到 y。任何我们定义的新类都允许进行此类赋值。对于新类，C++ 通常通过简单地将赋值号右侧对象的每个成员变量复制到左侧对象来执行赋值。这种复制方法称为自动赋值运算符。稍后我们将看到自动赋值运算符无法工作的示例。但目前，我们的新类可以使用自动赋值运算符。

**拷贝构造函数。** 拷贝构造函数是恰好带有一个参数的构造函数，且参数的数据类型与构造函数所属的类相同。例如，throttle 的拷贝构造函数有一个参数，该参数本身就是一个 throttle。拷贝构造函数的常见目的是将新对象初始化为现有对象的精确副本。例如，下面是一段代码，它创建一个名为 x 的 100 档位节流器，将 x 移至其中间位置，然后声明第二个节流器，将其初始化为 x 的精确副本：

```
throttle x(100);
x.shift(50);
throttle y(x);
```

节流器 y 被初始化为 x 的副本，因此两个节流器都位于 100 档位中的第 50 档位。

高亮语句激活了节流器的拷贝构造函数，将 y 初始化为 x 的精确副本。初始化后，x 和 y 可能会执行不同的操作，最终产生不同的燃料流量，但此时两个节流器都设置为 100 档位中的第 50 档位。

调用拷贝构造函数有另一种语法。与其写 throttle y(x);，不如写 throttle y = x;。这种替代语法看起来像赋值语句，但请记住，实际效果略有不同。赋值 y = x; 仅将 x 复制到已存在的对象 y。另一方面，声明 throttle y = x; 既声明了新对象 y，又调用拷贝构造函数将 y 初始化为 x 的副本。我们将始终使用原始形式 throttle y(x);，因为这种形式不太可能与普通赋值语句混淆。

作为类的实现者，你可以像编写其他构造函数一样编写拷贝构造函数——你将在后续章节的类中这样做。但目前我们可以利用 C++ 的一个特性：C++ 提供了自动拷贝构造函数。自动拷贝构造函数通过仅复制现有对象的所有成员变量来初始化新对象。例如，在声明 throttle y(x); 中，自动拷贝构造函数会将现有节流器 x 的两个成员变量复制到新节流器 y。

对于许多类，自动赋值运算符和自动拷贝构造函数工作良好。但正如我们所警告的，稍后我们将看到自动版本失效的类。仅复制成员变量并不总是足够。正因为如此，程序员对赋值和拷贝构造函数持谨慎态度。为解决这个问题，我们建议你的文档中包含一条注释，指明值语义可以安全使用。

### 编程提示

### 记录值语义

当你实现一个类时，文档中应包含一条注释，指明值语义可以安全使用。例如，在我们的 throttle 头文件中，我们写了：

```
// VALUE SEMANTICS for the throttle class:
// Assignments and the copy constructor may be used with throttle
// objects.
```

## 实现文件

新类的实现文件包含几个项目：首先，出现一小段注释，指明文档可在头文件中找到。其次，出现一条包含指令，导致编译器从头文件获取类定义。在我们的 throttle 示例中，包含指令如下：

- 注释
- 包含指令
- 重新打开命名空间并定义实现

```
#include "throttle.h"
```

当我们列出头文件名 "throttle.h" 时，使用引号而不是尖括号。尖括号（例如包含指令 #include <iostream>）仅用于包含标准库设施，而我们对自己的头文件使用引号。

包含指令之后，程序重新打开命名空间并给出类成员函数的实现。命名空间通过头文件中看到的相同语法重新打开：

```
namespace main_savitch_2A
{
    // The definitions of the member functions are written here.
}
```

大多数编译器要求实现文件名具有特定的后缀，例如 .cpp 或 .C。我们将对实现文件名使用 .cxx 后缀，例如图 2.6 中所示的完整实现文件 throttle.cxx。

### 类的实现文件

每个类都有一个单独的实现文件，其中包含类成员函数的实现。有关实现文件和头文件的更多内容，请参见 www.cs.colorado.edu/~main/separation.html。

### 图 2.6 节流器类的实现文件

### 一个实现文件

```
// FILE: throttle.cxx
// CLASS IMPLEMENTED: throttle (see throttle.h for documentation)

#include <cassert>    // Provides assert
#include "throttle.h" // Provides the throttle class definition

namespace main_savitch_2A
{
    throttle::throttle( )
    { // A simple on-off throttle
        top_position = 1;
        position = 0;
    }

    throttle::throttle(int size)
    // Library facilities used: cassert
    {
        assert(size > 0);
        top_position = size;
        position = 0;
    }

    void throttle::shift(int amount)
    {
        position += amount;

        if (position < 0)
            position = 0;
        else if (position > top_position)
            position = top_position;
    }
}
```
