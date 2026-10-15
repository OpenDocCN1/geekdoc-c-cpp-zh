
您可能已经在图 1-15 中注意到，代码视图和窗体设计器窗口在选项卡式环境中打开。此环境是 Visual Studio 中处理代码窗口的默认方式，但您可以更改它。与 Visual Studio 2010 中的任何其他窗口一样，您可以按住选项卡并将其拖到另一个位置。

这在 Visual Studio 2010 中特别有用，因为您可以将选项卡完全拖离主窗口并将其作为独立窗口在其他位置打开。因此，您可以将当前正在编辑的源文件拖到 Visual Studio 其余部分的单独监视器上——本章前面显示项目属性的屏幕就是此示例。如果您查看这些图像，您会看到它们并未嵌入更大的 Visual Studio 2010 框架中，而是被拉出到自己的窗口中。

### Running ProVB_VS2010

现在您已经查看了生成的项目的元素，让我们在继续之前测试代码。从 Visual Studio 运行应用程序有几种选择；首先是单击开始按钮，它看起来像录音机的播放按钮。或者，您可以转到`Debug`菜单并选择`Start`。最后，启动应用程序最常见的方法是按`F5`。

应用程序启动后，会显示一个空窗体，其中包含标准控件按钮（在右上角），可用于控制应用程序。窗体名称应为`Professional VB.NET`，这是您之前应用的。此时，示例没有任何自定义代码可供检查，因此下一步是向此应用程序添加一些简单元素。

### 自定义文本编辑器

除了能够自定义 Visual Studio 提供的整体环境外，您还可以自定义与开发环境相关的多个特定元素。与以往任何版本相比，修改环境的能力得到了增强。在 Visual Studio 2010 中，用户界面组件使用 WPF 重写，因此整个显示提供了更图形化的环境和更好的设计器支持。

Visual Studio 2010 和 Visual Basic 2010 Express Edition 都有一套丰富的自定义项，涉及各种环境和开发人员设置。不可否认，Visual Studio 2010 的功能集为编辑提供了更多选项，但请放心，Express Edition 包含的编辑选项比大多数人预期的要多得多。例如，这两个 IDE 都有一个可自定义的文本编辑器。如果您曾经需要在观众面前展示代码——例如在代码评审中——能够调整字体大小等类似选项的能力非常有用。

要利用 Visual Studio 的设置，请选择`Tools Options`以打开选项对话框，如图 1-16 所示。在对话框中，确保选中`Show all settings`复选框。接下来，选择`Text Editor`文件夹，然后选择`All Languages`文件夹。此部分使您能够对文本编辑器进行更改，这些更改适用于每个受支持的开发语言。此外，您还可以选择`Basic`文件夹，以对文本编辑器在编辑 VB 源代码时的行为进行特定更改。

![](img/d99870e80390742f93963da7be0b2e61_53_0.png)

图 1-16

从此对话框中，可以修改每个制表符将插入到源代码中的空格数，并管理编辑环境的其他几个元素。在此对话框中，您会看到适用于所有文本编辑环境的通用设置，以及根据特定语言自定义特定设置的能力。例如，特定于 Visual Basic 的部分包含允许换行和行号的设置。文本编辑器的一项鲜为人知但有用的功能是行号。选中`Line numbers`复选框将导致编辑器对所有行进行编号，这提供了一种明确引用代码行的方法。

Visual Studio 还提供视觉指示器，以便您在编辑时跟踪更改。启用`Text Editor`选项下的`Track changes`设置后，Visual Studio 会在您修改文件的位置提供彩色指示器。该指示器显示在显示左侧的彩色条。它显示源文件的哪些部分最近被编辑过，以及这些更改是否已保存到磁盘。

### IntelliSense、代码扩展和代码片段

Microsoft Visual Studio 如此受欢迎的开发环境之一的原因是它旨在支持开发人员生产力。这听起来很好，但让我们来证实一下。不熟悉 Visual Studio 的人可能会认为“生产力”指的是组织和启动项目。当然，正如迄今为止讨论的项目模板和项目设置所示，这是正确的，但这些功能并不会在您创建项目后加快开发速度。

本节介绍三种针对编写代码时生产力的功能。它们价值各不相同，并且特定于 Visual Studio。第一个`IntelliSense`一直是 Microsoft 工具和应用程序的热门功能。第二个功能代码扩展是自 Visual Studio 2005 以来提供的另一个热门功能：它使您能够输入关键字，例如“select”，然后按`Tab`键自动插入通用 select-case 代码块，然后您可以对其进行自定义。最后，超越这一点，您可以使用鼠标右键并在鼠标单击位置插入代码片段。可以看出，每一个都建立在 Visual Studio 的开发人员生产力能力之上。

#### IntelliSense

`IntelliSense`在 Visual Studio 2010 中得到了增强。早期版本的`IntelliSense`要求您首先识别类或属性，然后才能使用`IntelliSense`功能。从 Visual Studio 2008 开始，`IntelliSense`在您输入的第一个字母时激活，因此您可以快速识别所需的类、命令和关键字。此功能在 Visual Studio 2010 中继续存在，但 IDE 团队努力增强了`IntelliSense`性能，以便它不会有时感觉 IDE 正在努力跟上您的输入。

一旦您选择了类或关键字，`IntelliSense`将继续，使您不仅能够使用类的各种方法，还能自动显示与枚举属性列表关联的可能值列表，当定义了属性时。`IntelliSense`还在您进行方法调用时提供类似 ToolTip 的参数定义列表。

图 1-17 说明了`IntelliSense`如何在您输入的第一个字符时可用。请注意，下拉窗口底部有两个选项卡；一个针对您可能想要的项目进行了优化，而另一个显示所有可用内容。此外，`IntelliSense`可与多词命令一起使用。例如，如果您键入`Exit`和一个空格，`IntelliSense`会显示可能跟随`Exit`的关键字的下拉列表。提供下拉列表以显示可用选项的其他关键字包括`Goto`、`Implements`、`Option`和`Declare`。在大多数情况下，`IntelliSense`在环境中显示的 ToolTip 信息比 Visual Studio 的过去版本更多，并帮助开发人员匹配括号、花括号和方括号对。

![](img/d99870e80390742f93963da7be0b2e61_54_0.png)

图 1-17

最后，请注意`IntelliSense`基于您的编辑上下文。在编辑文件时，您可能会达到想要在`IntelliSense`中显示特定项的程度，但当您反复输入略有不同的版本时，什么也没有出现。`IntelliSense`认识到您不在方法中或在类的范围之外，因此它会从`IntelliSense`可用项列表中删除不适合源代码当前位置的项。

#### 代码扩展

超越`IntelliSense`的是代码扩展。代码扩展认识到某些关键字始终与其它代码行相关联。在最基本层面上，这发生在您声明新的`Function`或`Sub`时出现：Visual Studio 在您按`Enter`后自动插入`End Sub`或`End Function`行。从本质上讲，Visual Studio 将声明行扩展为包含其匹配的端点。

然而，真正的代码扩展比这更进一步。通过真正的代码扩展，您可以键入`For`、`ForEach`、`Select`或任何 Visual Basic 关键字。如果您然后使用`Tab`键，Visual Studio 将尝试识别该关键字并插入您否则需要记住并自行键入的代码块。例如，而不是需要记住如何格式化`Select`语句的控制值，您只需键入此命令的第一部分，然后按`Tab`即可获得以下代码块：

```
Select Case VariableName
  Case 1
  Case 2
  Case Else
End Select
```

不幸的是，这是一个仅仅向您展示代码是不够的情况。这是因为插入的代码中包含活动区域，表示您将自定义的关键项。因此，图 1-18 提供了当您将`Select`关键字扩展为完整的`Select Case`语句时插入内容的更好表示。

![](img/d99870e80390742f93963da7be0b2e61_55_0.png)

图 1-18

插入块时，编辑器会自动将光标定位在第一个突出显示的块中——`VariableName`。当您开始键入适用的变量名称时，编辑器会自动清除该

static `VariableName` string, which is acting as a placeholder. Once you have entered the variable name you want, you can just press `Tab`. At that point the editor automatically jumps to the next highlighted item. This capability to insert a block of boilerplate code and have it automatically respond to your customization is extremely useful.

Code expansion enables you to quickly shift between the values that need to be customized, but these values are also linked where appropriate, as in the next example. Another code expansion shortcut creates a new property in a class. If at the class level you type the letters “`prop`” and then press the `Tab` key twice, after the first tab you’ll find that your letters become the word “`Property`”; and after the second tab the code shown in Figure 1-19 will be added to your existing code. On the surface this code is similar to what you see when you expand the `Select` statement. Note that although you type prop, even the internal value is part of this code expansion. Furthermore, although Visual Basic implemented a property syntax that is no longer dependent on an explicit backing field, this expansion provides the more robust syntax that uses an explicit backing field.

![](img/d99870e80390742f93963da7be0b2e61_56_0.png)

### FIGURE 1-19

The difference, however, is that the same value `String` in Figure 1-19 is repeated for the property. The value you see is the default. However, when you change the first such entry from `String` to `Integer`, Visual Studio automatically updates all three locations because it knows they are linked. Using the code shown in Figure 1-19, update the property value to be `m_Count`. Press `Tab` and change the type to `Integer`; press `Tab` again and label the new property `Count`. This gives you a simple property on this form for use later when debugging.

The completed code should look like the following block:

```
Private m_Count As Integer
Public Property Count() As Integer
    Get
        Return m_Count
    End Get
    Set(ByVal value As Integer)
        m_Count = value
    End Set
End Property
```

This capability to fully integrate the template supporting the expanded code with the highlighted elements, helping you navigate to the items you need to edit, makes code expansion such a valuable tool.

### Code Snippets

You can, with a click of your mouse, browse a library of code blocks, which, as with code expansion, you can insert into your source file. However, unlike code expansion, these snippets aren’t triggered by a keyword. Instead, you right-click and (as shown in Figure 1-20) select `Insert Snippet` from the context menu. This starts the selection process for whatever code you want to insert.

![](img/d99870e80390742f93963da7be0b2e61_57_0.png)

### FIGURE 1-20

The snippet library, which is installed with Visual Studio, is fully expandable, as discussed later in this chapter. Snippets are categorized by the function on which each is focused. For example, all the code you can reach via code expansion is also available as snippets, but snippets go well beyond that list. There are snippet blocks for XML-related actions, for operating system interface code, for items related to Windows Forms, and, of course, a lot of data-access-related blocks. Unlike code expansion, which enhances the language in a way similar to `IntelliSense`, code snippets are blocks of code focused on functions developers often write from scratch.

As shown in Figure 1-21, the insertion of a snippet triggers the creation of a placeholder tag and a context window showing the categories of snippets. Each of the folders can contain a combination of snippet files or subdirectories containing still more snippet files. Visual Basic 2010 Express contains a subset of the folders provided with Visual Studio 2010. In addition, Visual Studio includes the folder `My Code Snippets`, to which you can add your own custom snippet files.
