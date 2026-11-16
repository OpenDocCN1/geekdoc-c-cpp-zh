

![](img/5340985153962870d4e4a3b9453b9146_14_0.png)

点击 File->New->Source File

或者直接按 Ctrl+N。现在，你将看到一个可以编写程序的空白区域。那么，我们开始吧，只需输入：

```
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello World";
    return 0;
}
```

现在按 F11 编译并运行程序，或者从菜单栏中找到 run、compile and run、build and run，选择其中任意一项来编译并运行程序。现在，系统会要求你保存程序

![](img/5340985153962870d4e4a3b9453b9146_15_0.png)

只需输入文件名并点击 Save 按钮，我建议将程序保存在桌面，以便我们可以看到幕后发生的一切。

现在，当你点击 Save 时，你将看到类似下面的内容：

![](img/5340985153962870d4e4a3b9453b9146_15_1.png)

现在，让我们逐行分析程序

```
#include<iostream>
```

- 它被称为预处理器。它用于特殊目的，其中最常见的有三个：
  - 包含一个文件
  - 定义一个宏
  - 使用条件

在这里，它被用来告诉编译器，我们将使用上述三项任务中的某一项。

include – 它是一个关键字，即那些为特殊目的保留并用于它们的字。这个关键字用于在程序中包含一个文件，这不仅仅意味着头文件，它可以是文本文件，甚至是 C 程序或 C++ 程序文件，或根据需要的其他一些文件。

<...> - 这是包含文件的一种格式。但是，你可以自由使用另一种格式，即“...”，因此我们也可以写 #include “iostream” 而不是 #include<iostream>

iostream – 它是一个名为头文件的预定义源代码。它包含对象 cout（读作 C out）的定义。iostream 中包含的另一个重要函数是 cin（读作 C in），用于扫描由标准输入设备（默认为键盘）给出的输入。

注意：请记住，如果你使用的是 turbo C++，则需要写 iostream.h 而不是 iostream，同样适用于用于文件处理的 fstream。

using namespace std; - Borland C++ 支持多个命名空间，这些命名空间用于长程序。我们甚至可以定义自己的命名空间。Turbo C++ 不支持多个命名空间。因此，using namespace std; 在那里没有意义。所以，你需要在 Turbo C++ 中删除这一行。

int main() – 在这里，main() 是一个函数。括号用于向函数传递参数。在这里，int 是函数返回的变量的返回类型。如果我们尝试用它来编写求和程序，会更容易理解。假设我们想要加两个数字并返回结果。因此，我们声明一个函数 int add(int a,int b)。在这里，我们提供两个数字 a 和 b，它们将被相加并返回结果。请记住，main() 是编译器编译的第一个函数，无论它上面或下面定义了多少个函数。

{...} – 所有语句都在其中声明和定义。这些花括号可以说将其中的所有语句绑定为一个整体。其他函数也在其中被调用。我们还根据需要在各种循环和条件中使用它。

cout – 这是一个带有 ‘<<’ 的对象，用于显示字符、字符串或数字。使用 cout 不仅可以显示一个，还可以显示许多。例如：cout<<1<<“Hello”<<“z”；

return 0 – 它用于将值返回给调用包含此 return 语句的函数的函数。例如，在以下函数中，return 用于返回两个数字的和。

```
int add(int a, int b)
{
    return a+b;
}
```

## 注释

注释是编译器忽略但能使程序更易读的行。例如，考虑以下程序

```
#include<iostream>
```

```
using namespace std;
```

```
int main()
{
 //This is a comment.
}
```

C++ 程序中支持两种类型的注释：

- 单行注释：对于单行注释，使用 //。例如：

```
#include<iostream>
using namespace std;
int main()
{
 //This is a single line comment.
}
```

- 多行注释：对于多行注释，我们通常使用以下结构：
  - /* 这是一个注释 */
  例如，考虑以下程序：

```
#include<iostream>
using namespace std;
int main()
{
 /*This is a
 multiple line
 comment*/
}
```

我们也可以使用多行注释符号来进行单行注释，例如：

```
#include<iostream>
using namespace std;
int main()
{
 /*This is a single line comment designed by multiple line comment symbol*/
}
```

我们也可以重复单行注释符号来设计多行注释，例如：

```
#include<iostream>
using namespace std;
int main()
{
    //This is a
    //multiple line
    //comments designed by
    //using single line comment symbol
    //multiple times.
}
```

![](img/5340985153962870d4e4a3b9453b9146_18_0.png)

## 变量、常量和关键字

计算机的金科玉律是：没有存储就无法使用任何东西。这并不意味着编译器总会显示值已被存储。包括 C++ 和 Python 在内的许多编程语言并不总是显示它们正在使用的值正在被存储。常量是定义后无法修改的数据类型。相反，变量是可以反复修改的数据类型。假设我们想要操作一个初始值为 5、最终值取决于中间操作的数字，那么我们将其存储在变量中，然后根据我们的意愿操作该变量。在变量部分，我们将学习如何在变量中存储和使用数字、字符和字符串。

### 字符集

C++ 程序中可以使用以下字符集

- **字母：** A,B,...,Z,a,b,...,z，
- **数字：** 0,1,...,9
- **特殊字符：** ~!@#$%^&*()-+=[]{}|;':",<>?/_

### 关键字

这些是为特殊目的所需的特殊单词。你不得将其用作变量名，否则编译器会显示错误。这些单词将在需要的地方详细讨论。现在让我们看看程序中使用的关键字

| asm | auto | bool | break | case | catch | char | class |
| --- | --- | --- | --- | --- | --- | --- | --- |
| const | const_cast | continue | default | delete | do | double | dynamic_cast |
| else | enum | explicit | export | extern | false | float | for |
| friend | goto | if | inline | int | long | mutable | namespace |
| new | operator | private | protected | public | register | reinterpret_cast | return |
| short | signed | sizeof | static | static_cast | struct | switch | template |
| this | throw | true | try | typedef | typeid | typename | union |
| unsigned | using | virtual | void | volatile | wchar_t | while |

### 变量

变量是内存位置的别名，其中可以存储一些数据。例如：

```
int num=5;
```

在这个赋值中，值 5 被赋给变量 num，它是一个 int 类型变量。现在，一个基本问题出现了。我们可以在整数类型变量中存储任何数字吗？答案是否定的。以下是我们可以使用的数据类型的范围：

| Data type | 32 bit compiler | 64 bit compiler |
|---|---|---|
| char | 1 | 1 |
| unsigned char | 1 | 1 |
| signed char | 1 | 1 |
| short | 2 | 2 |
| unsigned short | 2 | 2 |
| signed short | 2 | 2 |
| int | 2 | 4 |
| unsigned int | 2 | 4 |
| signed int | 2 | 4 |
| long | 4 | 4 |
| unsigned long | 4 | 4 |
| signed long | 4 | 4 |
| float | 4 | 4 |
| unsigned float | 不存在 | |
| signed float | 不存在 | |
| double | 8 | 8 |
| unsigned double | 不存在 | |
| signed double | 不存在 | |
| long double | 10 | 16 |
| unsigned long double | 不存在 | |
| signed long double | 不存在 | |

| 已分配内存（字节） | 范围 |
|---|---|
| 1 | -128 到 +127<br>无符号：0 到 +255<br>有符号：-128 到 +127 |
| 2 | -32768 到 32767<br>无符号：0 到 65535<br>有符号：-32768 到 32767 |
| 4 | -2^31 到 2^31-1<br>无符号：0 到 2^32-1<br>有符号：-2^31 到 2^31-1 |
| 8 | -2^63 到 2^63-1 |
| 10 | -2^79 到 2^79-1 |
| 16 | -2^127 到 2^127-1 |

这里，float、double 和 long double 也支持小数。而 int 和 long 不支持。但令人惊讶的是，如果你写 int num=5.7；它不会显示错误，而是会直接截断小数部分并将整数部分存储在 num 中，即 5 将被存储在 num 中。

C++ 还支持一次性多个定义，即以下定义是有效的：

```
int a=5,b=3,c;
```

在这里，定义了三个变量 a、b、c。同样，以下定义也是有效的：

```
char c='r',d='e';
```

```
float f=1.6*3.22+4;
```

让我们举个例子，比如说 int num=5；在这里，num 是变量名。变量名不能以数字或下划线以外的特殊字符开头，即以下声明无效。

```
int 1num=5; int 0.5a=3; int .5b=4;
```

