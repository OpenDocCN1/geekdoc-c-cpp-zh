
```c
    line[c] = '\0';
    printf("\n%s\n", line);
}
```

**输出**

```text
Enter text. Press <Return> at end
Programming in C is interesting.
Programming in C is interesting.
Enter text. Press <Return> at end
National Centre for Expert Systems, Hyderabad.
National Centre for Expert Systems, Hyderabad.
```

**图 4.2** 从终端读取一行文本的程序

读取包含空白字符的文本字符串的另一种更方便的方法是使用 `<stdio.h>` 头文件中可用的库函数 `gets`。这是一个简单的函数，只有一个字符串参数，调用方式如下：

```c
gets (str);
```

`str` 是已正确声明的字符串变量。它从键盘读取字符到 `str` 中，直到遇到换行字符，然后在字符串末尾追加一个空字符。与 `scanf` 不同，它不会跳过空白字符。例如，以下代码段

```c
char line[80];
gets(line);
printf("%s", line);
```

从键盘读取一行文本并显示在屏幕上。最后两条语句可以合并如下：

```c
printf("%s", gets(line));
```

> （注意不要输入超过所用字符串变量可存储容量的字符。由于 C 不检查数组边界，这可能会引发问题。）

C 不提供直接对字符串进行操作的运算符。例如，我们不能直接将一个字符串赋给另一个字符串。例如，以下赋值语句。

```c
string = "ABC";
string1 = string2;
```

### 示例 4.3 编写一个程序，将一个字符串复制到另一个字符串中，并统计复制的字符数。

该程序如图 4.3 所示。我们使用 for 循环将 `string2` 中包含的字符复制到 `string1` 中。当到达空字符时，循环终止。注意，我们再次将一个空字符赋给 `string1`。

**程序**

```c
main() {
    char string1[80], string2[80];
    int i;
    printf("Enter a string \n");
    printf("?");
    scanf("%s", string2);
    for( i=0 ; string2[i] != '\0'; i++)
        string1[i] = string2[i];
    string1[i] = '\0';
    printf("\n");
    printf("%s\n", string1);
    printf("Number of characters = %d\n", i );
}
```

**输出**

```text
Enter a string
?Manchester
Manchester
Number of characters = 10
Enter a string
?Westminster
Westminster
Number of characters = 11
```

**图 4.3** 将一个字符串复制到另一个字符串

## 4.4 将字符串写到屏幕

### 4.4.1 使用 printf 函数

我们已经大量使用了带 `%s` 格式的 `printf` 函数将字符串打印到屏幕。`%s` 格式可用于显示以空字符结尾的字符数组。例如，语句

```c
printf("%s", name);
```

可用于显示数组 `name` 的全部内容。我们还可以指定显示数组时使用的精度。例如，格式说明

```c
%10.4s
```

表示前四个字符要在宽度为 10 列的字段中打印。然而，如果我们在格式说明中包含负号（例如 `%-10.4s`），字符串将左对齐打印。示例 4.4 说明了各种 `%s` 格式说明符的效果。

### 示例 4.4 编写一个程序，将字符串 "United Kingdom" 存储在数组 country 中，并按各种格式说明显示该字符串

该程序及其输出如图 4.4 所示。输出说明了 `%s` 格式说明符的以下特性。

- 1. 当字段宽度小于字符串长度时，会打印整个字符串。
- 2. 小数点右侧的整数值指定要打印的字符数。
- 3. 当要打印的字符数指定为零时，不打印任何内容。
- 4. 格式说明中的负号使字符串左对齐打印。
- 5. 格式说明 `%.ns` 打印字符串的前 n 个字符。

**程序**

```c
main()
{
    char country[15] = "United Kingdom";
    printf("\n\n");
    printf("*123456789012345*");
    printf("------\n");
    printf("%-15s\n", country);
    printf("%5s\n", country);
    printf("%15.6s\n", country);
    printf("%-15.6s\n", country);
    printf("%15.05s\n", country);
    printf("%.3s\n", country);
    printf("%5s\n", country);
    printf("------\n");
}
```

**输出**

```text
*123456789012345*
------
United Kingdom
United Kingdom
         United
United
          Unite
Uni
United Kingdom
------
```

**图 4.4** 使用 `%s` 格式写字符串

UNIX 上的 `printf` 支持另一个很好的特性，它允许使用可变字段宽度或精度。例如

```c
printf("%*.*s\n", w, d, string);
```

在字段宽度 `w` 中打印字符串的前 `d` 个字符。

这个特性在打印字符序列时很方便。示例 4.5 说明了这一点。

### 示例 4.5 编写一个使用 for 循环的程序，打印以下输出：

- C
- CP
- CPr
- CPro
- ....
- ....
- CProgramming
- CProgramming
- ....
- ....
- CPro
- CPr
- CP
- C

图 4.5 中程序针对可变格式说明 `%12.*s`、`%6.*s` 和 `%*.1s` 的输出如图 4.6 所示，这进一步说明了可变字段宽度和精度说明。

**程序**

```c
main()
{
    int c, d;
    char string[] = "CProgramming";
    printf("\n\n");
    printf("-------------\n");
    for( c = 0 ; c <= 11 ; c++ )
    {
        d = c + 1;
        printf("%-12.*s\n", d, string);
    }
    printf("-------------\n");
    for( c = 11 ; c >= 0 ; c-- )
    {
        d = c + 1;
        printf("%-12.*s\n", d, string);
    }
    printf("-------------\n");
}
```

**输出**

```text
C
CP
CPr
CPro
CProg
CProgr
CProgra
CProgram
CProgramm
CProgrammi
CProgrammin
CProgramming
CProgramming
CProgrammin
CProgrammi
CProgramm
CProgram
CProgra
CProgr
CProg
CPro
CPr
CP
C
```

**图 4.5** 通过打印字符序列说明可变字段说明

![](img/fe6da5f61b1e2c77309bbee135b45e35_235_0.png)

**图 4.6** 可变格式说明的进一步说明

### 4.4.2 使用 putchar 和 puts 函数

与 `getchar` 类似，C 还支持另一个字符处理函数 `putchar`，用于输出字符变量的值。其形式如下：

```c
char ch = 'A';
putchar ( ch );
```

`putchar` 函数需要一个参数。该语句等价于：

```c
printf("%c", ch);
```

我们在第 5 章中使用了 `putchar` 函数将字符写到屏幕上。我们可以使用循环重复调用该函数，以输出存储在数组中的一串字符。例如：

```c
char name[6] = "PARIS";
for (i = 0; i < 5; i++)
    putchar(name[i]);
putchar('\n');
```

另一种更方便的打印字符串值的方法是使用头文件 `<stdio.h>` 中声明的函数 `puts`。这是一个单参数函数，调用方式如下：

```c
puts ( str );
```

其中 `str` 是包含字符串值的字符串变量。该函数打印字符串变量 `str` 的值，然后将光标移到屏幕上下一行的开头。例如，以下程序段

```c
char line[80];
gets (line);
puts (line);
```

从键盘读取一行文本并显示在屏幕上。注意，与使用 `scanf` 和 `printf` 语句相比，其语法非常简单。

## 4.5 字符的算术运算

C 允许我们像处理数字一样处理字符。每当在表达式中使用字符常量或字符变量时，系统都会自动将其转换为整数值。该整数值取决于系统的本地字符集。

要按字符的整数表示形式输出字符，可以将其作为整数输出。例如，如果机器使用 ASCII 表示，那么，

```c
x = 'a';
printf("%d\n", x);
```

将在屏幕上显示数字 97。

也可以对字符常量和变量执行算术运算。例如，

```c
x = 'z'-1;
```

是一条有效语句。在 ASCII 中，`'z'` 的值为 122，因此该语句将把值 121 赋给变量 `x`。

我们还可以在关系表达式中使用字符常量。例如，表达式

```c
ch >= 'A' && ch <= 'Z'
```

将测试变量 `ch` 中包含的字符是否为大写字母。

我们可以使用以下关系将字符数字转换为其等效整数值：

```c
x = character - '0';
```

其中 `x` 定义为整数变量，`character` 包含字符数字。例如，假设该字符包含数字 `'7'`。那么，

```text
x = ASCII value of '7' - ASCII value of '0'
  = 55 - 48
  = 7
```

C 库支持一个将数字字符串转换为其整数值的函数。该函数的形式为

```c
x = atoi(string);
```

`x` 是整数变量，`string` 是包含数字字符串的字符数组。考虑以下程序段：

```c
number = "1988";
year = atoi(number);
```

`number` 是一个字符串变量，被赋值为字符串常量 `"1988"`。函数 `atoi` 将（`number` 中包含的）字符串 `"1988"` 转换为对应的数值 1988，并将其赋给整数变量 `year`。字符串转换函数存放在头文件 `<stdlib.h>` 中。

### 示例 4.6 编写一个程序，以十进制和字符形式打印字母集 a 到 z 以及 A 到 Z。

该程序如图 4.7 所示。在 ASCII 字符集中，十进制数 65 到 90 表示大写字母，97 到 122 表示小写字母。使用 for 循环中的 if 语句排除 91 到 96 的值。

