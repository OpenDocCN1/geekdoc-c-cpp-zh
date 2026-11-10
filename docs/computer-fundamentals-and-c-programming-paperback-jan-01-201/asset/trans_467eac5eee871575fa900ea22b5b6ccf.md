

### 17.9.7 `>>` 运算符：按位右移

`>>` 右移运算符执行与 `<<` 相同的功能，但从 MSB 端（即数字的左端）开始。语法也类似：

```
operand >> num
```

`operand` 中的每一位根据 `num` 指定的位数向右移动。因此，`129 >> 1` 将 129 中的位向右移动一位。此操作丢弃 LSB 端的位，并在 MSB 端补零，如下所示：

```
10000001                        Decimal 129
01000000                        Decimal 64; result of 129 >> 1
```

左移将数字乘以 2，而右移则将数字除以 2。请注意，这种整数除法会截断小数部分。你可以将操作结果赋给变量：

```
y = x >> 4;
y >>= 4;                    等价于 y = y >> 4
```

对带符号数字使用 `>>` 运算符时需要特别注意，此时符号位本身也会被右移。ANSI 标准对左端的填充方式未作规定，因此不能想当然地认为会补零。结果实际上是依赖于实现的。

`>>` 运算符通过移动掩码中的位，从目标数字中提取位非常有用。程序 17.3 利用这一特性将十进制数转换为二进制数。

> **要点：** 每次移动一位时，`<<` 运算符将数字乘以 2，而 `>>` 将数字除以 2。整数除法会截断数字的小数部分。

> **注意：** 一般来说，使用按位移位运算符对数字进行乘除运算，比使用对应的算术运算符执行的速度更快。

## 17.10 `bitwise_operations.c`：使用按位运算符

程序 17.3 总结了除一个（`~`）之外所有按位运算符的特性。这个由四部分组成的程序，前两部分使用 AND 和 OR 运算符配合掩码来清除和设置一个短整数中的某个位。第三部分使用 XOR 在不使用临时变量的情况下交换两个数字。第四部分使用移位运算符将数字乘以或除以 2 的倍数。为便于理解，数字通常使用用户自定义的 `dec2bin` 函数以二进制形式显示。

```c
#include <stdio.h>
char *dec2bin(unsigned short num);
int main(void)
{
    unsigned short i, j, mask;
    i = 140; mask = 247;
    fputs("Clearing Bit 3 ...\n", stderr);
    printf("    i = %s (Decimal: %hd)\n", dec2bin(i), i);
    printf("mask = %s (Decimal: %hd)\n", dec2bin(mask), mask);
    j = i & mask;
    printf("    j = %s (Decimal: %hd)\n\n", dec2bin(j), j);
    i = 192; mask = 8;
    fputs("Setting Bit 3 ...\n", stderr);
    printf("    i = %s (Decimal: %hd)\n", dec2bin(i), i);
    printf("mask = %s (Decimal: %hd)\n", dec2bin(mask), mask);
    j = i | mask;
    printf("    j = %s (Decimal: %hd)\n\n", dec2bin(j), j);
    j = 50;
    printf("Before swapping, i = %hd, j = %hd\n", i, j);
    i ^= j;
    j ^= i;
    i ^= j;
    printf("After swapping, i = %hd, j = %hd\n\n", i, j);
    i = 25;
    printf("    i = %s (Decimal: %hd)\n", dec2bin(i), i);
    j = i << 2;
    fputs("Shifting left using i << 2 ...\n", stderr);
    printf("    j = %s (Decimal: %hd)\n", dec2bin(j), j);
    fputs("Shifting right using j >> 2 ...\n", stderr);
    printf("j >> 2: %s (Decimal: %hd)\n", dec2bin(j >> 2), j >> 2);
    return 0;
}

char *dec2bin(unsigned short num)
{
    unsigned short mask = 32768;  /* MSB = 1; other 15 bits = 0 */
    short i = 0;
    static char stg[17];          /* One slot reserved for NULL */
    while (mask > 0) {
        stg[i++] = (num & mask) == 0 ? '0' : '1';
        if (i == 8)
            stg[i++] = ' ';       /* A space after every 8 bits */
        mask = mask >> 1;         /* Shifts the 1 in MSB to the right */
    }
    stg[i] = '\0';
    return stg;
}
```

程序 17.3：**bitwise_operations.c**

```
Clearing Bit 3 ...
    i = 00000000 10001100 (Decimal: 140)
mask = 00000000 11110111 (Decimal: 247)
    j = 00000000 10000100 (Decimal: 132)

Setting Bit 3 ...
    i = 00000000 11000000 (Decimal: 192)
mask = 00000000 00001000 (Decimal: 8)
    j = 00000000 11001000 (Decimal: 200)

Before swapping, i = 192, j = 50
After swapping,  i = 50, j = 192

    i = 00000000 00011001 (Decimal: 25)
Shifting left using i << 2 ...
    j = 00000000 01100100 (Decimal: 100)
Shifting right using j >> 2 ...
j >> 2: 00000000 00011001 (Decimal: 25)
```

程序输出：**bitwise_operations.c**

前两部分清除和设置了整数 140 中的第 3 位（从右边数第 4 位）。注意，用于与 140 进行 AND 运算的所选掩码（247）在该位置为 0（11110111）。另一个掩码（8）的第 3 位为 1（00001000）。第三部分通过三个 XOR 操作交换两个整数，重新赋值 i 和 j。最后一部分将位移动两次，每侧各一次，其效果是将原始数字乘以 4 再除以 4。

**dec2bin** 函数在程序中多次使用。该函数返回一个字符串（即其指针），表示作为参数传入的十进制数的二进制等价形式。16 次循环迭代中，每次都将掩码中的置位位向右移动，从而将其值从 32768（第 15 位为 1）逐步减小到 1。在此过程中，`num & mask` 操作提取 `num` 中的每一位，并将该位以字符形式（'0' 和 '1'，而不是 0 和 1）保存到数组 `stg` 中。你将会发现，在处理按位运算符时，这个简单的函数非常有用。

## 17.11 指向函数的指针

*指向函数的指针*是一种强大而实用的工具，它允许函数 f2 或 f3 作为参数传递给函数 f1。由于可以在运行时决定选择 f2 还是 f3，因此通过指针声明、赋值和调用函数的整个过程可能有些棘手。不过，正如你很快就会发现的，其实不必如此。

正如变量在内存中有地址一样，函数也有地址。你可以将指针指向函数代码及其变量在内存中的基地址。表示指向函数指针的变量必须声明，然后将函数赋值给它，再通过解引用来执行所指向的函数。

以下语句声明了一个名为 fp1 的函数指针，它用于指向一个不带参数且不返回任何值的函数：

```
void (*fp1)();
```

*当前 fp1 尚未指向任何函数。*

这里，我们有一个指针变量 fp1，它*可以*指向一个不带参数（右边的 `()`）且不返回任何值（void）的函数。包裹 `*fp1` 的括号只是为了覆盖 `()` 相对于星号的默认优先级。如果使用 `void *fp1();`，则定义的是一个返回 void 指针的函数 fp1。

指针 fp1 现在可以指向一个函数，但只能指向不带参数且返回 void 的函数。如果以如下方式定义了一个名为 **print_something** 的函数：

```
void print_something(void)
{
    printf("Hello World\n");
    return;
}
```

那么我们可以用以下任一方式将此函数名赋给 fp1：

```
fp1 = print_something;
fp1 = &print_something;
```

*& 是可选的*

与数组类似，函数名表示指向其基地址的指针。由于 fp1 是一个指针变量，它可以与 **print_something** 断开，并转而指向另一个签名相同的函数。

我们现在可以使用指针来执行 **print_something**。这里我们同样有两种选择。由于 fp1 包含函数地址，我们可以解引用该地址并“求值”该地址处的内容。在这种情况下，求值意味着执行函数本身：

```
(*fp1)();
```

*执行 print_something 函数*

但 C 是一种智能语言。它知道你在尝试执行函数，因此它也允许你直接执行 fp1，而无需携带额外的符号：

```
fp1();
```

*同样执行 print_something 函数*

在探讨将 fp1 作为参数传递给另一个函数的机制之前，我们先考虑另一种类型的函数指针。接下来将讨论这一点。

### 17.11.1 用于带参数函数的函数指针

大多数函数使用参数并返回一个值，我们必须知道如何使用指向此类函数的指针。以下语句声明了一个函数指针 fp2，所指向的函数接受两个 float 参数并返回一个 float：

```
float (*fp2)(float, float);
```

我们可以为两个参数添加变量名，但编译器会直接忽略它们。在这里提供名称没有多大意义，因为 fp2 可以指向多个函数，而这些函数中的参数可能具有不同的名称。我们现在需要定义一个与 fp2 签名匹配的函数，例如 **add**：

