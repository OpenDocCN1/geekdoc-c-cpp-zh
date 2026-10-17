
# 代码片段

```vb
7295 Return CarPaint

7296 End Get

7297 //

7298 Set(ByVal value As String)

7299 CarPaint = value

7300 End Set

7301 //

7302 End Property // . . Property #5 CarModel

7303 //

7304 //

7305 Public Property Financing() As String

7306 Get

7307 Return Banker

7308 End Get

7309 Set(ByVal value As String)

7310 Banker = value

7311 End Set

7312 End Property // . . Property #6 Financing

7313 Public Property CarOwner() As String

7314 Get

7315 Return Ownership

7316 End Get

7317 //

7318 Set(ByVal value As String)

7319 Ownership = value

7320 End Set

7321 //

7322 End Property // . . Property #7 CarOwner

7323 Public Property CarPrice() As String

7324 Get

7325 Return CarCost

7326 End Get

7327 Set(value As String)

7328 CarCost = value

7329 End Set

7330 End Property // . . Property #8 CarPrice

7331 //

7332 End Structure
```

# 表单和事件处理代码

现在来处理表单和事件处理代码。

你选择何种顺序编写事件处理程序其实并不重要。但在代码块中，如果每次都以相同的顺序处理属性并在注释中对其编号，会更简单一些。

但是，有时字符串中会存在“不可见”的错误。

在打字时，你可能会击到一个无法显示的“控制”字符。

如果代码块执行失败而你没有在字符串中看到任何错误，请删除该字符串并从可以正常工作的地方复制它——或者作为最后的手段，重新输入整个字符串（“包括”周围的括号和引号）。

发现并纠正错误是编程中最困难的部分。在处理过程中对项目进行编号会变得更容易，特别是处理那些从各种对象属性填充的字符串。

## 为表单命名

`. .` 使用下划线符号（不要在名称中留空格）`Structure_Property_with_File_IO`。在文本属性中输入相同的名称。

在表单上添加这些控件并按所示命名；
- 8 个文本框 `textBox`，10 个标签 `label`，6 个按钮 `button`，1 个列表框 `ListBox`。

按照你看到的照片在表单上排列控件——或者如果你有更好的想法，尽管去用吧！！标签用于提示用户应该输入或点击的内容，通常还有一个针对整个项目的大型说明/指令说明标签。

- 8 个文本框, 6 个按钮, 10 个标签
- `txtBoxMfg` `btnDisplay` 随你喜欢命名
- `txtBoxModel` `btnSaveToFile`
- `txtBoxStyle` `btnClear`
- `txtBoxEngine` `btnDelete`
- `txtBoxColor` `btnEditSelectedRecord`
- `txtBoxFinancer` `btnSaveEdits`
- `txtBoxOwner` `ArrayList`
- `txtBoxCost` `myArrayLst`
- `listBox1` 保持默认名称

我们将在代码中创建 `ArrayList`，对用户是不可见的。它是我们结构体 `Struct` 的存储设备。

一旦在 MVS 工具栏 `<视图>` 中将控件添加到表单，表单上会出现包含默认标签顺序的矩形。点击矩形可以更改标签顺序。

收集信息的优先顺序是；
`(1)` 制造商, `(2)` 车型, `(3)` 样式, `(4)` 引擎, `(5)` 颜色, `(6)` 融资方, `(7)` 所有者和 `(8)` 价格。文本框和相关标签应该以此方式排列。垂直——或根据你的喜水平，但要按照此顺序和标签顺序。点击文本框旁的矩形直到它变为零 `(0)`。点击下一个控件（型号）的矩形直到它变为一 `(1)`。继续这样做，直到 8 个文本框按照按顺序处理项目的顺序顺序排列，我保证这将最大限度地减少你的错误。这将使用户按 `Tab` 键在控件之间移动非常方便。听起来很简单，但对用户来说是一个巨大的加分项，特别是当他们为此付费时。

我选择先编写 `btnDisplay` 事件处理程序。通常，在我们设置原始记录之前，我想用户会想查看文件中有什么记录。偶尔，用户可能会“添加”、“保存”或删除记录，但可能较少。让我们开始；到这里你已经知道如何操作了。此类的顶部部分如下：

```csharp
Imports System
Imports System.Array
Imports System.IO
Imports System.IO.DirectoryNotFoundException

Public Class Structure_Property_form
Public newStruct As AutomobileSpecs
Public myArrayLst As ArrayList
Public myObjIdx As Integer = 0
Public intSelected As Integer
Public intEditIdx As Integer
```

某些变量声明为 `Public` 以便我们在程序中使用它们。

`btnDisplay_Click(sender As System.Object, e As System.EventArgs) Handles btnDisplay` 声明并初始化 `StreamReader`

```vb
Dim myRdr As StreamReader
myRdr = New StreamReader("C:\App Target Files\AutomobileStruct.txt")
```

确保这是文件的准确路径、空格、大写字母等（所需的）。这是一个非常容易出错的地方，而且有时很难发现。

例如；
`myFileTest = My.Computer.FileExists("C:\App Target Files\AutomobileStruct.txt")`
`("C:\App Target Files\AutomobileStruct.txt")` 这是比较两个字符串的好方法 . . 将一个放在另一个下面作为注释

```csharp
// If (myfileTest = True) Then
// My.Computer.FileSystem.DeleteFile("C:\App Target Files\AutomobileStruct.txt")
// End If
```

如果 `myfileTest` 为 `True`，第二个命令应该正确执行。如果它没有执行，说明你在字符串中嵌入了不可见的控制字符。即：

第一个第一个命令可能是正常的并正确执行，返回 `True`，因为你“知道”文件存在。下一个命令可能会失败，因为你的字符串中有一个不可见的控制字符。是的，这种情况会发生！！！错误的结果是？你的文件中出现了垃圾，有时文件中会有两份相同的信息，这也是垃圾。

好了，话虽如此，让我们仔细。正确获取 get 字符串。

```csharp
// btnDisplay Sub btnDisplay_Click(sender As System.Object, e As System.EventArgs) Handles btnDisplay.Click
// 声明并初始化 StreamReader
Dim myRdr As StreamReader
myRdr = New StreamReader("C:\App Target Files\AutomobileStruct.txt")
// 读取文件并设置结构体属性
Dim myStrFromFile As String = ". . // 防止“While”
```

216 John Queen

```vb
7520 // 防止因空字符串导致失败。
7521 // 声明整数变量来计数
7522 // 我们读取的记录
7523 Dim intRecordCount As Integer = 0

7525 While myStrFromFile <> "" // 开始文件
7526 读取
7527 // <> 意味着不等于，"" 表示空。
7528 // "English" . . 当 myStrFromFile
7529 不为空时
7530 // 执行以下命令。
7531 // 声明并读取一个字符串。
7532 // 我知道 CarBuilder 是第一个，这是我们
7533 写入文件的方式。
7534 Dim myCarBuilder As String = "" // 属性 #1
7535 // 注意属性的编号。
7536 myCarBuilder = myRdr.ReadLine()
7537 //
7538 // 检查文件末尾，当我们到达
7539 末尾时停止。
7540 If (myCarBuilder = "" Or myCarBuilder =
7541 Nothing) Then
7542 myRdr.Close()
7543 myRdr.Dispose()
7544 Exit Sub // 当我们得到空
7545 字符串时退出
7546 End If // 结束
7547 // 将字符串 "myCarBuilder" 赋值给
7548 newStruct.CarMaker
7549 属性。
7550 newStruct.CarMaker = myCarBuilder
```

## 简单编程 C# 和 Visual Basic ...

```vb
7562 Dim myAutoMod As String = "" // 属性 #2
7563 myAutoMod = myRdr.ReadLine()
7564 newStruct.CarModel = myAutoMod
7565 //
7566 Dim myAutoStyle As String = "" // 属性 #3
7567 myAutoStyle = myRdr.ReadLine()
7568 newStruct.CarStyle = myAutoStyle
7569 //
7570 Dim myAutoColor As String = "" // 属性 #4
7571 myAutoColor = myRdr.ReadLine()
7572 newStruct.CarColor = myAutoColor
7573 //
7574 Dim myCarHP As String = "" // 属性 #5
7575 myCarHP = myRdr.ReadLine()
7576 newStruct.CarEngine = myCarHP
7577 //
7578 Dim myAutoOwner As String = "" // 属性 #6
7579 myAutoOwner = myRdr.ReadLine()
7580 newStruct.CarOwner = myAutoOwner
7581 //
7582 Dim myLoan As String = "" // 属性 #7
7583 myLoan = myRdr.ReadLine()
7584 newStruct.Financing = myLoan
7585 //
7586 Dim myAmt As String = "" // 属性 #8
7587 myAmt = myRdr.ReadLine()
7588 newStruct.CarPrice = myAmt
7589 //
7590 // 已完成文件中 1 条记录的
7591 8 行）的读取。
7592 Dim myListing As String = "" // 在这里
7593 创建，
7594 // 不是从文件中读取的。
7595 // 拼接一个字符串显示在
7596 listBox 中
7597 // 使用我们从文件中读取的字符串。
7598 myListing = myCarBuilder & "" & myAutoMod &
7599 "" & myAutoOwner
7600 //
7601 // 增加文件记录计数器
7602 // "intRecordCount"
7603 intRecordCount = intRecordCount + 1
```

218

John Queen

```vb
7604   // 将对象/Struct 添加到 ArrayList
7605   myArryLst.Add(newStruct)
7606   // 将列表项添加到 listBox1。
7607   ListBox1.Items.Add(myListing)
7608   End While // 结束 "While" . . . 完成
7609   读取一条记录
7610   // 如果没有得到空字符串，返回
7611   While
7612   // 并重复循环。
7613   // 在读取完所有记录后
7614   退出 "While" 循环。
7615   // 读取实际上在稍早一点
7616   停止，如果当我们 ""
7617   // 尝试读取另一个字符串并得到
7618   空
7619   // 作为字符串的内容。
7620   //
7621   End Sub // 结束 btnDisplay 事件处理程序
7622   //
7623   // 在此时，填充了数据的
7624   listBox1 屏幕变得
7625   对用户可见。
7626   //
7627   // 用户现在可以查看记录、保存记录
7628   但不能
7629   // 删除记录。我们需要添加
7630   该功能。
7631   //
7632   // 对于表单上添加的另一个名为
7633   btnDelete 的按钮，将文本属性设置为“Delete
7634   Record”。我建议将 Back 属性
7635   设置为“Red”，这会提醒用户
7636   他们所做操作的重大性。
7637   //
7638   进入“btnDeleteRecord”的
7639   事件处理块。输入此代码。
7640   // 删除“被选中”的记录
```

## 简单编程 C# 和 Visual Basic...

```csharp
7642 Private Sub btnDeleteRecord_Click(sender
7643 Object, e As System.EventArgs)
7644 Handles
7645 btnDeleteRecord.Click
7646 // intIdxSelected 是在程序
7647 顶部定义的变量
7648 // 如果用户没有在 listBox1 中
7649 // 选择记录，则返回
7650 //
7651 intIdxSelected = ListBox1.SelectedIndex
7652 // 建议用户在
7653 消息框中选择记录
7654 If (intIdxSelected = -1)
7655 // 括号内的第一个字符串是
7656 消息。
7657 // 逗号后面的字符串是
7658 消息框的标题。
7659 MessageBox.Show("没有
7660 记录要删除。点击
7661 记录")
```
