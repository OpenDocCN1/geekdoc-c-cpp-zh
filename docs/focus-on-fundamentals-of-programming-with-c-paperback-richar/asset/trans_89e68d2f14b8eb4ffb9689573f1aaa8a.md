

## 左移运算符

对一个值执行左移（`<<`）操作时，值中包含的位将被字面意义上向左移位。通过高阶位移出的位将丢失，0 总是移入低阶位。

例如：

```c
// lshift.c

#include <stdio.h>

int main(void) {
    int num = 3;        // 0000 0000 0000 0011

    num = num << 1;     // 0000 0000 0000 1100
    printf("num = %d\n", num);
    return 0;
}
```

在上面的程序中，`num` 的所有位都向左移了一位。输出结果是：

num = 6

请注意，将一个值左移一位相当于将该值乘以 2。左移操作也可以写成：

```
num <<= 1;
```

以下是一个输出 16 位 `int` 值位表示的函数：

```c
// bitprnt1.c
int bitprnt1(int num) {
    int i, mask;
    mask = 1;
    mask <<= 15;
    for (i = 1; i <= 16; i++) {
        printf(num & mask ? "1" : "0");
        num <<= 1;
    }
    return 0;
}
```

不幸的是，由于不同计算机上的 `sizeof(int)` 会有所不同，因此此函数不可移植。我们因此修改程序，使其可在不同计算机上移植，如下所示：

```c
// bitprnt2.c
int bitprnt2(int num) {
    int i, mask;
    mask = 1;
    mask <<= (sizeof(int) * 8) - 1;
    for (i = 1; i <= sizeof(int) * 8; i++) {
        printf(num & mask ? "1" : "0");
        num <<= 1;
    }
    return 0;
}
```

## 右移运算符

右移（`>>`）运算符将一个值的位向右移位。从低阶位移出的位将丢失。对无符号值进行右移时，左侧总是移入 0。

例如：

```c
// rshift.c
#include <stdio.h>
int main(void) {
    int num = 12;       // 0000 0000 0000 1100
    num = num >> 1;     // 0000 0000 0000 0110
    printf("%d\n", num);
    return 0;
}
```

在上面的程序中，num 的所有位都向右移了一位。输出结果是：

```
num = 6
```

请注意，将一个值右移一位相当于将该值除以 2。右移操作也可以写成：

```
num >>= 1;
```

对于有符号值，左侧移入的内容取决于被移位值的符号，以及该操作在你的系统上的实现方式。如果符号位为 0（正值），则无论在什么系统上，都会移入 0。如果符号位为 1，有些计算机会移入 1（算术右移），有些会移入 0（逻辑右移）。

C 标准规定，如果尝试将一个值左移或右移的位数大于或等于数据项（左操作数）大小的位数，则结果未定义。右操作数不能为负数。以下是一个统计整数参数中 1 位数量的函数。

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

以下是几个可移植的程序，用于计算 int 中的位数。

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

```c
// numbits2.c

#include <stdio.h>

int main(void) {
    int i;
    unsigned num = ~0;

    for (i = 0; num > 0; i++) {
        num >>= 1;
    }
    printf("%d\n", i);
    return 0;
}
```

```c
// numbits3.c

#include <stdio.h>

int main(void) {
    int i;
    unsigned num = ~0;

    for (i = 1; num >>= 1; i++) {
    }
    printf("%d\n", i);
    return 0;
}
```

## 旋转示例

汇编语言代码通常包含两条旋转指令。旋转右（ROR）指令将位向右移位。从右侧移出的位会从左侧移回。例如，以下汇编指令：

```
MOV AL, 10111011
ROR AL, 1
```

其效果是将一位从右侧移出并移回左侧：

![](img/0603fdf2eefeabaf26542250cc2fb439_545_0.png)

寄存器 AL 现在包含值 11011101。

旋转左（ROL）指令将位向左移位。从左侧移出的位会从右侧移回。例如，以下汇编指令：

```
MOV AL, 10000000
ROL AL, 1
```

其效果是将一位从左侧移出并移回右侧：

![](img/0603fdf2eefeabaf26542250cc2fb439_545_1.png)

寄存器 AL 现在包含值 00000001。请注意，如果你旋转 8 次，最终会得到原始数字！

不幸的是，C 语言没有左旋或右旋运算符。因此，让我们开发一个函数来模拟左旋和右旋语句。该函数将接受两个参数：

要旋转的值 (num)

值将被旋转的位数 (x)。如果 x 是正整数，我们将执行左旋；如果 x 是负整数，我们将执行右旋。

为了计算将 num 向左旋转 x 位的结果，我们将使用以下三步算法：

- 提取 num 的最左 x 位。
- 将 num 向左移 x 位。
- 将提取的位放回 num 的右侧。

我们将使用类似的算法来执行右旋。

```c
// rotate.c
unsigned rotate(unsigned num, int x) {
    unsigned bits, result;

    if (x > 0) {
        bits = num >> (sizeof(unsigned)*8 - x);
        result = num << x | bits;
    }
    else {
        x = -x;
        bits = num << (sizeof(unsigned)*8 - x);
        result = num >> x | bits;
    }
    return result;
}
```

## 位运算作业

- 1. 设 b1 = b2 = 1。以下哪项的结果与其他项不同？
  - a) b1 & b2
  - b) b1 | b2
  - c) b1 ^ b2
  - d) ~(~b2)

- 2. 求表达式的值：(00001000 & 11000101) ^ (11110000)
  - a) 00111101
  - b) 11000000
  - c) 00111101
  - d) 11110000

- 3. 对于任意 8 位整数 x，以下哪项的结果不是零？
  - a) x &= (~x)
  - b) x ^= x
  - c) x <<= 8
  - d) x |= x

- 4. 以下哪项是正确的？
  - a) 任何位与 0 "与" 的结果为 0。
  - b) 任何位与 1 "与" 的结果为 1。
  - c) 任何位与 0 "与" 的结果为 1。
  - d) 任何位与 1 "与" 的结果为 0。

- 5. 编写一条 C 语句，将 32 位整数 num 的中间 16 位设置为 0，但保留左侧 8 位和右侧 8 位的原始值。

- 6. 编写一个 C 函数，原型如下：

int compare(int x, int y);

该函数返回 x 和 y 中对应位不同的数量。例如，如果 x = 9 且 y = 97，则对应位不同的数量为三。

x = 9 = 0000 0000 0000 0000 0000 0000 0000 1001
y = 97 = 0000 0000 0000 0000 0000 0000 0110 0001

### 第一部分

编写一个名为 bitSet.c 的程序，其中包含一个名为 bitSet() 的函数，该函数将 int 中的指定位数设置为特定值，并以十六进制表示法输出结果 int。函数原型如下：

```c
void bitSet(int *num, int value, int start, int size);
```

函数参数定义如下：

| num | 指向要设置指定位的 int 的指针 |
| :--- | :--- |
| value | 包含要设置的值的 int，右对齐 |
| start | 指定起始位号的 int，最左侧位编号为 0 |
| size | 指定字段大小的 int |

例如，调用：

```
bitSet(&num, 0, 2, 5);
```

其效果是将 num 中从左侧第三位（位号 2）开始的五位设置为零。

同样，调用：

```
bitSet(&num, 0X55, 0, 8);
```

将把 num 的八个最左位设置为十六进制 55。

你的程序应能处理以下给定的数据：

| num | value | start | size |
|---|---|---|---|
| 0x12345678 | 0x0 | 2 | 5 |
| 0xABCD1234 | 0x55 | 0 | 8 |
| 0x0000FFFF | 0x17 | 4 | 9 |
| 0x76543210 | 0xAB | 7 | 8 |
| 0x00002F7A | 0xC4 | 3 | 10 |

请注意，你可以将测试数据硬编码到程序中。

### 第二部分

编写一个名为 bitSearch.c 的程序，其中包含一个名为 bitSearch() 的函数，该函数在 int 内部查找指定位模式的出现情况。函数原型如下：

```c
int bitSearch(int source, int pattern, int n);
```

该函数将从最左侧位开始搜索整数 source，以查看 pattern 的最右 n 位是否出现在 source 中。如果找到 pattern，则让函数返回模式开始的位号，其中最左侧位为位号 0。如果未找到 pattern，则让函数返回 -1。

例如，调用：

```
index = bitSearch(0x21F41234, 0x5, 3);
```

将导致 bitSearch() 搜索以下数字：

```
0x21F41234 (0010 0001 1111 0100 0001 0010 0011 0100)
```

