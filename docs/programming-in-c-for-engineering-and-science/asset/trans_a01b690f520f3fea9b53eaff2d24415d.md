

| 描述 | array/vector<T> 效率 | list<T> 效率 |
|---|---|---|
| 追加一个值 | O(1) | O(1) |
| 在位置 i 插入一个值 | O(n) | O(1)† |
| 删除所有值 | O(n) | O(n) |
| 检查是否存在一个值 | O(n) | O(n) |
| 比较两个容器 | O(n) | O(n) |
| 获取索引 i 处的值 | O(1) | O(n) |
| 查找值的首次出现索引 | O(n) | O(n) |
| 检查容器是否为空 | O(1) | O(1) |
| 查找值的最后一次出现索引 | O(n) | O(n) |
| 删除索引 i 处的值 | O(n) | O(1)† |
| 删除值的首次出现 | O(n) | O(1)† |
| 用一个值替换索引 i 处的对象 | O(1) | O(n) |
| 返回容器中的值数量 | O(1) | O(1) |
| † 这些当然要求迭代器首先被定位，这是一个 O(n) 操作。 | | |

## 15.5 指针和命令行参数

正如我们现在所知，每个 C++ 程序都有一个名为 main 的函数。main 函数与其它程序员定义的函数在许多方面有所不同。其中一个区别是，参数会通过指针数组传递给 main 函数。如何做到这一点是本节的主题。

main 函数不能直接调用。相反，我们可以认为它在程序执行时被调用。在 Unix 操作系统等命令行环境中，程序是通过在操作系统提示符后输入其名称来执行的。例如，在 Unix 系统上，操作系统提示符通常是 $ 符号，因此要在运行 Unix 的计算机上调用文本编辑器 emacs，我们可能会输入命令

```
$ emacs
```

程序就会开始执行。在任何命令行环境中，在命令行上输入 C++ 程序的名称都可以看作是对该程序的 main 函数的调用。

要在 Unix 环境中编辑 C++ 文件，我们可以输入如下形式的命令

```
$ emacs FileName
```

以这种方式调用时，程序（emacs）开始执行，搜索名为 FileName 的文件，并在找到后打开它以供编辑。在此示例中，我们希望编辑的文件（FileName）是命令行参数的示例。就像输入程序名称（emacs）类似于调用程序的 main 函数一样，输入程序名称后跟 FileName 就类似于调用程序的 main 函数并将 FileName 作为参数传递给它。

命令行参数在 Unix 等命令行环境中的许多系统命令中使用。例如，命令 mkdir projects 用于

argv[n-1] 的值是命令行第 n 个字符串的地址。

为了说明，考虑示例 15.3 中的简单 C++ 程序。

### 示例 15.3 介绍 argc 和 argv

```
/* Program to introduce the predefined parameters argc and argv.

    Output: The value of argc, followed by each string in argv.
    ---------------------------------------------------------------------------*/

#include <iostream>
using namespace std;

int main(int argc, char * argv[])
{
    cout << "\nThere are " << argc
         << " strings on the command line:\n";

    for (int i = 0; i < argc; i++)
        cout << '\t' << "argv[" << i << "] contains: "
             << argv[i] << endl;
}
```

在此程序中，main 函数的参数列表包含 argc 和 argv 的声明。如果此程序的编译版本存储在名为 commandLine 的文件中，则可以通过输入命令执行 commandLine

```
$ commandLine
```

输出为

```
There are 1 strings on the command line:
    argv[0] contains: commandLine
```

因此，在 commandline 中，argc 的值为 1，且 argv[0] 引用字符字符串 commandline。如果我们通过输入命令执行 commandline

```
$ commandLine I want an argument
```

输出将为

```
There are 5 strings on the command line:
    argv[0] contains: commandLine
    argv[1] contains: I
```

```
argv[2] contains: want
argv[3] contains: an
argv[4] contains: argument
```

从这些示例可以明显看出，argc 和 argv 的值取决于用户在调用程序时在命令行上输入的内容。如果用户输入程序名称后跟 i 个参数，则 argc 的值将为 i + 1，即在命令行上输入的字符字符串的数量；argv[0] 将引用程序的名称；argv[1] 到 argv[i] 将引用输入的 i 个参数。

### 15.5.2 示例：平方根计算器

作为 argv 和 argc 用法的简单说明，考虑设计一个平方根计算器的任务，该计算器允许用户在命令行上输入要处理的值，然后计算并显示每个值的平方根。例如，如果输入命令

```
$ sroot 4 9 16 25
```

则应显示值 2、3、4 和 5。

由于程序必须处理命令行参数，因此它通过 main 函数的参数（即 argc 和 argv）接收参数。用户可能输入的内容有以下几种可能性：

```
$ sroot                  // error—no data to process (argc is 1)
$ sroot A                // error—nonnumeric data (argc is 2, argv[1] is "A")
$ sroot -1               // error—negative data (argc is 2, argv[1] is "-1")
$ sroot 9                // one value (argc is 2, argv[1] is "9")
$ sroot 4 9              // two values (argc is 3, argv[1] is "4", argv[2] is "9")
```

从第一个示例我们可以看到，有效输入要求 argc > 1。此外，每个 argv[i] 引用一个字符字符串，我们必须对类型为 double 的值求平方根。这意味着存储在 argv[i] 中的字符字符串必须转换为相应的 double 值。幸运的是，C++ 在 cstdlib 中提供了 strtod() 函数来执行此操作。该函数也可以用来使我们的程序更健壮，通过检查其返回值——strtod() 如果无法将字符串转换为数值则返回 0，这就是第二个和第三个示例中的情况。一旦我们将字符字符串转换为相应的 double 值，剩下的就是求其平方根，这很容易，使用 cmath 中声明的 sqrt() 函数。然后我们只需显示该值及其平方根。

因此我们可以构建以下算法，该算法检查是否至少给出了一个命令行参数，如果给出，则使用循环处理每个参数。

### sroot 算法

+   1. 如果 argc 小于 2，则显示“使用不正确”错误消息并退出。

+   2. 对于范围 1 到 argc − 1 中的每个整数 i：

+   a. 获取 inValue，即参数 i 的 double 等价值。

+   b. 如果 inValue > 0
+   显示 inValue 及其平方根。
+   否则
+   显示“无效数据”错误消息。

将此算法编码为 C++ 很直接，如示例 15.4 所示。

### 示例 15.4 编码 sroot

```
/* Program to display the square roots of a sequence of values,
   specified by the user on the command line.

   Receive: One or more numeric (double) values
   Output: The square roots of the input values
   ------------------------------------------------------------ */

#include <iostream>               // cin, cout, <<, >>
#include <cmath>                  // sqrt()
#include <cstdlib>                // strtod()
using namespace std;

int main(int argc, char * argv[])
{
    if (argc < 2)
    {
        cout << "\n*** Usage: sroot List-of-Positive-Numbers \n\n";
        exit(1);
    }

    double inValue;               // double equivalent of an argument

    for (int i = 1; i < argc; i++)
    {
        inValue = strtod(argv[i], 0);
        cout <<"\n--> The square root of " << inValue
             << " is" << sqrt(inValue) << endl;
    }
}
```

### 示例运行：

./sroot 1 2 3 4 5 6
--> The square root of 1 is 1

+   --> The square root of 2 is 1.41421
+   --> The square root of 3 is 1.73205
+   --> The square root of 4 is 2
+   --> The square root of 5 is 2.23607
+   --> The square root of 6 is 2.44949

## 章节总结

+   address-of operator (&)
+   anonymous variable
+   assignment operator
+   base address
+   circular linked list
+   class pointer selector operator (->)
+   command-line environment
+   compile-time allocation
+   constant time
+   delete operation
+   doubly linked list
+   gateway
+   head node
+   indirection operator (*)
+   Internet Protocol (IP)
+   IP address
+   iterator
+   linear time
+   linked list
+   memory leak
+   new operation
+   node
+   null address
+   null pointer value
+   O(1)
+   O(n)
+   pointer
+   pointer variable
+   reference
+   run-time allocation
+   singly linked list
+   sizeof operator
+   time-efficiency

+   • 在声明中，星号运算符 * 必须置于作为指针的每个标识符之前。
+   • 0 可以赋给任何指针变量；它被称为空指针，也称为空地址。
+   • 赋给指针变量的值必须是其在声明中绑定的类型的对象的地址。

