

## 创建子类

要实现继承，你需要在项目中添加一个新类。使用 Project ➔ Add Class 菜单选项并添加一个名为 Employee.vb 的新类。从以下代码开始：

```
```vb
Public Class Employee

    Public Property HireDate() As Date

    Public Property Salary() As Double
End Class
```
```

这是一个普通的独立类，没有显式的继承。它可以用图 3-3 所示的类图表示。

再次，你可以看到类名、其实例变量列表，以及作为其接口一部分的属性。事实证明，在幕后，这个类从 System.Object 继承了一些功能。事实上，整个 .NET 平台中的每个类最终都隐式或显式地继承自 System.Object。这就是为什么所有 .NET 对象都有一个基本的一组通用功能，其中最值得注意的是 GetType 方法，该方法将在本章后面详细讨论。

虽然拥有具有入职日期和薪水的 Employee 对象是有用的，但它也应该具有 Name 和 BirthDate 属性，就像你在 Person 类中实现的那样。如果没有继承，你可能会直接将 Person 中的代码复制并粘贴到新的 Employee 类中，但有了继承，你就可以直接重用 Person 类中的代码。让我们使新类继承自 Person。

![](img/d99870e80390742f93963da7be0b2e61_161_0.png)

## Inherits 关键字

要使 Employee 成为 Person 的子类，添加一行代码：

```
```vb
Public Class Employee
    Inherits Person
```
```

Inherits 关键字表示一个类应该从现有类派生，继承该类的接口和行为。你可以从项目中的几乎任何类、.NET 系统类库或其它程序集中继承。它也可以防止继承，这将在本章后面介绍。当使用 Inherits 关键字从当前项目之外的类继承时，你需要指定包含该类的命名空间，或者在类的顶部放置一个 Imports 语句以导入该命名空间供你使用。

图 3-4 中的图表说明了 Employee 类现在是 Person 的子类这一事实。

从 Employee 向上连接到 Person 的线以一个开放三角形结束，这是使用 Visual Studio 中的 Class Designer 时表示继承的符号。正是这条线表明 Employee 类包含了 Person 的所有功能以及接口。

这意味着基于 Employee 类创建的对象不仅具有 HireDate 和 Salary 方法，还具有 Name 和 BirthDate。为了测试这一点，打开 Form1 的设计器

![](img/d99870e80390742f93963da7be0b2e61_161_1.png)

（因为你创建了一个 Windows Forms Application 项目，它会自动成为你的项目的一部分）并向窗体添加以下 TextBox 控件以及一个按钮：

| 控件类型 | 名称 | TEXT 属性值 |
|---|---|---|
| TextBox | txtName | <blank> |
| TextBox | txtBirthDate | <blank> |
| TextBox | txtHireDate | <blank> |
| TextBox | txtSalary | <blank> |
| button | btnOK | OK |

你也可以添加一些标签使窗体更易读。Form Designer 现在应该看起来像图 3-5。

![](img/d99870e80390742f93963da7be0b2e61_162_0.png)

图 3-5

双击按钮以打开代码窗口并输入以下代码：

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click
    Dim emp As New Employee()

    With emp
        .Name = "Fred"
        .BirthDate = #1/1/1960#
        .HireDate = #1/1/1980#
        .Salary = 30000

        txtName.Text = .Name
        txtBirthDate.Text = Format(.BirthDate, "Short date")
        txtHireDate.Text = Format(.HireDate, "Short date")
        txtSalary.Text = Format(.Salary, "$0.00")
    End With
```

来自 Person 的代码片段

> 最佳 Visual Basic 实践是使用 With 关键字，但请注意这可能会导致可移植性问题以及将代码转换为其它语言的问题。

即使 Employee 没有直接实现 Name 或 BirthDate 方法，它们也可以通过继承使用。当你运行此应用程序并单击按钮时，你的控件将被 Employee 对象的值填充。

当 Form1 中的代码在 Employee 对象上调用 Name 属性时，Person 类中的代码将被执行，因为 Employee 类本身没有这样的方法。然而，当在 Employee 对象上调用 HireDate 属性时，Employee 类中的代码将被执行，因为它确实在其代码中具有该方法。

从窗体的角度来看，方法是在 `Employee` 类中实现还是在 `Person` 类中实现并不重要；它们都是 `Employee` 对象的简单方法。此外，由于这些类中的代码被合并以创建 `Employee` 对象，因此调用由 `Employee` 类实现的方法与调用由 `Person` 类实现的方法之间没有性能差异。

## 方法重载

尽管你的 `Employee` 类通过继承自动获得了 `Name` 和 `BirthDate` 方法，但它也有自己的方法——`HireDate` 和 `Salary`。这显示了你通过向 `Employee` 子类添加方法和属性来扩展了基 `Person` 接口。

你可以向 `Employee` 类添加新的属性、方法和事件，它们将成为基于 `Employee` 创建的任何对象的一部分。这对 `Person` 类完全没有影响，只影响 `Employee` 类和 `Employee` 对象。

你甚至可以通过向子类添加与基类中方法和属性同名的方法来扩展基类的功能，只要这些方法和属性具有不同的参数列表。你实际上是在重载来自基类的现有方法。这与第 2 章中讨论的重载常规方法本质上是相同的。

例如，你的 `Person` 类目前为 `Name` 属性提供了你的实现。员工可能还有其它你也想存储的名称，也许除了常规名称外还有一个非正式名称和正式名称。满足此要求的一种方法是更改 `Person` 类本身以包含支持此新功能的重载 `Name` 属性。然而，你实际上只是在增强 `Employee` 类，而不是更通用的 `Person` 类，所以你想要的是在 `Employee` 类本身添加一个重载方法的方式，即使你正在重载其基类的方法。

你可以使用 `Overloads` 关键字来重载基类的方法。概念与第 2 章中描述的相同，但在这种情况下涉及一个额外的关键字。例如，要重载 `Name` 属性，你可以向 `Employee` 类添加一个新属性。首先，定义一个使用 `Enum` 关键字的枚举类型。此 `Enum` 将列出你想要存储的不同类型的名称。将此 `Enum` 添加到 `Employee.vb` 文件中，在类本身的声明之前：

```
Public Enum NameTypes
    Informal = 1
    Formal = 2
End Enum

Public Class Employee
```

然后你可以向 `Employee` 类本身添加一个重载的 `Name` 属性：

```
Public Class Employee
    Inherits Person

    Public Property HireDate As Date
    Public Property Salary As Double
    Private mNames As New Generic.Dictionary(Of NameTypes, String)
    Public Overloads Property Name(ByVal type As NameTypes) As String
        Get
            Return mNames(type)
        End Get
        Set(ByVal value As String)
            If mNames.ContainsKey(type) Then
                mNames.Item(type) = value
            Else
                mNames.Add(type, value)
            End If
        End Set
    End Property
```
