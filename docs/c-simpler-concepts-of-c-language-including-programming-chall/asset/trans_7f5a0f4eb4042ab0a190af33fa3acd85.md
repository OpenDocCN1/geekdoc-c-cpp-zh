
如果两个部分都是 1，那么 AND 运算符将求值为 1，结果打印“Login Successful”（登录成功）。

→ 如果 && (AND) 表达式的第一部分证明为 0（只有当字符串不匹配时，`strcmp()` 会返回一个正整数/负整数，然后通过 NOT 运算符转换为“零”），则 AND 的第二部分将不会执行。在这里，控制转移到 `else if`。

→ 类似于 AND 操作中后半部分的评估取决于前半部分的结果，在 OR 操作中，如果前半部分为 TRUE，则后半部分将完全不会执行。因此，如果用户名或密码部分任一处匹配，表达式都将求值为 TRUE。这在我们的登录案例中不应该发生，因为两个条件都必须为 TRUE。因此，在 `else` 部分内部进行第二级检查。

→ 如果值与存储的值不相同，则执行 `else` 部分！！

请参考输出 4.2 的说明。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_67_0.png)

输出 4.2

## 4.2.4. 位运算符

众所周知，计算机将一切都视为 0 和 1。它们被称为位（Binary digits 的缩写）。“C”作为一种高级程序语言，上述事实并无例外。它有处理位的运算符。此类类别中共有 6 种运算符。

- 位与运算符 (&)
- 位或运算符 (|)
- 位异异运算符 (^)
- 左移 (<<)
- 右移 (>>)
- 取反 (~)

# 运算符 57

在程序中使用这些运算符之前，让我们先对它们进行简要介绍。

## 位与运算符 (&)

考虑以下示例。
设 a=10; b=4。
a 的二进制等价形式是 1010，b 的二进制等价形式是 0100。
我们使用与逻辑 AND 相同的真值表进行位与运算，
（1&1 单独为 1，其余组合为 0），如下：

```
1010
&
0100
0000
```

如上述操作所示，该操作的结果为 0。
更多示例：

- 1. 10 & 25 = 8（因为 01010&11001 是 01000，它是 8 的二进制值！）。
- 2. 36 & 85 = 4（因为 110100&1010101 是 000100，它等于 4！）

## 位或运算符 (|)

在这里，OR 操作是按位执行的。真值与逻辑 OR 相似。
示例：

- 1. 设 a=10; b=4。位运算执行如下。
- 2. 6 | 3 = 7（因为 0110 | 0011 是 0111，它是 7！）。
- 3. 13 | 31 = 31（因为 01101 | 11111 是 11111，它是 31！）

```
1010
|
0110
1110 = 14
```

## 位异异运算符 (^)

XOR 操作的真值表执行如下，

| a | b | a^b |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

表 4.4 XOR 真值表

根据真值表的各项，对操作数逐位执行异异运算。

## 示例

- 1. 假设 a=10, b=6。执行位异异将产生输出 12，如下。

```
1010
^
01110
1100
```

- 2. a=36, b=12, a^b=40（因为 010100^001100 = 0101000，它是 40 的二进制等价形式）。

## 左移 (<<)

此特定运算符将操作数的位向左移动指定的位数。例如，10<<1 将操作数 '10' 向左移动 1 位。从图上来说，该操作可以解释如下。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_69_0.png)

图 4.1 左移

为了方便读者记忆，有一个关于位移运算符如何运作的提示。如果操作数需要移动 'n' 位，答案将等于操作数乘以 (2*n) 时的值。例如，(10<<1) 等于 (10*2^1)，即等于 20。当 n 为 0 时，此规则不适用。操作数将不会移动。答案将是数字本身。

## 示例

- 1. 15<<2 = 6
- 2. 11<<3 = 80
- 3. -10<<1=-20
- 4. 10<<0 = 10

## 右移 (>>)

此运算符与其对应的左移运算符相反。位向右移动指定的位数。例如，10>>1 将操作数 '10' 向右移动 1 位。

与执行左移时提到的提示类似，有一种寻找右移值的方法，即将将操作数除以 (2*n)，其中 'n' 是要移动的位数。例如，(10>>1) 等于 (10/(2^1))，即 5。

## 示例

- 1. 15>>2 = 3（如果操作数是奇数，结果将是向下取整）。
- 2. 11>>3 = 1
- 3. -10>>1=-5
- 4. 10>>0 = 0
- 5. 256>>1=128

## 取反 (~)

本节中的最后一个运算符简单的将位从 0 翻转为 1 反之亦然。例如，12 的取反值计算如下，
12 的二进制等价形式是：0000 0000 0000 1100（位处理器），所有的 0 都翻转为 1。

## 示例

- 1. ~(15) = fff
- 2. ~(33) = fde（因为 ~(0000 0000 0000 0001) 是 (1111 1111 1111 1110) 即 fde）。
- 3. ~(66) = fbfd

程序 4.3 解释了上述概念。

```c
#include<stdio.h>
void main()
{
    int a,b,c,d,e,bits;
    int choice;
    printf("choose the operation to be performed!\n1.Bitwise AND\n2.Bitwise OR\n3.Bitwise XOR\n4.Shift Left\n5.Shift Right\n6.One's Complement\n7.Exit");
    scanf("%d", &choice);
    do{
        switch (choice) {
            case 1:
                printf("Enter first number: ");
                scanf("%d", &a);
                printf("Enter second number: ");
                scanf("%d", &b);
                c = a & b;
                printf("Result: %d\n", c);
                break;
            case 2:
                printf("Enter first number: ");
                scanf("%d", &a);
                printf("Enter second number: ");
                scanf("%d", &b);
                c = a | b;
                printf("Result: %d\n", c);
                break;
            case 3:
                printf("Enter first number: ");
                scanf("%d", &a);
                printf("Enter second number: ");
                scanf("%d", &b);
                c = a ^ b;
                printf("Result: %d\n", c);
                break;
            case 4:
                printf("Enter first number: ");
                scanf("%d", &a);
                printf("Enter shift count: ");
                scanf("%d", &bits);
                c = a << bits;
                printf("Result: %d\n", c);
                break;
            case 5:
                printf("Enter first number: ");
                scanf("%d", &a);
                printf("Enter shift count: ");
                scanf("%d", &bits);
                c = a >> bits;
                printf("Result: %d\n", c);
                break;
            case 6:
                printf("Enter number: ");
                scanf("%d", &a);
                c = ~a;
                printf("Result: %d\n", c);
                break;
            case 7:
                exit(0);
        }
        printf("Choose again: ");
        scanf("%d", &choice);
    } while(choice!=7);
}
```
