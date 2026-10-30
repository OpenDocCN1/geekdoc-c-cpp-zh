

## 使用字符串

Visual Basic 提供了许多用于处理文本字符串的方法。Visual Studio 中的字符串是不可变的，这意味着一旦字符串创建，就无法更改。虽然本书中的许多程序似乎修改了字符串，但实际上是创建了一个新字符串并丢弃了旧字符串。

对于字符串处理，您可以使用 String 类的众多方法中的任何一种。您也可以使用 StringBuilder 类，如果您正在构建或修改字符串，它会更高效，因为字符串可以在内存中更改。换句话说，StringBuilder 是可变的（可更改的），而 String 是不可变的。

以下是 String 类方法的部分列表。对于共享方法，您不需要指定 String 实例；对于非共享方法，您必须将方法附加到 String 实例。例如：

共享方法

```
If Compare(AString, BString) > 0 Then
    ...
```

非共享方法

```
If MyString.EndsWith("ed") Then
    ...
```

| Method | Returns |
|---|---|
| Compare(AString, BString) (Shared) | Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, BString, IgnoreCaseBoolean) (Shared) | Case insensitive if IgnoreCaseBoolean is True.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, AStartInteger, BString, BStartInteger, LengthInteger) (Shared) | Compare substrings; start position indicates beginning character to compare for a length of LengthInteger.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, AStartInteger, BString, BStartInteger, LengthInteger, IgnoreCaseBoolean) (Shared) | Case insensitive if IgnoreCaseBoolean is True.
Compare substrings; start position indicates beginning character to compare for a length of LengthInteger.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| EndsWith(AString) | Boolean. True if the String instance ends with AString. Case sensitive. |
| Equals(AString) | Boolean. True if the String instance has the same value as AString. Case sensitive. |
| IndexOf(AString) | Integer. Index position in String instance that AString is found. Positive: String found at this position. Negative: String not found. |
| IndexOf(AString, StartPositionInteger) | Integer. Index position in String instance that AString is found, starting at StartPositionInteger. Positive: String found at this position. Negative: String not found. |
| IndexOf(AString, StartPositionInteger, NumberCharactersInteger) | Integer. Index position in String instance that AString is found, starting at StartPositionInteger, for a length of NumberCharactersInteger. Positive: String found at this position. Negative: String not found. |
| Insert(StartIndexInteger, AString) | New string with AString inserted in the String instance, beginning at StartIndexInteger. |
| LastIndexOf(AString) | Integer. Index position of AString within String instance, searching from the right end. |
| LastIndexOf(AString, StartPositionInteger) | Integer. Index position of AString within String instance, searching leftward, beginning at StartPositionInteger. |
| LastIndexOf(AString, StartPositionInteger, NumberCharactersInteger) | Integer. Index position of AString within String instance, searching leftward, beginning at StartPositionInteger, for a length of NumberCharactersInteger. |
| PadLeft(TotalLengthInteger) | New String with String instance right justified; padded on left with spaces for a total length of TotalLengthInteger. |
| PadLeft(TotalLengthInteger, PadChar) | New String with String instance right justified; padded on left with the specified character for a total length of TotalLengthInteger. |
| PadRight(TotalLengthInteger) | New String with String instance left justified; padded on right with spaces for a total length of TotalLengthInteger. |
| PadRight(TotalLengthInteger, PadChar) | New String with String instance left justified; padded on right with the specified character for a total length of TotalLengthInteger. |
| Remove(StartPositionInteger, NumberCharactersInteger) | New String with characters removed from String instance, beginning with StartPositionInteger for a length of NumberCharactersInteger. |
| Replace(OldValueString, NewValueString) | New String with all occurrences of the old value replaced by the new value. |
| StartsWith(AString) | Boolean. True if the String instance starts with AString. Case sensitive. |

## 启动对象

当项目开始执行时，启动窗体被加载到内存中。在 Project/ProjectName Properties 中设置启动窗体。

## 声明和显示窗体

要显示一个窗体，您需要实例化该窗体类的对象并显示它。

```
Dim ProgramSummaryForm As New SummaryForm
ProgramSummaryForm.Show()
```

或

```
ProgramSummaryForm.ShowDialog()
```

Show 方法将窗体显示为常规窗口，称为无模式窗口。ShowDialog 方法将窗体显示为模式窗口（对话框），这意味着用户必须响应对话框后才能切换到应用程序中的另一个窗口。

VB 还为项目中的每个窗体提供默认实例，因此在显示窗体之前无需声明和实例化窗体。

```
SummaryForm.Show()
```

## 关闭窗体

使用 Me.Close() 关闭当前窗体，或使用 NamedForm.Close() 关闭任何其他窗体。关键字 Me 指当前类，如果省略则假定，因此您只需使用 Close() 即可关闭当前窗体。

## 窗体属性

您始终设置的窗体的两个属性是 Name 和 Text。您还可以选择是否显示最小化按钮和最大化按钮、关闭按钮以及控制框（在标题栏左端弹出的系统菜单）。如果您想显示一个没有标题栏的窗体，必须将 ControlBox 设置为 false 并将 Text 设置为空字符串。

## 大小和位置属性

窗体首次显示时，使用多个属性来确定位置和大小。设置 StartPosition 以设置其在屏幕上的位置。WindowState 确定窗体以您创建的大小显示还是最大化或最小化。

Location 属性确定窗体在其容器中的放置位置，Size 属性以像素为单位设置大小。

将 IsMdiContainer 属性设置为 true 以创建将容纳子窗体的父窗体。要创建子窗体，不能在设计时设置属性；而必须在代码中设置父级：

```
Dim FirstChildForm As New FirstChildForm()
FirstChildForm.MdiParent = Me
FirstChildForm.Show()
```

## 确认和取消按钮

窗体上的一个按钮应为确认按钮，一个应为取消按钮。当用户在窗体上输入信息时，通常希望在完成后按 Enter 键，而不是拿起鼠标点击按钮。将窗体的 AcceptButton 设置为用户按 Enter 时应激活的按钮；将 CancelButton 设置为用户按 Escape 键时应激活的按钮。优秀的程序员确保在每个窗体上设置确认按钮，并在适当时设置取消按钮。

## 窗体事件

窗体首次加载到内存时，这些事件按此顺序发生：

| New | The constructor. Occurs once when the form is instantiated. |
| Load | Occurs once before the first time the form is displayed. The controls on a form are not available during the Load event; therefore, you cannot set the focus in this event handler. This procedure is the location most programmers use for initialization tasks. |
| Activate | Occurs when a form becomes the active window. During a project with multiple forms, the Activate event occurs each time the user switches from one form to another. The Deactivate event occurs for the form losing active status. |

窗体生命周期结束时发生这些事件。

| Deactivate | Occurs when the form loses focus to another form in the project. It does not occur if the user switches to another application, the application closes, or the form closes. |
| Closing | Occurs just before the Closed event. This gives the programmer a chance to cancel the close process if necessary. |
| Closed | Occurs after the form is closed. Most programmers place cleanup code in this event handler. |

## 使用多个窗体

项目可以显示和隐藏多个窗体。每个窗体都是一个类，可以有 Public 和 Private 成员。您可以从另一个窗体访问一个窗体的 Public 成员（变量和过程）。然而，这被认为是不良做法，因为它违反了封装规则。请注意，使用 Friend 关键字声明的成员对项目中的任何其他窗体都是公开的。

