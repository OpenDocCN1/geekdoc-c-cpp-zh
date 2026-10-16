
| `<sstream>` | Contains function prototypes for functions that perform input from strings in memory and output to strings in memory. |

| `<locale>` | Contains classes and functions normally used by stream processing to process data in the natural form for different languages (e.g., monetary formats, sorting strings, character presentation, etc.) |

| `<limits>` | Contains a class for defining the numerical data type limits on each computer platform. |

| `<typeinfo>` | Contains classes for run-time type identification (determining data types at execution time). |

### 命名空间

命名空间是 ANSI C++ 标准委员会引入的一个新概念。它为程序中使用的标识符定义了一个作用域。为了使用命名空间作用域中定义的标识符，我们必须包含 `using` 指令，如

```
using namespace std;
```

这里，`std` 是 ANSI C++ 标准类库定义的命名空间。所有 ANSI C++ 程序都必须包含此指令。这会将 `std` 中定义的所有标识符带入当前全局作用域。`using` 和 `namespace` 是 C++ 的新关键字。命名空间将在第 16 章详细讨论。

### `main()` 的返回类型

在 C++ 中，`main()` 将整数类型值返回给操作系统。因此，每个 C++ 中的 `main()` 都应以 `return(0)` 语句结束；否则可能会出现警告或错误。由于 `main()` 返回整数类型值，`main()` 的返回类型明确指定为 `int`。请注意，C++ 中所有函数的默认返回类型为 `int`。以下没有类型和返回的 `main` 将会发出警告运行：

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

**程序 2.2**

```cpp
cout << "Enter two numbers: ";    // prompt
cin >> number1;    // Reads numbers
cin >> number2;    // from keyboard

sum = number1 + number2;
average = sum/2;

cout << "Sum = " << sum << "\n";
cout << "Average = " << average << "\n";

return 0;
}
```

程序 2.2 的输出为：

```text
Enter two numbers:  6.5  7.5
Sum = 14
Average = 7
```

### 变量

程序中使用了四个变量 `number1`、`number2`、`sum` 和 `average`。它们由以下语句声明为 `float` 类型。

```cpp
float number1, number2, sum, average;
```

所有变量在程序中必须在使用之前进行声明。

### 输入运算符

语句

```cpp
cin >> number1;
```

是一条输入语句，它使程序等待用户键入一个数字。键入的数字被放入变量 `number1` 中。标识符 `cin`（读作“C in”）是 C++ 中预定义的对象，对应于标准输入流。在这里，该输入流代表键盘。

运算符 `>>` 被称为提取运算符或取值运算符。它从键盘提取（或取出）值并将其赋给其右侧的变量（图 2.2）。这对应于我们所熟悉的 `scanf()` 操作。与 `<<` 一样，运算符 `>>` 也可以被重载。

![](img/58ab8f034e2127e80560390a921c2523_40_0.png)

图 2.2 使用提取运算符进行输入

### I/O 运算符的级联

在前面两条打印结果的语句中，我们反复使用了插入运算符 `<<`。

语句

```cpp
cout << "Sum = " << sum << "\n";
```

首先将字符串 `"Sum = "` 发送给 `cout`，然后发送 `sum` 的值。最后，它发送换行符，以便下一个输出显示在新的一行。在一个语句中多次使用 `<<` 称为级联。当级联输出运算符时，我们应确保不同项之间有必要的空格。使用级联技术，最后两条语句可以合并如下：

```cpp
cout << "Sum = " << sum << "\n"
    << "Average = " << average << "\n";
```

这是一个语句，但提供了两行输出。如果你只需要一行输出，可以写成：

```cpp
cout << "Sum = " << sum << ", "
    << "Average = " << average << "\n";
```

输出将是：

```text
Sum = 14, Average = 7
```

我们也可以如下所示级联输入运算符 `>>`：

```cpp
cin >> number1 >> number2;
```

数值从左到右依次赋值。也就是说，如果我们键入两个值，例如 10 和 20，那么 10 将被赋给 `number1`，20 被赋给 `number2`。

## 2.5 一个使用类的示例

C++ 的主要特性之一是类。它们提供了一种将数据以及对数据进行操作的函数绑定在一起的方法。与 C 语言中的结构一样，类是用户自定义的数据类型。

程序 2.3 展示了在 C++ 程序中使用类的方法。

**程序 2.3**

**类的使用**

```cpp
#include <iostream>
using namespace std;
class person
{
    char name[30];
    int age;

    public:
        void getdata(void);
        void display(void);
};
void person :: getdata(void)
{
    cout << "Enter name: ";
    cin >> name;
    cout << "Enter age: ";
    cin >> age;
}
void person :: display(void)
{
    cout << "\nName: " << name;
    cout << "\nAge: " << age;
}

int main()
{
    person p;

    p.getdata();
    p.display();

    return 0;
}
```

程序 2.3 的输出为：

```text
Enter name: Ravinder
Enter age: 30

Name: Ravinder
Age: 30
```

> **注意：** `cin` 只能读取一个单词，因此我们不能使用带有空格的名称。

该程序将 `person` 定义为一种新的类数据类型。类 `person` 包含两个基本数据类型项和两个用于操作该数据的函数。这些函数被称为成员函数。主程序使用 `person` 来声明其类型的变量。如前所述，类变量被称为对象。这里，`p` 是 `person` 类型的一个对象。类对象被用来调用该类中定义的函数。关于类和对象的更多内容将在第 5 章讨论。

## 2.6 C++ 程序的结构

从程序 2.3 中可以看出，一个典型的 C++ 程序会包含如图 2.3 所示的四个部分。这些部分可以放在不同的代码文件中，然后独立编译或联合编译。

![](img/58ab8f034e2127e80560390a921c2523_42_0.png)

常见的做法是将程序组织成三个独立的文件。类声明放在头文件中，成员函数的定义放在另一个文件中。这种方法使程序员能够将接口的抽象规范（类定义）与实现细节（成员函数定义）分离开来。最后，使用该类的的主程序放在第三个文件中，该文件包含前两个文件以及其他任何需要的文件。

这种方法是基于图 2.4 所示的客户端-服务器模型的概念。包含成员函数的类定义构成了服务器，为称为客户端的主程序提供服务。客户端通过类的公共接口使用服务器。

![](img/58ab8f034e2127e80560390a921c2523_43_0.png)

## 2.7 创建源文件

与 C 程序一样，C++ 程序可以使用任何文本编辑器来创建。例如，在 UNIX 上，我们可以使用 `vi` 或 `ed` 文本编辑器来创建和编辑源代码。在 DOS 系统上，我们可以使用 `edit` 或任何其他可用的编辑器，或在非文档模式下的字处理系统。

有些系统如 Turbo C++ 提供了用于开发和编辑程序的集成环境。详细信息应查阅相应的手册。

文件名应具有正确的文件扩展名，以表明它是一个 C++ 程序文件。C++ 实现使用诸如 `.c`、`.C`、`.cc`、`.cpp` 和 `.cxx` 等扩展名。Turbo C++ 和 Borland C++ 使用 `.c` 表示 C 程序，使用 `.cpp`（C plus plus）表示 C++ 程序。Zortech C++ 系统使用 `.cxx`，而 UNIX AT&T 版本使用 `.C`（大写 C）和 `.cc`。应查阅操作系统手册以确定要使用的正确文件扩展名。

## 2.8 编译和链接

编译和链接的过程再次取决于操作系统。本节讨论几种流行的系统。

### Unix AT&T C++

在 UNIX 下实现 C++ 程序的过程与 C 程序类似。我们应该使用“`CC`”（大写）命令来编译程序。记住，我们使用小写“`cc`”来编译 C 程序。命令

```sh
CC example.C
```

在 UNIX 提示符下会编译文件 `example.C` 中的 C++ 程序源代码。编译器将生成目标文件 `example.o`，然后自动与库函数链接，生成可执行文件。默认的可执行文件名是 `a.out`。

对于分布在多个文件中的程序，可以按如下方式编译：

```sh
CC file1.C file2.o
```

该语句只编译文件 `file1.C`，并将其与之前编译好的 `file2.o` 文件链接。当只需要修改其中一个文件时，这很有用。未修改的文件不必重新编译。

### Turbo C++ 和 Borland C++

Turbo C++ 和 Borland C++ 在 MS-DOS 下提供了一个集成的程序开发环境。它们提供了一个内置编辑器和一个菜单栏，其中包括 File、Edit、Compile 和 Run 等选项。

我们可以通过 File 选项创建和保存源文件，通过 Edit 选项编辑它们。然后可以通过 Compile 选项编译程序，并通过 Run 选项执行程序。Run 选项也可以在不编译源代码的情况下使用。在这种情况下，RUN 命令会使系统在一步之内编译、链接并运行程序。Turbo C++ 是最流行的编译器，在 Turbo C++ 系统下创建和执行程序的详细内容将在附录 B 中讨论。

### Visual C++

它是 Microsoft 为 C++ 提供的应用程序开发系统，可在 Windows 下运行。Visual C++ 是一个可视化编程环境，可以通过菜单选择、按钮、图标和其他预定义方法来选择基本程序组件。在 Windows 下开发和执行 C++ 程序的简要说明见附录 C。

## 小结

- C++ 是 C 语言的超集。

- C++ 为 C 语言增加了许多面向对象的特性，如对象、继承、函数重载和运算符重载。这些特性使构建的程序更清晰、可扩展且易于维护。

- C++ 可用于构建各种系统，如编辑器、编译器、数据库、通信系统，以及许多更复杂的现实应用系统。

- C++ 支持交互式输入和输出功能，并引入了一个新的注释符号 `//`，可用于单行注释。它还支持 C 风格的注释。

- 与 C 程序一样，所有 C++ 程序的执行都从 `main()` 函数开始，到 `return` 语句结束。所有使用输入/输出操作的程序都应在开头包含头文件 `iostream`。

- 所有 ANSI C++ 程序必须包含 `using namespace std` 指令。

- 一个典型的 C++ 程序包含四个基本部分，即，包含文件部分、类声明部分、成员函数部分和主函数部分。

- 与 C 程序一样，C++ 程序可以使用任何文本编辑器创建。

- 大多数编译器系统为开发和执行程序提供集成环境。流行的系统有 UNIX AT&T C++、Turbo C++ 和 Microsoft Visual C++。

## 关键术语

- `#include`

- `a.out`

- Borland C++

- cascading

- `cin`

- `class`

- client

- comments

- `cout`

- edlin

- extraction operator

- `float`

- free-form

- get from operator

- input operator

- insertion operator

- `int`

- `iostream`

- `iostream.h`

- keyboard

- `main()`

- member functions

- MS-DOS

- `namespace`

- object

- operating systems

- operator overloading

- output operator

- put to operator

- `return ()`

- screen

- server

- Simula67

- text editor

- Turbo C++

- Unix AT&T C++

- `using`

- Visual C++

- Windows

- Zortech C++

## 复习问题

2.1 判断以下陈述是 TRUE 还是 FALSE。

- (a) 由于 C 是 C++ 的子集，所有 C 程序都可以在 C++ 编译器下运行。

- (b) 在 C++ 中，包含在类中的函数称为成员函数。

- (c) 通过查看一两行代码，我们可以很容易地识别程序是用 C 还是 C++ 编写的。

- (d) 在 C++ 中，很容易向对象的现有结构添加新特性。

- (e) 使用一个运算符用于不同目的的概念称为运算符重载。

- (f) 输出函数 `printf()` 不能在 C++ 程序中使用。

2.2 为什么我们需要预处理器指令 `#include <iostream>` ？

2.3 C++ 中的 `main()` 函数与 C 中的 `main()` 有何不同？

2.4 与旧的 C 类型注释相比，你认为 C++ 中注释 `//` 的主要优点是什么？

2.5 描述 C++ 程序的主要部分。

## 调试练习

2.1 识别以下程序中的错误。

```cpp
#include <iostream.h>
void main()
{
int i=10, j=5;
int modResult=0;
int divResult=0;

modResult = i%j;
cout << modResult << " ";

divResult = i/modResult;
cout << divResult;
}
```

2.4 找出以下 C++ 语句中的错误，如有的话。

- (a) `cout << "x=" x;`

- (b) `m = 5; // n = 10; // s = m + n;`

- (c) `cin >>x; >>y;`

- (d) `cout << \n "Name:" << name;`

- (e) `cout <<"Enter value:"; cin >> x;`

- (f) `/*Addition*/ z = x + y;`

## 编程练习

2.1 编写一个程序，使用单个 `cout` 语句显示以下输出。

Maths = 90

Physics = 77

Chemistry = 69

2.2 编写一个程序从键盘读取两个数字并在屏幕上显示较大值。

2.3 编写一个程序从键盘输入一个整数值，并在屏幕上显示 "WELL DONE" 该次数。

2.4 编写一个程序读取 `a`、`b` 和 `c` 的值并显示 `x` 的值，其中

`x = a / b - c`

对以下值测试你的程序：

(a) `a = 250, b = 85, c = 25`

(b) `a = 300, b = 70, c = 70`

2.5 编写一个 C++ 程序，要求输入华氏温度并以摄氏度显示。

2.6 使用名为 `temp` 的类和成员函数重做练习 2.5。

# 3 标记、表达式和控制结构

## 关键概念

- Tokens

- Keywords

- Identifier

- Data types

- User-defined types

- Derived types

- Symbolic constants

- Declaration of variables

- Initialization

- Reference variables

- Type compatibility

- Scope resolution

- Dereferencing

- Memory management

- Formatting the output

- Type casting

- Constructing expressions

- Special assignment expressions

- Implicit conversion
