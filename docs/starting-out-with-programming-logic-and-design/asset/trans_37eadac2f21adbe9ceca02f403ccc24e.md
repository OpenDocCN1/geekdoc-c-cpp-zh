

## 第 5 章 重复结构

## 图 5-5 程序 5-4 的主模块

## 图 5-6 showCommission 模块

![](img/c939132f78787c7f339c6977b3fc8c85_206_0.png)

## Do-While 循环

你已经学习过 while 循环循环是一种预测试循环，这意味着它在执行迭代之前会测试条件。`Do-While` 循环是后循环。这意味着它在测试条件之前会执行一次迭代。因此，即使初始条件为假，`Do-While` 循环也会至少执行一次迭代。Do-While 循环的逻辑如图 5-7 所示。

## 5.2 条件控制循环：While, Do-While 和 Do-Until

图 5-7 Do-While 循环的逻辑

![](img/c939132f78787c7f339c6977b3fc8c85_207_0.png)

在流程图中，执行一个或多个语句，然后测试条件。如果条件为真，程序的执行流将返回到循环体内第一条语句上方的点，并重复此过程。如果条件为假，程序将退出循环。

## 在伪代码中编写 Do–While 循环

在伪代码中，我们将使用 `Do-While` 语句来编写 `Do-While` 循环。以下是 `Do-While` 语句的通用格式：

```
Do
    statement
    statement
    etc.
While condition // 这些语句是循环体。它们始终会执行一次，然后在条件为真时重复执行。
```

在通用格式中，出现在 `Do` 和 `While` 子句之间行之间的语句是循环体。出现在 `While` 子句之后的条件是一个布尔表达式。当循环执行时，会执行循环体中的语句，然后对条件进行测试。如果条件为真，循环重新开始并再次执行循环体中的语句。然而，如果条件为假，程序将退出循环。

如通用格式所示，在编写 `Do-While` 语句时应遵循以下约定：

- 确保 `Do` 子句和 `While` 子句对齐。
- 缩进循环体中的语句。

## 第 5 章

如程序 5-5 所示，佣金计算程序可以很容易修改为使用 `Do-While` 循环代替 `While` 循环。注意在程序的这个版本的第 3 行中，我们没有用字符串 "y" 初始化 `keepGoing` 变量。这是没有必要的，因为第 7 行到第 15 行的 `Do-While` 循环将至少执行一次。这意味着在第 15 行测试条件之前，第 14 行的 `Input` 语句始终会执行获取一个值。

图 5-8 显示了主模块的流程图。

## 程序 5-5

```
Module main()
  // 局部变量
  Declare String keepGoing

  // 根据需要多次计算佣金。
  Do
    // 显示销售的佣金。
    Call showCommission()
    // 再来一次吗？
    Display "Do you want to calculate another"
    Display "Commission? (Enter y for yes)"
    Input keepGoing
  While keepGoing == "y"
End Module

\ // showCommission 模块获取
  // 销售金额并显示
  // 佣金。
Module showCommission()
  // 局部变量
  Declare Real sales, commission

  // 佣金率的常量
  Constant Real COMMISSION_RATE = 0.10

  // 获取销售金额。
  Display "Enter the amount of sales"
  Input sales

  // 计算佣金。
  Set commission = sales * COMMISSION_RATE

  // 显示佣金
  Display "The commission is $", commission
End Module
```

该程序的输出与程序 5-1 相同。

## 5.2 条件控制循环：While, Do-While 和 Do-Until

**图 5-8** 程序 5-5 主模块的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_209_0.png)

虽然 `Do-While` 循环在某些情况下使用起来很方便，但它不是必须的。任何可以写成 `Do-While` 循环的循环也可以写成 `While` 循环。正如之前提到的，某些情况要求你在执行 `While` 循环之前初始化数据，以确保它至少执行一次。

## 焦点聚焦：设计一个 Do-While 循环

Samantha 拥有一进口业务，她使用以下公式计算产品的零售价：

Retail Price = Wholes Cost × 2.5

她要求你设计一个程序来执行此计算。她要求你设计一个程序来执行此计算。对于她收到的每一个产品，你决定使用循环来计算并显示零售价，然后，在第 10 行询问她是否还有另一个产品。该循环在她的表示还有另一个产品时会循环。程序 5-6 显示了该伪代码，图 5-9 显示了其流程图。

## 程序 5-6

```
Module main()
  // 局部变量
  Declare String keepGoing

  Do
    // 显示销售的佣金。
    Call showCommission()
    // 再来一次吗？
    Display "Do you want to calculate another"
    Display "Commission? (Enter y for yes)"
    Input keepGoing
  While keepGoing == "y"
End Module

\ // showCommission 模块获取
  // 销售金额并显示
  // 佣金。
Module showCommission()
  // 局部变量
  Declare Real sales, commission

  // 佣金率的常量
  Constant Real COMMISSION_RATE = 0.10

  // 获取销售金额。
  Display "Enter the amount of sales"
  Input sales

  // 计算佣金。
  Set commission = sales * COMMISSION_RATE

  // 显示佣金
  Display "The commission is $", commission
End Module
```

## 5.2 条件控制循环：While, Do-While 和 Do-Until

## 程序输出（加粗）

```
Enter the amount of sales.
10.00
The retail price is $25
Do you have another item? (Enter y for yes.)
y
Enter the amount of sales.
15.00
The retail price is $37.50
Do you have another item? (Enter y for yes.)
n
```

**图 5-9** 程序 5-6 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_211_0.png)

该程序有两个模块：程序运行时执行的 `main` 以及计算并显示零售价的 `showRetail`。在 `main` 模块中，`Do-While` 循环出现在第 5 行到第 12 行。在第 7 行，循环调用 `showRetail` 模块。然后，在第 10 行提示用户“还有另一个吗？”，在第 11 行将用户的输入存储在 `doAnother` 中。在第 12 行，以下语句是 `Do-While` 循环的结束：

注意我们正在使用 `OR` 运算符来测试复合布尔表达式。`OR` 左侧的表达式当 `doAnother` 等于小写 "y" 时为真。`OR` 右侧的表达式当 `doAnother` 等于大写 "Y" 时为真。如果这两个子表达式中的任何一个为真，循环就会迭代。这是使比较大小敏感的简单方法，这意味着用户输入大写或小写字母都可以。

```
While doAnother == "y" OR doAnother == "Y"
```

## Do-Until 循环

`While` 和 `Do-While` 循环都是在条件为真时迭代。然而，有时更方便编写一个直到条件为真才停止的循环——也就是说一个在条件为假时迭代的循环，当条件变为真时停止。

例如，考虑汽车工厂中的一台机器，它在汽车沿着生产线移动时喷漆。当没有更多汽车可以喷漆时，机器就会停止。如果你在为这样的机器编程，你会希望设计一个循环，直到生产线上没有更多汽车为止让机器喷漆。

直到条件为真的로循环被称为 `Do-Until` 循环。图 5-10 显示了 `Do-Until` 循环的通用逻辑。

