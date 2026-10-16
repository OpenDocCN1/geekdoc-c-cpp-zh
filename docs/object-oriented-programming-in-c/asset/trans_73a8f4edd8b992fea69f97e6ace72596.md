

- 所有 ANSI C++ 程序必须包含 **using namespace std** 指令。
- 一个典型的 C++ 程序包含四个基本部分，即，包含文件部分、类声明部分、成员函数部分和主函数部分。
- 与 C 程序一样，C++ 程序可以使用任何文本编辑器创建。
- 大多数编译器系统为开发和执行程序提供集成环境。流行的系统有 UNIX AT&T C++、Turbo C++ 和 Microsoft Visual C++。

## 关键术语

- #include
- a.out
- Borland C++
- cascading
- cin
- class
- client
- comments
- cout
- edlin
- extraction operator
- float
- free-form
- get from operator
- input operator
- insertion operator
- int
- iostream
- iostream.h
- keyboard
- main()
- member functions
- MS-DOS
- namespace
- object
- operating systems
- operator overloading
- output operator
- put to operator
- return ()
- screen
- server
- Simula67
- text editor
- Turbo C++
- Unix AT&T C++
- using
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
- (f) 输出函数 printf() 不能在 C++ 程序中使用。

2.2 为什么我们需要预处理器指令 #include <iostream> ？

2.3 C++ 中的 main() 函数与 C 中的 main() 有何不同？

2.4 与旧的 C 类型注释相比，你认为 C++ 中注释 // 的主要优点是什么？

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

- (a) cout << "x=" x;
- (b) m = 5; // n = 10; // s = m + n;
- (c) cin >>x; >>y;
- (d) cout << \n "Name:" << name;
- (e) cout <<"Enter value:"; cin >> x;
- (f) /*Addition*/ z = x + y;

## 编程练习

2.1 编写一个程序，使用单个 cout 语句显示以下输出。
Maths = 90
Physics = 77
Chemistry = 69

2.2 编写一个程序从键盘读取两个数字并在屏幕上显示较大值。

2.3 编写一个程序从键盘输入一个整数值，并在屏幕上显示 "WELL DONE" 该次数。

2.4 编写一个程序读取 a、b 和 c 的值并显示 x 的值，其中
x = a / b - c
对以下值测试你的程序：
(a) a = 250, b = 85, c = 25
(b) a = 300, b = 70, c = 70

2.5 编写一个 C++ 程序，要求输入华氏温度并以摄氏度显示。

2.6 使用名为 temp 的类和成员函数重做练习 2.5。

## 3 标记、表达式和控制结构

### 关键概念

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
- Operator overloading
- Control structures

### 3.1 引言

如前所述，C++ 是 C 的超集，因此 C 的大多数构造在 C++ 中都是合法的，其含义保持不变。然而，存在一些例外和新增内容。在本章中，我们将讨论这些例外和新增内容，涉及标记和控制结构。

### 3.2 标记

众所周知，程序中最小的独立单元称为标记。C++ 有以下标记：

- Keywords
- Identifiers
- Constants
- Strings
- Operators

C++ 程序使用这些标记、空白字符和语言的语法编写。大多数 C++ 标记基本上与 C 标记相似，只是有些新增和细微修改。

### 3.3 关键字

关键字实现了特定的 C++ 语言特性。它们是明确保留的标识符，不能用作程序变量或其他用户定义程序元素的名称。

表 3.1 给出了完整的 C++ 关键字集合。其中许多与 C 共同。ANSI C 关键字以粗体显示。为了增强其特性和使其成为面向对象的语言，在 ANSI C 关键字的基础上添加了额外的关键字。ANSI C++ 标准委员会又添加了一些关键字以使语言更通用。这些单独显示。所有 C++ 关键字的含义和用途在附录 D 中给出。

### 3.4 标识符和常量

标识符指的是程序员创建的变量、函数、数组、类等的名称。它们是任何语言的基本要求。每种语言都有自己的命名规则。以下规则适用于 C 和 C++：

- 仅允许使用字母字符、数字和下划线。
- 名称不能以数字开头。
- 大写和小写字母是不同的。
- 已声明的关键字不能用作变量名。

C 与 C++ 的一个主要区别是名称长度的限制。虽然 ANSI C 仅识别名称中的前 32 个字符，但 ANSI C++ 对其长度没有限制，因此名称中的所有字符都有效。

在命名由包含 C 和 C++ 程序的多个文件共享的变量时应谨慎。某些操作系统对此类变量名的长度有限制。

常量指的是在程序执行期间不改变的固定值。

像 C 一样，C++ 支持几种类型的字面常量。它们包括整数、字符、浮点数和字符串。字面常量没有内存位置。示例：

```
123                // decimal integer
12.34              // floating point integer
037                // octal integer
0X2                // hexadecimal integer
"C++"             // string constant
'A'                // character constant
L'ab'              // wide-character constant
```

wchar_t 类型是 ANSI C++ 引入的宽字符字面量， intended for character sets that cannot fit a character into a single byte. 宽字符字面量以字母 L 开头。

**Table 3.1 C++ keywords**

|    |    |    |    |
|----|----|----|----|
| asm | double | new | switch |
| auto | else | operator | template |
| break | enum | private | this |
| case | extern | protected | throw |
| catch | float | public | try |
| char | for | register | typedef |
| class | friend | return | union |
| const | goto | short | unsigned |
| continue | if | signed | virtual |
| default | inline | sizeof | void |
| delete | int | static | volatile |
| do | long | struct | while |
| Added by ANSI C++ |  |  |  |
| bool | export | reinterpret_cast | typename |
| const_cast | false | static_cast | using |
| dynamic_cast | mutable | true | wchar_t |
| explicit | namespace | typeid |  |

Note: The ANSI C keywords are shown in bold face.

