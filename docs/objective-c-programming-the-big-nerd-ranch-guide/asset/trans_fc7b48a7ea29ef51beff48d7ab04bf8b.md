
## 补集

这是通过 `^` 运算符完成的。在 `main.c` 中添加：

```c
    unsigned char e = a ^ b;
    printf("Hex: %x ^ %x = %x\n", a, b, e);
    printf("Decimal: %d ^ %d = %d\n", a, b, e);
    return 0;
}
```

运行时你将看到：

十六进制：3c ^ a9 = 95
十进制：60 ^ 169 = 149

该运算符有时会让初学者感到困惑。在大多数电子表格程序中，`^` 运算符表示指数运算：2^3 意味着 2³。在 C 语言中，我们使用 **pow()** 函数进行指数运算：

```c
double r = pow(2.0, 3.0); // 计算 2 的三次方
```

## 补码

如果你有一个字节，其补码就是那个完全相反的字节的：每个 0 变成 1，每个 1 变成 0。

![](img/5f9368899ebf8d92fc145f8def1e89f8_253_0.png)

这是通过 `~` 运算符完成的。在 main.c 中添加几行代码：

```c
    unsigned char f = ~b;
    printf("Hex: The complement of %x is %x\n", b, f);
    printf("Decimal: The complement of %d is %d\n", b, f);
    return 0;
}
```

你应该看到：

十六进制：a9 的补码是 56
十进制：169 的补码是 86

## 左移

如果你将位向左移动，你会将每一位向最高有效位移动。位于数字左侧的位会被丢弃，而右侧产生的空位则填充零。

### 图 33.7 左移 2 位

![](img/5f9368899ebf8d92fc145f8def1e89f8_254_0.png)

左移是通过 `<<` 运算符完成的。在 `main.c` 中添加左移两位的操作：

```c
unsigned char g = a << 2;
printf("Hex: %x shifted left two places is %x\n", a, g);
printf("Decimal: %d shifted left two places is %d\n", a, g);
    return 0;
}
```

当这段代码运行时，你将看到：

```
Hex: 3c shifted left two places is f0
Decimal: 60 shifted left two places is 240
```

每次将一个数字左移一位，其值就会翻倍。

## 右移

右移运算符应该不会让你感到惊讶。在 `main.c` 中添加代码：

```c
unsigned char h = a >> 1;
printf("Hex: %x shifted right one place is %x\n", a, h);
printf("Decimal: %d shifted right one place is %d\n", a, h);
    return 0;
}
```

运行时：

```
Hex: 3c shifted right one places is 1e
Decimal: 60 shifted right two places is 30
```

### 图 33.8 右移 1 位

![](img/5f9368899ebf8d92fc145f8def1e89f8_254_1.png)

每次将一个数字右移一位，其值就会减半。（如果是奇数，则向下取整。）

## 使用 enum 定义位掩码

通常你会想要定义一个常量列表，每个常量都代表一个只有一位被置为 1 的整数。然后，这些整数可以通过按位或运算组合在一起，并通过按位与运算进行测试，如上文所述。

优雅的做法是定义一个使用左移运算符来定义值的枚举。以下是 **UIDataDetector** 常量定义的方式：

```objc
enum { 
    UIDataDetectorTypePhoneNumber   = 1 << 0,
    UIDataDetectorTypeLink          = 1 << 1,
    UIDataDetectorTypeAddress       = 1 << 2,
    UIDataDetectorTypeCalendarEvent = 1 << 3,
    UIDataDetectorTypeNone          = 0,
    UIDataDetectorTypeAll           = NSUIntegerMax 
};
```

## 更多字节

在本章中，我们使用了无符号字符（unsigned char），它是一个 8 位字节。任何无符号整数类型的工作方式都相同。例如，NSTextCheckingTypePhoneNumber 实际上被声明为 uint64_t，即一个 64 位无符号数。

## 挑战

编写一个程序，创建一个 64 位无符号整数，使其每隔一位被置为 1。（实际上有两个可能的结果数字：一个是偶数，另一个是奇数。请创建奇数那个。）显示该数字。

*此页有意留白*

# 34 C 字符串

如果有选择，Objective-C 程序员总是倾向于使用 **NSString** 对象而不是 C 字符串。然而，有时我们没有选择。我们最终使用 C 字符串的最常见原因是什么？当我们从 Objective-C 代码中访问 C 库时。例如，有一个 C 函数库可以让你的程序与 PostgreSQL 数据库服务器通信。该库中的函数使用的是 C 字符串，而不是 **NSString** 实例。

## char

在上一节中，我们谈到了字节如何被当作数字处理。我们也可以将字节当作字符处理。如前所述，有许多不同的字符串编码。最古老且最著名的是 ASCII。ASCII（美国信息交换标准代码）为每个字节定义了不同的字符。例如，0x4b 是字符 ‘K’。

创建一个新的 C 命令行工具并命名为 yostirng。在这个程序中，你将列出 ASCII 标准中的一些字符。编辑 *main.c*：

```c
#include <stdio.h>

int main (int argc, const char * argv[])
{
    char x = 0x21; // 字符 '!'

    while (x <= 0x7e) { // 字符 '~'
        printf("%x is %c\n", x, x);
        x++;
    }

    return 0;
}
```

你可能会好奇：“嘿，一个字节可以容纳 256 个数字中的任意一个。你刚才只打印出了 94 个字符。剩下的去哪了？”重要的是要意识到，ASCII 是为了驱动老式的电传风格终端而编写的，这些终端将内容打印在纸上，而不是屏幕上。例如，ASCII 中的数字 7 会使终端铃响。事实上，ASCII 中的字符 0 – 31 是不可打印的控制码。数字 32 是空格字符。数字 127 是删除键 – 它会导致上一个字符消失。那么字符 128 – 255 呢？ASCII 只使用 7 位。数字 128 没有对应的 ASCII 字符。

你可以在代码中使用 ASCII 字符作为字面量。只需将它们放在单引号内。修改你的代码以使用这些：

```c
int main (int argc, const char * argv[])
```

构建并运行它。

不可打印的字符可以使用以 `\` 开头的转义序列来表示。你已经使用过 `\n` 来表示换行符。以下是一些常见的：

表 34.1 常见转义序列

| 转义序列 | 描述 |
| :--- | :--- |
| `\n` | 换行 |
| `\t` | 制表符 |
| `\'` | 单引号 |
| `\"` | 双引号 |
| `\0` | 空字节 (0x00) |
| `\\` | 反斜杠 |

## char \*

C 字符串只是一组在内存中紧挨着排列的字符。当遇到字符 0x00 时，字符串结束。

![](img/5f9368899ebf8d92fc145f8def1e89f8_258_0.png)

接收 C 字符串的函数期望获得字符串第一个字符的地址。例如，strlen() 将计算字符串中的字符数量。尝试构建一个字符串并使用 strlen() 来计数：

```c
#include <stdio.h> // 用于 printf
#include <stdlib.h> // 用于 malloc/free
#include <string.h> // 用于 strlen

int main( int argc, const char * argv[]) {
    char x = '!'; // 字符 '!'

    while (x <= '~') { // 字符 '~'
       printf("%x is %c\n", x, x);
       x++;
    }

    // 获取堆上 5 字节内存的指针
    char *start = malloc(5);

    // 在第一个字节放入 'L'
    *start = 'L';

    // 在第二个字节放入 'o'
    *(start + 1) = 'o';

    // 在第三个字节放入 'v'
    *(start + 2) = 'v';

    // 在第四个字节放入 'e'
    *(start + 3) = 'e';

    // 在第五个字节放入零
    *(start + 4) = '\0';

    // 打印字符串及其长度
    printf("%s has %zu characters\n", start, strlen(start));

    // 打印第三个字母
    printf("The third letter is %c\n", *(start + 2));

    // 释放内存以便重用
    free(start);
    start = NULL;

    return 0;
}
```

构建并运行它。

注意你添加指针和数字的地方。`start` 被声明为 `char *`。一个 char 是一个字节。因此 `start + 1` 是指向内存中比 start 多一个字节的指针。`start + 2` 是指向内存中比 start 多两个字节的指针。

### 图 34.2 每个字符的地址

| start | start+1 | start+2 | start+3 | start+4 |
| :---: | :---: | :---: | :---: | :---: |
| L | o | v | e | \0 |

这种对指针相加并解引用结果的操作非常常见，因此有一个简写形式：`start[2]` 等价于 `* (start + 2)`。修改你的代码以使用它：

```c
char *start = malloc(5);
start[0] = 'L';
start[1] = 'o';
start[2] = 'v';
start[3] = 'e';
start[4] = '\0';

printf("%s has %zu characters\n", start, strlen(start));
printf("The third letter is %c\n", start[2]);

free(start);
start = NULL;

return 0;
}
```

构建并运行它。

应该提到的是，这适用于任何数据类型。例如，在这里，我可以制作一个我最喜欢的 3 个浮点数的列表并打印它们：

```c
int main ( int argc, const char * argv[ ])
{
    // 声明一块足以容纳三个 float 的内存
    float *favorites = malloc(3 * sizeof(float));

    // 将值推送到该缓冲区的位置中
    favorites[0] = 3.14158;
    favorites[1] = 2.71828;
    favorites[2] = 1.41421;

    // 打印列表中的每个数字
    for (int i = 0; i < 3; i++) {
        printf("%.4f is favorite %d\n", favorites[i], i);
    }

    // 释放内存以便重用
    free(favorites);
    favorites = NULL;

    return 0;
}
```

这里唯一有趣的区别是 `favorites` 的类型是 `float *`。一个 float 是 4 字节。因此 `favorites + 1` 是指向内存中比 `favorites` 多 4 字节的指针。

## 字符串字面量

如果你经常处理 C 字符串，使用 `malloc` 分配内存并逐个填充字符会非常麻烦。相反，你可以通过将字符串放在引号中来创建一个指向字符字符串（以零字符终止）的指针。修改你的代码以使用字符串字面量：
