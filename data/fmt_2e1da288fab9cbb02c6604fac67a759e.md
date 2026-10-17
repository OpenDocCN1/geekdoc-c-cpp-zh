
你将在 Visual Basic 编辑器的代码窗口执行大部分测试和编辑宏的实际工作。代码是纯文本编写的，你可以简单地在记事本中编写它，然后将其粘贴到代码编辑器中进行测试和调试。然而，Visual Basic 编辑器提供了许多实用的编程工具，只有少数天才才能在不寻求编辑器任何帮助的情况下凭目尝试获得良好结果。

## 图 2.5

对象浏览器提供了一种查找对象及其属性的方法。你可以看到 `Document` 对象中包含的属性。

![](img/03e3cf21a6476d99c08c2f87b3092f20_80_0.png)

Visual Basic 编辑器为每个项目提供一个单独的代码窗口，为项目中的每个包含代码的代码段提供，并为项目中的每个代码用户提供。每个代码窗口都通过项目名称、项目中的模块名称以及 Word 代码来标识。图 2.6 显示了了 `Transpose_Word_right` 宏的 Visual Basic 编辑器窗口。

## 图 2.6

你在代码窗口中编辑宏。

![](img/03e3cf21a6476d99c08c2f87b3092f20_80_1.png)

# 第 2 章开始使用 Visual Basic 编辑器

如从图中所示，代码窗口标题栏正下方出现了两个下拉列表框：

- 代码窗口左上角的 **Object**（对象）下拉列表框提供了在不同对象之间导航的快速方法。
- 代码窗口右上角的 **Procedure**（过程）下拉列表框允许你在当前模块内快速在各个过程之间移动。点击向下箭头按钮显示过程下拉列表。你会发现第一个过程是 `Declarations`（声明）。点击列表中的此项将你带到代码表顶部的声明区域，那里是你声明公共变量以及多个过程需要所需的其他 VBA 信息的地方。

Visual Basic 编辑器代码窗口提供了六项可以帮助你高效准确地编辑的功能，如下节将讨论。

## 单词补全 (COMPLETE WORD)

## 图 2.7

![](img/03e3cf21a6476d99c08c2f87b3092f20_81_0.png)

在打字时激活“单词补全”最简单的方法是按 `Ctrl+spacebar`。你也可以编辑单词补全，或点击工具栏上的单词补全（见图 2.8）。注意，编辑器工具栏默认不可见。通过转到 `工具栏 > 编辑` 或通过在编辑器的工具栏区域点击右键，然后从出现的快捷菜单中选择“编辑”来打开它。

## 图 2.8

编辑器工具栏包含在代码窗口工作时使用的功能。

![](img/03e3cf21a6476d99c08c2f87b3092f20_81_1.png)

## 快速信息 (QUICK INFO)

快速信息功能会显示一个屏幕提示（ScreenTip），显示有关当前选中变量、函数、方法、命令或子程序的语法信息。（“选中”指的是与闪烁的光标插入点相同或相邻的单词。）如果你输入一个诸如 `MsgBox` 这样的命令并按空格键，就会弹出提示以帮助你完成命令输入。提示显示了该命令的必需和可选元素。可选元素位于方括号内。

图 2.9 显示了快速信息屏幕提示的示例。

## 图 2.9

使用编辑器的快速信息功能查看 VB 语言命令的语法或状态的快速读取。

```
MsgBox([Buttons As MsgBoxStyle=vbOKOnly], [Title], [HelpFile], [Context] As MsgBoxResult)
```

要显示快速信息，可以使用以下方法之一：

- 直接在 VB 命令后输入空格。例如，输入 `messagebox` `。
- 点击编辑器工具栏上的快速信息图标。
- 右键点击 VB 命令并从快捷菜单中选择快速信息。
- 将插入点放在命令中并按 `Ctrl+space`。
- 将插入点放在命令中并按 `Ctrl+I`。

如果你输入一个诸如 `MsgBox` 这样的命令并按空格键，就会弹出提示以帮助你完成命令输入。提示显示了该命令的必需和可选元素。可选元素位于方括号内。

## 列表成员 (LIST MEMBERS)

Visual Basic 编辑器代码窗口提供了六项可以帮助你高效准确地编辑的功能，如下节将讨论。

列表成员允许你完成代码行。

# 图 2.11

列表常量 (The List Constants)

该功能可以节省你的时间和精力，并在输入复杂的常量时提高稳健性。

![](img/03e3cf21a6476d99c08c2f87b3092f20_84_0.png)

## 数据提示 (DATA TIPS)

数据提示功能会在鼠标指针悬停在 Visual Basic 编辑器上时显示包含值的屏幕提示（ScreenTip），前提是处于断点模式（你用于测试和调试宏的模式，将在本书的后后部分进行描述）。图 2.12 显示了一个示例。数据提示功能默认开启的，但你可以通过选择选项（Options）来关闭该功能及其他功能。

# 图 2.12

在运行代码或单步执行代码时，使用数据提示功能来检查变量的值。

```
strFirstName = "Tony"
strLastName = "DAnnassalada"
strWholeName = strFirstName & " " & strLastName
strFirstName = "Tony"
```

## 边缘指示器 (MARGIN INDICATORS)

边缘指示器功能允许你通过点击代码窗口的边缘来快速设置断点、下一条语句或书签。你将在后面学习设置断点、设置下一条语句以及设置书签。你也可以右键点击代码窗口左侧的灰色边缘，然后从快捷菜单中选择“切换”（Toggle）来操作断点或书签。你也可以只需左键单击切换断点。

## 其他编辑功能 (OTHER EDITING FEATURES)

除了这些功能外，代码窗口还包含标准的 Office 编辑功能，如复制和移动、剪切和粘贴以及拖放。例如，你可以将代码从一个过程或模块拖到另一个模块。

## 属性窗口 (The Properties Window)

Visual Basic 编辑器提供属性窗口，你可以用它来查看和修改 VBA 中对象的属性，例如属性、模块或类模块、用户表单或控件（例如对话框中的复选框）。如果属性窗口在编辑器中不可见，请按 `F4` 键。

在属性窗口顶部的下拉菜单中，你可以选择想要查看或修改的属性的对象。你也可以在项目管理器（Project Explorer）窗口中选择一个项目。“字母顺序”（Alphabetic）选项显示项目内属性的字母顺序列表，“分类”（Categorized）选项则呈现按分类划分的属性列表。通常我发现分类没有用，因为许多属性无法整齐地归入任何特定类别。

# 第 2 章入门视觉编辑器 (CHAPTER 2 GETTING STARTED WITH THE VISUAL EDITOR)

2.13 左侧显示 Excel 工作簿属性的字母顺序选项，右侧显示分类页面（显示 Excel 工作簿或工作表的分类页面感觉不太好，因为所有属于杂项（Misc）类别的属性都是杂项。这里完全没有分类。）

图 2.13 使用属性窗口查看项目、用户模块、类或控件的属性。

| 属性 - 工作簿 | 属性 - 工作簿 | 杂项 |
| :--- | :--- | :--- |
| Alphabetical | Categorized |  |
| Version | ThisWorkbook | ThisWorkbook |
| AutoOpenFrequency | 0 | AccuracyVersion |
|  | 0 |  |
| ChangeHistory | 0 | ChangeHistory |
| ChangeDuration | 0 |  |
| ChartDataPaths | True | ChartDataPath |
| CheckFile | False | Checkability |
|  | False |  |
| ConflictResolution | 1 | UserResolution |
|  | 1 |  |
| DefaultName | False | DefaultName |
|  | False |  |
| DrawingObjects | 404 -xShapes | DrawingObjects |
|  | 404 -xShapes |  |
| DisplayComments | True | DisplayComments |
|  | True |  |
| EnableAutoCorrect | True | EnablePromptForConvert |
|  | True |  |
| EnableEvents | True | EnableEvents |
|  | True |  |
| EnumerateFile | False | EncryptProvider |
|  | False |  |
| Emover | False | Final |
|  | False |  |
| FullCalculation | True | FullCalculation |
|  | True |  |
| HighChangeOrderScale | False | HighChangeOrderScale |
|  | False |  |
| InteractiveMode | True | InteractiveMode |
|  | True |  |
| IsLocked | False | IsLocked |
|  | False |  |
| KeepChangeHistory | True | KeepChangeHistory |
|  | True |  |
| LastOnChangeSheet | True | LastOnChangeSheet |
|  | True |  |
| Password | ***** | Password |
|  | ***** |  |
| PersonalNameSettings | True | PersonalUserSettings |
|  | True |  |
| PermissionDenied | False | PermissionDenied |
|  | False |  |
| ReadOnlyRecommended | False | ReadOnlyRecommended |
|  | False |  |
| RemoveHiddenInformation | True | RemoveHiddenInformation |
|  | True |  |
| Saved | True | Saved |
|  | True |  |
| SaveUnlinks | True | SaveUnlinks |
|  | True |  |
| ShowConflicts | True | ShowConflicts |
|  | True |  |
| ShowFirstTextField | True | ShowFirstTextField |
|  | True |  |
| TemplateNameveEditData | True | TemplateNameveEditData |
|  | True |  |
| UpdateReferences | 1 -xLinkUserSets | UpdateReferences |
|  | 1 -xLinkUserSets |  |
| WritePassword | ***** | WritePassword |
|  | ***** |  |

大多数工作簿属性的目的是很容易理解的。例如，如果 HasSlip 属性设置为 False，意味着该工作簿没有关联的邮件路由；如果 Saved 属性设置为 True，则表示工作簿已保存。

项目项及其生成的对话框都通过项目的描述来标识——例如，Word 模板的属性对话框被标识为 `TemplateProject – Project Properties`，Excel 工作簿的属性对话框被标识为 `VBAProject – Project Properties`。图 2.15 显示 Excel 工作簿项目的项目属性对话框。

## 图 2.15 VBAProject - Project Properties

使用项目对话框查看并设置项目的属性，并锁定项目以防止更改。

![](img/03e3cf21a6476d99c08c2f87b3092f20_88_0.png)

以下是可以在项目属性对话框的“常规”（General）选项卡中进行的操作：

- 在“项目名称”（Project Name）文本框中设置项目名称。此名称在对象浏览器（Object Browser）中以及必要时在 Windows 注册表中标识该项目。确保名称是唯一的，以避免与其他任何项目发生冲突。从技术上讲，项目名称是项目的类型库名称（类型库描述了项目包含的对象——如模块和用户表单）；它用于构建项目内类的完全限定名称（本书后将介绍）。项目名称可以包含下划线，但不能包含空格。
- 在“项目描述”（Project Description）文本框中输入项目描述。此描述出现在对象浏览器的“描述”窗中，帮助用户理解项目内容。因此，请尽可能简洁且具有描述性。
- 通过在“帮助文件名”（Help File Name）文本框中输入帮助文件的名称和路径来指定项目的帮助文件。点击帮助文件名文本框右侧带有省略号 (...) 的按钮可显示帮助文件对话框。选择文件并点击“打开”按钮将帮助文件的名称输入文本框中。（或者，你也可以输入或粘贴名称和路径）。
- 在“帮助上下文 ID”（Help Context ID）文本框中指定项目的帮助上下文。帮助上下文是指帮助文件中的某个位置。默认帮助上下文为 0，这会导致帮助文件显示其打开屏幕（这与你从“运行”对话框运行帮助文件或通过在资源管理器中双击文件时看到的屏幕相同）。你可以指定不同的帮助上下文，将用户引导到特定主题——例如，与他们正在查找的项目更相关的课题。
- 指定项目所需的任何条件编译参数，但大多数情况下不需要。它允许你根据在此对话框中指定的设置创建不同版本的 VBA 项目。对我个人而言，我觉得这样做麻烦得不偿失——而且令人困惑。我宁愿直接创建一个多个版本的项目。如果你对此主题感兴趣，请查看此处：

https://msdn.microsoft.com/en-us/library/x435tkkb(v=vs.98).aspx

以下是在项目属性对话框的“保护”（Protection）选项卡中可以的操作，如图 2.16 所示：

- 选择“锁定项目以供查看”（Lock Project for Viewing），防止其他人在不知道密码的情况下打开、查看和更改项目。
- 在“查看项目属性的密码”（Password To View Project Properties）分组框中，在“密码”（Password）文本框中输入项目密码，然后在“确认密码”（Confirm Password）文本框中输入相同的密码。点击“确定”按钮然后关闭项目。现在，如果它们在 Office 2007 之前很容易被破解，那么现在没有人可以打开或查看（更不用更改）该项目了。现在使用了更优的加密技术，但密码仍然可以破解，尽管难度大得多。更多信息请参阅第 19 章“使用 VBA 安全功能保护你的代码”。

![](img/03e3cf21a6476d99c08c2f87b3092f20_89_0.png)

## 如果你想防止他人打开项目，请选择锁定项目以供查看

如果你在“密码”文本框和“确认密码”文本框中输入了密码，但没有勾选“锁定项目以供查看”复选框，Visual Basic 编辑器将在下次尝试显示项目属性对话框时提示你输入密码。然而，你可以在不提供密码的情况下打开并查看项目及其内容。

## 自定义 Visual Basic 编辑器

考虑到你可能会在 Visual Basic 编辑器中花费大量时间，你应该对其进行自定义，以便工作得高效且舒适。

- 在 Visual Basic 编辑器中选择“编辑器和视图”（Editor and View）首好设置，以控制它与你的交互方式。
- 选择在 Visual Basic 编辑器中显示的窗口，并组织它们的布局，以便尽可能利用你的工作空间。
- 自定义 Visual Basic 编辑器中的工具栏和菜单，使所需的命令触手可及（而不会弄乱你的工作空间）。
- 自定义工具箱（Toolbox），使其包含你需要的工具。

## 自定义在应用程序之间是全局的

你对 VBA 编辑器进行的任何自定义都适用于所有应用程序。例如，如果你更改了 Excel 托管的 Visual Basic 编辑器中的字体，那么 Word、Outlook 等托管的编辑器的字体也会发生更改。

## 选择编辑器和视图首好

要开始选择编辑器和视图首好，选择“工具”（Tools） > “选项”（Options）来打开选项对话框（见图 2.17）。

## 图 2.17 选项对话框的编辑器页

![](img/03e3cf21a6476d99c08c2f87b3092f20_91_0.png)

## 编辑器页选项

选项对话框包含以下设置：
