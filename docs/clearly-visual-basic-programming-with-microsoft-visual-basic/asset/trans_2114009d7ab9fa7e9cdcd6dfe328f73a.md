

### 在 RectangularPool 类定义中输入默认构造函数

- **1.** 在最后一个 End Property 子句下方插入两个空行，然后键入 **Public Sub New** 并按 **Enter**。注意，代码编辑器会在默认构造函数名称后添加一对括号。
- **2.** 键入以下注释和代码行。

```vbnet
' default constructor
_decLength = 0
_decWidth = 0
_decDepth = 0
```

## 构造函数以外的方法

类还可以包含构造函数以外的方法。除了构造函数必须是 Sub 过程外，类中包含的方法可以是 Sub 过程或 Function 过程。回顾第 18 章，Function 过程在执行其分配的任务后返回一个值，而 Sub 过程不返回值。图 27-7 展示了一个非构造函数方法的语法。语法中的 {Sub | Function} 表示只能选择花括号内出现的关键字之一。与属性名一样，方法名应使用 Pascal 大小写形式输入。但是，与属性名不同，方法名中的第一个单词应为动词，后续单词应为名词和形容词。图 27-7 示例中使用的方法名 GetVolume 遵循此命名约定。

**语法**

```vbnet
Public {Sub | Function} methodName([parameterList]) As dataType
    instructions
End {Sub | Function}
```

**示例**

```vbnet
Public Function GetVolume() As Decimal
    Return _decLength * _decWidth * _decDepth
End Function
```

**图 27-7：** 非构造函数方法的语法和示例

如前所述，RectangularPool 对象应能够计算并返回其体积，以及计算并返回注满它所需的水的加仑数。要让 RectangularPool 对象执行这些任务，需要在类定义中包含两个额外方法：GetVolume 和 GetGallons。这两个方法都将是 Function 过程，因为每个方法都需要向包含该对象的应用程序返回一个值。

### 在 RectangularPool 类定义中输入 GetVolume 和 GetGallons 方法

- **1.** 在 End Sub 子句下方插入两个空行，然后键入 **public function GetVolume as decimal** 并按 **Enter**。这里同样，代码编辑器会在函数名后插入一对括号。键入 **return _decLength * _decWidth * _decDepth**。
- **2.** 在 End Function 子句下方插入两个空行。键入 **public function GetGallons as decimal** 并按 **Enter**。
- **3.** 回顾一下，通过将体积乘以 7.48 来确定水的加仑数。可以使用类的 GetVolume 方法获取体积。首先，声明一个变量来存储体积。键入 **dim decVol as decimal** 并按 **Enter**。然后键入 **decVol = GetVolume** 并按 **Enter**。注意，代码编辑器会在方法名后添加一对括号。现在键入 **return decVol * 7.48**，然后单击代码编辑器窗口中的**另一行**。
- **4.** 将你输入的代码与图 27-8 中显示的代码进行比较。进行任何必要的更正，然后保存解决方案。

```vbnet
Public Class RectangularPool
    Private _decLength As Decimal
    Private _decWidth As Decimal
    Private _decDepth As Decimal

    Public Property Length() As Decimal
        Get
            Return _decLength
        End Get
        Set(ByVal value As Decimal)
            If value >= 0 Then
                _decLength = value
            Else
                _decLength = 0
            End If
        End Set
    End Property

    Public Property Width() As Decimal
        Get
            Return _decWidth
        End Get
        Set(ByVal value As Decimal)
            If value >= 0 Then
                _decWidth = value
            Else
                _decWidth = 0
            End If
        End Set
    End Property

    Public Property Depth() As Decimal
        Get
            Return _decDepth
        End Get
        Set(ByVal value As Decimal)
            If value >= 0 Then
                _decDepth = value
            Else
                _decDepth = 0
            End If
        End Set
    End Property

    Public Sub New()
        ' default constructor
        _decLength = 0
        _decWidth = 0
        _decDepth = 0
    End Sub

    Public Function GetVolume() As Decimal
        Return _decLength * _decWidth * _decDepth
    End Function

    Public Function GetGallons() As Decimal
        Dim decVol As Decimal
        decVol = GetVolume()
        Return decVol * 7.48
    End Function
End Class
```

**图 27-8：** 完整的 RectangularPool 类定义

## 使用模式创建对象

定义类后，便可以使用它来实例化一个或多个对象。图 27-9 展示了完成此任务的两种基本语法版本。在两个版本中，*className* 是类的名称，*variableName* 是将对象存储在计算机内部内存中的变量名称。两个版本的区别在于对象实际创建的时间。计算机仅在处理包含 **New** 关键字的语句时才创建对象。如前面所学，**New** 是类构造函数的名称。回顾一下，构造函数负责创建对象并为 Private 变量赋初始值。图 27-9 还包含使用每种语法版本的示例。在示例 1 中，Private pool As RectangularPool 指令创建一个名为 pool 的模块级变量，该变量可存储 RectangularPool 对象；但是，它不创建对象。直到计算机处理 pool = New RectangularPool 语句时，才创建对象。该语句将对象赋给 pool 变量。在示例 2 中，Dim pool As New RectangularPool 指令创建一个名为 pool 的过程级变量。它还实例化一个新的 RectangularPool 对象并将其赋给该变量。

| 从类实例化对象 |
|---|
| **语法—版本 1**<br>**{Dim \| Private}** *variableName* **As** *className*<br>*variableName* = **New** *className*<br><br>**语法—版本 2**<br>**{Dim \| Private}** *variableName* **As New** *className*<br><br>**示例 1—版本 1 的语法**<br>Private pool As RectangularPool<br>pool = New RectangularPool<br>第一条指令声明一个名为 pool 的 RectangularPool 变量；第二条指令实例化一个 RectangularPool 对象，初始化其 Private 变量，并将该对象赋给 pool 变量 |

**图 27-9：** 实例化对象的基本语法版本和示例

## 软件工程

- 项目管理
- 需求工程
- 软件设计
- 实现
- 测试
- 维护

软件工程是将工程方法系统化地应用于软件开发。

![](img/cf88270932e011575089da06b940a1d9_630_0.png)

![](img/cf88270932e011575089da06b940a1d9_631_0.png)

**图 27-10：** RectangularPool 对象的属性和方法列表

- **6.** 如有必要，单击列表中的 **Length**，然后按 **Tab**。单击代码编辑器窗口中的**另一行**。
- **7.** 自行将第二个 TryParse 方法中的 poolSize.decWidth 改为 **pool.Width**，并将第三个 TryParse 方法中的 poolSize.decDepth 改为 **pool.Depth**。
- **8.** 现在使用类的 GetVolume 方法获取体积。在最后一个 TryParse 方法下方的语句中选择 CalcVolume(poolSize)，然后键入 **pool.**（务必键入句点）。单击列表中的 **GetVolume**，然后按 **Tab**。
- **9.** 最后，使用类的 GetGallons 方法获取加仑数。自行将 decPoolVolume * 7.48 改为 **pool.GetGallons**。图 27-11 显示了修改后的 Click 事件过程。你对过程所做的更改在图中以底纹显示。

```vb
Private Sub btnCalc_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnCalc.Click
    'calculates volume and number of gallons
    Dim pool As New RectangularPool
    Dim decPoolVolume As Decimal
    Dim decGallons As Decimal

    Decimal.TryParse(txtLength.Text, pool.Length)
    Decimal.TryParse(txtWidth.Text, pool.Width)
    Decimal.TryParse(txtDepth.Text, pool.Depth)

    decPoolVolume = pool.GetVolume
    decGallons = pool.GetGallons

    lblVolume.Text = decPoolVolume.ToString("N0")
    lblGallons.Text = decGallons.ToString("N0")
End Sub
```

**图 27-11：** btnCalc 控件修改后的 Click 事件过程

