
马匹获胜四次，获得第二名三次，获得第三名三次，并且有十次未进入前三名。创建一个新的 Visual Basic Windows 应用程序。分别将解决方案、项目和窗体文件命名为 Waterglen Solution、Waterglen Project 和 frmMain.vb。将应用程序保存到 ClearlyVB\Chap21 文件夹中。如有必要，将窗体名称更改为 frmMain。创建图21-21所示的界面。使用一个四行五列的数组存储比赛结果来编写应用程序。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_505_0.png)

![](img/cf88270932e011575089da06b940a1d9_505_1.png)

- 10. 打开 FigureThisOut Solution（FigureThisOut Solution.sln）文件，该文件位于 ClearlyVB\Chap21\FigureThisOut Solution 文件夹中。打开代码编辑器窗口，然后找到 btnCount 控件的 Click 事件过程。可以通过将行数乘以列数来确定二维数组中的元素个数。编写该过程以显示数组元素个数。保存解决方案，然后启动并测试应用程序。停止应用程序。关闭代码编辑器窗口，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_506_0.png)

- 11. 在本练习中，你将找出应用程序代码中的一个错误。打开 SwatTheBugs Solution（SwatTheBugs Solution.sln）文件，该文件位于 ClearlyVB\Chap21\SwatTheBugs Solution 文件夹中。打开代码编辑器窗口并研究现有代码。启动并测试应用程序。注意应用程序运行不正确。单击“调试”，然后单击“停止调试”。找出并更正代码中的任何错误。保存解决方案，然后再次启动并测试应用程序。停止应用程序，然后关闭解决方案。

## “试一试”练习答案

- 1. 见图21-22。

```vb
Private Sub btnDisplay_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' displays the price associated with the product
    ' ID entered by the user

    Dim strPriceList(,) As String = {{"BX35", "13"}, _
                                      {"CR20", "10"}, _
                                      {"FE15", "12"}, _
                                      {"KW10", "24"}, _
                                      {"MM67", "4"}}

    Dim strSearchFor As String
    Dim strFound As String
    Dim intRow As Integer
    Dim intNumRows As Integer

    ' assign the product ID to a variable
    strSearchFor = txtId.Text.ToUpper

    ' search for the product ID in the first column of the array
    ' continue searching until there are no more rows to search or
    ' the product ID is found
    intRow = 0
    strFound = "N"
    intNumRows = strPriceList.GetUpperBound(0) + 1

    Do Until intRow = intNumRows OrElse strFound = "Y"
        If strPriceList(intRow, 0) = strSearchFor Then
            strFound = "Y"
        Else
            intRow = intRow + 1
        End If
    Loop

    ' determine whether the product ID
    ' was found in the array
    If strFound = "Y" Then
        Dim intPrice As Integer
        intPrice = strPriceList(intRow, 1)
        lblPrice.Text = intPrice.ToString("C0")
    Else
        MessageBox.Show("Invalid product ID", _
            "Treasures Gift Shop", MessageBoxButtons.OK, _
            MessageBoxIcon.Information)
    End If
End Sub
```

**图21-22**

- 2. 见图21-23。

```vb
Private Sub btnDisplay_Click(ByVal sender As Object, _
        ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' displays the sum of the values stored in the array
    Dim intInventory(,) As Integer = {{34, 56}, _
                                      {75, 67}, _
                                      {5, 6}}
    Dim intTotal As Integer ' accumulator
    ' total the array values
    For intRow As Integer = 0 To intInventory.GetUpperBound(0)
        For intColumn As Integer = 0 To intInventory.GetUpperBound(1)
            intTotal = intTotal + intInventory(intRow, intColumn)
        Next intColumn
    Next intRow
    ' display the total
    lblTotal.Text = intTotal.ToString
End Sub
```

**图21-23**

## 22 构建自己的结构

学习第22章后，你应该能够：

![](img/cf88270932e011575089da06b940a1d9_508_0.png)

- 创建结构
- 声明和使用结构变量
- 理解使用结构的优点
- 将结构变量传递给过程
- 创建结构变量数组

### 整合各部分

在前面的章节中，你只使用了 Visual Basic 内置的数据类型，例如 Integer 和 Decimal 数据类型。你也可以使用 **Structure 语句** 在 Visual Basic 中创建自己的数据类型。使用 Structure 语句创建的数据类型称为**结构**。与数组类似，你可以使用结构将相关项组合在一起。但是，与数组中的项不同，结构中的项不必具有相同的数据类型。因此，你可以将具有 String 数据类型的项（例如员工的 ID、名字和姓氏）与具有数值数据类型的项（例如 Decimal 薪资金额）组合在一起。图22-1显示了 Structure 语句的语法。结构名称出现在 Structure 子句中。约定使用 Pascal 命名法输入结构名称，这意味着名称首字母以及名称中后续每个单词的首字母都要大写。在 Structure 和 End Structure 子句之间，定义结构中包含的成员。成员可以是变量或过程；但是，在本书中，你将只学习如何包含变量。这是因为大多数程序员使用 Class 语句（而不是 Structure 语句）来创建包含过程的数据类型。（你将在第27章学习 Class 语句。）在大多数结构中，成员变量使用关键字 Public 定义，后跟变量名、关键字 As 以及变量的 *dataType*。*dataType* 标识变量将存储的数据类型。*dataType* 可以是 Visual Basic 中可用的任何标准数据类型；也可以是另一个结构。图22-1所示的 Employee 结构包含四个成员：三个 String 变量和一个 Decimal 变量。

**创建结构**

语法
```vb
Structure structureName
    Public memberVariableName1 As dataType
    [Public memberVariableNameN As dataType]
End Structure
```

示例
```vb
Structure Employee
    Public strId As String
    Public strFirstName As String
    Public strLastName As String
    Public decSalary As Decimal
End Structure
```

**图22-1：** 创建结构的语法和示例

在大多数应用程序中，Structure 语句输入在窗体的声明部分，即代码编辑器窗口中 Public Class 和 End Class 行之间的区域。Structure 语句本身不会在计算机内部内存中预留任何位置。相反，它提供了一种数据类型的模式，可用于预留内存位置。使用结构声明的变量通常称为**结构变量**。图22-2显示了创建结构变量的语法。使用 Dim 关键字声明过程级结构变量，使用 Private 关键字声明模块级结构变量。该图还包含一个使用图22-1中的 Employee 结构声明结构变量的示例。

### 声明结构变量

语法
```vb
{Dim | Private} structureVariableName As structureName
```

示例
```vb
Dim manager As Employee
```

声明一个名为 manager 的 Employee 结构变量；该结构变量包含四个成员

**图22-2：** 声明结构变量的语法和示例

