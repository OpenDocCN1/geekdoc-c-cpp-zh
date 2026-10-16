

```
int main()
{
    cout << "C++ is better than C.\n";  // C++ statement
    
    return 0;
}           // End of example
```

这个简单的程序演示了几个 C++ 特性。

## 程序特性

与 C 语言一样，C++ 程序是由函数组成的集合。上面的例子只包含一个函数 main()。通常，执行从 main() 开始。每个 C++ 程序都必须有一个 main()。C++ 是一种自由格式语言。除了少数例外，编译器会忽略回车和空白。与 C 语言一样，C++ 语句以分号结束。

## 注释

C++ 引入了新的注释符号 //（双斜杠）。注释以双斜杠符号开始，并在行尾结束。注释可以开始于行的任何位置，其后直到行尾的内容将被忽略。请注意，没有结束符号。

双斜杠注释基本上是单行注释。多行注释可以写成如下形式：

```
//  This is an example of
//  C++ program to illustrate
//  Some of its features
```

C 注释符号 /*、*/ 仍然有效，且更适合多行注释。以下注释是允许的：

```
/*  This is an example of
    C++ program to illustrate
    some of its features
*/
```

我们可以在程序中使用其中一种或两种风格。由于这是一本关于 C++ 的书，我们将只使用 C++ 风格。然而，请记住，我们不能在程序行的文本中插入 // 风格的注释。例如，双斜杠注释不能按如下所示的方式使用：

```
for(j=0; j<n; /* loops n times */ j++)
```

## 输出运算符

程序 2.1 中唯一的语句是输出语句。语句

```
cout << "C++ is better than C.";
```

会导致引号中的字符串显示在屏幕上。该语句引入了两个新的 C++ 特性，cout 和 <<。标识符 cout（读作‘C out’）是一个预定义对象，表示 C++ 中的标准输出流。这里，标准输出流表示屏幕。输出也可以重定向到其他输出设备。我们稍后将详细讨论流。

运算符 << 被称为插入或 put to 运算符。它将右侧变量的内容插入（或发送）到左侧的对象（图 2.1）。

![](img/58ab8f034e2127e80560390a921c2523_35_0.png)

图 2.1 ⇔ 使用插入运算符输出

对象 cout 具有简单的接口。如果 string 表示一个字符串变量，则以下语句将显示其内容：

```
cout << string;
```

你可能记得运算符 << 是按位左移运算符，它仍然可以用于此目的。这是一个运算符可以根据上下文用于不同目的的例子。这个概念被称为运算符重载，是多态性的一个重要方面。运算符重载将在第 7 章详细讨论。

需要注意的是，我们仍然可以使用 printf() 来显示输出。C++ 接受这种记法。然而，我们将使用 cout << 以保持 C++ 的精神。

## iostream 文件

我们在程序中使用了以下 #include 指令：

```
#include <iostream>
```

该指令导致预处理器将 iostream 文件的内容添加到程序中。它包含标识符 cout 和运算符 << 的声明。一些旧版本的 C++ 使用名为 iostream.h 的头文件。这是 ANSI C++ 引入的更改之一。（如果编译器不支持 ANSI C++ 特性，我们应该使用 iostream.h。）

头文件 iostream 应该包含在所有使用输入/输出语句的程序开头。请注意，头文件的命名约定可能有所不同。一些实现使用 iostream.hpp；还有一些使用 iostream.hxx。我们必须根据程序的内容和实现包含适当的头文件。

表 2.1 和表 2.2 提供了 C++ 程序中可能需要的 C++ 标准库头文件列表。带 .h 扩展名的头文件是“旧式”文件，应与旧编译器一起使用。表 2.1 还给出了应与 ANSI 标准编译器一起使用的这些文件的版本。

## 表 2.1 常用旧式头文件

| Header file | Contents and purpose | New version |
| <assert.h> | Contains macros and information for adding diagnostics that aid program debugging | <cassert> |
| <ctype.h> | Contains function prototypes for functions that test characters for certain properties, and function prototypes for functions that can be used to convert lowercase letters to uppercase letters and vice versa. | <cctype> |
| <float.h> | Contains the floating-point size limits of the system. | <cfloat> |
| <limits.h> | Contains the integral size limits of the system. | <climits> |
| <math.h> | Contains function prototypes for math library functions. | <cmath> |
| <stdio.h> | Contains function prototypes for the standard input/output library functions and information used by them. | <cstdio> |
| <stdlib.h> | Contains function prototypes for conversion of numbers to text, text to numbers, memory allocation, random numbers, and various other utility functions. | <cstdlib> |
| <string.h> | Contains function prototypes for C-style string processing functions. | <cstring> |

## 表 2.1 （续）

| Header file | Contents and purpose | New version |
|---|---|---|
| <time.h> | Contains function prototypes and types for manipulating the time and date. |  |
| <iostream.h> | Contains function prototypes for the standard input and standard output functions. | <iostream> |
| <iomanip.h> | Contains function prototypes for the stream manipulators that enable formatting of streams of data. | <iomanip> |
| <fstream.h> | Contains function prototypes for functions that perform input from files on disk and output to files on disk. | <fstream> |

## 表 2.2 ANSI C++ 中包含的新头文件

| Header file | Contents and purpose |
|---|---|
| <utility> | Contains classes and functions that are used by many standard library header files. |
| <vector>, <list>, <deque> <queue>, <set>, <map>, <stack>, <bitset> | The header files contain classes that implement the standard library containers. Containers store data during a program's execution. We discuss these header files in Chapter 14. |
| <functional> | Contains classes and functions used by algorithms of the standard library. |
| <memory> | Contains classes and functions used by the standard library to allocate memory to the standard library containers. |
| <iterator> | Contains classes for manipulating data in the standard library containers. |
| <algorithm> | Contains functions for manipulating data in the standard library containers. |
| <exception>, <stdexcept> | These header files contain classes that are used for exception handling. |
| <string> | Contains the definition of class string from the standard library. Discussed in Chapter 15 |
| <sstream> | Contains function prototypes for functions that perform input from strings in memory and output to strings in memory. |
| <locale> | Contains classes and functions normally used by stream processing to process data in the natural form for different languages (e.g., monetary formats, sorting strings, character presentation, etc.) |
| <limits> | Contains a class for defining the numerical data type limits on each computer platform. |
| <typeinfo> | Contains classes for run-time type identification (determining data types at execution time). |

## 命名空间

命名空间是 ANSI C++ 标准委员会引入的一个新概念。它为程序中使用的标识符定义了一个作用域。为了使用命名空间作用域中定义的标识符，我们必须包含 using 指令，如

```
using namespace std;
```

这里，std 是 ANSI C++ 标准类库定义的命名空间。所有 ANSI C++ 程序都必须包含此指令。这会将 std 中定义的所有标识符带入当前全局作用域。using 和 namespace 是 C++ 的新关键字。命名空间将在第 16 章详细讨论。

## main() 的返回类型

在 C++ 中，main() 将整数类型值返回给操作系统。因此，每个 C++ 中的 main() 都应以 return(0) 语句结束；否则可能会出现警告或错误。由于 main() 返回整数类型值，main() 的返回类型明确指定为 int。请注意，C++ 中所有函数的默认返回类型为 int。以下没有类型和返回的 main 将会发出警告运行：

```
main()
{
      ......
      ......
}
```

## 2.4 更多 C++ 语句

让我们考虑一个稍微复杂一点的 C++ 程序。假设我们想从键盘读取两个数字并在屏幕上显示它们的平均值。完成此操作的 C++ 语句如程序 2.2 所示。

![](img/58ab8f034e2127e80560390a921c2523_38_0.png)

```
#include <iostream>

using namespace std;

int main()
{
    float number1, number2,
          sum, average;
```

(Contd)

