
动画类具有`EasingFunction`属性。此属性接受实现`IEasingFunction`接口的对象（使用 WPF）或派生自基类`EasingFunctionBase`（使用 Windows 通用应用）。使用此类型，缓动函数对象可以定义值随时间如何被动画化。有多种缓动函数可用于创建非线性动画。示例包括使用指数公式进行动画的`ExponentialEase`；使用 2、3、4 或 5 次幂的`QuadraticEase`、`CubicEase`、`QuarticEase`和`QuinticEase`；以及具有可配置幂级的`PowerEase`。特别有趣的是使用正弦曲线的`SineEase`；创建弹跳效果的`BounceEase`；以及类似于弹簧来回振荡的动画值的`ElasticEase`。

以下代码片段将`BounceEase`函数添加到`DoubleAnimation`。添加不同的缓动函数会产生非常有趣的动画效果：

```
<DoubleAnimation Storyboard.TargetProperty="(Ellipse.Width)" Duration="0:0:3" AutoReverse="True" FillBehavior=" RepeatBehavior="Forever" From="100" To="300">
<DoubleAnimation.EasingFunction>
<BounceEase EasingMode="EaseInOut" />
</DoubleAnimation.EasingFunction>
</DoubleAnimation>
```

要查看不同的缓动动画效果，下一个示例让椭圆在两个小矩形之间移动。`Rectangle`和`Ellips`元素在`Canvas`内定义，并且椭圆定义了一个`TranslateTransform`变换来移动椭圆（代码文件`Animation[WPF|UWP]\EasingFunctions.xaml`）：

```
<Canvas Grid.Row="1">
<Rectangle Fill="Blue" Width="10" Height="200" Canvas.Left="50" Canvas.Top="100" />
<Rectangle Fill="Blue" Width="10" Height="200" Canvas.Left="550" Canvas.Top="100" />
<Ellipse Fill="Red" Width="30" Height="30" Canvas.Left="60" Canvas.Top="185">
<Ellipse.RenderTransform>
<TranslateTransform x:Name="translate1" X="0" Y="0" />
</Ellipse.RenderTransform>
</Ellipse>
</Canvas>
```

图 30.25 显示了矩形和椭圆。

# 31 使用 XAML 应用的模式

## 本章内容？

- 代码共享
- 创建模型
- 创建存储库
- 创建视图模型
- 定位器
- 依赖注入
- 视图模型之间的消息传递
- 使用 IoC 容器

## 本章 Wrox.com 代码下载

本章的 wrox.com 代码下载可在`www.wrox.com/go/professionalcsharp6`的 Download Code 选项卡上找到。本章的代码分为以下主要示例：

- Books Desktop App (WPF)
- Books Universal App (UWP)

## 为什么使用 MVVM？

技术和框架在不断变化。我使用 ASP.NET Web Forms 创建了我的公司网站（`http://www.cninnovation.com`）的第一个版本。当 ASP.NET MVC 出现时，我尝试将其用于将我网站的一个功能迁移到 MVC。进展比我预期的要快得多。在一天之内，我就将整个网站转换为了 MVC。该网站使用 SQL Server，集成 RSS 源，并显示培训和书籍。有关培训和书籍的信息来自 SQL Server 数据库。快速迁移到 ASP.NET MVC 只有在我从一开始就进行关注点分离的情况下才有可能；我为数据访问和业务逻辑创建了单独的层。使用 ASP.NET Web Forms，可以直接在 ASPX 页面中使用数据源和数据控件。分离数据访问和业务逻辑在开始时花费了更多时间，但最终证明是巨大的优势，因为它允许单元测试和重用。由于我以这种方式分离了事物，因此迁移到另一种技术变得轻而易举。

就 Windows 应用程序而言，技术变化也很快。多年来，Windows Forms 是将原生 Windows 控件包装起来创建桌面应用程序的首选技术。接下来是 Windows Presentation Foundation（WPF），其中用户界面使用 XML for Applications Markup Language（XAML）定义。Silverlight 提供了一个轻量级框架，用于在浏览器内运行基于 XAML 的应用程序。Windows 8 之后推出了 Windows Store 应用，并在 Windows 8.1 中改为可在 PC 和 Windows Phone 上运行的通用 Windows 应用。借助 Windows 8.1 和 Visual Studio 2013，创建了三个具有共享代码的项目，以同时支持 PC 和手机。这一变化在 Visual Studio 2015、Windows 10 和通用 Windows 平台（UWP）中发生。您可以拥有一个项目来支持 PC、手机、Xbox One、Windows IoT、Surface Hub 等大型屏幕，甚至微软的 HoloLens。

一个项目支持所有 Windows 10 平台可能不符合您的需求。您能编写仅支持 Windows 10 的程序吗？有些客户可能仍在使用 Windows 7。在这种情况下，WPF 是答案，但它不支持手机和其他 Windows 10 设备。关于支持 Android 和 iOS 呢？您也可以使用 Xamarin 在此创建`C#`和`.NET`代码，但它有所不同。

目标应该是尽可能重用代码，支持所需的平台，并轻松地从一种技术切换到另一种技术。这些目标——在许多组织中，管理与开发作为 DevOps 结合，以快速向用户提供新功能和错误修复——需要自动化测试。单元测试是必须的，需要由应用程序架构支持。

对于基于 XAML 的应用程序，Model-View-ViewModel（MVVM）设计模式被青睐用于将视图与功能分离。此设计模式由 Expression Blend 团队的 John Gossman 发明，作为对 Model-View-Controller（MVC）和 Model-View-Presenter（MVP）模式的改进，更适合 XAML，因为它使用数据绑定，这是 XAML 的头号功能。

对于基于 XAML 的应用程序，XAML 文件和代码隐藏文件紧密耦合在一起。这使得重用代码隐藏变得困难，也难以进行单元测试。为了解决这个问题，MVVM 模式允许代码与用户界面之间更好地分离。

原则上，MVVM 模式并不难理解。然而，当您基于 MVVM 模式创建应用程序时，您需要关注更多需求：多种模式会发挥作用以使应用程序工作并使重用成为可能，包括用于实现独立性的依赖注入机制以及视图模型之间的通信。

所有这些内容都在本章中介绍，有了这些信息，您就可以不仅使用相同的代码与 Windows 应用和 Windows 桌面应用程序，但借助 Xamarin，你也可以将其用于 iOS 和 Android。本章将为你提供一个示例应用，涵盖支持不同技术所需的各种不同方面和模式，以实现良好的分离。

> **NOTE** 单元测试在第 19 章“Testing”中介绍。

## 定义 MVVM 模式

首先，让我们看看 MVC 设计模式，它是 MVVM 模式的起源之一。*模型-视图-控制器*（MVC）模式将模型、视图和控制器分离开来（参见图 31.1）。模型定义了视图中显示的数据，以及关于如何更改和操作数据的业务规则。控制器是模型和视图之间的管理者，负责更新模型，并将数据发送到视图进行显示。当用户请求到来时，控制器采取行动，使用模型，并更新视图。

![](img/3d365b72b289213a91ade7eb366b8f35_1162_0.png)

**图 31.1**

> **注意** *MVC 模式在 ASP.NET MVC 中被广泛使用，相关内容将在第 41 章“ASP.NET MVC”中介绍。*

使用*模型-视图-展示器*（MVP）模式（参见图 31.2）时，用户与视图交互。展示器包含视图的所有业务逻辑。展示器可以通过使用视图的接口作为契约与视图解耦。这样就便于更改视图实现以进行单元测试。使用 MVP 时，视图和模型彼此完全隔离。

![](img/3d365b72b289213a91ade7eb366b8f35_1163_0.png)

**图 31.2**

基于 XAML 的应用程序使用的主要模式是*模型-视图-视图模型*（MVVM）模式（参见图 31.3）。该模式充分利用了 XAML 的数据绑定功能。使用 MVVM 时，用户与视图交互。视图使用数据绑定访问视图模型中的信息，并调用同样在视图中绑定的视图模型中的命令。视图模型不直接依赖视图。视图模型本身使用模型来访问数据，并从模型获取更改信息。

![](img/3d365b72b289213a91ade7eb366b8f35_1163_1.png)

**图 31.3**

在本章接下来的各节中，你将看到如何在应用程序中使用此架构来创建视图、视图模型、模型以及其他所需模式。

## 共享代码

在创建示例解决方案并开始创建模型之前，我们需要退一步，看看如何在不同平台之间共享代码的不同选项。本节将介绍用于应对你需要支持的不同平台和你所需 API 的不同选项。

### 在通用 Windows 平台上使用 API 契约

通用 Windows 平台定义了一套适用于所有 Windows 10 设备的 API。但是，此 API 可能会随着较新的版本而改变。通过“项目属性”中的“应用程序设置”（参见图 31.4），你可以定义应用程序的*目标版本*（即你要为其构建的版本）和系统所需的*最低版本*。你选择的所有软件开发工具包（SDK）的版本都需要安装在你的系统上，这样你才能验证哪些 API 可用。要使用目标版本中提供、但最低版本中不可用的功能，你需要在调用该 API 之前以编程方式检查设备是否支持你需要的特定功能。

![](img/3d365b72b289213a91ade7eb366b8f35_1164_0.png)

**图 31.4**

使用 UWP，你可以支持不同的设备系列。UWP 定义了多个设备系列：通用、桌面（PC）、移动（平板、平板手机、手机）、IoT（Raspberry Pi、Microsoft Band）、Surface Hub、全息（HoloLens）和 Xbox。随着时间的推移，还会有更多设备系列出现。这些设备系列中的每一个都提供了仅适用于该设备系列的 API。设备系列的 API 通过 API 契约来指定。每个设备系列可以提供多个 API 契约。

你可以使用特定于设备系列的功能，但仍然可以创建一个能在所有设备上运行的二进制映像。通常，你的应用程序不会支持所有设备系列，但可能会支持其中的几个。要支持特定的设备系列并使用这些系列的 API，你可以从解决方案资源管理器中添加扩展 SDK；选择“引用 ➔ 添加引用”，然后选择“通用 Windows ➔ 扩展”（参见图 31.5）。在那里你可以看到已安装的 SDK，并选择你需要的 SDK。

![](img/3d365b72b289213a91ade7eb366b8f35_1165_0.png)

**图 31.5**

选择扩展 SDK 后，一旦验证 API 契约可用，你就可以在代码中使用该 API。`ApiInformation`类（命名空间`Windows.Foundation.Metadata`）定义了`IsApiContractPresent()`方法，你可以通过它检查具有特定主版本和次版本的特定 API 契约是否可用。下面的代码片段请求`Windows.Phone.PhoneContract`主版本 1。如果此契约可用，则可以使用`VibrationDevice`：

```
if
(ApiInformation.IsApiContractPresent("Windows.Phone.PhoneContract", 1))
{
    VibrationDevice vibration = VibrationDevice.GetDefault();
    vibration.Vibrate(TimeSpan.FromSeconds(1));
}
```

你可能会担心最终得到到处使用 API 契约检查的错综复杂的代码。如果你只面向单个设备系列，则无需检查 API 是否存在。在前面的示例中，如果应用程序只面向手机，就不需要 API 检查。如果你面向多个设备平台，则只需检查要调用的设备特定 API。仅使用通用 API，你就能编写出涵盖多个设备系列的有用应用。如果你要支持多个设备系列并涉及大量设备特定 API 调用，我建议你避免使用`ApiInformation`，而是使用依赖注入，这将在本章后面的“服务与依赖注入”一节中介绍。

### 使用共享项目

使用 API 契约共享同一二进制文件只适用于通用 Windows 平台。如果你需要共享代码，例如在 Windows 桌面应用程序（使用 WPF）与 UWP 应用之间，或 Xamarin.Forms 应用与 UWP 应用之间共享，则不能采用此方案。当你创建这些无法使用同一二进制文件的项目类型时，可以使用 Visual Studio 2015 的共享项目模板。

Visual Studio 的共享项目模板创建的项目不会生成二进制文件——不会构建任何程序集。相反，代码会在引用该共享项目的所有项目之间共享。你需要在每个引用共享项目的项目中编译代码。

当你创建如下代码片段所示的类时，此类可以用于所有引用共享项目的项目。你甚至可以使用预处理器指令编写特定于平台的代码。Visual Studio 2015 的通用 Windows 应用模板设置了条件编译符号`WINDOWS_UWP`，因此你可以使用该符号标记那些只应在通用 Windows 平台上编译的代码。对于 WPF，你可以在 WPF 项目中向条件编译符号添加`WPF`。

```
public partial class Demo
{
    public int Id { get; set; }
    public string Title { get; set; }

#if WPF
    public string WPFOnly { get; set; }
#endif

#if WINDOWS_UWP
    public string WinAppOnly {get; set; }
#endif
}
```

使用 Visual Studio 编辑器编辑共享代码时，你可以在左上角栏中选择项目名称，当前项目未激活的代码部分会变暗（参见图 31.6）。编辑文件时，IntelliSense 也会为所选项目提供相应的 API。

![](img/3d365b72b289213a91ade7eb366b8f35_1167_0.png)

**图 31.6**

除了使用预处理器指令，你还可以在 WPF 或通用 Windows 平台项目中维护类的不同部分。将类声明为`partial`是有充分理由的。

> **注意** `C#` `partial` *关键字* 在第 3 章“对象和类型”中解释。

当你在 WPF 项目中以相同命名空间定义相同类名时，就可以扩展共享类。也可以使用基类（如果共享项目没有定义基类）：

```
public class MyBase
{
    // etc.
}
public partial class Demo: MyBase
{
    public string WPFTitle => $"WPF {Title}";
}
```

### 使用可移植类库

还有另一种共享代码的方式：共享库。如果所有技术都可以使用 .NET Core，那就很简单：只需创建一个 .NET Core 库，就可以在不同平台之间共享它。如果你需要支持的技术可以使用 .NET Core NuGet 包，最好使用这些包。如果不能，则可以使用可移植类库。

> **注意** 创建 NuGet 包在第 17 章“Visual Studio 2015”中进行了讨论。

使用可移植库，Microsoft 维护着一个庞大的列表，说明哪些 API 由哪个平台支持。当你创建可移植库时，会看到配置需要支持的目标平台的对话框。图 31.7 显示了对 .NET Framework 4.6、Windows Universal 10.0、Xamarin.Android 和 Xamarin.iOS 的选择。通过此选择，你只能使用所有所选目标平台都可用的 API。通过当前选择，你可以在对话框中看到说明 .NET Framework 4.5、Windows 8 和 Xamarin.iOS（Classic）也会自动被定位，因为这些平台没有任何 API 是不在所选组合交集中的。

![](img/3d365b72b289213a91ade7eb366b8f35_1168_0.png)

**图 31.7**

可移植库的巨大缺点是，你不能拥有仅在特定平台上可用的代码。你只能使用在所有所选目标平台上都可用的内容。作为一种变通方法，你可以使用可移植库来定义合约的代码，并在需要时用特定于平台的库来实现这些合约。要将来自特定于平台的库的代码与非特定于平台的库一起使用，可以使用依赖注入。如何做到这一点是本章更大示例的一部分，在“View Models”部分中进行了介绍。

## 示例解决方案

示例解决方案由一个用于显示和编辑书籍列表的 WPF 应用程序和一个通用 Windows 平台应用程序组成。为此，解决方案使用了以下项目：

- `BooksDesktopApp` — 用于 .NET Framework 4.6 桌面应用程序 UI 的 WPF 项目
- `BooksUniversalApp` — 用于现代应用 UI 的 UWP 应用项目
- `Framework` — 包含对所有基于 XAML 的应用程序有用的类的可移植库
- `ViewModels` — 包含 WPF 和 UWP 共用的视图模型的可移植库
