
# 嵌套循环

就像语句一样，循环语句也可以嵌套。你可以在 `while` 循环中放置 `while` 循环，在 `for` 循环中放置 `for` 循环，在 `for` 循环中放置 `while` 循环或任何组合。当循环嵌套时，每对循环包含一个内部循环和一个外部循环。内部循环必须完全包含在外部循环内部：循环不会重叠。图 5-14 显示了一个阴影循环嵌套在另一个循环中的图；阴影区域是内部循环以及外部循环的体。

假设你想在不同的利率下显示不同年份的银行余额。图 5-15 显示了一个包含由利率控制的外部循环（从图中第一个阴影语句开始）和由年份控制的内部循环（从第二个阴影语句开始）的应用程序。该程序显示在 4%、6% 和 8% 利率下，1000 美元在一到五年内的年复利。图 5-16 显示了输出。

## 使用嵌套循环

**图 5-14** 嵌套循环

```csharp
using static System.Console;
class LoopingBankBal2
{
    static void Main()
    {
        double bankBal;
        double rate;
        int year;
        const double START_BAL = 1000;
        const double START_INT = 0.04;
        const double INT_INCREASE = 0.02;
        const double LAST_INT = 0.08;
        const int END_YEAR = 5;
        for(rate = START_INT; rate <= LAST_INT; rate += INT_INCREASE)
        {
            bankBal = START_BAL;
            WriteLine("Starting bank balance is {0}",
                bankBal.ToString("C"));
            WriteLine("Interest Rate: {0}", rate.ToString("P"));
            for(year = 1; year <= END_YEAR; ++year)
            {
                bankBal = bankBal + bankBal * rate;
                WriteLine("After year {0}, bank balance is {1}",
                    year, bankBal.ToString("C"));
            }
        }
    }
}
```

**图 5-15** LoopingBankBal2 程序

## 第5章 循环

**图 5-16** LoopingBankBal 程序的输出

当你在循环内部嵌套循环时，应该始终将外层循环考虑为包含性循环。在描述任务时，对内层循环使用“每个”（each）一词。例如，如果你想在 10 年内每年输出不同利率下的余额，你可以按照如下所示的方式适当地初始化某些常量：

```csharp
const double RATE1 = 0.03;
const double RATE2 = 0.07;
const double RATE_INCREASE = 0.01;
const int END_YEAR = 10;
```

然后你可以使用以下嵌套的 `for` 循环：

```csharp
for(rate = RATE1; rate += RATE_INCREASE)
for(year = 1; year < END_YEAR; ++year)
  WriteLine(bankBal + bankBal * rate);
```

然而，如果你想显示每个利率下不同年份的余额，将使用以下代码：

```csharp
for(year = 1; year <= END_YEAR; ++year)
for(rate = RATE1; rate <= RATE2; rate += RATE_INCREASE)
  WriteLine(bankBal + bankBal * rate);
```

在这两种情况下，显示的都是相同的 50 个值——5 种不同的利率（从 0.03 到 0.07）对应 10 年（1 到 10）。但是，在第一个例子中，第 1 年到第 10 年的将在每个利率内部显示；而在第二个例子中，每个利率的每个余额将在每个年份分类内显示。换句话说，在第一个例子中，显示的前 10 个金额将全部使用 0.03 的初始利率持续 10 年；而在第二个例子中，显示的前 5 个金额将在第一年使用不同的利率值。

## 使用嵌套循环

观看视频“使用嵌套循环”（Using Nested Loops）。

# 两个真，一假

## 使用嵌套循环

- 1. 以下循环的体执行了六次：

  ```csharp
  for(a = 1; a < 4; ++a)
  for(b = 2; b < 3; ++b)
  ```

- 2. 下一个循环的体执行了四次：

  ```csharp
  for(c = 1; c < 3; ++c)
  for(d = 1; d < 3; ++d)
  ```

- 3. 下一个循环的体执行了 15 次：

  ```csharp
  for(e = 1; e <= 5; ++e)
  for(f = 2; f <= 4; ++f)
  ```

内层循环 1、2 和 3 在当内层循环在每个循环中仅执行一次时才会执行。外层循环只执行了三次。错误的陈述是 #1。该循环执行了 # 次。

## 你来做

### 使用嵌套循环

在接下来的步骤中，你将编写一个程序创建一个小费表，餐厅顾客可以使用它可以估算餐费的小费。价格范围从 $10 到 $100 不等，小费百分率范围从 10% 到 25%。该程序使用了几个循环。

- 1. 打开一个新文件开始创建一个名为 `TippingTable` 的程序。首先声明用于晚餐价格、小费百分率率和小费金额的变量。

（继续）

## 第5章 循环

（继续）

- 2. 接下来，创建一些常量。从 10% 到 25% 的每个小费将以 5% 为间隔进行计算，因此将这些值声明为 `LOWRATE`、`MAXRATE` 和 `TIPSTEP`。小费将针对最高 $100.00 的晚餐价格以每 $10.00 为间隔进行计算，因此也声明这些常量。

```csharp
const double LOWRATE = 0.10;
const double MAXRATE = 0.25;
const double TIPSTEP = 0.05;
const double MAXDINNER = 100.00;
const double DINNERSTEP = 10.00;
```

- 3. 创建表格表头。（为了对齐，在 Price 之后插入三个空格。）在同一行，使用一个循环以 `TIPSTEP` 为增量显示通过 `MAXRATE` 的每个利率。换句话说，小费率为 0.10、0.15、0.20 和 0.25。使用 `Write()` 语句将光标移动到下一行，使用 `WriteLine()` 语句显示虚线。

```csharp
Write("Price");
for(tipRate = LOWRATE; tipRate <= MAXRATE; tipRate += TIPSTEP)
  Write("{0,8}", tipRate.ToString("F"));
WriteLine("--------------------------------------");
```

> **注意**：`for` 循环中，第一个分号执行一次，循环体执行，然后第二个分号右边的表达式执行。换句话说，`TIPSTEP` 会加到 `tipRate` 上，直到 `tipRate` 在循环中显示。

> **提示**：作为在 `Write()` 语句中输入 40 个虚线的替代方案，可以使用循环显示 40 次虚线。当完成 40 个虚线后，可以使用 `Write()` 将光标移动到下一行。

```csharp
int NUM_DASHES = 40;
for(int x = 0; x < NUM_DASHES; ++x)
  Write("-");
WriteLine();
```

- 4. 将 `tipRate` 重置为 0.10。在最后一个循环之后，速率将大于 0.25。

```csharp
tipRate = LOWRATE;
```

- 5. 创建一个嵌套循环，当 `dinnerPrice` 小于 100.00 (`MAXDINNER`) 时继续。该循环的每次迭代显示表格的一行。在这个循环内部，显示 `dinnerPrice`，然后使用循环显示 `tipRate` 从 0.10 变化到 0.25。在循环结束时，将 `dinnerPrice` 增加 10.00，将 `tipRate` 重置为 0.10 以准备下一行，并写入一个新行以移动光标。

```csharp
while(dinnerPrice <= MAXDINNER)
{
    Write("{0,8}", dinnerPrice.ToString("C"));
    while(tipRate <= MAXRATE)
    {
        tip = dinnerPrice * tipRate;
        Write("{0,8}", tipRate.ToString("F"));
        tipRate += TIPSTEP;
    }
    dinnerPrice += DINNERSTEP;
    tipRate = LOWRATE;
    WriteLine();
}
```

> **注意**：`Write()` 语句中的 `{0, 8}` 格式字符串将第一个参数显示在 8 个字符的字段中。你在第 2 章学过格式字符串。

- 6. 添加两个大括号——一个用于 `Main()` 方法，一个用于类。

- 7. 保存文件、编译并执行程序。输出如图 5-17 所示。

| Price | 0.10 | 0.15 | 0.20 | 0.25 |
| :--- | :--- | :--- | :--- | :--- |
| $10.00 | 1.00 | 1.50 | 2.00 | 2.50 |
| $20.00 | 2.00 | 3.00 | 4.00 | 5.00 |
| $30.00 | 3.00 | 4.50 | 6.00 | 7.50 |
| $40.00 | 4.00 | 6.00 | 8.00 | 10.00 |
| $50.00 | 5.00 | 7.50 | 10.00 | 12.50 |
| $60.00 | 6.00 | 9.00 | 12.00 | 15.00 |
| $70.00 | 7.00 | 10.50 | 14.00 | 17.50 |
| $80.00 | 8.00 | 12.00 | 16.00 | 20.00 |
| $90.00 | 9.00 | 13.50 | 18.00 | 22.50 |
| $100.00 | 10.00 | 15.00 | 20.00 | 25.00 |

```text
C:\Chapter.05>TippingTable
```

**图 5-17** TippingTable 程序的输出

（继续）

在本章末尾的练习中，你将被要求制作一个 `TTable` 程序的交互版本，其中许多值将由用户输入，而不是作为未命名常量编码在程序中。

## 你来做

### 使用 do 循环

在接下来的步骤中，修改 Tipping 程序以用 `do` 循环代替 `while` 循环。

- 1. 打开 Tipping 程序，将类名更改为 `Tipping2` 并将文件保存为 `Tipping2`。
- 2. 剪切 `while` 循环语句 (`while(dinnerPrice <= MAXDINNER)`)，将其替换为 `do`。
- 3. 将 `while` 循环语句粘贴到循环结束的大括号之后、程序最后的两个大括号之前，然后添加一个分号。
- 4. 保存、编译并执行程序。输出与图 5-17 相同。

### 累加总和

许多计算机程序显示总和。当你收到信用卡或电话服务账单时，通常会提供个人交易详情，但你最感兴趣的是总金额。同样，某些程序会汇总学生的学分、公司所有员工的总工资或组织的应收账款总值。这些总和是累加的——也就是说，它们在循环中逐个汇总。

图 5-18 显示累加用户总量的交互程序示例。程序提示用户输入价格或按 O 。当循环继续输入非零值时，金额会被加到总和中。每次循环，总和都会重新计算以包含新的购买金额。在用户输入终止循环的 O 后，可以显示累加的总和。图 5-19 显示了典型的执行过程。

**图 5-18** 一个累加用户总购买金额的应用程序

```csharp
using System;
using static System.Console;
class TotalPurchase
{
    static void Main()
    {
      double purchase;
      double total = 0;
      string inputString;
      const double QUIT = 0;
      Write("Enter purchase amount >> ");
    }
}
```

**图 5-19** TotalPurchase 程序的典型执行过程

```text
C:\#Chapter.05>TotalPurchase
Enter purchase amount >> 5:10
Enter next purchase amount, or to quit >> 12.87
Enter next purchase amount, or to quit >> 100.00
Enter next purchase amount, or to quit >> 0
Your total is $112.87
C:\#Chapter.05>_
```

回想第 2 章的内容，表达式 `total += purchase` 使用了复合加法赋值运算符，它等同于 `total = total + purchase`。在维护运行总和时，经常使用加法赋值运算符。

在图 5-18 的应用程序中，在循环开始之前将用于累加的 `total` 变量设为 0 是非常重要的。如果不这样做，程序将无法编译。未知的、未赋值的值被称为“垃圾值”。C# 编译器通过要求你提供一个初始值来防止你看到错误的总和：C# 不会恰好存储在未初始化内存位置的垃圾值。

## 第5章 循环

在图 5-18 的应用程序中，`total` 变量必须初始化为 0，但 `purchase` 变量是未初始化的。许多程序员会认为初始化这个变量是没有意义的，因为无论你提供什么值，在变量被使用之前，第一条输入语句就会改变它的值。从风格的角度来看，如果初始化从未被使用，本书通常不会对变量进行初始化；这样做可能会误导你，认为该变量具有某种用途。

## 两个真理一假

### 累加总和

- 1. 当累加总和时，会将 1 加到代表总和的变量上。
- 2. 用于保存总和的变量在用于累加总和之前必须设为 0。
- 3. C# 编译器不允许在未初始化的变量中累加总和。

当累加总和时，并不是在循环中累加一个总和，而是每个循环增加一个分数。如果你每个循环只给总和变量加 1，那么该变量代表总和。例如，如果你有 10 个测试分数，那么错误的语句是 #1。当累加总和时，可能会加上任何值。

## 提高循环性能

无论你决定在应用程序中使用 `while`、`for` 还是其他循环，你都可以通过以下方法提高循环性能：

- 确保循环避免不必要的操作。
- 考虑短路运算符的求值顺序。
- 采用循环合并（loop fusion）。
- 使用前置递增而不是后置递增。

### 避免不必要的操作

可以通过让循环不包含不必要的操作或语句来提高循环性能。例如，假设循环在 `x` 小于两个整数 `a` 和 `b` 之和时执行，且循环体中没有修改 `a` 或 `b`。可以写为：

```csharp
while(x < a + b)
  // 循环体
```

如果这个循环执行 1,000 次，那么表达式 `a + b` 就会被计算 1,000 次。相反，如果你使用以下代码，结果是相同的，但算术只执行一次：

```csharp
int sum = a + b;
while(x < sum)
  // 循环体
```

当然，如果 `a` 或 `b` 在循环中发生了变化，那么必须在循环中重新计算。然而，如果在循环开始前固定 `a` 和 `b` 的和，效率会更高。例如，假设在循环中使用一个临时变量来存储 `a + b` 的和，这样可以写为：

```csharp
int sum = a + b;
while(x < sum)
  // 循环体
```

由于变量在循环开始前就停止了，这种方式效率更高。在循环中声明 `tempTotal` 如下：

```csharp
while(x < a + b)
  // 循环体
```

如果这个循环执行 1,000 次，那么表达式 `a + b` 就会被计算 1,000 次。相反，如果你使用以下代码，结果是相同的，但算术只执行一次：

```csharp
int sum = a + b;
while(x < sum)
  // 循环体
```

当然，如果 `a` 或 `b` 在循环中发生了变化，那么必须在循环中重新计算。然而，如果在循环开始前固定 `a` 和 `b` 的和，效率会更高。例如，在循环中使用一个临时变量来存储 `a + b` 的和，这样可以写为：

```csharp
int sum = a + b;
while(x < sum)
  // 循环体
```
