
你可以改用这个简写形式：

```
flags &= ~MASK;
```

## 用法：切换位

切换一个位意味着：如果它是开的就把它关掉，如果它是关的就把它打开。你可以使用按位异或（EXCLUSIVE OR）运算符来切换一个位。其原理是：如果 b 是一个位的值（1 或 0），那么当 b 为 1 时，1 ^ b 为 0；当 b 为 0 时，1 ^ b 为 1。另外，无论 b 的值如何，0 ^ b 均为 b。因此，如果用一个掩码通过 ^ 与一个值组合，那么掩码中与 1 对应的位会被切换，与 0 对应的位保持不变。要切换 flags 中的位 1，你可以采用以下任一方式：

```
flags = flags ^ MASK;
flags ^= MASK;
```

例如，假设 flags 为 00001111，MASK 为 10110110。表达式

```
flags ^ MASK
```

变为

```
(00001111) ^ (10110110)  // expression
```

并计算得到以下结果：

```
(10111001)          // resulting value
```

MASK 中所有设置为 1 的位都会导致 flags 中对应的位被切换。flags 中与 MASK 中 0 位对应的那些位则保持不变。

## 用法：检查位的值

你已经了解了如何改变位的值。现在假设你想检查某个位的值。例如，flags 的位 1 是否被设置为 1？你不应该简单地将 flags 与 MASK 进行比较：

```
if (flags == MASK)
    puts("Wow!");    /* doesn't work right */
```

即使 flags 中的位 1 被设置为 1，flags 中的其他位也可能会使这个比较不成立。相反，你必须先屏蔽 flags 中的其他位，以便只将 flags 的位 1 与 MASK 进行比较：

```
if ((flags & MASK) == MASK)
    puts("Wow!");
```

按位运算符的优先级低于 ==，因此需要加上括号把 flags & MASK 括起来。

为了避免边缘信息泄露，位掩码的宽度至少应与被掩码的值的宽度相同。

## 按位移位运算符

现在来看 C 语言的移位运算符。按位移位运算符将位向左或向右移动。同样，我们将明确写出二进制数来展示其原理。

## 左移：<<

左移运算符（<<）将左操作数的值的各位向左移动右操作数所指定的位数。空出的位置补 0，超出左操作数末端被移出的位则丢失。因此，在下面的示例中，每个位向左移动两位：

```
(10001010) << 2  // expression
(00101000)        // resulting value
```

该操作会产生一个新的位值，但不会改变其操作数。例如，假设 stonk 为 1，那么 stonk<<2 为 4，但 stonk 仍然是 1。你可以使用左移赋值运算符（<<=）来真正改变变量的值。该运算符将变量中的位向左移动右侧值所指定的位数。下面是一个示例：

```
int stonk = 1;
int onkoo;
onkoo = stonk << 2;  /* assigns 4 to onkoo */
stonk <<= 2;         /* changes stonk to 4 */
```

## 右移：>>

右移运算符（>>）将左操作数的值的各位向右移动右操作数所指定的位数。超出左操作数右端被移出的位则丢失。对于无符号类型，左端空出的位置补 0。对于有符号类型，结果取决于具体机器。空出的位置可能补 0，也可能用符号位（最左端位）的副本填充：

```
(10001010) >> 2  // expression, signed value
(00100010)        // resulting value, some systems
(10001010) >> 2  // expression, signed value
(11100010)        // resulting value, other systems
```

对于一个无符号值，情况如下：

```
(10001010) >> 2  // expression, unsigned value
(00100010)        // resulting value, all system
```

每个位向右移动两位，空出的位置补 0。

右移赋值运算符（>>=）将左侧变量中的位向右移动所指定的位数，如下所示：

```
int sweet = 16;
int ooosw;
```

```
ooosw = sweet >> 3;  // ooosw = 2, sweet still 16
sweet >>=3;          // sweet changed to 2
```

## 用法：按位移位运算符

按位移位运算符可以提供快速、高效（取决于硬件）的 2 的幂次乘法和除法：

| number << n | 将 number 乘以 2 的 n 次方 |
| number >> n | 如果 number 不为负，则将 number 除以 2 的 n 次方 |

这些移位操作类似于十进制系统中移动小数点以乘以或除以 10 的做法。

移位运算符还可以用于从较大的数据单元中提取位组。例如，假设你使用一个 unsigned long 值来表示颜色值，其中低字节存储红色强度，下一个字节存储绿色强度，第三个字节存储蓝色强度。假设你随后想把每种颜色的强度存储到各自的 unsigned char 变量中，那么你可以这样做：

```
#define BYTE_MASK 0xff
unsigned long color = 0x002a162f;
unsigned char blue, green, red;
red = color & BYTE_MASK;
green = (color >> 8) & BYTE_MASK;
blue = (color >> 16) & BYTE_MASK;
```

这段代码使用右移运算符将 8 位的颜色值移动到低字节，然后使用掩码技术将低字节赋值给所需的变量。

## 编程示例

在第 9 章“函数”中，我们使用递归编写了一个将数字转换为二进制表示的程序。现在我们用按位运算符来解决同样的问题。程序清单 15.1 中的程序从键盘读取一个整数，并将其和一个字符串地址传递给名为 itobs() 的函数（当然，即 integer-to-binary string，整数转二进制字符串）。该函数随后使用按位运算符来确定正确的 1 和 0 模式，并放入字符串中。

## 程序清单 15.1 binbit.c 程序

```
/* binbit.c -- using bit operations to display binary */
#include <stdio.h>
#include <limits.h> // for CHAR_BIT, # of bits per char
char * itobs(int, char *);
void show_bstr(const char *);

int main(void)
{
    char bin_str[CHAR_BIT * sizeof(int) + 1];
    int number;

    puts("Enter integers and see them in binary.");
    puts("Non-numeric input terminates program.");
    while (scanf("%d", &number) == 1)
    {
        itobs(number,bin_str);
        printf("%d is ", number);
        show_bstr(bin_str);
        putchar('\n');
    }
    puts("Bye!");

    return 0;
}

char * itobs(int n, char * ps)
{
    int i;
    const static int size = CHAR_BIT * sizeof(int);

    for (i = size - 1; i >= 0; i--, n >>= 1)
        ps[i] = (01 & n) + '0'; // assume ASCII or similar
    ps[size] = '\0';

    return ps;
}

/* show binary string in blocks of 4 */
void show_bstr(const char * str)
{
    int i = 0;

    while (str[i]) /* not the null character */
    {
        putchar(str[i]);
```

```
if(++i % 4 == 0 && str[i])
    putchar(' ');
}
}
```

程序清单 15.1 使用了 limits.h 中的 CHAR_BIT 宏。该宏表示 char 中的位数。sizeof 运算符返回以 char 为单位的大小，因此表达式 CHAR_BIT * sizeof(int) 就是 int 中的位数。bin_str 数组有那么多元素，再加 1 用于存放终止的空字符。

itobs() 函数返回传入它的同一个地址，因此你可以将该函数用作，比如说，printf() 的参数。初次进入 for 循环时，函数计算表达式 01 & n。01 是一个掩码的八进制表示，除第 0 位外其余各位均设置为 0。因此，01 & n 就是 n 中最后一位的值。这个值是 0 或 1，但对于数组来说，你需要的是字符 '0' 或字符 '1'。加上 '0' 的编码即可完成这种转换。（这里假设数字是按顺序编码的，如在 ASCII 中那样。）结果被放在数组的倒数第二个元素中。（最后一个元素保留给空字符。）

顺便说一下，你也可以用 1 & n 代替 01 & n。使用八进制 1 而不是十进制 1 只是让气氛更有点计算机韵味。从这个角度看，也许 0x1 & n 甚至更好。

然后循环执行语句 i-- 和 n >>= 1。第一条语句将数组索引前移一个元素，第二条语句将 n 中的位向右移动一位。于是，下一次循环时，代码就会找到新的最右端位的值。相应的数字字符随即被放在最后一个数字之前的元素中。这样，函数就从右到左填充数组。

你可以使用 printf() 或 puts() 来显示结果字符串，但程序清单 15.1 定义了 show_bstr() 函数，它把位分成每 4 位一组，以便于阅读。

下面是一个示例运行：

```
Enter integers and see them in binary.
Non-numeric input terminates program.
7
7 is 0000 0000 0000 0000 0000 0000 0000 0111
2013
2013 is 0000 0000 0000 0000 0000 0111 1101 1101
-1
-1 is 1111 1111 1111 1111 1111 1111 1111 1111
32123
32123 is 0000 0000 0000 0000 0111 1101 0111 1011
q
Bye!
```

