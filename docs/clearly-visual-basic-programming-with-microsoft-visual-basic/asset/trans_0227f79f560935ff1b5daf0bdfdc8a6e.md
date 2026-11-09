
有 10 条记录，每条记录有四个字段：ID、Title、CreditHours 和 Grade。CreditHours 字段是数值型；其他字段包含文本。打开 College Courses Solution (College Courses Solution.sln) 文件，该文件位于 ClearlyVB\Chap26\College Courses Solution 文件夹中。打开设计器窗口。将应用程序连接到 Courses 数据库。将表拖到分组框控件中，然后将 DataGridView 控件停靠在其父容器中。（在这种情况下，父容器是分组框控件。）使用任务列表禁用“添加”、“编辑”和“删除”。将 DataGridView 控件的 AutoSizeColumnsMode 属性更改为 Fill。通过从组件栏删除 BindingNavigator 对象，从窗体中移除 BindingNavigator 控件。打开代码编辑器窗口。删除“保存数据”按钮的 Click 事件过程。为“下一条记录”和“上一条记录”按钮编写代码。为“显示”按钮编写代码，使用户可以显示所有记录或与特定成绩匹配的记录。为“计算 GPA”按钮编写代码，使其显示学生的 GPA。（A 成绩值 4 分，B 值 3 分，依此类推。）保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

- 7. 打开 FigureThisOut Solution (FigureThisOut Solution.sln) 文件，该文件位于 ClearlyVB\Chap26\FigureThisOut Solution 文件夹中。打开代码编辑器窗口并研究现有代码。btnDisplay 控件的 Click 事件过程中的 LINQ 语句执行什么任务？启动并测试应用程序。停止应用程序。关闭代码编辑器窗口，然后关闭解决方案。

- 8. 在本练习中，你要找出应用程序代码中的一个错误。打开 SwatTheBugs Solution (SwatTheBugs Solution.sln) 文件，该文件位于 ClearlyVB\Chap26\SwatTheBugs Solution 文件夹中。打开代码编辑器窗口并研究现有代码。启动并测试应用程序。注意该应用程序运行不正确。停止应用程序。查找并更正代码中的任何错误。保存解决方案，然后再次启动并测试应用程序。停止应用程序，然后关闭解决方案。

## “试一试”练习答案

- 1. 参见图 26-6。

```vb
Private Sub btnSort_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnSort.Click
    ' displays records in descending order by the Cost field

    Dim records = From magazine In MagazinesDataSet.tblMagazine _
        Order By magazine.Cost Descending _
        Select magazine
    TblMagazineBindingSource.DataSource = records
End Sub

Private Sub btnDisplayCode_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplayCode.Click
    ' displays the record whose Code field contains PG24

    Dim records = From magazine In MagazinesDataSet.tblMagazine _
        Where magazine.Code = "PG24" _
        Select magazine
    TblMagazineBindingSource.DataSource = records
End Sub

Private Sub btnDisplayName_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplayName.Click
    ' displays the record whose MagName field contains Java

    Dim records = From magazine In MagazinesDataSet.tblMagazine _
        Where magazine.MagName = "Java" _
        Select magazine
    TblMagazineBindingSource.DataSource = records
End Sub
```

图 26-6

- 2. 参见图 26-7。

```vb
Private Sub btnDisplayCost_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplayCost.Click
    ' displays magazines costing $4 or more

    Dim records = From magazine In MagazinesDataSet.tblMagazine _
                  Where magazine.Cost >= 4 Select magazine
    TblMagazineBindingSource.DataSource = records
End Sub

Private Sub btnDisplayName_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplayName.Click
    ' displays magazines whose name starts with C

    Dim records = From magazine In MagazinesDataSet.tblMagazine _
                  Where magazine.MagName Like "C*" _
                  Select magazine
    TblMagazineBindingSource.DataSource = records
End Sub

Private Sub btnAverage_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnAverage.Click
    ' displays the average cost of a magazine

    Dim avgCost = Aggregate magazine In MagazinesDataSet.tblMagazine _
                  Select magazine.Cost Into Average()
    MessageBox.Show("Average cost of a magazine: " _
                    & avgCost.ToString("C2"), "Magazines", _
                    MessageBoxButtons.OK, MessageBoxIcon.Information)
End Sub
```

**图 26-7**

## 真正有品位的对象

Visual Basic 2008 是一种面向对象编程语言，这种语言允许程序员使用对象来实现程序目标。面向对象程序中使用的对象可以呈现许多不同形式。大多数 Windows 程序中包含的文本框、标签和按钮都是对象。对象也可以表示现实生活中的事物，例如信用卡收据、支票，甚至员工。每个对象都是由类创建的，类是计算机在创建对象时遵循的模式或蓝图。使用面向对象编程（OOP）术语来说，对象是从类实例化（创建）的，每个对象称为该类的一个实例。例如，按钮控件是 Button 类的实例，Button 类就是实例化按钮所用的类。另一方面，文本框是 TextBox 类的实例。类本身不是对象；只有类的实例才是对象。每个对象都有特性，即描述该对象的特征。特性也称为属性。按钮和文本框的特性包括 Name 和 Text 属性。DataGridView 控件具有 DataSource 属性以及 AutoSizeColumnsMode 属性。除了特性之外，每个对象还有行为。对象的行为包括方法和事件。方法是对象能够执行的操作（动作）。例如，按钮控件可以使用其 Focus 方法将焦点发送给自身。事件是对象可以响应的动作。例如，按钮控件的 Click 事件允许按钮响应鼠标单击。类包含——用 OOP 术语说，就是封装——它实例化的对象的所有特性和行为。

在前几章中，你使用 Visual Basic 内置的类（如 TextBox 和 Label 类）实例化对象。你在许多不同的应用程序中以多种方式使用了这些对象。在某些应用程序中，你使用文本框输入姓名，而在其他应用程序中，你使用它输入销售税率，或显示可滚动文本。同样，你使用标签控件来标识文本框，也用于显示计算结果。能够将一个对象用于多种目的可节省编程时间和金钱——这一优势促进了面向对象编程的流行。除了使用 Visual Basic 类之外，你还可以定义自己的类，然后从这些类创建实例（对象）。与 Visual Basic 类一样，你的类必须指定其创建对象的特性和行为。你使用 Class 语句定义类，其语法如图 27-1 所示。虽然语法并不要求，但约定使用帕斯卡命名法输入类名。回顾一下，帕斯卡命名法是指名称中的首字母以及名称中任何后续单词的首字母都大写。Visual Basic 类的名称（例如 String 和 TextBox）也遵循此命名约定。在 Class 语句内，你定义该类将创建的对象的特性和行为。特性由变量和 Property 过程表示。你将在本章学习 Property 过程。行为由 Sub 和 Function 过程表示，通常称为方法。（某些行为由事件过程表示；不过，该主题超出了本书的范围。）图 27-1 还包含一个 Class 语句示例，该语句定义了一个名为 RectangularPool 的类。

```text
THE CLASS STATEMENT
Syntax

Public Class className
    attributes section (contains variables and Property procedures)
    behaviors section (contains Sub and/or Function procedures)
End Class

Example

Public Class RectangularPool
    attributes
    behaviors
End Class
```

图 27-1：Class 语句的语法和示例

你将在 Willow Pools 应用程序中使用 Class 语句，你将在下一节开始编写该应用程序的代码。

## 重新审视 Willow Pools 应用程序

你在第 22 章编写了 Willow Pools 应用程序。你可能还记得，该应用程序计算并显示矩形水池的体积以及填满水池所需的水量。体积通过将水池的长度乘以宽度，再将结果乘以水池的深度来计算。假设长度、宽度和深度以英尺为单位，这样得到的是以立方英尺为单位的体积。要确定水的加仑数，需将立方英尺数乘以 7.48，
