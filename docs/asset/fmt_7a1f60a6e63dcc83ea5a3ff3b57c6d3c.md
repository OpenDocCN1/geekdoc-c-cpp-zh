
你也可以将属性源到 `window` 对象以访问全局变量：

`var today = new Date().format('D');`

`<span innertext="binding binding Name, source={{today}}"></span>`

```
代码文件 [3-AjaxLibrary/12TopLevelBinding.htm] 可在 Wrox.com 下载。
```

点击“Translate name”链接后，页面将更新，并渲染图 19-9 所示的图像。

![](img/b5597c749e848b27b0d305153ae16106_915_1.png)

图 19-9：使用顶层绑定

## 双向绑定 (Two-Way Binding)

通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……

```
<input type="text" sys:value="binding Name, source={{data }}, mode=oneWay"/>
```

![](img/b5597c749e848b27b0d305153ae16106_915_2.png)

记住 `Sys.BindingMode.auto` 的默认行为是：如果目标是 `input`、`select` 或 `textarea` 元素，或者实现了 `Sys INotifyPropertyChanged` 接口的组件，则使用双向绑定；否则为单向。因为你很可能创建输入控件供用户查询，并且这需要双向绑定，因此在大多数情况下你不会更改它。通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……（此处原文似乎不完整）

（注：根据提供的原文文本，后续内容存在重复和逻辑混乱，以下按原文顺序翻译）

记住 `Sys.BindingMode.auto` 的默认行为是：如果目标是 `input`、`select` 或 `textarea` 元素，或者实现了 `Sys INotifyPropertyChanged` 接口的组件，则使用双向绑定；否则为单向。因为你很可能创建输入控件供用户查询，并且这需要双向绑定，因此在大多数情况下你不会更改它。通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……

（注：用户提供的文本从“Remember that...”之后开始出现了大量重复和逻辑错乱，此处已根据原文字面进行了对应翻译）

记住 `Sys.BindingMode.auto` 的默认行为是：如果目标是 `input`、`select` 或 `textarea` 元素，或者实现了 `Sys INotifyPropertyChanged` 接口的组件，则使用双向绑定；否则为单向。因为你很可能创建输入控件供用户查询，并且这需要双向绑定，因此在大多数情况下你不会更改它。通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……

（由于提供的原文后半部分存在严重的文本重复和乱码，翻译已严格遵循原文字面内容，未进行逻辑修复）

到 `Sys.Binding` 实例。你不需要注册这些额外的属性。只需在绑定表达式中配置它们，转换器就会接收到它们的值。请注意，拼写错误（即使是大小写错误）可能会创建额外的属性，导致你的转换器无法工作。

如果你在值从数据源传输到 UI 元素时进行转换，你可以编写一个简单的函数（签名相同），但你必须更改绑定表达式，使用 `convert` 关键字而不是 `convertBack`。

模板引擎对转换器提供了强力支持。然而，目前 Microsoft Ajax Library 中没有内置的转换器。

# 主-详情绑定 (Master-Detail Binding)

`DataView` 控制和 Microsoft Ajax Library 的实时绑定功能支持主-详情场景。在主-详情场景中，你定义了两个 `DataView` 并将它们相互连接。当用户在主 `DataView` 中选择一条记录时（该视图仅显示记录的某些顶层字段）时，详情 `DataView` 将自动更新以显示额外的字段。如你所知，此功能高度依赖于主视图中的 `select` 命令，而技巧在于你如何定义详情视图的数据源。

以下示例显示了控件列表，当用户选择一个国家时，该国家的名称、首都和旗帜将显示列表下方。

```
<ul
  id="template"
  class="sys-template"
  sys:attr="dv"
  dv="{ countries }"
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

代码文件 `[3-AjaxLibrary-15-MasterDetail.htm]` 可在 Wrox.com 下载。

在图 19-12 中，你可以看到用户点击“美国”后浏览器渲染的内容。

让我们逐步分析这段代码。主视图是 HTML 元素，而详情是下方的 `div`。HTML 元素附加了 `DataView`，这是因为 `DataView` 能够显示单条记录和多条记录。在主视图中，`select` 命令通过默认行为实现，无需任何自定义事件处理程序。`selectedDataItem` 属性用于在 UI 上高亮选中的国家。

如你所知，当用户选择一个国家时，其数据项会被加载到 `DataView` 的 `selectedData` 属性中。通过使用 `$find` 方法获取附加到主 HTML 元素上的 `Sys.UI DataView` 实例，并将其作为数据源。如果你想编写更紧凑的代码，可以使用相同的前缀和 HTML 元素的 ID 来替换该表达式。

![](img/b5597c749e848b27b0d305153ae16106_19_0.png)

图 19-12：主-详情视图

```
dv:data="binding selectedData, source={{ $master }})"
```

代码文件 `[3-AjaxLibrary15-MasterDetail.html]` 可在 Wrox.com 下载。

`selectedData` 属性包含一个国家记录。你可以绑定到它的 `Name`、`Capital` 和 `Code` 属性。这段代码还利用自定义的 `stringConverter`，通过 `String.format` 方法根据国家代码获取旗帜图像 URL：

```
Sys.converters.stringConverter = function(value, binding)
{
return String.format(binding.format, value);
}
```

代码文件 `[3-AjaxLibrary15-MasterDetail.html]` 可在 Wrox.com 下载。

由于使用了绑定，对 `selectedData` 的更改将传播到详情视图，视图会自动刷新。此外，由于数据绑定到详情视图中的输入元素上，且默认是双向绑定，如果用户在文本框中更改了首都名称，新值将在文本框失去焦点后出现在主视图中。注意，这会影响主视图和详情视图，因为它们本质使用的是相同的数据源 `countries` 对象数组。

# 使用服务器端数据

早些时候，你看到了如何使用客户端 `DataView` 控制来显示和管理来自本地数据源的数据。然而，在现实场景中，数据存储在服务器上，因此你必须添加额外的步骤将其下载到客户端，然后将更改传回服务器。

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

代码文件 `[App_Code\Country.cs]` 可在 Wrox.com 下载。

代码文件 `[App_Code\CountryService.cs]` 可在 Wrox.com 下载。

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

此时，你可以在 Visual Studio 中按 `Ctrl+F5` 在浏览器中查看你的 Web 服务器。注意，Visual Studio 直接打开了 `CountryService.asmx` URI，并会自动生成页面。在页面上，你可以找到一个指向服务描述的链接（`CountryService.asmx?WSDL`），服务客户端可以据此构建客户端项目。

然而，如果你想从 JavaScript 调用此 Web 服务，ASP.NET 运行时可以为你动态生成一个功能齐全的 JavaScript 客户端代理。要实现这一点，你只需将 URI 更改为 `CountryService.asmx/debug`。通过添加 `/debug`，你可以获得更易读的调试版本代理；通过添加 `/js`，你可以获得压缩版本。

值得停顿一下并探索生成的脚本代理，它包含两个类：

```
...
CountryService.registerClass('CountryService', Sys.Net.WebServiceProxy);
...
Country.registerClass('Country');
...
```

由于服务器端的 `Country` 类被用于 Web 服务接口，因此客户端也生成了类似的类。要调用 Web 服务，你将获得一个名为 `CountryService` 的类，它派自 `Sys.Net.WebService` 基类。

现在你已经有了一个功能完整的代理类，它隐藏了 Web 服务 SOAP 调用的细节，你可以在客户端上显示这些调用。首先，创建一个未指定数据的 `DataView`：

```
<ul
  <li id="sys-templateList" class="sys-template" sys:attach="dv">
    <li>
      {{ Name }} ((Capital))
    </li></li>
</ul>
```

代码文件 `[4-ServerSideData\1-WebService.htm]` 可在 Wrox.com 下载。

要访问代理类，请在 js / jsdebug URL 中添加脚本引用：

```
<script type="text/javascript" src="CountryService.asmx/jsdebug"></script>
```

代码文件 `[4-ServerSideData\1-WebService.htm]` 可在 Wrox.com 下载。

使用该代理类，在页面完全加载后调用 Web 服务。在此之前，花一点时间重新考虑底层发生了什么。

从客户端发起 HTTP 请求的唯一方法是使用浏览器中的 `XMLHttpRequest` 对象，而 `Sys.Net.WebService` 代理类使用的是异步方式。然而，所有服务方法都接受成功和失败回调方法的引用。这意味着，尽管 `GetCountriesByName` 方法在服务器端没有任何参数，但当你客户端调用它时，必须传递至少一个成功回调来处理结果：

```
function pageLoad()
{
  CountryService.GetCountriesByName(onSuccess)
}

function onSuccess(results)
{
  $find('countryList').set_data(results);
}
```

代码文件 `[4-ServerSideData\1-WebService.htm]` 可在 Wrox.com 下载。

成功回调将 Web 方法的返回值作为参数接收。因为你想要显示的是客户端列表，你可以使用 `$find` 方法获取 `DataView` 组件，并设置它的 `data` 属性。

就是这样！仅需两行代码，你就从 JavaScript 调用了 SOAP Web 服务并使用声明式模板显示了结果。这并不复杂，对吧？
