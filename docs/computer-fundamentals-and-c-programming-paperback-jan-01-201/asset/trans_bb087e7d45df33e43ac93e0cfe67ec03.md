
/* scanf_char_string.c: Uses the %c and %s format specifiers to read
   individual characters and split a string into three. */
#include <stdio.h>
#define FLUSH_BUFFER while (getchar() != '\n');

int main(void)
{
    char c1, c2, c3;
    char month1[4], month2[4], month3[4];

    while (printf("Enter three characters: ")) {
        if (scanf("%c %c %c", &c1, &c2, &c3) == EOF)
            break;
        FLUSH_BUFFER
        printf("ASCII values: %c = %d, %c = %d, %c = %d\n",
               c1, c1, c2, c2, c3, c3);
    }

    printf("\nEnter 3 month names as a nine-character string: ");
    scanf("%3s%3s%3s", month1, month2, month3);
    FLUSH_BUFFER
    printf("Months split as %s | %s | %s\n", month1, month2, month3);
    return 0;
}

**程序 9.7：scanf_char_string.c**

```
Enter three characters: ABC
ASCII values: A = 65, B = 66, C = 67
Enter three characters: a b c
ASCII values: a = 97, b = 98, c = 99
Enter three characters: [Ctrl-d]
Enter 3 month names as a nine-character string: sepoctnov
Months split as sep | oct | nov
```

**程序输出：scanf_char_string.c**

扫描集反转其通常含义。因此，`%[^aeiou]` 只匹配非元音字符。扫描集可以包含转义序列和范围（如 0-9），如下例所示：

- `char stg[10];`
- `scanf("%[aeiou]", stg);` — 仅匹配元音。
- `scanf("%[0-9a-zA-Z]", stg);` — 仅匹配字母数字字符。
- `scanf("%[^,]", stg);` — 匹配除逗号外的所有字符。
- `scanf("%[^\n]", stg);` — 匹配整行——很有用的特性。

**scanf** 在遇到不属于该集合的字符时立即停止扫描。它会在数组末尾自动填充一个 NUL，而数组在声明时必须多包含一个元素。最后两个示例在程序 9.8 中使用，该程序拆分并操作从键盘输入的字符串。

```c
/* scanf_char_string2.c: Uses the %c and %s format specifiers
   and the scan set to rearrange text. */
#include <stdio.h>
#define FLUSH_BUFFER while (getchar() != '\n');

int main(void)
{
    char c1, c2, c3;
    char month1[4], month2[4], month3[4], lastname[20], firstname[20];

    while (printf("Enter three characters: ")) {
        if (scanf("%c %c %c", &c1, &c2, &c3) == EOF)
            break;
        FLUSH_BUFFER
        printf("ASCII values: %c = %d, %c = %d, %c = %d\n",
               c1, c1, c2, c2, c3, c3);
    }

    printf("\nEnter 3 month names as a nine-character string: ");
    scanf("%3s%3s%3s", month1, month2, month3);
    FLUSH_BUFFER
    printf("Months split as %s | %s | %s\n", month1, month2, month3);

    printf("Last name, First Name: ");
    scanf("%[^,], %[^\n]", lastname, firstname);
    printf("Name is %s %s\n", firstname, lastname);

    return 0;
}
```

**程序 9.8：scanf_char_string2.c**

```text
Enter three characters: ABC
ASCII values: A = 65, B = 66, C = 67
Enter three characters: a b c
ASCII values: a = 97, b = 98, c = 99
Enter three characters: [Ctrl-d]
Enter 3 month names as a nine-character string: sepoctnov
Months split as sep | oct | nov
Last name, First Name: Ritchie, Dennis
Name is Dennis Ritchie
```

**程序输出：scanf_char_string2.c**

**scanf** 首先在一个循环中运行，并使用控制字符串 "%c %c %c" 来匹配 ABC 和 a b c。然后它使用 "%3s%3s%3s" 将一个九字符单词拆分为三个组成部分。最后，**scanf** 使用两个不同的扫描集来拆分包含两个逗号分隔字符串的一行。第一个扫描集匹配不包含逗号的一组字符，而第二个扫描集匹配除换行符之外的所有字符。它们共同使得反转名和姓成为可能。

**注意：** 即使 **scanf** 可以使用扫描集 `[^\n]` 读取整行，C 还提供了另一种机制，使用两个函数——**fgets** 和 **sscanf** 来处理此任务。**fgets** 将一行读入字符数组，**sscanf** 将该行拆分为多个字段。这个重要机制将在第 13 章中讨论。

### 9.11.2 * 标志

星号（*）标志位于 % 和转换代码之间，用于跳过一个字段。例如，%*d 跳过 int 类型的字段。如下所示，被跳过的字段没有变量地址作为参数：

```
int number; float amount;
printf("Key in an int, char and float: ");
scanf("%d%*c%f", &number, &amount);
```

`*%c skips char`

在使用 **scanf**（或 **fscanf**）读取文件时，这是一个有用的特性。如果文件的每一行有六个字段，而只需要读取四个，我们可以使用 * 跳过两个字段。星号（*）在 *printf*（9.13）中具有不同的含义。

### 9.11.3 %p、%n 和 %% 说明符

%p 说明符匹配指针，这是一种特殊数据类型，将在第 12 章探讨。目前只需知道，%p 匹配表示内存地址的数字。

%n 说明符不匹配任何内容，而是使用其匹配参数将输入的字符数存储到 int 变量中。下面的示例使用这个有用的验证特性来检查是否输入了六字符字符串：

```
int count, num;
printf("Enter a 6-digit number: ");
scanf("%d%n", &num, &count);
if (count != 6)
    printf("Not a 6-digit number.\n");
```

由于 % 在控制字符串中具有特殊含义，必须有一种方法向程序表明该字符应按字面处理。这通过重复该符号来实现：

```
scanf("%d%%", &rate);
```

输入的数字必须带有 % 后缀

此调用期望输入一个数字，后跟一个 %，两者之间可有或没有空白。如果需要匹配两个 %，请使用 %%%%。

**scanf** 的近亲 **sscanf** 和 **fscanf** 将分别在第 13 章和第 15 章中讨论。**scanf** 使用的许多格式说明符也被 **printf** 使用，尽管含义并不总是相同。尽管 **printf** 没有提供任何独特的格式说明符，但它支持一组 **scanf** 不使用的标志。

## 9.12 格式化输出：`printf` 函数

原型：`int printf(cstring, var1, var2, ...);`  
头文件：`stdio.h`  
返回值：打印的字符数，出错时返回负值。

`printf` 是一组格式化输出函数中的主要成员，该组函数还包括 `fprintf` 和 `sprintf`。与 `scanf` 一样，它使用可变数量的参数，其中第一个参数（`cstring`）表示控制字符串。如果 `cstring` 包含一个或多个格式说明符，则其后必须跟有数量匹配的数据项（`var1`、`var2` 等）。数据项可以是变量、表达式或常量。图 9.3 展示了一个包含三个格式说明符和三个匹配变量的 `printf` 语句。

![](img/d75612dcf3ab36327142238ab5bb21d8_310_0.png)

**图 9.3** `printf` 的组成部分

`printf` 使用控制字符串中的信息，将所有格式说明符替换为其匹配参数的值。由于这些值可以是不同的数据类型，因此在替换之前会将它们转换为字符串。然后整个字符串显示在终端上。例如，图 9.3 中的 `printf` 语句在显示之前，将 `amount` 的浮点值（`%5.2f`）和 `days` 的整数值（`%hd`）转换为字符。

与 `scanf` 中一样，格式说明符是 `%` 和转换代码（如 `d` 或 `f`）的组合。该代码可选地带有前缀修饰符，以处理数据子类型（如 `%hd` 中的 `h`）和字段宽度（如 `%80s` 中的 80）。`printf` 支持 `scanf` 使用的所有转换代码和修饰符（表 9.3），有时会有所修改。`printf` 格式说明符还可以包含*精度*。

数据项的数量必须等于格式说明符的数量。如果它们不相等，编译器只会生成警告。`printf` 忽略多余的数据项，但对于多余的格式说明符会打印垃圾值：

```
printf("%d %d\n", x, y, z);
printf("%d %d\n", x);
```

*不会打印 z 的值*  
*第二个 %d 会打印垃圾值*

格式说明符和值之间也可能发生数据类型不匹配。当你使用 `%d` 打印字符串或使用 `%s` 打印数字时，编译器仅仅发出警告。每个由格式说明符支持的数据项都会被写出，即使它们的数据类型可能不匹配。

