

编程提示：当异常可能在循环中发生时，你必须决定是将 try 块放在循环体内——在这种情况下，每次循环周期都会捕获异常（如第一个示例所示）——还是将整个循环放在 try 块内——在这种情况下，异常只会被捕获一次（如第二个示例所示）。两种选择没有哪一种更好，但如果你做出了错误的选择，客户端可能无法获得必要的信息。

注意：有时 catch 块会故意终止程序执行。当块不这样做，而是完成其执行时，最后一个 catch 块之后出现的任何语句都将接着执行。

## C3.5 程序员定义的异常类

你可能会发现 C++ 标准库中已有一个定义好的异常类，适合你程序的异常需求。你也可能想要定义自己的异常类。通常，C++ 异常类 exception 或其派生类之一是程序员定义异常类的基类。遵循这一做法可为处理异常提供标准化接口。如果你遵循这一做法，则需要使用 std 命名空间。

异常类通常由一个带有 string 参数的构造函数组成。例如，你可以定义类 TargetNotFoundException 为

```
#include <stdexcept>
#include <string>
using namespace std;

class TargetNotFoundException: public exception
{
public :
   TargetNotFoundException(const string& message = "")
      : exception("Target not found: " + message.c_str())
   { // end constructor
   }; // end class TargetNotFoundException
```

构造函数为 throw 语句提供了一种识别导致异常的条件的方法。例如，语句

```
throw TargetNotFoundException(target + " not found in a box");
```

调用 TargetNotFoundException 的构造函数。传递给构造函数的消息由从类 exception 继承的方法 what 返回。因此，诸如下面这样的 catch 块可以访问该消息：

```
catch(TargetNotFoundException except)
{
   cout << except.what() << endl;
}
```

如果在执行此块时 target 的值为 "glasses"，则输出为

Target not found: glasses not found in a box!

虽然字符串消息很有帮助，但有时我们想要向客户端返回更多信息以帮助解决问题。我们可以向异常类添加一个私有数据字段来存储其他错误详细信息。构造函数中的第二个参数用于接收这些详细信息的初始值，以及一个公共访问器方法，以便客户端可以检索它们，也是必需的。当方法抛出此异常时，它将调用构造函数，并将额外数据和消息作为其两个参数发送。

## 编程提示：使用异常

在函数中抛出异常：

- 确定必须检查哪些错误、前置条件、后置条件和异常情况，以及在哪里检查它们，以便函数能够正确执行其任务。
- 检测错误、前置条件、后置条件或异常情况。通常这是通过 if 语句完成的。
- 如果发生了错误条件，请使用 throw 语句抛出异常。作为异常类构造函数的参数，传递描述错误原因的字符串。
- 向函数头添加 throw 子句，指示函数抛出的异常。
- 派生一个自定义异常类，以更好地识别导致错误的条件。虽然这样做是可选的，但很可取。

处理异常或使用可能抛出异常的函数

- 将可能抛出异常的语句放在 try 块中。try 块中的语句越少越好。不要在 try 块中使用 new 创建对象。
- 在 try 块之后，为 try 块中的语句可能抛出的每种异常类型放置 catch 块。按从最具体的异常类到更通用的异常类的顺序放置 catch 块。

## ADT 栈的实现

## 第 7 章

- 目录
- 7.1 基于数组的实现 242
- 7.2 基于链接的实现 245
- 7.3 使用异常的实现 249

- 摘要 251
- 练习 251
- 编程问题 252

- 先修知识
- 第 3 章 基于数组的实现
- C++ 间奏 2 指针、多态和内存分配
- 第 4 章 基于链接的实现
- 第 6 章 栈
- C++ 间奏 3 异常

本章使用在第 3 章和第 4 章中为 ADT 袋描述的技术来实现 ADT 栈。我们首先将使用数组，然后使用链接节点链来存储栈的条目。你应该会很高兴发现这些实现的简单性和高效性。我们随后将修改这些实现，以使用异常作为方法信号异常情况（例如，尝试从空栈获取条目）的一种方式。

## 7.1 基于数组的实现

图 7-1a 显示了一个包含栈条目的数组草图。栈顶条目应该在数组的哪个位置？由于条目在栈顶添加或删除，如果我们将栈底固定在索引 0 并使用索引 top 跟踪栈顶的位置，就可以避免移动当前条目。然后，如果 items[top] 是栈顶条目，items 和 top 可以是我们栈类的私有数据成员。图 7-1b 说明了这些细节。请注意，此图中栈顶位于索引 2。我们可以在索引[3]处添加新条目并递增 top，或者通过将 top 递减到 1 来删除索引[2]中的栈顶条目。

我们的类将有一个默认构造函数来初始化私有数据成员 items 和 top。但是，由于我们计划在静态分配的内存中存储栈的条目，编译器生成的析构函数和拷贝构造函数将足够。另一方面，如果我们使用动态分配的数组，则需要定义析构函数和拷贝构造函数。

清单 7-1 显示了 ADT 栈基于数组实现的头文件。描述方法的注释在第 6 章的清单 6-1 中。

### 图 7-1 使用数组存储栈的条目：(a) 初步草图；(b) 实现细节

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_268_0.png)

### 清单 7-1 基于数组栈的头文件

```
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
   int top; // Index to top of stack
public:
    ArrayStack(); // Default constructor
    bool isEmpty() const;
    bool push(const ItemType& newEntry);
    bool pop();
    ItemType peek() const;
}; // end ArrayStack

#include "ArrayStack.cpp"
#endif
```

前一个头文件声明的方法的实现如清单 7-2 所示。这些定义很简单，但请注意，方法 peek 使用 assert 来强制执行其前置条件，即栈至少包含一个条目。本章稍后，我们将修改 peek，以便在客户端在栈为空时调用它时抛出异常。

### 清单 7-2 基于数组栈的实现文件

/* @file ArrayStack.cpp */

#include <cassert> // For assert
#include "ArrayStack.h" // Header file

template<class ItemType>
ArrayStack<ItemType>::ArrayStack() : top(-1)
{ } // end default constructor

// Copy constructor and destructor are supplied by the compiler

template<class ItemType>
bool ArrayStack<ItemType>::isEmpty() const
{
   return top < 0;
} // end isEmpty

template<class ItemType>
bool ArrayStack<ItemType>::push(const ItemType& newEntry)
{
   bool result = false;
   if (top < MAX_STACK - 1) // Does stack have room for newEntry?
   {
      top++;
      items[top] = newEntry;
      result = true;
   } // end if

   return result;
} // end push

template<class ItemType>
bool ArrayStack<ItemType>::pop()

(continues)

