

## 在命名空间中使用项目

一旦头文件和实现文件就绪，任何程序都可以使用我们的新类。在程序顶部，你放置一个包含指令来包含头文件，如下所示为我们的示例：

```
#include "throttle.h"
```

> 请注意，我们只包含头文件，而不包含实现文件。

在包含指令之后，程序可以以三种方式之一使用命名空间中定义的项目：

- 1. 放置一个 using 语句，使整个命名空间可用。该语句的格式为：
  using namespace main_savitch_2A;

  这个 using 语句使来自指定命名空间（main_savitch_2A）的所有项目可用。这是我们一直用来从标准库中获取所有可用项目的相同技术（使用语句 `using namespace std`）。

- 2. 如果我们只需要使用命名空间中的特定项目，那么我们放置一个由关键字 using、命名空间名称、两个冒号和我们想要使用的项目名称组成的语句。例如：
  using main_savitch_2A::throttle;

  这允许我们从命名空间中使用 throttle；但是，如果命名空间中有其他项目，则它们不可用。

- 3. 没有 using 语句，我们仍然可以通过在使用项目的位置将项目名称与命名空间和 "::" 前缀来使用任何项目。例如，我们可以用语句声明一个 throttle 变量：
  main_savitch_2A::throttle apollo;

  这种 "::" 的用法是我们在第 42 页看到的作用域解析运算符的一个示例。它澄清了我们要求使用哪个特定的 throttle。

创建和使用命名空间的摘要如图 2.7 所示，包括一个警告，即永远不要在头文件中放置 using 语句。

我们使用修改后的 throttle 的完整演示程序出现在第 61 页的图 2.8 中。当完整程序实际被编译时，您可能需要提供关于在哪里找到实现文件 throttle.cxx 的编译版本的额外信息。这个过程称为链接，因编译器而异（参见附录 D）。

## 图 2.7 创建和使用命名空间的摘要

**1. 全局命名空间：** 任何未明确放置在命名空间中的项目都成为所谓的 **全局命名空间** 的一部分。这些项目可以在任何点使用，而不需要 using 语句或作用域解析运算符。

**2. C++ 标准库：** 如果你使用新的 C++ 头文件名称（例如 `<iostream>` 或 `<cstdlib>`），那么 C++ 标准库中的所有项目都自动成为 `std` 命名空间的一部分。使用这些项目的最简单方法是在包含语句后放置一个 using 指令：`using namespace std;`。另一方面，如果你使用旧的 C++ 头文件名称（例如 `<iostream.h>` 或 `<stdlib.h>`），那么项目是全局命名空间的一部分，因此不需要 using 语句或作用域解析运算符。

**3. 创建你自己的命名空间：** 要创建一个新命名空间，项目被放置在一个命名空间分组中，形式如下：
```
namespace <The name for the namespace>
{
    // Any item that belongs to the namespace is written here.
}
```
单词 `namespace` 是 C++ 关键字。命名空间的名称可以是任何 C++ 标识符，但应选择以避免与其他人的命名空间可能发生冲突（通过使用你真实姓名或电子邮件地址的一部分）。一个命名空间可以有几个不同的命名空间分组，可能位于不同的文件中。例如，类定义可以出现在头文件中的一个命名空间分组中，而成员函数定义出现在实现文件中的同一命名空间的第二个分组中。

**4. 使用命名空间：**
- 要使用命名空间中的所有项目，请在所有包含语句后放置一个 using 指令，形式为：
  `using namespace <The name for the namespace> ;`
- 要使用命名空间中的一个项目，请在所有包含语句后放置一个特定的 using 指令，形式为：
  `using <The name for the namespace>::<The name of the item> ;`
- 没有 using 指令，你仍然可以通过在项目前加上命名空间名称和 "::" 来直接在程序中使用项目。

**永远不要将 using 语句实际放在头文件中**
有时头文件本身需要使用来自命名空间的某个东西。在这种情况下，始终使用上面显示的第三种形式；永远不要将 using 语句放在头文件中（因为这样做可能会在包含头文件的其他程序中产生意外结果）。

## 图 2.8 修改后的 Throttle 类示例程序

### 一个程序

```
// FILE: demo2.cxx
// This small demonstration shows how the revised throttle class is used.
#include <iostream>     // Provides cout and cin
#include <cstdlib>      // Provides EXIT_SUCCESS
#include "throttle.h"   // Provides the throttle class
using namespace std;
using main_savitch_2A::throttle;

const int DEMO_SIZE = 5; // Number of positions in a demonstration throttle

int main( )
{
    throttle sample(DEMO_SIZE); // A throttle to use for our demonstration
    int user_input;             // The position to which we set the throttle

    // Set the sample throttle to a position indicated by the user.
    cout << "I have a throttle with " << DEMO_SIZE << " positions." << endl;
    cout << "Where would you like to set the throttle?" << endl;
    cout << "Please type a number from 0 to " << DEMO_SIZE << ": ";
    cin >> user_input;
    sample.shift(user_input);

    // Shift the throttle down to zero, printing the flow along the way.
    while (sample.is_on( ))
    {
        cout << "The flow is now " << sample.flow( ) << endl;
        sample.shift(-1);
    }
    cout << "The flow is now off" << endl;

    return EXIT_SUCCESS;
}
```

### 示例对话

我有一个有 5 个位置的节流阀。
你想把节流阀设在哪里？
请输入 0 到 5 之间的数字：3
当前流量为 0.6
当前流量为 0.4
当前流量为 0.2
当前流量已关闭

## 第 2.3 节自测练习

- 13. 程序员阅读什么来学习如何使用新类？
- 14. 宏保护的目的是什么？
- 15. 如果 x 和 y 是对象，赋值 y = x 的正常操作是什么？
- 16. 假设 x 是一个 throttle。声明 throttle(x) 的效果是什么？
- 17. 编写 #include 指令和一个 using 语句，主程序必须使用它们才能使用 throttle 类。

- 18. 设计并实现一个名为 circle_location 的类，用于跟踪绕圆移动的单个点的位置。该类的对象将点的位置记录为角度，从圆顶部顺时针方向测量。包括这些公共成员函数：
  - 一个默认构造函数，将点放在圆顶部。
  - 另一个构造函数，将点放在指定位置。
  - 一个函数，将点移动指定的度数绕圆。使用正参数顺时针移动，使用负参数逆时针移动。
  - 一个函数，返回点的当前位置，以度为单位，从圆顶部顺时针测量。
  你的解决方案应包括一个单独的头文件、实现文件和一个使用新类的主程序示例。

- 19. 设计并实现一个名为 clock 的类。一个 clock 对象保存一个时间值的实例，例如 9:48 PM。至少要有这些公共成员函数：
  - 一个默认构造函数，将时间设置为午夜
  - 一个函数，显式分配给定时间（你需要为该函数考虑适当的参数）
  - 检索信息的函数：当前小时、当前分钟，以及一个布尔函数来确定时间是否在中午或之前
  - 一个函数，将时间向前推进给定的分钟数

- 20. 什么是全局命名空间？
- 21. 当命名空间的一部分需要在实际头文件中使用时，应该使用第 59 页中的哪三种形式之一？

