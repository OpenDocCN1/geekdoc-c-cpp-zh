

### 图 4-9：FinancialPlanner 中 while 循环的流程图

![](img/143bad48262566137acc9c41f668a88f_144_0.png)

步骤 2-1：从 Tutorial_Starts 文件夹中的项目 Ch4_Loops 打开名为 FinancialPlanner 的窗体，如图 4-8 所示。窗体具有以下控件：

- 三个 TextBoxes：txtInvestment、txtGrowthRate 和 txtTargetAmt
- 三个 Labels
- 一个按钮：btnHowLong
- 一个 ListBox：lstDisplay

完整代码如图所示 4-10。

程序的前三个部分由以下子任务组成：

- 从 TextBoxes 获取输入数据。
- 打印标题。
- 将年份和投资价值设为零。

### 图 4-10：FinancialPlanner 窗体的代码

```csharp
20    private void btnHowLong_Click(object sender, EventArgs e)
21    {
22        // Get input data from TextBoxes:
23        double yearlyInvestment = double.Parse(txtInvestment.Text);
24        float YearlyGrowthPercent = float.Parse(txtGrowthRate.Text);
25        double targetAmt = double.Parse(txtTargetAmt.Text);
26
27        // Print heading
28        string formatCode = "{0,7}{1,20}";
29        lstDisplay.Items.Add(string.Format(formatCode, "years", "Investment Value"));
30
31        lstDisplay.Items.Add("");
32
33        // Set year and investment value to zero
34        int year = 0;
35        double investmentValue = 0;
36
37        // Use while loop to compute investment value for each year
38        while (investmentValue < targetAmt)
39        {
40            year = year + 1;    // Increment year by one
41            investmentValue = (investmentValue + yearlyInvestment) *
42                            (1+ YearlyGrowthPercent/100);
43            lstDisplay.Items.Add(string.Format(formatCode, year,
44                                investmentValue.ToString("C")));
45        }
```

让我们关注使用 while 循环的代码的第四部分。

while 语句会评估布尔表达式 (investmentValue < targetAmt)。如果为真，则 while 子句中的语句会被处理以递增年份并计算投资价值；如果不为真，则控制权会传递给循环之后的语句（方法末尾的右括号）。

第一次处理 while 语句时，investmentValue 为零，布尔表达式 (0 < 500000) 为真。因此，while 子句中的语句会被处理以执行以下操作：

- 将年份递增到 1，
- 使用第 41 行中的表达式计算第 1 年的投资价值，其值为 10,700，并且
- 显示年份和投资价值。

计算投资价值的公式将在后面讨论。

正如图 4-9 中的流程图所示，在处理完 while 子句中的最后一个语句后，控制会自动传递到循环的开头，在那里使用第一次迭代中计算的 investmentValue (10,700) 评估布尔表达式，以开始第二次迭代。

在第二次迭代中，布尔表达式 (10700 < 500000) 为真。因此，while 子句中的语句第二次被处理以将年份递增到 2，计算新的投资价值 (22,149) 并显示它。

## 预测试循环

while 循环有一个在循环开始时检查的布尔表达式。因此，while 循环被称为预测试循环。因为它是预测试循环，如果在第一次迭代中布尔表达式为假，则循环中的语句甚至一次也不会被处理。例如，如果 investValue 初始化为大于 500,000 的值，则循环中的语句将不会被处理。

步骤 2-5：将 investmentValue 的初始值（第 35 行）更改为 501,000。运行窗体。注意 ListBox 中没有输出显示，表明循环中的语句未被执行。

是时候练习了！完成练习 4-1 和 4-2。

## 复习问题

4.1 修正以下程序中的错误（如果有），该程序旨在计算如果每年存入 $750 且没有利息的情况下 4 年的总储蓄。

```csharp
int yearlyDeposit = 750;
int totalSavings = 0;
while (year < 4)
{
    int year = 0;
    year = year + 1;
    totalSavings = totalSavings + yearlyDeposit;
}
```

4.2 以下程序的输出会是什么？（特别注意循环内部的语句。）

```csharp
int yearlyDeposit = 750;
int totalSavings = 0;
int year = 0;
while (year < 3)
{
    year = year + 1;
    totalSavings = yearlyDeposit;
}
lstOutput.Items.Add(totalSavings);
```

4.3 以下程序的输出会是什么？

```csharp
int year = 2016;
int population = 75000;
while (population < 77000)
{
    year = year + 1;
    population = population + 1000;
    lstOutput.Items.Add(year + " " + population.ToString());
}
```

4.4 以下程序中的循环会被执行多少次？

```csharp
int year = 3;
while (year < 3)
{
    year = year + 1;
}
```

### 图 4-14：for 循环的流程图

![](img/143bad48262566137acc9c41f668a88f_153_0.png)

## 教程 3：for 循环：财务规划应用程序

让我们构建使用 for 循环计算固定年数投资价值的 FinPlannerForLoop 窗体。

步骤 3-1：从项目 Ch4_Loops 打开名为 FinPlannerForLoop 的窗体。添加图 4-13 中第 37-44 行的代码以创建 for 循环。

步骤 3-2：在循环头部以及开始和结束大括号处设置断点。运行窗体，并观察第一次通过循环时 year 的值以及它在第一次迭代结束和第二次迭代开始之间如何变化。

步骤 3-3：为帮助理解循环的终止，将第 42 行和第 43 行中显示输出的语句复制到循环的右大括号之后的行，如图 4-15 所示。运行窗体。当 year 的值变为 23 时，循环的处理终止，因为布尔表达式 (year<= numberOfYears) 为假。因此，第 23 年的 investmentValue 未被计算，它与第 22 年的值相同，如以下输出所示：

| Years | Investment Value |
| --- | --- |
| 21 | $480,057.39 |
| 22 | $524,361.41 |
| 23 | $524,361.41 |

变量 year 在循环外部可用，因为它是在循环外部声明的。

### 在循环内部声明计数器变量

步骤 3-4：按如下方式修改循环的头部以在头部内声明计数器变量：

```csharp
// int year;
for (int year = 1; year <= numberOfYears; year = year + 1)
```

运行窗体。

错误！程序无法运行，因为变量 year 在循环内部声明，但在第 45 行用于在循环外部显示其值。

删除使用变量 year 在循环外部显示值的第 45 行和第 46 行的语句。错误消失了。

再次，变量的作用域如果在循环内部声明，则仅限于循环。

### 按非 1 的值递增计数器

步骤 3-5：按如下方式修改头部以在每次迭代中将 year 递增 5：

```csharp
for (int year = 1; year <= numberOfYears; year = year + 5)
```

运行窗体。注意 year 的值如何变化。

警告！除第一年外，计算的投资价值都是不正确的，因为公式假设每年递增。

| years | Investment Value |
| --- | --- |
| 1 | $10,700.00 |
| 6 | $22,149.00 |
| 11 | $34,399.43 |
| 16 | $47,507.39 |
| 21 | $61,532.91 |

### 递减计数器变量

步骤 3-6：按如下方式更改循环的头部以递减计数器变量：

```csharp
for (int year = 5; year >= 1; year = year - 1)
```

运行窗体。year 的值从 5 变到 1，如下所示：

| years | Investment Value |
| --- | --- |
| 5 | $10,700.00 |
| 4 | $22,149.00 |
| 3 | $34,399.43 |
| 2 | $47,507.39 |
| 1 | $61,532.91 |

## 复习问题

4.6 以下程序的输出会是什么？

```csharp
int population = 65000;
for (int year = 2016; year <= 2018; year = year + 1)
{
    population = population + 1000;
    lstOutput.Items.Add(year + " " + population.ToString());
}
```

4.7 以下程序的输出会是什么？

```csharp
int population = 65000;
for (int yr = 2018; yr > 2016; yr = yr - 1)
{
    population = population - 1000;
    lstDisplay.Items.Add(yr + " " + population.ToString());
}
```

## 4.6 break 和 continue 语句

break 和 continue 语句让你偏离循环的正常处理。

### break 语句

你可以使用 break 语句跳出循环。

步骤 3-7：按图 4-16 所示修改代码，通过添加 if 语句和 break 语句，如果 investmentValue 超过 100,000，则跳出循环。将第 42 行的显示语句复制到第 47 行，如图所示，并确保 year 在循环外部声明。

