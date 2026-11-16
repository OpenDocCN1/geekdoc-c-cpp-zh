
枚举类型的一个令人烦恼的方面是它们不被 C 输入输出语句识别。例如：

```
enum direction { north, south, east, west };
direction d1 = south;
printf("%d\n", south);
```

输出的值为 1。

如果希望将特定的整数值与枚举值关联，则可以在定义数据类型时将整数赋给该值。随后出现在列表中的枚举值将被指定从指定整数值加 1 开始的顺序值。

例如：

```
enum direction { up, down, left = 10, right };
```

| 枚举值 | 数值 |
|---|---|
| up | 0 |
| down | 1 |
| left | 10 |
| right | 11 |

定义枚举数据类型时可以省略数据类型的名称。定义数据类型时，也可以将变量声明为特定的枚举数据类型：

```
enum { east, west, south, north } location;
```

请注意，在函数内定义枚举数据类型会将该定义的使用范围限制在函数内定义的变量上。在程序开头（任何函数之外）定义枚举数据类型，会使类型定义对文件全局有效。

## typedef 语句

`typedef` 语句使程序员可以为数据类型指定一个替代名称。例如：

```
typedef int COUNTER;
```

这将名称 COUNTER 定义为与 C 数据类型 `int` 等效。现在可以将变量声明为 COUNTER 类型：

```
COUNTER a, b, c;
```

这提高了程序的可读性。下面是另一个示例：

```
typedef char *STRING_PTR;
```

这将名称 `STRING_PTR` 定义为 `char` 指针。现在可以定义 `STRING_PTR` 类型的变量：

```
STRING_PTR buffer;
```

C 编译器会将其视为字符指针。

另一个示例：

```
typedef char STRING[81];
```

这定义了一个名为 `STRING` 的类型，它是包含 81 个字符的数组。现在可以定义 `STRING` 类型的变量，如下所示：

```
STRING text;
```

这相当于定义变量 text 为包含 81 个字符的字符数组，并等价于：

```
char text[81];
```

## 定义新类型名称的步骤

- 1. 编写语句，仿佛正在定义所需类型的变量。
- 2. 在通常出现已定义变量名称的位置，替换为新的类型名称。
- 3. 在最前面放置关键字 typedef。

```
#define Bool unsigned char
typedef unsigned char Bool
Bool a;
```

## 枚举与 typedef 作业

1. a) 声明一个枚举标记，其值表示一周中的七天。

```
enum Day { Sun, Mon, Tue, Wed, Thus, Fri, Sat };
```

b) 使用 typedef 为枚举定义一个名称。

```
typedef enum Day THEWEEK
typedef enum {Sun, Mon, Tue, Wed, Thus, Fri, Sat} Day;
```

2. 关于枚举常量的以下哪些陈述是正确的？

a) 枚举常量可以表示程序员指定的任何整数。

b) 枚举常量与使用 #define 创建的常量具有完全相同的属性。错误

c) 枚举常量默认值为 0、1、2、...

d) 枚举中的所有常量必须具有不同的值。错误

e) 枚举常量可在表达式中用作整数。

3. 假设 b 和 i 声明如下：

```
enum { FALSE, TRUE } b;
int i;
```

以下哪些语句是合法的？哪些是“安全”的（始终产生有意义的结果）？

- a) b = FALSE; 合法/安全
- b) b = i;
- c) b++; 合法 / 安全（有效？）
- d) i = b; 合法 安全 -> 值为 1
- e) i = 2 * b + 1; 安全 -> 值 = 2*0+1 ... 1

所有语句都是合法的，因为 C 允许整数和枚举值无限制地混合。但是，只有 (a)(d)(e) 是安全的。

(b) 如果 b 的值不是 0 或 1，则无意义 (c) 如果 b ... 则不会产生有意义的结果

4. 假设 direction 变量声明如下：

```
enum { NORTH, SOUTH, EAST, WEST } direction;
```

设 x 和 y 为 int 变量。编写一个 switch 语句来测试 direction 的值，如果 direction 是 EAST 则递增 x，如果 direction 是 WEST 则递减 x，如果 direction 是 SOUTH 则递增 y，如果 direction 是 NORTH 则递减 y。

5. 以下各声明中枚举常量的整数值分别是多少？

- a) enum { NORTH, EAST, SOUTH, WEST };
  0   1   2   3
- b) enum { DIAMONDS = 5, HEARTS, CLUBS, SPADES };
  5   6   7   8
- c) enum { MON = 8, TUES, WED, THURS = 14, FRI };
  8   9   10  14  15
- d) enum { RED = 5, BLUE, GREEN, YELLOW = 12, BROWN };
  5   6   7   12  13

```
int main(void)
enum direction: int x,y
for (direction: NORTH; direction <= WEST; ++direction)
switch (direction) {
    case NORTH: y--; break;
    case SOUTH: y++; break;
    case EAST: x++; break;
    case WEST: x--; break;
}
return 0;
}
```

- 结构体简介
- 操作整个结构体
- 结构体示例：今天的日期和明天的日期
- 结构体数组
- 嵌套结构体
- 结构体作业
- 数据库实验

free() -> 释放清理

![](img/7f36c52b5170b89b142dbb7b1ea4666b_410_0.png)

```
typedef struct {
 char f_name[20];
 char l_name[10];
 int ph;
 PHONE_BOOK_ENTRY + NEXT,
} PHONE_BOOK_ENTRY;
```

- 步骤 1：使用 malloc() 为 phone_book_Entry 结构体预留空间
- 2：初始化记录。
- 3：如果是第一个电话簿记录，则转到第一条记录。
- 如果不是第一条记录，则添加到列表末尾
- 4：将 NULL 赋给最后一个元素的 (next)（next 字段）
- 称为“链表”

![](img/7f36c52b5170b89b142dbb7b1ea4666b_410_1.png)

## 结构体简介

我们之前曾使用数组以单个名称存储相同类型（且大小指定）的数据集合：

```
int num[10];
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_411_0.png)

我们学习了使用 num[1] 或 num[1] 等下标来引用数组的单个元素。

![](img/7f36c52b5170b89b142dbb7b1ea4666b_411_1.png)

通常，我们需要创建包含不同类型相关数据的集合。例如，如果我想收集学生信息，我可能对以下信息感兴趣：

- 学生姓名（字符串）
- 学生绩点（双精度浮点数）
- 学生预期毕业年份（整数）

我们可以在 C 中使用称为 struct 的数据类型来建模此类集合。struct 是用户定义数据类型的一个示例，即我们可以定义自己的 struct 来建模所需的任何数据。

例如：

```
typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;
```

这充当创建名为 Student 的新数据类型的蓝图或模板。这种新的用户定义数据类型 Student 可以像任何内置数据类型一样用于声明变量：

```
typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;

int main(void) {
   Student s1, s2, s3;
   ...
   return 0;
}
```

上面的声明创建了三个 Student 类型的变量：s1、s2 和 s3。这些变量中的每一个现在在内存中都有存储字符串、double 和 int 的空间。请注意，我们的新数据类型名称以大写字母开头。虽然这不是必须的，但遵循这一规则是个好习惯。

还要注意，struct 在 main() 之外的全局作用域中声明。这使得 struct 对程序的所有部分都可见。如果 struct 仅在 main() 内声明，那么它将局部于 main() 且仅在 main() 内可见。

结构体可以如下表示：

| | 姓名 | 绩点 | 年份 |
|---|---|---|---|
| s1 | Sammie | 3.85 | 2016 |

## 引用结构体元素。

我们现在在结构体上遇到了与数组相同的问题。我们如何引用结构体的单个元素（称为组件或字段）？对于数组，我们使用下标。对于结构体，我们使用句点，也称为直接组件选择运算符（或者更简单地说，简称选择运算符）。

例如，我们可以如下为结构体的每个字段赋值：

```
s1.gpa = 3.85;
s1.year = 2016;
strcpy(s1.name, "Sammy");
```

## 示例：日期结构体。

假设我们需要跟踪各种日期。我们可以如下定义 Date 数据类型：

```
typedef struct {
    int month;
    int day;
    int year;
} Date;
```

定义 Date 数据类型后，我们可以如下创建 Date 变量：

```
typedef struct {
    int month;
    int day;
    int year;
} Date;

int main(void) {
    Date yesterday, today, tomorrow, appointment, birthday;
    ...
    ...
    return 0;
}
```
