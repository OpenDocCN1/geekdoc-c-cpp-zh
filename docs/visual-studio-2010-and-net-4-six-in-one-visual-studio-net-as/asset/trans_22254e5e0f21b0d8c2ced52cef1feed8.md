

# 深入研究 .vsettings 文件

现在你已经可以想象 .vsettings 文件中存储了哪些设置。该文件采用 XML 格式（遗憾的是它的 schema 并没有发布），研究它可以让你对 Visual Studio 是如何存储你保存的设置有所启发。以下代码片段提取自一个 .vsettings 文件：

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

如果你仔细观察，可以识别出“选项”（Options）对话框中的几个类别、页面和设置。<ToolOptions>`、`<ToolOptionsCategory>` 和 `<ToolOptionsSubCategory>` 元素构成了选项对话框中的层级结构。`<PropertyValue>` 元素定义了你可以在页面中管理的设置。

你可以在 Visual Studio 2010 安装目录的 `Common\IDEProfiles` 文件夹中找到预定义配置文件的 .vsettings 文件。你应该花时间检查这些文件，以获取更多关于设置的信息。

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

