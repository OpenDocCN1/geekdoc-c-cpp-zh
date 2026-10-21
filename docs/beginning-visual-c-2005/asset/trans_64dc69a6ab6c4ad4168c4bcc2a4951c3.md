

## 第10章

以下代码显示了问题所在：

```
int main(int argc, char* argv[])
{
    Name myName("Ivor", "Horton");                 // Try a single object

    // Retrieve and store the name in a local char array
    char theName[10];
    cout << "\nThe name is " << myName.getName(theName);

    // Store the name in an array in the free store
    char* pName = new char[myName.getNameLength()];
    cout << "\nThe name is " << myName.getName(pName);

    cout << endl;
    return 0;
}
```

两条阴影线都有错误。第一条阴影线提供了 10 个字符的数组来存储姓名。实际上需要 12 个：10 个用于两个名字，一个用于空格，一个用于末尾的 '\0'。第二条阴影线应将 getNameLength() 函数返回的值加 1，以允许末尾的 '\0'。因此，main() 中的代码应为：

```
int main(int argc, char* argv[])
{
    Name myName("Ivor", "Horton");                 // Try a single object

    // Retrieve and store the name in a local char array
    char theName[12];
    cout << "\nThe name is " << myName.getName(theName);

    // Store the name in an array in the free store
    char* pName = new char[myName.getNameLength()+1];
    cout << "\nThe name is " << myName.getName(pName);

    cout << endl;
    return 0;
}
```

类中 getNameLength() 成员的定义存在更严重的问题。它省略了第一个名字和第二个名字之间空格的 1 个字符，因此返回的值总是少一个。定义应为：

```
int Name::getNameLength() const
{
#ifdef FUNCTION_TRACE
    // Trace function calls
    cout << "\nName::getNameLength() called.";
#endif
    return strlen(pFirstname)+strlen(pSurname)+1;
}
```

事情到此并没有结束。您可能已经发现您的类仍然存在严重错误，但继续进行测试，看看它们是否会在测试中暴露出来。

## 测试扩展的类

根据输出结果，一切正常运行，因此是时候将重载比较运算符的定义添加到 Name 类中了。我假设这是一个新的 Win32 控制台项目，Ex10_02。要为 Name 对象实现比较运算符，您可以使用 `<cstring>` 头文件中声明的比较函数。从“小于”运算符开始：

// Less than operator
bool Name::operator<(const Name& name) const
{
    int result = strcmp(pSurname, name.pSurname);
    if(result < 0)
        return true;
    if(result == 0 && strcmp(pFirstname, name.pFirstname) < 0)
        return true;
    else
        return false;
}
```

您现在可以非常轻松地用 < 运算符来定义 > 运算符：

// Greater than operator
bool Name::operator>(const Name& name) const
{
    return name > *this;
}
```

对于确定相等的姓名，您再次使用标准库中的 `strcmp()` 函数：

// Equal to operator
bool Name::operator==(const Name& name) const
{
    if(strcmp(pSurname, name.pSurname) == 0 &&
                         strcmp(pFirstname, name.pFirstname) == 0)
        return true;
    else
        return false;
}
```

现在扩展测试程序。您可以创建一个 Name 对象数组，以任意方式初始化它们，然后使用 Name 对象的比较运算符比较数组元素。以下是 `main()` 以及用于初始化 Name 数组的函数 `init()`：

// Ex10_02.cpp : Extending the test operation

#include <iostream>
using namespace std;
#include "Name.h"
```

```
// Function to initialize an array of random names
void init(Name* names, int count)
{
    char* firstnames[] = { "Charles", "Mary", "Arthur", "Emily", "John"};
```

```
<< names[j].getName(jName);
}
cout << endl;
return 0;
}
```

init() 函数从名字数组中依次选择名字和姓氏的组合来初始化 Name 对象数组。生成 25 个名字后会重复，但这里只需要 10 个。

## 寻找下一个错误

如果您使用调试工具栏上的“开始调试”按钮在调试器控制下启动程序，程序再次失败。图 10-18 所示的消息框被显示。

![](img/2359b0c604600c58fba3539c738a356e_634_0.png)

消息框表明您已超出可用栈内存的容量，如果您选择“中断”按钮，调用堆栈窗口会告诉您出了什么问题。您有 operator> () 函数的连续调用，因此它一定是在调用自身。如果查看代码，您可以看到原因：一个拼写错误。函数体中的单行应为：

```
return name < *this;
```

您可以修复它，重新编译，然后再试一次。这次它能正确工作，但不幸的是类仍然有缺陷。它存在内存泄漏，在这里没有症状，但在其他上下文中可能会造成混乱。内存泄漏通常很难检测，但您可以从 Visual C++ 2005 获得一些额外帮助。

## 调试动态内存

动态分配内存是错误的重要来源，也许在这种情况下最常见的错误是内存泄漏。只是提醒您，内存泄漏是指您使用 new 运算符分配内存，但在完成后从未使用 delete 运算符再次释放它。除了只是忘记删除已分配的内存外，您还应特别注意

类层次结构中的非虚析构函数也可能导致此问题——因为它可能导致在销毁对象时调用错误的析构函数，正如您所见。当然，当您的程序结束时，所有内存都会被释放；然而，在程序运行期间，它仍然分配给您的程序。内存泄漏在很多时候没有明显的症状，在某些情况下可能永远不会有，但内存泄漏会损害机器的性能，因为内存被占用而没有起到任何作用。有时，这可能导致程序在所有可用内存都被分配后发生灾难性故障。

对于检查程序对自由存储的使用，Visual C++ 2005 提供了多种诊断例程；这些例程使用自由存储的特殊调试版本。这些例程在头文件 crt dbg.h 中声明。对这些例程的所有调用都会自动从程序的发布版本中删除，因此您无需担心为它们添加预处理器控制。

## 检查自由存储的函数

以下是检查自由存储操作和如何检测内存泄漏所涉及内容的概述。crt dbg.h 中声明的函数使用存储在 _CrtMemState 类型结构中的记录来检查自由存储。此结构相对简单，定义如下：

```
typedef struct _CrtMemState
{
    struct _CrtMemBlockHeader* pBlockHeader; // Ptr to most recently allocated block
    unsigned long lCounts[_MAX_BLOCKS];       // Counter for each type of block
    unsigned long lSizes[_MAX_BLOCKS];// Total bytes allocated in each block type
    unsigned long lHighWaterCount;      // The most bytes allocated at a time up to now
    unsigned long lTotalCount;          // The total bytes allocated at present
} _CrtMemState;
```

您不会直接关心自由存储状态的细节，因为您使用的是以更易读形式呈现信息的函数。跟踪自由存储操作涉及相当多的函数，但您只会查看其中最有趣的五个。这些函数为您提供以下功能：

- 在任何一点记录自由存储的状态
- 确定自由存储的两个状态之间的差异
- 输出状态信息
- 输出自由存储中对象的相关信息
- 检测内存泄漏

以下是这些函数的声明以及它们所做的简要说明：

```
void _CrtMemCheckpoint(_CrtMemState* state);
```

这会将自由存储的当前状态存储在 _CrtMemState 结构中。您传递给函数的参数是指向要记录状态的 _CrtMemState 结构的指针。

```
int _CrtMemDifference(_CrtMemState* stateDiff,
    const _CrtMemState* oldState,
    const _CrtMemState* newState);
```

