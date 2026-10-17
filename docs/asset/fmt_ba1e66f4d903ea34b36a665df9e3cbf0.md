
```
public void ConfigureServices(IServiceCollection services)
{
    services.AddLocalization(
        options => options.ResourcesPath = "CustomResources");
}
```

通过依赖注入，`IStringLocalizer<Startup>` 作为 `Configure` 方法的参数被注入。泛型类型 `Startup` 参数用于在资源目录中找到同名的资源文件；这与 `Startup.resx` 相匹配。

```
public void Configure(IApplicationBuilder app,
IStringLocalizer<Startup> sr)
{
    // etc.
}
```

以下代码片段使用类型为 `IStringLocalizer<Startup>` 的 `sr` 变量，通过索引器和 `GetString` 方法访问名为 `message1` 的资源。资源 `message2` 使用字符串格式占位符，这些占位符通过 `GetString` 方法的重载注入，可以传递任意数量的参数：

```
public void Configure(IApplicationBuilder app,
IStringLocalizer<Startup> sr)
{
    // etc.
    app.Run(async context =>
    {
        // etc.
        await context.Response.WriteAsync($"<div>{sr["message1"]}</div>");
        await context.Response.WriteAsync($"<div>{sr.GetString("message1")}</div>");
        await context.Response.WriteAsync($"<div>{sr.GetString("message2", requestCulture.Culture, requestCulture.UICulture)}</div>");
    });
}
string localized1 = sr["message1"];
```

`message2` 的资源使用字符串格式占位符定义：

```
Using culture {0} and UI culture {1}
```

运行 Web 应用程序后，结果显示如图 28.8 所示的视图。

![](img/3d365b72b289213a91ade7eb366b8f35_1054_0.png)

图 28.8

### 使用通用 Windows 平台进行本地化

使用通用 Windows 平台（UWP）进行本地化基于你迄今为止学到的概念，但它带来了本节所述的一些新想法。为了获得最佳体验，你需要安装可通过 Visual Studio 扩展和更新获得的多语言应用工具包。

文化、区域和资源的概念是相同的，但由于 Windows 应用可以用 C# 和 XAML、C++ 和 XAML 以及 JavaScript 和 HTML 编写，这些概念需要对所有语言可用。只有 Windows Runtime 可用于所有这些编程语言和 Windows Store 应用。因此，Windows Runtime 中提供了用于全球化和资源的新命名空间：`Windows.Globalization` 和 `Windows.ApplicationModel.Resources`。借助全球化命名空间，你可以找到 `Calendar`、`GeographicRegion`（与 .NET `RegionInfo` 相比）和 `Language` 类。借助子命名空间，还有根据语言变化的数字和日期格式化类。使用 C# 和 Windows 应用时，你仍然可以使用 .NET 类来处理文化和区域。

让我们通过一个示例来了解通用 Windows 应用中的本地化。创建一个小型应用程序，使用 Blank App（Universal App）Visual Studio 项目模板。将两个 `TextBlock` 控件和一个 `TextBox` 控件添加到页面。

```
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    base.OnNavigatedTo(e);
    txt1.Text = DateTime.Today.ToString("D");
    //...
}
```

#### 在 UWP 中使用资源

在 UWP 中，你可以使用文件扩展名为 `resw` 而不是 `resx` 创建资源文件。在幕后，`resw` 文件使用相同的 XML 格式，并且你可以使用相同的 Visual Studio 资源编辑器创建和修改这些文件。以下示例使用如图 28.9 所示的结构。子目录 `Messages` 包含一个子目录 `en-us`，其中创建了两个资源文件 `Errors.resw` 和 `Messages.resw`。在文件夹 `Strings\en-us` 中，创建了资源文件 `Resources.resw`。

![](img/3d365b72b289213a91ade7eb366b8f35_1056_0.png)

图 28.9

`Messages.resw` 文件包含一些英文文本资源，`Hello` 的值为 `Hello World`，以及名为 `GoodDay`、`GoodEvening` 和 `GoodMorning` 的资源。文件 `Resources.resw` 包含资源 `Text3.Text` 和 `Text3.Width`，其值分别为 `"This is a sample message for Text 4"` 和 `"300"`。

借助代码，你可以使用来自命名空间 `Windows.ApplicationModel.Resources` 的 `ResourceLoader` 类访问资源。在此你使用字符串 `"Messages"` 调用 `GetForCurrentView` 方法。因此，你使用的是资源文件 `Messages.resw`。调用 `GetString` 方法检索键为 `"Hello"` 的资源（代码文件 `UWPLocalization/MainPage.xaml.cs`）：

```
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    // etc.
    var resourceLoader =
ResourceLoader.GetForCurrentView("Messages");
    text2.Text = resourceLoader.GetString("Hello");
}
```

在 UWP Windows 应用中，直接从 XAML 代码使用资源也很简单。以下 `TextBox` 的 `x:Uid` 属性被赋值为 `Text3`。这样，就会在资源文件 `Resources.resw` 中搜索名为 `Text3` 的扩展资源。该资源文件包含键 `Text3.Text` 和 `Text3.Width` 的值。检索值后，`Text` 和 `Width` 属性将被设置（代码文件 `UWPLocalization/MainPage.xaml`）：

```
<TextBox x:Uid="FileName_Text3" HorizontalAlignment="Left" Margin="50" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top"/>
```

#### 使用多语言应用工具包进行本地化

要本地化 UWP 应用，你可以下载前面提到的多语言应用工具包。该工具包与 Visual Studio 2015 集成。安装工具包后，你可以在 Visual Studio 中通过菜单 `Tools → Multilingual App Toolkit → Enable Selection` 来启用它。这会在项目文件中添加一个构建命令，并在解决方案资源管理器中添加一个上下文菜单选项。在解决方案资源管理器中打开上下文菜单并选择 `Multilingual App Toolkit → Add Translation Languages` 以调用如图 28.10 所示的对话框，在其中可以选择应翻译的语言。示例使用伪语言、法语、德语和西班牙语。对于这些语言，可使用 Microsoft Translator。此工具现在创建包含所选语言 `.xlf` 文件的 `MultilingualResources` 子目录。`.xlf` 文件使用 XLIFF（XML 本地化互换文件格式）标准定义。这是开放式 XML 作者和本地化参考架构（OAXAL）的标准。

![](img/3d365b72b289213a91ade7eb366b8f35_1058_0.png)

图 28.10

> NOTE 多语言应用工具包也可以从 `http://aka.ms/matinstallv4` 安装，而无需使用 Visual Studio。下载多语言应用工具包。

下一次为项目启动构建过程时，XLIFF 文件将被所有资源的内容填充。当你在解决方案资源管理器中选择 XLIFF 文件时，可以将其发送进行翻译。为此，在选择 `.xlf` 文件时打开解决方案资源管理器中的上下文菜单，并选择 `Multilingual App Toolkit → Export Translations…`，这将打开如图 28.11 所示的对话框。通过此对话框，你可以配置应发送的信息，并可以发送一封附带 XLIFF 文件的电子邮件。

![](img/3d365b72b289213a91ade7eb366b8f35_1059_0.png)

#### 图 28.11

要进行翻译，你也可以使用微软的翻译服务。在 Visual Studio 解决方案资源管理器中选择 `.xlf` 文件，打开上下文菜单后，选择多语言应用工具包 ⇨ 生成机器翻译。

打开 `.xlf` 文件时，会打开多语言编辑器（见图 28.12）。使用该工具，你可以检查自动翻译并进行必要的修改。

![](img/3d365b72b289213a91ade7eb366b8f35_1060_0.png)

#### 图 28.12

不要未经人工审阅就使用机器翻译。该工具会为每个已翻译的资源显示状态。自动翻译后，状态会设置为需要审阅。你可能见过一些应用程序的机器翻译不准确——有时甚至非常可笑。

### 创建自定义区域性

随着时间推移，.NET Framework 支持的语言越来越多。然而，并非世界上所有语言都可用于 .NET，对于这些语言，你可以创建自定义区域性。例如，创建自定义区域性有助于支持某一区域内的少数群体，或为不同方言创建子区域性。

你可以使用 `System.Globalization` 命名空间中的 `CultureAndRegionInfoBuilder` 类创建自定义区域性和区域。该类位于程序集 `sysglob1` 中。

通过 `CultureAndRegionInfoBuilder` 类的构造函数，你可以传入区域性的名称。构造函数的第二个参数需要 `CultureAndRegionModifiers` 类型的枚举。该枚举允许三个值之一：`Neutral` 表示中性区域性，`Replacement` 表示应替换现有的框架区域性，或者 `None`。

实例化 `CultureAndRegionInfoBuilder` 对象后，可以通过设置属性来配置区域性。通过该类的属性，你可以定义所有区域性和区域信息，例如名称、日历、数字格式、度量信息等。如果区域性应基于现有的区域性和区域，可以使用 `LoadDataFromCultureInfo` 和 `LoadDataFromRegionInfo` 方法设置实例的属性，然后再通过设置属性来更改不同的值。

调用 `Register` 方法可在操作系统中注册新的区域性。实际上，你可以在目录 `<windows>\Globalization` 中找到描述该区域性的文件。查找扩展名为 `.nlp` 的文件（代码文件 `CustomCultures\Program.cs`）：

```
using System;
using System.Globalization;
using static System.Console;

namespace CustomCultures
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Create a Styria culture
                var styria = new CultureAndRegionInfoBuilder("de-AT-ST",
                    CultureAndRegionModifiers.None);
                var cultureParent = new CultureInfo("de-AT");
                styria.LoadDataFromCultureInfo(cultureParent);
                styria.LoadDataFromRegionInfo(new RegionInfo("AT"));
                styria.Parent = cultureParent;
                styria.RegionNativeName = "Steiermark";
                styria.RegionEnglishName = "Styria";
                styria.CultureEnglishName = "Styria (Austria)";
                styria.CultureNativeName = "Steirisch";
                styria.Register();
            }
            catch (UnauthorizedAccessException ex)
            {
                WriteLine(ex.Message);
            }
        }
    }
}
```

由于在系统上注册自定义语言需要管理权限，示例应用程序使用控制台应用程序项目模板生成，并添加了应用程序清单文件。该清单文件指定请求的执行权限。在项目属性中，需要在应用程序设置中设置该清单文件：

```
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1"
xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>
    <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">
        <security>
            <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
                <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
            </requestedPrivileges>
        </security>
    </trustInfo>
</asmv1:assembly>
```

现在，你可以像使用其他区域性一样使用新创建的区域性：

```
var ci = new CultureInfo("de-AT-ST");
CultureInfo.CurrentCulture = ci;
CultureInfo.CurrentUICulture = ci;
```

你可以将该区域性用于格式化和资源。如果启动本章前面编写的 `Cultures In Action` 应用程序，你也可以看到自定义区域性。

### 小结

本章演示了如何对 .NET 应用程序进行全球化和本地化。对于应用程序的全球化，你学习了如何使用 `System.Globalization` 命名空间来格式化依赖于区域性的数字和日期。此外，你还了解到字符串排序默认会因区域性而异，并了解了使用固定区域性进行与区域性无关的排序。通过使用 `CultureAndRegionInfoBuilder` 类，你已经学会了如何创建自定义区域性。

应用程序的本地化是通过使用资源完成的，你可以将资源打包到文件、附属程序集或自定义存储（如数据库）中。用于本地化的类位于 `System.Resources` 命名空间中。要从其他位置（如附属程序集或资源文件）读取资源，你可以创建自定义资源读取器。

你还学习了如何本地化 WPF、ASP.NET Core 以及使用通用 Windows 平台的应用程序。

下一章提供有关 XAML 的信息。XAML 同时用于通用 Windows 平台和 WPF，因此下一章为这两种技术奠定基础。

## 第三部分

## Windows 应用程序

- 第 37 章：ADO.NET

- 第 38 章：Entity Framework Core

- 第 39 章：Windows 服务

- 第 40 章：ASP.NET Core

- 第 41 章：ASP.NET MVC

- 第 42 章：ASP.NET Web API

- 第 43 章：WebHooks 和 SignalR

- 第 44 章：Windows Communication Foundation

- 第 45 章：部署网站和服务

### 第 29 章

### 核心 XAML

#### 本章有哪些内容？

- XAML 语法

- 依赖属性

- 路由事件

- 附加属性

- 标记扩展
