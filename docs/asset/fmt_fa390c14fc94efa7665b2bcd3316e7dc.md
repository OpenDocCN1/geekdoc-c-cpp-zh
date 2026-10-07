
## Q104. 当你想在流上写入指定大小的项目并返回写入的项目数时，应该使用哪个函数？

+ a. `language[20] = 'programming';`
+ b. `char language[20] = 'programming';`
+ c. `char language[20] = "programming";`
+ d. `char language[] = 'programming';`
+ a. `fprintf()`
+ b. `fwrite()`
+ c. `fprintf()`
+ d. `fopen()`

## Q97. 哪个函数用于拼接两个字符串，其中一个指定数量的字符附加另一个的末尾？

## Q105. 哪一个符合语法：

```
strncmp(str1,data1_data2,n);
strcat(str1,data1_data2);
strncat(str1,data1_data2);
strncat(str1,data1_data2,n);
```

考虑以下语句：

上述语法中的元素代表什么？

```
fseek(FILE, ll, int);
```

上述语句将文件指针移动到文件中的哪个字节？

+ a. 你想要打印的元素的数据类型
+ b. 文件的数据类型
+ c. 你想要显示的元素
+ d. 输出输出的格式
+ a. 第10个
+ b. 第11个
+ c. 第12个

## Q106. `fseek()` 函数的第二个参数指定什么？

+ a. 要移动的字节数
+ b. 文件指针名称
+ c. 移动的起始位置
+ d. 文件中的特定位置
+ b. C++
+ c. 作为数据结构的 C
+ d. Java

## Q107. 下列哪个函数在 C 中不执行任何输入或输出操作？

a. `read()`
b. `fseek()`
c. `write()`
d. `ftell()`

## Q117. 下面哪项是无效的标识符？

a. `int`
b. `_rollo`
c. `class 1`
d. `james_bond`

## Q108. 关于 C 语言，以下哪些是正确的？

a. C 是低级语言。
c. C 是中级语言。
c. C 是高级语言。
d. 以上都是

## Q118. C 程序的执行从哪个函数开始。

a. `main()`
b. `printf()`
c. 用户定义
d. `scanf()`

## Q109. 下面哪项不是 C 语言的标准？

a. ANSI C
b. OS C
c. ISO C
d. K&R C

## Q119. 下面哪种 C 标准是由 ISO 引入的？

a. ISO C
b. ANSI C
c. C59
d. K&R

## Q110. 标识符可以由组成

a. 保留字
b. 下划线
c. 字母
d. 数字

## Q111. 下面哪项是有效的标识符？

a. Salpry
b. salary
c. default
d. ary

## Q112. 下面哪项不是语言的关键字？

a. volatile
b. static
d. switch

## Q113. 下面哪项不是 C 的特性？

a. 面向对象
b. 可移植性
c. 允许指针
d. 允许运算符

## Q114. C 引入于何年

a. 1972
b. 1962
c. 1986
d. 1952

## Q115. 哪个函数用于从文件中读取数据？

a. `fopen()`
b. `getc()`
c. `putc()`
d. `fclose()`

## Q116. 在 C 语言引入之前使用了哪些语言？

a. BCPL

## Q121. 哪个运算符用于访问结构体的成员？

a. `->`
c. `*`
d. 以上都不是

## Q122. 当声明一个指向整数的 ptr 和整数变量 x 时，以下哪个不能用于赋值？

a. `ptr = x;`
b. `ptr = 1;`
c. `ptr = x;`
d. `ptr = &x;`

+ a. 150
+ b. 200
+ c. 100
+ d. 250

## Q123. `getchar()` 和 `putchar()` 函数属于哪个头文件。

a. `stdio.h`
b. `conio.h`
c. `string.h`
d. `ctypes.h`

## Q130. 预处理器语句使用预处理器指令来执行特定操作。

a. 编译器
b. 程序员
c. 程序
d. 执行器

## Q124. 下面哪项不是基础 C 程序的一部分？

a. 预处理器语句
b. 注释
c. 用户定义函数
d. 接口

## Q125. 下面哪个预处理器指令用于在 C 程序中包含文件？

a. `#include`
b. `#else`
c. `#endif`
d. `#ifdef`

## Q131. 哪个预处理器指令用于定义宏？

a. `#ifndef`
b. `#ifdef`
c. `#define`
d. `#include`

## Q126. 下面哪个代码语句正确定义了值为3.15的常量 'pi'？

a. `#define pi 3.15`
b. `#define pi=3.15`
c. `const float pi=3.15`

## Q132. `#ifdef` 指令验证下面哪个预处理器对立条件？

a. `#else`
b. `#if`
c. `#ifndef`
d. `#endif`

## Q127. 下面哪个是带参数的宏定义语法？

a. `#define identifier arg0, arg1, arg2`
b. `#define identifier(arg0, arg1, arg2)`
c. `#define identifier(arg0, arg1, arg5)`

## Q133. 哪个预处理器指令允许在 `#if` 测试失败时指定替代条件？

a. `#else`
b. `#else`
c. `#ifndef`
d. `#endif`

## Q128. 下面哪项是编译器指令？

a. `#define`
b. `#undef`
c. `#if`
d. `#include`

## Q134. 下面程序的输出是什么

```c
#include <stdio.h>
/* 使用 #define 指令 */
#define value 35
#define msg "HELLO"
int main() {
int r;
clrscr();
r = value; result = value-5;
printf("result = %d\n", result);
printf(msg);
getch();
return 0;
}
```

## Q129. 下面程序的输出是什么？

```c
#define v 100
main() {
#undef v
#if defined(v)
#define t 200
#else
#define v 150
#define t 250
#endif
clrscr();
printf("%d\n", v);
printf("%d\n", t);
getch();
}
```

+ a. result = value-5 result = 30 HELLO
+ b. result = value-5 result = 30 msg
+ c. result = 35-5 result = 30 HELLO
+ d. result == value-5 result == 35
d. 语句 `arr[3] = 8;` 将值8 赋值给数组元素

## Q135. 当输入流到达文件结束条件时，下面哪个函数返回 EOF？

+ a. `get()`
+ b. `scanf()`
+ c. `putchar()`
+ d. `getch()`

## Q143. 数组可以有多少个维度？

a. 一维
b. 二维
c. 三维
d. 任意维度

+ a. `get()`
+ b. `scanf()`
+ c. `putchar()`
+ d. `getch()`

## Q144. 下面哪项是二维数组的示例？

+ a. 有两个元素的数组
+ b. 有10个元素的数组
+ c. 一个矩阵
+ d. 两个变量

## Q136. 下面哪个指令验证宏是否定义？

+ a. `#define`
+ b. `#if`
+ c. `#ifdef`
d. `#undef`

## Q145. 当声明一个大小为15的整数指针时，下面哪个语句指向第四个元素？

a. `(*test[3])`
b. `test[4];`
c. `(*test[4])`
d. `test+3;`

## Q137. 下面哪个头文件（编译器）用于存储？

+ a. INCLUDE
b. LIB
d.CLASS

## Q138. 下面哪项是 C 程序需要包含的一维头？

+ a. `stdio.h`
b. `stdlib`
d. Arr

## Q139. 数组用于存储

+ a. 通过内存存储相同类型的值
+ b. 通过内存存储不同类型的值
+ c. 在内存中相邻存储相同类型的值
+ d. 在内存中相邻存储不同类型的值

## Q140. 大小为n的数组索引范围是：

+ a. 0
+ b. 0 到 n-1
+ c. 1
+ d. 1 到 n

## Q141. 下面哪个数组语句决定数组的维度？

+ a. 数组元素的数量
+ b. 元素的值
+ c. 数组地址
+ d. 数组第一个元素的索引
+ a. 数组的每个元素应该是相同类型

## Q142. 下面哪个语句是不正确的？

a. 语句 `arr[30];` 声明了一个大小为30的数组

## Q148. 默认情况下，静态数组元素初始化为

a
b. 浮点值
c. 字符值
d. 未初始值

数组元素的索引代表在数组中的位置

数组的大小可以增加超过指定大小的元素是真的吗？

## Q149. 数组元素存储在：

a. 随机内存位置
b. 顺序内存位置
c. 散落在内存位置
d. 直接内存位置

## Q150. 如果使用超出大小的索引初始化数组，会发生什么？

+ a. 无影响
+ b. 编译器生成错误信息
c. 操作系统
d. 数组元素被赋予垃圾值
+ b. 表达式 `arr[0]` 代表第一个元素
+ c. 表达式 `arr[1]` 代表第一个元素

# 572 附录 F

## Q151. 联合（union）同时可以存储多少个值？

- a. 仅一个值
- b. 两个值
- c. 任意数量的值
- d. 无值

## Q152. 下列中将数组传递给函数的正确语法是？

- a. `function(name[])`
- b. `function(name_array[])`
- c. `function(name_array, size)`
- d. `function(name_array[size])`

## Q153. 在以下代码中，x 指向什么字符串？

```c
char *x;
char mystr[12] = "asdfghj";
x = mystr;
clr(x);
x += 5;
```

- a. as
- b. bdf
- c. hj
- d. dfghj
- e. 以上均不是

## Q154. 下列哪个语句返回整型变量 x 的内存地址？

- a. `&`
- b. `address(x)`
- c. `*x`
- d. `address(x);`

## Q155. 数组是通过什么方式传递给函数的？

- a. 值
- b. 引用
- c. 值和引用都是
- d. 上下文

## Q156. 下述程序的输出是什么？

```c
#include <stdio.h>
#include <conio.h>
void main()
{
    int arr[4] = {2};
    int i;
    for(i=0; i<4; i++)
    printf("%d", ++arr[0]);
}
```

- a. 11111
- b. 22222
- c. 23456
- d. 34567

## Q157. 下列哪个语句是错误的？

- a. 结构体（structure）用于在相同名称下存储不同数据类型的值
- b. 结构体成员存储在独立的内存位置
- c. 结构体使用 structure 关键字定义
- d. 每个结构体成员必须是相同的数据类型

## Q158. 下述程序的输出是什么？

```c
#include <stdio.h>
#include <conio.h>
void main()
{
    struct {
        unsigned long no: 8;
        unsigned age: 5;
    };
    struct stdl data = {55, 24, 65};
    printf("%d%d%d",std.roll_no,std.marks);
    getch();
}
```

- a. 1 0 7
- b. 8 5 7
- c. 55 54 65
- d. 编译时错误

## Q159. 下述程序的输出是什么？

```c
#include <stdio.h>
#include <conio.h>
void main()
{
    struct bit1 {
        unsigned a:5;
        unsigned b:5;
        char c;
        int d;
    } bit1;
    clrscr(c);
    printf("%d",sizeof(bit1));
    getch();
}
```

- a. 7
- b. 4
- c. 5
- d. 编译时错误

## Q160. 当结构体和联合包含以下内容时，它们的大小相同：

a. 单一成员

- a. 单一成员
- b. 任意数量的成员
- c. (a) 和 (b)
- d. 以上都不是

# 答案

| Q1 | b | Q39 | b |
| :--- | :--- | :--- | :--- |
| Q2 | b | Q40 | c |
| Q3 | b | Q41 | d |
| Q4 | b | Q42 | a |
| Q5 | c | Q43 | d |
| Q6 | a | Q44 | a |
| Q7 | b | Q45 | b |
| Q8 | c | Q46 | c |
| Q9 | a | Q47 | a |
| Q10 | d | Q48 | d |
| Q11 | b | Q49 | a |
| Q12 | a | Q50 | b |
| Q13 | b | Q51 | a |
| Q14 | c | Q52 | b |
| Q15 | d | Q53 | b |
| Q16 | c | Q54 | b |
| Q17 | b | Q55 | b |
| Q18 | d | Q56 | b |
| Q19 | d | Q57 | b |
| Q20 | b | Q58 | d |
| Q21 | d | Q59 | d |
| Q22 | a | Q60 | b |
| Q23 | d | Q61 | b |
| Q24 | c | Q62 | a |
| Q25 | a | Q63 | b |
| Q26 | b | Q64 | c |
| Q27 | d | Q65 | d |
| Q28 | c | Q66 | c |
| Q29 | a | Q67 | a |
| Q30 | b | Q68 | c |
| Q31 | - | Q69 | a |
| Q32 | a | Q70 | b |
| Q33 | d | Q71 | a |
| Q34 | c | Q72 | b |
| Q35 | b | Q73 | d |
| Q36 | b | Q74 | b |
| Q37 | b | Q75 | c |
| Q38 | c | Q76 | c |
| | | Q77 | c |
| | | Q78 | c |
| | | Q79 | a |
| | | Q80 | b |
| Q81 | a | Q122 | c |
| Q82 | d | Q123 | a |
| Q83 | a | Q124 | d |
| Q84 | a | Q125 | a |
| Q85 | c | Q126 | a |
| Q86 | a | Q127 | b |
| Q87 | d | Q128 | c |
| Q88 | b | Q129 | a |
| Q89 | c | Q130 | a |
| Q90 | d | Q131 | a |
| Q91 | c | Q132 | c |
| Q92 | a | Q133 | b |
| Q93 | d | Q134 | a |
| Q94 | c | Q136 | d |
| Q95 | c | Q137 | d |
| Q96 | a | Q138 | a |
| Q97 | d | Q139 | c |
| Q98 | c | Q140 | b |
| Q99 | b | Q141 | d |
| Q100 | b | Q142 | c |
| Q101 | a | Q143 | b |
| Q102 | a | Q144 | c |
| Q103 | c | Q145 | a |
| Q104 | b | Q146 | a |
| Q105 | c | Q147 | c |
| Q106 | a | Q148 | a |
| Q107 | b | Q149 | b |
| Q108 | b | Q150 | d |
| Q109 | b | Q151 | a |
| Q110 | b, c, d | Q152 | c |
| Q111 | b | Q153 | c |
| Q112 | c | Q154 | a |
| Q113 | a | Q155 | b |
| Q114 | a | Q156 | d |
| Q115 | b | Q157 | d |
| Q116 | a | Q158 | c |
| Q117 | a | Q159 | a |
| Q118 | a | Q160 | a |
| Q119 | a | | |
| Q120 | a | | |
| Q121 | a | | |

# 常见口答题

**Q1.** 你如何理解硬件（hardware）和软件（software）？
