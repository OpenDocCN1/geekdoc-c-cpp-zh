
### 示例 6-17

```csharp
int total = 0;
for (int nValue = 0; nValue < 10; nValue++)
{
    if (nValue == 5)
    {
        break;
    }
    total += nValue;
    Console.Write(nValue + "\t");
}
Console.WriteLine("\nTotal is equal to {0}.", total);
```

此代码的输出为：

```
0    1    2    3    4
Total is equal to 10.
```

当条件表达式 `(nValue == 5)` 求值为 true 时，break 语句被执行，这会停止循环体。循环条件表达式 `(nValue < 10)` 不会再次被求值。语句 `Console.WriteLine("\nTotal is equal to {0}.", total);` 被执行。

![](img/e33ae760e23d89eac66541252ad65de8_366_0.png)

对于前面的示例，如果将条件表达式修改为 `(nValue < 5)`，你会得到相同的结果。

循环中使用的另一种无条件控制转移选项是 continue 语句，将在下一节中讨论。

## 继续语句

continue 语句与 break 一样，是一种跳转语句的形式。当遇到 continue 时，最接近的 while、do...while、for 或 foreach 语句的新迭代开始。从物理上讲，执行位置并不重要。它可能在循环体的顶部或底部。当 continue 被到达并执行时，该次迭代的循环体剩余部分不会被执行。continue 会立即将控制直接转移到条件表达式进行求值。

![](img/e33ae760e23d89eac66541252ad65de8_366_1.png)

对于 for 语句，转移回到下一迭代的顶部，这实际上会在条件表达式重新求值之前执行更新部分。

该语句的一般形式为：

```csharp
continue;
```

### 示例 6-18

示例 6-18 仅添加并打印奇数值。当条件表达式 `(nValue % 2 == 0)` 求值为 `true` 时，`continue` 语句被执行，这会导致循环体在该位置停止。循环中的剩余语句将被跳过，控制权转移回去更新 `nValue`。变量 `total` 不会被递增，且 `Console.Write(nValue)` 不会被执行 for that iteration through the loop。

```csharp
int total = 0;
for (int nValue = 0; nValue < 10; nValue++)
{
    if (nValue % 2 == 0)
    {
        continue;
    }
    total += nValue;
    Console.Write(nValue + "\t");
}
Console.WriteLine("\nTotal is equal to {0}.", total);
```

此代码的输出为：

```
1      3      5      7      9
Total is equal to 25.
```

请注意，`break` 和 `continue` 语句之间的区别在于，`continue` 语句不会停止循环体的执行，而是暂停该次迭代并将控制权转移到循环的下一次迭代。

C# 中的其他跳转语句是 `goto`、`throw` 和 `return`。你将在第 12 章异常处理中学习 `throw` 语句。你已在返回值的 方法中使用过 `return` 语句。`goto` 语句将控制权转移到由标签标记的语句。`goto` 语句名声不好。它与设计不良、难以调试和维护的意大利面条代码相关联。你不应在程序中使用 `goto` 跳转语句。

`break` 和 `continue` 语句也应谨慎使用。使用 `break` 语句与 `switch` 语句一起是适当且必要的。然而，当你在循环中使用 `break` 和 `continue` 语句时，你违反了开发循环的 **单一入口和单一出口** 准则。这意味着循环应该只有一个入口和一个出口。当从多个位置退出循环时，调试变得更加困难。循环可能因为条件求值为

![](img/e33ae760e23d89eac66541252ad65de8_369_0.png)

**图 6-16** LoanApplication 示例的问题规范

## 分析问题

你应查看图 6-16 中的问题规范，并确保理解问题定义。若干值被输入到程序中以表示贷款金额、利率和贷款期限。这些值作为 **string** 变量输入，然后被解析或转换为数值字段，以便进行计算。

需要开发两个独立的类。为 Loan 对象创建单独的类使该类能够被其他应用程序使用。该类包含生成摊销表的算法。它还包含一个独立的方法来确定贷款期限内的总利息支付。

## 数据

表 6-3 和 6-4 列出了 LoanApplication 问题所需的数据字段成员。

**表 6-3** Loan 类的实例字段成员

| 数据项描述 | 类型 | 标识符 |
| --- | --- | --- |
| 贷款金额 | double | loanAmount |
| 利率 | double | rate |
| 已支付总利息 | double | totalInterestPaid |
| 月付款金额 | double | paymentAmount |
| 贷款当前余额 | double | balance |
| 当前支付的本金金额 | double | principal |
| 付款次数 | int | numPayments |
| 当月利息 | double | monthInterest |

使用 Loan `class` 的客户端 `class` 将需要额外的数据。如问题规范所述，客户端或应用程序 `class` 允许用户输入贷款值。表 6-4 标识了应用程序 `class` 所需的一些局部变量。

**表 6-4** LoanApp 类的局部变量

| 数据项描述 | 类型 | 标识符 |
| --- | --- | --- |
| 贷款金额 | double | loanAmount |
| 利率 | double | interestRate |
| 融资贷款的年数 | int | years |
| 更多计算循环状态控制变量 | char | anotherLoan |

表 6-4 中的前三项将用于实例化 Loan `class` 的一个 `object`。在值输入并转换为数值后，将调用贷款构造函数来创建 Loan `object`。

### 常量

此应用程序未使用常量。

### 公式

需要公式来计算以下内容：

- `1. numPayments = years * 12`
- `2. term = (1 + rate / 12.0)^numPayments`
- `3. paymentAmount = loanAmount * rate / 12 * term / (term - 1.0)`
- `4. monthInterest = rate / 12 * balance`
- `5. principal = payment - monthInterest`
- `6. balance = balance - principal`
- `7. totalInterestPaid = totalInterestPaid + monthInterest`

## 设计解决方案

期望的输出是显示月付款金额、摊销表以及贷款期限内的总利息支付。图 6-17 显示了最终输出的原型。原型中放置了 xxx 以表示应出现计算值的位置。

![](img/e33ae760e23d89eac66541252ad65de8_371_0.png)

**图 6-17** Loan Application 示例的原型

面向对象的 方法专注于对象。贷款应用程序具有可以识别的数据和行为特征。类图用于帮助设计和记录这些特征。图 6-18 显示了 Loan Application 示例的类图。

![](img/e33ae760e23d89eac66541252ad65de8_372_0.png)

**图 6-18** 类图

**class** 图未显示特定方法可能需要的局部变量的属性。表 6-5 列出了将定义属性的数据成员，并指明是否需要 **get** 和/或 **set**。属性的名称也显示。

**表 6-5** Loan 类的属性

| 数据成员标识符 | 属性标识符 | Set | Get |
| --- | --- | --- | --- |
| paymentAmount | PaymentAmount |  | ✓ |
| loanAmount | LoanAmount | ✓ | ✓ |
| rate | Rate | ✓ | ✓ |
| numPayments (in months) | Years | ✓ | ✓ |
| totalInterestPaid | TotalInterestPaid |  | ✓ |

属性成员 PaymentAmount 和 TotalInterestPaid 设置为只读属性，因为它们是涉及不止单个数据成员的计算值。

