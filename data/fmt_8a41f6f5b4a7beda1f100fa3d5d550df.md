
此应用程序演示了在处理您自己的应用程序中可能遇到的错误和异常时可以使用的多种不同方式。

### 调用方信息

在处理错误时，获取有关错误发生位置的信息通常非常有用。在本章前面，使用`#line`预处理器指令来更改代码的行号，以便借助调用堆栈获得更好的信息。要从代码中获取行号、文件名和成员名称，可以使用 C# 编译器直接支持的属性和可选参数。属性`CallerLineNumber`、`CallerFilePath`和`CallerMemberName`定义在`System.Runtime.CompilerServices`命名空间中，可以应用于参数。通常，对于可选参数，如果调用信息中未提供这些参数，编译器会在方法调用时分配默认值。而对于调用方信息属性，编译器不会填充默认值；而是填充行号、文件路径和成员名称。

代码示例`CallerInformation`使用了以下依赖项和命名空间：

#### 依赖项

- `NETStandard.Library`

#### 命名空间

- `System`
- `System.Runtime.CompilerServices`
- `static System.Console`

以下代码片段中的`Log`方法演示了如何使用这些属性。通过该实现，信息会写入控制台（代码文件`CallerInformation/Program.cs`）：

```csharp
public void Log([CallerLineNumber] int line = -1,
    [CallerFilePath] string path = null,
    [CallerMemberName] string name = null)
{
    WriteLine((line < 0) ? "No line" : "Line" + line);
    WriteLine((path == null) ? "No file path" : path);
    WriteLine((name == null) ? "No member name" : name);
    WriteLine();
}
```

让我们用几种不同的场景来调用这个方法。在下面的`Main`方法中，`Log`方法分别通过`Program`类的实例、在属性的 set 访问器内以及 lambda 表达式内被调用。没有向该方法传入参数值，因此编译器可以替我们填充它们：

```csharp
public static void Main()
{
    var p = new Program();
    p.Log();
    p.SomeProperty = 33;
    Action a1 = () => p.Log();
    a1();
}

private int _someProperty;

public int SomeProperty
{
    get { return _someProperty; }
    set
    {
        Log();
        _someProperty = value;
    }
}
```

运行该程序的结果如下所示。在调用`Log`方法的位置，你可以看到行号、文件名和调用方成员名称。当`Log`位于`Main`方法内部时，成员名称是`Main`。在属性`SomeProperty`的 set 访问器内调用`Log`方法时，显示的是`SomeProperty`。lambda 表达式内的`Log`方法不会显示生成的方法名，而是显示调用该 lambda 表达式的方法名（`Main`），这当然更有用。

```text
Line 12
c:\ProCSharp\ErrorsAndExceptions\CallerInformation\Program.cs
Main
Line 26
c:\ProCSharp\ErrorsAndExceptions\CallerInformation\Program.cs
SomeProperty
Line 14
c:\ProCSharp\ErrorsAndExceptions\CallerInformation\Program.cs
Main
```

在构造函数中使用`Log`方法时，调用方成员名称显示为`ctor`。对于析构函数，调用方成员名称是`Finalize`，因为这是生成的方法名。

> **注意**：`CallerMemberName` **特性**的一个绝佳用途是配合 `INotifyPropertyChanged` *接口的实现*来使用。这个*接口*要求在方法实现中传入属性名。在本书的多个章节中可以看到该接口的实现，例如第 31 章“XAML 应用模式”。

### 小结

本章探讨了 C# 通过异常来处理错误情况所提供的丰富机制。你不限于处理代码可能输出的通用错误代码；相反，你可以深入并专门处理最细粒度的错误情况。有时这些错误情况由 .NET Framework 本身提供；不过，有时你可能需要像本章所示那样编写自己的错误情况。无论哪种情况，你都有很多方法可以保护应用程序的工作流免受不必要且危险的故障影响。

下一章将深入介绍异步编程的重要关键字：`async` 和 `await`。

后台任务可能需要一段时间，并且可能需要在任务仍在运行时将其取消。本章将说明如何做到这一点。

第 21 章“任务与并行编程”和第 22 章“任务同步”涵盖了并行编程的其他信息。

当应用程序不能立即响应请求时，用户会感到很烦。对于鼠标操作，我们已经习惯了延迟，因为这种体验是几十年来养成的。而使用触摸 UI 时，应用程序需要立即响应用户请求。否则，用户会尝试重新执行该操作。

由于在旧版 .NET Framework 中难以实现异步编程，因此在应该采用异步编程的地方，它并不总是被采用。有一款相当频繁阻塞 UI 线程的应用程序，就是旧版 Visual Studio。在那个版本中，打开一个包含数百个项目的解决方案，意味着你可以去享受一段漫长的咖啡休息时间。从 Visual Studio 2012 开始，情况不再如此，因为项目会在后台异步加载，并且首先加载所选项目。Visual Studio 2015 的一项新进展是 NuGet 包管理器，它不再以模态对话框的形式实现。新的 NuGet 包管理器可以在你同时做其他事情时异步加载包信息。这些只是 Visual Studio 2015 中与异步编程相关的重要变化的一小部分例子。

.NET Framework 中的许多 API 同时提供同步和异步版本。由于 API 的同步版本使用起来容易得多，因此经常被用在不适合的地方。在新的 Windows Runtime (WinRT) 中，如果 API 调用预计耗时超过 40 毫秒，则只有异步版本可用。自 C# 5 起，异步编程已经变得和同步编程一样容易，因此使用异步 API 不应有任何障碍。

### 异步模式

在深入介绍新的 `async` 和 `await` 关键字之前，最好先了解 .NET Framework 中的异步模式。自 .NET 1.0 起就有了异步功能，.NET Framework 中的许多类实现了一种或多种此类模式。异步模式也可用于委托类型。

由于使用异步模式在 UI（无论是 Windows Forms 还是 WPF）上执行更新相当复杂，.NET 2.0 引入了基于事件的异步模式。在这种模式中，事件处理程序从拥有同步上下文的线程中调用，因此使用这种模式可以轻松处理 UI 代码的更新。

以前，这种模式也被称为异步*组件模式*。

.NET 4.5 引入了另一种实现异步编程的方式：*基于任务的异步模式*（TAP）。这种模式基于 `Task` 类型，并利用编译器对 `async` 和 `await` 关键字的支持。

为了理解 `async` 和 `await` 关键字的优势，第一个示例应用程序使用 Windows Presentation Foundation (WPF) 和网络编程来概览异步编程。如果你没有 WPF 和网络编程经验，不要灰心。你仍然可以跟上这里的要点，理解异步编程是如何实现的。下面的示例演示了这些异步模式之间的差异。看完这些示例后，你将通过一些简单的控制台应用程序了解异步编程的基础知识。

> **注意**：*WPF 将在第 29 章至第 31 章以及第 34 章至第 36 章中详细讲解。网络编程在第 25 章“网络”中讨论。*

用来展示异步模式差异的示例应用是一个 WPF 应用，它使用了类库中的类型。该应用使用 Bing 和 Flickr 服务在网上查找图像。用户可以输入搜索词来查找图像，搜索词会通过一个简单的 HTTP 请求发送到 Bing 和 Flickr 服务。

Visual Studio 设计器中的 UI 设计如 _图 15.1_ 所示。屏幕顶部是一个文本输入框，后面是几个按钮，用于启动搜索或清空结果列表。控件区域下方的左侧包含一个 `ListBox`，用于显示所有找到的图像。右侧是一个 `Image` 控件，用于以更高分辨率显示在 `ListBox` 控件中选中的图像。

![](img/3d365b72b289213a91ade7eb366b8f35_528_0.png)

**图 15.1**

为了理解示例应用，我们先从包含几个辅助类的类库`AsyncLib`开始。这些类由 WPF 应用使用。

`SearchItemResult` 类表示结果集合中的一个项，用于显示图像以及图像的标题和来源。这个类只定义了简单的属性：`Title`、`Url`、`ThumbnailUrl` 和 `Source`。`ThumbnailUrl` 属性用于引用缩略图，`Url` 属性包含指向更大尺寸图像的链接，`Title` 包含描述图像的一些文本。`SearchItemResult` 的基类是 `BindableBase`。该基类通过实现 `INotifyPropertyChanged` 接口来实现通知机制，WPF 使用该接口通过数据绑定进行更新（代码文件 `AsyncLib/SearchItemResult.cs`）：

```
namespace Wrox.ProCSharp.Async
{
    public class SearchItemResult : BindableBase
    {
        private string _title;
        public string Title
        {
            get { return _title; }
            set { SetProperty(ref _title, value); }
        }
        private string _url;
        public string Url
        {
            get { return _url; }
            set { SetProperty(ref _url, value); }
        }
        private string _thumbnailUrl;
        public string ThumbnailUrl
        {
            get { return _thumbnailUrl; }
            set { SetProperty(ref _thumbnailUrl, value); }
        }
        private string _source;
        public string Source
        {
            get { return _source; }
            set { SetProperty(ref _source, value); }
        }
    }
}
```

`SearchInfo` 类是另一个用于数据绑定的类。`SearchTerm` 属性包含用户输入，用于搜索此类图像。`List` 属性返回一个列表，其中包含以 `SearchItemResult` 类型表示的所有已找到图像（代码文件 `AsyncLib/SearchInfo.cs`）：

```
using System.Collections.ObjectModel;

namespace Wrox.ProCSharp.Async
{
    public class SearchInfo : BindableBase
    {
```

```xml
<StackPanel HorizontalAlignment="Stretch" Orientation="Vertical" Background="{StaticResource linearBackgroundBrush}">
    <TextBlock Text="{Binding Source}" Foreground="White" />
    <TextBlock Text="{Binding Title}" Foreground="White" />
    <Image HorizontalAlignment="Center" Source="{Binding ThumbnailUrl}" Width="100" />
</StackPanel>
</Grid>
</DataTemplate>
</ListBox.ItemTemplate>
</ListBox>
<GridSplitter Grid.Column="1" Width="3" HorizontalAlignment="Left" />
<Image Grid.Column="1" Source="{Binding List/Url}" />
</Grid>
```

现在让我们进入`BingRequest`类。这个类包含一些关于如何向 Bing 服务发起请求的信息。该类的`Url`属性返回一个 URL 字符串，可用于请求图片。该请求由搜索词、应请求的图片数量（`Count`）和要跳过的图片数量（`Offset`）组成。使用 Bing 需要进行身份验证。用户 ID 通过`AppId`定义，并与`Credentials`属性一起使用，该属性返回一个`NetworkCredential`对象。要运行该应用程序，你需要在 Windows Azure Marketplace 中注册并订阅 Bing Search API。在撰写本文时，每月最多有 5000 次免费事务——这应该足够运行示例应用程序了。每次搜索算一次事务。Bing Search API 的注册链接是 https://datamarket.azure.com/dataset/bing/search。注册后，你需要复制账户密钥。获得应用程序账户密钥后，将其复制到`BingRequest`类的`AppID`中。

通过使用创建的 URL 向 Bing 发送请求后，Bing 会返回 XML。`BingRequest`类的`Parse`方法解析该 XML，并返回一个`SearchItemResult`对象的集合（代码文件`AsyncLib/BingRequest.cs`）：

> 注意：`BingRequest`和`FlickrRequest`类中的`Parse`方法使用了 LINQ to XML。有关如何使用 LINQ to XML，请参阅第 27 章“XML 和 JSON”。

```csharp
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Xml.Linq;

namespace Wrox.ProCSharp.Async
{
    public class BingRequest : IImageRequest
    {
        private const string AppId = "enter your Bing AppId here";

        public BingRequest()
        {
            Count = 50;
            Offset = 0;
        }

        private string _searchTerm;
        public string SearchTerm
        {
            get { return _searchTerm; }
            set { _searchTerm = value; }
        }

        public ICredentials Credentials => new NetworkCredential(AppId, AppId);

        public string Url =>
            $"https://api.datamarket.azure.com/" +
            "Data.ashx/Bing/Search/v1/Image?Query=%27{SearchTerm}%27&" +
            "$top={Count}&$skip={Offset}&$format=Atom";

        public int Count { get; set; }
        public int Offset { get; set; }

        public IEnumerable<SearchItemResult> Parse(string xml)
        {
            XElement respXml = XElement.Parse(xml);
            XNamespace d = XNamespace.Get(
                "http://schemas.microsoft.com/ado/2007/08/dataservices");
            XNamespace m = XNamespace.Get(
```
