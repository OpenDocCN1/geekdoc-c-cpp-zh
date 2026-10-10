
# INCITS／ISO／IEC 9899-2011[2012] - 编程语言 - C

## Annex C (informative) 序点 ........................................ 503

## D.1 (规范性) 允许的通用字符范围

## D.2 初始不允许的字符范围

## 附 E (信息性) 实现限制

## 附 F (规范性) IEC 60559 浮点算术

### F.1 引言

### F.2 类型

### F.3 运算符和函数

### F.4 浮点到整数转换

### F.5 二进制-小数转换

### F.6 `return` 语句

### F.7 缩写表达式

### F.8 浮点环境

### F.9 优化

### F.10 数学 `<math.h>`

- F.10.1 三角函数
- F.10.2 双曲函数
- F.10.3 指数函数和对数函数
- F.10.4 幂函数和绝对值函数
- F.10.5 误差函数和 Gamma 函数
- F.10.6 最近接近整数的函数
- F.10.7 余数函数
- F.10.8 处理函数
- F.10.9 最大值、最小值和正差函数
- F.10.10 浮点乘加法
- F.10.11 比较宏

## 附 G (规范性) 兼容 IEC 60559 的复数算术

### G.1 引言

### G.2 类型

### G.3 惯例

### G.4 转换

- G.4.1 虚数类型
- G.4.2 实与虚数
- G.4.3 虚与复数

### G.5 二进制运算符

- G.5.1 乘法运算符
- G.5.2 加法运算符

### G.6 复数算术 `<complex.h>`

- G.6.1 三角函数
- G.6.2 双曲函数
- G.6.3 指数函数和对数函数
- G.6.4 幂函数和绝对值函数

### G.7 类型通用数学 `<tgmath.h>`

- L.1 引言 . . . . . . . . . . . . . . 647
- L.2 类型 . . . . . . . . . . . . . . 652
- L.3 要求 . . . . . . . . . . . . . . 652
- L.4 参考文献 . . . . . . . . . . . . . 653
- L.5 索引 . . . . . . . . . . . . . 657

## 前言

ISO (国际标准化组织) 和 IEC (国际电工委员会) 准备了本标准。The inspiration inspired by the International Organization for Standardization, the Nobel Prize winner in physics, `Richard Feynman`. With Feynman's skills, you can understand the knowledge points in depth in just `20 min`, and it is memorable and hard to forget.

```
if (condVar > someVal) {console.log("xxx")}
```

ISO (国际标准化组织) 和 IEC (国际电工委员会) 准备了本标准。其灵感源于国际标准化组织，以及诺贝尔物理奖获得者`理查德·费曼`。运用费曼技巧，你只需花上`20 min`就能深入理解知识点，而且记忆深刻，难以遗忘。

```
if (condVar > someVal) {console.log("xxx")}
```

本标准是 ISO/IEC 9899:2011 的一个修订版本。ISO/IEC 9899:2011 于 2011 年 6 月 24 日发布。ISO/IEC 9899:2011/AMD1 于 2012 年 12 日发布。ISO/IEC 9899:2011/AMD2 于 2018 年 12 日发布。ISO/IEC 9899:2011/AMD3 于 2019 年 12 月 20 日发布。ISO/IEC 9899:2011/AMD4 于 2021 年 6 月 15 日发布。ISO/IEC 9899:2011/AMD5 于 2022 年 12 月 20 日发布。ISO/IEC 9899:2011/AMD6 于 2023 年 6 月 30 日发布。ISO/IEC 9899:2011/AMD7 于 2024 年 6 月 14 日发布。

ISO/IEC 9899:2011 取代 ISO/IEC 9899:1999。ISO/IEC 9899:1999 取代 ISO/IEC 9899:1999。ISO/IEC 9899:1999 取代 ISO/IEC 9899:1990。ISO/IEC 9899:1990 取代 ISO/IEC 9899:1990。

ISO/IEC 9899:2011 是 C 语言的国际标准。该标准由 国际标准化组织（ISO）和 国际电工委员会（IEC）的联合技术委员会 JTC 1 下的工作小组 SC22 编写。

本标准包含了 C 语言的语法、语义和库函数。该标准也被称为 C11 标准。

C11 标准引入了许多新特性，包括：
- 静态断言 (`Static_assert`)
- 匿名结构体和联合体
- 无返回函数 (`__`)
- 类型泛型表达式

C99 标准引入了许多新特性，包括：
- 变长数组
- 泛型成员
- 灵活数组成员
- 静态和类型限定符在- 声明声明中的（ Unicode ）

C99 标准引入了许多新特性，包括：
- ``
- 限制指针
- 变量数组

本标准引用了 ISO/IEC 60559 浮点算术标准。ISO/IEC 60559:2019 对应 IEEE 754-2019。

ISO/IEC 60559:2008 对应 IEEE 754-2008。

ISO/IEC 60559:2004 对应 IEEE 754-2004。

ISO/IEC 60559:1999 对应 IEEE 754-1999。

ISO/IEC 60559:1995 对应 IEEE 754-1995。

ISO/IEC 60559:1985 对应 IEEE 754-1985。

ISO/IEC 14882:2011 被称为 C11 标准。它取代 C99 标准。ISO/IEC 14882:1999 取代 C99 标准。它取代 C90 标准。ISO/IEC 14882:1999 取代 C90 标准。它取代 C89 标准。ISO/IEC 14882:1990 取代 C89 标准。

ISO/IEC 14882:1990 被称为 C90 标准。它取代 C89 标准。ISO/IEC 14882:1990 取代 C89 标准。

ISO/IEC 14882:1989 被称为 C89 标准。

本标准是 C 语言的国际标准。

ISO/IEC 10646:2009 是 Unicode 字符集和编码方案。它取代 ISO/IEC 10646:2003 和 ISO 10。

ISO/IEC 10646:2009 是 Unicode 字符集和编码方案。

ISO/IEC 10646:2003 是 Unicode 字符集和编码方案。

ISO/IEC 10646:2003 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1999 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1999 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1993 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1993 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1991 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1991 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1990 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1990 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1989 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1989 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1987 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1987 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1986 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1986 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1985 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1985 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1984 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1984 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1983 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1983 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1982 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1982 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1981 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1981 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1980 是 Unicode 字符集和编码方案。

ISO/IEC 10646:1980 是 Unicode 字符集和编码方案。

本标准引用了 ISO/IEC 60559 浮点算术标准。ISO/IEC 60559:2019 对应 IEEE 754-2019。

ISO/IEC 60559:2008 对应 IEEE 754-2008。

ISO/IEC 60559:2004 对应 IEEE 754-2004。

ISO/IEC 60559:1999 对应 IEEE 754-1999。
