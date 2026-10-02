
| Strict | 当设置为 `True` 时，使用 Visual Basic Strict 模式编译主页。默认设置为 `False`。 |

| WarningLevel | 指定想要停止页面编译的编译器警告级别。可能的值从 0 到 4。 |

以下是如何使用 `@Master` 指令的示例：

```
<@Master Language="C#" AutoEventWire="true"
CodeBehind="ProfessionalASNet45-Layout.cs"
Inherits="ASPNet45_0CS.ProfessionalASNet45_Layout" %>
```

# @Control

`@Control` 指令与你在构建 ASP.NET 用户控件时使用的 `@Page` 指令类似。`@Control` 指令允许你定义要被用户控件继承的属性。这些值在页面解析和编译时会被分配给用户控件。可用的属性少于 `@Page` 指令，但它们允许你在构建用户控件时进行所需的修改。表 3-6 详细列出了这些可用属性。

## 表 3-6

| 属性 | 描述 |
| :--- | :--- |
| AutoEventWire | 设置为 `True` 时，指定是否自动绑定用户控件的事件。默认设置为 `True`。 |
| ClassName | 指定在页面编译时绑定到用户控件的类名。 |
| ClientIDMode | 指定页面在为页面上的服务器控件生成 `ClientID` 值时应使用的算法。默认值是 `AutoID`（ASP.NET 4 之前 ASP.NET 页面使用的模式）。 |
| CodeBehind | 引用与主页关联的代码后台文件。在 ASP.NET 2.0 或更高版本中，应配合 `Inherits` 使用 `CodeFile`。 |
| CodeFile | 引用与用户控件关联的代码后台文件。 |
| CodeFileClass | 指定与代码后台类使用的基类类型名称，该类型由 `CodeFile` 属性使用。 |
| CompilationMode | 指定是否应该编译控件。 |
| CompilerOptions | 表示用户控件编译选项的编译器字符串。 |
| Debug | 设置为 `True` 时，使用调试符号编译用户控件。 |
| Description | 提供用户控件的文本描述。ASP.NET 解析器会忽略此属性及其分配的值。 |
| EnableTheming | 设置为 `True` 时，启用用户控件使用主题。此属性的默认设认为 `True`。 |
| EnableState | 设置为 `True` 时，为用户控件维护视图状态（`ViewState`）。默认值是 `True`。 |
| Explicit | 设置为 `True` 时，启用 Visual Basic 显式声明。默认设置为 `False`。 |
| Inherits | 指定用户控件继承的 `CodeBehind` 类。 |
| Language | 定义用于任何联渲染和脚本块的语言。 |
| LinePragma | 布尔值，指定是否在生成的程序集中中使用行处理指令（line pragmas）。 |
| Src | 指向用于渲染的用户控件代码后台的类的源文件。 |
| Strict | 设置为 `True` 时，使用 Visual Basic Strict 模式编译控件。默认设置为 `False`。 |
| WarningLevel | 指定停止编译用户控件的编译器警告级别。可能的值为 0 到 4。 |

`@Control` 指令旨在用于 ASP.NET 用户控件。以下是使用该指令的示例：

```
<@ Control Language="C#" AutoEventWireup="true"
CodeBehind="RegistrationUserControl.ascx.cs"
Inherits="ProfessionalASPnet45_03CS.RegistrationUserControl">
```

# @Import

`@Import` 允许你指定要导入到 ASP.NET 页面或用户控件的命名空间。通过导入，命名空间的所有类和接口对页面或用户控件可用。该指令仅支持一个属性：`Namespace`。

`Namespace` 属性接受一个字符串值，指定要导入的命名空间。`@Import` 指令不能包含多个属性/值对。因此，你必须像下面的示例所示将多个命名空间放在多行：

```
<@Import Namespace="System.Data">
@Import Namespace="System.Data.Client">
```

你的应用程序引用了多个程序集。你可以通过查看 `C\Windows\.NET\Framework\v4.0.xxxxx\Config` 下的 `web.config` 文件来查找导入的程序集列表。你可以从 `<compilation>` 元素的 `<assemblies>` 子元素找到这些被引用的程序集列表。`web.config` 文件中的设置如下：

```
<assemblies>
  <add assembly="Microsoft.VisualStudio.Web.ProjectInspector, Version=1.0.0.0, PublicKeyToken=b0f5f7f1d50a3a" />
  <add assembly="mscorlib" />
  <add assembly="Microsoft.CSharp, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.Configuration, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.Web.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.Drawing, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.EnterpriseServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.WebModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
  <add assembly="System.WebModel.Activation, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
  <add assembly="System.WebModel.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
  <add assembly="System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
  <add assembly="System.ServiceModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
  <add assembly="System.WorkflowServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
  <add assembly="System.Core, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
</assemblies>
<add assembly="System.Web.Extensions, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
<add assembly="System.Data.DataSetExtensions, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
<add assembly="System.Xml.Linq, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a55c6934e089" />
<add assembly="System.ComponentModel.DataAnnotations, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
<add assembly="System.Web.DynamicData, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
<add assembly="System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
<add assembly="System.*" />
<add assembly="System.Web.Deployment, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
<add assembly="System.Web.Deployment, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf85ad3645" />
</assembly>

由于由于 web config 文件中的这些引用，这些程序集不需要在 References 文件夹中引用，除非你使用的是 ASP.NET I/O.1。你可以从此列表中添加这些程序集。如果你有一个服务器上每个应用程序都持续引用的自定义程序集，只需在这些程序集旁边添加你的自定义程序集的类似引用。你也可以通过应用程序特定的 `web.config` 文件执行此任务。

> 注意：尽管你可以编辑 `C:\Windows\Microsoft\.NET Framework\vX.X.XXXX\.config` 文件夹中的 `.config` 文件，但强烈建议永久保持这些文件不变。此外，如果你将应用程序部署到 Web ，任何针对机器的更改必须在每台服务器上进行。

即使引用了程序集，你仍必须将这些程序集的命名空间导入到页面中。同一个 `web.config` 文件包含自动导入到应用程序每个页面的命名空间列表。这是通过 `<pages>` 元素的 `<namespaces>` 子元素指定的。

```
<namespaces>
<add namespace="System" />
<add namespace="System.Collections" />
<add namespace="System.Collections.Generic" />
<add namespace="System.Collections.Specialized" />
<add namespace="System.ComponentModel.DataAnnotations" />
<add namespace="System.Configuration" />
<add namespace="System.Linq" />
<add namespace="System.Text" />
<add namespace="System.Text.RegularExpressions" />
<add namespace="System.Web" />
<add namespace="System.Web.Caching" />
<add namespace="System.Web.DynamicData" />
<add namespace="System.Web.SessionState" />
<add namespace="System.Web.Security" />
<add namespace="System.Web.Profile" />
<add namespace="System.Web.UI" />
<add namespace="System.Web.UI.Controls" />
<add namespace="System.Web.UI.WebParts" />
<add namespace="System.Web.UI.HtmlControls" />
<add namespace="System.Xml.Linq" />
</namespaces>
```

从此 XML 列表中，你可以看到有很多命名空间被导入到你的每一个 ASP.NET 页面中。同样，你可以自由地在根 `web.config` 文件中修改这些选择，甚至从应用程序的 `web.config` 文件中选择命名空间。

例如，你可以在应用程序的 `web.config` 文件中导入命名空间，以便该命名空间在所有它的每个页面上都可用。

```xml
<?xml version="1.0"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5" />
    <httpRuntime targetFramework="4.5" />
    <pages>
      <namespaces>
        <add namespace="Widgets" />
      </namespaces>
    </pages>
  </system.web>
</configuration>
```

请记住，将命名空间导入到 ASP.NET 页面或用户控件中，让你有机会在无需完整标识类名的情况下使用这些类。例如，通过向 ASP.NET 页面导入 `System.IO` 命名空间，你可以通过单个类名引用该命名空间内的类（将 `System.IO.Directory` 简化为 `Directory`）。

## @Implements

`@Implements` 指令允许 ASP.NET 页面实现指定的 .NET Framework 接口。该指令仅支持一个属性：`Interface`。

`Interface` 属性直接指定 .NET Framework 接口。当 ASP.NET 页面或用户控件实现一个接口时，它可以访问该接口的所有事件、方法和属性。

下面是 `@Implements` 指令的示例：

```cs
@Implements Interface="System.Web.UI.IValidator" />
```

## @Register

`@Register` 指令将别名与命名空间和类名关联，以便在自定义服务器控制语法中表示。当你将用户控件拖放到任何一个 `.aspx` 页面上时，就可以看到 `@Register` 指令。将用户控件拖动到 `.aspx` 页面会使 Visual Studio 2012 在页面顶部创建一个 `@Register` 指令。这在页面上注册了你的用户控件，以便通过特定名称在 `.aspx` 页面上访问该控件。

`@Register` 指令支持五个属性，如表 3-7 所示。

### 表 3-7

| ATTRIBUTE | DESCRIPTION |
| :--- | :--- |
| Assembly | 你与 `TagPrefix` 关联的程序集 |
| Namespace | 与 `TagPrefix` 关联的命名空间 |
| Src | 用户控件的位置 |
| TagName | 与类名关联的别名 |
| TagPrefix | 与命名空间关联的别名 |

下面是使用 `@Register` 指令将用户控件导入到 ASP.NET 页面的示例：
```cs
@Register TagPrefix="MyTag" Namespace="MyNamespace" Assembly="MyAssembly" %>
```
