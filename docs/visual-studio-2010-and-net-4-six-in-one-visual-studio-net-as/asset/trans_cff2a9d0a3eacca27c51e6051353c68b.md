
当你为命令创建快捷键时，它们被存储为与所选方案中定义的快捷键相关的更改。稍后，当你重置方案时，你已应用的更改将会被简单删除。

## 导出和导入键盘方案

在本章的早些部分，你学习了设置的导出和导入。你在“选项”对话框的“键盘”页中定义的快捷键默认是导出设置集的一部分。如果你只想导出键盘映射，必须在“导入和导出设置”向导的“选择要导出的设置”页面上仅选择“键盘”项。

## 设置文件中的键盘快捷键

当你导出键盘映射时，`.vsettings` 文件仅包含你对所选映射方案所应用的差异（删除和新创建的快捷键）。

让我们来看一个示例，看看这意味着什么。按照以下步骤操作：

- 1. 在“键盘”选项页上，选择 Visual C# 2005 映射方案并点击 Ctrl+Q.Reset。
- 2. 为 `Edit.CommentSelection` 命令添加新的编辑器快捷键（例如，Ctrl+Q, Ctrl+C）。
- 3. 从全局范围（Global）定义的 `Edit.Copy` 命令中删除 Ctrl+C 快捷键。
- 4. 使用“导入和导出设置”向导将映射方案导出到你可以记住的位置。
- 5. 在 Visual Studio 2010 中打开保存的 `.vsettings` 文件以进行检查。

列表 5-1 显示了 `.vsettings` 文件的示例。

列表 5-1：持久化的键盘设置

```
<UserSettings>
<ApplicationIdentity version="10.0"/>
<ToolsOptions>
<ToolsOptionsCategory name="Environment" RegisteredName="Environment"/>
</ToolsOptions>
<Category name="Database Tools" RegisteredName="Database Tools"/>
<Category name="Environment_Group" RegisteredName="Environment_Group"/>
<Category name="Environment_KeyBindings">
Category="(F9035FI1-8D02-4312-8EC4-3D54A4BC4C4)"
Package=(DA9FB551-C724-11d0-AE1F-00AC9C0FFC3)"
RegisteredName="Environment_KeyBindings"
PackageName="Visual Studio Environment Package">
<Version>10.0.0</Version>
</KeyboardShortcuts>
<ScopeDefinitions>
<!--
<Scope Name="Text Editor" ID="(8B382828-6202-11D1-D871-88000F87759D2)"/>
-->
continues
```

列表 5-1（续）

```
<!-- ... -->
<Scope Name="Global" ID="5FC7975-14BC-11CF-92B2-00AA00573819"/>
<Scope Name="Class" ID="59B0B277-D7DF-4E36-A2ED-02DAC5B9E2FA0"/>
<Scope Name="XML Activity Diagram" ID="9503C878-B510-4BC5-9051-4279A870364"/>
<Scope Name="Use Case Diagram" ID="F5ECC27C-3151-4B84-A85A-909F50505A70"/>
<!-- ... -->
</ScopeDefinitions>
<DefaultShortcuts>
<ShortcutsScheme>Visual C# 2005</ShortcutsScheme>
<UserShortcuts>
<Shortcut Command="Edit.CommentSelection"
Scope="Text Editor">Ctrl+Q, Ctrl+C</Shortcut>
<RemoveShortcut Command="Edit.Copy">
Scope="Global">ctrl+C</RemoveShortcut>
</UserShortcuts>
</KeyboardShortcuts>
</Category>
</UserSettings>
```

通过理解此列表中的所有细节，你可以立即识别出文件中的几个元素。`<ShortcutsScheme>` 元素命名了键盘方案。`<UserShortcuts>` 元素包含了你对方案应用的更改。在该文件中，它有两个节点：

- `<Shortcut>` 描述了你添加到 `Edit.CommentSelection` 命令的快捷键。
- `<RemoveShortcut>` 描述了从 `Edit.Copy` 命令中删除的 Ctrl+C。

文件包含一个 `<ScopeDefinitions>` 部分，列出了所有关联的快捷键。列表中大多数定义被省略了，但剩余部分告诉你是结构。每个范围定义在“选项”页上显示，并具有用于 Visual Studio IDE 的标识符。

## 启动页

2002 年 2 月发布的第一个 Visual Studio 版本引入了“启动页”的概念。当你启动 Visual Studio 时，启动页会提供一些选项，例如创建新项目、打开最近的项目之一、阅读最新新闻、获取指导等。

启动页的格式和内容随着每个 Visual Studio 版本的更新而更改。关于启动页内容的讨论在社区中持续，有些人认为它很有用，而另人则建议更改。启动页从第一个版本开始就是可自定义的。那时，具有良好 XML 架构的 Tab Definition 文件被用于描述页面的自定义部分。

## 创建你自己的启动页

创建你自己的启动页。启动页的格式和内容随着每个 Visual Studio 版本的更新而更改。关于启动页内容的讨论在社区中持续，有些人认为它很有用，而另人则建议更改。启动页从第一个版本开始就是可自定义的。那时，具有良好 XML 架构的 Tab Definition 文件被用于描述页面的自定义部分。
