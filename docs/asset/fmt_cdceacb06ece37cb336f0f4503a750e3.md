
如果操作数类型不同，则在操作进行之前，‘较低’类型会自动转换为‘较高’类型。结果为较高类型。

下面给出的是在求值表达式时应用的一系列规则。

所有`short`类型都会自动转换为`int`；然后

1. 如果其中一个操作数是`long double`，另一个将被转换为`long double`，结果也是`long double`；

2. 否则，如果其中一个操作数是`double`，另一个将被转换为`double`，结果也是`double`；

3. 否则，如果其中一个操作数是`float`，另一个将被转换为`float`，结果也是`float`；

4. 否则，如果其中一个操作数是`unsigned long int`，另一个将被转换为`unsigned long int`，结果也是`unsigned long int`；

5. 否则，如果其中一个操作数是`long int`，另一个是`unsigned int`，那么：如果`unsigned int`可以转换为`long int`，则`unsigned int`操作数将按此转换，结果为`long int`；否则，两个操作数都将转换为`unsigned long int`，结果也是`unsigned long int`；

6. 否则，如果其中一个操作数是`long int`，另一个将被转换为`long int`，结果也是`long int`；

7. 否则，如果其中一个操作数是`unsigned int`，另一个将被转换为`unsigned int`，结果也是`unsigned int`。

表达式的最终结果在赋值给赋值号左侧的变量之前，会转换为该变量的类型。然而，在最终赋值过程中会引入以下变化：

1. `float`转换为`int`会导致小数部分被截断。

2. `double`转换为`float`会导致数字舍入。

3. `long int`转换为`int`会导致多余的高位被丢弃。

### 3.2.2 混合模式表达式

当一个操作数是实数而另一个是整数时，该表达式称为混合模式算术表达式。如果任一操作数是实数类型，则只执行实数运算，结果总是实数。因此

`25 / 10.0 = 2.5`

而

`25 / 10 = 2`

- 1. 当`float`数提供的精度不足时，可以使用`long float`类型来定义该数。（对/错）

- 2. `double`数据类型使用________位。

- 3. 如果操作数属于不同数据类型，则在操作进行之前，‘较低’类型会自动转换为‘较高’类型。（对/错）

- 4. 在最终赋值期间，将________转换为`int`会导致多余的高位被丢弃。

- 5. 表达式`22.0/10`的值是________。

### 3.3 强制类型转换运算符

C语言会自动执行类型转换。然而，在某些情况下，我们希望以不同于自动转换的方式强制进行类型转换。例如，考虑计算一个城镇中医生与工程师的比例。

```c
Ratio = doctor_number / engineer_number
```

由于在程序中`doctor_number`和`engineer_number`被声明为整数，除法结果的小数部分将会丢失，`Ratio`将表示一个错误的值。这个问题可以通过在局部将其中一个变量转换为浮点数来解决，如下所示：

```c
Ratio = (float) doctor_number / engineer_number
```

为了对表达式求值，运算符`(float)`将`doctor_number`转换为浮点数。然后利用自动转换规则，除法以浮点模式执行，从而保留结果的小数部分。请注意，运算符`(float)`绝不会影响变量`doctor_number`的值。而且，在程序的其他部分，`doctor_number`的类型仍然是`int`。

这种局部转换的过程称为强制类型转换（casting）。强制类型转换的一般形式为：

```c
(type-name) expression
```

其中`type-name`是标准C数据类型之一。表达式可以是常量、变量或表达式。

**表3.2：** 强制类型转换的用途

| 示例 | 作用 |
| --- | --- |
| `X = (int) 8.5` | 8.5通过截断转换为整数。 |
| `A = (int) 21.3 / (int) 4.5` | 按21/4求值，结果为5。 |
| `B = (double) sum/n` | 以浮点模式执行除法。 |
| `Y = (int) (a+b)` | a+b的结果转换为整数。 |
| `Z = (int) a+b` | a转换为整数后再与b相加。 |
| `P = cos((double) x)` | 在使用x之前将其转换为double。 |

#### 程序3.4：下面的程序演示了强制类型转换的使用

```c
main()
{
/* Program to find average of two integers */
float avg;
int n = 2, n1, n2;
printf("enter any 2 numbers\n");
scanf("%d %d", &n1, &n2);
avg = (n1 + n2) / (float) n;
printf(" their average is %f\n", avg);
}
```

强制类型转换可用于对给定值进行四舍五入。考虑以下语句：

```
X= (int) (y+0.5);
```

如果 y 为 37.7，则 y+0.5 为 38.2，进行强制转换后结果为 38，这就是赋给 X 的值。当然，被转换的表达式本身不会改变。在表达式中组合两种不同类型的变量时，切勿假设自动转换的规则。显式强制转换始终是一个好习惯。它更安全，也更可移植。例如，当 y 和 p 是 double 类型，m 是 int 类型时，以下两条语句是等价的。

```
y = p + m;
```

```
y = p + (double)m;
```

然而，第二条语句更可取。它在所有机器上都能以相同方式工作，并且可读性更强。

6. 强制类型转换可用于对给定值进行四舍五入。（正确/错误）

7. 表达式 A=(int)11.35/(int)14.5 中 A 的值是 ________。8. 如果 X 的值为 35.2，则表达式 A = (int)(X+0.5); 中 A 的值是 ________。

### 3.4 char 类型

单个字符可以定义为字符（char）类型的数据。字符通常存储在 8 位（1 字节）的内部存储中。限定符 signed 或 unsigned 可以显式应用于 char。unsigned char 的取值范围为 0 到 255，而 signed char 的取值范围为 -128 到 127。

字符常量是将字符括在一对单引号中形成的。因此，'b'、'.' 和 '5' 都是字符常量的有效示例。请注意，用单引号括起来的单个字符构成的字符常量，与用双引号括起来的任意数量字符构成的字符串是不同的。

格式字符 `%c` 可用于 `printf` 语句中，以在终端上显示 char 变量的值。

#### 程序 3.5：以下程序演示了如何使用 char 数据类型。

```
#include<stdio.h>
main()
{
char c='A';
int a=65;
printf("%c\n",c);
printf("%d\n",c);
printf("%c\n",a);
}
```

#### 输出

A

65

A

请注意，使用格式字符 `%d` 时，显示的是字符的 ASCII 码值；使用格式字符 `%c` 时，显示的是给定 ASCII 码值对应的字符。

### 自测题

9. 显示 char 变量值的格式字符是什么？

10. 以下 C 语句的输出是 ________。

printf("%c", 70);

### 3.5 关键字

关键字是编程语言的保留字。所有关键字都有固定的含义，这些含义不能更改。关键字是程序语句的基本构建块。ANSI C 中的所有关键字列于表 3.3 中。

- auto

- break

- case

- char

- const

- continue default

- do

#### 表 3.3：ANSI C 关键字

- double int

- else long

- enum register

- extern return

- float short

- for signed

- goto sizeof

- if static

- struct

- switch

- typedef union

- unsigned void

- volatile

- while

所有关键字都必须用小写字母书写。有些编译器可能会使用额外的关键字，这些关键字需要查阅 C 语言手册来确定。

### 自测题

- 11. 所有关键字都必须用 __________ 书写。

- 12. `default` 不是 C 语言中的有效关键字。（正确/错误）

### 3.6 字符输入与输出

读取输入最基本的方式是调用 `getchar()` 函数。`getchar()` 从“标准输入”（通常是用户的键盘）读取一个字符。`getchar()` 返回它所读取的字符（这很明显），或者如果没有更多可用字符，则返回特殊值 EOF（“文件结束”）。该值将在 stdio.h 文件中定义。通常，EOF 会被赋值为 -1，但不同的编译器可能有所不同。

`getchar()` 函数的语法如下：

```
character variable = getchar()
```

其中 *字符变量* 指的是先前声明的某个字符变量。

示例：

```
char c;

...
```

```
c = getchar();
```

第一条语句声明 c 是一个字符类型变量。第二条语句从键盘输入一个字符，并将其赋给 c。

与之配套的函数是 `putchar()`，它将一个字符写入“标准输出”（标准输出通常是用户的屏幕）。

`putchar()` 函数的语法如下：

```
*putchar(character variable)*
```

其中 *字符变量* 指的是先前声明的某个字符变量。

示例：

```
char c;

...

putchar(c);
```

第一条语句声明 c 是一个字符类型变量。第二条语句将 c 的当前值传送到用户显示器上并显示出来。

利用这两个函数，我们可以编写一个非常基本的程序，将输入逐个字符地复制到输出：

#### 程序 3.6：将输入逐个字符复制到输出的程序

```
#include <stdio.h>

/* copy input to output */
main()
{

```

```
int c;
c = getchar();
while(c != EOF)
{
putchar(c);
c = getchar();
}
return 0;
}
```

执行上述程序并观察结果。

它读取一个字符，如果该字符不是 EOF 代码，则进入 while 循环，打印一个字符并再读取一个字符，只要读取到的字符不是 EOF。char 变量可以保存与字符集值对应的整数，而 int 可以保存更任意范围内的整数（从 -32768 到 +32767）。由于大多数字符集只包含几百个字符（远不到 32767），因此 int 变量通常可以轻松容纳所有 char 值，而且还有余量。因此，将 c 声明为 int 并没有什么问题。但事实上，这样做很重要，因为 `getchar()` 可以返回每一个字符值，外加一个特殊的、非字符的 EOF 值，用来表示没有更多字符了。char 类型只保证能够容纳所有字符值，并不保证能够容纳 EOF 值而不与某些实际字符值混淆。因此，你应该始终记住：凡是要接收 `getchar()` 返回值的地方，都要使用 int 类型。

当你运行这个字符复制程序时，它会开始将输入（你输入的内容）复制到输出（你的屏幕），这时你可能会想如何让它停下来。它在收到文件结束符（EOF）时停止，但如何发送 EOF 呢？答案取决于你使用的计算机类型。在 Unix 及 Unix 相关系统上，几乎总是使用 Ctrl-D。在 MS-DOS 机器上，使用 Ctrl-Z，然后按回车键。

（还要注意，你在键盘上输入以产生文件结束条件的字符，与 `getchar()` 返回的特殊 EOF 值并不相同。`getchar()` 返回的 EOF 值是一个代码，表示输入系统检测到了文件结束条件，无论它是在读取键盘、文件、磁带、网络连接还是其他任何输入。至少在一个磁盘文件中，不太可能有任何字符与 EOF 对应；就你的程序而言，EOF 表示没有更多字符可读了。）

做任何编程时，另一件值得了解的好事情是如何终止失控的程序。如果程序因等待输入而无限运行，你通常可以通过发送文件结束符来停止它，如上所述；但如果它并非在等待什么而无限运行，你就需要采取更极端的措施。在 Unix 下，Ctrl-C（或偶尔使用 DELETE 键）几乎总能终止当前程序。在 MS-DOS 下，Ctrl-C 或 Ctrl-BREAK 有时可以终止当前程序。

### 自测题

13. `getchar()` 函数是一个输出函数。（正确/错误）

14. 为了停止读取输入字符，可以使用一个称为 _____________ 的值。

### 3.7 格式化输入与输出

可以通过标准 C 库函数 `scanf()` 从标准输入设备将输入数据输入到计算机中。该函数可用于输入数值、单个字符和字符串的任意组合。该函数返回成功输入的数据项数目。

`scanf` 函数的语法如下：

```
scanf(control string, arg1, arg2, ...argn)
```

其中 *control string* 指包含特定所需格式信息的字符串，而 *arg1, arg2,... argn* 是代表各个输入数据项的参数。参数代表 *pointers*，指示计算机内存中数据项的 *addresses*。

*control string* 由控制字符、空白字符和非空白字符组成。控制字符前面有一个 `%` 符号，列在表 3.4 中。

#### Table 3.4: Control characters and their explanations

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

也可以使用 `scanf()` 函数输入此类字符串。为此，必须用方括号括起来的字符序列替换 `s` 控制字符，指定为 `[...]`. 方括号内可以包含空白字符，从而容纳包含此类字符的字符串。

#### Example

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

#### Formatted Output

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

#### Table 3.5: Format specifiers for printf()

| Format specifier | Description |
|---|---|
| `%d` | Print an `int` argument in decimal. |
| `%ld` | Print a `long int` argument in decimal. |
| `%c` | Print a character. |
