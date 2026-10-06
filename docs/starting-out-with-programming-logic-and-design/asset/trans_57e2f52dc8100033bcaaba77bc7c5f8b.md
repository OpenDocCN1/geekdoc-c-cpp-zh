

## 4.5 Case 结构

图 4-18 Case 结构

![](img/c939132f78787c7f339c6977b3fc8c85_175_0.png)

Select testExpression
Case value_1:
  statement
  statement
  etc.

> 这是一个变量或表达式。
如果 testExpression 等于 value_1，则执行这些语句。

Case value_2:
  statement
  statement
  etc.

> 如果 testExpression 等于 value_2，则执行这些语句。

根据需要插入任意数量 Case 部分
Case value_N:
  statement
  statement
  etc.

> 如果 testExpression 等于 value_N，则执行这些语句。

Default:
  statement
  statement
  etc.

> 如果 testExpression 不等于 Case 语句之后列出的任何值，则执行这些语句。

End Select 这是该结构的结束。

该结构的第一行以 Select 单词开头，后面跟着一个 testExpression。testExpression 通常是一个变量，但在许多语言中，它可以是任何产生值的内容（例如表达式）。结构内部包含一个或多个以 Case 语句开头的语句块。注意 Case 后面跟着一个值。

当 Select case 语句执行时，它会将 testExpression 的值与每个 case 语句后的值（从上到下）进行比较。当它找到与 testExpression 值匹配的 Case 值时，程序跳转到 Case 语句。紧随 Case 语句的语句将被执行，然后程序跳出该结构。如果 testExpression 不匹配任何 Case 值，程序将跳转到 Default 语句并执行紧随其后的语句。

例如，以下伪代码与图 4-18 所示的流程图的操作相同。

```
Select month
Case 1:
  Display "January"
Case 2:
  Display "February"
Case 3:
  Display "March"
Default:
  Display "Error: Invalid month"
End Select
```

在这个示例中，testExpression 是 month 变量。如果 month 变量值为 1，程序将跳转到 Case 1: 部分并执行紧随其后的 Display "January" 语句。如果 month 变量值为 2，程序将跳转到 Case 2: 部分并执行紧随其后的 Display "February" 语句。如果 month 变量值为 3，程序将跳转到 Case 3: 部分并执行紧随其后的 Display "March" 语句。如果 month 变量值不是 1、2 或 3，程序将跳转到 Case 1: 部分并执行紧随其后的 Display "Error: Invalid month" 语句。

> 注意：在许多语言中，case 结构被称为 switch 语句。

Case 结构并非总是需要的，因为可以使用嵌套决策结构实现相同的逻辑。例如，图 4-19 显示了等同于图 4-18 Case 结构的嵌套决策结构。然而，在可以使用它们的情况下，case 结构更加直观。

## 图 4-19 嵌套决策结构

![](img/c939132f78787c7f339c6977b3fc8c85_176_0.png)

### 焦点：使用 Case 结构

Lenny's Stereo and Television 店的老板 Lenny 邀请你编写一个程序，让客户选择三种电视型号中的一种，并显示所选型号的价格和尺寸。以下是算法：

- 1. 获取电视型号号。
- 2. 如果型号为 100，则显示该型号的信息。
  否则，如果型号为 200，则显示该型号的信息。否则，如果型号为 300，则显示该型号的信息。

首先，考虑设计一个嵌套决策结构来确定型号并显示正确的信息。但你意识到 case 结构同样可以工作，因为单个值（即型号号）将用于确定程序将要执行的操作。型号号可以存储在变量中，该变量可以通过 case 结构进行测试。假设型号号存储在名为 modelNumber 的变量中，图 4-20 显示了 case 结构的流程图。程序 4-8 显示了该程序的伪代码。

## 图 4-20 Case 结构的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_177_0.png)

## 程序 4-8

```
// 电视价格的常量
Constant Real MODEL_100_PRICE = 199.99
Constant Real MODEL_200_PRICE = 269.99
Constant Real MODEL_300_PRICE = 349.99

// 电视尺寸的常量
Constant Integer MODEL_100_SIZE = 24
Constant Integer MODEL_200_SIZE = 27
Constant Integer MODEL_300_SIZE = 32
Declare Integer modelNumber

// 型号号变量
// 获取型号号
Display "Which TV are you interested in?"
Input modelNumber

// 显示价格和尺寸
Select modelNumber
Case 100:
  Display $199.99
  Display 24
Case 200:
  Display $269.99
  Display 27
Case 300:
  Display $349.99
  Display 32
Default:
  Display "Invalid model"
End Select
```

## 4.6 逻辑运算符

编程语言提供一组被称为逻辑运算符，您可以使用它们来创建复杂的表达式。表 4-3 描述了这些运算符。

### 表 4-3 逻辑运算符

| 运算符 | 含义 |
| --- | --- |
| AND | AND 运算符连接两个布尔表达式。只有当两个表达式都为真时，复合表达式才为真。 |
| OR | OR 运算符连接两个布尔表达式。一个或两个表达式为真时，表达式即为真。其中一个表达式为真即可。 |
| NOT | NOT 运算符是一个元运算符，意味着它只作用于操作数。操作数必须是布尔值。NOT 运算符反转操作数的真值。如果它应用于一个真表达式，则返回假。如果应用于一个假表达式，则返回真。 |

### 表 4-4 使用逻辑运算符的复合表达式

| 表达式 | 含义 |
| --- | --- |
| x > y AND a < b | x 大于 y 且 a 小于 b？ |
| x == y OR x == z | x 等于 y 或 x 等于 z？ |
| NOT (x > y) | 表达式 > y 不是？ |

> 注意：在许多语言中（特别是 C、C++ 和 Java），AND 运算符写为 &&，而 NOT 运算符写为 !

### AND 运算符

AND 运算符接收两个布尔表达式作为操作数，并创建一个仅当两个子表达式都为真时为真的复合表达式。以下使用 AND 运算符的 If 语句示例：

```
If temperature < 20 AND minutes > 12 Then
    Display "The temperature is in the danger zone."
End If
```

在该语句中，两个布尔表达式 temperature < 20 AND minutes > 12 被合并为一个复合表达式。只有当温度小于 20 且分钟大于 12 时，才会执行 Display 语句。如果任何一个布尔子表达式为假，复合表达式即为假，信息就不会显示。

表 4-5 显示了 AND 运算符的真值表。真值表列出了与 AND 运算符连接的所有真假值组合。同时也显示了表达式的结果值。

