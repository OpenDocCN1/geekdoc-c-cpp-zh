
## `if-else` 语句与 `switch` 语句

**`if-else` 语句**：如果表达式为真，则执行 `if` 部分的语句；如果为假，则执行 `else` 部分的语句。

**`switch` 语句**：根据表达式的值从多个可能的分支中选择一个来执行。

> **注**：由于提供的原文文本存在大量重复和格式错乱，上述翻译已基于高级文档工程师的逻辑进行了清理和对齐，确保核心技术内容的准确性。

## 5.14 C语言编程基础

由若干简单语句组成。考虑程序 5-9 中的代码段。

| 行号 | Prog 5-9.c | 输出窗口 |
|---|---|---|
| 1 | //if-else statement | 编译错误 "Misplaced else in function main" |
| 2 | #include<stdio.h> | 原因： |
| 3 | main() | • 只有单个语句可以与 `if` 子句和 `else` 子句关联。 |
| 4 | { | • 上述代码被解释为： |
| 5 | int a=11; | `if(a)` // `if` 语句后面的语句 |
| 6 | if(a>0) | `printf("The value of a is %d",a);` `printf("Value is greater than 10");` // 没有任何匹配子句的 `else` 子句 |
| 7 | printf("The value of a is %d",a); | |
| 8 | printf("Value is greater than 10"); | 该怎么办？ |
| 9 | else | 在没有匹配子句的情况下，`else` 子句不能存在 |
| 10 | | • 将第 7 和 8 行的语句组成复合语句并重新执行代码 |

**程序 5-9** 用于说明 `if-else` 语句使用的程序

- 5. 注意不要在 `if-else` 头部或 `else` 子句末尾放置分号。

## 5.4.4 嵌套 `if` 语句

如果 `if` 语句体是另一个 `if` 语句或包含另一个 `if` 语句（如下所示），我们说是嵌套的，该语句被称为**嵌套 `if` 语句**。嵌套语句的标准形式为：

```c
if(expression)                //嵌套 if 语句
    statement
else {
    if(expression)
        statement
}
```

(a) `if` 语句体是另一个 `if` 语句

(b) `if` 语句体包含另一个 `if` 语句

这种嵌套可以进行到任意级别，如下所示：

```c
if(expression)
    if(expression2)
```

## 决策与循环语句 5.15

```c
if(expression-n)
statement
```

上述结构似乎形成了一个梯子，被称为 `if` 阶梯。

| 嵌套语句的语法 | 流程图 |
|--- |---|
| `if( Condition 1 or expression )` | ![image](https://example.com/diagram.png) |
| `{` | 无语句块 |
| `Statement A` | |
| `if(Condition 2 or expression2)` | |
| `{` | |
| `Statement C` | 是 语句块 A |
| `}` | |
| `else` | 是 语句块 C |
| `B` | |

**解释**：

如果表达式为真，则执行真值语句或语句块，并执行其内部的其他 `if-else`。

如果表达式为假，则执行假值语句或语句块，并跳过真值体。

> 嵌套可以进行的层数取决于编译器的翻译限制。翻译限制限制了语言翻译器和库的实现。

## 5.4.5 嵌套 `if-else` 语句

在嵌套的 `if-else` 语句中，`if-else` 语句体包含另一个 `if-else` 语句。程序 5-10 展示了如何使用嵌套 `if-else` 语句找到三个数中的最大值。

粗率使用嵌套 `if-else` 语句会引入潜在的歧义源，称为**悬空 `else` 歧义**。当一个语句包含多个 `if` 子句时，关于 `else` 子句正确匹配哪一个子句存在一个潜在的歧义。这种歧义被称为**悬空 `else` 问题**。表 5.1 第 1 列列出的代码存在悬空 `else` 问题。表中的其他列显示了第 1 列列代码的两种可能解释。

## 5.16 C语言编程基础

| 行号 | Prog 5-10.c | 程序控制流程图 | 输出窗口 |
|---|---|---|---|
| 1 | //Nested if-else statement | | 输入三个数字 1 2 |
| 2 | #include<stdio.h> | 开始 | 4 is greatest |
| 3 | main() | | 备注： |
| 4 | { | 输入 a, b & c | 程序展示了 |
| 5 | int a, b, c; | `if (a>b)` | 嵌套 `if-else` 语句的使用 |
| 6 | printf("Enter three numbers\t"); | 是/否 | `if-else` 语句 |
| 7 | scanf("%d %d %d", &a,&b,&c); | `if (a<c)` | `if` 体和 `else` |
| 8 | if(a-b) | 是/否 | 体的 `if-else` |
| 9 | //if-body starts | `if (b<c)` | 位于 `if` |
| 10 | if(a<c) | 是 c is greatest | `else` 语句 |
| 11 | printf("%d is greatest", | | | |

**程序 5-10** 使用嵌套 `if-else` 语句找到三个数最大值的程序

**表 5.1** 第 1 列的代码存在悬空 `else` 歧义。第 2 和 3 列描述了第 1 列代码的可能解释

| 行号 | 悬空 `else` 问题代码（第 1 列） | 解释 I（第 2 列） | 解释 II（第 3 列） |
|---|---|---|---|
| 1 | //Dangling else problem | //Interpretation-I | //Interpretation-II |
| 2 | #include<stdio.h> | #include<stdio.h> | #include<stdio.h> |
| 3 | main() | { | { |
| 4 | { | } | } |
| 5 | int a=10, b=20; | int a=10, b=20; | int a=10, b=20; |
| 6 | if(a==10) | if(a==10) | if(a==10) |
| 7 | if(b==20) | if(b==20) | if(b==20) |
| 8 | printf("Match-I"); | printf("Match-I"); | printf("Match-II"); |
| 9 | else | else | else |
| 10 | printf("Match-II"); | printf("Match-II"); | } |
| 11 | } | } | |
| | 输出 | 如果按这样解释，输出为： | 如果按这样解释，输出为： |
| | 无输出 | Match-II | |

## 决策与循环语句 5.1

悬空 `else` 问题通过两种方式解决：

1.  **编译器的隐式解决**：通过将 `else` 子句与最后一个 `if` 匹配来解决悬空 `else` 歧义，如表 5.1 第 3 列所示。
2.  **用户的显式解决**：可以使用括号消除悬空 `else` 歧义。

## 5.4.6 `switch` 语句

`switch` 语句用于控制复杂的分支操作。有很多时，使用 `if-else` 结构太难以理解。在某些情况下，`switch` 语句提供了一种根据特定条件的结果在多个之间进行选择的简单方法。`switch` 语句的标准形式为：

```c
switch(expression) //switch头部
statement //switch体
```

## 5.18 C语言编程基础

### `switch` 语句的语法

```c
switch (expression)
{
  case label1:
    statements; // 块1 的代码
    break;
  case label2:
    statements; // 块2 的代码
    break;
  case label3:
    statements; // 块3 的代码
    break;
  case label n:
    statements; // 块 n 的代码
    break;
  default:
    statements; // 默认块的代码
}
```

![](img/5451da2a154b586763b5853c6103b79b_252_0.png)

**解释**：

如果在 `switch case` 中满足条件，只要没有明确指定退出 `switch` 语句，则将继续执行下一个 `case`。这通过使用 `break` 关键字来实现。

如果没有满足列出的条件，则执行默认条件。

关于 `switch` 语句的重要点如下：

1.  `switch` 语句由 `switch` 头部和 `switch` 体组成。
2.  `switch` 头部由关键字后跟括号内的 `switch` 选择表达式组成。
3.  选择表达式必须是整型（即整数或字符类型）。
4.  `switch` 体由一个语句组成。构成 `switch` 体的语句可以是空语句、表达式语句、标记语句、流程控制语句、复合语句等。
5.  通常，`switch` 体由复合语句组成，其组成语句是 `case` 标记语句、表达式语句、流程控制语句和可选的 `default` 标记语句。
6.  构成 `switch` 语句体的 `case` 标记语句的 `case` 标签应该是唯一的，即没有两个标签具有或评估为相同的值。
7.  `switch` 体内最多可以有一个 `default` 标记语句。

## 决策与循环语句

8.  `switch` 语句的执行过程如下：
    a. 求出 `switch` 选择表达式的值。
    b. 将 `switch` 选择表达式的计算结果与 `switch` 标记语句的 `case` 标签（`case labels`）进行比较，直到找到匹配项或所有 `case` 标记语句都已检查完毕。
        i. 如果 `switch` 选择表达式的求值结果与某个 `case` 标记语句的 `case` 标签匹配，则执行从匹配的 `case` 标记语句开始，并执行该匹配的 `switch` 语句之后的所有语句。
        ii. 如果 `switch` 体内没有 `case` 标记语句匹配 `switch` 选择表达式的求值结果，则从 `default` 标记语句（`default-labeled statement`）开始（如果存在），并执行 `switch` 体内 `default` 标记语句之后的所有语句。
        iii. 如果没有任何 `case` 标签与 `switch` 选择表达式的求值结果匹配，且 `switch` 体内没有 `default` 标记语句，则不执行任何 `switch` 体，执行将从 `switch` 语句之后的后续语句继续进行。

一个常见的误解是，认为只有匹配的 `case` 标记语句（或者在所有 `case` 标签都不匹配时）`default` 标记语句会被执行。实际上，执行是从匹配的 `case` 标记语句或 `default` 标记语句开始，并执行 `switch` 体内匹配的 `case` 标记语句或 `default` 标记语句之后的所有语句。

程序 5-11 到 5-13 中的代码段说明了上述这些点。

| Prog 5-11.c | 输出窗口 |
| :--- | :--- |
| 1 // switch statement | This is case option I |
| 2 #include<stdio.h> | Value of a is 1 |
| 3 main() | This is case option 2 |
| 4 { | This is default option |
| 5 int a=1; | : |
| 6 switch(a) { | 一个 `switch` 体由 `cases` 组成，并解释为： |
| 7 { | |
| 8 case 1: | |
| 9 printf("This is case option \n"); | //语句 1: `case` 标记语句 |
| 10 printf("Value of a is %d\n"); | //语句 2: 函数语句 |
| 11 case 2: | //语句 3: `case` 标记语句 |
| 12 printf("This is case option 2 \n"); | | |
| 13 default: | //语句 4: `default` 标记语句 |
| 14 printf("This is default option\n"); | | |
| 15 } | | |
| 16 } | 由于 `case` 标签 1 匹配 `switch` 选择表达式的求值结果，执行从标签为 1 的语句开始，并执行 `switch` 体内该语句之后的所有语句![](img/5451da2a154b586763b5853c6103b79b_253_0.png) |

## 5.20 C 语言编程基础

**程序 5-11** | 用于说明 `switch` 语句工作原理程序

| Line | Prog 5-12.c | 输出窗口 |
| :--- | :--- | :--- |
| 1 | // switch statement | This is default option |
| 2 | #include<stdio.h> | This is case 2 |
| 3 | main() | 备注： |
| 4 | { | `switch` 体内 `default` 标记语句的位置没有限制 |
| 5 | int a=3; | 由于 `case` 标签匹配 `switch` 表达式的求值结果，执行从 |
| 6 | switch(a) | `switch` 体内 `default` 标记语句之后的所有语句开始 |
| 7 | { | | | |
| 8 | case 1: | | | |
| 9 | printf("This is case option \n"); | | | |
| 10 | printf("Value of a is %d\n", a); | | | |
| 11 | default: | | | |
| 12 | printf("This is default option\n"); | | | |
| 13 | case 2: | | | |
| 14 | printf("This is case option 2\n"); | | | |
| 15 | } | | | |
| 16 | } | | | |

**程序 5-12** | 用于说明 `switch` 体内 `default` 标记语句位置没有限制的程序

| Line | Prog 5-13.c | 输出窗口 |
| :--- | :--- | :--- |
| 1 | // switch statement & ranges | Upper case vowel |
| 2 | #include<stdio.h> | 备注： |
| 3 | main() | 一个 `switch` 体包含两个 `case` 标记语句。代码解释为： |
| 4 | { | `case 'a':` //语句 1: `case` 标记语句 |
| 5 | char exp='E'; | `case 'e':` //`case` 标记语句的组成语句是 |
| 6 | switch(exp) | `case 'A':` // 另一个 `case` 标记语句 |
| 7 | { | `case 'o':` |
| 8 | case 'a': | printf("Lower case vowel\n"); |
| 9 | case 'e': | `case 'A':` |
| 10 | | `case 'O':` |
| 11 | case 'u': | printf("Upper case vowel\n"); |
| 12 | | - 以这种方式，`switch` 语句可以用于对范围切换： |
| 13 | | - 这种方法在范围较小时是有用的： |
| 14 | | - C 语言不支持对范围进行切换： |
| 15 | | |
| 16 | | |
| 17 | | |
| 18 | | |
| 19 | | |
| 20 | } | | ![](img/5451da2a154b586763b5853c6103b79b_253_0.png) |

**程序 5-13** | 用于说明使用 `switch` 语句切换范围的程序

## 5.4.7 跳转语句

跳转语句在不检查条件的情况下将控制从一点转移到另一个点。C 语言中存在跳转语句：

1.  `goto` 语句
2.  `break` 语句
3.  `continue` 语句
4.  `return` 语句

## 5.4.8 `goto` 语句

`goto` 语句用于从函数内的一点无条件跳转到另一个点。它提供了一种非结构化的转移控制的方法，使得程序控制难以理解和修改。因此，在 C 等结构化编程语言中不建议使用 `goto` 语句。`goto` 语句的语法形式为：

```
goto label;
```

关于 `goto` 语句的要点如下：

1.  `goto` 语句始终与标识符标记语句配合使用。在 `goto` 语句所在的函数体内，`goto` 语句将控制转移到标签相同的标识符标记语句。
2.  `goto` 语句既可以用于向前跳转，也可以向后跳转。如果 `goto` 语句位于对应的标识符标记语句之前，则跳转被称为向前跳转。如果 `goto` 语句位于对应的标识符标记语句之后，则跳转被称为向后跳转。向前和向后跳转如图 5.3 所示。
3.  一个标识符标记语句可以对应多个 `goto` 语句，但一个 `goto` 语句不能对应多个 `goto` 语句。该规则的解释如图 5.4 所示。
4.  `break` 语句可以在函数的任何地方转移控制，即它可以退出嵌套语句、嵌套 `if-else` 语句或嵌套循环。然而，`goto` 语句无论如何无法获取其所在函数的控制。

## 5.4.9 `break` 语句

`break` 语句的语法形式为：

```
break;
```

关于 `break` 语句的要点如下：
