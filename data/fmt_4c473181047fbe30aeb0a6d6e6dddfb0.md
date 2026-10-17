
``` 
1 Module main()
2 // 局部变量
3 Declare Real sales, commissionRate, advancedPay

5 // 获取销售额。
6 Set sales = getSales()

8 // 获取预支金额。
9 Set advancedPay = getAdvancedPay()

11 // 确定佣金率。
12 Set commissionRate = determineCommissionRate(sales)

14 // 计算工资。
15 Set pay = sales * commissionRate - advancedPay

17 // 显示工资金额。
18 Display "The pay is $", pay

20 // 判断工资是否为负。
21 If pay < 0
22 Display "The salesperson must reimburse
23 Display "the company.\"
24 End If
25 End Module
```

# 第 6 章 函数

第 3 行声明了变量 `sales`、`commissionRate` 和 `advancedPay`。第 6 行调用 `getSales` 函数，它获取销售额并返回该值。第 9 行调用 `getAdvancedPay` 函数，获取预支金额并返回该值。第 12 行调用 `determineCommissionRate` 函数并将 `sales` 作为参数传递。第 15 行计算工资，第 18 行显示该金额。第 21 到 24 行的 `If-then` 语句判断工资是否为负，如果是，则显示销售人员必须向公司还款的消息。图 6-11 显示了主模块的流程图。

## 图 6-11 主模块的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_268_0.png)

接下来是 `getSales` 函数的定义。

## 6.2 编写自己的函数

```
27 // getSales 函数获取销售人员的
28 月销售额并返回
29 该值作为 Real 类型。
30 Function getSales()
31 // 用于存储价格的局部变量。
32 Declare Real monthlySales

34 // 获取月销售额。
35 Display "Enter the salesperson's monthly sales."
36 Input monthlySales

38 // 返回月销售额。
39 Return monthlySales
40 Function
```

`getSales` 函数的目的是提示用户输入销售额并返回该金额。第 32 行声明了局部变量 `monthlySales`。第 35 行告诉用户输入销售额，第 36 行获取用户的输入并将其存储在 `monthlySales` 变量中。第 39 行返回 `monthlySales` 变量中的金额。图 6-12 显示了该函数的流程图。

## 图 6-12 getSales 函数的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_269_0.png)

接下来是 `getAdvancedPay` 函数的定义。

```
42 // getAdvancedPay 函数获取给销售人员的
43 预支金额并
44 返回该金额作为 Real 类型。
45 Function Real getAdvancedPay()
46 // 用于存储预支金额的局部变量。
47 Declare Real advanced

49 // 获取预支金额。
50 Display "Enter the amount of advanced pay, or"
51 Display "0" if no advanced pay was given."
52 Input advanced

54 // 返回预支金额。
55 Return advanced
56 End Function
```

`getAdvancedPay` 函数的目的是提示用户输入销售人员的预支金额并返回该金额。第 47 行声明了局部变量 `advanced`。第 50 和第 51 行告诉用户输入预支金额（如果没有预支则输入 0），第 52 行获取用户的输入并将其存储在局部变量中。第 55 行返回 `advanced` 变量中的金额。图 6-13 显示了该函数的流程图。

## 图 6-13 getAdvancedPay 函数的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_270_0.png)

### 6.2 编写你自己的函数

接下来是定义 `determineCommissionRate` 函数。

| 程序 6-8 | 佣金率程序（续）：determineCommissionRate 函数 |
|---|---|

| 58 | // determineCommissionRate 函数接收 |
| 59 | // 销售额作为参数，并返回 |
| 60 | // 实数 Real 类型的佣金率 |
| 61 | Function Real determineCommissionRate(Real sales) |
| 62 | // 用于存储佣金率的局部变量。 |
| 63 | Declare Real rate |
| 64 | |
| 65 | |
| 66 | // 确定佣金率。 |
| 67 | If sales < 10000.00 Then |
| 68 | Set rate = 0.10 |
| 69 | Else If sales >= 10000.00 AND sales <= 14999.99 Then |
| 70 | Set rate = 0.12 |
| 71 | Else If sales >= 15000.00 AND sales <= 17999.99 Then |
| 72 | Set rate = 0.14 |
| 73 | Else If sales >= 18000.00 AND sales <= 21999.99 Then |
| 74 | Set rate = 0.16 |
| 75 | Else |
| 76 | Set rate = 0.18 |
| 77 | End If |
| 78 | // 返回佣金率。 |
| 79 | Return rate |
| 80 | End Function |

`determineCommissionRate` 函数接收销售额作为参数，并返回该销售额对应的佣金率。第 63 行声明了一个名为 `rate` 的局部变量，用于存储佣金率。第 66 行到 76 行的 `If-Then-Else` 语句测试 `sales` 参数并将正确的值分配给局部变量。第 79 行返回 `rate` 变量中的值。图 6-14 显示了该函数的流程图。

图 6-14 determineCommissionRate 函数的流程图

![](img/c93132f7878c9fc85_272_0.png)

程序输出（输入部分加粗**）

输入销售人员的每月销售额。

4650.00 [Enter]

输入预付金额，或如果没有发放预付。

10000.00 [Enter]

工资为 $758.00

程序输出（输入部分加粗**）

输入销售人员的每月销售额。

9000.00 [Enter]

输入预付金额，或如果没有发放预付。

0 [Enter]

工资为 $2000.00

程序输出（输入部分加粗**）

输入销售人员的每月销售额。

12000.00 [Enter]

输入预付金额，或如果没有发放预付。

2000.00 [Enter]

工资为 $56.00

### 返回字符串

你已经看到了了返回数字的函数示例。大多数编程语言允许你编写返回字符串的函数。例如，下面的伪代码提示用户输入他们的姓名，然后返回用户输入的字符串。

```
Function String getName()
// 用于存储用户姓名的局部变量。
Declare String name
// 获取用户名。
Display "Enter your name."
Input name
// 返回姓名。
Return name
End Function
```

### 返回布尔值

大多数语言允许你编写布尔函数，其返回 `True`（真）或 `False`（假）。你可以使用布尔函数来测试条件，然后返回 `True` 或 `False` 来指示该条件是否存在。布尔函数对于简化决策和重复结构中测试的复杂条件有用。

例如，假设你正在设计一个程序，允许用户输入一个数字，然后判断该数字是偶数还是奇数。伪代码显示了如何进行判断：

```
If number MOD 2 == 0 Then
Display "The number is even."
Else
Display "The number is odd."
End If
```

这个 `If-Then` 语句测试的布尔表达式的含义并不清楚，让我们仔细观察一下：

```
number MOD 2 ==
```

该表达式使用了第 2 章引入的 `MOD` 运算符。回想一下 `MOD` 运算符除两个整数并返回除法的余数。因此，这段伪代码的意思是：“如果 number 除以 2 的余数为 0，则显示一条指示数字为偶数的消息，否则显示指示数字为奇数的消息。”

因为偶数除以 2 的余数始终为 0，所以这个逻辑是通行的。然而，如果你能将其重写为“如果数字是偶数，则显示它是偶数的消息，否则显示它是奇数的消息”，那么伪代码将更容易理解。事实证明，可以通过布尔函数来实现。在这个示例中，你可以设计一个名为 `isEven` 的函数，它接受一个数字作为参数，如果数字是偶数则返回 `True`，否则返回 `False`。以下是此类函数的伪代码。

```
Function Boolean isEven(Integer number)
// 用于存储 True 或 False 的局部变量。
Declare Boolean status

// 确定 number 是否为偶数。如果是，则将
// status 设置为 True。否则，设置为 False。
If number MOD 2 == 0 Then
Set status = True
Else
Set status = False
End If

// 返回 status 的值。
Return status
End Function
```

然后你可以重写 `If` 语句，使其调用 `isEven` 函数来判断数字是否为偶数：

```
If isEven(number) Then
Display "The number is even."
Else
Display "The number is odd."
End If
```

这不仅让你更容易理解，而且你现在有了一个可以在任何需要的地方判断偶数的函数。

### 检查点

- 6.6 `Return` 语句在函数的目的是是什么？

- 6.7 查看下面的伪代码定义：

  Function doSomething(Integer number)

  Return number

  a. 该函数的名称是什么？

  b. 该函数返回什么类型的数据？

  c. 给定该函数定义，以下语句将显示什么？

- 6.8 布尔函数是什么？

## 更多库函数

> 注意：本书中提供的函数是你在实际编程语言中找到的函数的通用版本。它们的工作方式可能会有所不同。

### 数学函数

大多数编程语言提供了多种数学函数。这些函数通常接受一个或多个参数，执行数学运算并返回结果。例如 `sqrt` 和 `pow`。

### sqrt 函数

`sqrt` 函数接受一个参数并返回其平方根。这里是它的使用示例：

```
Set result = sqrt(16)
```

该语句调用 `sqrt` 函数，将 16 作为参数。`sqrt` 函数返回参数的平方根，然后赋值给 `result` 变量。

程序 6-9

```
// 变量声明
Declare number
Declare Real squareRoot

// 获取一个数字。
Display "Enter a number."
Input number

// 计算并显示其平方根。
Set squareRoot = sqrt(number)
Display "The square root of number is ", squareRoot
```

程序输出（输入部分加粗**）

输入一个数字。

25 [Enter]

数字的平方根为 5

程序 6-10 寻找三角形的直边。程序使用了以下公式，你可能在几何课上学过：

$$c = a²+b²$$

在公式中，$c$ 是直边的长度，$a$ 和 $b$ 是另外两条边的长度。

程序 6-10

```
// 变量声明
Declare a, b, c

// 获取边 A 的长度。
Display "Enter the length of side A."
Input a

// 获取边 B 的长度。
Display "Enter the length of side B."
Input b

// 计算直边的长度。
Set c = sqrt(a²+b²)

// 显示直边的长度。
Display "The length of the hypotenuse is ", c
```

程序输出（输入部分加粗**）

输入边 A 的长度。

5.0 [Enter]

输入边 B 的长度。

12.0 [Enter]

直边的长度为 13

### pow 函数

另一个常见的数学函数是 `pow` 函数。`pow` 函数的目的是计算数字的幂。简单而言之，它与我们一直使用的 `^` 运算符的功能相同。然而，在某些编程语言中，并没有计算数字幂的运算符。相反，它们使用诸如 `pow` 的函数。这里是 `pow` 函数的使用方法：

```
Set area = pow(4, 2)
```

该语句调用 `pow` 函数，将 4 和 2 作为参数。函数返回 4 的 2 次方的值，将其赋值给 `area` 变量。

# 表 6-2 其他常用的数学函数

| 函数名称 | 描述和示例用法 |
| --- | --- |
| abs | 返回参数的绝对值。<br>示例：执行以下语句后，变量 y 将包含变量 x 中值的绝对值。变量 x 将保持不变。<br><br>y = abs(x) |
| cos | 返回参数的余弦值。参数应该是以弧度为单位的角度。<br>示例：执行以下语句后，变量 y 将包含存储在变量 x 中的角度的余弦值。变量 x 将保持不变。<br><br>y = cos(x) |
| round | 接受实数作为参数，并返回四舍五入到最近整数的参数值。例如，round(3.5) 将返回 4，而 round(3.2) 将返回 3。<br>示例：执行以下语句后，变量 y 将包含变量 x 的四舍五入到最近整数后的值。变量 x 将保持不变。<br><br>y = round(x) |
| sin | 返回参数的正弦值。参数应该是以弧度为单位的角度。<br>示例：执行以下语句后，变量 y 将包含存储在变量 x 中的角度的正弦值。变量 x 将保持不变。<br><br>y = sin(x) |
| tan | 返回参数的正切值。参数应该是以弧度为单位的角度。<br>示例：执行以下语句后，变量 y 将包含变量 x 中值的正切值。变量 x 将保持不变。<br><br>y = tan(x) |

## 数据类型转换函数

大多数编程语言都提供了库函数，可以将一种数据类型转换为另一种类型。例如，大多数语言都提供一个将实数转换为整数的函数，以及一个将整数转换为实数的函数。在本书的伪代码中，我们使用 `toInt` 函数将实数转换为整数，并使用 `toReal` 函数将整数转换为实数。这些函数在表 6-3 中描述。

# 表 6-3 数据类型转换函数

| 函数 | 描述和示例用法 |
| --- | --- |
| toInteger | toInteger 接受一个实数作为参数，并返回该数字转换后的整数。如果实数有小数部分，则小数部分将被丢弃。例如，调用函数 toInteger(2.5) 将返回 2。 \n示例：如果以下是实际代码，在这些语句执行后，变量 i 将包含值 2。\n```Declare Integer i\nDeclare Real r = 2.5\nSet i = toInteger(r)\n``` |
| toReal | toReal 接受一个整数作为参数，并返回该数字转换后的实数。 \n示例：如果以下是实际代码，变量 v 将包含值 7.0。\n```Declare Integer i = 7\nDeclare Real r\nSet r = toReal(i)\n``` |

在许多语言中，如果你尝试将一种类型的值赋值给另一种数据类型的变量，就会发生错误。例如，查看以下伪代码：

```
Declare Integer number
Set number = 6.17 这在许多语言中会导致错误！
```

第一条语句声明了一个名为 number 的整数变量。第二条语句尝试将实数 6.17 赋值给该变量。在某些编程语言中这将会导致错误，因为整数变量不能持有小数值。这种错误结果有时被称为类型不匹配错误。

> 注意：大多数语言允许你将整数赋值给实数而不会导致错误，因为这样做不会导致数据丢失。将整数转换为实数的函数仍然存在，以防你需要显式地执行这种类型转换。

有时你可能会编写出在没有意识的情况下导致类型不匹配错误的代码。例如，查看程序 6-11 中的伪代码。该程序计算用给定数量柠檬水可以服务的人数。

# 程序 6-11

```
1 // 声明一个变量来存储可用柠檬水的
2 // 盎司数。
3 // Declare Real ounces
4 
5 // 声明一个变量来存储我们可以服务的
6 // 人数。
```

## 6.3 更多库函数
