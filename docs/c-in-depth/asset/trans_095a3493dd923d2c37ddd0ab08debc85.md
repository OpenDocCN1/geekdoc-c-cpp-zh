
b15 b14 b13 b12 b11 b10 b9 b8 b7 b6 b5 b4 b3 b2 b1 b0  （原始值）
0 0 0 0 0 0 0 0 0 1 0 0 0 0 0  （掩码）
b15 b14 b13 b12 b11 b10 b9 b8 b7 b6 b5 b4 b3 b2 b1 b0  （新值）

mask = 0x20;
a = a ^ mask

因此，我们可以使用该运算符在 0 和 1 之间翻转位。例如，如果我们有一个整型变量 a，并且想要翻转它的第 5 位。

假设最初变量 a 中的第 5 位为 1
mask = 0x20;
a = a ^ mask   （第 5 位变为 0，其他所有位保持不变）
a = a ^ mask   （第 5 位变为 1，其他所有位保持不变）
a = a ^ mask   （第 5 位变为 0，其他所有位保持不变）

从上述操作我们还可以看出，当一个操作数与一个值进行两次异或运算时，结果与原操作数相同。这一特性可用于加密。

例如，如果变量 var 的初始值为 var = 0xF13A
var = var ^ 0x1F; （加密）
var = var ^ 0x1F; （解密）
执行第一条语句后，var 的值变为 0xF125，而执行第二条语句后，我们得到 var 的原始值（0xF13A）。

```
/*P13.9 A program to toggle 5th bit using bitwise XOR operator*/
#include<stdio.h>
main()
{
    int a,bit_mask=0x20;
    printf("Enter an integer : ");
    scanf("%d",&a);
    printf("a = %d\t",a);    bit_pattern(a);
    a = a^bit_mask;
    printf("a = %d\t",a);    bit_pattern(a);
    a = a^bit_mask;
    printf("a = %d\t",a);    bit_pattern(a);
}
```

当一个值与自身进行异或运算时，结果为 0，这很明显，因为所有对应位都相同。例如，像 var^var 这样的表达式的值将为 0。异或运算符的这一特性可用于比较两个值是否相等。

## 13.8.4 使用按位与和按位取反运算符关闭位

我们已经看到，可以使用按位与运算符关闭位。让我们看看使用按位与运算符时会出现什么样的可移植性问题。

假设我们想要关闭整型变量 a 的第 5 位，可以将掩码取为 - 1111 1111 1101 1111 (0xFFDF)

```
a = a & 0xFFDF;
```

现在假设我们在使用 32 位存储整数的计算机上使用这段代码，那么 0xFFDF 将被表示为 -
0000 0000 0000 0000 1111 1111 1101 1111

现在这个掩码还会关闭最左边的 16 位，这不是我们想要的结果。因此，在使用 32 位表示整数的计算机上，关闭第 5 位所需的合适掩码应该是 -
1111 1111 1111 1111 1111 1111 1101 1111 ( 0xFFFFFFDF )

```
a = a & 0xFFFFFFDF;
```

如果我们能为两种类型的计算机编写同一行代码，那就更好了。我们可以通过将按位取反运算符与 AND 运算符结合来实现，如下所示 -

```
a = a & ~0x20
```

在使用 16 位表示整数的计算机上，这被解释为 -
a = a & 1111 1111 1101 1111
而在使用 32 位表示整数的计算机上，这被解释为 -
a = a & 1111 1111 1111 1111 1111 1111 1101 1111

```
/*P13.10 A program to switch off the 5th bit*/
#include<stdio.h>
main()
{
int a,bit,mask=0x20;
printf("Enter an integer : ");
scanf("%d",&a);
printf("a = %d\t",a);  bit_pattern(a);
a=a&~mask;
printf("After switching off the 5th bit, the value of a is :\n");
printf("a = %d\t",a);  bit_pattern(a);
}
```

现在让我们总结对整型变量 a 中第 5 位的不同操作 -
mask = 0x20;
测试变量 a 中的第 5 位：a & mask
打开变量 a 中的第 5 位：a = a | mask;
关闭变量 a 中的第 5 位：a = a & ~ mask;
反转变量 a 中的第 5 位：a = a ^ mask;

类似地，我们可以通过这些操作处理任意位，只需恰当地选择掩码。
处理第 6 位：mask = 0x40  (0000 0000 0100 0000)
处理第 9 位：mask = 0x200  (0000 0010 0000 0000)
处理第 3 位和第 6 位：mask = 0x48  (0000 0000 0100 1000)
我们可以通过将整数 1 左移位数来计算掩码。
处理第 4 位：mask = 1<<4 ( 0000 0000 0001 0000 )
处理第 6 位：mask = 1<<6 ( 0000 0000 0100 0000 )

```
/*P13.11 Program to test any bit in an integer*/
#include<stdio.h>
main()
{
    int a,bit,mask,bitposition;
    printf("Enter an integer : ");
    scanf("%d",&a);
    printf("Enter the bit position : ");
    scanf("%d",&bitposition);
    mask=1<<bitposition;
    printf("a = %d\t",a);    bit_pattern(a);
    if((a&mask)==0)
        bit=0;
    else
        bit=1;
    printf("The bit at position %d is %d\n",bitposition,bit);
}
```

如果我们想逐位处理所有位，那么可以使用循环。例如，下面这个程序将打开整型变量 a 中的所有位。

```
/*P13.12 Program to switch on all the bits in an integer variable*/
#include<stdio.h>
main()
{
    int a,mask,i;
    printf("Enter the value of a : ");
    scanf("%d",&a);
    printf("%d\t",a);  bit_pattern(a);
    for(i=0;i<=15;i++)
    {
        mask=1<<i;
        a=a|mask;  /*switch on the ith bit*/
    }
    printf("%d\t",a);  bit_pattern(a);
}
```

还有另一种方法可以为特定位置计算合适的掩码。我们可以采用一个掩码数组，如下所示 -

unsigned int arr_mask[] = { 0x1, 0x2, 0x4, 0x8, 0x10, 0x20, 0x40, 0x80, 0x100, 0x200, 0x400, 0x800, 0x1000, 0x2000, 0x4000, 0x8000};

现在，用于处理任意位的掩码可以这样计算 -
    mask = arr_mask[bitposition];

例如，要打开第 4 位，我们可以写
    x = x | arr_mask[4];

## 13.9 一些附加问题

### 问题 1

编写一个程序，打印 16 位整数的位模式。

现在我们可以编写一直使用的函数 bit_pattern() 的定义了。打印整数的二进制模式需要测试该整数中的每一位。位编号是从右到左，但我们必须从左到右打印各位，因此首先打印第 15 位，然后打印第 14 位，依此类推，直到第 0 位。所以我们将从第 15 位开始测试各位。要测试第 15 位，掩码应为 1<<15。类似地，要测试第 14 位，掩码应为 1<<14，依此类推。

```
/*P13.13 Printing the binary pattern of a 16 bit integer*/
#include<stdio.h>
main()
{
    int a;
    printf("Enter an integer : ");
    scanf("%d",&a);
    bit_pattern(a);
}
bit_pattern(int a)
{
    int i,mask;
    for(i=15;i>=0;i--)
    {
        mask=1<<i;
        if((a&mask)==0)
            printf("0");
        else
            printf("1");
    }
    printf("\n");
}
```

第 1 次迭代中，掩码为：1000 0000 0000 0000，测试并打印第 15 位
第 2 次迭代中，掩码为：0100 0000 0000 0000，测试并打印第 14 位
第 3 次迭代中，掩码为：0010 0000 0000 0000，测试并打印第 13 位
....................
....................
最后一次迭代中，掩码为：0000 0000 0000 0001，测试并打印第 0 位

为了使该程序具有可移植性，我们可以将 for 循环修改为 -
for( i = sizeof(int)-1 ; i>=0; i-- )

### 问题 2

编写一个程序，使用按位运算符判断一个数是偶数还是奇数。

如果一个数的最低有效位（最右边）为 1，则该数为奇数；如果其最低有效位为 0，则该数为偶数。这意味着我们只需测试最低有效位是 1 还是 0。我们知道按位与运算符适合测试位。现在我们必须选择合适的掩码。由于我们要检查最右边的位，因此将采用最右边位为 1、所有其他位为 0 的掩码。

```
/*P13.14 Program to find whether a number is even or odd*/
#include<stdio.h>
main()
{
    int num;
    int mask=0x1;
    printf("Enter a number : ");
    scanf("%d",&num);
    if((num&mask)==0)
        printf("Number is even\n");
    else
        printf("Number is odd\n");
}
```

### 问题 3

编写一个程序，输入小于或等于 16 位的二进制模式，并将其转换为整数

```
/*P13.15 Program to convert a binary pattern to an integer*/
#include<stdio.h>
main()
{
    char bit;
    int i,num=0;
    printf("Enter any bit pattern less than or equal to 16 bits :\n");
    for(i=0;i<=15;i++)
    {
        bit=getchar();
        if(bit=='0')
            num=num<<1;
        else if(bit=='1')
            num=(num<<1)+1;
        else
            break;
    }
    printf("Hexadecimal : %x\n",num);
    printf("Decimal : %d\n",num);
}
```

### 问题 4

编写一个程序，在给定的无符号 16 位整数中交换前 8 位和后 8 位。

例如，如果最初的位模式为 - 1000 1111 0011 0001
交换后应变为 - 0011 0001 1000 1111
这可以通过以下方式实现 -
x          1000 1111 0011 0001
x<<8       0011 0001 0000 0000
x>>8       0000 0000 1000 1111
x<<8 | x>>8 0011 0001 1000 1111
如果该整数是无符号的，则此方法可以正常工作；但如果该整数是有符号负数，那么根据算术移位，在右移后，最左边的 8 位将被填充为 1
