
- 3. 保存解决方案，然后启动应用程序。在 **数字 1** 文本框中输入 **22**，在 **数字 2** 文本框中输入 **12**，然后单击 **计算** 按钮。btnCalc 控件的 Click 事件过程将这两个整数相加，并在 **答案** 标签中显示和（34）。
- 4. 单击 **减法** 复选框，然后单击 **计算** 按钮。btnCalc 控件的 Click 事件过程从较大的整数（22）中减去较小的整数（12），然后在 **答案** 标签中显示差（10）。
- 5. 将 **数字 1** 文本框的内容改为 **5**，然后单击 **计算** 按钮。btnCalc 控件的 Click 事件过程交换文本框中的值。然后从较大的整数（12）中减去较小的整数（5），并在 **答案** 标签中显示差（7）。见图 10-13。

![](img/cf88270932e011575089da06b940a1d9_224_0.png)

**图 10-13：** 显示值已交换的界面

- 6. 单击 **退出** 按钮。关闭 **代码编辑器** 窗口，然后关闭解决方案。

## 这对我来说逻辑性太强了

在第 9 章中，你学习了如何在 If...Then...Else 语句的条件中包含比较运算符。你也可以在条件中包含逻辑运算符。**逻辑运算符**（有时称为 **布尔运算符**）允许你将两个或更多条件组合成一个复合条件。图 10-14 列出了 Visual Basic 中可用的两个逻辑运算符及其优先级顺序。该图还包含在 If...Then...Else 语句的条件中使用逻辑运算符的示例。与包含比较运算符的表达式一样，包含逻辑运算符的表达式始终求值为布尔值。请记住，在表达式中，逻辑运算符始终在任何比较运算符之后求值。

| 运算符 | 运算 | 优先级编号 |
| --- | --- | --- |
| AndAlso | 复合条件中的所有条件都必须为 True，复合条件才为 True | 1 |
| OrElse | 只需其中一个条件为 True，复合条件即为 True | 2 |

### 示例 1

```vb
    If intPopulation > 25000 AndAlso intPopulation <= 50000 Then
```

当 intPopulation 变量包含大于 25000 但小于或等于 50000 的数时，复合条件求值为 True；否则，求值为 False。

### 示例 2

```vb
    If chkBonus.Checked = True AndAlso decSales > 50000 Then
```

当 chkBonus 控件被选中，并且同时 decSales 变量包含大于 50000 的值时，复合条件求值为 True；否则，求值为 False。

### 示例 3

```vb
    If intPayCode = 1 OrElse intPayCode = 2 Then
```

当 intPayCode 变量包含数字 1 或数字 2 时，复合条件求值为 True；否则，求值为 False。

### 示例 4

```vb
    If intRating = 5 OrElse decSales <= 2500 Then
```

当 intRating 变量包含数字 5，或者 decSales 变量包含小于或等于 2500 的值时，复合条件求值为 True；否则，求值为 False。

**图 10-14：** 逻辑运算符的列表和示例

到目前为止，在本书中，你已经学习了算术运算符（第 6 章）、比较运算符（第 9 章）和逻辑运算符。如果一个表达式包含逻辑运算符、比较运算符和算术运算符，则先计算算术运算符，然后计算比较运算符，最后计算逻辑运算符。因此，当计算机处理表达式 12 > 0 AndAlso 12 < 10 * 2 时，它会先计算算术运算符（*），然后计算两个比较运算符（> 和 <），最后计算逻辑运算符（AndAlso）。该表达式的求值结果为 True，如图 10-15 所示。

| 求值步骤 | 结果 |
| --- | --- |
| 原始表达式 | `12 > 0 AndAlso 12 < 10 * 2` |
| 先计算 10 * 2 | `12 > 0 AndAlso 12 < 20` |
| 接着计算 12 > 0 | `True AndAlso 12 < 20` |
| 然后计算 12 < 20 | `True AndAlso True` |
| 最后计算 True AndAlso True | `True` |

**图 10-15：** 包含算术、比较和逻辑运算符的表达式的求值步骤

研究图 10-16 所示的问题说明和算法。算法中的选择结构对员工的工作时长做出判断。更具体地说，它判断工作时长是否在可接受范围内。在本例中，可接受范围是大于或等于 0 但小于或等于 40。现在，将算法中的选择结构与图 10-17 所示的代码进行比较。请注意，“如果工作时长大于或等于 0 但小于或等于 40，则执行以下操作：”这一行在 Visual Basic 中编码为 `If decHours >= 0 AndAlso decHours <= 40 Then`。

![](img/cf88270932e011575089da06b940a1d9_226_0.png)

**图 10-16：** 总工资问题的说明和算法

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates and displays a gross pay amount

    Dim decHours As Decimal
    Dim decGross As Decimal

    ' calculate and display gross pay, or display an error message
    Decimal.TryParse(txtHours.Text, decHours)
    If decHours >= 0 AndAlso decHours <= 40 Then
        decGross = decHours * 8.35
        lblGross.Text = decGross.ToString("C2")
    Else
        lblGross.Text = "Incorrect hours"
    End If
End Sub
```

选择结构

**图 10-17：** 与图 10-16 的算法对应的代码

### 完成 Gross Pay 应用程序的代码：

- 1. 打开 **Gross Pay 解决方案（Gross Pay Solution.sln）** 文件，该文件位于 ClearlyVB\Chap10\Gross Pay Solution 文件夹中。如有必要，打开设计器窗口。
- 2. 打开 **代码编辑器** 窗口，其中包含 **btnExit** 控件的 Click 事件过程的代码。在部分完成的 **btnCalc** 控件的 Click 事件过程中，输入图 10-17 所示的选择结构。
- 3. 保存解决方案，然后启动应用程序。在 **工作时长** 文本框中输入 **20**，然后单击 **计算** 按钮。由于工作时长在可接受范围内，**btnCalc** 控件的 Click 事件过程计算总工资，并在 **总工资** 标签中显示结果（$167.00）。
- 4. 在 **工作时长** 文本框中输入 **45**，然后单击 **计算** 按钮。在这种情况下，工作时长不在可接受范围内，因此 **btnCalc** 控件的 Click 事件过程会在 **总工资** 标签中显示“Incorrect hours”消息。见图 10-18。

![](img/cf88270932e011575089da06b940a1d9_227_0.png)

**图 10-18：** 界面中显示的错误消息

- 5. 单击 **退出** 按钮。关闭 **代码编辑器** 窗口，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_228_0.png)

有关逻辑运算符的更多示例，请参阅 Ch10WantMore.pdf 文件中的“逻辑运算符”部分。

## 小测验 2

- 1. 下列哪个条件用于判断 intQuantity 变量包含的数是否小于 0 或大于 1000？
  - a. intQuantity < 0 AndAlso intQuantity > 1000
  - b. intQuantity < 0 OrElse intQuantity > 1000
  - c. intQuantity < 0 AndAlso > 1000
  - d. intQuantity < 0 OrElse > 1000
- 2. 下列哪个条件用于判断 decPrice 变量包含的数是否大于 15.45 但小于 25.75？
  - a. decPrice < 15.45 AndAlso decPrice < 25.75
  - b. decPrice > 15.45 OrElse < 25.75
  - c. decPrice > 15.45 AndAlso decPrice < 25.75
  - d. decPrice > 15.45 OrElse decPrice < 25.75
- 3. 下列哪个条件用于判断两个复选框是否都被选中？
  - a. chkDiscount.Checked = True AndAlso chkCoupon.Checked = True
  - b. chkDiscount.Checked = True OrElse chkCoupon.Checked = True
  - c. chkDiscount.Selected = True AndAlso chkCoupon.Selected = True
  - d. chkDiscount.Selected = True OrElse chkCoupon.Selected = True
- 4. 表达式 6 + 3 > 7 AndAlso 8 < 4 的求值结果为 ________。
  - a. True
  - b. False

![](img/cf88270932e011575089da06b940a1d9_228_1.png)

现在该观看 Ch10-Nested Selection Structure 视频了。
