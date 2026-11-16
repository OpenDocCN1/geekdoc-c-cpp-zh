

## 按位或

与逻辑或运算符（||）类似，按位或运算符（|）在至少一个操作数为真（即具有非零值）时产生真值。

| b1 | b2 | b1 \| b2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

```c
// or1.c

#include <stdio.h>

int main(void) {
    int x = 0x2719;    // 0010 0111 0001 1001
    int y = 0x85CD;    // 1000 0101 1100 1101
    int z;

    z = x | y;    // 1010 0111 1101 1101
    printf("z = 0x%x\n", z);    // A 7 D D
    return 0;
}
```

该程序的输出为：

```
z = 0xA7DD
```

按位或运算符用于将字中的指定位设置为1（即打开位）。例如，假设我们要将int的最右边3位设置为1，无论操作执行前这些位的状态如何：

```c
// or2.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;       // 0001 0010 0011 0100
    int mask = 0x0007;    // 0000 0000 0000 0111
    int z;
    z = x | mask;
    printf("z = 0x%x\n", z); // 0001 0010 0011 0111
    return 0;
}
```

该程序的输出为：

```
z = 0x1237
```

现在假设我们想编写一个程序来翻转int的第5位（如果是开则关；如果是关则开）。一种方法是：

```c
// flip1.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;       // 0001 0010 0011 0100
    int mask = 0x0010;    // 0000 0000 0001 0000
    if (x & mask)
        x &= 0xFFEF;      // bit is on, turn it off
    else
        x |= 0x0010;      // bit is off, turn it on
    printf("x = 0x%x\n", x); // 0001 0010 0001 0100
    return 0;
}
```

产生的输出为：

```
x = ...
```

这段代码工作正常，但可以使用按位异或运算符进行简化。

## 按位异或

按位异或运算符在两个操作数值不同时产生1，在两个操作数相同时产生0。

| b1 | b2 | b1 ^ b2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

例如：

```c
// xor1.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;
    int y = 0x85CD;
    int z;
    z = x ^ y;
    printf("z = 0x%x\n", z);
    return 0;
}
```

该程序的输出为：

```
z = 0x97F9
```

请注意，任何值与自身异或都会产生0：

```c
// xor2.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;
    printf("x = 0x%x\n", x ^ x);
    return 0;
}
```

该程序的输出为：

```
x = 0x0
```

此概念在汇编语言中经常用于清除寄存器：

```
XOR AL, AL
```

现在我们可以使用按位异或运算符来重写之前的程序，该程序用于翻转int从右数的第5位：

```c
// flip2.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;       // 0001 0010 0011 0100
    int mask = 0x0010;    // 0000 0000 0001 0000
    x ^= mask;            // 0001 0010 0010 0100
    printf("x = 0x%x\n", x);
    return 0;
}
```

产生的输出为：

```
x = 0x1224
```

按位异或运算符还可以用于交换两个值，而不需要临时第三个变量：

```c
// xor3.c

#include <stdio.h>

int main(void) {
    int x = 0x1234;    // 0001 0010 0011 0100
    int y = 0xABCD;    // 1010 1011 1100 1101

    x ^= y;
    y ^= x;
    x ^= y;
    printf("x = 0x%x\n", x);
    printf("y = 0x%x\n", y);
    return 0;
}
```

产生的输出为：

```
x = 0xABCD
y = 0x1234
```

## 按位取反

按位取反运算符是一个一元运算符。这意味着该运算符只需要一个操作数。其效果是翻转操作数的位。

| b | ~b |
|---|---|
| 0 | 1 |
| 1 | 0 |

例如：

```c
// negate1.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;    // 0001 0010 0011 0100
    int y;
    y = ~x;            // 1110 1101 1100 1011
    printf("y = 0x%x\n", y);
    return 0;
}
```

该程序的输出为：

```
y = 0xEDCB
```

请记住不要将按位取反（~）运算符与算术减（-）运算符或逻辑非（!）运算符混淆。例如，如果x等于0：

```
-x = 0
!x = 1   (true)
~x = -1  (when treated as a signed value)
```

请注意，按位与、按位或和按位异或的结果不依赖于计算机的字长，但按位取反的结果依赖。我们可以利用这一点。

假设我们想写一个二进制值，它由所有1位组成，除了低序3位。我们不应该将该值写为：

```
0xFFF8 (16-bit value)
```

也不应写为：

```
0xfffffff8 (32-bit value)
```

而应写为：

```
~7
```

这适用于任何字长！！！

当对两个大小不同的值（long和short）执行按位操作时，系统将操作数右对齐。如果两个项目中较短的是有符号量，且值为负，则符号将向左扩展以匹配较大值所包含的位数。

最后，按位运算符（&, |, ^）的优先级低于==和 !=。这意味着像这样的位测试表达式：

```
if ((x & mask) == 0)
```

必须完全加括号才能得到正确结果。

## 左移运算符

当对值执行左移（<<）操作时，值中的位将被向左移位。通过高序位移出的位将丢失，0始终移入低序位。

例如：

```c
// lshift.c
#include <stdio.h>
int main(void) {
    int num = 3;       // 0000 0000 0000 0011
    num = num << 1;    // 0000 0000 0000 0100
    printf("num = %d\n", num);
    return 0;
}
```

在上述程序中，num的所有位向左移一位。产生的输出为：

```
num = 6
```

请注意，将值左移一位相当于将被移位的值乘以2。左移操作也可以写成：

```
num <<= 1;
```

以下是一个输出16位int值位表示的函数：

```c
// bitpntr1.c

int bitpntr1(int num) {
    int i, mask;

    mask = 1;
    for (i = 1; i <= 16; i++) {
        printf(num & mask ? "1" : "0");
        num <<= 1;
    }

    return 0;
}
```

不幸的是，由于sizeof(int)在不同计算机上会有所不同，此函数不可移植。因此我们修改程序以使其可在不同计算机上移植，如下所示：

```c
// bitpntr2.c

int bitpntr2(int num) {
    int i, mask;

    mask = 1;
    for (i = 1; i <= sizeof(int)*8; i++) {
        printf(num & mask ? "1" : "0");
        num <<= 1;
    }

    return 0;
}
```

## 右移运算符

右移（>>）运算符将值的位向右移位。移出低序位的位将丢失。对无符号值进行右移将始终导致0移入左侧。

例如：

```c
// rshift.c
#include <stdio.h>
int main(void) {
    int num = 12;      // 0000 0000 0000 1100
    num = num >> 1;    // 0000 0000 0000 0110
    printf("%d\n", num);
    return 0;
}
```

在上述程序中，num的所有位向右移一位。产生的输出为：

```
num = 6
```

请注意，将值右移一位相当于将被移位的值除以2。右移操作也可以写成：

```
num >>= 1;
```

对于有符号值，移入左侧的内容取决于被移位值的符号，以及该操作在你的系统上的实现方式。如果符号位为0（正值），则无论我们在什么系统上，都会移入0。如果符号位为1，有些计算机会移入1（算术右移），有些会移入0（逻辑右移）。

C保证，如果尝试将值左移或右移的位数大于或等于数据项大小（左操作数）中的位数，则结果未定义。右操作数不能为负。以下是一个用于计算整数参数中1位数量的函数。

```c
// bitcount.c

int bitCount(unsigned num) {
    int count = 0;

    while(num) {
        if(num & 1) {
            count++;
        }
        num >>= 1;
    }
    return count;
}
```

以下是几个可移植程序，用于计算int中的位数。

```c
// numbits1.c

#include <stdio.h>
int main(void) {
    int i = 0, num = 1;

    while(num) {
        num <<= 1;
        i++;
    }
    printf("%d\n", i);
    return 0;
}
```

