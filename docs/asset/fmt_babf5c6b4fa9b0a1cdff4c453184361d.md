
| 3 | `#define PI 2` | `#pragma warn -dup` |
| 4 | `#define PI 4` | `#pragma warn -pia` |
| 5 | `main()` | `#pragma warn -rch` |
| 6 | `{` | `#pragma warn -rvl` |
| 7 | `int a=10;` | `#pragma warn -aus` |
| 8 | `if(a=PI)` | `#define PI 2` |
| 9 | `printf("The value of PI is %d",PI);` | `#define PI 4` |
| 10 | | `main()` |
| 11 | | `{` |
| 12 | | `int a=10;` |
| 13 | | `if(a=PI)` |
| 14 | | `printf("The value of PI is %d",PI);` |
| 15 | | `return;` |
| 16 | | `printf("This is unreachable statement");` |
| 17 | | `}` |
| 18 | | Output window |
| 19 | | The value of PI is 4 |
| 20 | | Warnings(5): |
| 21 | | Redefinition of 'macro' is not identical |
| 22 | | Possibly incorrect assignment |
| 23 | | Unreachable code |
| 24 | | 'Identifier' is assigned a value that is never used |

**程序 10-38** | 一个演示使用 `#pragma warn` 抑制各种警告的程序

- 3. pragma startup and exit：`#pragma startup` 和 `#pragma exit` 分别用于设置先置条件和清理任务。程序 10-39 中的代码段演示了 `#pragma startup` 和 `#pragma exit` 指令。这些指令可以写为：

```
#pragma startup function_name
#pragma exit function_name
```

| 行 | Prog 10-39.c | 修改后的代码 |
|---|---|---|
| 1 | //Nested multi-line comments | //Nested multi-line comments |
| 2 | `#include <stdio.h>` | `#include <stdio.h>` |
| 3 | `main()` | `#pragma option -C` |
| 4 | `{` | `main()` |
| 5 | `/*Start of Outer Comment` | `/*Start of Outer Comment` |
| 6 | `//Inner Comment*/` | `/*Inner Comment*/` |
| 7 | `End of Outer Comment*/` | `End of Outer Comment*/` |
| 8 | `printf("By default nested comments are not allowed\n");` | `printf("By default nested comments are not allowed\n");` |
| 9 | `}` | `printf("#pragma option -C makes them allowed\n");` |
| 10 | | `}` |
| 11 | Output window Compilation error | |

**程序 10-37** | 一个演示使用 `#pragma option -C` 允许嵌套注释的程序

## 10.5.4.6 条件指令

条件编译意味着只有在某些条件成立时才编译程序的某些部分。可用的条件编译指令如下：

```
#if, #ifdef, #else, #elif, #endif
```

使用条件编译指令的语法见表 10.7。

**表 10.7** | 条件编译指令的语法和语义 |

| 序号 | 条件编译指令 | 语法 | 语义 |
| --- |---|---|---|
| 1. | `#if`-`#endif` | `#if constant-exp statements-set #endif` | 只有当常量表达式为真时才编译语句 |
| 2. | `#if`-`#else`-`#endif` | `#if constant-exp statements-set1 #else statements-set2 #endif` | 如果常量表达式为真，则编译 `statements-set1`，否则编译 `statements-set2` |
| 3. | `#if`-`#elif`-`#endif` | `#if constant-exp statements-set1 #elif constant-exp2 statements-set2 #endif` | 如果表达式1为真，则编译 `statements-set1`。只有当表达式1为假且表达式2为真时，才编译 `statements-set2` |
| 4. | `#ifdef`-`#endif` | `#ifdef identifier statements-set #endif` | 只有当标识符为定义的宏名称或之前通过定义预处理器指令定义为宏名称且中间没有相同标识符的定义指令时，才编译语句-set |
| 5. | `#ifdef`-`#else`-`#endif` | `#ifdef identifier statements-set1 #else statements-set2 #endif` | 只有当标识符为定义的宏名称或之前通过定义预处理器指令定义为宏名称且中间没有相同标识符的定义指令时，才编译 `statements-set1`，否则编译 `statements-set2` |

## 存储类与预处理器指令 10.33

| 行号 | `#ifdef`-`#elif`-`#endif` | 语句 |
| :--- | :--- | :--- |
| 6. | `#ifdef identifier statements-set1 #elif constant-exp statements-set2 #endif` | 只有当 `identifier` 是预定义宏或之前通过宏预处理器指令定义（且中间没有相同标识符的指令）时，`statements-set1` 将会被编译。如果没有定义由 `identifier` 指定的宏且常量表达式求值为真，则 `statements-set2` 将会被编译。如果该宏未被定义且常量表达式求值为假，则没有任何语句集会被编译。 |
| 7. | `#ifndef`-`#endif` | `#ifndef identifier statements-set #endif` | 如果之前没有定义由 `identifier` 指定的宏，则 `statements-set` 将会被编译。否则，如果不满足某种条件，则不编译。 |
| 8. | `#ifndef`-`#else`-`#endif` | `#ifndef identifier statements-set1 #else statements-set2 #endif` | 如果之前没有定义由 `identifier` 指定的宏，则 `statements-set1` 将会被编译。否则，`statements-set2` 将会被编译。 |
| 9. | `#ifndef`-`#elif`-`#endif` | `#ifndef identifier statements-set1 #elif constant-exp statements-set2 #endif` | 如果之前没有定义由 `identifier` 指定的宏，则 `statements-set1` 将会被编译。如果宏-常量表达式求值为真，则 `statements-set2` 将会被编译。 |

使用条件编译指令的关键点如下：

1. 条件编译预处理器指令可以出现在程序中的任何位置。
2. 语句可以是空的，也可以包含预处理器指令或 C 语句。

程序 `main.c` 中的代码段说明了条件编译指令的使用。

| 行号 | 程序 main.c | 输出 |
| :--- | :--- | :--- |
| 1 | //条件编译指令 | 嵌入式系统被实际应用 |
| 2 | `#include <stdio.h>` | |
| 3 | `#define EMBEDDED` | |
| 4 | `#ifndef EMBEDDED` | |
| 5 | `#error 此代码仅用于系统` | |
| 6 | `#endif` | |
| 7 | `main()` | |
| 8 | `{` | |
| 9 | `#ifdef EMBEDDED` | |
| 10 | `printf("Embedded systems are used in real applications\n");` | |
| 11 | `#else` | |
| 12 | 这部分程序将不会被编译 | |
| 13 | 放置用于非嵌入式系统的代码 | |
| 14 | `#endif` | |
| 15 | `}` | |

程序 `main.c` | 一个用于说明条件编译指令用的程序

### 10.5.4 空指令 (Null Directive)

空指令的形式如下：

```c
#pragma line
```

空指令没有任何作用。

## 10.6 总结

1. 翻译器是将用源语言编写的程序转换为目标语言等效程序的程序。
2. 翻译器根据其源语言和目标语言的类别进行分类。
3. 根据源语言和目标语言的类别，翻译器分为预处理器、编译器、汇编器和解释器。
4. 预处理器是在编译器调用之前被调用的翻译器。
5. 预处理器由称为预处理器指令的命令控制，这些指令不是 C 语言的一部分。
6. 将源程序文件转换为可执行文件共有八个翻译阶段。
7. 三元组替换（Trigraph replacement）是翻译的第一阶段。在此阶段，三元组序列会被替换为相应的单字符等效字符。
8. 在翻译的第二阶段（即行合并 Line splicing）中，处理器会删除一个紧跟换行符的反斜杠字符实例。
9. 翻译的第三阶段是标记化（Tokenization），在此期间，源文件被分解为预处理标记和一系列空白字符。
10. 在翻译的第四阶段，将执行预处理器指令并展开宏。
11. 预处理器指令始终以 `#`（井号）符号开头。
12. 宏是 C 预处理器提供的一种机制，通过它可以用用户定义的字符序列替换标记。
13. 可以创建两种类型的宏：对象类宏（Object-like macros）和函数类宏（Function-like macros）。
14. 对象类宏也称为符号常量。
15. 函数类宏是带有参数的宏。
16. 如果一个函数类宏的行为像函数调用，则称它是安全的。
17. 如果在定义和使用宏时不小心，宏可能会产生问题。
18. 预处理标记 `#` 称为字符串化运算符（stringizing operator）。
19. 预处理标记 `##` 用于标记粘合（token pasting）。
20. 条件编译指令用于条件编译。这意味着只有当某个条件为真时，程序的某部分会被编译。
21. 条件编译指令包括：`#if`, `#ifdef`, `#ifndef`, `#else`, `#elif`, `#endif`。

## 概念问答

1. 什么是翻译器？它们是如何分类的？

   参见第 10.4 节。

2. 程序在执行之前会经历哪些各个阶段？

   程序经历的各个阶段为：

   1. 预处理
   2. 编译
   3. 链接

3. 翻译的各个阶段有哪些？

   翻译的各个阶段为：

   1. 三元组替换
   2. 行合并
   3. 标记化
   4. 预处理器指令执行与宏展开
   5. 代码生成
   6. 汇编生成
   7. 库链接
   8. 加载

4. 什么是预处理器指令？

   预处理器指令是以 `#` 符号开头的命令，用于控制预处理器。

5. 什么是宏？

   宏是 C 预处理器提供的，可以用用户定义的字符序列替换标记。

6. 宏有哪些类型？

   宏有两种类型：对象类宏和函数类宏。

## 10.38 结构体与联合

在预处理阶段进行宏展开后，表达式 `result=1/square(2);` 变为 `result=1/2*2;`。由于除法运算符和乘法运算符具有相同的优先级且从左到右结合，因此先执行除法，再执行乘法。因此，结果为 0.500000。给出的这段代码可以通过对宏的替换列表加上括号来修正，以保护其中的任何低优先级运算符，免受周围表达式中存在的高优先级运算符的影响。修正后的代码如下：

```c
#define square(x) ((x)*(x))
main()
{
    float result;
    result=1.0/square(2);
    printf("Result is %f", result);
}
```

上述修正后的代码在执行时输出为：Result is 0.250000

- 13. 我按照上一个问题回答中建议的方法定义了宏，并编写了以下代码：

```c
#define square(x) ((x)*(x))
main()
{
    int number=2,result;
    result=square(number+1);
    printf("Square of 3 is %d",result);
}
```

代码仍然没有按照预期工作，输出的是 5 而不是 9。为什么？我该如何修正它？

在预处理阶段完成宏展开后，给出的代码变为：

```c
main()
{
    int number=2,result;
    result=((number+1)*(number+1));
    printf("Square of 3 is %d",result);
}
```

表达式 `((number+1)*(number+1))` 的结果为 9，符合预期。原文中展开为 `(number+1*number+1)` 系笔误，实际按运算符优先级计算结果为 5。修正方法是对宏替换列表中所有参数的出现处加上括号，以保护实际参数中的任何低优先级运算符不受宏展开其余部分的影响。修正后的代码如下：

```c
#define square(x) ((x)*(x))
main()
{
    int number=2,result;
    result=square(number+1);
    printf("Square of 3 is %d",result);
}
```

上述修正后的代码在执行时输出为：Square of 3 is 9

- 14. 如果我按照上一个问题回答中的建议定义宏 `square` 并在表达式中调用它，是否可以安全地假设我的代码运行正常，就像一个由返回输入参数值的函数调用组成的表达式语句一样？

## 10.39 存储类与预处理器指令

宏 `square` 是按照第 13 回答中的建议方式定义的，仍然无法安全地假设包含宏 `square` 调用的表达式等同于包含返回输入参数值的函数调用的表达式。考虑以下代码段及其执行结果的差异：

| 代码-I 宏版本 | 代码-II 函数版本 |
| :--- | :--- |
| `#define square(x) ((x)*(x))` | `int square(int x){` |
| `main()` | `return x*x;}` |
| `{` | `main()` |
| `int i=2,result;` | `{` |
| `result=square(++i);` | `int i=2,result;` |
| `printf("The value of result is %d",result);` | `result=square(++i);` |
| `}` | `printf("The value of result is %d",result);` |
| | `}` |
| | `}` |

代码-I 的执行（即宏）输出：The value of result is 16。

代码-II 的执行（即函数）输出：The value of result is 9。

宏 `square` 表现出这种行为，是因为它的参数是一个表达式（即 `++i`），具有副作用。

- 15. 定义宏时应该注意哪些点？

参见 10.5。

- 16. 泛式宏和函数之间的区别是什么？

虽然泛式宏和函数看起来一样，但实际上并不是。泛式宏和函数的主要区别如下：

| 泛式宏 | 函数 |
| :--- | :--- |
| 1. 泛式宏在每次遇到时都在预处理阶段替换。没有参数传递。 | 1. 在函数调用中，参数传递给调用函数并返回给调用函数。 |
| 2. 由于没有参数传递，节省了调用函数的时间。泛式宏相比函数提供了更好的性能。 | 2. 控制权在函数和调用者之间传递，这会减慢程序。 |
| 3. 由于宏名在预处理阶段被替换为替换列表，会增加代码大小。这增加了冗余。 | 3. 函数重复使用相同的代码。因此，这是使用函数的优点。 |
| 4. 因此，泛式宏使程序运行更快，但增加了程序大小。 | 4. 因此，使用函数使程序更小紧凑，但会损害程序速度。 |

## 10.40 结构体与联合

17. 我遇到了以下代码：

```c
#define PI 3.14
#undef PI
main()
{
    int rad=2;
    printf("Area of circle is %f",PI);
}
```

给出的代码在编译时显示“未定义符号”，由于 PI 在使用前被 `#undef` 取消定义；因此编译器会显示错误。

18. 标记替换和标记粘贴是什么？

参见 10.5.4.1。

19. 宏替换会在字符串字面量内进行吗？例如，考虑以下代码：

```c
#define LINE 100
main()
{
    int LINE=25;
    printf("The LINE is %d",LINE);
}
```

上述代码在执行时打印：The LINE is 25。

20. 包含指令有何不同的编写方式？

参见 10.5。

21. 使用双引号包含文件会有区别吗？

根据 ANSI 标准：

- (1) `<name-file>` 在指定的目录中搜索并嵌入整个内容。如果搜索失败，将显示“无法包含”。
- (2) `"name-file"` 搜索当前工作目录。如果该搜索失败，将显示“无法包含”。
