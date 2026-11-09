
- 12. *单击* **显示不同值** 按钮（图VB-7.9）。来自第一个列表框中值列表的不同值将显示在第二个列表框中，如图VB-7.10所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_250_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_250_1.png)

图VB-7.9　　　　　　　　　　　　　　　　　图VB-7.10

这是集合运算符的一个示例，其中使用 **Distinct** 子句从一组可能包含重复值的值中查找一些唯一值。

## 筛选运算符

筛选，顾名思义，是指修改结果集以使其仅包含满足指定条件的元素的操作。

表7.4列出了LINQ中的所有筛选运算符：

| 运算符 | 描述 | 查询表达式语法（Visual Basic） |
|---|---|---|
| OfType | 从一组值中选择可转换为指定类型的值 | 不可用 |
| Where | 从一组值中选择与给定条件匹配的值 | Where |

执行以下步骤，使用 **Where** 子句筛选数据：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中*选择* **文件→新建→项目**。将打开 **新建项目** 对话框。
- 3. 在 **新建项目** 对话框的左窗格中，从 **已安装的模板** 部分*选择* **Visual Basic→Windows**。
- 4. 在中间窗格中*选择* **Windows 窗体应用程序** 选项，以创建 Windows 窗体应用程序。
- 5. 在 **名称** 文本框中*输入*应用程序的名称 **FilteringOperator**（也可在 CD 上获得），并在 **位置** 组合框中输入应用程序的适当位置。
- 6. *单击* **确定** 按钮以关闭 **新建项目** 对话框。将创建 **FilteringOperator** 应用程序（图VB-7.11）。
- 7. 从 **工具箱** 中*拖放*两个 **Label** 控件、两个 **ListBox** 控件和一个 **Button** 控件到窗体上（图VB-7.11）。
- 8. 将 **Label1**、**Label2** 和 **Button1** 控件的 **Text** 属性分别*设置*为 **筛选前**、**筛选后** 和 **筛选数据**，如图VB-7.11所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_251_0.png)

图VB-7.11

- 9. *双击*窗体以创建其 **Load** 事件的事件处理程序，并将清单7.7中所示的高亮代码片段添加到代码编辑器中：

### **清单7.7：** 处理窗体的 Load 事件

```
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
    Handles MyBase.Load
    Dim values() As Integer = {1, 2, 3, 4, 5, 6, 7, 8, 9}
    For Each v In values
        ListBox1.Items.Add(v.ToString())
    Next
End Sub
```

清单7.7显示了 Form1 的 Load 事件的事件处理程序代码。在高亮代码片段中，我们首先声明一个 Integer 类型的数组 values，并使用一组整数值初始化该数组。然后，我们使用 For Each 循环将 values 数组的元素添加到窗体上第一个 ListBox1 控件的 Items 集合中。

- 10. *双击*窗体中的“筛选数据”按钮，以创建其 **Click** 事件的事件处理程序，并将清单7.8中所示的高亮代码片段添加到代码编辑器中：

### **清单7.8：** 处理 Button1 的 Click 事件

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    Dim values(8) As Integer
    For index = 0 To 8
        values(index) = ListBox1.Items(index)
    Next
    Dim filteredValues = From v In values Where v Mod 2 = 0 Select v
    ListBox2.Items.Clear()
    For Each v In filteredValues
        ListBox2.Items.Add(v.ToString())
    Next
End Sub
```

清单7.8显示了 Button1 的 Click 事件的事件处理程序代码。在高亮代码片段中，我们首先声明一个 Integer 类型的数组 values，并使用 ListBox1 控件中的项初始化该数组。然后，我们在 filteredValues 查询中使用 Where 子句，从数组中检索偶数值。最后，我们将筛选后的值添加到 ListBox2 控件的 Items 集合中。

- 11. *按* F5 键运行应用程序。应用程序的输出将出现，在窗体上的第一个列表框中显示值列表（图VB-7.12）。
- 12. 单击“筛选数据”按钮（图VB-7.12）。来自第一个列表框中值列表的偶数值将显示在第二个列表框中，如图VB-7.13所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_252_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_252_1.png)

在图VB-7.13中，可以看到 Where 子句筛选给定序列并返回满足给定条件的值。

## 投影运算符

投影运算符用于将对象转换为新对象，新对象的形式通常由后续将要使用的那些属性组成。可以使用投影运算符构造一个由每个对象构建而成的不同类型的新对象。

表7.5列出了LINQ中的所有投影运算符：

| 运算符 | 描述 | 查询表达式语法（Visual Basic） |
|---|---|---|
| Select | 从单个序列或集合中投影（或选择）值 | Select |
| SelectMany | 从多个序列或集合中投影（或选择）值 | 将 Select 子句与多个 From 子句一起使用 |

执行以下步骤，使用 Select 子句投影一个单词序列：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中*选择* **文件→新建→项目**。将打开 **新建项目** 对话框。
- 3. 在 **新建项目** 对话框的左窗格中，从 **已安装的模板** 部分*选择* **Visual Basic→Windows**。
- 4. 在中间窗格中*选择* **Windows 窗体应用程序**，以创建 Windows 窗体应用程序。
- 5. 在 **名称** 文本框中*输入*应用程序的名称 **ProjectionOperator**（也可在 CD 上获得），并在 **位置** 组合框中输入应用程序的适当位置。
- 6. *单击* **确定** 按钮以关闭 **新建项目** 对话框。将创建 **ProjectionOperator** 应用程序（图VB-7.14）。
- 7. 从 **工具箱** 中*拖放*两个 **Label** 控件、两个 **ListBox** 控件和一个 **Button** 控件到窗体上（图VB-7.14）。
- 8. 将 **Label1**、**Label2** 和 **Button1** 控件的 **Text** 属性分别*设置*为 **投影前：**、**投影后：** 和 **投影数据**，如图VB-7.14所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_253_0.png)

图VB-7.14

- 9. *双击*窗体以创建其 Load 事件的事件处理程序，并将清单7.9中所示的高亮代码片段添加到代码编辑器中：

### **清单7.9：** 处理窗体的 Load 事件

```
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
    Dim words() As String = {"red", "blue", "white", "yellow", "green"}
    For Each w In words
        ListBox1.Items.Add(w.ToString())
    Next
End Sub
```

清单7.9显示了 Form1 的 Load 事件的事件处理程序代码。在高亮代码片段中，我们首先声明一个 String 类型的数组 words，并使用一组字符串值初始化该数组。然后，我们使用 For Each 循环将 words 数组的元素添加到窗体上 ListBox1 控件的 Items 集合中。

- 10. *双击*窗体中的 **投影数据** 按钮，以创建其 Click 事件的事件处理程序，并将清单7.10中所示的高亮代码片段添加到代码编辑器中：

### **清单7.10：** 处理按钮的 Click 事件

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    Dim words(4) As String
    For index = 0 To 4
        words(index) = ListBox1.Items(index)
    Next
    Dim query = From word In words Select word.Substring(0, 1)
    For Each letter In query
        ListBox2.Items.Add(letter.ToString())
    Next
End Sub
```

清单7.10显示了 Button1 的 Click 事件的事件处理程序代码。在高亮代码片段中，我们首先声明一个 String 类型的数组 words，并使用 ListBox1 控件中的项初始化该数组。然后，我们在 LINQ 查询中使用 Select 子句来选择 words 数组中所有元素的第一个字母。最后，我们将这组字母添加到 ListBox2 控件的 Items 集合中。

- 11. 按 F5 键运行应用程序。应用程序的输出将出现，在窗体上的第一个列表框中显示单词列表（图VB-7.15）。
