
当你使用 `<<` 运算符将移位结果存储到变量中时，请确保变量的类型足够大以容纳该值。例如，考虑以下程序：

```c
#include <stdio.h>
int main(void)
{
    unsigned char a = 1;

    a <<= 8; /* Equivalent to a = a << 8; */
    printf("%d\n", a);
    return 0;
}
```

语句 `a <<= 8;` 将 `a` 的值向左移动八位，并在右侧插入八个零位。因此，移位结果为 100000000。然而，由于 `a` 被声明为 `unsigned char`，它只能保存八个低位的值。因此，程序显示 0 而不是你可能期望的 256。如果它被声明为 `int`，程序将显示 256。

再看另一个例子。如果我们写：

```c
char a = 8;
a <<= 4;
```

`a` 的值向左移动四位并变为 10000000。如果 `char` 类型是有符号的，最左边的位保留用于数字的符号，`a` 变为 -128。如果 `a` 被声明为 `unsigned char`，其值将为 128。

> 记住，使用无符号类型执行位运算更安全。

## Exercises

### C.4.7

编写一个程序，读取一个对应于密码密钥的整数，以及另一个将用该密钥加密的整数。加密是通过对它们应用 `^` 运算符来执行的。然后，程序应再次使用 `^` 运算符来解密加密后的结果。

```c
#include <stdio.h>
int main(void)
{
    int num, key;

    printf("Enter key: ");
    scanf("%d", &key);

    printf("Enter number: ");
    scanf("%d", &num);

    num = num ^ key;
    printf("Encrypted : %d\n", num);

    num = num ^ key;
    printf("Original: %d\n", num);
    return 0;
}
```

**Comments:** 由于 `(a ^ b) ^ b = a`，解密的结果是输入的数字。

### C.4.8

以下程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    printf("%d\n", ~(~0 << 4));
    return 0;
}
```

**Answer:** 根据附录 A 中的优先级表，`~` 运算符的优先级高于 `<<` 运算符；因此，先计算表达式 `~0`，然后将结果向左移动四位。在 32 位系统中，`~0` 的结果是所有 32 位都设为 1 的数字。因此，`(~0 << 4)` 的值是数字：

```
11111111 11111111 11111111 11110000
```

由于 `~` 运算符反转其位，整个表达式的值为：

```
00000000 00000000 00000000 00001111
```

程序显示 15。

### C.4.9

以下程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    unsigned int i = 10;
    if((i >> 4) != 0)
        printf("One\n");
    else
        printf("Two\n");
    printf("%d\n", i);
    i = i;
    if((i << 3) == 8)
        printf("One\n");
    else
        printf("Two\n");
    printf("%d\n", i);
    return 0;
}
```

```c
#include <stdio.h>
int main(void)
{
    unsigned int num, pos;
    printf("Enter number: ");
    scanf("%d", &num);
    printf("Enter bit position [1-32]: ");
    scanf("%d", &pos);
    printf("bit%d is %d\n", pos, (num >> (pos-1)) & 1);
    return 0;
}
```

### C.4.12

编写一个程序，读取 [0, 255] 范围内的整数，然后交换其二进制数字的两个四位组并显示新的数字。例如，如果用户输入 10 (00001010)，程序应显示 160 (10100000)。

```c
#include <stdio.h>
int main(void)
{
    unsigned char num, tmp;
    printf("Enter number [0-255]: ");
    scanf("%d", &num);
    tmp = num & 0xF; /* The value of the four lower bits is stored into tmp. 0xF is 1111 in binary. Of course, we could use 15 instead of 0xF. */
    tmp <<= 4; /* Shift the value four places to the left. */
    tmp += num >> 4; /* Add to tmp the value of num shifted four places to the right. */
    printf("%d\n", tmp);
    return 0;
}
```

**Comments:** 如果你想知道 `num` 的值，它的值不会改变。此外，我们可以省略 `tmp` 并写：`printf("%d\n", ((num & 0xF) << 4) + (num >> 4));` 或 `printf("%d\n", (unsigned char)(num << 4) + (num >> 4));`

### C.4.13

位运算符常用于网络通信中的数据编码。例如，传输控制协议 (TCP) 数据包头部中的某些特定位被编码如图所示 4.1 所示。

![](img/b8da5dcf9ba7f1fad5213c453d095246_86_0.png)

- FIN (bit1): 如果为 1，则表示 TCP 连接的释放。
- SYN (bit2): 如果为 1，则表示 TCP 连接的建立。这就是臭名昭著的负责拒绝服务 (DoS) 洪水攻击的位，但这是另一个故事...
- ACK (bit5): 如果为 1，则表示数据接收的确认。
- URG (bit6): 如果为 1，则表示紧急数据的传输。

编写一个程序，读取 URG、ACK、SYN 和 FIN 位的值并将此信息编码到程序变量中。然后，程序应解码该变量的值并显示各位的值。

```c
#include <stdio.h>
int main(void)
{
    unsigned char temp, urg, ack, syn, fin;

    printf("Enter FIN bit: ");
    scanf("%d", &fin);

    printf("Enter SYN bit: ");
    scanf("%d", &syn);

    printf("Enter ACK bit: ");
    scanf("%d", &ack);

    printf("Enter URG bit: ");
    scanf("%d", &urg);

    temp = fin + (syn << 1) + (ack << 4) + (urg << 5);
    printf("\nEncoding: %d\n", temp);

    fin = temp & 1;
    syn = (temp >> 1) & 1;
    ack = (temp >> 4) & 1;
    urg = (temp >> 5) & 1;
    printf("FIN = %d, SYN = %d, ACK = %d, URG = %d\n", fin, syn, ack, urg);

    return 0;
}
```

### C.4.14

以下程序做什么？

```c
#include <stdio.h>
int main(void)
{
    unsigned char ch = 3;

    ch = ((ch&1) << 7) | ((ch&2) << 5) | ((ch&4) << 3) | ((ch&8) << 1)
    | ((ch&16) >> 1) | ((ch&32) >> 3) | ((ch&64) >> 5) | ((ch&128) >> 7);
    printf("%d\n", ch);
    return 0;
}
```

**Answer:** 假设 `ch` 以二进制编码为 `x_7x_6x_5x_4x_3x_2x_1x_0`，其中每个 `x_i` 为 1 或 0。因此，表达式 `(ch&1) << 7` 的值为：

```text
    x_7 x_6 x_5 x_4 x_3 x_2 x_1 x_0
&   0   0   0   0   0   0   0   1
-------------------------------------
    0   0   0   0   0   0   0   x_0 << 7 = x_0 0   0   0   0   0   0   0
```

同样，`(ch&2) << 5` 的值为：

```text
    x_7 x_6 x_5 x_4 x_3 x_2 x_1 x_0
&   0   0   0   0   0   0   1   0
-------------------------------------
    0   0   0   0   0   0   x_1 0 << 5 = 0 x_1 0   0   0   0   0   0
```

以类似的方式：

```text
The value of (ch&4) << 3 is: 0 0 x_2 0 0 0 0 0
The value of (ch&8) << 1 is: 0 0 0 x_3 0 0 0 0
The value of (ch&16) >> 1 is: 0 0 0 0 x_4 0 0 0
The value of (ch&32) >> 3 is: 0 0 0 0 0 x_5 0 0
The value of (ch&64) >> 5 is: 0 0 0 0 0 0 x_6 0
The value of (ch&128) >> 7 is: 0 0 0 0 0 0 0 x_7
```

因此，整个表达式被计算为：

```text
(x_0 0 0 0 0 0 0 0) | (0 x_1 0 0 0 0 0 0) | (0 0 x_2 0 0 0 0 0) | (0 0 0 x_3 0 0 0 0) |
(0 0 0 0 x_4 0 0 0) | (0 0 0 0 0 x_5 0 0) | (0 0 0 0 0 0 x_6 0) | (0 0 0 0 0 0 0 x_7) =
x_0 x_1 x_2 x_3 x_4 x_5 x_6 x_7
```

事实上，程序反转了 `ch` 的位，而不使用第二个变量。因此，`ch` (00000011₂) 变为 192 (11000000₂)，程序显示 192。

### C.4.15

位运算符常用于与硬件通信的应用程序中。例如，异步串行通信中常用的配置方法是八位字符，具有一个 *起始位*、一个 *停止位* 和一个 *奇偶校验位*。数据的传输通过将 *起始位* 设为 0 来发出信号，以通知接收方数据的到来。*停止位* 表示传输的结束。例如，数据位 10100 被编码如图所示 4.2 所示。

![](img/b8da5dcf9ba7f1fad5213c453d095246_88_0.png)

**FIGURE 4.2**
Communication example.

发送方可以选择性地传输 *奇偶校验位*，接收方用它来检测传输错误。奇偶校验有两种变体：偶校验和奇校验。在偶校验中，*奇偶校验位* 的值是按这样计算的，使得数据中 1 的总数加上奇偶校验位为偶数。在奇校验的情况下，总数应为奇数。在我们的示例中，我们选择偶校验。因此，由于数据中 1 的数量为二，即为偶数，*奇偶校验位* 设为 0。

编写一个程序来模拟发送方。程序应读取五个数据位的值并使用偶校验生成一个 8 位值。

```c
#include <stdio.h>
int main(void)
{
    unsigned char data, ones, bit1, bit2, bit3, bit4, bit5,
parity_bit;

    ones = 0;

    printf("Enter bit1: ");
    scanf("%d", &bit1);
    if (bit1 == 1)
        ones++;

    printf("Enter bit2: ");
    scanf("%d", &bit2);
    if (bit2 == 1)
        ones++;

    printf("Enter bit3: ");
    scanf("%d", &bit3);
    if (bit3 == 1)
        ones++;

    printf("Enter bit4: ");
    scanf("%d", &bit4);
    if (bit4 == 1)
        ones++;

    printf("Enter bit5: ");
    scanf("%d", &bit5);
    if (bit5 == 1)
        ones++;

    if (ones & 1) /* It means that the number of 1s is odd. */
        parity_bit = 1;
    else
        parity_bit = 0;

    data = (bit1 << 6) + (bit2 << 5) + (bit3 << 4) + (bit4 << 3) +
(bit5 << 2) + (parity_bit << 1) + 1; /* The last 1 represents the
stop_bit. */
    printf("%d\n", data);
    return 0;
}
```
