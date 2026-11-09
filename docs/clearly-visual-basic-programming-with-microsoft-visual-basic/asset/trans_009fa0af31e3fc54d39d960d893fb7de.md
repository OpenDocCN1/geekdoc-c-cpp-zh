
## 下一个要处理的 Case 是什么？

If...Then...Else 语句并不是在 Visual Basic 中编写多路径选择结构时可以使用的唯一语句；你还可以使用 **Select Case 语句**。图 11-7 显示了 Select Case 语句的语法。它还显示了如何使用该语句编写一个多路径选择结构，该结构显示与字母等级对应的消息。Select Case 语句以关键字 Select Case 开头，后面跟一个 *selectorExpression*。*selectorExpression* 可以包含变量、常量、方法、运算符或属性的任意组合。在图 11-7 的示例中，*selectorExpression* 是一个名为 strGrade 的 String 变量。Select Case 语句以 End Select 子句结束。在 Select Case 和 End Select 子句之间是各个 Case 子句。每个 Case 子句表示计算机可以遵循的一条不同路径。通常要缩进每个 Case 子句以及每个 Case 子句中的指令，如图所示。在 Select Case 语句中，可以根据需要拥有任意多个 Case 子句。但是，如果 Select Case 语句包含 Case Else 子句，则 Case Else 子句必须是该语句中的最后一个子句。除 Case Else 子句外，每个单独的 Case 子句都必须包含一个 *expressionList*，其中可以包括一个或多个表达式。要在 *expressionList* 中包含多个表达式，请用逗号分隔每个表达式，如 *expressionList* Case "D", "F" 中那样。*selectorExpression* 只需匹配 *expressionList* 中列出的一个表达式。表达式的数据类型必须与 *selectorExpression* 的数据类型兼容。如果 *selectorExpression* 是数值型，则 Case 子句中的表达式应为数值型。同样，如果 *selectorExpression* 是字符串，则表达式应为字符串。在图 11-7 的示例中，*selectorExpression*（strGrade）是字符串，表达式 "A"、"B"、"C"、"D" 和 "F" 也是字符串。

```vb
SELECT CASE STATEMENT
Syntax

Select Case selectorExpression
    Case expressionList1
        instructions for the first Case
    [Case expressionList2
        instructions for the second Case]
    [Case expressionListN
        instructions for the Nth case]
    [Case Else
        instructions for when the selectorExpression does not match any of the expressionLists]
End Select

Example

Dim strGrade As String = txtGrade.Text.ToUpper
Select Case strGrade
    Case "A"
        lblMsg.Text = "Excellent"
    Case "B"
        lblMsg.Text = "Above Average"
    Case "C"
        lblMsg.Text = "Average"
    Case "D", "F"
        lblMsg.Text = "Below Average"
    Case Else
        lblMsg.Text = "Error"
End Select
```

图 11-7：Select Case 语句的语法和示例

在处理 Select Case 语句时，计算机首先将 *selectorExpression* 的值与 *expressionList1* 中列出的值进行比较。如果找到匹配项，计算机将处理第一个 Case 的指令，直到遇到另一个 Case 子句或 End Select 子句时停止；然后跳到 End Select 子句之后的指令。如果在 *expressionList1* 中未找到匹配项，计算机跳到第二个 Case 子句，在那里将 *selectorExpression* 与 *expressionList2* 中列出的值进行比较。如果找到匹配项，计算机处理第二个 Case 子句的指令，然后跳到 End Select 子句之后的指令。如果未找到匹配项，计算机跳到第三个 Case 子句，依此类推。如果 *selectorExpression* 不匹配任何 *expressionList* 中列出的任何值，计算机处理 Case Else 子句中列出的指令（如果有），然后跳到 End Select 子句之后的指令。请记住，如果 *selectorExpression* 匹配多个 Case 子句中的值，则只处理第一个匹配项中的指令。

### 使用 Select Case 语句编写 Fitness For Good 应用程序：

- 1. 打开 **Fitness Solution (Fitness Solution.sln)** 文件，该文件位于 ClearlyVB\Chap11\Fitness Solution-Select Case 文件夹中。如有必要，打开设计器窗口。应用程序的界面（前面图 11-4 中所示）会出现在屏幕上。

- 2. 打开代码编辑器窗口。在 btnDisplay 控件的 Click 事件过程中，输入图 11-8 所示的 Select Case 语句。

![](img/cf88270932e011575089da06b940a1d9_247_0.png)

```vb
' assign code to a variable
strCode = txtCode.Text.ToUpper

' determine fee
Select Case strCode
    Case "S"
        intFee = intSINGLE
    Case "F"
        intFee = intFAMILY
    Case "S&S"
        intFee = intSINGLE_SENIOR
    Case "C&S"
        intFee = intCOUPLE_SENIOR
End Select

' display fee
lblFee.Text = intFee.ToString("C0")
```

**图 11-8：** 在 btnDisplay 控件的 Click 事件过程中输入的 Select Case 语句

- 3. 保存解决方案，然后启动应用程序。

- 4. 输入 **f** 作为代码，然后单击 **显示费用** 按钮。按钮 Click 事件过程中的 strCode = txtCode.Text.ToUpper 语句将大写字母 F 赋给 strCode 变量。接下来处理 Select Case 语句。处理该语句时，计算机首先将 strCode 变量的内容（F）与第一个 Case 子句的 *expressionList*：“S”进行比较。F 不等于 S，因此计算机跳到第二个 Case 子句，在那里将 strCode 变量的内容（F）与字符串“F”进行比较。F 等于 F，因此计算机处理第二个 Case 子句中的 intFee = intFAMILY 赋值语句。然后跳到 End Select 子句之后的指令。

### ABC 公司价格表

| 订购物品数量 | 每件价格 |
|---|---|
| 1-5 | $25 |
| 6-10 | $23 |
| 超过 10 | $20 |

Example

```vb
Select Case intNumOrdered
  Case 1 To 5
    intPrice = 25
  Case 6 To 10
    intPrice = 23
  Case Is > 10
    intPrice = 20
  Case Else
    intPrice = 0
End Select
```

图 11-9：在 Select Case 语句中使用 To 和 Is 关键字的示例

**编写 ABC 公司应用程序，然后测试该应用程序：**

- 1. 打开 **ABC Solution (ABC Solution.sln)** 文件，该文件位于 ClearlyVB\Chap11\ABC Solution 文件夹中。如有必要，打开设计器窗口。应用程序的界面如图 11-10 所示。

![](img/cf88270932e011575089da06b940a1d9_249_0.png)

图 11-10：ABC 公司应用程序的用户界面

- 2. 打开代码编辑器窗口。在 btnDisplayPrice 控件的 Click 事件过程中，输入图 11-11 所示的 Select Case 语句。

```vb
Private Sub btnDisplayPrice_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' displays the price per item

    Dim intNumOrdered As Integer
    Dim intPrice As Integer

    ' assign number ordered to a variable
    Integer.TryParse(txtNumOrdered.Text, intNumOrdered)

    ' determine the price per item, then display the price
    Select Case intNumOrdered
        Case 1 To 5
            intPrice = 25
        Case 6 To 10
            intPrice = 23
        Case Is > 10
            intPrice = 20
        Case Else
            intPrice = 0
    End Select
    lblPrice.Text = intPrice.ToString("C2")
End Sub
```

**图 11-11：** 在 btnDisplayPrice 控件的 Click 事件过程中输入的 Select Case 语句

- 3. 保存解决方案，然后启动应用程序。

- 4. 输入 **4** 作为订购数量，然后单击 **显示价格** 按钮。按钮 Click 事件过程中的 Integer.TryParse(txtNumOrdered.Text, intNumOrdered) 语句将订购数量赋给 intNumOrdered 变量。接下来处理 Select Case 语句。处理该语句时，计算机首先将 intNumOrdered 变量的内容（4）与第一个 Case 子句的 expressionList：范围 1 To 5 进行比较。数字 4 包含在该范围内，因此计算机将数字 25 赋给 intPrice 变量。然后跳到 End Select 子句之后的指令。该指令在 lblPrice 控件中显示 intPrice 变量的内容（转换为带两位小数的 Currency）；在本例中，它显示 $25.00。

- 5. 自行使用以下数字测试应用程序：**10**、**-3**、**12** 和 **x**。价格应分别为 $23.00、$0.00、$20.00 和 $0.00。

- 6. 单击 **退出** 按钮结束应用程序。关闭代码编辑器窗口，然后关闭解决方案。

有关使用 Select Case 语句编写多路径选择结构的更多示例，请参阅 Ch11WantMore.pdf 文件中的“Select Case 多路径选择结构”部分。

![](img/cf88270932e011575089da06b940a1d9_250_0.png)

