

> 如果你停止并重新启动 VB6 应用程序，Visual Studio 会保持附加状态，但如果你关闭 VB6 IDE，则需要在 Visual Studio 中重新附加调试器。

## VB6 开发

总体而言，VB6 中的开发过程很简单。一旦你构建了项目或将其部署到安装有 VB IDE 的机器上，你需要为 Microsoft Interop Form Toolkit 库和你的自定义 DLL 添加引用。请记住，这两个 DLL 都必须在你的 VB6 IDE 机器上注册，才能使其可见。如果你是在同一台机器上构建，那么它们会自动可见。一旦为这些库添加了引用，你就可以创建 Interop Form 的 Form 类的新实例并调用标准方法以及你在该表单上公开的任何自定义方法。

需要记住的一个关键点是，如前所述但值得重申，如果你创建了自定义构造函数，要使用它，你需要在 Interop Form 的 Form 类上调用 Initialize 方法。

## 最终 Interop 提示

如本书前面在讨论 WPF Interop 控件时所述，Interop 控件包并不完美。每个都有某些限制，降低了其长期使用的吸引力。为了解决这个问题，请跟踪你已经转换的各个分支的多少。将会有一个时机，需要转换更大的部分，以便减少你正在使用的不同 Interop DLL 的数量。

沿着这一思路，注意你不能将 Interop Form 和 Interop 用户控件放在同一个项目中。这些项目各自需要自己的 DLL；事实上，你应该将其视为最佳实践，只为单个表单或控件公开 DLL。同样，不要计划从你的 Interop Form 中调用 VB6 表单。Interop 逻辑是为使你能够从 VB6 调用 .NET 而编写的。

就接口而言，Interop 层设计为仅支持最少数量的接口类型。特别是 String、Integer 和 Boolean 类型应该是你期望传递的数据的核心。在理论上，Object 类型是受支持的，这使你能够传递自定义数据，因此你可以将 Recordset 从 .NET 传递到 VB6 或反之；当然，VB6 不知道 Dataset 对象，因此你需要将 VB6 类型引用为通用对象。一般来说，最佳实践是尽可能保持接口简单。

当你使用项目启动 VB6 IDE 时，它会附加到你的 DLL。通常这不是问题，直到你第一次运行 VB6 应用程序。此时，你无法重建 Interop 项目。Interop 项目实际上被引用，因此被 VB6 锁定。如果你需要重建 Interop 项目，你需要先关闭 VB6 开发环境，以便你的代码正确引用最新的构建。如前所述，从 VB6 调试 Interop 项目并不是最有效的一系列步骤。

如果你更改了任何方法属性，你需要重新生成在创建 Interop Forms 项目的最后一步中生成的 Interop 包装类。此外，虽然没有涉及，但你可以从 .NET 向 VB6 引发错误。为此，你希望利用在 Interop Form 的一部分中定义的自定义 My 命名空间上的以下方法调用：

```
My.InteropToolbox.EventMessenger.RaiseApplicationEvent("CRITICAL_ERROR", _ "Error Detail.")
```

你可能遇到的另一个运行时问题是，某些 .NET 应用程序的内部事件不会以与 VB6 相同的方式触发。例如，在 VB6 下，当你引用 Form 类上的属性时，这会触发该类上的 Load 事件。在 .NET 下，Load 事件要到表单显示时才会被触发，因此你需要认识到这对任何先前设置为在 Load 事件上运行的代码的影响。

剩余的问题与 VB6 IDE 相关。IDE 和 VB6 实际上并不认识到，如果你启动了一个 .NET DLL，就有其他需要释放的内存中类。对于已部署的应用程序，这不是问题，因为当应用程序关闭时，与应用程序关联的所有内存都会自动释放。然而，当你在 VB6 中调试时，核心进程与 IDE 相关联，而不是你的应用程序。因此，资源在调试周期之间不会被释放。为了确保它们被释放，你可以显式实例化 Interop 帮助文件中包含的一系列代码修改并释放与你的应用程序关联的 .NET 资源。建议仅在你与 Interop 工具的引用正常工作后才实现这些调用。

## 使用 POWER PACKS 3.0 工具

与 Interop Forms Toolkit 不同，Power Packs 扩展旨在促进与 VB6 中存在的某些开发简便性，例如打印。这些类并非旨在支持 Interop，它们旨在支持迁移，意义在于创建简单几何形状或使用 VB 风格的表单打印的代码可以使用与 VB6 类似的语法实现。在这些 Power Packs 发布后，打印语法如此受欢迎，以至于 Visual Basic 团队将这些类迁移到 Visual Studio 2008 的核心功能中。3.0 功能的持续成功导致了大部分 3.0 Power Packs 类被包含在 Visual Studio 2008 的 Service Pack 1 中。这些组件以及中继器控件继续随 Visual Studio 2010 一起提供。

与 Interop Forms Toolkit 类似，Power Packs Tools 已为 Visual Studio 2010 安装。对于 Visual Studio 的早期版本，可以从 Microsoft 下载中下载并安装。如果你在 Visual Studio 2010 中查看典型的 Windows Forms 项目，你会看到图 B-4 所示的显示，其中控件已作为默认工具箱的一部分包含在内。

与 Interop Forms Toolkit 不同，无需从特殊项目模板开始。因为 Power Packs 不针对 VB6，所以不涉及 COM Interop。它们针对的是希望能够继续以与 VB6 中相同的方式实现某些任务的经验丰富的 VB 开发人员。

当你的应用程序发布时，你仍需要确保为 Power Packs 库创建依赖项，如果你未使用随 Visual Studio 包含的 DLL，则如此，仅此而已。此外，由于 Power Packs 只是另一组 .NET 库，因此与调试无关的问题。

对于图 B-4 所示的示例项目，你可以创建一个新的 Windows Forms 应用程序并向其添加 PrintForm 控件。Visual Studio 2010 具有 Visual Basic Power Packs 的工具箱部分，显示 OvalShape 和 RectangleShape 形状控件以及 LineShape、Data Repeater 和 PrintForm 控件，如图 B-4 所示。

在显示的上部添加一个 RectangleShape，在显示的中心添加一个 OvalShape。在这里不涉及大量细节，使用 Visual Studio 设计器，你应该通过添加各种控件来自定义显示的外观和感觉。花点时间用纯色为形状控件着色和填充。渐变颜色通过选择填充颜色（Coral）、FillGradientColor（Navy）、FillGradientStyle（Horizontal）和 FillStyle（Solid）来定义。所有这些都可以在 Visual Studio 设计器中完成，以实现与图 B-5 所示类似的显示。

![](img/d99870e80390742f93963da7be0b2e61_1155_0.png)

## FIGURE B-4

![](img/d99870e80390742f93963da7be0b2e61_1155_1.png)

## FIGURE B-5

应用程序应该可以构建。下一步是确保图示中右下中心标记为“Landscape”的复选框已选中。完成此操作后，将显示底部中心的按钮标记为“Print Me”，并在设计视图中双击它以触发自动事件处理程序生成。

