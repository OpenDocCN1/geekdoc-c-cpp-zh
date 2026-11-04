
```
if((val & t) == 0) Console.Write("0 ");
}
}
```

输出如下所示：

```
0 1 1 1 1 0 1 1
```

for 循环依次使用按位与测试 val 中的每一位，以确定其是开启还是关闭。如果位为开启，则显示数字 1；否则显示 0。

按位或可用于打开位。任一操作数中被设置为 1 的任何位都会导致变量中对应的位被设置为 1。例如

```
1101 0011
| 1010 1010
------------
1111 1011
```

你可以利用或将前面显示的 make-even 程序改为 make-odd 程序，如下所示：

```csharp
// Use bitwise OR to make a number odd.
using System;
class MakeOdd {
    static void Main() {
        ushort num;
        ushort i;
        for(i = 1; i <= 10; i++) {
            num = i;
            Console.WriteLine("num: " + num);
            num = (ushort) (num | 1);
            Console.WriteLine("num after turning on bit zero: "
                + num + "\n");
        }
    }
}
```

该程序的输出如下所示：

```
num: 1
num after turning on bit zero: 1

num: 2
num after turning on bit zero: 3

num: 3
num after turning on bit zero: 3

num: 4
num after turning on bit zero: 5

num: 5
num after turning on bit zero: 5

num: 6
num after turning on bit zero: 7

num: 7
num after turning on bit zero: 7

num: 8
num after turning on bit zero: 9

num: 9
num after turning on bit zero: 9

num: 10
num after turning on bit zero: 11
```

该程序通过将每个数字与值 1 进行或运算，因为 1 是在二进制中仅设置零位的值。当此值与任何其他值进行或运算时，会产生低位被设置而所有其他位保持不变的结果。因此，偶数值将增加 1，变为奇数。

异或，通常缩写为 XOR，仅当比较的位不同时才会设置位开启，如下所示：

```
    0 1 1 1 1 1 1 1
  ^ 1 0 1 1 1 0 0 1
    ----------------
    1 1 0 0 0 1 1 0
```

XOR 运算符具有一种有趣的属性，在各种情况下都很有用。当某个值 X 与另一个值 Y 进行异或，然后将该结果再次与 Y 进行异或时，会得到 X。也就是说，给定序列

```
R1 = X ^ Y;
R2 = R1 ^ Y;
```

R2 与 X 的值相同。因此，使用相同值进行两次异或的序列的结果会产生原始值。XOR 的这一特性可以用来创建一个简单的密码，其中某个整数作为密钥，通过对消息中的字符进行异或来同时编码和解码消息。编码时，第一次应用 XOR 操作，得到密文。解码时，第二次应用 XOR，得到明文。当然，这种密码没有实际价值，因为它很容易被破解。然而，它提供了一种有趣的方式来演示 XOR 的效果，如以下程序所示：

```csharp
// Demonstrate the XOR.

using System;

class Encode {
    static void Main() {
        char ch1 = 'H';
        char ch2 = 'i';
        char ch3 = '!';
        int key = 88;

        Console.WriteLine("Original message: " + ch1 + ch2 + ch3);

        // Encode the message.
        ch1 = (char) (ch1 ^ key);
        ch2 = (char) (ch2 ^ key);
        ch3 = (char) (ch3 ^ key);

        Console.WriteLine("Encoded message: " + ch1 + ch2 + ch3);

        // Decode the message.
        ch1 = (char) (ch1 ^ key);
        ch2 = (char) (ch2 ^ key);
        ch3 = (char) (ch3 ^ key);

        Console.WriteLine("Encoded message: " + ch1 + ch2 + ch3);
    }
}
```

输出如下：

```
Original message: Hi!
Encoded message: 9)y
Encoded message: Hi!
```

如你所见，使用相同密钥进行两次 XOR 的结果会产生解码后的消息。（请记住，这种简单的 XOR 密码不适用于任何现实世界的实际用途，因为它本质上是不安全的。）

一元按位取反（NOT）运算符会反转操作数所有位的状态。例如，如果某个整数 A 的位模式为 1001 0110，则 ~A 会产生位模式为 0110 1001 的结果。

以下程序通过以二进制形式显示一个数字及其补码来演示 NOT 运算符：

```csharp
// Demonstrate the bitwise NOT.

using System;

class NotDemo {
    static void Main() {
        sbyte b = -34;

        for(int t=128; t > 0; t = t/2) {
            if((b & t) != 0) Console.Write("1 ");
            if((b & t) == 0) Console.Write("0 ");
        }
        Console.WriteLine();
    }
}
```

```csharp
for(int i = 0; i < 8; i++) {
    for(int t=128; t > 0; t = t/2) {
        if((val & t) != 0) Console.Write("1 ");
        if((val & t) == 0) Console.Write("0 ");
    }
    Console.WriteLine();
    val = val << 1; // left shift
}
Console.WriteLine();

val = 128;
for(int i = 0; i < 8; i++) {
    for(int t=128; t > 0; t = t/2) {
        if((val & t) != 0) Console.Write("1 ");
        if((val & t) == 0) Console.Write("0 ");
    }
    Console.WriteLine();
    val = val >> 1; // right shift
}
}
```

程序的输出如下所示：

```
0 0 0 0 0 0 0 1
0 0 0 0 0 0 1 0
0 0 0 0 0 1 0 0
0 0 0 0 1 0 0 0
0 0 0 1 0 0 0 0
0 0 1 0 0 0 0 0
0 1 0 0 0 0 0 0
1 0 0 0 0 0 0 0

1 0 0 0 0 0 0 0
0 1 0 0 0 0 0 0
0 0 1 0 0 0 0 0
0 0 0 1 0 0 0 0
0 0 0 0 1 0 0 0
0 0 0 0 0 1 0 0
0 0 0 0 0 0 1 0
0 0 0 0 0 0 0 1
```

由于二进制基于 2 的幂，移位运算符可用于将整数乘以或除以 2。左移使值加倍。右移使其减半。当然，这仅在你不将位移出任一端时才有效。以下是示例：

```csharp
// Use the shift operators to multiply and divide by 2.

using System;

class MultDiv {
    static void Main() {
        int n;
        n = 10;

        Console.WriteLine("Value of n: " + n);

        // Multiply by 2.
        n = n << 1;
        Console.WriteLine("Value of n after n = n * 2: " + n);

        // Multiply by 4.
        n = n << 2;
        Console.WriteLine("Value of n after n = n * 4: " + n);

        // Divide by 2.
        n = n >> 1;
        Console.WriteLine("Value of n after n = n / 2: " + n);

        // Divide by 4.
        n = n >> 2;
        Console.WriteLine("Value of n after n = n / 4: " + n);

        // Reset n.
        n = 10;
        Console.WriteLine("Value of n: " + n);

        // Multiply by 2, 30 times.
        n = n << 30; // data is lost
        Console.WriteLine("Value of n after left-shifting 30 places: " + n);
    }
}
```

输出如下所示：

```
Value of n: 10
Value of n after n = n * 2: 20
Value of n after n = n * 4: 80
Value of n after n = n / 2: 40
Value of n after n = n / 4: 10

Value of n: 10
Value of n after left-shifting 30 places: -2147483648
```

请注意输出中的最后一行。当值 10 左移 30 次时，信息会丢失，因为位被移出了 int 的范围。在这种情况下，产生的垃圾值是负数，因为 1 位被移入用作符号位的高位，导致数字被解释为负数。这说明了在使用移位运算符将值乘以或除以 2 时必须小心的原因。（参见第 3 章，了解有符号与无符号数据类型的解释。）

## 位运算符复合赋值

所有二进制位运算符都可用于复合赋值。例如，以下两个语句都将 x 与值 127 进行 XOR 的结果赋给 x：

```
x = x ^ 127;
x ^= 127;
```

## ? 运算符

C# 最迷人的运算符之一是 ?，它是 C# 的条件运算符。? 运算符通常用于替换某些类型的 if-then-else 构造。? 被称为三元运算符，因为它需要三个操作数。其一般形式为

```
Exp1 ? Exp2 : Exp3;
```

其中 Exp1 是一个 bool 表达式，Exp2 和 Exp3 是表达式。Exp2 和 Exp3 的类型必须相同。请注意冒号的使用和位置。

? 表达式的值确定如下：首先计算 Exp1。如果为真，则计算 Exp2 并成为整个 ? 表达式的值。如果 Exp1 为假，则计算 Exp3，其值成为表达式的值。考虑以下示例，它将 absval 赋值为 val 的绝对值：

```
absval = val < 0 ? -val : val; // get absolute value of val
```

这里，如果 val 为零或更大，则 absval 将被赋值为 val 的值。如果 val 为负，则 absval 将被赋值为该值的负值（从而得到正值）。

以下是 ? 运算符的另一个示例。此程序将两个数字相除，但不允许除以零。

```csharp
// Prevent a division by zero using the ?.

using System;

class NoZeroDiv {
    static void Main() {
        int result;
        for(int i = -5; i < 6; i++) {
            result = i != 0 ? 100 / i : 0;
            if(i != 0)
                Console.WriteLine("100 / " + i + " is " + result);
        }
    }
}
```

程序的输出如下所示：

```
100 / -5 is -20
100 / -4 is -25
100 / -3 is -33
100 / -2 is -50
100 / -1 is -100
100 / 1 is 100
100 / 2 is 50
100 / 3 is 33
100 / 4 is 25
100 / 5 is 20
```
