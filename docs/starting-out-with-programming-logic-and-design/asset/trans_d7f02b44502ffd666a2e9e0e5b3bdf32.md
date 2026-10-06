

# 程序 6-7

```
// 折扣百分比的全局常量。
Constant Real DISCOUNT_PERCENTAGE = 0.20
// 主模块是程序的起始点。
Module main()
    // 用于存储原价和销售价的局部变量。
    Declare regularPrice,salePrice
    // 获取物品的原价。
    Set regularPrice = getRegularPrice()
    // 计算销售价。
    Set salePrice = regularPrice - discount(regularPrice)
    // 显示销售价。
    Display "The sale price is $", salePrice
End Module
// getRegularPrice 函数提示用户
// 输入物品的原价，并
// 将该值作为 Real 类型返回。
Function getRegularPrice()
    // 用于存储价格的局部变量。
    Declare regularPrice
    // 获取原价。
    Display "Enter the item's regular price."
    Input price
// 返回原价。
    Return price
End Function
// discount 函数接收物品的价格作为
// 参数，并返回由 DISCOUNT_PERCENTAGE
// 指定的折扣金额。
Function discount(Real price)
    Return price * DISCOUNT_PERCENTAGE
End Function
```

# 程序输出（输入部分加粗显示）

Enter the [item]'s regular price.
**100.00 [Enter]**
nThe sale price is $80

# 在函数中使用 IPO 图

你在第 2 章中学习过，IPO 图是设计程序的一种简单而有效的工具。回想一下 IPO 代表输入（input）、处理（processing）和输出（output），IPO 图描述了程序的输入、处理和输出。你也可以为程序中的每个函数创建 IPO 图。输入列显示了作为参数传递给函数的数据描述，处理列显示了函数执行的操作描述，输出列描述了从函数返回的数据。例如，图 6-10 是你在中看到的 getPrice 和 discount 函数的 IPO 图。

**图 6-10** getPrice 和 discount 函数的 IPO 图

| getPrice 函数的 IPO 图 | | |
|---|---|---|
| 输入 (Input) | 处理 (Processing) | 输出 (Output) |
| 无 | 提示用户输入物品的原价 | 物品的价格，Real 类型 |

| discount 函数的 IPO 图 | | |
|---|---|---|
| 输入 (Input) | 处理 (Processing) | 通过原价乘以全局常量 DISCOUNT_PERCENTAGE 来计算物品折扣 | 物品的折扣，Real 类型 |

注意，IPO 图仅对函数的输入、处理和输出提供简要描述，但没有显示函数中执行的具体步骤。然而在许多情况下，IPO 图包含了足够的信息，可以用来代替流程图。是否使用 IPO 图或流程图通常取决于程序员的个人喜好。

# **焦点：**
**使用函数模块化**

Hal 拥有一名为“Make Your Own Music”的业务，销售吉他、鼓、班卓琴、合成器等许多乐器。Hal 的员工严格按佣金工作。在月底，每位销售人员的佣金根据根据表 6-1 计算的。

**表 6-1** 销售佣金率

| 本月销售额 | 佣金率 |
|---|---|
| 少于 $10,000.00 | 10% |
| $10,000.00–14,999.99 | 12% |
| $15,000.00–17,999.99 | 14% |
| $18,000.00–21,999.99 | 16% |
| $22,000 或更多 | 18% |

![](img/c939132f78787c7f339c6977b3fc8c85_266_0.png)

# 6.2 编写自己的函数

例如，月销售额为 $16,000 的销售人员将获得 14% 的佣金（$2,240）。另一位月销售额为 $20,000 的销售人员将获得 16% 的佣金（$3,200）。月销售额为 $30,000 的人将获得 18% 的佣金（$5,400）。

由于员工每月结算一次，Hal 允许每位员工每月预支高达 $2,000。在计算销售佣金时，每位员工的预支金额将从佣金中减去。如果任何销售人员的佣金低于其预支金额，该销售人员必须向 Hal 补差额。为了计算销售人员的月薪，Hal 使用以下公式：
工资 = 销售额 × 佣金率 – 预支工资

Hal 请你写一个程序为他进行此计算。以下算法大概述了程序必须采取的步骤：

1. 获取销售人员的月销售额。
2. 获取预支金额。
3. 使用月销售额确定佣金率。
4. 计算销售人员的工资；如果金额为负，则表示该销售人员必须向公司还款。

程序 6-8 显示了程序的伪代码，该程序通过许多函数实现了模块化。我们不一次性展示整个程序，而是先检查主模块和每个函数。以下为主模块：

# 程序 6-8 佣金率程序：主模块

```
1 Module main()
2 // 局部变量
3 Declare Real sales, commissionRate, advancedPay
4
5 // 获取销售额。
6 Set sales = getSales()
7
8 // 获取预支金额。
9 Set advancedPay = getAdvancedPay()
10
11 // 确定佣金率。
12 Set commissionRate = determineCommissionRate(sales)
13
14 // 计算工资。
15 Set pay = sales * commissionRate - advancedPay
16
17 // 显示工资金额。
18 Display "The pay is $", pay
19
20 // 判断工资是否为负。
21 If pay < 0
22 Display "The salesperson must reimburse
23 Display "the company.\"
24 End If
25 End Module
```

# 第 6 章 函数

第 3 行声明了变量 sales、commissionRate 和 advancedPay。第 6 行调用 getSales 函数，它获取销售额并返回该值。第 9 行调用 getAdvancedPay 函数，获取预支金额并返回该值。第 12 行调用 determineCommissionRate 函数并将 sales 作为参数传递。第 15 行计算工资，第 18 行显示该金额。第 21 到 24 行的 If-then 语句判断工资是否为负，如果是，则显示销售人员必须向公司还款的消息。图 6-11 显示了主模块的流程图。

# 图 6-11 主模块的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_268_0.png)

接下来是 getSales 函数的定义。

# 6.2 编写自己的函数

```
27 // getSales 函数获取销售人员的
28 月销售额并返回
29 该值作为 Real 类型。
30 Function getSales()
31 // 用于存储价格的局部变量。
32 Declare Real monthlySales
33
34 // 获取月销售额。
35 Display "Enter the salesperson's monthly sales."
36 Input monthlySales
37
38 // 返回月销售额。
39 Return monthlySales
40 Function
```

getSales 函数的目的是提示用户输入销售额并返回该金额。第 32 行声明了局部变量 monthlySales。第 35 行告诉用户输入销售额，第 36 行获取用户的输入并将其存储在 monthlySales 变量中。第 39 行返回 monthlySales 变量中的金额。图 6-12 显示了该函数的流程图。

# 图 6-12 getSales 函数的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_269_0.png)

接下来是 getAdvancedPay 函数的定义。

```
42 // getAdvancedPay 函数获取给销售人员的
43 预支金额并
44 返回该金额作为 Real 类型。
45 Function Real getAdvancedPay()
46 // 用于存储预支金额的局部变量。
47 Declare Real advanced
48
49 // 获取预支金额。
50 Display "Enter the amount of advanced pay, or"
51 Display "0" if no advanced pay was given."
52 Input advanced
53
54 // 返回预支金额。
55 Return advanced
56 End Function
```

getAdvancedPay 函数的目的是提示用户输入销售人员的预支金额并返回该金额。第 47 行声明了局部变量 advanced。第 50 和第 51 行告诉用户输入预支金额（如果没有预支则输入 0），第 52 行获取用户的输入并将其存储在局部变量中。第 55 行返回 advanced 变量中的金额。图 6-13 显示了该函数的流程图。

# 图 6-13 getAdvancedPay 函数的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_270_0.png)

