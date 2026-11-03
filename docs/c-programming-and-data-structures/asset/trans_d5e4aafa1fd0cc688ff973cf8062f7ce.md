

```
char name;
name = getchar();
```

当我们在键盘上按下 H 键时，这会将字符 'H' 赋给变量 name。由于 getchar 是一个函数，因此它需要像所示那样带一对圆括号。

## 示例 1.23 图 1.76 中的程序展示了在交互式环境中使用 getchar 函数的方法。

该程序向用户显示一个 YES/NO 类型的问题，并将用户的回答读取为单个字符（Y 或 N）。如果回答是 Y 或 y，则输出消息

My name is BUSY BEE

否则，输出

You are good for nothing

注意：输入文本与输出消息之间有一行空行。

```
Program
#include <stdio.h>
main()
{
char answer;
printf("Would you like to know my name?\n");
printf("Type Y for YES and N for NO: ");
answer = getchar(); /* .... Reading a character.... */
if(answer == 'Y' || answer == 'y')
printf("\n\nMy name is BUSY BEE\n");
else
printf("\n\nYou are good for nothing\n");
}
```

Output
Would you like to know my name?
Type Y for YES and N for NO: Y
My name is BUSY BEE
Would you like to know my name?
Type Y for YES and N for NO: n
You are good for nothing

图 1.76 使用 getchar 函数从键盘读取一个字符

可以连续调用 getchar 函数来读取一行文本中包含的字符。例如，下面的程序段会一个接一个地从键盘读取字符，直到按下“回车”键为止。

```
char character;
character = ' ';
while(character != '\n')
{
    character = getchar();
}
```

> **警告**
>
> `getchar()` 函数会接受键入的任意字符，包括 RETURN 和 TAB。这意味着当我们输入单个字符时，在 `getchar()` 返回后，换行符会停留在输入队列中。如果在循环中以交互方式使用 `getchar()`，这可能会造成问题。可以使用一个哑 `getchar()` 来“吃掉”多余的换行字符。我们也可以使用 `fflush` 函数将不需要的字符刷新出去。

> *注意：* 我们将在本章中大量使用 if、if...else 和 while 等判断语句。这些语句将在第 8 章和第 9 章中详细讨论。

## 示例 1.24 图 1.77 中的程序请求用户输入一个字符，并在屏幕上显示一条消息，告诉用户该字符是字母、数字，还是其他特殊字符。

该程序从键盘接收一个字符，并测试它是否是字母或数字，然后相应地打印消息。这些测试借助以下函数完成：

`isalpha(character)`
`isdigit(character)`

例如，如果参数 `character` 包含字母，`isalpha` 取非零值（TRUE）；否则取 0（FALSE）。`isdigit` 函数的情况与此类似。

```
Program
```c
#include <stdio.h>
#include <ctype.h>
main()
{
    char character;
    printf("Press any key\n");
    character = getchar();
    if (isalpha(character) > 0)/* Test for letter */
        printf("The character is a letter.");
    else
        if (isdigit(character) > 0)/* Test for digit */
            printf("The character is a digit.");
        else
            printf("The character is not alphanumeric.");
}
```
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

图 1.77 测试字符类型的程序

C 还支持许多其他类似的函数，见表 1.14。这些字符函数包含在文件 ctype.h 中，因此程序中必须包含语句

```
#include <ctype.h>
```

## 表 1.14 字符测试函数

| 函数 | 测试 |
|---|---|
| isalnum(c) | c 是否为字母数字字符？ |
| isalpha(c) | c 是否为字母字符？ |
| isdigit(c) | c 是否为数字？ |
| islower(c) | c 是否为小写字母？ |
| isprint(c) | c 是否为可打印字符？ |
| ispunct(c) | c 是否为标点符号？ |
| isspace(c) | c 是否为空白字符？ |
| isupper(c) | c 是否为大写字母？ |

## 1.41 写入字符

与 getchar 类似，还有一个用于一次一个字符地写入终端的类似函数 putchar。其形式如下所示：

```
putchar (variable_name);
```

其中 variable_name 是一个 char 类型的变量，包含一个字符。该语句会在终端显示 variable_name 中包含的字符。例如，语句

```
answer = 'Y';
putchar (answer);
```

会在屏幕上显示字符 Y。语句

```
putchar ('\n');
```

会使屏幕上的光标移动到下一行的开头。

### 示例 1.25 图 1.78 中给出了一个从键盘读取字符然后以相反大小写打印的程序。也就是说，如果输入是大写，则输出为小写，反之亦然。

该程序使用了三个新函数：islower、toupper 和 tolower。islower 是一个条件函数，如果参数是小写字母，则取 TRUE 值；否则取 FALSE 值。toupper 函数将小写参数转换为大写字母，而 tolower 函数则执行相反的操作。

```
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
```

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

图 1.78 以相反大小写读取和写入字母

## 1.42 格式化输入

格式化输入是指按特定格式排列的输入数据。例如，考虑以下数据：

15.75 123 John

这一行包含三段数据，它们按特定形式排列。读取这种数据时，必须遵循其出现的格式。例如，数据的第一个部分应读入 float 变量，第二个部分应读入 int 变量，第三个部分应读入 char 变量。这种操作在 C 中可以使用 scanf 函数完成（scanf 意为“扫描格式化输入”）。

之前我们已经在许多示例中使用了这个输入函数。这里，我们将探讨使用 scanf 函数读取格式化数据时可用的所有选项。scanf 的一般形式为

```
scanf ("control string", arg1, arg2, ..., argn);
```

控制字符串指定数据输入时的字段格式，参数 arg1、arg2、...、argn 指定数据存储位置的地址。控制字符串和参数之间用逗号分隔。

控制字符串（也称为格式字符串）包含字段规格，用于指导对输入数据的解释。它可能包括：

- 字段（或格式）规格，由转换字符 %、一个数据类型字符（或类型说明符）以及一个可选的数字组成，该数字指定字段宽度。
- 空格、制表符或换行符。

空格、制表符和换行符会被忽略。数据类型字符指示要赋给与相应参数关联的变量的数据类型。字段宽度说明符是可选的。下面的讨论将阐明这些概念。

### 1.42.1 输入整数

读取整数的字段规格为：

```
%w d
```

百分号（%）表示后面是一个转换规格。w 是一个整数，指定要读取的数字的字段宽度；d 称为数据类型字符，指示要读取的数字是整数模式。请考虑以下示例：

```
scanf ("%2d %5d", &num1, &num2);
```

数据行：
50 31426
值 50 被赋给 num1，31426 被赋给 num2。假设输入数据如下：
31426 50

由于 %2d，变量 num1 将被赋值为 31，而 num2 将被赋值为 426（31426 中未读到的部分）。未读取的值 50 将在下一次 scanf 调用时赋给第一个变量。如果我们使用不带字段宽度说明的字段规格，则可以消除这类错误。也就是说，语句

```
scanf ("%d %d", &num1, &num2);
```

会正确读取数据
31426 50
并将 31426 赋给 num1，将 50 赋给 num2。

输入数据项必须用空格、制表符或换行符分隔。标点符号不计为分隔符。当 scanf 函数在输入数据行中搜索要读取的值时，它总是会跳过任何空白字符。

如果输入的是浮点数而不是整数，会发生什么？小数部分可能会被去除！此外，scanf 可能会跳过后续输入。

当 scanf 读取某个值时，一旦达到字段宽度指定的字符数（如果指定了），或者遇到对该值无效的字符，读取就会立即终止。对于整数，有效字符是可有符号的数字序列。

可以通过在字段宽度位置指定 * 来跳过输入字段。例如，语句

```
scanf ("%d %*d %3d", &a, &b);
```

> 注意：我们在字段规格之间提供了空格。对于数字输入，这些空格并不是必需的，但包含它们是良好的实践。

### 示例 1.26 图 1.79 中的程序尝试了读取整数的各种输入格式化选项。

