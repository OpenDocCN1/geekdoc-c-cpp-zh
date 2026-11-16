

## 解决方案、项目……

Solutions are like filing cabinets that hold and manage Projects and other files. Easy enough in principle, but what exactly does that mean? Why would you have more than one Project? What are these “other files”, and what exactly does “manage” mean? Let’s look at some examples of the kinds of files you might include in a Solution.

解决方案就像文件柜，用于保存和管理项目及其他文件。原则上很简单，但这究竟是什么意思？为什么你会有多个项目？这些“其他文件”是什么，“管理”究竟意味着什么？让我们看看你可能在解决方案中包含的文件示例。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_78_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_78_1.png)

## 主界面项目

You'll usually have a project (sometimes more than one) that contains the forms that comprise your application user interface.

你通常会有一个项目（有时不止一个），其中包含构成应用程序用户界面的窗体。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_78_2.png)

## 数据集项目

If your application references a data source, you'll usually have a separate project that handles the data interface.

如果你的应用程序引用数据源，你通常会有一个单独的项目来处理数据接口。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_78_3.png)

## 实用程序类

In cooking, you often need to translate between teaspoons, tablespoons and cups. The classes that do that conversion might be useful in other applications, so it makes sense to put those in a separate project that we can reference when we need them.

在烹饪中，你经常需要在茶匙、汤匙和杯之间进行换算。执行该换算的类可能在其他应用程序中也很有用，因此将它们放在一个单独的项目中以便需要时引用是合理的。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_78_4.png)

## 测试项目

Visual Studio 2010 provides great support for a technique called Test-Driven Development. If you adopt this approach, you'll need projects that contain your tests.

Visual Studio 2010 对一种称为测试驱动开发的技术提供了出色的支持。如果你采用这种方法，你将需要包含测试的项目。

## ……以及其他内容

Projects have multiple files, as well. You'll have code and designer files, of course, you've already seen that, but Visual Studio will also allow you to associate other files with the project, just to keep them handy.

项目也有多个文件。当然，你会有代码文件和设计器文件，这一点你已经见过了，但 Visual Studio 还允许你将其他文件与项目关联，以便随时使用。

### 设计器文件

These are the files that are created by the Visual Studio designers. They're text files, but if you mess with them outside the Designer, your changes might get overwritten the next time you use the designer, so you'll typically leave them alone.

这些是由 Visual Studio 设计器创建的文件。它们是文本文件，但如果你在设计器外部修改它们，下次使用设计器时你的更改可能会被覆盖，因此你通常会不去动它们。

### 源文件

These are the files that contain your code. They have the same name as the files the Designer creates, with the extension ".cs".

这些是包含你代码的文件。它们与设计器创建的文件同名，扩展名为“.cs”。

### 设计文档

You can also include documents like this class diagram or even specifications. These files aren't part of the project code.

你还可以包含像这个类图甚至规范这样的文档。这些文件不是项目代码的一部分。

### 资源

If your project includes things like custom cursors or icons these are separate files in the Project.

如果你的项目包含自定义光标或图标等内容，这些是项目中的单独文件。

### 动动脑筋

Find at least two ways to add a Project to a Solution and two ways to add a file to a Project.

找出至少两种将项目添加到解决方案的方法，以及两种将文件添加到项目的方法。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_80_0.png)

## 做得怎么样？

The problem was to figure out how to add Solutions and files...

问题是要想出如何添加解决方案和文件...

## 将项目添加到解决方案：

You can also add existing Projects, which is handy if you're reusing utilities or custom widgets, or exclude a project that you've added by accident.

你也可以添加现有项目，如果你正在重复使用实用程序或自定义小部件，这很方便，或者排除你不小心添加的项目。

The New Project item can be found on the File menu and on the context menu displayed when you right-click the Solution name in the Solution Explorer.

“新建项目”项可以在“文件”菜单上找到，也可以在右键单击解决方案资源管理器中解决方案名称时显示的上下文菜单中找到。

## 将文件添加到项目：

You can add new and existing items from the Solution Explorer by right-clicking the Project name,

你可以通过右键单击项目名称，从解决方案资源管理器中添加新项和现有项，

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_80_1.png)

The Project menu provides specific options for the most common types of Projects, or you can choose Add New Item... to display the New Item dialog.

“项目”菜单为最常见的项目类型提供特定选项，或者你可以选择“添加新项...”以显示“新建项”对话框。

## 独立练习

You know how to add an item to a Project, and you knew how to configure a simple WPF window, so let's put these two things together. Change your Hello, World application to display a window instead of a MessageBox:

你知道如何将项添加到项目，并且你知道如何配置简单的 WPF 窗口，所以让我们将这两件事结合起来。将你的 Hello, World 应用程序更改为显示窗口而不是 MessageBox：

- 1. Add a new window to the Project. Accept the default name of Window1.
- 2. Drag a Label from the Toolbox to the design surface, and configure the window and label properties however you like. Have some fun! You can't hurt anything.
- 3. Display the code for the original form (NOT the one you just created.) If the form is open, you can double-click the button or press F7. If the form isn't open, you can right-click the form name in the Solution Explorer and choose Show Code.
- 4. Delete the line that displays the MessageBox, and replace it with the following:

```
Window newWin = new Window1();
newWin.ShowDialog();
```

- 5. Run the application by pressing F5, and then click the button on the first form.

- 1. 向项目添加一个新窗口。接受默认名称 Window1。
- 2. 从工具箱将标签拖动到设计图面，并按喜好配置窗口和标签属性。尽情享受！你不会弄坏任何东西。
- 3. 显示原始窗体的代码（不是你刚创建的那个。）如果窗体已打开，你可以双击按钮或按 F7。如果窗体未打开，你可以在解决方案资源管理器中右键单击窗体名称并选择“显示代码”。
- 4. 删除显示 MessageBox 的行，并用以下内容替换它：

```
Window newWin = new Window1();
newWin.ShowDialog();
```

- 5. 按 F5 运行应用程序，然后单击第一个窗体上的按钮。

## 休息一下

Why don't you take a quick break before we move on to controlling the way Solutions and Projects behave by setting their properties?

在我们继续通过设置属性来控制解决方案和项目的行为之前，为什么不先休息一下呢？

## 解决方案和……

When you created and modified your windows on the design surface, you saw that you could control the appearance of the widgets by setting their properties. Well, Solution and Projects have properties, as well. We'll need some of these as we move through the book, so let's get started by looking at how to display the property dialogs.

当你在设计图面上创建和修改窗口时，你已经看到可以通过设置属性来控制小部件的外观。同样，解决方案和项目也有属性。在本书后续内容中我们会用到其中一些属性，所以让我们先从如何显示属性对话框开始。

The easiest way to display the Solution Properties dialog is to select the Solution in the Solution Explorer and click the Properties button on the Solution Explorer toolbar, but you can also choose Properties Page from the View menu.

显示“解决方案属性”对话框的最简单方法是在解决方案资源管理器中选择解决方案，然后单击解决方案资源管理器工具栏上的“属性”按钮，但你也可以从“视图”菜单中选择“属性页”。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_82_0.png)

Most of the Solution properties are managed by Visual Studio, and you only need to change them in unusual circumstances, but you'll often need to specify a Startup Project whenever you have a Solution that contains multiple Projects. The STARTUP PROJECT is the one that Visual Studio will run when you press F5.

大多数解决方案属性由 Visual Studio 管理，你只需在特殊情况下更改它们，但当你的解决方案包含多个项目时，你通常需要指定启动项目。启动项目是 Visual Studio 在你按 F5 时运行的项目。

By default, Visual Studio sets the first project you add to the solution as the STARTUP PROJECT. You can change that by choosing a different Project from the combobox.

默认情况下，Visual Studio 将你添加到解决方案的第一个项目设置为启动项目。你可以通过从组合框中选择不同的项目来更改它。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_82_1.png)

You can also set the startup project from the Project menu when the project you want is selected in the Solution Explorer. Visual Studio almost always has several ways to do something.

你也可以在解决方案资源管理器中选择想要的项目后，从“项目”菜单设置启动项目。Visual Studio 几乎总是有多种方法来做某事。

## 项目属性

Solution properties display in a dialog box, but Visual Studio has a designer (called the Project Designer) for project properties that displays in a tab. You can display the Project Designer by clicking the Solution Explorer toolbar button when a Project is selected, by choosing <ProjectName> Properties... from the Project menu when the Project is selected, by right-clicking the Project name in the Solution Explorer and choosing Properties, or by selecting the Solution name in the Solution Explorer and pressing Alt+Enter. And probably by doing some other things that I haven't discovered yet...

解决方案属性在对话框中显示，但 Visual Studio 有一个设计器（称为项目设计器）用于项目属性，它在选项卡中显示。你可以通过以下方式显示项目设计器：在选择项目时单击解决方案资源管理器工具栏按钮；在选择项目时从“项目”菜单中选择“<ProjectName> 属性...”；在解决方案资源管理器中右键单击项目名称并选择“属性”；或者在解决方案资源管理器中选择解决方案名称并按 Alt+Enter。可能还有我尚未发现的其他方法...

The Application tab will change depending on the type of Project you choose, but it always controls the type of application and how it is compiled.

“应用程序”选项卡会根据你选择的项目类型而变化，但它始终控制应用程序的类型及其编译方式。

The Build and Build Events tabs control how the application is DEPLOYED (distributed to users), while the Debug tab controls how the application behaves during testing. We'll look at all of these in the next chapter.

“生成”和“生成事件”选项卡控制应用程序的部署方式（分发给用户），而“调试”选项卡控制应用程序在测试期间的行为。我们将在下一章中查看所有这些内容。

Resources and Settings are things like icons and string that are included in the executable. We'll use the Resources tab in just a minute to create an icon for our application.

资源和设置是包含在可执行文件中的图标和字符串等内容。我们将在稍后使用“资源”选项卡为我们的应用程序创建一个图标。

Signing and Security help you secure your application and its users from bad people and bad software. Security is an important issue, but it's also a huge one, and we won't be talking about it in any detail.

“签名”和“安全”可帮助你保护应用程序及其用户免受不法分子和恶意软件的侵害。安全是一个重要问题，但也是一个庞大的问题，我们不会详细讨论它。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_83_0.png)

The Publish tab is used to deploy your application using ClickOnce. We'll talk about that in the next chapter.

“发布”选项卡用于使用 ClickOnce 部署你的应用程序。我们将在下一章中讨论这个问题。

> Not all of these options are available in every version of Visual Studio. The Code Analysis tab, for example, only appears in Visual Studio Premium and Ultimate, so don't panic if your screen looks a little different from this one. (You are opening these screens, right?)

> 并非所有这些选项在每个版本的 Visual Studio 中都可用。例如，“代码分析”选项卡仅出现在 Visual Studio Premium 和 Ultimate 中，所以如果你的屏幕看起来与这个略有不同，请不要惊慌。（你正在打开这些屏幕，对吧？）

## 添加图标

All Windows applications need an icon. If you don't provide one, Visual Studio will use the default icon. The default image isn't very exciting, and it doesn't distinguish your application from all the others out there. So let's use the Project Properties dialog to add a custom icon to Hello, World. To make that happen in a WPF application (other application types can be a little different), we need just three steps:

所有 Windows 应用程序都需要一个图标。如果你不提供一个，Visual Studio 将使用默认图标。默认图像不太有趣，也无法将你的应用程序与其他应用程序区分开来。所以让我们使用“项目属性”对话框为 Hello, World 添加一个自定义图标。要在 WPF 应用程序中实现此操作（其他应用程序类型可能略有不同），我们只需要三个步骤：

- 1. Specify the icon file in the Application tab of Project Properties.
- 2. Build the application to make the icon available.
- 3. Set the icon property of the window in the WPF Designer.

- 1. 在“项目属性”的“应用程序”选项卡中指定图标文件。
- 2. 生成应用程序以使图标可用。
- 3. 在 WPF 设计器中设置窗口的图标属性。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_84_0.png)

This is the default icon. Pretty boring huh?

这是默认图标。相当无聊，对吧？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_84_1.png)

We'll replace it with this one that looks a bit cooler and represents what our application actually does. This icon file is called conversation.ico, and it's included with the sample code. You can use this one or any other icon file you like. (Try searching for ".ico" in the Windows Explorer.) Just copy it to the application folder for our sample app.

我们将用这个看起来更酷且代表我们应用程序实际功能的图标替换它。这个图标文件名为 conversation.ico，随示例代码一起提供。你可以使用这个图标或任何其他喜欢的图标文件。（尝试在 Windows 资源管理器中搜索“.ico”。）只需将其复制到我们示例应用程序的应用程序文件夹中即可。

## 请注意

Visual Studio includes sample editors for most resource types, including icons, from the Resources tab of Project Properties, or you can also use a third-party tool. You can even open most third-party tools right inside Visual Studio by right-clicking the resource and choosing Open With...

Visual Studio 在“项目属性”的“资源”选项卡中包含大多数资源类型（包括图标）的示例编辑器，或者你也可以使用第三方工具。你甚至可以通过右键单击资源并选择“用...打开”来直接在 Visual Studio 内打开大多数第三方工具。

And if you're not feeling particularly artistic, there are lots of icon sets available for free or fee on the Web that you can use. Just be sure to respect the artists' terms of use, or the karma gods will get you, even if copyright law doesn't.

而且，如果你不太有艺术天赋，网上有很多免费或付费的图标集可供使用。只要确保尊重艺术家的使用条款即可，否则业力之神会找上你，即使版权法不会。

