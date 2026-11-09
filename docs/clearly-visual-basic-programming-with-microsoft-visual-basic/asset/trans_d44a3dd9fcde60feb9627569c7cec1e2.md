
**要继续编写 Employee 应用程序的代码，然后测试该应用程序：**

- 1. 插入点应位于 strFound = "N" 语句下方。键入 **intNumRows = strEmployInfo.GetUpperBound(0) + 1**，然后按 **Enter**。

- 2. 算法中的第 5 步是一个预测试循环，它会重复执行其指令，直到以下两个条件之一为真：要么已在数组的第一列中找到该 ID，要么行下标等于数组中的行数（这表示没有更多行可供搜索）。你将使用 Do...Loop 语句（而不是 For...Next 语句）来编写该循环，因为你不清楚循环指令应被处理的确切次数。键入 **Do Until strFound = "Y" OrElse intRow = intNumRows**，然后按 **Enter**。

- 3. 循环中的第一条指令是一个选择结构，它将数组中当前行第一列存储的 ID 与 strSearchFor 变量中存储的 ID 进行比较。如果两个 ID 匹配，则该选择结构的真路径会将 "Y" 赋给 strFound 变量，以指示已在数组中找到该 ID。如果两个 ID 不匹配，则该选择结构的假路径会将行下标增加 1；这将允许循环搜索数组中的下一行。键入图 21-7 所示的选择结构。

![](img/cf88270932e011575089da06b940a1d9_494_0.png)

```vb
' search for the ID in the first column in the array
' continue searching until the ID is found or each
' row has been searched
intRow = 0
strFound = "N"
intNumRows = strEmployInfo.GetUpperBound(0) + 1
Do Until strFound = "Y" OrElse intRow = intNumRows
    If strEmployInfo(intRow, 0) = strSearchFor Then
        strFound = "Y"
    Else
        intRow = intRow + 1
    End If
Loop
```

**图 21-7：** 在过程中输入的选择结构

- 4. strFound 变量中存储的字母指示是否在数组中找到了该 ID，并决定应显示的适当信息。如果找到了该 ID，则该过程应显示数组中当前行第二列存储的薪资；否则，应显示“Invalid ID”消息。单击 ' determine whether the ID was found 注释下方的 **空白行**，然后键入图 21-8 所示的附加选择结构。

输入此选择结构。

```vb
' determine whether the ID was found
If strFound = "Y" Then
    lblSalary.Text = strEmployInfo(intRow, 1)
Else
    lblSalary.Text = "Invalid ID"
End If
End Sub
```

**图 21-8：** 在过程中输入的附加选择结构

- 5. 保存解决方案，然后启动应用程序。首先，输入一个有效 ID。在 Employee ID 框中键入 **c510**。该 ID 位于 `strEmployInfo(2, 0)` 元素中，其关联薪资位于 `strEmployInfo(2, 1)` 元素中。单击 **显示薪资** 按钮。正确的薪资额会显示在 Salary 框中，如图 21-9 所示。请注意，该薪资额未格式化，这与第 20 章的 Employee 应用程序中一样（见图 20-6）。

![](img/cf88270932e011575089da06b940a1d9_495_0.png)

**图 21-9：** 界面中显示的薪资额

- 6. 单击 **退出** 按钮。

在第 20 章的 Employee 应用程序中，薪资额被当作数字处理，并存储在 Integer 数组中。因此，在显示薪资时，你可以使用 ToString 方法对其进行格式化。在本章的 Employee 应用程序中，薪资额是字符串，并存储在 String 数组中。在使用 ToString 方法之前，你需要先将薪资转换为数字。

**要格式化薪资额，然后测试该应用程序：**

- 1. 按图 21-10 所示修改第二个选择结构。

![](img/cf88270932e011575089da06b940a1d9_496_0.png)

```vb
' determine whether the ID was found
If strFound = "Y" Then
    Dim intSalary As Integer
    intSalary = strEmployInfo(intRow, 1)
    lblSalary.Text = intSalary.ToString("C0")
Else
    lblSalary.Text = "Invalid ID"
End If
```

**图 21-10：** 修改后的选择结构

- 2. 保存解决方案，然后启动应用程序。在 Employee ID 框中键入 **c510**，然后单击 **显示薪资** 按钮。格式化后的薪资额（$43,000）会显示在 Salary 框中。

- 3. 现在输入一个无效 ID。在 Employee ID 框中键入 **c511**，然后单击 **显示薪资** 按钮。消息“Invalid ID”会显示在 Salary 框中。

- 4. 再使用有效和无效 ID 测试该应用程序几次。完成应用程序测试后，单击 **退出** 按钮。关闭代码编辑器窗口，然后关闭解决方案。

## CALENDAR ORDERS 应用程序

Calendar Orders 应用程序显示三家商店在六个月中每个月订购的日历总数。每家商店每月订购的数量存储在一个三行六列的数组中。数组中的每一行代表一家商店，每一列代表一个月。要显示订购的日历总数，你需要累加二维数组中存储的值。

**要打开 Calendar Orders 应用程序，然后编写并测试该应用程序：**

- 1. 打开 **Orders Solution (Orders Solution.sln)** 文件，该文件位于 ClearlyVB\Chap21\Orders Solution 文件夹中。如有必要，打开设计器窗口。

- 2. 打开代码编辑器窗口，然后找到 btnDisplay 控件的 Click 事件过程的代码模板。首先，声明该二维数组。单击 ' declare the two-dimensional array 注释下方的 **空白行**。输入图 21-11 所示的数组声明语句，然后按图中所示放置插入点。

![](img/cf88270932e011575089da06b940a1d9_497_0.png)

**图 21-11：** 在过程中输入的数组声明

- 3. 该过程将需要一个累加器变量来汇总订单。键入 **Dim intTotal As Integer**，按 **Tab**，然后键入 **' accumulator**，再按 **Enter**。

- 4. 要累加数组中存储的值，你需要访问每个数组元素。如前所述，你可以使用外层循环和嵌套循环来完成此操作。你可以逐行或逐列访问这些元素；在本例中，你将逐列访问它们。单击 ' accumulate the calendars ordered 注释下方的 **空白行**。输入图 21-12 所示的两个重复结构。

![](img/cf88270932e011575089da06b940a1d9_497_1.png)

**图 21-12：** 在过程中输入的重复结构

- 5. 最后，显示订购的日历总数。单击 'display the number of calendars ordered 注释下方的 **空白行**。键入 **lblTotal.Text = intTotal.ToString**，然后按 **Enter**。

- 6. 保存解决方案，然后启动应用程序。单击 **显示总计** 按钮。订购的日历总数会显示在 Total ordered 框中，如图 21-13 所示。

![](img/cf88270932e011575089da06b940a1d9_498_0.png)

**图 21-13：** 显示订购日历总数的界面

- 7. 单击 **退出** 按钮。关闭代码编辑器窗口，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_498_1.png)

要详细了解二维数组，请参阅 Ch21WantMore.pdf 文件中的 Two-Dimensional Arrays 一节。

## 小结

- 二维数组中的每个元素由两个下标的唯一组合来标识：行下标和列下标。这些下标出现在数组名后的括号中。先列出行下标，然后是一个逗号，再列出列下标。
- 二维数组中的第一个行下标是 0。第一个列下标也是 0。
- 声明二维数组时，你要么提供最高行下标和列下标，要么提供初始值。
- 二维数组中的行数比其最高行下标大 1。同样，列数比其最高列下标大 1。
- 引用二维数组中的某个元素时，使用数组名后跟该元素的行下标和列下标，两者之间用逗号分隔。
- 你使用外层循环和嵌套循环来访问二维数组中的每个元素。一个循环控制行下标，另一个循环控制列下标。
- 数组的 GetLowerBound 和 GetUpperBound 方法分别返回数组中的最低下标和最高下标。
