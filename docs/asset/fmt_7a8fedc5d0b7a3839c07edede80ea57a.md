
这里是 BASIC 编程历史 deBASIC 的另一个例子，在所有其他版本的 BASIC 和 VBA 中，你都使用 `True` 和 `False` 来表示真和假。从某种意义上说这是合理的。在 PowerPoint 2016 中，你也可以使用内置常量 `msoTrue` 和 `msoFalse` 来例如设置幻灯片页脚的 `Visible` 属性。幸运的是，这些常量是可选的。你仍然可以使用传统的 `True` 和 `False`。Microsoft Office 的真与一般的真之间没有区别。（我严格在这些常量的语境下讨论。）

`Mso` 也出现在 `MsoState` 变量中——就是你在上一节中遇到的那种奇异布尔（Boolean）类型。

## ADDTEXTEFFECT 方法的特定参数

以下参数仅适用于 `AddTextEffect` 方法：

- `PresetTextEffect` 是必填参数，指定要使用的预设文本效果。这些预设文本效果通过常量 `msoTextEffect1` 到 `msoEffect38` 识别，它们对应于 WordArt 对话框中的顺序。

- `Text` 是必填参数，指定要使用的文本。

- `FontBold` 是必填参数，设置为 `msoTrue` 可使字体加粗。

- `Fontalic` 是必填参数，设置为 `msoTrue` 可使字体倾斜。

- `FontName` 是必填参数，指定字体名称。

- `FontSize` 是必填参数，指定字体大小。

## ADDOLEOBJECT 方法的特定参数

以下参数仅适用于 `AddOLEObject` 方法：

- `ClassName` 是可选字符串参数，指定程序 ID（ProgID）。你必须使用 `ClassName` 或 `FileName`，不能两者都用。

- `DisplayIcon` 是可选参数，设置为 `msoTrue` 可以图标显示 OLE 对象而不是显示本身。

- `FileName` 是可选字符串参数，指定要显示的图标的文件。

- `IconIndex` 是可选整数参数，指定 `FileName` 指定文件中的图标索引。如果你省略了 `IconIndex`，VBA 将使用文件中的第二个图标（位置 0 是第一个图标）。

- `IconLabel` 是可选字符串参数，你可以用它指定说明。

- `Link` 是可选参数，设置为 `msoTrue` 可建立链接。

## 使用 AddShape 的示例

以下语句使用 `AddShape` 方法在最后一个幻灯片上添加一个弯箭头。在执行此示例之前，点击 PowerPoint 的“文件”选项卡，然后点击左侧的“新建”查看所有模板。双击一个模板，以便有幻灯片运行此示例。（在 2013 之前的 PowerPoint 版本中，你需要打开示例模板）：

```vba
ActivePresentation.Slides(ActivePresentation.Slides.Count).Shapes.AddShape Type:=msoUpArrow, Left:=575, Top:=10, Width:=150, Height:=75
```

查看发生了什么，查看所有幻灯片并注意上面添加了一个形状——一个弯箭头。

## 使用 AddText 的示例

以下示例使用 `AddText` 方法在第三张幻灯片上叠加一个 WordArt 项目。通过按几次 Ctrl+M 确保至少有三张幻灯片。此代码在幻灯片上绘制了 Questions & Answers（分三行）文本。我们的代码指示该 WordArt 项目使用 54 磅加粗 Garamond。

```vba
ActivePresentation.Slides(3).Shapes.AddTextEffect PresetTextEffect:=msoTextEffect14, Text:="Questions" + Chr(CharCode:=13) + "&" + Chr(CharCode:=13) + "Answers", FontName:=="Garamond", FontSize:=54, Bold:=msoTrue, FontItalic:=msoFalse, Left:=230, Top:=125
```

你可以尝试 30 个 `msoText` 常量。它们的范围从 `msoTextEffect1` 到 `msoTextEffect30`。`msoTextEffect14` 很好，它提供了一种金属效果。见图 25。

图 25.1

`msoTextEffect 14`

提供了金属外观。

### 使用 AddTextbox 方法的示例

以下示例在活动演示文的第二张幻灯片上添加文本框，并为其分配文本：

```vba
Dim myTextBox As Shape

With ActivePresentation.Slides(2)
Set myTextBox = .Shapes.AddTextbox(Orientation=msoTextOrientationHorizontal, Left=100, Top=50, _
Width=400, Height=100)
myTextBox.TextFrame.Range.Text = "Corrective Lenses"
End With
```

### 删除形状

要删除形状，请对适当的 Shape 对象使用 Delete 方法。例如，以下语句将删除活动演示文稿中第二张幻灯片上的第一个形状：

```vba
ActivePresentation.Slides(2).Shapes(1).Delete
```

### 选择所有形状

要选择幻灯片上的所有形状，请使用相应 Shapes 集合的 SelectAll 方法。例如，以下语句将选择活动演示文稿中第一张幻灯片上的所有形状：

```vba
ActivePresentation.Slides(1).Shapes.SelectAll
```

### 重新调整形状的位置和大小

要重新调整形状的位置，请使用其 Left 属性（指定从幻灯片左边缘到形状左边缘的磅数）和其 Top 属性（指定从幻灯片顶部到形状顶部的磅数）。

要更改形状的大小，请将其 Width 和 Height 属性设置为适当的磅数。

例如，以下语句将活动演示文稿中第一张幻灯片上的第一个形状放置在距离幻灯片左边缘 200 点、距离其顶部 100 点的位置，并将形状设为宽 300 点、高 200 点：

```vba
With ActivePresentation.Slides(1).Shapes(1)
.Left = 200
.Top = 100
.Width = 300
.Height = 200
End With
```

您还可以使用 IncrementLeft 方法和 IncrementTop 方法相对于当前位置移动形状。使用 IncrementRotation 方法对其旋转。

请注意，这些方法不是幻灯片内的绝对指定位置。相反，它们相对于形状当前的位置或旋转角度。这些方法中的每个都接受一个 Increment 参数：

- 对于 IncrementLeft 和 IncrementTop 方法，Increment 指定移动形状的磅数。负数将形状向左或向上移动，正数将形状向右或向下移动。

- 对于 IncrementRotation 方法，Increment 指定旋转形状的度数。正数使形状顺时针旋转；负数使形状逆时针旋转。

以下示例适用于活动演示文稿中第三张幻灯片上的第一个形状，向左移动 100 点，向下移动 200 点，并逆时针旋转 90 度：

```vba
With ActivePresentation.Slides(3).Shapes(1)
.IncrementLeft Increment:=100
.IncrementTop Increment:=200
.IncrementRotation Increment:=-90
End With
```

### 将格式从一个形状复制到另一个

通常，对多个形状应用相同的格式非常有用。当一个形状具有你所需的格式时，可以使用 Shape 的 Pickup 方法从该形状复制格式，然后使用 Apply 方法将该格式应用到另一个形状。

Pickup 方法和 Apply 方法均不使用参数。以下示例从活动演示文稿中第二张幻灯片上的第一个形状复制格式，并将其应用到第三张或第四张幻灯片：

```vba
With ActivePresentation
.Slides(2).Shapes(1).Pickup
.Slides(4).Shapes(3).Apply
End With
```

### 在形状中处理文本

形状内的文本包含在 TextRange 对象中，而该对象本身包含在 TextFrame 对象中。要处理形状中的文本，您可以使用 Shape 的 TextFrame 属性返回 TextFrame 对象，然后使用 TextFrame 对象的 TextRange 属性返回 TextRange 对象。明白了吗？（记住某些对象之间可能存在复杂的、甚至可以说是令人困惑的关系。）

在 TextRange 对象中，Text 属性包含文本，Font 对象包含字体格式，ParagraphFormat 对象包含段落格式，而 ActionSettings 集合包含该文本范围的操作设置。

### 查出形状是否具有文本框

并不是每个形状都有文本框；在操作文本之前，最好先确定你正在处理的形状实际上*确实*（has）文本框。

要做到这一点，请检查 Shape 对象的 HasTextFrame 属性是否为 `msoTrue`，如例所示：

```vba
If ActivePresentation.Slides(1).Shapes.HasTextFrame = msoTrue Then
MsgBox "该形状包含文本框"
End If
```

您可能还需要检查文本框是否包含文本。要做到这一点，请检查 Text 对象的 HasText 属性是否为 `msoTrue`。这里有一个示例：

```vba
With ActivePresentation.Slides(1).TextFrame
If .HasText = msoTrue Then MsgBox "文本框包含文本"
End With
```

### 返回并设置文本框中的文本

要返回（读取）或设置（指定）文本范围中的文本，可以简单地使用 Range 对象的属性。例如，以下语句将由变量 `myPresentation` 标识的演示文稿第四张幻灯片上的第一个形状设置为“Strategic Meeting”：

```vba
Sub Text()

Dim myPresentation As Presentation
Set myPresentation = Presentations(1)
myPresentation.Slides(4).Shapes(1).TextFrame.Range = "Strategic Meeting"

End Sub
```

您还可以通过 Paragraphs 方法、Sentences 方法、Lines 方法、Words 方法或 Runs 方法返回文本部分。以下是使用 Paragraphs 方法的语法：

```vba
expression.Paragraphs(Start, Length)
```

语法的组件如下：

- `expression` 是指定的 TextRange 对象。

- `Start` 是可选的 Long 参数，指定要返回的项目（段落、句子、单词或文本范围）。

- `Length` 是可选的 Long 参数，指定返回的项目数量（例如，两个段落、三个句子）。

### 理解文本范围 (Runs)

一个 run 是具有相同字体格式的字符序列。Text runs 对于提取具有特定格式的文本部分非常有用。

代码示例返回活动演示文稿第一张幻灯片上第二个到第五个单词（从第二个单词开始四个）：

```vba
MsgBox ActivePresentation.Slides(1).Shapes(1).TextFrame

.TextRange.Words(Start:=2, Length:=4)
```

代码示例将由 `myPresentation` 标识的演示文稿第六张幻灯片上第二个形状的第二个段落文本设置为“VP of Development”：

```vba
myPresentation.Slides(6).Shapes(2).TextFrame
.TextRange.Paragraphs(Start:=2, Length:=1).Text = "VP of Development"
```

### 设置文本范围的格式

要对文本范围进行格式设置，请使用 ParagraphFormat 对象控制段落格式（使用对齐以及前后的空间），并使用 Font 对象控制字体格式。

这些是 ParagraphFormat 对象最有用的属性：

- Alignment 属性控制对齐方式。使用 `ppAlignLeft` 用于左对齐，`ppAlignCenter` 用于居中，`ppAlignJustify` 用于端对齐，`ppAlignDistribute` 用于分布对齐（使用所有可用空间），或 `ppAlignRight` 用于右对齐。

- Bullet 属性返回 BulletObject，该对象表示项目符号格式。详情见下一节。

- LineBefore、LineAfter 和 LineRuleWithin 属性决定由 SpaceBefore、SpaceAfter 和 SpaceWithin 属性设置的测量值使用的是行（`msoTrue`）还是磅数（`msoFalse`）。

- SpaceBefore 属性和 SpaceAfter 属性控制每个段落前后的空间。SpaceWithin 属性控制段落内行之间的间距。

### 操作形状

```vba
Dim mySlide As Slide

Set mySlide = Presentations(1).Slides(2)

With mySlide.Shapes(2).TextFrame.TextRange.ParagraphFormat
.Alignment = ppAlignLeft
.LineRuleAfter = msoFalse
.SpaceAfter = 18
.LineRuleBefore = msoFalse
.SpaceBefore = 18
.LineRuleWithin = msoFalse
.SpaceWithin = 12
End With
```

### 为文本范围设置项目符号

项目符号和数字对于许多 PowerPoint 幻灯片中的列表至关重要。要控制项目符号和数字的外，可以使用 `TextRange` 对象的 `Bullet` 属性返回 `BulletFormat` 对象，并操作 `BulletFormat` 对象的属性和方法。

要使项目符号和数字可见，将 `BulletFormat` 对象的 `Visible` 属性设置为 `msoTrue`；隐藏项目符号和数字，将 `Visible` 设置为 `msoFalse`。

要指定使用什么类型的项目符号或编号，将 `BulletFormat` 对象的 `Type` 属性设置为 `ppBulletUnnumbered`（项目符号）、`ppBulletNumbered`（数字）、`ppBulletPicture`（图片）或 `ppBulletNone`（无项目符号）。

### 另一种混合数据类型

当选择包含多个类型的项目符号时，`BulletFormat` 对象的 `Type` 类型返回值 `BulletMixed`。你不能（写入）将 `ppBulletMixed` 给 `Type`。你只能读取它。

要指定项目符号字符，使用 `Character` 属性和字符数字。你可以从“符号”对话框或“字符表”中找到字符数字，在 Windows 10 中可以通过按 Windows 键打开开始菜单（或在 Windows 8 中显示图标）并输入“字符表”来运行它。

在 Windows 的早期版本中查看此桌面应用程序有些笨拙。对于 Windows 7 及更早版本，点击“所有程序 > 附件程序 > 字符表”。

遗憾的是，字符代码是以十六进制系统给出的。如果你查找后续代码示例中使用的 `Wingdings` 字体复选框符号，字符表工具不会在我们人类的人类十进制系统中显示为 254。相反，它显示的是“字符代码：0FE”（254 的十六进制表示法）。

## 第 25 章操作形状和运行幻灯片

这种来自计算早期的冗长遗留问题在字符代码中没有特殊用途，但你必须处理它。为什么？因为有些人认为这种无意义的复杂很酷，或者它能让编程看起来比实际上更神秘。这种复杂性有助于职业服务，因为经理们很容易被他们认为的像十六进制这样复杂的谜团所迷住。十六进制（hexadecimal）基于 16 个数字：0 1 2 3 4 5 6 7 8 9 A B C D E F。每只手都有手指的人具有此优势。

要解决十六进制字符代码问题，你可以可以使用可以在十六进制和十进制之间转换的计算器，或者只需假装在十六进制前面加上 `&HH` 字符，让 VBA 在你执行宏时对其进行翻译。

例如，在下面的代码示例中，我使用了 254（一个十进制数字），因为我可以翻译十六进制（用我的 HP 科学计算器可以）。如果你不能，或者更可能不想麻烦，只需在“字符”对话框中点击你想要使用的字符，然后查看对话框底部的十六进制值。在这个示例中，它列为 0FE（这意味着你猜对了，是 254）。因为 `Wingdings` 只有 256 个字符，忽略 0 部分，在代码中使用 FE，如下所示：

```vba
.Character = &HFE
```

使用该属性指定字体名称、大小和颜色。下面的示例将由对象 `mySlide` 标识的幻灯片上形状的项目符号设置为 `Wingdings` 字符 254（复选框），使用 RGB(255,255,255) 颜色和 44 点大小：

```vba
mySlide.Shapes(1).Frame.TextRange.ParagraphFormat.Bullet
.Type = ppBulletUnnumbered
.Character = 254
.Name = "Wingdings"
.Size = 44
.Color = RGB(255, 255, 255)
```

颜色当然是任何设计中的重要元素。你可以通过访问此网页轻松找到颜色的 RGB 值：

```
http://cloford.com/resources/colours/580col.htm
```
