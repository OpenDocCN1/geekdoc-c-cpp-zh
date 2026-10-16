

```
</ControlTemplate>
    </Button.Template>
    </Button>
</Canvas>
```

在 OnPrint 处理程序中，可以通过调用 PrintDialog 的 PrintVisual 方法来启动打印作业。PrintVisual 接受任何派生自基类 Visual 的对象（代码文件 PrintingDemo/MainWindow.xaml.cs）：

```
private void OnPrint(object sender, RoutedEventArgs e)
{
    var dlg = new PrintDialog();
    if (dlg.ShowDialog() == true)
    {
        dlg.PrintVisual(canvas1, "Print Demo");
    }
}
```

若要在无需用户干预的情况下以编程方式打印，可以使用 System.Printing 命名空间中的 PrintDialog 类来创建打印作业并调整打印设置。类 LocalPrintServer 提供有关打印队列的信息，并通过 DefaultPrintQueue 属性返回默认的 PrintQueue。可以使用 PrintTicket 配置打印作业。PrintQueue.DefaultPrintTicket 返回与该队列关联的默认 PrintTicket。PrintQueue 的 GetPrintCapabilities 方法返回打印机的功能，根据这些功能，可以按照以下代码段所示配置 PrintTicket。打印票证配置完成后，静态方法 PrintQueue.CreateXpsDocumentWriter 返回一个 XpsDocumentWriter 对象。XpsDocumentWriter 类此前用于创建 XPS 文档，也可以用它来启动打印作业。XpsDocumentWriter 的 Write 方法不仅接受 Visual 或 FixedDocument 作为第一个参数，还接受 PrintTicket 作为第二个参数。如果通过第二个参数传递了 PrintTicket，则写入器的目标就是与该票证关联的打印机，因此写入器会将打印作业发送到该打印机：

```
var printServer = new LocalPrintServer();
PrintQueue queue = printServer.DefaultPrintQueue;
PrintTicket ticket = queue.DefaultPrintTicket;
PrintCapabilities capabilities =
    queue.GetPrintCapabilities(ticket);
if (capabilities.DuplexingCapability.Contains(Duplexing.TwoSidedLongEdge))
    ticket.Duplexing = Duplexing.TwoSidedLongEdge;
if (capabilities.InputBinCapability.Contains(InputBin.AutoSelect))
    ticket.InputBin = InputBin.AutoSelect;
if (capabilities.MaxCopyCount > 3)
    ticket.CopyCount = 3;
if (capabilities.PageOrientationCapability.Contains(PageOrientation.Landscape))
    ticket.PageOrientation = PageOrientation.Landscape;
if (capabilities.PagesPerSheetCapability.Contains(2))
    ticket.PagesPerSheet = 2;
```

```
if (capabilities.StaplingCapability.Contains(Stapling.StapleBottomLeft))
    ticket.Stapling = Stapling.StapleBottomLeft;
XpsDocumentWriter writer =
    PrintQueue.CreateXpsDocumentWriter(queue);
writer.Write(canvas1, ticket);
```

## 小结

在本章中，你学习了如何将 WPF 功能用于文档，如何创建可根据屏幕尺寸自动调整的流文档，以及如何创建始终保持外观一致的固定文档。你还了解了如何打印文档，以及如何将可视元素发送到打印机。

下一章将以部署为主题，结束本书的客户端应用编程部分。

## 36
部署 Windows 应用

### 本章内容

- 部署要求
- 部署场景
- 使用 ClickOnce 进行部署
- 部署 UWP 应用

### 本章的 Wrox.com 代码下载

本章的 wrox.com 代码下载可在 www.wrox.com/go/professionalcsharp6 的 Download Code 选项卡中找到。本章代码包含在以下示例中：

- WPFSampleApp
- UniversalWinApp

## 部署作为应用程序生命周期的一部分

开发过程并不会在源代码编译完成且测试结束时就宣告终止。在这一阶段，将应用程序交付到用户手中的工作才刚刚开始。无论是 ASP.NET 应用程序、WPF 客户端应用程序，还是通用 Windows 平台（UWP）应用，软件都必须部署到目标环境中。

部署应在应用程序设计之初就尽早考虑，因为这可能会影响应用程序本身所使用的技术。

与过去相比，.NET Framework 使部署变得容易得多。注册 COM 组件和向注册表写入新配置单元的麻烦已经消除。

本章从桌面客户端应用程序（WPF）和 UWP 应用两个方面，探讨可用于应用程序部署的选项。

> 注意 Web 应用程序的部署在第 45 章“部署网站和服务”中介绍。

### 规划部署

通常，部署在开发过程中是事后才考虑的事情，这可能会导致令人头疼甚至代价高昂的意外。为了避免部署场景中的烦恼，你应在初始设计阶段就规划部署过程。任何特殊的部署考虑——例如服务器容量、桌面安全性或程序集的加载位置——都应从一开始就纳入设计中，从而使部署过程更加顺畅。

你应在开发过程早期处理的另一个问题是用于测试部署的环境。虽然应用程序代码的单元测试和部署选项可以在开发人员的系统上完成，但部署必须在与目标系统相似的环境中进行测试。这对于消除目标计算机上不存在的依赖关系非常重要。一个例子是第三方库，它可能在项目早期就已安装在开发人员的计算机上，而目标计算机可能没有这个库。很容易忘记将其包含在部署包中。在开发人员的系统上进行测试无法发现该错误，因为该库已经存在。记录依赖关系有助于消除这个潜在问题。

对于大型应用程序，部署过程可能很复杂。在实际实施部署过程时，规划部署可以节省时间和精力。

你必须像对待正在开发的系统其他方面一样，以同样的细心和规划来选择正确的部署选项。选择错误的选项会使将软件交付到用户手中的过程变得困难和令人沮丧。

### 部署选项概述

本节概述了可供 .NET 开发人员使用的部署选项。其中大多数选项将在本章后面更详细地讨论：

- **xcopy**——xcopy 实用程序允许你将一个程序集或一组程序集复制到应用程序文件夹，从而缩短开发时间。由于程序集是自描述的（也就是说，描述程序集的元数据包含在程序集本身中），你无需在注册表中注册任何内容。

  每个程序集都会跟踪它执行所需的其他程序集。默认情况下，程序集会在当前应用程序文件夹中查找依赖项。将程序集移动（或探测）到其他文件夹的过程将在本章后面讨论。

- **ClickOnce**——ClickOnce 技术提供了一种构建自更新 Windows 应用程序的方法。ClickOnce 允许将应用程序发布到网站、文件共享甚至 CD。当应用程序的更新和新版本构建完成后，开发团队可以将它们发布到相同的位置或站点。当最终用户使用应用程序时，它可以自动检查该位置以查看是否有可用更新。如果有，则会尝试更新。

- **Windows Installer**——在某些 ClickOnce 无法满足需求的情况下存在限制。如果安装需要管理员权限（例如，用于部署 Windows 服务），Windows Installer 可能是最佳选择。

- **UWP 应用**——这些应用可以通过 Windows 应用商店或使用命令行工具进行部署。为 Windows 应用商店应用创建包将在本章后面介绍。

### 部署要求

审视基于 .NET 的应用程序的运行时要求是很有启发性的。在任何托管应用程序可以执行之前，CLR 对目标平台有一定的要求。

必须满足的第一个要求是操作系统。目前，以下操作系统可以运行基于 .NET 4.6 的应用程序：

- Windows Vista SP2

