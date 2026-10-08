
# <Project Name>

将项目命名为“`VS VB Simple Class Proj`”
`<OK>`

在表单的空白处点击右键并选择属性（`properties`）。
将表单的文本（`text`）属性设置为“`VS VB Simple Class Proj`”，并将启动位置（`Start-up Location`）设置为居中（`Center Screen`），然后向表单添加以下控件：

- 7 个名为 `txtBoxCarMaker`、`txtBoxModel`、`txtBoxCarType`、`txtBoxEngine`、`txtBoxCost`、`txtBoxCarColor` 和 `txtBoxModelYr` 的文本框（`textboxes`）。
- 8 个与文本框对应的标签（`labels`），将属性“`enabled`”属性设置为 False。
- 4 个名为 `btnSave`、`btnDisplay`、`btnClear` 和 `btnExit` 的按钮。

根据你的喜好设置其他属性 . . 例如字体（`Font`）、背景颜色（`BackColor`）等。

根据需要将控件拖到表单上的合适位置。

在顶部任务栏上点击 `<View><Tab Order>`

注意：每个控件上都会出现白色矩形，显示制表顺序数字。点击第一个控件（`textBox`）的制表顺序，用户将输入信息，例如汽车制造商、型号等 . . . 逐个点击，直到制表顺序符合用户输入所需信息的顺序。制表顺序决定了用户按下按键时，光标在控件之间移动的顺序。

`MVS`（Microsoft Visual Studio）另一个需要注意并利用其优势的功能是智能提示（`intellisense`）。当你使用“点符号表示（Dot Notation）”来“设置”或“获取”类的属性时 . . 在输入“点（`.`”后，你会看到下拉菜单中列出的所有可用属性。点击你选择的属性，它将精确地输入到代码中，与你在类中定义的属性完全一致。使用 MVS 的这一功能有助于防止拼写错误和其他错误。这意味着你不需要依靠记忆来确保使用了所有属性。

我们完成的项目在用户输入信息、保存并显示它们后，将生成一个像所示的屏幕 . . . (`img/a3c8d8cba71ab82fe2f1c28dd8b56f186_0.png`)

## 屏幕

在我们编写事件处理块之前，让我们定义一下将在事件处理程序中引用的“类”。在解决方案管理器（`Solution Explorer`）中，“右键点击”`<project name>`并选择`<Add>`。弹出菜单后点击`<New Item>`。接下来选择 `<Class>`（类），将类重命名为 `<Automobile>`，点击`<Add>`。几秒钟后，`AutomobileClass` 将作为一个文件出现在解决方案管理器中 . . . 双击类名。现在你应该处于 `AutomobileClass` 的骨架代码块中了。

我们将为该类定义七个属性。

注意：注释超级重要 . . 它们让我们意识到自己正在处理哪个“属性”，并使查找和纠正错误变得容易得多。

```vbnet
Public Class AutomobileClass // 公共，即可以在项目的其他地方访问

    ########## HorsePower

    Private intHorsePower As Integer // 私有 . . 仅在此类内部访问 . . .

    Public Property intEngineHP() As Integer //当我们引用此属性时，将使用公共属性名 . . 意味着可以接受或返回值。引用将使用“点”符号，例如 AutomobileClass.intEngineHP

        Get // 处理值的“调用”

            Return intHorsePower // 返回值给“调用者”

        End Get

        Set(value As Integer) // 接收并将“调用”中的参数赋值给“Set”值，由MVS自动生成的特殊变量 value "As Integer"必须由我们的代码添加

            intHorsePower = value

        End Set

    End Property 遵循此模式，// 当传入参数为数字时，使用每个整数或小数

    // 下一个“属性”大 same

    ########## Car Class

    Private strCarClass As String

    Public Property strType()

        Get

            Return strCarClass

        End Get

        Set(value) // string 是默认的 "value" 变量类型

            strCarClass = value

        End Set

    End Property //----------------

    ########## Car Class

    Private decCarPrice As Decimal

    Public Property decCarCost() As Decimal

        Get

            Return decCarPrice

        End Get

        Set(value As Decimal)

            decCarPrice = value

        End Set

    End Property // ########### Car Manufacturer

    Private strCarManufacturer As String

    Public Property strCarMaker() As String

        Get

            Return strCarManufacturer

        End Get

        Set(value As String) // String 是默认的，仅为了清晰而输入

            strCarManufacturer = value

        End Set

    End Property ##################### Car Model

    // #############################

    Private strCarModel As String

    Public Property strCarModelDesc() As String

        Get

            Return strCarModel

        End Get

        Set(value As String)

            strCarModel = value

        End Set

    End Property

    // 下一个属性 . . . .

    // ################################# Car Model

    Private strCarYear As String

    Public Property strCarYr() As String

        Get

            Return strCarYear

        End Get

        Set(value As String)

            strCarYear = value

        End Set

    End Property // ################################## Car Model
```

只需编程 C# 和 Visual Basic...

```vbnet
Set(value As String)

  strHairColor = value

End Set

End Property

End Class
```

现在我们已经定义了类，可以返回表单并输入事件处理代码了。在解决方案中点击 `<Form1>` 并使用 `<设计视图>`。

```vbnet
双击 btnSave 并输入事件处理代码.

// 注意：我们在这里使用 "Public" 是为了让信息在

// 其他地方可用
```

```vbnet
Public Sub btnSave_Click(sender As System.Object, e As System.EventArgs Handles btnSave.Click
    // 从 AutomobileClass 实例化一个活跃的“类”
    Dim mycls As Automobile = New AutomobileClass()

    //
    // 设置 mycls.strCarMaker 属性值
    // 字符串变量与 Automobile 属性定义中使用的属性“变量类型”匹配 . . 后面的所有内容也是如此。
    // 在此处使用整数。如果类中预期的变量是整数，// 类中预期的变量是字符串，则在此处使用字符串。变量类型必须匹配。
    //

    Dim strMfg As String = txtBoxMfg.Text
    mycls.strCarMaker = strMfg

    '/'

    Dim decCost As Decimal = txtPrice.Text
    mycls.decCost = Convert.ToDecimal(txtPrice.Text)

    '/'

    Dim myModel As String = txtModel.Text
    mycls.strCarModelDesc = myModel

    '/'

    Dim myModelYear As String = txtModelYr.Text
    mycls.strCarYr = myModelYear

    '/'

    Dim intMyEngine As Integer = txtEngine.Text
    mycls.intEngineHP = intMyEngine

    '/'

    Dim myCarColor As String = txtColor.Text
    mycls.strCarPaint = myCarColor

    '/'

    Dim myStyle As String = txtAutoStyle.Text
    mycls.strCarType = myStyle

    '/'

    myName = mycls
    mycls = Nothing
End Sub
```

在我们“实例化”的类“`myClass`”中设置属性值的操作就完成了。接下来，我们将编写代码来获取刚刚“设置”的属性值。

在解决方案中
`<Form1>`+设计视图>

双击 `<btnDisplay>`
输入事件处理代码。

```vbnet
Private Sub btnDisplayProperties_Click(sender As System.Object, e As System.EventArgs) Handles btnDisplayProperties.Click

// 我们正在使用“标签”来显示我们的属性值。

// 确保标签的 Autosize 属性为“False”

//

// 注意，我们正在为标签的 Text 属性“拼接”字符串。我们添加了“Visual Basic”

// “回车换”和“换行”字符，以便在标签中每行显示一个属性。

//

// 此外，注意引号内字面量字符串后面的“空格”，用以将属性值与字面量隔离开。

//

// 这使得显示的信息更易读。

//

lblDisplayProperties.Text = "Make " + mycls.strCarMaker
lblDisplayProperties.Text = lblDisplayProperties.Text + vbCrLf + "Model " + mycls.strCarModelDesc
lblDisplayProperties.Text = lblDisplayProperties.Text + vbCrLf + "Car Class " + mycls.strCarType
lblDisplayProperties.Text = lblDisplayProperties.Text + vbCrLf + "Year " + mycls.strCarYr
lblDisplayProperties.Text = lblDisplayProperties.Text + vbCrLf + "Price $" + Convert.ToString(mycls.decCost)
lblDisplayProperties.Text = lblDisplayProperties.Text + vbCrLf + "Color " + mycls.strCarPaint
lblDisplayProperties.Text = lblDisplayProperties.Text + vbCrLf + "Horse Power " + Convert.ToString(mycls.intEngineHP)

// 确保标签可见

lblDisplayProperties.Visible = True
End Sub
```

大搞定！！运行程序，输入一些信息并保存，然后显示你设置的属性。稍后我们将学习永久地保存信息，一步到位。休息一下，你得的！！！VB 代码的完整副本位于附录 I。C# 代码位于附录 J。

## 下一个结构

与类相比，一种稍微不复杂且易于使用的存储设备是另一种用户定义变量。它具有许多与类处理不同类型变量相同的功能，例如整数和字符串可以在结构体中共存。如果需要，结构体也可以定义在类块“内部”，或者像我们对类做的那样将其放在自己的容器中。它们可以其他变量一样被复制并保存到硬盘上。我们将结构体放在它自己的“类”容器中，并命名为“`StructurePropertyDemo`”。

我们将首先定义结构体，向我们的表单添加控件和事件处理块。这使得编写表单代码变得更容易，因为 IntelliSense 会在我们需要时为结构体的属性提供引用。

启动 VS... `<工具> <项目和解决方案>` 将位置设置为你的 VS 项目文件夹。`<确定> <文件> <新建项目> <Visual Basic> <Windows 表单>` 命名项目为 ... `VS Struct` `<确定>` 当空表单出现时，忽略它几分钟。在解决方案中，右键点击项目名称，然后 `<添加> <新建项> <类>` 将类命名为 `StructurePropertyDemo` `<添加>` 当类文件在解决方案中出现时，双击文件名进入代码块。删除所有内容，在新类代码中重复“所有”骨架代码然后 ... 输入此代码。

## 简单编程 C# 和 Visual Basic . . .

将表单的文本属性更改为
`VB Structure_Property_Form`

现在，双击表单上的空白处，我们将进入 `Form1_Load` 事件处理程序块。我们将使用 `Load_Event` 来定义和初始化结构体（`Struct`），并在添加到表单的标签（`labels`）中显示属性的内容。

在屏幕的最上方，紧接此行下方：
`Public Class Structure_Property_form`

添加此行代码 . . .
// 实例化结构体的可工作实例
`Public newStruct As New StructurePropertyDemo`

在 `Form1_Load` 事件处理程序内部添加以下代码：

```vb
// 这行应该已经存在；

// Public Sub Structure_Property_form_Load(sender
// As System.Object, e As System.EventArgs) Handles
// MyBase.Load

//
```

```vb
// 使用“点”符号法设置 newStruct 属性
// 以访问 newStruct 的属性
//

newStruct.CarMaker = "Ford" // #1
newStruct.CarModel = "2004" // #2
newStruct.CarEngine = 140 // CarEngine #3
newStruct.CarColor = "Red"
newStruct.Color = "Maroon" // #4
newStruct.CarOwner = "Personal" // #5
//newStruct.Financing = "CapitalOne" . . 读取
// 只有这一行会产生错误.. 我们不能在这里“重设”它。
// 它在定义结构体时已经被“设置”了 . . #6
newStruct.CarPrice = 14200 // #7
//
// 显示 newStruct 的属性
//

1blMaker.Text = newStruct.CarMaker // # 1
1blModel.Text = newStruct.CarModel // # 2
// newStruct 属性 "Engine" 是整数，
// 它必须
// 转换为字符串以便标签显示
1blEngine.Text = Convert.ToString(newStruct.CarEngine) // # 3
1blColor.Text = newStruct.Color // # 4 使用 newStruct 中的
// 公有字符串变量 Color
1blColor.Text = newStruct.CarColor // # 4 使用属性
// CarColor . . 均可行
1blOwnership.Text = newStruct.CarOwner // # 5
1blFinancier.Text = newStruct.Financing // # 6
// newStructCarPrice 是整数，它必须
// 转换为字符串以便标签中显示
```
