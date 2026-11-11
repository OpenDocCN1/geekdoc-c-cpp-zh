
可能还记得，我们在第3章的示例程序5中包含了一条语句

```c
#include <math.h>
```

其中使用了数学库函数 `cos(x)`。这是为了指示编译器从数学库中获取函数 `cos(x)`，并说明它并不是C语言的一部分。同样，每个使用标准输入/输出函数的程序都必须在开头包含语句

```c
#include <stdio.h>
```

不过，也可能有例外。例如，对于已定义为C语言一部分的函数 **printf** 和 **scanf**，这并非必需。

文件名 `stdio.h` 是 *标准输入输出头文件* 的缩写。指令 `#include <stdio.h>` 告诉编译器“搜索名为 `stdio.h` 的文件，并将其内容放在程序中的这个位置”。头文件的内容在编译时成为源代码的一部分。

## 6.2 读取一个字符

**学习目标 6.1**

所有输入/输出操作中最简单的是从“标准输入”单元（通常是键盘）读取一个字符，并将其写入“标准输出”单元（通常是屏幕）。读取单个字符可以通过使用函数 `getchar` 来完成。（这也可以借助 `scanf` 函数完成，该函数将在 6.4 节讨论。）`getchar` 采用以下形式：

```c
variable_name = getchar();
```

*variable_name* 是一个有效的 C 名称，已声明为 **char** 类型。当遇到这条语句时，计算机会等待按键，然后将该字符作为值赋给 `getchar` 函数。由于 `getchar` 用在赋值语句的右侧，`getchar` 的字符值又会赋给左侧的变量名。例如

```c
char name;
name = getchar();
```

当我们在键盘上按下 H 键时，会将字符‘H’赋给变量 name。由于 `getchar` 是一个函数，它需要像所示那样带一对圆括号。

### 例题 6.1

图 6.1 中的程序展示了 `getchar` 函数在交互环境中的使用。

该程序向用户显示一个 YES/NO 类型的问题，并以单个字符（Y 或 N）读取用户的响应。如果响应是 Y 或 y，则输出消息

我的名字是 BUSY BEE

否则，输出

你一无是处

> **注意** *输入文本和输出消息之间有一行空白。*

### 例题 6.2

图 6.2 的程序请求用户输入一个字符，并在屏幕上显示一条消息，告诉用户该字符是字母、数字还是其他特殊字符。

该程序从键盘接收一个字符，测试它是字母还是数字，并相应地打印一条消息。这些测试借助以下函数完成：

```text
isalpha(character)
isdigit(character)
```

例如，如果参数 **character** 包含字母，**isalpha** 取非零值（TRUE）；否则取 0（FALSE）。函数 **isdigit** 的情况类似。

```c
Program

#include <stdio.h>
#include <ctype.h>
main()
{
    char character;
    printf("Press any key\n");
    character = getchar();
    if (isalpha(character) > 0) /* Test for letter */
        printf("The character is a letter.");
    else
        if (isdigit(character) > 0) /* Test for digit */
            printf("The character is a digit.");
        else
            printf("The character is not alphanumeric.");
}

Output

Press any key
h
The character is a letter.
Press any key
5
The character is a digit.
Press any key
*
The character is not alphanumeric.
```

**图 6.2** *测试字符类型的程序*

C 支持许多其他类似函数，这些函数列在表 6.1 中。这些字符函数包含在文件 **ctype.h** 中，因此语句

```c
#include <ctype.h>
```

必须包含在程序中。

表 6.1 字符测试函数

| 函数 | 测试 |
|---|---|
| isalnum(c) | c 是字母数字字符吗？ |
| isalpha(c) | c 是字母字符吗？ |
| isdigit(c) | c 是数字吗？ |
| islower(c) | c 是小写字母吗？ |
| isprint(c) | c 是可打印字符吗？ |
| ispunct(c) | c 是标点符号吗？ |
| isspace(c) | c 是空白字符吗？ |
| isupper(c) | c 是大写字母吗？ |

## 6.3 写入一个字符

**学习目标 6.2**

与 `getchar` 类似，有一个类似的函数 `putchar`，用于一次一个字符地写入终端。它采用如下所示的形式：

```c
putchar(variable_name);
```

其中 `variable_name` 是一个包含字符的 `char` 类型变量。这条语句在终端显示 `variable_name` 中包含的字符。例如，以下语句

```c
answer = 'Y';
putchar(answer);
```

将在屏幕上显示字符 Y。语句

```c
putchar('\n');
```

会使屏幕上的光标移动到下一行的开头。

### 例题 6.3

图 6.3 给出了一个从键盘读取字符，然后以相反大小写打印该字符的程序。也就是说，如果输入是大写，输出将是小写，反之亦然。

该程序使用了三个新函数：`islower`、`toupper` 和 `tolower`。函数 `islower` 是一个条件函数，如果参数是小写字母，则取值 TRUE；否则取值 FALSE。函数 `toupper` 将小写参数转换为大写字母，而函数 `tolower` 则进行相反转换。

```c
Program

#include <stdio.h>
#include <ctype.h>
main()
{
    char alphabet;
    printf("Enter an alphabet");
    putchar('\n'); /* move to next line */
    alphabet = getchar();
    if (islower(alphabet))
        putchar(toupper(alphabet)); /* Reverse and display */
    else
        putchar(tolower(alphabet)); /* Reverse and display */
}

Output

Enter an alphabet
a
A
Enter an alphabet
Q
q
Enter an alphabet
z
Z
```

**图 6.3** *以相反大小写读取和写入字母*

## 6.4 格式化输入

格式化输入是指按特定格式排列的输入数据。例如，考虑以下数据：

```text
15.75 123 John
```

这一行包含三个数据项，按特定形式排列。此类数据必须按照其出现格式来读取。例如，数据的第一部分应读入一个 **float** 变量，第二部分读入 **int**，第三部分读入 **char**。在 C 中，使用 **scanf** 函数可以做到这一点。（**scanf** 意为 *扫描格式化*。）

我们已经在许多示例中使用过这个输入函数。这里，我们将探讨使用 **scanf** 函数读取格式化数据时可用的所有选项。**scanf** 的一般形式是

```c
scanf("control string", arg1, arg2, ..., argn);
```

*控制字符串* 指定数据输入时所采用的字段格式，而参数 *arg1*、*arg2*、...、*argn* 指定数据存储位置的地址。控制字符串和参数之间用逗号分隔。

控制字符串（也称为 *格式字符串*）包含字段说明，用于指导输入数据的解释。它可能包括：

- 字段（或格式）说明，由转换字符 `%`、数据类型字符（或类型说明符）以及一个 *可选的* 数字组成，用于指定字段宽度。
- 空格、制表符或换行符。

空格、制表符和换行符会被忽略。数据类型字符表示要赋给对应参数所关联变量的数据类型。字段宽度说明符是可选的。接下来的讨论将阐明这些概念。

### 6.4.1 输入整数

读取整数的字段说明为：

```c
%wd
```

百分号（`%`）表示后面跟着一个转换说明。`w` 是一个整数，指定要读取数字的 *字段宽度*，而 `d` 称为数据类型字符，表示要读取的数字为整数模式。考虑以下示例：

```c
scanf("%2d %5d", &num1, &num2);
```

数据行：

```text
50 31426
```

值 50 被赋给 **num1**，31426 被赋给 **num2**。假设输入数据如下：

```text
31426 50
```

变量 **num1** 将被赋值为 31（因为 `%2d`），而 **num2** 将被赋值为 426（31426 中未读取的部分）。未读取的值 50 将在下一次 **scanf** 调用中赋给第一个变量。如果我们使用不带字段宽度说明的字段说明，这类错误就可以消除。也就是说，语句

```c
scanf("%d %d", &num1, &num2);
```

将读取数据

```text
31426 50
```

正确地将 31426 赋给 **num1**，将 50 赋给 **num2**。

输入数据项必须用空格、制表符或换行符分隔。标点符号不算作分隔符。当 **scanf** 函数在输入数据行中搜索要读取的值时，它总是会跳过任何空白字符。

如果我们输入浮点数而不是整数，会发生什么？小数部分可能会被去掉！此外，**scanf** 可能会跳过读取后续输入。

当 **scanf** 读取某个特定值时，一旦达到字段宽度所指定的字符数（如果指定了），或者遇到对于正在读取的值无效的字符，该值的读取就会终止。对于整数，有效字符是可选带符号的数字序列。

可以通过在字段宽度的位置指定 `*` 来跳过一个输入字段。例如，语句

```c
scanf("%d %*d %d", &a, &b);
```

将把数据

```text
123 456 789
```

按如下方式赋值：

```text
123 to a
456 skipped (because of *)
789 to b
```

数据类型字符 `d` 前面可以加上 `l`（字母 ell）以读取长整数，加上 `h` 以读取短整数。

> **注意** *我们在字段说明之间提供了空白。这些空格对于数值输入并非必需，但包含它们是良好的做法。*

