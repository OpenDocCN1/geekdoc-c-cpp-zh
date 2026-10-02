
# 10.24 结构体与联合体

程序 10-27 中的代码演示了 `__DATE__` 宏的使用。

| 行号 | 程序 10-27.c | 输出窗口 (使用 Turbo C 3.0) |
|---|---|---|
| 1 | `__DATE__` macro | 编译日期为 Apr 02 2009 |
| 2 | `#include<stdio.h>` | |
| 3 | `main()` | 输出窗口 (使用 Turbo C 4.5) |
| 4 | `{` | 编译日期为 Apr 2 2009 |
| 5 | `printf("Date of compilation is %s",__DATE__);` | |
| 6 | `}` | |

**程序 10-27** | 一个演示预定义宏 `__DATE__` 使用的程序

该宏展开为定义 C 处理器被调用时时间的字符串。展开后的字符串包含八个字符，格式为 "hh:mmss"。程序 10-28 中的代码演示了 `__TIME__` 宏的使用。

| 行号 | 程序 10-28.c | 输出窗口 (使用 Turbo C 4.5) |
|---|---|---|
| 1 | `__TIME__` macro | 预处理时间为 18:56:55 |
| 2 | `#include<stdio.h>` | |
| 3 | `main()` | |
| 4 | `{` | |
| 5 | `printf("Time of preprocessing is %s",__TIME__);` | |
| 6 | `}` | |

**程序 10-28** | 一个演示预定义宏 `__TIME__` 使用的程序

如果编译器符合 ANSI C 和 ISO 标准，则该宏展开为 1。

某些编译器可能不支持此宏。例如，Turbo C 3.0 不支持此宏。程序 10-29 中的代码演示了 `__STDC__` 宏的使用。

| 行号 | 程序 10-29.c | 输出窗口 (使用 Turbo C 4.5) |
|---|---|---|
| 1 | `__STDC__` macro | 此编译器符合 ANSI C 和 ISO 标准 |
| 2 | `#include<stdio.h>` | |
| 3 | `main()` | |
| 4 | `{` | |
| 5 | `if (__STDC__==1)` | |
| 6 | `printf("This compiler conforms to ANSI C and ISO standards");` | |
| 7 | `else` | |
| 8 | `printf("This compiler does not conform with ANSI C and ISO standards");` | |
| 9 | `}` | |

**程序 10-29** | 一个演示预定义宏 `__STDC__` 使用的程序

## 10.25 存储类与预处理器指令

| 行号 | Prog 10-30.c | 输出窗口 (Turbo C 3.0) |
|---|---|---|
| 1 | `//Predefined macros` | 编译错误 |
| 2 | `#include<stdio.h>` | "Define directive needs an identifier" |
| 3 | `#define _TIME_ID` | "Bad undef directive syntax" |
| 4 | `#undef _DATE_` | |
| 5 | `main()` | |
| 6 | `{` | |
| 7 | `printf("define and undefine directives cannot be used with predefined macros");` | |
| 8 | `}` | |

**程序 10-30** | 一个用于说明不允许重新定义和取消定义宏的程序。

某些实现提供了额外的预定义宏。可以通过参考其实现文档来检查特定实现是否支持某个预定义宏。常见的实现预定义宏包括：

1. `__cppplus`：在使用 C++ 编译器时定义。用于测试是否使用了 C 或 C++ 编译器。
2. `NULL`：`NULL` 宏在头文件 `stdio.h` 和 `stddef.h` 中定义。它表示空指针。空指针定义为 `(void*)0`。通过 `NULL` 创建的空指针不指向任何对象或函数，并且与初始化的指针不同，后者可能指向任何地方。
3. `EOF`：`EOF` 宏在头文件 `stdio.h` 中定义。该宏表示遇到文件结束时返回的整数值。

## 10.5.4.1.6 undef 指令

`undef` 预处理器指令会导致标识符不再作为宏名定义。`undef` 预处理器指令的一般形式为：

```
#undef identifier
```

程序 10-31 中的代码说明了 `undef` 指令的使用。

| 行号 | Prog 10-31.c | 输出窗口 |
|---|---|---|
| 1 | `//undef directive` | 编译错误 "Undefined symbol 'VER' in function main" |
| 2 | `#include<stdio.h>` | |
| 3 | `#define VER 2.2` | |
| 4 | `#undef VER` | |
| 5 | `main()` | |
| 6 | `{` | |
| 7 | `printf("Current version of software is %f",VER);` | |
| 8 | `}` | |

**程序 10-31** | 一个说明 `undef` 指令用法的程序。

## 10.26 结构体与联合体

关于 `undef` 指令的重要要点如下：

1. 如果 `undef` 指令指定的标识符当前未定义为宏名，则会被忽略。
2. `undef` 指令指定的标识符不能是预定义宏的名称。
3. 宏可以在程序的任何地方重新定义。在展开宏时，会考虑该宏的最近一次定义。如果宏的重新定义不相同（即与宏的首次定义不同），编译器将发出警告信息 'Redefinition of 'macro' is not identical'。在重新定义宏之前，并非强制要求 `undef` 该宏。程序 10-32 中的代码段说明了上述事实。

| Prog 10-32.c | 输出窗口 |
|---|---|
| `//Redefining a macro` | 2 的两倍是 4 |
| `#include<stdio.h>` | 警告: |
| `#define DOUBLE 2` | Redefinition of 'DOUBLE' is not identical |
| `#define DOUBLE(x) (2*x)` | 备注: |
| `main()` | - 在未取消定义的情况下重新定义了宏 `DOUBLE` |
| `{` | - 在重新定义宏之前并非强制要求 `undef` 宏 |
| | - 在将 `DOUBLE` 重新定义为函数类宏后，无法将其作为对象类宏使用，即作为符号常量 |
| `printf("Double of 2 is %d", DOUBLE(2));` | - 将 `DOUBLE` 用作符号常量而非函数类宏会导致编译错误 |
| `}` | - 如果满足以下情况，宏定义将不再被考虑： |
| | - 其中一个宏是对象类宏而另一个是函数类宏 |
| | - 两者都是对象类宏但它们具有不同的替换列表 |
| | - 两者都是函数类宏但它们具有不同的参数列表或替换列表 |

**程序 10-32** | 一个说明宏重新定义的程序。

## 10.5.4.1.7 宏定义的范围

定义为宏的标识符可以从其定义点一直使用，直到遇到 `undef` 指令（或者如果没有遇到，则一直持续到翻译单元（文件）的结束）。与其他标识符（如变量、标签等）的作用范围不同，宏名的作用范围独立于块结构。程序 10-33 中的代码段说明了这一事实。

| 行号 | Prog 10-33.c | 输出窗口 |
|---|---|---|
| 1 | `//Scope of macro definitions` | 宏 `MAC` 和变量 `var` 尚未定义 |
| 2 | `#include<stdio.h>` | 它们在此处使用 |
| 3 | `main()` | MAC-10 的值 |

**程序 10-33** | 一个说明宏定义概念的程序。

## 10.5.4.3 文件包含

源文件包含指令告诉预处理器将指令替换为文件的内容。源文件包含指令通常用于包含原型和定义的头文件。它有三种编写方式：

1. `#include <name-of-file>`：`#include<name-of-file>` 会搜索目录。如果未找到文件，将显示错误 "Unable to include name-of-file"。
2. `#include "name-of-file"`：`#include"name-of-file"` 会搜索当前目录。如果搜索失败，将显示错误 "Unable to include name-of-file"。
3. `#include token-sequence`：`#include token-sequence` 告诉预处理器将指令替换为标记序列指定的文本。程序 10-34 中的代码说明了第三种形式的使用。

| 行号 | Prog 10-34.c | 输出窗口 |
|---|---|---|
| 1 | `//Source file directive` | Third form |
| 2 | `#define STR(x) #x` | |
| 3 | `#include STR(stdio.h)` | |
| 4 | `main()` | |
| 5 | `{` | |
| 6 | `printf("Third form of file inclusion");` | |
| 7 | `}` | |

**程序 10-34** | 说明第三种形式用法的程序。

## 10.5.4.2 line 指令

`line` 指令用于重置由 `__LINE__` 和 `__FILE__` 宏报告的行号和文件名。`line` 指令有两种形式：

- `line constant`：这种形式的指令使编译器确定行等于指定的整数常量。对 `__FILE__` 宏报告的文件没有影响。
- `line constant "filename"`：这种形式的指令使编译器根据常量确定行，并通过指定的标识符命名文件。程序 10-35 中的代码说明了 `line` 指令的使用。

| 行号 | Prog 10-35.c | 输出窗口 |
|---|---|---|
| 1 | `//line directive` | Line no. is 5. Filename is 10-35.c |
| 2 | `#include <stdio.h>` | Now, Line no. is 200. Filename is 10-35.c |
| 3 | `main()` | Atlas. Line no. is 100. Filename is Abc.c |
| 4 | `{` | |
| 5 | `printf("Line no. is %s. Filename is %s\n", __LINE__, __FILE__);` | |
| 6 | `# 200` | 备注: |
| 7 | `printf("Line no. is %s. Filename is %s\n", __LINE__, __FILE__);` | 在行号 6，`line` 指令分配 100 为... |
| 8 | `# 100 "Abc.c";` | |
| 9 | `printf("Atlas, Line no. is %s. Filename is %s\n", __LINE__, __FILE__);` | |
| 10 | `}` | |

**程序 10-35** | 说明 `line` 指令用法的程序。

## 10.5.4.4 error 指令

`error` 指令导致预处理器生成自定义诊断消息并导致编译失败。`error` 指令具有以下形式：

- `#error`：该指令导致预处理器发布不带信息的错误。
- `#error token-sequence`：该指令导致预处理器发布包含标记序列指定文本的错误消息。

`error` 指令通常与条件编译指令一起使用。程序 10-36 中的代码段说明了 `error` 指令的使用。

**程序 10-36** | 一个演示 `error` 指令使用的程序

## 10.5.4 pragma 指令

`pragma` 指令用于为编译器指定各种选项。这些选项取决于所使用的编译器和平台。`pragma` 指令可以配置某些原本可以通过命令行配置的编译器选项。请注意，并不是所有的编译器选项都可以使用 `pragma` 指令配置。无法识别的 `pragma` 指令将被忽略，且不会产生错误或警告信息。强烈建议在参考编译器文档后使用 `pragma` 指令。`pragma` 指令的写法为：

```
#pragma token-sequence
```

`pragma` 指令的常用形式如下：

1. **Pragma option**：格式为 `#pragma option [options...]`。表 10.5 列出了 Turbo 3.0 和 DOS 环境下常用选项。

| 序号 | 选项 | 作用 |
|---|---|---|
| 1. | `-E` | 允许嵌套注释 |
| 2. | `-C` | (默认) 不允许注释嵌套 |
| 3. | `-G` | 使编译器在优化时倾向于速度而非大小 |
| 4. | `-g` | (默认) 使编译器在优化时倾向于大小而非速度 |
| 5. | `-r` | (默认) 启用寄存器变量 |
| 6. | `-R` | 抑制寄存器变量的使用 |
| 7. | `-a` | 强制结构成员按机器字边界对齐 |
| 8. | `-A` | (默认) 产生字节对齐 |

**表 10.5** | Turbo 3.0 中提供的某些 pragma 选项

> 参见第 10.5.4.6 节关于条件编译指令中 pragma 的描述。

## 10.30 结构体与联合

程序 10-37 演示了 `pragma option -C` 的使用。

| 行 | Prog 10-37.c | 修正后的代码 |
|---|---|---|
| 1 | `//Nested multi-line comments` | `//Nested multi-line comments` |
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

**程序 10-37** | 一个演示使用 `pragma option -C` 允许嵌套注释的程序

2. **pragma warn**：`pragma warn` 可用于开启、关闭或切换警告状态。`pragma warn` 可以写为：

```
#pragma warn +www  (开启字符代码为 www 的警告)
#pragma warn -www  (关闭字符代码为 www 的警告)
#pragma warn .www  (切换字符代码为 www 的警告状态)
```

特定警告的字符代码可以通过参考编译器文档确定。Turbo C 3.0 中配合 `pragma` 指令常用的警告字符代码见表 10.6。

**表 10.6** | Turbo C 3.0 中可配合 pragma 指令使用的某些警告代码 |

| 序号 | 警告代码 | 警告 |
|---|---|---|
| 1. | `dup` | 'macro' 重定义不相同 |
| 2. | `voi` | void 函数可能没有返回值 |
| 3. | `rvl` | 函数应返回一个 |
| 4. | `par` | 参数 'parameter' 从未被使用 |
| 5. | `pia` | 可能存在错误的赋值 |
| 6. | `rch` | 不可达的代码 |
| 7. | `aus` | 'Identifier' 被赋值了一个从未被使用的值 |

程序 10-38 中的代码段演示了如何使用 `#pragma warn` 来抑制上述常见警告。

| 行 | Prog 10-38.c | 修改后的代码 |
|---|---|---|
| 1 | `//Suppression of warning messages` | `//Suppression of warning messages` |
| 2 | `#include<stdio.h>` | `#include<stdio.h>` |
