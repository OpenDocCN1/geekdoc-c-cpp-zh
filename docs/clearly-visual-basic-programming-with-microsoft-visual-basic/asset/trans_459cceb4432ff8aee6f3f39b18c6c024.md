
（输入项）在 txtRadius 控件中。当用户单击 Calculate 按钮时，该按钮的 Click 事件过程将使用圆的半径来计算圆的面积（输出项）。你可能还记得数学课程中的内容，计算圆面积的公式是 πr²，其中 π 代表圆周率。在该过程结束前，它将在 lblArea 控件中显示圆的面积。

![](img/cf88270932e011575089da06b940a1d9_148_0.png)

**图 7-6：** Circle Area 应用程序的界面

- 2. 打开“代码编辑器”窗口，其中包含 btnExit 控件的 Click 事件过程的代码。
- 3. 打开 btnCalc 控件的 Click 事件过程。首先，你将输入声明必要变量的指令。通常将变量声明语句输入在过程开头。输入图 7-7 中所示的注释和两条 Dim 语句，然后按图中所示放置插入点。每个变量名下方的绿色锯齿线表示该变量已声明，但尚未被该过程中的任何其他语句使用。

```vb
' Name:         Circle Area Project
' Purpose:      Display the area of a circle
' Programmer:   <your name> on <current date>

Public Class frmMain

    Private Sub btnExit_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnExit.Click
        Me.Close()
    End Sub

    Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
        ' calculates and displays the area of a circle

        ' declare variables
        Dim dblArea As Double
        Dim dblRadius As Double

    End Sub
End Class
```

**图 7-7：** 在该过程中输入的注释和 Dim 语句

现在你可以开始编写应用程序的算法代码。算法中的第一步是输入圆的半径。回想一下，用户在 txtRadius 控件中输入半径。第二步是通过将半径乘以自身，然后将结果乘以 3.141593（π 的值四舍五入到六位小数）来计算圆的面积。运用你在第 6 章学到的内容，你可以使用表达式 Val(txtRadius.Text) * Val(txtRadius.Text) * 3.141593 来计算圆的面积。该表达式告诉计算机将 txtRadius 控件的 Text 属性内容（临时转换为数字）乘以 txtRadius 控件的 Text 属性内容（再次临时转换为数字），然后将结果乘以数字 3.141593。然而，尽管 Val 函数自 Visual Basic 语言诞生以来就是其组成部分，微软并不保证它会始终是该语言的一部分。因此，大多数程序员现在使用 TryParse 方法将文本转换为数字。

## TRYPARSE 方法

Visual Basic 中的每种数值数据类型都有一个 **TryParse 方法**，可用于将文本转换为该数值数据类型。TryParse 方法的基本语法是 *dataType*.**TryParse**(*text*, *variable*)。在该语法中，*dataType* 是 Visual Basic 中可用的数值数据类型之一，例如 Double、Decimal 和 Integer。*text* 参数是要转换为 *dataType* 类型数字的文本，通常是控件的 Text 属性。*variable* 参数是数值变量的名称，TryParse 方法可在其中存储该数字。该数值变量必须具有与语法中 *dataType* 部分指定的数据类型相同的数据类型。换句话说，当使用 TryParse 方法将文本转换为 Double 数字时，需要向该方法提供一个用于存储该数字的 Double 变量名。TryParse 方法会解析文本，这意味着它会查看文本中的每个字符，以确定该文本能否转换为指定数据类型的数字。如果文本可以转换，TryParse 方法会将文本转换为数字，并将该数字存储在 *variable* 参数指定的变量中。但是，如果 TryParse 方法确定文本无法转换为适当的数据类型，该方法会将数字 0 赋给 *variable*。图 7-8 显示了 TryParse 方法的基本语法，并包含使用该方法的示例。（要了解更多关于 TryParse 方法的信息，请完成本章末尾的 FIGURE THIS OUT 练习。）

### TRYPARSE 方法的基本语法

语法

`dataType.TryParse(text, variable)`

示例 1

`Double.TryParse(txtRadius.Text, dblRadius)`

如果 txtRadius 控件中输入的文本可以转换为 Double 数字，TryParse 方法会转换该文本并将结果存储在 dblRadius 变量中；否则，它会在 dblRadius 变量中存储数字 0。

示例 2

`Decimal.TryParse(txtSales.Text, decSales)`

如果 txtSales 控件中输入的文本可以转换为 Decimal 数字，TryParse 方法会转换该文本并将结果存储在 decSales 变量中；否则，它会在 decSales 变量中存储数字 0。

示例 3

`Integer.TryParse(txtNum.Text, intNum)`

如果 txtNum 控件中输入的文本可以转换为 Integer 数字，TryParse 方法会转换该文本并将结果存储在 intNum 变量中；否则，它会在 intNum 变量中存储数字 0。

**图 7-8：** TryParse 方法的基本语法和示例

在输入计算圆面积的指令之前，你首先将使用 TryParse 方法将 txtRadius 控件的 Text 属性转换为数字。你将让该方法把得到的数字赋给 dblRadius 变量。然后你将在圆面积计算中使用 dblRadius 变量。

**要继续编写 Circle Area 应用程序的代码：**

- 1. 插入点应位于前面图 7-7 所示的位置。输入 **assign radius to a variable** 并按 **Enter**，然后输入 **Double.TryParse(txtRadius.Text, dblRadius)** 并按两次 **Enter**。
- 2. 现在可以在计算圆面积的表达式中使用 dblRadius 变量。你将把计算结果赋给 dblArea 变量。输入 **calculate area** 并按 **Enter**，然后输入 **dblArea = dblRadius * dblRadius * 3.141593** 并按两次 **Enter**。（也可以使用 dblArea = dblRadius ^ 2 * 3.141593。）
- 3. 算法中的第 3 步（前面图 7-5 所示）是显示圆的面积。输入 **display area** 并按 **Enter**，然后输入 **lblArea.Text = dblArea** 并按 **Enter**。图 7-9 显示了该过程的代码。

```vb
Private Sub btnCalc_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnCalc.Click
    ' calculates and displays the area of a circle

    ' declare variables
    Dim dblArea As Double
    Dim dblRadius As Double

    ' assign radius to a variable
    Double.TryParse(txtRadius.Text, dblRadius)

    ' calculate area
    dblArea = dblRadius * dblRadius * 3.141593

    ' display area
    lblArea.Text = dblArea

End Sub
End Class
```

**图 7-9：** 在 btnCalc 控件的 Click 事件过程中输入的代码

- 4. 保存解决方案。

大多数变量在过程（例如事件过程）中声明。这些变量称为 **过程级变量**，并且被认为具有 **过程作用域**，因为它们只能由声明它们的过程使用。**作用域** 指变量在应用程序代码中被识别的区域。图 7-9 中的 dblRadius 和 dblArea 变量是过程级变量，只能由 btnCalc 控件的 Click 事件过程使用。当过程结束时，其过程级变量将从计算机的内部存储器中移除。程序员将变量在内存中保留的时间长度称为它的 **生存期**。过程级变量的生存期与声明它的过程相同。

## 检查一下……我准备好了

在使用计算机测试 Circle Area 应用程序之前（这是第 3 章问题求解过程中的第 7 步），你将执行第 6 步，即对程序进行桌面检查。你可以使用桌面检查表来完成此操作，类似于你对算法进行桌面检查时使用的表。程序的桌面检查表将为每个变量包含一列。例如，你将使用半径值 6.5 和 10 对 Circle Area 程序进行桌面检查。图 7-10 显示了完成的桌面检查表。请自行使用其他值对该程序进行桌面检查。

| dblRadius | dblArea |
|---:|---:|
| 6.5 | 132.73230425 |
| 10 | 314.1593 |

**图 7-10：** Circle Area 程序的桌面检查表

