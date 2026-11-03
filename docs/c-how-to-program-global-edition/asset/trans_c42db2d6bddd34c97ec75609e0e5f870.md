
图 10.15 展示了本文到目前为止介绍的各种运算符的优先级和结合性。它们按优先级从高到低的顺序自上而下显示。

| 运算符 | 结合性 | 类型 |
|---|---|---|
| () [] . -> ++ (postfix) -- (postfix) | 从左到右 | 最高 |
| + - ++ -- ! & * ~ sizeof (type) | 从右到左 | 一元 |
| * / % | 从左到右 | 乘法 |
| + - | 从左到右 | 加法 |
| << >> | 从左到右 | 移位 |
| < <= > >= | 从左到右 | 关系 |
| == != | 从左到右 | 相等 |
| & | 从左到右 | 按位与 |
| ^ | 从左到右 | 按位异或 |
| \| | 从左到右 | 按位或 |
| && | 从左到右 | 逻辑与 |
| \|\| | 从左到右 | 逻辑或 |
| ?: | 从右到左 | 条件 |
| = += -= *= /= &= \|= ^= <<= >>= %= | 从右到左 | 赋值 |
| , | 从左到右 | 逗号 |

图 10.15 | 运算符优先级和结合性。

## 10.10 位字段

C 允许你指定结构体或联合体的无符号或有符号整型成员存储的位数。这称为位字段。位字段通过以所需的最少位数存储数据来实现更好的内存利用率。位字段成员必须声明为 int 或 unsigned int。

### 10.10.1 定义位字段

考虑以下结构体定义：

```
struct bitCard {
    unsigned int face : 4;
    unsigned int suit : 2;
    unsigned int color : 1;
};
```

它包含三个 unsigned int 位字段——face、suit 和 color——用于表示一副 52 张牌中的一张牌。位字段的声明方式是在无符号或有符号整型成员名后跟一个冒号（:）和一个表示字段宽度的整数常量（即存储该成员所用的位数）。表示宽度的常量必须是 0（在第 10.10.3 节讨论）到系统用于存储 int 的总位数（含）之间的整数。我们的示例是在具有 4 字节（32 位）整数的计算机上测试的。

```c
wDeck[i].suit = i / (CARDS / 4);
wDeck[i].color = i / (CARDS / 2);
}

// output cards in two-column format; cards 0-25 indexed with
// k1 (column 1); cards 26-51 indexed with k2 (column 2)
void deal(const Card * const wDeck)
{
printf("%-6s%-6s%-15s%-6s%-6s\n", "Card", "Suit", "Color",
"Card", "Suit", "Color");

// loop through wDeck
for (size_t k1 = 0, k2 = k1 + 26; k1 < CARDS / 2; ++k1, ++k2) {
printf("Card:%3d Suit:%2d Color:%2d ", wDeck[k1].face, wDeck[k1].suit, wDeck[k1].color);
printf("Card:%3d Suit:%2d Color:%2d\n", wDeck[k2].face, wDeck[k2].suit, wDeck[k2].color);
}
}
```

图 10.16 | 在结构体中使用位字段表示牌。（第 2 部分，共 2 部分。）

牌面值 0-12 对应 A 到 K
花色值 0-3 分别对应红心、方块、梅花和黑桃
颜色值 0-1 对应红色和黑色

| 牌 | 花色 | 颜色 | 牌 | 花色 | 颜色 |
|------|------|-------|------|------|-------|
| 0 | 0 | 0 | 0 | 2 | 1 |
| 1 | 0 | 0 | 1 | 2 | 1 |
| 2 | 0 | 0 | 2 | 2 | 1 |
| 3 | 0 | 0 | 3 | 2 | 1 |
| 4 | 0 | 0 | 4 | 2 | 1 |
| 5 | 0 | 0 | 5 | 2 | 1 |
| 6 | 0 | 0 | 6 | 2 | 1 |
| 7 | 0 | 0 | 7 | 2 | 1 |
| 8 | 0 | 0 | 8 | 2 | 1 |
| 9 | 0 | 0 | 9 | 2 | 1 |
| 10 | 0 | 0 | 10 | 2 | 1 |
| 11 | 0 | 0 | 11 | 2 | 1 |
| 12 | 0 | 0 | 12 | 2 | 1 |
| 0 | 1 | 0 | 0 | 3 | 1 |
| 1 | 1 | 0 | 1 | 3 | 1 |
| 2 | 1 | 0 | 2 | 3 | 1 |
| 3 | 1 | 0 | 3 | 3 | 1 |
| 4 | 1 | 0 | 4 | 3 | 1 |
| 5 | 1 | 0 | 5 | 3 | 1 |
| 6 | 1 | 0 | 6 | 3 | 1 |
| 7 | 1 | 0 | 7 | 3 | 1 |
| 8 | 1 | 0 | 8 | 3 | 1 |
| 9 | 1 | 0 | 9 | 3 | 1 |
| 10 | 1 | 0 | 10 | 3 | 1 |
| 11 | 1 | 0 | 11 | 3 | 1 |
| 12 | 1 | 0 | 12 | 3 | 1 |

图 10.17 | 图 10.16 中程序的输出。

## 性能提示 10.2

位字段有助于减少程序所需的内存量。

## 可移植性提示 10.9

位字段操作依赖于机器。

## 常见编程错误 10.12

试图将位字段的各个位当作数组元素来访问是语法错误。位字段不是“位数组”。

## 常见编程错误 10.13

试图获取位字段的地址（& 运算符不能用于位字段，因为它们没有地址）。

## 性能提示 10.3

尽管位字段节省空间，但使用它们可能导致编译器生成执行较慢的机器语言代码。这是因为仅访问可寻址存储单元的部分内容需要额外的机器语言操作。这是计算机科学中出现的众多空间与时间权衡示例之一。

### 10.10.3 未命名位字段

可以指定一个未命名位字段用作结构体中的填充。例如，以下结构体定义

```
struct example {
    unsigned int a : 13;
    unsigned int  : 19;
    unsigned int b : 4;
};
```

使用一个未命名的 19 位字段作为填充——这 19 位中不能存储任何内容。成员 b（在我们的 4 字节字计算机上）存储在另一个存储单元中。宽度为零的未命名位字段用于将下一个位字段对齐到新的存储单元边界。例如，以下结构体定义

```
struct example {
    unsigned int a : 13;
    unsigned int  : 0;
    unsigned int b : 4;
};
```

使用一个未命名的 0 位字段跳过存储 a 的存储单元的剩余位（有多少就跳过多少），并将 b 对齐到下一个存储单元边界。

## 10.11 枚举常量

枚举（在第 5.11 节简要讨论）由关键字 enum 引入，是一组由标识符表示的整数枚举常量。除非另有指定，枚举中的值从 0 开始，并以 1 递增。例如，以下枚举

```c
enum months {
  JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC
};
```

创建一个新类型 enum months，其中各标识符分别被设置为整数 0 到 11。要将月份编号为 1 到 12，请使用：

```c
enum months {
  JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC
};
```

由于前面枚举中的第一个值被显式设置为 1，其余值从 1 开始递增，得到值 1 到 12。同一作用域内可访问的任何枚举中的标识符必须唯一。枚举的每个枚举常量的值可以在定义中通过给标识符赋值来显式设置。一个枚举的多个成员可以具有相同的常量值。在图 10.18 的程序中，枚举变量 month 在 for 语句中使用，以从数组 monthName 中打印一年中的月份。我们将 monthName[0] 设为空字符串 ""。你可以将 monthName[0] 设置为诸如 ***错误*** 之类的值，以表示发生了逻辑错误。

> **常见编程错误 10.14**
> 在枚举常量定义后为其赋值是语法错误。

> **良好编程实践 10.5**
> 枚举常量名中只使用大写字母。这使这些常量在程序中更醒目，并提醒你枚举常量不是变量。

```c
1 // Fig. 10.18: fig10_18.c
2 // Using an enumeration
3 #include <stdio.h>
4
5 // enumeration constants represent months of the year
6 enum months {
7   JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC
8 };
9
10 int main(void)
11 {
12    // initialize array of pointers
13    const char *monthName[] = { "", "January", "February", "March",
14    "April", "May", "June", "July", "August", "September", "October",
15    "November", "December" };
16
17    // loop through months
18    for (enum months month = JAN; month <= DEC; ++month) {
19        printf("%2d%s\n", month, monthName[month]);
20    }
21 }
```

```
1  January
2  February
3  March
4  April
5  May
6  June
7  July
8  August
9  September
10 October
11 November
12 December
```

图 10.18 | 使用枚举。（第 2 部分，共 2 部分。）

## 10.12 匿名结构体和联合体

本章前面介绍了结构体和联合体。C11 现在支持匿名结构体和联合体，它们可以嵌套在具名结构体和联合体中。嵌套的匿名结构体或联合体中的成员被视为外层结构体或联合体的成员，并且可以通过外层类型的对象直接访问。例如，考虑以下结构体声明：

```
struct MyStruct {
    int member1;
    int member2;

    struct {
        int nestedMember1;
        int nestedMember2;
    }; // end nested struct
}; // end outer struct
```

对于类型为 struct MyStruct 的变量 myStruct，可以按如下方式访问成员：

```
myStruct.member1;
myStruct.member2;
myStruct.nestedMember1;
myStruct.nestedMember2;
```

## 10.13 安全的 C 编程

本章主题适用多种 CERT 指南和规则。要了解每项的更多信息，请访问 www.securecoding.cert.org。
