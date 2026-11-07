
## 编译和运行程序

本书示例的 C++ 源代码文件存储在一个专为此目的创建的目录中。该目录名为“MyPrograms”——在 Windows 系统上其绝对地址为 **C:\MyPrograms**，在 Linux 上为 **/home/user/MyPrograms**。你可以重新创建此目录，用于存放等待编译的程序：

- 1. 将[此处](here)创建的“hello.cpp”程序源代码文件移动到系统上的“MyPrograms”目录。
- 2. 在命令提示符下，使用“cd”命令导航到“MyPrograms”目录。
- 3. 输入命令尝试编译程序 **c++ hello.cpp**。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_13_0.png)

你可以使用命令 **c++ --version** 查看编译器版本号，并使用 **c++ --help** 显示其所有选项。

当尝试成功时，编译器会在原始源代码文件旁边创建一个可执行文件。默认情况下，可执行文件在 Windows 系统上命名为 **a.exe**，在 Linux 上命名为 **a.out**。此时在同一目录中编译不同的源代码文件会在没有警告的情况下覆盖第一个可执行文件。这显然不可取，因此在编译程序时，应使用编译命令中编译器的 **-o** 选项为可执行文件指定自定义名称。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_13_1.png)

命令 **c++** 是 GNU C++ 编译器的别名——也可以使用命令 **g++**。

- 4. 输入命令编译程序，在源文件旁创建名为“hello.exe”的可执行文件 **c++ hello.cpp -o hello.exe**。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_13_2.png)

- 5. 要在 Windows 中运行生成的可执行程序文件，只需在“MyPrograms”目录中的提示符下输入文件名——可选地，可以省略文件扩展名。在 Linux 中，必须使用完整文件名，并在前面加上 `./`（点斜杠）——因为 Linux 除非被明确指示，否则不会查看当前目录：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_14_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_14_1.png)

本书中的所有命令行示例均已使用撰写时可用的最新 GNU C++ 编译器进行编译和测试——使用其他编译器时可能无法完全重现。

## 创建变量

在 C++ 程序中，“变量”就像一个容器，数据值可以存储在其中，位于计算机内存中。存储的值可以通过变量名来引用。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_15_0.png)

程序员可以为变量选择任意名称，只要它遵循 C++ 命名约定——所选名称只能包含字母、数字和下划线字符，但不能以数字开头。此外，必须避免使用本书封二列出的 C++ 关键字。选择有意义的名称以使代码更易理解是一种良好做法。

要在程序中创建新变量，必须对其进行“声明”，指定它可包含的数据类型及其所选名称。变量声明具有以下语法：

```
**data-type variable-name** ;
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_15_1.png)

在 C++ 中名称区分大小写——因此名为 VAR、Var 和 var 的变量被视为三个独立变量。传统上，C++ 变量名使用小写，且很少以下划线开头，因为某些 C++ 库使用该约定。

可以在单个声明中创建多个相同数据类型的变量，作为逗号分隔列表，使用以下语法：

```
**data-type variable-name1 , variable-name2 , variable-name3** ;
```

下表列出了五种基本 C++ 数据类型，以及简要说明和示例内容：

| 数据类型： | 说明： | 示例： |
|---|---|---|
| char | 一个字节，能够容纳一个字符 | 'A' |
| int | 整数 | 100 |
| float | 浮点数，精确到六位小数 | 0.123456 |
| double | 浮点数，精确到 10 位小数 | 0.0123456789 |
| bool | 布尔值 true 或 false，或者数值上零为 false，任何非零为 true | false 或 0；true 或 1 |

![](img/bf8dbdfb89042fadbaa73b4160c74bac_15_2.png)

char 数据类型的字符值必须始终用单引号括起来——而不是双引号。

变量声明必须出现在可执行语句之前——这样它们才能在语句中供引用。

当为变量赋值时，称其已被“初始化”。可选地，变量可以在其声明中初始化。任何已初始化变量中存储的值都可以通过 **cout** 函数显示到标准输出，此处使用该函数显示“Hello World!”问候语。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_16_0.png)

vars.cpp

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来启动新程序

```cpp
#include <iostream>
using namespace std ;
```

- 2. 添加一个包含最终 **return** 语句的 main 函数

```cpp
int main()
{
    // Program code goes here.
    return 0 ;
}
```

- 3. 在 main 函数中，插入语句以声明并初始化各种数据类型的变量

```cpp
char letter ; letter = 'A' ;       // Declared then initialized.
int number ; number = 100 ;        // Declared then initialized.
float decimal = 7.5 ;              // Declared and initialized.
double pi = 3.14159 ;              // Declared and initialized.
bool isTrue = false ;              // Declared and initialized.
```

- 4. 现在，插入语句以输出每个存储的值

```cpp
cout << "char letter: " << letter << endl ;
cout << "int number: " << number << endl ;
cout << "float decimal: " << decimal << endl ;
cout << "double pi: " << pi << endl ;
cout << "bool isTrue: " << isTrue << endl ;
```

- 5. 保存、编译并运行程序以查看输出

![](img/bf8dbdfb89042fadbaa73b4160c74bac_16_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_16_2.png)

布尔变量名应始终以“is”开头，以便能立即识别为布尔值。此外，对于所有由多个单词组成的变量名，应使用“lowerCamelCase”（小驼峰式命名法）——其中除第一个单词外，所有单词均以大写字母开头，例如“isTrue”。

## 使用变量数组

数组是一种可以存储多个数据项的变量——不同于普通变量只能存储一个数据项。这些数据项按顺序存储在编号从零开始的数组“元素”中。因此，第一个值存储在元素零中，第二个值存储在元素一中，依此类推。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_17_0.png)

数组的声明方式与其他变量相同，但还必须在声明中指定数组的大小，放在数组名后面的方括号中。例如，声明一个名为“nums”的数组以存储六个整数的语法如下所示：

```cpp
int nums[6];
```

可选地，数组可以在声明时通过为每个元素赋值来初始化，这些值是以逗号分隔的列表，括在花括号（大括号）中。例如：

```cpp
int nums[6] = { 0, 1, 2, 3, 4, 5 };
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_17_1.png)

数组编号从零开始——因此六元素数组中的最后一个元素编号是五，而不是六。

单个元素可以通过数组名后跟包含元素编号的方括号来引用。这意味着 **nums[1]** 引用上面示例中的第二个元素——而不是第一个元素，因为元素编号从零开始。

可以为任何 C++ 数据类型创建数组，但每个元素只能包含相同数据类型的数据。如果最后一个元素包含特殊的 `\0` 空字符，则字符数组可用于存储文本字符串。例如：

```cpp
char name[5] = { 'm', 'i', 'k', 'e', '\0' };
```

|  | [0] | [1] | [2] |
|---|---:|---:|---:|
| [0] | 1 | 2 | 3 |
| [1] | 4 | 5 | 6 |

整个字符串可以仅通过数组名来引用。这是 C 语言中处理字符串的主要方式，但[第四章](#)中介绍的 C++ string 类要简单得多。

数组的元素统称为“索引”。数组可以有多个索引——以表示多个维度，而不是常规数组的单一维度。三个及更多索引的多维数组不常见，但二维数组对于存储基于网格的信息（例如坐标）很有用。例如：

```cpp
int coords[2][3] = { { 1, 2, 3 }, { 4, 5, 6 } };
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_17_2.png)
