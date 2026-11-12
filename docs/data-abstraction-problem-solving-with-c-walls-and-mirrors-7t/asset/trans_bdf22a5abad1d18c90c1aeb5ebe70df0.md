

```cpp
char newChar = (static_cast<int>(str[i]) - base + 3) % 26 + base;
try
{
    str.replace(i, 1, newChar);
}
catch (out_of_range e)
{
    cout << "No character at position " << i << endl;
    // end try-catch
} // end encodeChar
```

main 中的调用 encodeString(99, str) 会导致 encodeChar 被调用 99 次，因此异常被抛出 98 - str.length() 次。encodeChar 的以下输出是结果。

- 位置 99 处没有字符
- 位置 98 处没有字符
- 位置 97 处没有字符
- ...

当异常未被处理时，程序在异常第一次发生时终止。处理异常允许代码继续执行。

虽然 out_of_range 异常是在函数 encodeChar 中抛出的，但那不一定是处理异常的最佳位置。例如，如果客户端调用了 encodeString(10000, str)，encodeChar 打印的消息将出现 9999 - str.length() 次！在这种情况下，try 和 catch 块出现在函数 encodeString 中而不是 encodeChar 中更合理，如下所示：

```cpp
void encodeString(int numChar, string& str)
{
    try
    {
        for (int i = numChar - 1; i >= 0; i--)
            encodeChar(i, str);
    }
    catch (out_of_range e)
    {
        cout << "The string does not contain " << numChar;
        cout << " characters." << endl;
        cout << e.what() << endl;
    } // end try-catch
} // end encodeString
```

现在当 encodeChar 抛出 out_of_range 异常时，异常会传播回函数 encodeString，该函数结束 try 块中语句的执行并执行 catch 块中的语句。表达式 e.what() 调用异常 e 的 what 方法，因此它表示一个描述异常的字符串。对于此示例，将显示以下输出。

- 字符串不包含 10 个字符。
- 无效的字符串位置

消息只打印一次，因为 for 循环在 try 块内部，当异常发生时该块会被放弃。如果 try 块被放在 for 循环内部，encodeChar 将在循环的每次迭代中被调用——因此异常会被抛出并处理——结果将是多份消息的副本。

### 编程提示：当异常可能在循环中发生时

当异常可能在循环中发生时，你必须决定是将 try 块放在循环体内（在这种情况下，每次循环周期都会捕获异常，如第一个示例所示），还是将整个循环放在 try 块内（在这种情况下，异常只会被捕获一次，如第二个示例所示）。两种选择都不比另一种更好，但如果你做出了错误的选择，客户端可能无法获得必要的信息。

### 注意：有时 catch 块会故意终止程序执行

有时 catch 块会故意终止程序执行。当块不这样做，而是完成其执行时，最后一个 catch 块之后出现的任何语句将接下来执行。

## C3.5 程序员定义的异常类

你可能会发现 C++ 标准库中已定义了一个适合你程序异常需求的异常类。你也可能想定义自己的异常类。通常，C++ 异常类 exception 或其派生类之一是程序员定义的异常类的基类。遵循此做法可为使用异常提供标准化接口。如果你遵循此做法，则需要使用 std 命名空间。

异常类通常由带有字符串参数的构造函数组成。例如，你可以定义类 TargetNotFoundException 如下：

```cpp
#include <stdexcept>
#include <string>
using namespace std;
class TargetNotFoundException: public exception
{
public:
   TargetNotFoundException(const string& message = "")
      : exception("Target not found: " + message.c_str())
   { } // end constructor
}; // end class TargetNotFoundException
```

构造函数为 throw 语句提供了一种识别导致异常的条件的方法。例如，语句

```cpp
throw TargetNotFoundException( target + " not found in a box" );
```

调用 TargetNotFoundException 的构造函数。传递给构造函数的消息由从类 exception 继承的方法 what 返回。因此，诸如以下的 catch 块可以访问该消息：

```cpp
catch(TargetNotFoundException except)
{
   cout << except.what() << endl;
}
```

如果 target 在此块执行时具有值 "glasses"，则输出为

未找到目标：在盒子中未找到眼镜！

虽然字符串消息很有帮助，但有时我们想向客户端返回更多信息以帮助解决问题。我们可以向异常类添加一个私有数据字段来存储其他错误详细信息。还需要构造函数中的第二个参数来接收这些详细信息的初始值，以及一个公共访问器方法，以便客户端可以检索它们。当方法抛出此异常时，它将调用构造函数并将额外数据和消息作为其两个参数发送。

### 编程提示：使用异常

在函数中抛出异常：

- 确定必须检查哪些错误、前置条件、后置条件和异常情况以及在哪里检查它们，以便你的函数可以正确执行其任务。
- 检测错误、前置条件、后置条件或异常情况。通常这是通过 if 语句完成的。
- 如果发生了错误条件，请使用 throw 语句抛出异常。作为异常类构造函数的参数，传递描述错误原因的字符串。
- 向函数头添加 throws 子句，指示函数抛出的异常。
- 派生自定义异常类以更好地识别导致错误的条件。虽然这样做是可选的，但很可取。

处理异常或使用可能抛出异常的函数

- 将可能抛出异常的语句放在 try 块中。try 块中的语句越少越好。不要在 try 块中使用 new 创建对象。
- 在 try 块之后，为 try 块中的语句可能抛出的每种异常类型放置 catch 块。按从最具体的异常类到更一般的异常类的顺序放置 catch 块。

## ADT 栈的实现

## 第 7 章

- 目录
- 7.1 基于数组的实现 242
- 7.2 基于链接的实现 245
- 7.3 使用异常的实现 249
- 小结 251
- 习题 251
- 编程问题 252

- 先修知识
- 第 3 章 基于数组的实现
- C++ 间奏 2 指针、多态和内存分配
- 第 4 章 基于链接的实现
- 第 6 章 栈
- C++ 间奏 3 异常

本章使用我们在第 3 章和第 4 章中为 ADT 袋描述的技术来实现 ADT 栈。我们首先将使用数组，然后使用链接节点链来存储栈的条目。你应该会发现这些实现的简单性和高效性，从而感到高兴。然后我们将修改这些实现以使用异常作为方法信号异常情况的一种方式，例如尝试从空栈中获取条目。

### 7.1 基于数组的实现

图 7-1a 显示了包含栈条目的数组的草图。栈顶条目应该在数组的哪个位置？由于条目在栈顶添加或删除，如果我们将栈底固定在索引 0 并使用索引 top 跟踪栈顶的位置，就可以避免移动当前条目。然后，如果 items 是数组且 items[top] 是栈顶条目，items 和 top 可以是我们栈类的私有数据成员。图 7-1b 说明了这些细节。请注意，此图中栈顶位于索引 2。我们可以在索引 [3] 处添加新条目然后递增 top，或者通过将 top 递减到 1 来删除索引 [2] 中的栈顶条目。

我们的类将有一个默认构造函数来初始化私有数据成员 items 和 top。但是，由于我们计划在静态分配的内存中存储栈的条目，编译器生成的析构函数和拷贝构造函数将足够。另一方面，如果我们使用动态分配的数组，则必须定义析构函数和拷贝构造函数。

清单 7-1 显示了 ADT 栈基于数组实现的头文件。描述方法的注释在第 6 章的清单 6-1 中。

### 图 7-1 使用数组存储栈的条目：(a) 初步草图；(b) 实现细节

![](img/288a0c22d14d2450c1e772f228f867b0_268_0.png)

### 清单 7-1 基于数组的栈的头文件

```cpp
/* ADT stack: Array-based implementation.
   File ArrayStack.h */
#ifndef _ARRAY_STACK
#define _ARRAY_STACK
#include "StackInterface.h"
const int MAX_STACK = maximum-size-of-stack;
template<class ItemType>
class ArrayStack : public StackInterface<ItemType>
{
private:
   ItemType items[MAX_STACK]; // Array of stack items
   int top;    // Index to top of stack
```

