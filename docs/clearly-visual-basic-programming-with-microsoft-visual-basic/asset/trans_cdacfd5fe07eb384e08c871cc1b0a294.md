
### FWT 表 - 每周工资发放周期

**单身人士**

如果应税工资为：应预扣的所得税金额为

| 超过 | 但不超过 | 基础金额 | 百分比 | 超过以下金额的部分 |
| :--- | :--- | :--- | :--- | :--- |
|  | $ 51 | 0 |  |  |
| $ 51 | $ 198 | 0 | 10% | $ 51 |
| $ 198 | $ 653 | $ 14.70 加 | 15% | $ 198 |
| $ 653 | $1,533 | $ 82.95 加 | 25% | $ 653 |
| $1,533 | $3,202 | $ 302.95 加 | 28% | $1,533 |
| $3,202 | $6,916 | $ 770.27 加 | 33% | $3,202 |
| $6,916 |  | $1,995.89 加 | 35% | $6,916 |

**已婚人士**

如果应税工资为：应预扣的所得税金额为

| 超过 | 但不超过 | 基础金额 | 百分比 | 超过以下金额的部分 |
| :--- | :--- | :--- | :--- | :--- |
|  | $ 154 | 0 |  |  |
| $ 154 | $ 453 | 0 | 10% | $ 154 |
| $ 453 | $1,388 | $ 29.90 加 | 15% | $ 453 |
| $1,388 | $2,651 | $ 170.15 加 | 25% | $1,388 |
| $2,651 | $3,994 | $ 485.90 加 | 28% | $2,651 |
| $3,994 | $7,021 | $ 861.94 加 | 33% | $3,994 |
| $7,021 |  | $1,860.85 加 | 35% | $7,021 |

图17-26：每周联邦预扣税表

- a. 创建一个新的 Visual Basic Windows 应用程序。分别将解决方案、项目和窗体文件命名为 Harvey Industries Solution、Harvey Industries Project 和 frmMain.vb。将应用程序保存在 ClearlyVB\Chap17 文件夹中。如有必要，将窗体名称更改为 frmMain。

- b. 创建图17-27所示的界面，然后为应用程序编写代码。在代码中至少使用两个子过程：一个用于计算联邦预扣税，另一个用于清除总工资、FWT、FICA 和净工资框的内容。当 Hours、Rate 或 Allowances 文本框发生更改时，或单击其中一个单选按钮时，应清除这四个框。为 Hours、Rate 和 Allowances 文本框编写 KeyPress 事件过程。还要使用 Math.Round 方法，您已在第7章的高级练习8和9中学过。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_413_0.png)

图17-27：Harvey Industries 应用程序的用户界面

![](img/cf88270932e011575089da06b940a1d9_413_1.png)

- 10. 打开 FigureThisOut Solution（FigureThisOut Solution.sln）文件，该文件位于 ClearlyVB\Chap17\FigureThisOut Solution 文件夹中。打开代码编辑器窗口并研究现有代码。btnClear 控件的 Click 事件过程中的第一条语句将空字符串赋给 txtSales 控件的 Text 属性。正如您在本章所学，当文本框的内容发生更改时，文本框的 TextChanged 事件就会发生。在此情况下，TextChanged 事件过程调用 ClearLabels 过程来清除两个标签控件的内容。请注意，btnClear 控件的 Click 事件过程中的第二条语句也调用了 ClearLabels 过程；您的任务是确定第二条语句是否真的必要。在 btnClear 控件的 Click 事件过程中的 Call ClearLabels() 语句前插入一个单引号，使该语句成为注释。保存解决方案，然后启动并测试应用程序。为什么 btnClear 控件必须调用 ClearLabels 控件？停止应用程序。删除您插入的单引号。保存并关闭解决方案。

- 11. 在本练习中，您将找出应用程序代码中的一个错误。打开 SwatTheBugs Solution（SwatTheBugs Solution.sln）文件，该文件位于 ClearlyVB\Chap17\SwatTheBugs Solution 文件夹中。打开代码编辑器窗口并研究现有代码。启动并测试应用程序。请注意，应用程序未正常工作。停止应用程序。在代码中找出并更正任何错误。保存解决方案，然后再次启动并测试应用程序。停止应用程序，然后关闭解决方案。

### “试一试”练习答案

- 1. 参见图17-28。

```vb
    Public Class frmMain
        Private Sub CalcAndDisplayBonus(ByVal decTotal As Decimal)
            ' calculates and displays the bonus

            Dim decBonus As Decimal

            If decTotal > 1200 Then
                decBonus = decTotal * 0.1
            Else
                decBonus = decTotal * 0.08
            End If
            lblBonus.Text = decBonus.ToString("C2")
        End Sub

        Private Sub btnExit_Click ...

        Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles ...
            ' prompts the user to enter two sale amounts, then totals both amounts,
            ' and then calls a sub procedure to calculate and display the bonus

            Dim strInputSale1 As String
            Dim strInputSale2 As String
            Dim decSale1 As Decimal
            Dim decSale2 As Decimal
            Dim decSum As Decimal

            strInputSale1 = InputBox("First sale amount", "Bonus Solution")
            strInputSale2 = InputBox("Second sale amount", "Bonus Solution")

            Decimal.TryParse(strInputSale1, decSale1)
            Decimal.TryParse(strInputSale2, decSale2)
            decSum = decSale1 + decSale2
            Call CalcAndDisplayBonus(decSum)
        End Sub

    End Class
```

图17-28

- 2. 参见图17-29。

```vb
Public Class frmMain

    Private Sub CalcBonus(ByVal decS1 As Decimal, _
                          ByVal decS2 As Decimal, _
                          ByRef decBonusAmt As Decimal)
        ' calculates the bonus

        Dim decSum As Decimal

        decSum = decS1 + decS2
        If decSum > 1200 Then
            decBonusAmt = decSum * 0.1
        Else
            decBonusAmt = decSum * 0.08
        End If
        lblBonus.Text = decBonusAmt.ToString("C2")
    End Sub

    Private Sub btnExit_Click ...

    Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
        ' prompts the user to enter two sale amounts, then calls a
        ' sub procedure to calculate the bonus, then displays the bonus

        Dim strInputSale1 As String
        Dim strInputSale2 As String
        Dim decSale1 As Decimal
        Dim decSale2 As Decimal
        Dim decBonus As Decimal

        strInputSale1 = InputBox("First sale amount", "Bonus Solution")
        strInputSale2 = InputBox("Second sale amount", "Bonus Solution")

        Decimal.TryParse(strInputSale1, decSale1)
        Decimal.TryParse(strInputSale2, decSale2)
        Call CalcBonus(decSale1, decSale2, decBonus)
        lblBonus.Text = decBonus.ToString("C2")
    End Sub
End Class
```

**图17-29**

## 18 跟我聊聊

**学习第18章后，您应该能够：**

- 解释子过程和函数过程之间的区别
- 创建函数过程
- 调用函数过程

### 答案是什么？

除了创建子过程（您在第17章已学过）之外，您还可以创建函数过程。这两种过程之间的区别在于，**函数过程**在执行其指定任务后会返回一个值，而子过程不返回值。函数过程更简单地称为**函数**。图18-1显示了创建函数的语法。函数的头部和尾部与子过程的头部和尾部几乎相同，不同之处在于函数的头部和尾部包含的是 **Function** 关键字，而不是 **Sub** 关键字。与子过程头部不同的另一点是，函数的头部包含 As *数据类型* 部分。您使用头部的这一部分来指定函数返回的值的数据类型。如果函数返回字符串，则在头部末尾输入 As String；如果函数返回 Double 数字，则输入 As Double。与子过程一样，函数可以按*值*或按*引用*接收信息。它接收的信息列在头部的 *参数列表* 中。在函数的头部和尾部之间，输入您希望计算机在调用函数时处理的指令。在大多数情况下，函数内的最后一条语句是 Return *表达式*，其中 *表达式* 表示将返回给调用该函数的语句的唯一值。Return 语句中 *表达式* 的数据类型必须与头部 As *数据类型* 部分指定的数据类型一致。除了语法之外，图18-1还包含一个函数示例，以及在代码编辑器窗口中输入函数所遵循的步骤。与子过程一样，您可以将函数输入在第一个事件过程上方、最后一个事件过程下方，或调用它们的那个过程下方。在本书中，您将把函数输入在第一个事件过程上方。与子过程名称一样，函数名称使用 Pascal 大小写输入，并且通常以动词开头。名称应表明函数执行的任务。例如，对于返回新价格的函数，一个好的名称是 GetNewPrice。

### 创建函数过程

### 语法

函数过程头部

```vb
    Private Function procedureName([parameterList]) As dataType
        [one or more statements]
        Return expression
    End Function
```

函数过程尾部

**图18-1：**创建函数过程的语法、示例和步骤 *（续下页）*

