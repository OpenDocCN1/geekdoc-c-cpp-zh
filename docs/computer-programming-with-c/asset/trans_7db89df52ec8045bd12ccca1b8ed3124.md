
> **请记住**
>
> 单行注释风格仅受 C++ 支持，而不受 C 支持。
>
> `// This commenting style is only supported in C++`
>
> 多行注释风格同时受 C 和 C++ 支持。
>
> `/* This commenting style is supported by C as well as C++ */`

下面给出一个示例，其中包含我们在为在计算机屏幕上打印文本消息而创建的程序中所添加的注释。

```c
/* This is a program to print a message
I like Computer Programming
on the computer screen */
#include <stdio.h>
void main()
{
    /* The below statement prints the text message on the screen */
    printf("I like Computer Programming");
}
```

**输出：**

I like Computer Programming

## 2.4 常量或字面量

常量或字面量是程序中不能改变其值的组成部分。C/C++ 中的常量分类如下：

- 1. 整数常量
- 2. 实数常量
- 3. 字符常量
- 4. 字符串常量

我们可以直接在程序中创建/使用上述任意常量，以便使用常量值执行操作。下面给出上述每一类常量的说明，并给出 C 和 C++ 都支持的每种常量值类型的示例。

### 2.4.1 整数常量

这些是不带小数点的数字，可以直接写在程序中。整数常量可以是正数或负数，常量值中不包含任何小数部分。

下面给出一些整数常量的有效和无效示例：

```c
10       /* This is a VALID integer constant */
-95      /* This is a VALID integer constant which represents
            a negative value */
45.9     /* This is an INVALID integer constant as there is a decimal
            point in the number */
25,000   /* This is an INVALID integer constant as there is a comma
            used in between the digits of the number */
```

请注意，整数常量在代码中必须由数字 0 到 9 组合而成，数字之间不能包含逗号或空格等特殊字符。

### 2.4.2 实数常量

这些是带小数点的数字，可以直接写在程序中。实数常量可以是正数或负数，也可以包含作为常量值一部分的小数部分。在 C/C++ 中，*实数常量* 也称为 *浮点常量* 或 *双精度常量*。

下面给出一些实数常量的有效和无效示例：

```c
10.5        /* This is a VALID floating point constant */
-90.832     /* This is a VALID floating point constant */
25,000.976  /* This is an INVALID floating point constant as there
               is a comma used in between the digits of the number */
```

请注意，与整数常量一样，*实数常量* 在代码中必须由数字 0 到 9 组合而成，数字之间不能包含逗号或空格等特殊字符。*实数常量* 可以在数字之间恰好包含一个小数点，以表示浮点值。

### 2.4.3 字符常量

*字符常量* 是用单引号括起来的单个符号。下面给出 C/C++ 中字符常量的一些有效和无效示例。

```c
'e'   /* This is a VALID character constant which represents a letter e */
'1'   /* This is a VALID character constant which represents a symbol 1 */
'$'   /* This is a VALID character constant which represents a symbol
          dollar */
' '   /* This is a VALID character constant which represents a blank
          space */
'10'  /* This is an INVALID character constant as it encloses two
          different symbols (1 and 0) within the single quotes */
'ad'  /* This is an INVALID character constant as it encloses two
          different symbols (letters 'a' and 'd') within the single quotes */
```

### 2.4.4 字符串常量

字符的集合称为字符串。字符串常量通过将多个字符括在双引号中形成。

下面给出 C/C++ 中字符串常量的一些有效和无效示例：

```text
"Computer"   /* This is a VALID string constant which is a collection
                of eight characters */
"C"          /* This is a VALID string constant which contains just a single
                character */
'com'        /* This is an INVALID string constant. This is because a
                string cannot be enclosed in single quotes */
"456+6"      /* This is a VALID string constant which is a collection of
                4 characters */
```

C/C++ 中的每个字符串都以一个称为 NULL 字符的特殊字符结尾，该字符由 `'\0'` 表示。例如，字符串“Computer”在内存中的内部存储方式如图 2.6 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_46_0.png)

请注意，字符串的最后一个字符会自动添加为 `'\0'`，它是字符串结束标记，称为 NULL 字符。字符串常量及其处理的详细信息将在本教材第 6 章中讨论。

> **为什么我们要在内存中存储字符常量的 ASCII 值？**
>
> 回顾第 1 章可知，用高级语言编写的每个符号都必须先转换为机器语言，才能由 CPU 处理。整数常量或实数常量可以通过用“二进制数系统”表示它们，直接转换为机器语言。为了便于将字符常量存储在计算机内存中，每个字符常量在内部都会被分配一个整数代码，称为该字符的 ASCII 值。因此，我们现在只需用“二进制数系统”表示字符的 ASCII 代码，就可以将字符常量存储在计算机内存中。

### 2.5 变量和数据类型

变量是用于在内存中存储特定值的占位符。这意味着变量是计算机内存中保留的一块区域，我们可以在其中存储值。创建变量的过程称为变量的“声明”，而将特定值存储到变量中的过程称为变量的“初始化”。

每个变量都与特定的数据类型相关联。变量的数据类型决定了可以在该变量中存储的值的类型。C/C++ 支持的基本数据类型列表如下：

| 数据类型 | 描述 | 大小（字节） | 取值范围 |
|---|---|---:|---|
| `int` | int 类型的变量可以存储范围为 −32,768 到 +32,767 的任意整数类型常量 | 2 字节 | −32,768 到 +32,767 |
| `float` | float 类型的变量可以存储范围为 −3.4e−38 到 +3.4e+38 的任意带小数点的数字 | 4 字节 | −3.4e−38 到 +3.4e+38 |
| `char` | 数据类型 char 用于存储字符常量，即用单引号括起来的单个符号 | 1 字节 | −128 到 +127 |
| `double` | double 类型的变量可以存储范围为 −1.7e−308 到 +1.7e+308 的任意带小数点的数字。与 float 相比，此数据类型具有更高的精度。因此，double 类型变量在内存中需要 8 字节，而 float 类型变量在计算机内存中只需要 4 字节 | 8 字节 | −1.7e−308 到 +1.7e+308 |
| `short int` | short int 类型的变量可以存储范围为 −128 到 +127 的任意整数类型常量。关键字 short int 定义了 C++ 中 int 类型的较小版本。因此，short int 变量在计算机内存中只需要 1 字节，而 int 变量在计算机内存中实际上需要 2 字节 | 1 字节 | −128 到 +127 |
| `long` | long 类型的变量可以存储范围为 −2147483648 到 +2147483647 的任意整数类型常量。关键字 long 表示 C++ 中 int 类型的较大版本。因此，long 变量在计算机内存中需要 4 字节，而 int 变量在计算机内存中只需要 2 字节 | 4 字节 | −2147483648 到 +2147483647 |

¹ 本教材通篇假设使用 16 位编译器，其中整数的大小为 2 字节（16 位）。如果你得到的整数大小为 4 字节，则说明你使用的是 32 位编译器。

## 2.5.1 计算数据类型的范围

特定类型的变量中可以存储的值的范围取决于该“数据类型”在计算机内存中的大小。特定数据类型的范围可以通过考虑分配给该变量的位值所能表示的总排列数来确定。例如，让我们考虑一个在计算机内存中需要 2 字节的整数类型变量。由于每个字节由八位组成，我们可以说一个整数变量在计算机内存中需要 16 位。因此，使用 16 位可以表示的总排列数（X）可按如下方式计算：

排列数（X）= 2¹⁶ = 65,536
