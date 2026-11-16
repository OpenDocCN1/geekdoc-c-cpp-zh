

- 位运算符简介
- 位与掩码
- WordStar
- 位或
- 位异或
- 位取反
- 左移运算符
- 右移运算符
- 旋转示例
- 提取位字段
- 位运算符作业
- 位运算符实验

## 位运算符简介

C 提供了一系列专门用于对单个位进行操作的运算符：

```
a = 0x34 = 0011 0100
b = 0x0A = 0000 1010
```

除了位取反运算符外，所有位运算符都是二元运算符，因此需要两个操作数。C 中可以对任何类型的整数值执行位操作，例如：

| int | 无符号 int |
| --- | --- |
| short | 无符号 short |
| long | 无符号 long |
| char | 无符号 char |

但不能对：

| 浮点数 |
| --- |
| 双精度浮点数 |
| 长双精度浮点数 |

位运算符会并行地应用于每个操作数中的各个位位置。这与逻辑运算符不同，逻辑运算符将每个操作数视为单个零（假）或非零（真）值。

## 位与

与逻辑 AND 运算符（&&）类似，位与运算符（&）仅在两个操作数都为真（即具有非零值）时才产生真值。

| b1 | b2 | b1 & b2 |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

我们假设一个 16 位整数：

```c
// and1.c

#include <stdio.h>

int main(void) {
   int x = 0x2719; // 0010 0111 0001 1001
   int y = 0x35CD; // 0011 0101 1100 1101
   int z;

   z = x & y; // 0010 0101 0000 1001
   printf("z = %#x\n", z); // z = 0x2509
   return 0;
}
```

该程序的输出为：

```
z = 0x2509
```

请注意，每个 int 变量中的对应位都会进行按位与运算。

下面是另一个示例：

```c
// and2.c

#include <stdio.h>

int main(void) {
    int x = 0x1234;    // 0001 0010 0011 0100
    int y = 0x3468;    // 0011 0100 0110 1000
    int z = 0x5248;    // 0101 0010 0100 1000

    printf("0%x\n\n", x & x);   => 0x1234
    printf("0%x\n\n", x & y);   => 0x1020
    printf("0%x\n\n", x & y & z); => 0x1000
    printf("0%x\n\n", x & y & z); => 0x0000

    return 0;
}
```

在第一个 printf() 语句中，任何数值与自身进行按位与运算都会返回其自身作为值：

```
x = 0x1234 = 0001 0010 0011 0100
x = 0x1234 = 0001 0010 0011 0100

0001 0010 0011 0100 = 0x1234
```

在第二个 printf() 语句中，变量 x 和 y 进行按位与运算，产生：

```
x = 0x1234 = 0001 0010 0011 0100
y = 0x3468 = 0011 0100 0110 1000

0001 0000 0010 0000 = 0x1020
```

在第三个 printf() 语句中，所有三个变量 x、y 和 z 进行按位与运算，产生：

```
x = 0x1234 = 0001 0010 0011 0100
y = 0x3468 = 0011 0100 0110 1000
z = 0x5248 = 0101 0010 0100 1000

0001 0000 0000 0000 = 0x1000
```

第四个 printf() 语句的作用是提取 x 的最右位，即 0 或 1。

```
x = 0x1234 = 0001 0010 0011 0100
0x0001 = 0000 0000 0000 0001
              0000 0000 0000 0000 = 0x0
```

请注意，这是一个判断 x 是奇数还是偶数的好方法：

```
printf("%s", x & 1 ? "Odd" : "Even");
```

请记住位与运算符（&）和逻辑与运算符（&&）之间的区别：

```c
// and3.c
#include <stdio.h>

void main(void) {
    int x = 1;
    int y = 2;
    printf("bitwise = %d \nlogical = %d\n", x & y, x && y);
    return 0;
}
```

输出如下：

```
bitwise = 0   logical = 1
```

## 掩码

按位与运算常用于掩码操作。掩码是一个常量或变量，用于提取变量或表达式中所需的位。掩码可用于将数据项中的特定位设置为 0。在下面的示例中，我们将保留 x 的最右两位，并将所有其他位置零（掩码）：

```c
// mask1.c
#include <stdio.h>

int main(void) {
    int x = 0x679;    // 0000 0110 0111 1001
    int mask = 0x0003; // 0000 0000 0000 0011

    x = x & mask;      // 0000 0000 0000 0001
    printf("x = %#x\n", x);
    return 0;
}
```

输出如下：

```
x = 0x1
```

请注意，也可以写成：

```
x &= mask;
```

现在假设我们要将一个字中除了最右四位之外的所有位都设置为 0：

```c
// mask2.c

#include <stdio.h>

int main(void) {
    int x = 0x1234; // 0001 0010 0011 0100
    int mask = 0x000F; // 0000 0000 0000 1111

    x &= mask; // 0000 0000 0000 0100
    printf("x = 0x%x\n", x);

    return 0;
}
```

输出如下：

```
x = 0x4
```

我们还可以使用掩码来确定 int 表达式的低阶位：

```c
// mask3.c

#include <stdio.h>

int main(void) {
    int i;
    int mask = 0x0001; // 0000 0000 0000 0001

    for (i = 0; i < 10; i++) {
        printf("%d ", i & mask);
    }

    return 0;
}
```

上述程序打印出交替的 0 和 1 序列：

```
0 1 0 1 0 1 0 1 0 1
0 1 2 3 4 5 6 7 8 9
```

如果我们想查找表达式中特定位的值，可以使用在该位置为 1、其他位置为 0 的掩码。例如，我们可以检查 int 从右数第 5 位：

```c
// mask4.c

#include <stdio.h>

int main(void) {
    int x = 0x1234;    // 0001 0010 0011 0100
    int mask = 0x0010; // 0000 0000 0001 0000

    if (x & mask) {
        printf("Bit is a 1.\n");
    } else {
        printf("Bit is a 0.\n");
    }

    return 0;
}
```

输出如下：

```
Bit is a 1.
```

## WordStar

WordStar 是一款文字处理器应用程序，在 20 世纪 80 年代初至中期占据主导市场份额。它使用 ASCII 字符的高阶位用于特殊格式目的。

WordStar 会在单词的最后一个字符上设置高阶位，以标记可以插入空格以对齐右边距的位置。它还会在插入的空格上设置高阶位，以便在对齐文本时知道可以删除哪些空格。例如，它不希望删除你在句末放置的双空格。

如果你使用简单的文本编辑器输出 WordStar 创建的文件中的字符，可能看起来像这样：

```
6E† Writā · functiō calleō find_strinā tō determinā īē onāt characterō ō strināt existōt insidā anotheōt stringōt Thā firōō argumenōt tōt thā ō functiō shoulō bā thā characterō stringō thaō 10 tō bā searcheō auk thā ō secondō argumenōt thā strinā wā āra interestekt 10t findingō īāt thā ō functiō findō thā specificō stringō y tōēō havā 10 returō tōa locatiō ō 10 thā sourcō strinā whēn thā strinā wāō foundōt 12 thā functiō dēō ō Not find the string, then have it return -1. (25)
```

事实上，这是我 1986 年使用 WordStar 编写的一份考试中的问题。我最近找到了这个文件，想查看其内容。所有这些乱码的原因是 WordStar 在许多字符上设置了高阶位。请记住，ASCII 实际上是一种 7 位代码，从未使用高阶位来定义字符。WordStar 将此高阶位用于自己的目的！

因此，我创建了一个程序，一次读取一个字符。该程序在输出字符之前创建一个掩码来关闭高阶位：

```
putchar(c & 0x7f);
```

该语句将字符与掩码 01111111 进行按位与运算，从而有效地关闭高阶位。

下面是代码：

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int c;
    char fileName[32];
    FILE *fp;

    printf("Enter filename: ");
    gets(fileName);

    if ((fp = fopen(fileName, "r"))) {
        printf("File could not be opened.\n");
        exit(1);
    }

    while((c = getc(fp)) != EOF) {
        putchar(c & 0x7f);
    }
    fclose(fp);
    return 0;
}
```

下面是输出：

6. 编写一个名为 find_string 的函数，用于确定一个字符串是否存在于另一个字符串中。函数的第一个参数应为要搜索的字符串，第二个参数为我们感兴趣的要查找的字符串。如果函数找到指定字符串，则让它返回字符串在源字符串中找到的位置。如果函数未找到字符串，则让它返回 -1。（25）

这道考试题不错！

