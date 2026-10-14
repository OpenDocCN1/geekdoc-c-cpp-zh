

其中 *control string* 指包含特定所需格式信息的字符串，而 *arg1, arg2,... argn* 是代表各个输入数据项的参数。参数代表 *pointers*，指示计算机内存中数据项的 *addresses*。

*control string* 由控制字符、空白字符和非空白字符组成。控制字符前面有一个 `%` 符号，列在表 3.4 中。

### Table 3.4: Control characters and their explanations

| Control Character | Explanation |
|---|---|
| `%c` | a single character |
| `%d` | a decimal integer |
| `%i` | an integer |
| `%e`, `%f`, `%g` | a floating-point number |
| `%o` | an octal number |
| `%s` | a string |
| `%x` | a hexadecimal number |
| `%p` | a pointer |
| `%n` | an integer equal to the number of characters read so far |
| `%u` | an unsigned integer |
| `%[]` | a set of characters |
| `%%` | a percent sign |

`scanf()` 读取输入，与格式字符串中的字符进行匹配。当读取到控制字符时，它会将值放入下一个变量。空白字符（制表符、空格等）会被跳过。非空白字符会与输入匹配，然后被丢弃。如果在 `%` 符号和控制字符之间出现数字，则只有这么多字符会被输入到变量中。如果 `scanf()` 遇到由 `%[]` 控制字符表示的字符集，则方括号内的任何字符都会被读取。

也可以使用 `scanf()` 函数输入此类字符串。为此，必须用方括号括起来的字符序列替换 `s` 控制字符，指定为 `[...]`。方括号内可以包含空白字符，从而容纳包含此类字符的字符串。

### Example

```c
#include <stdio.h>

main()
{
    char str[80];
    ...
    scanf("%[ ABCDEFGHIJKLMNOPQRSTUVWXYZ]", str);
    ...
}
```

此示例说明了使用 `scanf()` 函数输入由大写字母和空白组成的字符串。请注意，如果你想允许输入小写字母，则必须在控制字符串中包含所有小写字母（即 a-z）。

## Formatted Output

输出数据可以使用库函数 `printf()` 从计算机写入到标准输出设备。此函数可用于输出任意组合的数值、单个字符和字符串。它与输入函数 `scanf()` 类似，只是其目的是显示数据而不是输入到计算机中。`printf()` 函数的语法可写为如下形式：

```c
printf(control string, arg1, arg2, ...argN);
```

其中 *control string* 指包含格式信息的字符串，而 arg1, arg2, ..., argn 是代表各个输出数据项的参数。参数可以写成常量、单个变量或数组名，或更复杂的表达式。

Examples:

```c
printf("Hello, world!\n");
```

```c
printf("i is %d\n", i);
```

```c
printf("%d", 10);
```

```c
printf("%d", i+j);
```

第一个语句只是显示作为 `printf()` 函数参数的字符串。在第二个语句中，`printf()` 函数用变量 `i` 的值替换两个字符 `%d`。在第三个语句中，要打印的参数是一个常量，在第四个语句中，参数是一个表达式。

`printf()` 有相当多的格式说明符。其中一些列在表 3.5 中。

### Table 3.5: Format specifiers for printf()

| Format specifier | Description |
|---|---|
| `%d` | Print an `int` argument in decimal. |
| `%ld` | Print a `long int` argument in decimal. |
| `%c` | Print a character. |
| `%s` | Print a string. |
| `%f` | Print a `float` or `double` argument. |
| `%e` | Same as `%f`, but use exponential notation. |
| `%g` | Use `%e` or `%f`, whichever is better. |
| `%o` | Print an `int` argument in octal (base 8). |
| `%x` | Print an `int` argument in hexadecimal (base 16). |
| `%%` | Print a single `%`. |

也可以指定数字和字符串插入时的宽度和精度；例如，记号 `%3d` 表示以至少 3 个空格宽的字段打印 `int`；记号 `%5.2f` 表示以至少 5 个空格宽的字段打印 `float` 或 `double`，小数点后两位。

举几个例子来说明：调用

```c
printf("%c %d %f %e %s %d%%\n", '3', 4, 3.24, 66000000, "nine", 8);
```

会打印

```text
3 4 3.240000 6.600000e+07 nine 8%
```

调用

```c
printf("%d %o %x\n", 100, 100, 100);
```

会打印

```text
100 144 64
```

对 `printf()` 的连续调用只是逐块构建输出，因此调用

```c
printf("Hello, ");
printf("world!\n");
```

也会打印 `Hello, world!`（在一行输出中）。

我们之前学过，C 在内部将字符表示为对应于机器字符集中字符值的很小的整数。这意味着在 C 中，字符和整数之间并没有太大区别；大部分区别在于我们是否选择将整数解释为整数或字符。`printf()` 就是我们可以做出这种选择的地方之一：`%d` 将整数值打印为表示其十进制值的数字字符串，而 `%c` 打印对应于字符集值的字符。因此，行

```c
char c = 'A';
int i = 97;
printf("c = %c, i = %d\n", c, i);
```

会将 `c` 打印为字符 `A`，将 `i` 打印为数字 97。但如果另一方面我们调用

```c
printf("c = %d, i = %c\n", c, i);
```

我们会看到字符 `'A'` 的十进制值（由 `%d` 打印），后面跟着恰好具有十进制值 97 的字符（无论它是什么）。

调用 `printf()` 时必须小心。它无法知道你传递了多少个参数或它们的类型，除了通过查找格式字符串中的格式说明符。如果格式说明符（即 `%` 符号）比参数多，或者参数的类型与格式说明符不匹配，`printf()` 可能会表现得很糟糕，通常会打印无意义的数字或（更糟的是）会误导你认为程序的其他部分出现故障的数字。

由于我们尚未涵盖的一些自动转换规则，你在将表达式作为参数传递给 `printf()` 时有一定的灵活性。`%c` 的参数可以是 `char` 或 `int` 类型，`%d` 的参数可以是 `char` 或 `int` 类型。`%s` 的字符串参数可以是字符串常量、字符数组或指向某些字符的指针。最后，对应于 `%e`、`%f` 和 `%g` 的参数可以是 `float` 或 `double` 类型。但其他组合不可靠：`%d` 不会打印 `long int` 或 `float` 或 `double`；`%ld` 不会打印 `int`；`%e`、`%f` 和 `%g` 不会打印 `int`。

## Self Assessment Questions

15. The _________ string consists of control characters, whitespace characters, and non-whitespace characters.
16. The control string used to read a hexadecimal character is _________.
17. `scanf()` function needs the address of the data item to be read as the argument. (True/False)
18. The output of the following statement is ____________.  
    `printf("%d %%o %%x\n", 64, 10, 75);`
19. To print an `int` argument in octal, you can use _________ format string.
20. The output of the following program segment is __________.  
    `int a = 97;`  
    `printf("%c", a);`

## 3.8 The gets() and puts() functions

`gets()` 和 `puts()` 函数促进了计算机与标准输入/输出设备之间字符串的传输。这两个函数都接受单个参数。参数必须是代表字符串（字符数组）的数据项。字符串可以包含空白字符。在 `gets()` 的情况下，字符串将从键盘输入，并以换行符终止（即当用户按下 RETURN 键时字符串结束）。

Example: Reading and writing a line of text.

```c
#include <stdio.h>
main()
{
    char line[80];
    gets(line);
    puts(line);
}
```

此程序使用 `gets()` 和 `puts()` 函数而不是 `scanf()` 和 `printf()`，来将文本行传输进出计算机。

## Self Assessment Questions

21. `gets()` is a formatted input statement. (True/False)

