
# 调试 Interop Forms Toolkit 项目

When you first start planning to work with the toolkit, you might try to keep the `VB6 IDE` on a separate machine from your primary development machine. However, this leads to two issues. First, in order to work with the Interop Forms tools on your `VB6` machine, you need to install the tools package a second time. That’s a minor issue. Second, because `VB6` doesn’t know how to step into `.NET` applications, if you want to debug the Interop Form you created in `.NET`, you have a problem. The solution to this, of course, is to run both development environments on the same machine.

Alternatively, you can try to create a simple Windows Forms EXE that will call and initiate your Interop Forms project from within `.NET`. The debugging isn’t perfect, of course, because you aren’t actually calling your code across the correct interface, but it should enable you to find most pure `.NET` coding issues. You can also leverage the `Debug` and `Trace` classes, but you won’t have any interactive breakpoints in that scenario.

This still leaves unresolved the issue that you can’t just open Visual Studio and expect the `VB6 IDE` to call it when you are in Debug mode. Therefore, this section briefly discusses debugging Interop Forms Toolkit projects when you are running your `VB6` application.

Once you have compiled your `.NET` application, you have a `DLL`. This `DLL` is then exposed to your `VB6` development environment and added as another COM component in your `VB6` application. However, when you debug, you can’t step into this `DLL` from Visual Basic. Presuming you have started your Visual Basic 6.0 project so that its process is now running, your next step is to open Visual Studio and your Interop Forms project. It is hoped that you have set typical breakpoints in your source code and you might even add new breakpoints.

Next, go to the `Tools` menu in Visual Studio and select the `Attach to Process` menu item. At this point, you get a dialog containing a list of running processes. Locate the `Visual Basic 6.0.exe` process. Once you have found this process, which represents the running application in `VB6`, attach to this process.

At this point, you can work with your running application; and when the call is made into your `.NET` code, Visual Studio detects the call into the `DLL` and stops you on your breakpoint. In order for Visual Studio to detect the `DLL` call, you must be calling the same copy of your `DLL` that your Interop Forms project references. In other words, you can’t just copy it off to some other location on your local machine for installation.

> 如果你停止并重新启动 `VB6` 应用程序，Visual Studio 会保持附加状态，但如果你关闭 `VB6 IDE`，则需要在 Visual Studio 中重新附加调试器。

## VB6 开发

总体而言，`VB6` 中的开发过程很简单。一旦你构建了项目或将其部署到安装有 `VB IDE` 的机器上，你需要为 `Microsoft Interop Form Toolkit` 库和你的自定义 `DLL` 添加引用。请记住，这两个 `DLL` 都必须在你的 `VB6 IDE` 机器上注册，才能使其可见。如果你是在同一台机器上构建，那么它们会自动可见。一旦为这些库添加了引用，你就可以创建 Interop Form 的 `Form` 类的新实例并调用标准方法以及你在该表单上公开的任何自定义方法。

需要记住的一个关键点是，如前所述但值得重申，如果你创建了自定义构造函数，要使用它，你需要在 Interop Form 的 `Form` 类上调用 `Initialize` 方法。

## 最终 Interop 提示

如本书前面在讨论 `WPF Interop` 控件时所述，Interop 控件包并不完美。每个都有某些限制，降低了其长期使用的吸引力。为了解决这个问题，请跟踪你已经转换的各个分支的多少。将会有一个时机，需要转换更大的部分，以便减少你正在使用的不同 Interop `DLL` 的数量。

沿着这一思路，注意你不能将 Interop Form 和 Interop 用户控件放在同一个项目中。这些项目各自需要自己的 `DLL`；事实上，你应该将其视为最佳实践，只为单个表单或控件公开 `DLL`。同样，不要计划从你的 Interop Form 中调用 `VB6` 表单。Interop 逻辑是为使你能够从 `VB6` 调用 `.NET` 而编写的。

就接口而言，Interop 层设计为仅支持最少数量的接口类型。特别是 `String`、`Integer` 和 `Boolean` 类型应该是你期望传递的数据的核心。在理论上，`Object` 类型是受支持的，这使你能够传递自定义数据，因此你可以将 `Recordset` 从 `.NET` 传递到 `VB6` 或反之；当然，`VB6` 不知道 `Dataset` 对象，因此你需要将 `VB6` 类型引用为通用对象。一般来说，最佳实践是尽可能保持接口简单。

当你使用项目启动 `VB6 IDE` 时，它会附加到你的 `DLL`。通常这不是问题，直到你第一次运行 `VB6` 应用程序。此时，你无法重建 Interop 项目。Interop 项目实际上被引用，因此被 `VB6` 锁定。如果你需要重建 Interop 项目，你需要先关闭 `VB6` 开发环境，以便你的代码正确引用最新的构建。如前所述，从 `VB6` 调试 Interop 项目并不是最有效的一系列步骤。

如果你更改了任何方法属性，你需要重新生成在创建 Interop Forms 项目的最后一步中生成的 Interop 包装类。此外，虽然没有涉及，但你可以从 `.NET` 向 `VB6` 引发错误。为此，你希望利用在 Interop Form 的一部分中定义的自定义 `My` 命名空间上的以下方法调用：

```
My.InteropToolbox.EventMessenger.RaiseApplicationEvent("CRITICAL_ERROR", _ "Error Detail.")
```

你可能遇到的另一个运行时问题是，某些 `.NET` 应用程序的内部事件不会以与 `VB6` 相同的方式触发。例如，在 `VB6` 下，当你引用 `Form` 类上的属性时，这会触发该类上的 `Load` 事件。在 `.NET` 下，`Load` 事件要到表单显示时才会被触发，因此你需要认识到这对任何先前设置为在 `Load` 事件上运行的代码的影响。

剩余的问题与 `VB6 IDE` 相关。`IDE` 和 `VB6` 实际上并不认识到，如果你启动了一个 `.NET DLL`，就有其他需要释放的内存中类。对于已部署的应用程序，这不是问题，因为当应用程序关闭时，与应用程序关联的所有内存都会自动释放。然而，当你在 `VB6` 中调试时，核心进程与 `IDE` 相关联，而不是你的应用程序。因此，资源在调试周期之间不会被释放。为了确保它们被释放，你可以显式实例化 Interop 帮助文件中包含的一系列代码修改并释放与你的应用程序关联的 `.NET` 资源。建议仅在你与 Interop 工具的引用正常工作后才实现这些调用。

## 使用 POWER PACKS 3.0 工具

与 Interop Forms Toolkit 不同，Power Packs 扩展旨在促进与 `VB6` 中存在的某些开发简便性，例如打印。这些类并非旨在支持 Interop，它们旨在支持迁移，意义在于创建简单几何形状或使用 `VB` 风格的表单打印的代码可以使用与 `VB6` 类似的语法实现。在这些 Power Packs 发布后，打印语法如此受欢迎，以至于 Visual Basic 团队将这些类迁移到 Visual Studio 2008 的核心功能中。3.0 功能的持续成功导致了大部分 3.0 Power Packs 类被包含在 Visual Studio 2008 的 Service Pack 1 中。这些组件以及中继器控件继续随 Visual Studio 2010 一起提供。

与 Interop Forms Toolkit 类似，Power Packs Tools 已为 Visual Studio 2010 安装。对于 Visual Studio 的早期版本，可以从 Microsoft 下载中下载并安装。如果你在 Visual Studio 2010 中查看典型的 Windows Forms 项目，你会看到图 B-4 所示的显示，其中控件已作为默认工具箱的一部分包含在内。

与 Interop Forms Toolkit 不同，无需从特殊项目模板开始。因为 Power Packs 不针对 `VB6`，所以不涉及 COM Interop。它们针对的是希望能够继续以与 `VB6` 中相同的方式实现某些任务的经验丰富的 `VB` 开发人员。

当你的应用程序发布时，你仍需要确保为 Power Packs 库创建依赖项，如果你未使用随 Visual Studio 包含的 `DLL`，则如此，仅此而已。此外，由于 Power Packs 只是另一组 `.NET` 库，因此与调试无关的问题。

对于图 B-4 所示的示例项目，你可以创建一个新的 Windows Forms 应用程序并向其添加 `PrintForm` 控件。Visual Studio 2010 具有 Visual Basic Power Packs 的工具箱部分，显示 `OvalShape` 和 `RectangleShape` 形状控件以及 `LineShape`、`Data Repeater` 和 `PrintForm` 控件，如图 B-4 所示。

在显示的上部添加一个 `RectangleShape`，在显示的中心添加一个 `OvalShape`。在这里不涉及大量细节，使用 Visual Studio 设计器，你应该通过添加各种控件来自定义显示的外观和感觉。花点时间用纯色为形状控件着色和填充。渐变颜色通过选择填充颜色 `Coral`、`FillGradientColor` `Navy`、`FillGradientStyle` `Horizontal` 和 `FillStyle` `Solid` 来定义。所有这些都可以在 Visual Studio 设计器中完成，以实现与图 B-5 所示类似的显示。

![](img/d99870e80390742f93963da7be0b2e61_1155_0.png)

## FIGURE B-4

![](img/d99870e80390742f93963da7be0b2e61_1155_1.png)

## FIGURE B-5

应用程序应该可以构建。下一步是确保图示中右下中心标记为 `Landscape` 的复选框已选中。完成此操作后，将显示底部中心的按钮标记为 `Print Me`，并在设计视图中双击它以触发自动事件处理程序生成。

此打印演示所需的唯一代码位于此按钮的事件处理程序中。该代码隐藏按钮，确定是否选中 `横向` 复选框，并使用 Power Packs 的 `PrintForm` 控件对文档进行打印预览。完成后，`打印我` 按钮将再次可见：

```
Private Sub ButtonPrintForm_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles ButtonPrintForm.Click
' Hide the print button since you don't want to see it in the output.
ButtonPrintForm.Visible = False
' Set the printing to landscape mode by default
PrintForm1.PrinterSettings.DefaultPageSettings.Landscape =
    CheckBox2.Checked
' Update the print action to PrintPreview so instead of wasting paper
' we see what the output would look like if sent to a printer.
PrintForm1.PrintAction = Printing.PrintAction.PrintToPreview
' Execute the print logic.
PrintForm1.Print(Me,
    PowerPacks.Printing.PrintForm.PrintOption.ClientAreaOnly)
'PrintForm1.Print()
' Restore the print button
ButtonPrintForm.Visible = True
End Sub
```

来自 `Form1` 的代码片段

该代码演示了如何引用 `PrinterSettings` 属性，该属性包含用于更改页面打印方式的页面设置。`PrintAction` 定义了控件应执行的操作。有三个选项：打印到默认/选定的打印机、打印到文件或使用 `打印预览` 窗口。在本例中，显示结果 `打印预览` 是最有用的选项。

默认情况下，下一行代码就是你打印当前窗口所需的全部内容。请注意，此控件不会调用窗体来确定窗体上可见的内容，而是实质上是捕获窗体的当前屏幕截图以进行打印。

当前代码使用的是 `ClientAreaOnly` 选项，建议你对其进行测试。如果打开该项目并将其调整得足够宽，然后以纵向模式打印，你将看到该控件如何截断打印图像 `见图 B-6`。

![](img/d99870e80390742f93963da7be0b2e61_1156_0.png)

## 图 B-6

如图 B-6 所示，默认行为是显示屏幕内容而不显示边框。遗憾的是，在本例中，打印输出的内容少于完整的窗口内容。但是，不要停留在这一选项上，试试其他选项。不同的显示选项并不总是能准确捕捉屏幕，所以请进行测试。在某些情况下，打印预览窗口中唯一可见的是形状控件。

但是，在再次打印之前，请转到打印事件处理程序，注释掉带参数的打印行，并取消注释默认打印行。在本例中，指定窗口 `即 Me`，然后添加一个打印选项。现在正确的结果如图 B-7 所示。

![](img/d99870e80390742f93963da7be0b2e61_1157_0.png)

## 图 B-7

总体而言，Power Packs 形状控件使你能够轻松为原本灰色的窗体添加自定义外观。这些控件有些功能有限，但如果你想用快速简便的方式添加图形，它们就能派上用场。同样，`Print` 控件提供了一种快捷简便的方法，为应用程序所显示的内容创建硬拷贝。但是，请记住，`Print` 控件为了提供简单的界面，牺牲了功能和自定义能力。

Power Packs 3.0 提供了 `VB6` 开发人员可用于迁移应用程序的工具；对于快速应用程序设计 `RAD` 原型，它们提供了动态且具有视觉吸引力的显示。只需记住，对于形状控件，如果你需要任何精美的图形，则建议利用 `WPF` 中提供的图形功能。

### 小结

本附录涵盖了 Visual Basic Power Packs。这组非周期发布的工具使经验丰富的 Visual Basic 开发人员能够利用他们的知识和现有代码，结合 `.NET` 的新功能。Visual Basic 团队创建了两个可下载的软件包，它们提高了你管理 COM 到 `.NET` 互操作迁移以及继续以与以前相同的方式打印和创建图形的能力。与所有专注于互操作的解决方案一样，在使用 Interop Forms Toolkit 时存在一些关键限制，但
