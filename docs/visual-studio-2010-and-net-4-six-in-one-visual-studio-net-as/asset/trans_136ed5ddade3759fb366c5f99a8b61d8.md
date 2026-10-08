
到 `Sys.Binding` 实例。你不需要注册这些额外的属性。只需在绑定表达式中配置它们，转换器就会接收到它们的值。请注意，拼写错误（即使是大小写错误）可能会创建额外的属性，导致你的转换器无法工作。

如果你在值从数据源传输到 UI 元素时进行转换，你可以编写一个简单的函数（签名相同），但你必须更改绑定表达式，使用 `convert` 关键字而不是 `convertBack`。

模板引擎对转换器提供了强力支持。然而，目前 Microsoft Ajax Library 中没有内置的转换器。

# 主-详情绑定 (Master-Detail Binding)

DataView 控制和 Microsoft Ajax Library 的实时绑定功能支持主-详情场景。在主-详情场景中，你定义了两个 DataView并将它们相互连接。当用户在主 DataView 中选择一条记录时（该视图仅显示记录的某些顶层字段）时，详情 DataView 将自动更新以显示额外的字段。如你所知，此功能高度依赖于主视图中的 `select` 命令，而技巧在于你如何定义详情视图的数据源。

以下示例显示了控件列表，当用户选择一个国家时，该国家的名称、首都和旗帜将显示列表下方。

```
<ul
  id="template"
  class="sys-template"
  sys:attr="dv"
  dv="{ countries }}"
  dv:selecteditemclass="selected">
  <li sys:command="Select" style="cursor: pointer;">
    {{ Name }}
    <span>{{ binding Capital }}</span>
  </li>
</ul>
<div
  class="sys-template"
  sys:attr="dv"
  dv="{ binding selectedData,
    source={ { $find('master') } }">
  <img
    sys:src="{ binding Code,
    convert=stringConverter,
    format=../images/flag(0).gif"
    style="float: left; margin-right: 10px;" />
  <h2 id="txtCapital">Capital:</h2>
  <label for="txtCapital">Capital:</label>
  <input type="text" id="txtCapital"
    sys:value="{ binding Capital }" />
</div>
```

![](img/b5597c749e848b27b0d305153ae16106_918_0.png)

代码文件 [3-AjaxLibrary-15-MasterDetail.htm] 可在 Wrox.com 下载。

在图 19-12 中，你可以看到用户点击“美国”后浏览器渲染的内容。

让我们逐步分析这段代码。主视图是 HTML 元素，而详情是下方的 `div`。HTML 元素附加了 DataView，这是因为 DataView 能够显示单条记录和多条记录。在主视图中，`select` 命令通过默认行为实现，无需任何自定义事件处理程序。`selectedDataItem` 属性用于在 UI 上高亮选中的国家。

如你所知，当用户选择一个国家时，其数据项会被加载到 DataView 的 `selectedData` 属性中。通过使用 `$find` 方法获取附加到主 HTML 元素上的 `Sys.UI DataView` 实例，并将其作为数据源。如果你想编写更紧凑的代码，可以使用相同的前缀和 HTML 元素的 ID 来替换该表达式。

![](img/b5597c749e848b27b0d305153ae16106_19_0.png)

图 19-12：主-详情视图

```
dv:data="binding selectedData, source={{ $master }})"
```

代码文件 [3-AjaxLibrary15-MasterDetail.html] 可在 Wrox.com 下载。

`selectedData` 属性包含一个国家记录。你可以绑定到它的 `Name`、`Capital` 和 `Code` 属性。这段代码还利用自定义的 `stringConverter`，通过 `String.format` 方法根据国家代码获取旗帜图像 URL：

```
Sys.converters.stringConverter = function(value, binding)
{
return String.format(binding.format, value);
}
```

代码文件 [3-AjaxLibrary15-MasterDetail.html] 可在 Wrox.com 下载。

由于使用了绑定，对 `selectedData` 的更改将传播到详情视图，视图会自动刷新。此外，由于数据绑定到详情视图中的输入元素上，且默认是双向绑定，如果用户在文本框中更改了首都名称，新值将在文本框失去焦点后出现在主视图中。注意，这会影响主视图和详情视图，因为它们本质使用的是相同的数据源 `countries` 对象数组。

# 使用服务器端数据

早些时候，你看到了如何使用客户端 DataView 控制来显示和管理来自本地数据源的数据。然而，在现实场景中，数据存储在服务器上，因此你必须添加额外的步骤将其下载到客户端，然后将更改传回服务器。

Microsoft Ajax Library 完全支持与服务器上的 Web 服务、启用 Ajax 的 WCF 服务以及 ADO.NET Data Services 交互。

要将国家示例迁移到服务器，首先在 C# 中创建一个 `Country` 类来封装所有与国家相关的数据：

```csharp
public class Country
{
    public string Name;
    public string Code;
    public string Capital;

    public Country()
{
}

    public Country(string name, string code, string capital)
    {
        this.Name = name;
        this.Code = code;
        this.Capital = capital;
    }
}
```

![](img/b5597c749e848b27b0d305153ae16106_920_0.png)

然后，创建一个名为 `CountryService` 的新 ASMX Web 服务，带有一个私静态 `countries`，并用国家数据初始化它：

```csharp
[WebServiceNamespace = "http://example.com/Samples/"]
[System.Web.Services.WebService]
public class CountryService : System.Web.Services.WebService
{
    private static List<Country> countries = new List<Country>
    {
        new Country("Austria", "at", "Vienna"),
        new Country("Australia", "au", "Canberra"),
        new Country("Brasil", "br", "Brasilia");
        // 在此处添加更多国家...
    }
}
```

![](img/b5597c749e848b27b0d305153ae16106_920_1.png)

代码文件 [App_Code\Country.cs] 可在 Wrox.com 下载。

代码文件 [App_Code\CountryService.cs] 可在 Wrox.com 下载。

你可能注意到 `ScriptService` 特性被添加到服务类中。如果你想从 JavaScript 访问 Web 服务，此属性是必须。最后，添加你想发布的 Web 服务方法。

```csharp
[WebMethod]
public Country[] GetNames()
{
    return this.GetCountries(true);
}
```

```csharp
[WebMethod]
public Country[] GetCountries( string orderby, bool asc )
{
    Func<Country, string> keySelector;
    switch ( orderby)
    {
        case "Name":
            keySelector = new Func<Country, string>( c => c.Name);
            break;
        case "Code":
            keySelector = new Func<Country, string>( c => c.Code);
            break;
        case "Capital":
            keySelector = new Func<Country, string>( c => c.Capital);
            break;
        default:
            keySelector = new Func<Country, string>( c => c.Name);
    }
    IEnumerable<Country> result = asc ?
        CountryService.countries.OrderBy(keySelector) :
        CountryService.countries.OrderByDescending(keySelector);
    return result.ToArray();
}
```

![](img/b5597c749e848b27b0d305153ae16106_920_2.png)

此时，你可以在 Visual Studio 中按 Ctrl+F5 在浏览器中查看你的 Web 服务器。注意，Visual Studio 直接打开了 `CountryService.asmx` URI，并会自动生成页面。在页面上，你可以找到一个指向服务描述的链接（CountryService.asmx?WSDL），服务客户端可以据此构建客户端项目。

然而，如果你想从 JavaScript 调用此 Web 服务，ASP.NET 运行时可以为你动态生成一个功能齐全的 JavaScript 客户端代理。要实现这一点，你只需将 URI 更改为 `CountryService.asmx/debug`。通过添加 `/debug`，你可以获得更易读的调试版本代理；通过添加 `/js`，你可以获得压缩版本。

值得停顿一下并探索生成的脚本代理，它包含两个类：

```
...
CountryService.registerClass('CountryService', Sys.Net.WebServiceProxy);
...
Country.registerClass('Country');
...
```

