
```xml
<UserSettings>
<ApplicationID version="10.0"/>
<ToolOptions>
  <ToolOptionsCategory name="Environment" RegisteredName="Environment">
    <ToolOptionsSubCategory name="Documents" RegisteredName="Documents" PackageName="Visual Studio Environment Package">
      <PropertyValue name="ShowFilesProject" value="true"/></PropertyValue>
      <PropertyValue name="AutoLoadExternalChanges" value="false"/></PropertyValue>
      <PropertyValue name="ChangeDocumentSettings" value="true"/></PropertyValue>
      <PropertyValue name="SaveAsUncodeWhenDataLoss" value="true"/></PropertyValue>
      <PropertyValue name="InitializeFromFileCurrentDocument" value="true"/></PropertyValue>
    </PropertyValue>
    <PropertyValue name="ResaveSavedActiveWindow" value="false"/></PropertyValue>
    <PropertyValue name="DetectChangesOutsideIDE" value="true"/></PropertyValue>
    <PropertyValue name="DontShowGlobalUndoChangeLossDialog" value="true"/></PropertyValue>
    <PropertyValue name="AllowEditingReadOnlyFiles" value="true"/></PropertyValue>
    <PropertyValue name="DocumentDocPreference" value="0"/></PropertyValue>
    <PropertyValue name="MisProjectPathSavesLastItems" value="0"/></PropertyValue>
  </ToolOptionsSubCategory>
  <ToolOptionsSubCategory name="FindAndReplace" RegisteredName="FindAndReplace" PackageName="Visual Studio Environment Package">
    <PropertyValue name="ShowingMessages" value="true"/></PropertyValue>
    <PropertyValue name="InitializeFromEditor" value="true"/></PropertyValue>
    <PropertyValue name="MessageBoxes" value="true"/></PropertyValue>
    <PropertyValue name="HideWindowAfterMatchQuickFindReplace" value="false"/></PropertyValue>
  </ToolOptionsSubCategory>
</ToolOptionsCategory>
</ToolOptions>
<!-- ... -->
</UserSettings>
```

如果你仔细观察，可以识别出“选项”（Options）对话框中的几个类别、页面和设置。`<ToolOptions>`、` `<ToolOptionsCategory>` 和 `<ToolOptionsSubCategory>` 元素构成了选项对话框中的层级结构。`<PropertyValue>` 元素定义了你可以在页面中管理的设置。

你可以在 Visual Studio 2010 安装目录的 `Common\IDEProfiles` 文件夹中找到预定义配置文件的 `.vsettings` 文件。你应该花时间检查这些文件，以获取更多关于设置的信息。

# 使用快捷键减少工作量

Visual Studio 有许多命令，你可以从 IDE 的菜单或工具栏启动它们。尽管你可以通过移动鼠标指针并点击相应的菜单或工具栏项目来启动所有命令，但在许多情况下，这可能会非常干扰，以至于你必须中断工作。例如，当你编辑代码并要注释一段指令时，你必须遵循以下步骤：

- 1. 即使光标位于要取消注释的代码块开头，你也必须将鼠标移动到光标位置，点击左鼠标键并按住以选择整个文本。

- 2. 将鼠标移动到“编辑”（Edit）菜单项上并点击。

- 3. 找到“编辑”菜单中的“高级”（Advanced）项，并将鼠标悬停在其上方（或点击它）。高级菜单项将显示在屏幕上。

- 4. 点击“命令选择”（Command Selection）项。

这些步骤的真正问题在于，你必须手离开键盘，找到鼠标，看着屏幕并点击几次鼠标；如果你在输入代码时被中断了。

你不允许使用鼠标！按下 `Shift` + `下方向键` 并保持按住状态，直到所有要注释的行都被选中。然后，只需按下 `Ctrl+K` 然后再按 `Ctrl+C` 即可。你不需要手离开键盘，也不需要使用鼠标。`Ctrl+K`, `Ctrl+C` 序列是“编辑+命令选择”的快捷键。

这只是键盘快捷键有多实用的一个简单例子。许多命令都有与其关联的快捷键。你可能会发现其中一些很容易记忆，而另一些很难使用——这取决于你使用它们的频率以及上下文。

IDE 允许对分配给命令的快捷键进行完全控制。你可以根据需要对它们进行定制，以减少执行最频繁任务所需的精力。

## 命令与命令上下文

Visual Studio 2010 提供了许多可用命令。你可以想象为它们的每个命令寻找快捷键是多么困难（而且要通过背背来更具挑战性）。没有理由进行这种完整的映射，因为很多命令很少使用。如果你统计自己在 IDE 中工作时频繁使用的命令，最后只会有几个命令，而不会更多。根据帕累托法则，你应该为最频繁使用的命令分配快捷键，以提高 80% 的效率。

![](img/b5597c749e848b27b0d305153ae16106_196_0.png)

> *在安装期间，Visual Studio 2010 会根据你选择的设置应用默认的快捷键组合方案。Visual Studio 2010 还包含其他六种键盘映射方案，每种方案在默认分配给 UI 元素的快捷键组合上都与其他有所不同。有关按映射方案组织的这些组合列表，请参阅 http://msdn.microsoft.com/en-us/ 中的“预定义快捷键”（Pre-defined Keyboard Shortcuts）。*

Visual Studio 中的命令与命令目标（知道如何解释命令的实体）紧耦合。例如，剪切、复制和粘贴命令在不同的上下文中工作方式。如果你在文本编辑器中，复制命令会复制选中内容。如果你使用 WPF 设计器，则复制当前选的对象。文本编辑器和 WPF 设计器都是命令目标，它们知道在发送命令时该做什么。

Visual Studio 使用路由算法将命令转发到命令目标。与其深入研究该算法的所有细微细节，此处的讨论仅提供一个高层概述。

在寻找目标的路径上，命令从每一层向上冒泡。活动命令范围有权处理该命令或拒绝它，然后继续冒泡。路由算法定义了以下从根节点到根结的的范围：

- 已加载的插件和特殊扩展（Visual Studio 程序包）范围——命令首先提供给注册并加载的插件，或特殊的 Visual Studio 程序包。

- 上下文（快捷）菜单——如果用户从右键菜单使用命令，属于该菜单的命令目标具有处理该命令的机会。如果不处理，则回到正常路由（从已加载的插件开始）。

- 焦点范围——拥有焦点的窗口是下一个可以承担命令的实体。这可能是工具窗口或文档窗口。命令的管理取决于关注的是哪种窗口。

- 文档窗口范围——文档窗口在逻辑上由两个部分组成：负责显示文档 UI 的文档视图，以及负责处理文档信息的文档数据对象。文档和文档视图都可以被管理。如果视图不支持，命令首先进入数据对象。

- 工具窗口范围——工具窗口可以使用自己的逻辑处理命令。有些工具窗口会将内部的命令路由到嵌套的命令目标。解决方案管理器窗口就是一个例子。在解决方案管理器内部，命令通过由元素构成的层级进行路由，每个节点都有处理命令的能力。这种内部路由也从较低层级向上到较高层级。

- 当前项目范围——当前项目获取命令。如果它不处理，命令将在项目层级中向上到达解决方案级别。该节点上的所有节点都可以像其他命令对象一样管理命令。

- 全局范围——如果命令在之前的级别未被处理，环境将尝试将其路由到相应的程序包（Visual Studio 扩展）。如有必要，Visual Studio 将相应的程序包加载到内存中。

属于全局范围（Global scope）的快捷键组合命令可能会根据 IDE 的当前上下文被其他作用范围内的命令覆盖。例如，如果你正在编辑一个文件，属于文本编辑器（Text Editor）作用范围的命令优先级高于具有相同按键组合的全局范围命令。例如，如果多个命令的按键组合以 Ctrl + K 开头，而文本编辑器也有多个以 Ctrl + K 开头的按键组合，当你编辑文本编辑器时，这些按键组合将生效，而全局按键组合将被忽略。

## 使用键盘快捷键

“工具 选项（Tools Options）”对话框中“环境（Environment）”类别下的“键盘（Keyboard）”页面是你管理快捷键的起点。页面包含了执行以下操作所需的所有信息：

- 确定分配给命令的快捷键

- 修改命令的快捷键

- 创建自定义快捷键

图 5-23 显示了“键盘”页面，展示了关于 `Edit.CommentSelection` 命令的信息。

![](img/b5597c749e848b27b0d305153ae16106_198_0.png)

图 5-23：“键盘”页面允许你在 IDE 中工作时选择使用的键盘映射方案。

页面顶部的组合框允许你点击“重置（Reset）”按钮；你可以将映射方案重置为初始状态。

页面中间的列表列出了所有可以分配键盘快捷键的 Visual Studio 命令。列表非常长，查找命令会很费力。你可以使用列表上方的文本框输入命令的一部分，列表将仅填充匹配你搜索定义的的命令名称。

在列表下方，你将看到几个控件，帮助你确定该命令是否关联了任何快捷键，这些控件也帮助你为所选命令定义快捷键。

## 确定分配给命令的快捷键

Visual Studio IDE 的主菜单在菜单项名称右侧显示键盘快捷键，你可以轻松地找到用于特定命令的快捷键。然而，某些命令在主菜单中是不可见的，或者很难找到。通过“键盘”页面，你可以找到任何命令关联的快捷键。

在命令列表上方的文本框中输入命令名称的一部分，以帮助你在列表中定位命令。图 5-23 显示了“Comment”一词如何帮助定位 `Edit.Comment` 命令。

在列表正下方，你可以看到显示与命令关联的键盘快捷键的框。你可以为每个命令关联零、一个或多个快捷键。如果命令没有分配快捷键，则该框处于禁用状态。你可以展开组合框以显示该命令的所有快捷键。当你选择 `Edit.Paste` 命令时，列表包含两个项目：`Ctrl+V` 和 `Shift+Ins`，它们都定义在全局作用范围内。

列表显示了调用该命令必须按的键，并显示了与之关联的快捷键名称。图 5-23 显示了 `Edit.CommentSelection` 命令在文本编辑器作用范围内的键盘快捷键（`Ctrl+K`, `Ctrl+C`）。你最多可以使用两个按键作为快捷键的组合。

### 移除快捷键

你可以轻松地删除快捷键。从快捷键组合框中选择你想要删除的项，然后点击“删除（Remove）”按钮。选中的项将从列表中移除，不会弹出确认询问。当你移除所有项时，组合框和“删除”按钮将被禁用，表示该命令不再关联有更多快捷键。

## 创建新的键盘快捷键

在大多数情况下，你可能因为以下原因想为命令分配新的键盘快捷键：

- 该命令尚没有任何快捷键。

- 你想更改现有的快捷键，或为同一命令添加另一个快捷键。

- 你想覆盖全局作用范围内定义的快捷键。

这些每一种都可以通过“在新作用范围中使用快捷键（Use new shortcut in）”组合框和“按下快捷键（Press shortcut keys）”文本框来处理。

首先，从“在新作用范围中使用”组合框中选择作用范围。在大多数情况下，你会希望使用全局或文本编辑器，但你可以看到许多其他可以定义快捷键的作用范围。接下来，点击“按下快捷键”文本框，按下一个或两个键（按键组合）与之关联。带有修饰符的键将显示在文本框中。

> 快捷键可以是 Shift、Alt 和/或 Ctrl 键与字母、数字、功能键或多个符号组合。虽然你可以将 Shift+Alt+Ctrl 组合配合功能键，但不建议这样做，因为你必须同时按住四个键。

> 以下键不能分配给全局作用范围内的命令：Print Scrn/Up、Scroll Lock、Pause/Break、Tab、Caps Lock、Insert、Home、End、Page Up、Page Down、Windows 标志键、应用程序键、任何方向键或 Enter；数字键盘上的 Num Lock、Del 或 Ctrl；或 Ctrl+Alt+Delete。

你可能会选择一个已经分配给另一个命令（一个或多个在不同作用范围内存）的组合。“当前正在使用的快捷键（Shortcut currently used by）”组合框会显示每一个冲突。

点击“分配（Assign）”按钮将新快捷键关联到所选命令。当快捷键已分配给同一作用范围内的另一个命令时，之前的关联将被移除，快捷键将属于新命令。

> 通常，当你通过“取消（Cancel）”按钮关闭对话框时，键盘不会保存任何更改。

### 仅使用键盘

在本章前面的部分，你已经学习了窗口管理。除了更改焦点，你还可以移动和停靠窗口。首先，使用上述的 `Alt+F7` 或 `Ctrl+Tab` 组合设置要移动或停靠的窗口。然后按下 `Alt+Space` 使用方向键导航到窗口菜单中的“移动（Move）”命令。回车。现在你可以使用方向键移动窗口。当你移动窗口时，鼠标指针会跟随你。按下按键后，屏幕上会出现引导图标。当你使用方向键移动到任何引导图标上（而不是使用鼠标）时，你可以看到窗口被停靠。回车将窗口停靠在指定位置（或释放在当前位置）。

你可以按 `Esc` 取消操作。

当选中目标窗口时，可以使用以下组合在工具或文档之间切换焦点：

- `Alt+F7` — 此键组合切换工具窗口。

- `Ctrl+Tab` — 此键组合切换活动文档。

- 按 `F7` 或 `Tab` 移动列表中的下一个窗口，释放功能键，保留修饰键（Alt 或 Ctrl）。

- 主窗口中心会出现一个弹出窗口（如图24所示），帮助你在工具窗口和文档之间导航。

## 处理键盘映射方案

安装 Visual Studio 时，它会设置五个键盘映射方案文件，这些文件可以在 Visual Studio 安装根目录下的 `Common\IDE` 文件夹找到，扩展名为 `.vsk`。这些是代表特定方案内命令关联快捷键的二进制文件：

- `Visual Basic 6.vsk`

- `Visual C# 2005.vsk`

- `Visual C++ 2.vsk`

- `Visual C++ 6.vsk`

- `Visual Studio 6.vsk`

你可以在键盘选项页面顶部的组合框中找到这些文件名。当你选择一个键盘映射方案时，IDE 将使用所选方案中的组合。

当你为命令创建快捷键时，它们被存储为与所选方案中定义的快捷键相关的更改。稍后，当你重置方案时，你已应用的更改将会被简单删除。

## 导出和导入键盘方案

在本章的早些部分，你学习了设置的导出和导入。你在“选项”对话框的“键盘”页中定义的快捷键默认是导出设置集的一部分。如果你只想导出键盘映射，必须在“导入和导出设置”向导的“选择要导出的设置”页面上仅选择“键盘”项。

## 设置文件中的键盘快捷键

当你导出键盘映射时，`.vsettings` 文件仅包含你对所选映射方案所应用的差异（删除和新创建的快捷键）。

让我们来看一个示例，看看这意味着什么。按照以下步骤操作：

- 1. 在“键盘”选项页上，选择 Visual C# 2005 映射方案并点击 `Ctrl+Q.Reset`。

- 2. 为 `Edit.CommentSelection` 命令添加新的编辑器快捷键（例如，`Ctrl+Q, Ctrl+C`）。

- 3. 从全局范围（Global）定义的 `Edit.Copy` 命令中删除 `Ctrl+C` 快捷键。

- 4. 使用“导入和导出设置”向导将映射方案导出到你可以记住的位置。

- 5. 在 Visual Studio 2010 中打开保存的 `.vsettings` 文件以进行检查。

列表 5-1 显示了 `.vsettings` 文件的示例。

列表 5-1：持久化的键盘设置
