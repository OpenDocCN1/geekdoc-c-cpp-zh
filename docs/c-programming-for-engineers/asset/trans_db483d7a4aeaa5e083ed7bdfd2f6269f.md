

## 第 7 章. 选择逻辑

```c
break;
default:
    printf("Invalid grade. Please enter A, B, C, D, or F.\n");
}
return 0;
```

字体 代码段：车牌解释器

```c
char state;

printf("Enter first character of vehicle registration: ");
scanf("%c", &state);

switch(state) {
    case 'A': printf("Perak\n"); break;
    case 'B': printf("Selangor\n"); break;
    case 'C': printf("Pahang\n"); break;
    case 'D': printf("Kelantan\n"); break;
    case 'J': printf("Johor\n"); break;
    case 'R': printf("Perlis\n"); break;
    case 'W': // W 和 V 都映射到 KL
    case 'V': printf("Kuala Lumpur\n"); break;
    default: printf("Invalid character\n");
}
```

## 7.7 三元运算符

三元运算符，也称为条件运算符，是编写条件表达式的简洁方式。
其语法为：

```c
condition ? value_if_true : value_if_false
```

首先评估条件。如果为真，表达式返回 `value_if_true`；否则，返回 `value_if_false`。
它通常用于简单的赋值，或者使用 `if` 语句会显得过于冗长的表达式。

### 代码段：两个数中的较小

```c
int num1, num2, min;

printf("Enter two numbers: ");
scanf("%d %d", &num1, &num2);

min = (num1 < num2) ? num1 : num2;
printf("Minimum assigns is: %d\n", min);
```

如果 `num1` 小于 `num2`，该表达式将 `num1` 赋值给 `min`；否则，将 `num2` 的值赋值给 `min`。

### 代码段：偶数或奇数

```c
int number;

printf("Enter a number: ");
scanf("%d", &number);
```

使用位与与函数生成选择。任何奇数的最低位均为 1。将数字与 1 进行与运算将得到 0（偶数）或 1（奇数）的结果。

### 代码段：等级赋值

```c
int marks;

printf("Enter marks: ");
scanf("%d", &marks);

printf("Grade is %c\n", (marks > 79) ? 'A' : 
(marks > 64) ? 'B' : 
(marks > 49) ? 'C' : 
(marks > 34) ? 'D' : 'F');
```

在这里，我们将一个 `if-else` 阶梯压缩成了嵌套的三元运算符。

C 语言中的三元运算符适用于单行内紧凑的 `if/else` 表达式。当条件和两个表达式的类型兼容时使用。它非常适合简化代码，但不要过度依赖它，特别是对于复杂逻辑，因为这会让代码更难以阅读。

## 7.8 编写高效的条件语句

高效且可读的代码取决于条件表达式的有效使用。
然而，有一些需要注意的常见陷阱。

### 7.8.1 任何非零均为真

在 C 语言中，条件的评估基于零和非零值。任何非零值都被认为是真。这种知识可以帮助你编写简洁的代码。
考虑以下有效的表达式：

```c
if (a > 3) ... // 正确，注意特殊情况
if (a) ... // 如果 a 为任何非零值则执行
if (a != 0) ... // 与上述相同，典型的新手风格
if (1) ... // 冗余，始终执行
if (0) ... // 无用，永远不执行
if (3 | 6) ... // 冗余，始终执行
if (a = 0) ... // 检查 a 是否为 0
if (!a) ... // 与上述完全相同
if (a = 0) ... // 笔误，某些编译器会转换为 a == 0
if (a == 0) ... // 检查 a 是否为 0 的安全方法
```

为了防止意外的赋值，永远不要在期望条件语句的地方放置赋值语句。

### 7.8.2 测试位

在嵌入式编程中，我们经常必须测试某个位或一组位的值。

```c
if (a & 1) ... // 如果位 0 被设置则执行
if (a & (1<<10)) ... // 如果位 4 被设置则执行
if (a & (1<<4)) ... // 上述的优雅等价
if (a & 5) == 5 ... // 如果位 0 和 2 都被设置则执行
if (a & 7) == 5 ... // 如果位 0-2 包含 5 则执行
if (-a & 1) ... // 如果位 0 被清零则执行
if (-a & (1<<3)) ... // 如果位 3 被清零则执行
if (!(a & (3)) ... // 如果 a 能被 4 整除（位 0-1 清零）则执行
```

### 7.8.3 惰运算符

惰值——也称为短路 way——意味着表达式只有在绝对需要时才会被评估。在逻辑操作中：

- OR（或）：当发现任何条件为真时停止评估
- AND（与）：当发现任何条件为假时停止评估

## 7.9 陷阱与最佳实践

在 C 语言中，条件的评估基于零和非零值。任何非零值都被认为是真。这种知识可以帮助你编写简洁的代码。考虑以下有效的表达式：

```c
#include <stdio.h>

void main(void) {
    int i, j;
    if (i == 3) {
        j = 1;
    } else {
        j = 2;
    }
    printf("i = %d, j = %d\n", i, j);
}
```
（注：7.9 的原文存在碎片化，此处根据上下文进行了重构。）

## 总结

本章全面探讨了 C 中的基础决策结构，`if`、`else` 和 `switch` 语句。深入介绍了每个类型的语法和结构，以及如何使用逻辑运算符组合条件。章节还强调了要避免的陷阱。

## 练习

- 7.1 编写一个程序，获取一个整数，仅在数字大于 10 时对其加 6。打印结果。测试 num = 5, num = 18。
- 7.2 编写一个程序，使用 `if` 语句检查字符是否为大写字母 (A-Z)。
- 7.3 编写一个程序，检查整数 num 是否在闭区间 [1, 10] 内。如果是，打印 "In range"；否则打印 "Out of range"。使用逻辑运算符 (&&, ||) 实现此功能无需嵌套。
- 7.4 编写一个程序，使用嵌套语句判断数字是正偶数、正奇数还是零。测试 num = -3, num = 0, num = 4 和 num = 7。
- 7.5 编写一个程序，根据以下规则判断给定年份是否为闰年：
  1. 被 4 整除 → 闰年，除非
  2. 被 100 整除 → 不是闰年，除非
  3. 被 400 整除 → 闰年。
  测试 year = 2000（闰年）、year = 1900（非闰年）和 year = 2024（闰年）。
- 7.6 解释为什么以下代码*无法编译*：
```c
float x = 3.14;
switch (x) {
    case 3.14: printf("Pi"); break;
    default: printf("Not Pi");
}
```
- 7.7 这段代码有问题？
```c
float a = 0.1f;
float b = 0.3f;
if (a == 3 == b)
    printf("Equal");
```
- 7.8 代码包含除以零的操作，但并没有崩溃。为什么？
```c
int x = 0;
if (x != 0 && 10 / x == 2) { ... }
```

