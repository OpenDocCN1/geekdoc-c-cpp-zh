
每个类应当负责自己的数据，并且只能通过 Property、Set 和 Get 过程来共享变量。

*注意：* 早期版本的 VB 以及许多其他编程语言，将可在项目中任何位置引用的变量称为*全局变量*。VB 已弃用这一术语。

## 模块级

**模块级作用域**有时也称为*类级作用域*。模块级变量是在任何类、结构或模块内部但在任何子过程或函数外部声明的 Private 变量。按照约定，应在类的顶部声明模块级变量，但实际上可以在类内部、过程或函数之外的任何位置声明这些变量。

```
Private TotalDecimal As Decimal
```

*注意：* 如果省略可访问性修饰符（*Public* 或 *Private*），则变量默认为 Private。

在 Visual Basic 的某些早期版本中，每个文件都称为一个模块，因此在文件顶部（而不是在子过程或函数内部）声明的任何变量都是模块级变量。这一术语沿用到当前版本的 VB，尽管该语言现在具有 Module / End Module 构造，可以包含不属于类的各种过程和函数。

## 过程级

在过程或函数内部但不在块内声明的任何变量都具有过程级作用域，也称为局部作用域。可以在过程内部的任何位置引用该变量，但不能在其他过程中引用。请注意，Public 关键字在过程内部是非法的；所有过程级变量都是私有的，并使用 Dim 关键字声明。

## 块级

如果在代码块内声明变量，则该变量具有块级作用域。也就是说，只能在该块内引用该变量。代码块包括

```
If / End If
Do / Loop
For / Next
Select Case / End Select
Try / Catch / Finally / End Try
```

可能引起混淆的块是 Try / Catch / Finally / End Try。Try 是一个块；每个 Catch 是独立的块；Finally 也是独立的块。这意味着不能在 Try 中声明变量然后在 Catch 或 Finally 块中引用它。这也意味着可以为每个 Catch 声明相同的变量名，因为每个变量的作用域仅限于该 Catch 块。

```
Try
    ' Declare a block-level variable.
    ' Bad idea, since it cannot be referenced outside of this Try block.
    Dim AmountDecimal As Decimal = Decimal.Parse(AmountTextBox.Text)
Catch Err As InvalidCastException
    ' Err is a block-level variable valid only inside this Catch block.
    MessageBox.Show(Err.Message, "Invalid Input Data.")
Catch Err As Exception
    ' Err is a block-level variable valid only inside this Catch block.
    MessageBox.Show(Err.Message, "Unknown Error.")
Finally
    ' Any variable declared here is valid only inside this Finally block.
End Try
```

在实例化对象时，如果创建有可能失败，就应该在 Try/Catch 块内创建新对象。但是，如果在 Try 块内声明变量，当 Try 块完成时该变量将超出作用域。因此，大多数情况下，应在模块级或过程级声明对象变量，并在 Try 块内实例化该对象。

```
' Declare the object variable at the module level.
Private APayroll As Payroll

Private Sub CalculateButton_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles CalculateButton.Click
    ' Create a Payroll object to connect to the business services tier.

    Try
        ' Instantiate the object in the Try block.
        APayroll = New Payroll(Decimal.Parse(Me.HoursTextBox.Text), _
            Decimal.Parse(Me.RateTextBox.Text))
    Catch ...
```

## 生存期

变量的生存期（包括对象变量）与变量保持在作用域内的时间一样长。命名空间级变量的生存期与程序运行时间相同。模块级变量的生存期与对该类的任何引用存在的时间相同，通常与程序运行时间相同。

过程级变量的生存期是过程的一次执行。每次执行过程时，都会建立并初始化一个新变量。因此，不能使用过程级变量来维护累计总数或计数，除非使用 Static 关键字声明它们，这将把过程级变量的生存期更改为类或模块的生存期。

## 可访问性域

你已经使用 Public 和 Private 关键字声明了变量和类。还可以使用 Protected、Friend 和 Protected Friend（表 2.1）。这些关键字中的每一个都定义了变量或类的可访问性。

## 声明可访问性域的关键字

### 表 2.1

| 关键字 | 描述 |
|---|---|
| Public | 可从项目中的任何位置或引用此项目的任何其他项目访问。 |
| Private | 可从此类中的任何位置访问。 |
| Protected | 可从此类内部或继承此类的任何类中的任何位置访问。 |
| Friend | 可从该项目/程序集中的任何位置访问。 |
| Protected Friend | Protected 和 Friend 的组合。可从该项目/程序集中的任何位置以及继承此类的任何类中访问，即使派生类位于不同的项目/程序集中。 |

## 创建继承类

要创建继承类，首先应向项目添加一个新类。尽管单个文件可以包含多个类定义，但推荐的方法是为每个 Public 类创建一个新文件，并使文件名与类名匹配。唯一的例外是永远不会被其他应用程序使用的小型“辅助类”。这些辅助类应使用 Friend 关键字声明，因为它们仅用于当前项目。

## 添加新类文件

通过选择“项目 / 添加类”为类添加新文件，这将创建一个扩展名为 .vb 的新文件。确保为类指定你想要使用的名称；文件将被正确命名，解决方案和项目也将使用正确的名称进行设置。

新添加的类将具有以下第一行和最后一行代码：

```
Public Class ClassName
End Class
```

在 Class 声明之后的第一行上添加 Inherits 子句，并在 Class 语句上方添加注释。

```
'Project: Ch02PayrollInheritance
'Module: PayrollSalaried Class
'Programmer: Bradley/Millspaugh
'Date: June 2009
'Description: A class in the business services tier for payroll calculation:
' validates input data and calculates the pay for
' salaried employees.

Public Class PayrollSalaried
    Inherits Payroll
End Class
```

## 创建构造函数

子类必须有自己的构造函数，因为构造函数不会被继承。但是，如果不创建构造函数（Sub New），VS 会创建一个隐式的空构造函数。

继承类的构造函数中的第一条语句应使用 MyBase 关键字调用基类的构造函数：

```
MyBase.New()
```

如果基类只有参数化构造函数，则必须向构造函数传递参数。

```
MyBase.New(HoursDecimal, RateDecimal)
```

与基类一样，你可以拥有多个重载的 New 构造函数，每个构造函数对应基类的一个签名。

## 继承变量和方法

如你所知，当从现有类派生新类时，所有 Public 和 Protected 变量和方法都会被继承，但基类的构造函数除外。

## 隐藏和重写方法

继承类可以具有与其基类中方法同名的方法。根据声明方式的不同，新方法可能会隐藏（shadow）或重写（override）基类方法。

### 重写

要重写基类中的方法，必须将该方法声明为可重写（overridable）：

```
' Base Class.
Public|Protected Overridable Sub DoSomething()
```

在派生类中，必须使用 Overrides 关键字，并具有与基类相同的可访问性（Public|Private）：

```
' Derived Class.
Public|Protected Overrides Sub DoSomething()
```

如果基类方法有多个签名（重载方法），则重写仅适用于具有相同签名的基类方法。必须编写单独的方法来重写基类方法的每个版本（签名）。

### 隐藏

派生类中的方法可以隐藏基类中的方法。新的（隐藏）方法将替换派生类中的基类方法，但不会替换从该类派生的任何新类中的方法。隐藏方法会“隐藏”基类中所有同名的签名（重载方法）。
