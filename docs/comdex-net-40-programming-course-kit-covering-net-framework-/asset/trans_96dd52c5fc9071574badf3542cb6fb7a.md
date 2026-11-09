
![](img/9862a98a1a2d3bb14334137965a1ec60_272_0.png)

图 VB-7.42

你可以在图 VB-7.42 中注意到，对象关系设计器的左窗格中添加了一个 LINQ to SQL 实体类 **Customer**，它对应 **Customers** 表。你还可以注意到，**Customers** 表的列已成为 **Customer** 类的属性。

- 31. *双击*设计器中 form1 的标题栏以打开代码编辑器，并将代码清单 7.20 中突出显示的代码片段*添加*到代码编辑器中：

### 代码清单 7.20：处理窗体的 Load 事件

```vb
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
    Handles MyBase.Load
    Dim dc As MyClassDataContext = New MyClassDataContext()
    Dim query = From c In dc.Customers Select c
    For Each c In query
        ListView1.Items.Add(c.CustomerID.ToString() & _
            ", " & c.CustName.ToString())
    Next
End Sub
```

代码清单 7.20 显示了 **Form1** 的 Load 事件的事件处理程序代码。在突出显示的代码行中，我们首先创建 **MyClassDataContext** 类的对象，以检索应用程序中要使用的数据。然后，我们创建一个 LINQ 查询，从 **Customers** 表中检索所有数据。最后，我们使用 For Each 循环，将 **Customers** 表中 **CustomerID** 和 **CustName** 列的数据添加到窗体上的 **ListView** 控件中。

- 32. 按 F5 键运行应用程序。应用程序的输出如图 VB-7.43 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_272_1.png)

图 VB-7.43

## 在查询中使用匿名类型

LINQ 中的匿名类型提供了一种便捷方式，可将一组只读属性组合成一个要包含在查询结果中的元素。你无需为这些属性定义类型，因为类型由编译器定义。这些类型使你能够创建某个类的对象，而无需编写类定义。此类类没有名称，因此称为匿名类型。匿名类型使你能够在查询中以任意顺序选择可用字段的任意组合，而无需为任何元素定义命名数据类型。

编译器动态构造匿名类型并为其分配名称。每次生成应用程序时名称都会改变，因此匿名类型的名称不能直接在应用程序中使用。

LINQ 中的匿名类型用于查询表达式，以组合查询所选的数据列。它们使你能够编写选择任意数量列且顺序任意的查询。

执行以下步骤，以在 LINQ 查询中使用匿名类型：

- 1. *启动 Visual Studio 2010。*
- 2. *从菜单栏中选择* **文件 → 新建 → 项目**。**新建项目** *对话框打开。*
- 3. *在* **新建项目** *对话框的左窗格中，从* **已安装的模板** *部分选择* **Visual Basic→Windows**。
- 4. *在中间窗格中选择* **Windows 窗体应用程序** *以创建 Windows 窗体应用程序。*
- 5. *在* **名称** *文本框中输入应用程序的名称* **AnonymousTypes** *（该程序也可在光盘中找到），并在* **位置** *组合框中为应用程序输入适当的位置。*
- 6. *单击* **确定** *按钮关闭* **新建项目** *对话框。* **AnonymousTypes** *应用程序即创建完成（图 VB-7.44）。*
- 7. *从* **工具箱** *中将一个* **ListView** *控件拖放到窗体上（图 VB-7.44）。*
- 8. *在窗体中选择该控件，并单击控件右上角的右箭头按钮，以打开* **ListView** *控件的* **智能标记** *（图 VB-7.44）。*
- 9. *单击* **ListView** *控件智能标记中* **视图** *下拉列表的下箭头按钮，然后从下拉菜单中选择* **平铺** *选项（图 VB-7.44）。*
- 10. *单击* **ListView** *控件智能标记中的* **在父容器中停靠** *链接，将* **ListView** *控件停靠在其父容器（窗体）中（图 VB-7.45）。*

![](img/9862a98a1a2d3bb14334137965a1ec60_273_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_273_1.png)

- 11. *双击*设计器中的窗体以打开代码编辑器，并将代码清单 7.21 中突出显示的代码片段*添加*到代码编辑器中。

### 代码清单 7.21：演示在 LINQ 查询中使用匿名类型

```vb
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
    Dim words As String() = {"APPLE", "BlAckBeRrY", "baNaNa", "oRange", "Mango", "StrawBeRrY"}
    Dim lWords = From w In words Select New With {Key .Upper = w.ToUpper(), Key .Lower = w.ToLower()}
    For Each w In lWords
        ListView1.Items.Add(w.Upper & " <--> " & w.Lower)
    Next w
End Sub
```

代码清单 7.21 显示了 Form1 的 Load 事件的事件处理程序代码。在突出显示的代码行中，我们首先创建一个 String 类型的数组 words，它由随机组合大小写字母构成的单词组成。然后，我们通过创建 LINQ 查询来创建一个匿名类型，该类型有两个成员：Upper 和 Lower。匿名类型的 Upper 和 Lower 成员分别存储 words 数组中单词的大写和小写版本。最后，我们使用 For Each 循环将单词的大写和小写版本添加到窗体上的 ListView 控件中。

- 12. 按 F5 键运行应用程序。应用程序的输出如图 VB-7.46 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_274_0.png)

图 VB-7.46

通过这种方式，你已经看到可以借助 LINQ 查询创建匿名类型。

## 在 LINQ 查询中使用 Lambda 表达式

Lambda 表达式是一个没有名称的函数，它计算并返回单个值。它在定义的同时执行。LINQ 中的 Lambda 表达式构成了使用 LINQ 中许多标准查询运算符的基础。编译器创建 Lambda 表达式来操作查询中定义的计算，例如 Where、Select 和 Order By。Lambda 表达式的用法与标准函数类似，只是它不符合以下特征：

- 没有名称
- 不能有修饰符，例如 Overloads 或 Overrides
- 不为表示 lambda 表达式的函数返回类型使用 As 子句
- 其主体是表达式而不是语句
- 没有 Return 语句；相反，函数返回的值是函数主体中表达式的值
- 没有 End Function 语句
- 不接受泛型参数

执行以下步骤，以在 LINQ 查询中使用 lambda 表达式：

- 1. *启动 Visual Studio 2010*。
- 2. *选择* **文件 → 新建 → 项目** from the menu bar. **新建项目** 对话框打开。
- 3. *选择* **Visual Basic→Windows** from the **已安装的模板** section in the left pane of the **新建项目** dialog box.
- 4. *选择* **Windows 窗体应用程序** in the middle pane to create a Windows Forms application.
- 5. 在 **名称** 文本框中输入应用程序的名称 **LambdaExpression**（该程序也可在光盘中找到），并在 **位置** 组合框中为应用程序输入适当的位置。
- 6. *单击* **确定** 按钮关闭 **新建项目** 对话框。**LambdaExpression** 应用程序即创建完成（图 VB-7.47）。
- 7. *拖放*两个 **Label** 控件、两个 **ListBox** 控件和一个 **Button** 控件，从 **工具箱** 到窗体上（图 VB-7.47）。
- 8. 使用“属性”窗口，将第一个和第二个 Label 控件的 Text 属性分别设置为“姓名列表”和“以‘S’开头的姓名”，并将 Button 控件的 Text 属性设置为“创建新列表”，如图 VB-7.47 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_275_0.png)

图 VB-7.47

- 9. 双击窗体以创建其 Load 事件的事件处理程序，并将代码清单 7.22 中突出显示的代码片段添加到代码编辑器中。

### 代码清单 7.22：处理窗体的 Load 事件

```vb
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
    Dim persons() As String = {"Peter", "Steve", "John", "Scott", "Mark", _
        "David", "Robert"}
    For Each p In persons
        ListBox1.Items.Add(p.ToString())
    Next
End Sub
```

代码清单 7.22 显示了 Form1 的 Load 事件的事件处理程序代码。在突出显示的代码片段中，我们首先声明一个 String 类型的数组 persons，并用一组姓名初始化该数组。然后，我们使用 For Each 循环将 persons 数组的元素添加到窗体上 ListBox1 控件的 Items 集合中。

- 10. 双击窗体中的“创建新列表”按钮以创建其 Click 事件的事件处理程序，并将代码清单 7.23 中突出显示的代码片段添加到代码编辑器中。

### 代码清单 7.23：处理 Button1 的 Click 事件

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    Dim persons(6) As String
    For index = 0 To 6
        persons(index) = ListBox1.Items(index)
    Next
    Dim query = From p In persons.Where(Function(n) n.StartsWith("S")) Select p
    For Each q In query
        ListBox2.Items.Add(q.ToString())
    Next
End Sub
```

代码清单 7.23 显示了 Button1 的 Click 事件的事件处理程序代码。在突出显示的代码片段中，我们首先声明一个 String 类型的数组 persons，并用 ListBox1 控件中的项初始化该数组。然后，我们创建一个 LINQ 查询，其中使用 lambda 表达式从 persons 数组中检索以字母“S”开头的姓名。最后，我们使用 For Each 循环将检索到的姓名添加到 ListBox2 控件的 Items 集合中。
