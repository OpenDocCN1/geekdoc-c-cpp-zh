
- 4. 现在，添加一个条件宏，用于指定一个文本字符串来标识 Linux 主机平台

```c
#ifdef linux
#define SYSTEM "Linux"
#endif
```

- 5. 接下来，添加一个 main 函数，用于输出由预处理器替换后的文本字符串值

```c
int main()
{
    printf("\n\t%s \n\t%s \n", LINE, TITLE);
    printf("\t by %s \n\t %s \n", AUTHOR, LINE);
    printf("\n Operating System: %s \n", SYSTEM);
}
```

- 6. 在 main 函数块的末尾，按照函数声明的要求返回零整数值

```c
return 0;
```

- 7. 保存程序文件，然后编译并执行程序，以查看字符串常量的输出

![](img/d1dfb0563339ba187decb78799155b7f_48_0.png)

此示例中的 LINE 字符串只是一系列下划线字符。

![](img/d1dfb0563339ba187decb78799155b7f_48_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_48_2.png)

尝试执行命令 `cpp -dM define.c` 以查看所有已定义的常量。

![](img/d1dfb0563339ba187decb78799155b7f_48_3.png)

### 调试定义

可以使用 `#if`、`#else` 和 `#elif`（else if）预处理指令来提供替代方案。这些指令允许根据求值结果进行条件分支，以执行代码段。

最初由预处理 `#define` 指令定义的常量，随后可以用 `#undef` 指令取消定义。还可以使用 `#ifndef`（如果未定义）预处理指令进行求值，以考虑某个常量是否未定义。

所有求值都可以在函数块中进行，并与常规 C 语句混合使用，而且可以相互嵌套。这类宏对于调试源代码特别有用，因为只需更改 **DEBUG** 宏的状态，就可以轻松隐藏或显示整段代码。

![](img/d1dfb0563339ba187decb78799155b7f_49_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_49_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_49_2.png)

此示例中使用的 `==` 相等运算符表示“等于”。

- 1. 使用预处理指令包含标准输入/输出库函数 `#include <stdio.h>` 来开始一个新程序

- 2. 再添加一个预处理指令来建立宏 `#define DEBUG 1`

- 3. 接下来，添加一个包含预处理指令的 main 函数，用于求值并报告宏状态

```c
#if DEBUG == 1
    printf("Debug status is 1\n");
#elif DEBUG == 2
    printf("Debug status is 2\n");
#else
    #ifdef DEBUG
        printf("Debug is defined!\n");
    #endif
    #ifndef DEBUG
        printf("Debug is not defined!\n");
    #endif
#endif
```

- 4. 在 main 函数块的末尾，按照函数声明 `return 0;` 的要求返回零整数值

- 5. 保存程序文件，然后编译并执行程序，以查看报告的宏状态。

![](img/d1dfb0563339ba187decb78799155b7f_50_0.png)

```text
C:\MyPrograms>gcc debug.c -o debug.exe
C:\MyPrograms>debug
Debug status is 1
C:\MyPrograms>
```

- 6. 修改宏值，然后保存、重新编译并再次执行程序，以查看报告的新宏状态

```c
#define DEBUG 2
```

![](img/d1dfb0563339ba187decb78799155b7f_50_1.png)

```text
C:\MyPrograms>gcc debug.c -o debug.exe
C:\MyPrograms>debug
Debug status is 2
C:\MyPrograms>
```

- 7. 再次修改宏值，然后保存、重新编译并再次执行程序，以查看变化

```c
#define DEBUG 3
```

![](img/d1dfb0563339ba187decb78799155b7f_50_2.png)

```text
C:\MyPrograms>gcc debug.c -o debug.exe
C:\MyPrograms>debug
Debug is defined!
C:\MyPrograms>
```

- 8. 在函数块的开头插入另一个预处理指令，然后保存、重新编译并再次执行程序，以查看报告的宏状态

```c
#undef DEBUG
```

![](img/d1dfb0563339ba187decb78799155b7f_50_3.png)

```text
C:\MyPrograms>gcc debug.c -o debug.exe
C:\MyPrograms>debug
Debug is not defined!
C:\MyPrograms>
```

![](img/d1dfb0563339ba187decb78799155b7f_50_4.png)

每个预处理器条件测试都必须以 **#endif** 指令结束。

### 小结

- 永远不变的固定数据值应存储为常量，并使用 const 关键字声明。
- 声明常量时，声明必须始终用其固定数据值初始化该常量。
- enum 关键字会创建一系列按顺序编号的整数常量，默认从零开始。
- 枚举系列中的任何常量都可以显式赋予一个整数值，该系列中后续常量将在此基础上递增。
- 枚举常量系列可以被视为一种新数据类型，可以基于它创建变量，以存储该类型所定义枚举集合中的值。
- 可以使用 typedef 关键字定义自定义数据类型，然后使用与声明常规变量相同的语法创建该类型的变量。
- 预处理 #define 指令可用于指定在编译前要替换的常量文本值。
- 条件预处理 #ifdef 指令用于求值当前是否存在某个定义。
- 宏是一种预处理例程，必须以 #endif 指令结束。
- 编译器定义的常量（例如 _WIN32 和 linux）可以确定主机操作系统。
- 可以使用 #if、#else 和 #elif 预处理指令提供宏替代方案。
- 常量宏定义可以用 #undef 指令取消定义，并用 #ifndef 指令求值其是否未定义。
- 宏可以通过轻松隐藏或显示代码段来帮助调试源代码。

## 4 执行运算

本章演示如何使用 C 运算符在 C 程序中操作数据。

- 52 执行算术运算
- 54 赋值
- 56 比较值
- 58 评估逻辑
- 60 检查条件
- 62 测量大小
- 64 比较位值
- 66 标记位
- 68 理解优先级
- 70 小结

### 执行算术运算

C 程序中常用的算术运算符及其执行的操作如下表所示：

| 运算符： | 操作： |
|---|---|
| + | 加法 |
| - | 减法 |
| * | 乘法 |
| / | 除法 |
| % | 取模 |
| ++ | 自增 |
| -- | 自减 |

加法、减法、乘法和除法运算符的作用与预期一致。但是，当使用多个运算符时，必须注意用括号括起表达式以使其清晰：

```c
a = b * c - d % e / f;        /* This is unclear. */
a = (b * c) - ((d % e) / f);  /* This is clearer. */
```

![](img/d1dfb0563339ba187decb78799155b7f_53_0.png)

与运算符一起构成表达式的数字称为“操作数”——在表达式 2 + 3 中，数字 2 和 3 是操作数。

% 取模运算符将第一个给定数字除以第二个给定数字，并返回运算的余数。这对于判断一个数字是奇数还是偶数很有用。

++ 自增运算符和 -- 自减运算符将给定数字改变一，并返回得到的新值。它们最常用于统计循环中的迭代次数。自增运算符将值增加一，自减运算符将值减少一。

自增和自减运算符可以放在操作数之前或之后，从而产生不同效果。如果放在操作数之前（前缀），其值会立即改变；如果放在操作数之后（后缀），则先记录其值，然后再改变。

- 1. 使用预处理指令包含标准输入/输出库函数来开始一个新程序

```c
#include <stdio.h>
```

![](img/d1dfb0563339ba187decb78799155b7f_54_0.png)

- 2. 添加一个 main 函数，声明并初始化几个整数变量

```c
int main()
{
    int a = 4, b = 8, c = 1, d = 1;
}
```

- 3. 接下来，在 main 函数块中，输出对变量值执行算术运算的结果

```c
printf("Addition: %d \n", a + b);
printf("Subtraction: %d \n", b - a);
printf("Multiplication: %d \n", a * b);
printf("Division: %d \n", b / a);
printf("Modulus: %d \n", a % b);
```

- 4. 现在，在 main 函数块中，输出后缀和前缀自增运算的结果

```c
printf("Postfix increment: %d \n", c++);
printf("Postfix now: %d \n", c);
printf("Prefix increment: %d \n", ++d);
printf("Prefix now: %d \n", d);
```

- 5. 在 main 函数块的末尾，按照函数声明的要求返回零整数值

```c
return 0;
```

- 6. 保存程序文件，然后编译并执行程序，以查看算术运算的结果

```text
Command Prompt
C:\MyPrograms>gcc arithmetic.c -o arithmetic.exe
C:\MyPrograms>arithmetic
Addition: 12
Subtraction: 4
Multiplication: 32
Division: 2
Modulus: 4
Postfix increment: 1
Postfix now: 2
Prefix increment: 2
Prefix now: 2
C:\MyPrograms>
```

> **注意**
>
> 请注意，只有使用前缀自增运算符时变量值才会立即增加——使用后缀运算符时，变量值会在下次被引用时增加。

