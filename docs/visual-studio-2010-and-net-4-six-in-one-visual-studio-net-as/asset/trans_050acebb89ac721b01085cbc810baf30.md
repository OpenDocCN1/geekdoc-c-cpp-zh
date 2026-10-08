

# 总结

本章讨论了 Visual Studio 2010 与 UI 相关的特性和功能。你学习了外壳（Shell）本身的变化，包括新的窗口管理和多显示器支持。你学习了新的代码编辑器功能以及扩展的可能性。此外还介绍了新的可视化设计器及其功能。最后，你还领略了新 IDE 中为架构师提供的功能。

第 3 章深入探讨了 Visual Studio 代码片段（Code Snippets）以及一些可以帮助你在日常工作中提高工作效率的功能。

# Visual Studio 代码片段

在开发应用程序时，你花费了大量时间输入源代码。尽管 Visual Studio 中有许多设计器和向导可以生成代码骨架、资源信息以及许多代码相关的文件，但根结底，每位开发人员都需要编写代码。有时，输入是非常枯燥的。例如，假设你在 C# 中按照以下模式定义了 Name 属性：

```c
private string _Name;

public string Name
{
    get { return _Name; }
    set
        {
            _Name = value;
            PropertyChanged("Name", value);
        }
}
```

这几乎可以用 C# 的自动语法编写（该语法是在 C# 3.0 中引入的），但遗憾的是你在属性设置器中有一个 `PropertyChanged` 调用，这需要一个后台字段和手动创建的 getter-setter 定义。如果你还有 Title、Description、Active 等其他属性，并遵循与 Name 相同的模式，那么除了输入之前的模式外，你必须将大量出现的 `Name` 和 `_Name` 替换为相应的标识符。

Visual Basic 程序员的工作变得更加繁琐，因为他们必须输入更多内容，如下所示：

```vb
Private _Name As String
Public Property Name() As String
Get
    Return _Name
End Get
```

```vb
Set (ByVal value As String)
  _Name = value
  PropertyChanged("Name", value)
  End Set
  End Property
```

如果你只需通过输入名称就能创建许多具有此类语义的属性会怎样？你可以使用代码片段！

Visual Studio 的早期版本没有包含任何防止开发人员进行此类重复性工作的功能。请求最高的功能之一是在 Visual Studio 中添加某种工具，该工具能够根据某些模板机制创建代码，以简化输入。代码补全提供了很大帮助，它可以节省你每一次按键，但它的效率还不够。

Visual Studio 2005 引入了代码片段的概念。这一概念背后的想法（为了满足社区的愿望）是允许开发人员创建一个代码模板，然后根据需要多次使用它。模板具有零、一个或多个用户可以更改的占位符 —— 在一处的更改会改变模板中该占位符的所有出现位置。这一概念成功地补偿了功能开发人员，这种补偿在 Visual Studio 早期 .NET 相关版本中是缺失的。

代码片段对于那些乐于将时间花在有用事情上的开发人员来说，是非常合适的工具。本章提供了帮助你学习代码片段的细节。阅读本章后，你将熟悉以下内容：

-   理解代码片段的概念。—— 本章将简要说明什么是代码片段以及如何使用它们。你还将学习一些依赖语言的片段功能，这些功能突出了 C# 代码编辑器与 Visual Basic 编辑器之间的差异。

-   创建代码片段。—— 你将创建一个非常简单的片段并将其集成到 Visual Studio 集成开发环境（IDE）中，并学习定义代码片段的文件格式细节。

-   管理代码片段。—— 在日常工作中，你可能不仅使用一个，而是几十个代码片段。在本章中，你将查看片段是如何存储在计算机上的，以及如何使用代码片段管理器（Code Snippets Manager）来管理它们。

在本章结束时，你将学习一些高级功能和扩展机会，以及一些优秀的社区工具来帮助你开发代码片段。

# 理解代码片段

代码片段背后的概念简单而强大。片段是从字符到页的源代码部分，可以轻松地插入到代码中。要插入的代码是通过模板机制定义的，允许定义占位符。当然，相同的占位符可以放入模板的许多地方，相应地更改所有出现位置。让我们回顾一下定义属性的代码：

```csharp
private string _Name;
public string Name
{
    get { return _Name; }
    set
        {
            _Name = value;
            PropertyChanged("Name", value);
        }
}
```

在这里你看到作为标识符或字面量的 Name。该属性的片段模板可能是这样的：

```csharp
private string %Name%;
public string %Name%
{
    get { return %Name%; }
    set
        {
            %Name% = value;
            PropertyChanged("%Name%", value);
        }
}
```

当插入代码模板时，%Name% 值可以更改当前值以应用模板。尽管代码片段很简单，但有一些细节是你需要知道的

-   从功能的角度来看，有这类片段。通过扩展片段，代码模板简单地插入到当前编辑器位置。通过周围片段，你让片段包含代码。（此处后续由于原文存在大量重复的段落，已按要求处理翻译并保持逻辑一致）

（注：由于原文后半部分存在大量重复的描述段落，译文已根据指令逻辑进行了精简并保留了核心结构。）

