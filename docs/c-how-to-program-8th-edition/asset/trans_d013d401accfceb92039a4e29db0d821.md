

```cpp
// Fig. F.3: figF_03.cpp
// Using command-line arguments
#include <iostream>
#include <fstream>
using namespace std;

int main( int argc, char *argv[] )
{
    // check number of command-line arguments
    if ( argc != 3 )
        cout << "Usage: copyFile infile_name outfile_name" << endl;
    else
    {
        ifstream inFile( argv[1], ios::in );

        // input file could not be opened
        if ( !inFile )
        {
            cout << argv[1] << " could not be opened" << endl;
            return -1;
        } // end if

        ofstream outFile( argv[2], ios::out );

        // output file could not be opened
        if ( !outFile )
        {
            cout << argv[2] << " could not be opened" << endl;
            inFile.close();
            return -2;
        } // end if

        char c = inFile.get(); // read first character

        while ( inFile )
        {
            outFile.put( c );  // output character
            c = inFile.get();  // read next character
        } // end while
    } // end else
} // end main
```

**图 F.3** 使用命令行参数。

此命令行指示将输入文件复制到输出文件。程序执行时，如果 argc 不为 3（copyFile 算作参数之一），程序会打印错误消息（第 11 行）。否则，argv 包含字符串 "copyFile"、"input" 和 "output"。命令行上的第二和第三个参数被程序用作文件名。通过创建 ifstream 对象 inFile 和 ofstream 对象 outFile 来打开文件（第 14 行和第 23 行）。如果两个文件都成功打开，则使用成员函数 get 从输入文件读取字符，并使用成员函数 put 写入输出文件，直到输入文件的文件结束指示符被设置（第 35–39 行）。然后程序终止。结果是输入文件的精确副本。请注意，并非所有计算机系统都像 UNIX、LINUX、Mac OS X 和 Windows 那样容易支持命令行参数。例如，某些 VMS 和较旧的 Macintosh 系统需要特殊设置来处理命令行参数。有关命令行参数的更多信息，请参阅系统手册。

## F.5 编译多源文件程序的注意事项

如前文所述，构建由多个源文件组成的程序是很正常的（参见第 9 章）。创建多文件程序时需要考虑几个问题。例如，函数的定义必须完全包含在一个文件中——它不能跨越两个或更多文件。

在第 6 章中，我们介绍了存储类和作用域的概念。我们了解到，在任何函数定义之外声明的变量默认为存储类 static，称为全局变量。全局变量可被同一文件中在变量声明之后定义的任何函数访问。全局变量也可被其他文件中的函数访问；然而，全局变量必须在每个使用它们的文件中声明。例如，如果我们在一个文件中定义全局整数变量 flag，并在第二个文件中引用它，则第二个文件必须包含声明

```cpp
extern int flag;
```

在该文件中使用该变量之前。在前面的声明中，存储类说明符 extern 向编译器指示变量 flag 要么在同一文件的后部定义，要么在不同的文件中定义。编译器通知链接器该文件中出现了对变量 flag 的未解析引用。（编译器不知道 flag 在哪里定义，因此它让链接器尝试查找 flag。）如果链接器无法定位 flag 的定义，则报告链接器错误。如果找到了正确的全局定义，链接器将通过指出 flag 的位置来解析这些引用。

> **性能提示 F.1**
>
> *全局变量能够提高性能，因为任何函数都可以直接访问它们——消除了向函数传递数据的开销。*

> **软件工程观察 F.2**
>
> *除非应用程序性能至关重要，或者变量表示诸如 cin 之类的共享全局资源，否则应避免使用全局变量，因为它们违反了最小权限原则，并使软件难以维护。*

正如 extern 声明可用于向其他程序文件声明全局变量，函数原型可用于在其他程序文件中声明函数。（函数原型中不需要 extern 说明符。）这可以通过在每个调用函数的文件中包含函数原型，然后编译每个源文件并将生成的目标代码文件链接在一起来实现。函数原型向编译器指示指定函数在同一文件的后部或在不同的文件中定义。编译器不尝试解析对此类函数的引用——该任务留给链接器。如果链接器无法定位函数定义，则会产生错误。

作为使用函数原型扩展函数作用域的一个示例，请考虑任何包含预处理指令 `#include <cstring>` 的程序。该指令

```cpp
// display message before termination
void print()
{
    cout << "Executing function print at program termination\n"
         << "Program terminated" << endl;
} // end function print
```

```
Enter 1 to terminate program with function exit
Enter 2 to terminate program normally
2

Terminating program by reaching the end of main
Executing function print at program termination
Program terminated
```

```
Enter 1 to terminate program with function exit
Enter 2 to terminate program normally
1

Terminating program with function exit
Executing function print at program termination
Program terminated
```

**图 F.4** | 使用函数 exit 和 atexit。（第 2 部分，共 2 部分。）

使用函数 exit 终止程序只会运行程序中静态和全局对象的析构函数。使用函数 abort 终止程序则不会运行任何析构函数。

## F.7 类型限定符 volatile

**volatile** 类型限定符应用于可能被程序外部修改的变量定义（即该变量不完全受程序控制）。因此，编译器无法执行那些依赖于“知道”变量行为仅受编译器可观察的程序活动影响的优化（例如加速程序执行或减少内存消耗）。

## F.8 整数和浮点常量的后缀

C++ 提供了整数和浮点后缀，用于指定整数和浮点常量的类型。整数后缀有：**u** 或 **U** 表示 **unsigned** 整数，**l** 或 **L** 表示 **long** 整数，**ul** 或 **UL** 表示 **unsigned long** 整数。以下常量分别属于 unsigned、long 和 unsigned long 类型：

```
174u
8358L
26373ul
```

如果整数常量没有后缀，其类型为 int；如果该常量无法存储在 int 中，则存储在 long 中。

浮点后缀是：**f** 或 **F** 表示 float，**l** 或 **L** 表示 *long double*。以下常量分别属于 long double 和 float 类型：

```
3.14159L
1.2F
```

没有后缀的浮点常量的类型为 double。带有不当后缀的常量会导致编译器警告或错误。

## F.9 信号处理

意外事件，即**信号**，可以提前终止程序。此类事件包括**中断**（在 UNIX、LINUX、Mac OS X 或 Windows 系统上按**\<Ctrl\> C**）、**非法指令**、**段错误**、**操作系统的终止命令**和**浮点异常**（除以零或乘以大的浮点数值）。**信号处理库**提供了 signal 函数来**捕获意外事件**。**signal** 函数接收两个参数——一个整数信号编号和一个指向信号处理函数的指针。信号可以由 **raise** 函数生成，它接受一个整数信号编号作为参数。图 F.5 总结了头文件 **\<signal\>** 中定义的标准信号。下一个示例演示了函数 signal 和 raise。

图 F.6 使用函数 signal 捕获交互信号（SIGINT）。程序以 SIGINT 和一个指向函数 signalHandler 的指针调用 signal。（回想一下，函数名就是指向该函数的指针。）当发生 SIGINT 类型的信号时，将调用函数 signalHandler，打印一条消息，并让用户选择是否继续正常执行程序。如果用户希望继续执行，则通过再次调用 signal 来重新初始化信号处理程序（某些系统要求重新初始化信号处理程序），然后控制返回到程序中检测到信号的位置。在该程序中，函数 raise 用于模拟交互信号。选择一个 1 到 50 之间的随机数。如果该数字是 25，则调用 raise 来生成信号。通常，交互信号是在程序外部发起的。例如，在 UNIX、LINUX、Mac OS X 或 Windows 系统上，在程序执行期间按 **\<Ctrl\> C** 会生成一个终止程序执行的交互信号。可以使用信号处理来捕获交互信号并阻止程序终止。

| 信号 | 说明 |
|---|---|
| SIGABRT | 程序的异常终止（例如调用 abort）。 |
| SIGFPE | 错误的算术运算，例如除以零或导致溢出的运算。 |
| SIGILL | 检测到非法指令。 |
| SIGINT | 收到交互注意信号。 |
| SIGSEGV | 对存储器的无效访问。 |
| SIGTERM | 发送给程序的终止请求。 |

**图 F.5** | 头文件 **\<csignal\>** 中定义的信号。

