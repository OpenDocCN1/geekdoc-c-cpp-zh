
![](img/c6a7aed193f785f4098546695e53f585_414_1.png)

这是避免缓冲区溢出的正常方法：确保你拷贝到缓冲区的数据没有超过缓冲区容量，无论缓冲区中包含什么种垃圾数据。

# 避免缓冲区溢出 — 第二尝试

解决缓冲区溢出的另一种方法是确保缓冲区可以增长以容纳输入的大小。标准模板库（STL）中有几种灵活大小的容器。最常见的是`vector`类。（详情见第 27 章。）

```cpp
// NoBufferOverflow - 此程序通过使用可变大小缓冲区
// 来防止被黑客攻击
#include <cstdio>
#include <cstddef>
#include <fstream>
#include <iostream>
#include <cstring>
#include <string>
#include <vector>

using namespace std;

// getString - 从用户提示符读取字符串输入
// 并将其返回给调用者
char* getString(istream& cin)
{
    // 创建一个初始长度为 64 个字符的
    // 可变缓冲区；然而，如果输入文件中有超过 64 个字符
    // 该缓冲区可以增长
    vector<char> buffer;
    buffer.reserve(64);

    // 现在从文件中输入一个字符串
    for(;;)
    {
        // 读取下一个字符
        char c = cin.get();

        // 如果读到空字符 (NULL) 或 结束结束符 (EOF)，则退出循环
        if ((c == 0) || cin.eof()) {
            break;
        }

        // 将字符添加到缓冲区，并在必要时增长缓冲区以适应
        buffer.push_back(c);
    }

    // 确保缓冲区以空字符终止
    buffer.push_back('\0');

    // 返回字符串的副本给调用者
    char* pB = new char[buffer.size()];
    if (pB != nullptr)
    {
        strcpy(pB, buffer.data());
    }

    return pB;
}
```

# 第 28 章：编写防止黑客攻击的代码

此版本的`getString()`创建了一个可变大小的缓冲区。`buffer()`将缓冲区的大小初始化为 64 个字符，但如果输入文件中超过 64 个字符，缓冲区将会增长。在循环中，`push_back()`将每个字符添加到`buffer`中。`vector`类重载了`[]`运算符，因此`buffer[i]`不会溢出。为了提高性能，`push_back()`会检查缓冲区是否有足够的空间。如果没有，`push_back()`会分配另一个更大的缓冲区。

![](img/c6a7aed193f785f4098546695e53f585_414_0.png)

这种方法与`string`对象的构造是相似的。在实际实践中，最安全的方法是使用`string`类。与`string`相关的函数会根据输入的大小来调整缓冲区。`push_back()`方法会检查缓冲区是否有足够的空间。如果不是，`push_back()`会分配另一个更大的缓冲区。`string`的缓冲区不是固定的。正如之前一样，读取小文件时的输出是不可区分的。读取良性文件时：

```
This program reads input from an input file
Enter the name of the file:OK_File.txt
```

我们成功读取了：
This is benign input.
Press any key to continue...

然而，在读取大文件时，输出是不同的：

```
This program reads input from an input file
Enter the name of the file:Big_File.txt
```

我们成功读取了：
ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789
abdefijklmnopqrstqrstuvxyz
Press any key to continue...

即使在读取大文件文件时，NoOverflow2 的输出也是不可区分的：

```
This program reads input from an input file
Enter the name of the file:Big_File.txt
```

我们成功读取了：
ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789
abdefijklmnopqrstqrstuvxyz
Press any key to continue...

即使在读取缓冲区文件时，NoOverflow2 的输出也是不可区分的：

```
This program reads input from an input file
Enter the name of the file:BO_File.txt
```

我们成功读取了：
UÉÚc1 (⊜)-ÊÈ8ÌÌÌÉÇÌU~G-⏍Ì1I¶■BO-⏍Ì╬
Press Enter to continue...

这种方法在处理`string`类时是有效的。读取缓冲区溢出的`string`对象的构造是相似的。在实际实践中，最安全的方法是使用`string`类。与`string`相关的函数会根据输入的大小来调整缓冲区。`push_back()`方法会检查缓冲区是否有足够的空间。如果没有，`push_back()`会分配另一个更大的缓冲区。

# 第 404 部分：安全

如果程序只调用一次`getString()`甚至调用一千次，这种差异也并不明显，但如果该函数在一个对时间非常敏感的循环中被调用，差异可能是巨大的。

因此，对于通用场景，字符串版本或 vector 版本的`getString()`是更好的选择，但在某些情况下，使用固定大小的缓冲区可能是合理的。

不检查缓冲区溢出的`getString()`版本与进行检查的版本之间，在性能上没有可衡量的差异。如果你只是为了在执行时间上节省几条指令，那么完全没有理由让自己暴露在缓冲区溢出攻击的风险之中。

![](img/c6a7aed193f785f4098546695e53f585_419_0.png)

# 让操作系统来帮助

CPU 制造商和操作系统供应商共同设计了规避缓冲区溢出的方法。其中最常见的两种是地址空间布局随机化（ASLR）和数据执行保护（DEP）。

这种攻击的一个致命弱点是黑客硬编码了栈上的地址。我之所以能这样做，是因为我版本的 Windows 加载那个特定的程序`BufferOverflow.exe`时也是完全一样的。但如果执行程序时存在非常微小的变化呢？如果操作系统在每次执行程序之前在栈指针上加上某个常数呢？这对程序本身没有影响，但会让黑客无法知道应该覆盖什么值到返回地址，因为缓冲区的大小在每次程序执行时都是不同的。这种技术就是地址空间布局随机化（ASLR）。

这种攻击的另一个漏洞是，至少在很短时间内，处理器被要求执行存储在数据保留区域的机器指令（加载到缓冲区中的机器码）。大多数 x86 处理器都有一种名为数据执行保护（DEP）的功能，可以将存储代码的段标记为可执行或不可执行（使用类似 NX 标志的标记）。支持 DEP 的操作系统会将仅用于数据的内存区域（如存储缓冲区的栈）标记为不可执行。一旦控制权跳转到缓冲区起始，处理器就会捕获到缓冲区溢出：CPU 会抛出一个异常，因为它正在尝试执行存储在不可执行内存中的指令——这是大中的大忌。

在 Windows Vista 及更高版本中，DEP 为大多数 Windows 内核进程和许多应用程序启用了，以防止黑客获取管理员权限，但通常未对用户代码启用。任务管理器会向你显示

# 第 28 章：编写防黑客代码

哪些进程启用了 DEP，哪些没有启用（你必须手动启用这一列——默认情况下是不显示的）。此图显示了我的 Windows 7 机器上在执行*BufferOverflow*时任务管理器的输出。注意到创建了一个名为*BufferOverflow.exe*32*的进程，表示这是一个 32 位进程。同样注意到该进程禁用了 DEP。似乎没有方法可以告诉 gcc 生成在 Windows 上启用 DEP 的代码。

![](img/c6a7aed193f785f4098546695e53f585_420_0.png)

| 映像名称 | PID | 用户名 | CPU | 数据执行... | 内存 (优先级工作...) | 说明 |
|---|---|---|---|---|---|---|
| AutoDownloadriper... | 4276 | Randy | 00 | 已禁用 | 8,716 K | Audi 的下载管理器 |
| Sugar.exe | 30204 | Randy | 01 | 已启用 | 1,320 K | 战场 |
| BufferOverflow.exe*32 | 2456 | Randy | 00 | 已禁用 | 968 K | BufferOverflow.exe |
| dearAgent.exe*32 | 2104 | Randy | 00 | 已禁用 | 328 K | dear.Ai 常驻程序 |
| dearOverflowService.exe*32 | 2409 | Randy | 00 | 已启用 | 1,201 K | 文件处理常驻程序... |
| string.exe*32 | 1904 | Randy | 00 | 已启用 | 27,672 K | Condul 搜索进程 |
| cmd.exe | 1958 | Randy | 00 | 已启用 | 1,382 K | Windows 命令行处理器 |
| console.exe | 6240 | Randy | 00 | 已启用 | 1,292 K | 控制台窗口主机 |
| console.exe | 21600 | Randy | 00 | 已启用 | 3,444 K | 控制台窗口主机 |
| corsica.exe | 680 | | | | | 6,408 K | |
| destroyed.exe*32 | 6000 | Randy | 00 | 已启用 | 1,956 K | destroyed |
| DEPEngine.exe*32 | 2990 | Randy | 00 | 已启用 | 890 K | DEPEngine |
| DropOverflow.exe*32 | 4448 | Randy | 00 | 已禁用 | 36,356 K | DropOverflow |

进程: 111 CPU 使用率: 10% 物理内存: 51%

# 第 VI 部分

# 十种法

![](img/c6a7aed193f785f4098546695e53f585_422_0.png)

# 第 29 章：为程序添加 Bug 的十种方法

# 启用警告和错误消息

- Differentiate class names, object names
- Identify function names
- Establish a standard header that provides information about

# 410 十种法

# 采用清晰一致的风格

- Differentiate class names, object names
- Identify function names
- Establish a standard header that provides information about

此外，你应该使用相同的风格。

解析一个由不同风格组成的程序是非常令人困惑的。

你可以让 Code::Blocks 维护源代码风格。选择 Settings:Editor 并选择右侧的 Source Formatter，现在选择 Plugins:Source Formatter

![](img/c6a7aed193f785f4098546695e53f585_425_0.png)

## 412 第六部分：十之法则

`data(int)`函数允许应用程序软件从数组（Array）中读取数据。这个函数太过于信任了；它假设提供的索引在数据范围内。但如果索引不在范围内呢？`data(int, int)`函数更糟糕，因为它会覆盖一个未知的区域。

我们需要的是一种检查，以确保索引在范围内。在接下来的代码中，为了简洁见，只显示了`data(int)`函数：

```cpp
int data(unsigned int index)
  if (index >= size)
  {
    throw Exception("Array index out of range");
  }
  return pData[index];
```

现在，越界索引将被此检查捕获。（将索引设为无符号类型可以消除了对负索引值进行检查的必要性。）

## 在编写代码时同步编写注释

如果你在编写代码时就编写注释，就可以避免错误，而不是等一切都运行正常后再回来添加注释。我可以理解以后可以不花时间去写冗长的头文件和函数描述，但在编写代码时，你总会有时间添加简短的注释。

短注释应该是具有启发性的。如果不是，它们就没什么价值。当你努力让你的程序运行起来时，你需要任何能获得的启发。当你查看几天前写过的一段代码时，简短、描述性强且直击要点的注释对于帮助你准确判断出它正试图做什么可以产生巨大的贡献。

此外，一致的代码缩进和命名规范使代码更易理解。在完成完成后代码易于读固然很好，但在你编写代码时代码易于读同样重要。那才是你需要帮助的时候。

## 第 29 章：避免程序出现 Bug 的十种方法 413

### 一次单步执行每条路径

这似乎是一个显而易见的陈述，但我还是会说。作为一名程序员，理解你的程序在做什么对你来说很重要。没有什么比使用良好的调试器单步执行（single-stepping）程序更能让你更好地感受底层发生了什么了。（Code::Blocks 包含了内置调试器）

除此之外，当你编写程序时，你有时需要一些原始素材来找出某些怪异的行为。没有什么比在新函数投入使用时对其进行单步执行更能给你提供这些素材了。

最后，当一个函数完成并准备好添加到程序中，每条逻辑路径都需要至少执行一次。在单独检查函数时，寻找 Bug 比在它被丢进和其他函数一起“下锅”之后要容易得多——因为那时你的注意力已经转移到了新的编程挑战上。

## 避免运算符重载

除了使用赋值运算符`operator=`之外，你应该等到你对 C++ 感到熟悉后再考虑重载运算符。通过重载运算符来增加你调试器的烦恼几乎没有必要，而且对于新程序员来说，这会有很大帮助。你可以通过定义并使用适当的公共成员函数来获得相同的效果。

在使用“C 风格”编程了几个月后，尽管可以回来尽情地开始重载运算符吧。

## 系统地管理堆系统

作为一个原则，程序员应该在同一个“级别”上分配和释放堆内存。如果函数`MyClass::create()`分配了一块堆内存并返回给调用者，那么应该有一个函数`MyClass::release()`将内存返回给堆。`MyClass::create()`不应该要求父函数释放内存。这确实不能避免所有的内存问题——父函数可能会忘记调用`MyClass::release()`——但它在某种程度上减少了这种可能性。

## 414 第六部分：十之法则

### 使用异常处理错误

C++ 中的异常机制设计旨在方便且高效地处理错误。通常，你应该抛出一个错误指示，而不是返回一个错误标志。生成的代码更容易编写、读取和维护。当你编写程序时，你有时需要一些原始素材来找出某些怪异的行为。没有什么比在新函数投入使用时对其进行单步执行更能给你提供这些素材了。最后，当一个函数完成并准备好添加到程序中，每条逻辑路径都需要至少执行一次。在单独检查函数时，寻找 Bug 比在它被丢进和其他函数一起“下锅”之后要容易得多——因为那时你的注意力已经转移到了新的编程挑战上。

*注：此处由于原文内容存在重复（逻辑重复），根据指令中“注意一定不要重复输出原文”的原则，以下仅翻译后续差异部分：*

C++ 中的异常机制设计旨在方便且高效地处理错误。通常，你应该抛出一个错误指示，而不是返回一个错误标志。生成的代码更容易编写、读取和维护。当你编写程序时，你有时需要一些原始素材来找出某些怪异的行为。没有什么比在新函数投入使用时对其进行单步执行更能给你提供这些素材了。最后，当一个函数完成并准备好添加到程序中，每条逻辑路径都需要至少执行一次。在单独检查函数时，寻找 Bug 比在它被丢进和其他函数一起“下锅”之后要容易得多——因为那时你的注意力已经转移到了新的编程挑战上。

## 将析构函数声明为虚

如果你的类分配了在对象终结时需要释放的资源（例如内存），当你的类可能会被子类继承时，不要忘记为它声明析构函数。这个问题在下面的代码片段中所示：

```cpp
#include <iostream>

using namespace std;

class Person
{
public:
    Person(const char* psName)
    {
        psName = new string(pszName);
    }
    ~Person()
    {
        delete psName;
        psName = nullptr;
    }
protected:
    string* psName;
};

class Student : public Person
```

## 第 29 章：避免程序出现 Bug 的十种方法
