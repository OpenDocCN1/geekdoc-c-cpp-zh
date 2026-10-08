

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

代码文件 [4-ServerSideData\1-WebService.htm] 可在 Wrox.com 下载。

要访问代理类，请在 js / jsdebug URL 中添加脚本引用：

```
<script type="text/javascript" src="CountryService.asmx/jsdebug"></script>
```

代码文件 [4-ServerSideData\1-WebService.htm] 可在 Wrox.com 下载。

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

代码文件 [4-ServerSideData\1-WebService.htm] 可在 Wrox.com 下载。

成功回调将 Web 方法的返回值作为参数接收。因为你想要显示的是客户端列表，你可以使用 `$find` 方法获取 `DataView` 组件，并设置它的 `data` 属性。

就是这样！仅需两行代码，你就从 JavaScript 调用了 SOAP Web 服务并使用声明式模板显示了结果。这并不复杂，对吧？

确实如此。尽管如此，这是一个经常使用的场景，每一行代码都至关重要，因此 `DataView` 接口对其提供了直接支持。你可以移除 `<script>` 标签、Web 服务和成功回调，直接在 `DataView` 上配置 Web 服务 URI。

```
<<ul>
  <ul class="sys-template"
    sys:attach="dv"
    dv:autofetch="true"
    dv:dataProvider="../Services/CountryService.asmx"
    dv:fetchoperation="GetCountriesByName">
  <li>
    {{ Name }} ((( Capital )))
  </li>
</</ul>
</ul>
```

代码文件 [4-ServerSideData2-DataFromService.htm] 可在 Wrox.com 下载。

`DataView` 类的 `dataProvider` 可以指向 JSON Web 服务 URI，或者 `Sys.Net.WebService` 对象的实例，或任何实现 `Sys.DataProvider` 接口的类。在 `fetchoperation` 属性中，你定义可以调用的方法名称。通过将 `autofetch` 属性设置为 `true`，你可以确保无需手动更新 `DataView`。它会在加载时、或者当 `dataProvider` 或 `fetchoperation` 更改时，立即从源检索数据。

如果你想调用一个期望参数的方法，还必须设置 `fetchParameters` 属性：

```
<<ul>
  <ul class="sys-template"
    sys:attach="dv"
    dv:autofetch="true"
    dv:dataProvider="../Services/CountryService.asmx"
    dv:fetchoperation="GetCountries"({ orderby: 'Capital', asc: false })"
  <li>
    {{ Name }} ((( Capital )))
  </li>
</</ul>
</ul>
```

- 排序依据：Capital
- 希腊（雅典）
- 巴西（巴西利亚）
- 德国（柏林）
- 匈牙利（布达佩斯）
- 澳大利亚（堪培）
- 芬兰（赫尔辛基）
- 英国（伦敦）
- 西班牙（马德里）
- 瑞典（斯德哥尔摩）
- 奥地利（维也纳）
- 美国（华盛顿特区）
- 克罗地亚（萨格勒布）

图 19-13：用户可以选择记录的顺序

代码文件 [4-ServerSideData3-DataFromServiceWithParameters.htm] 可在 Wrox.com 下载。

当然，你甚至可以让用户选择国家的排序，如图 19-13 所示。

首先，提供一个下拉列表框，并显示可选排序：

```
<select onchange="onSubmit(this.value)">
  <option value="Name">Name</option>
  <option value="Capital">Capital</option>
</select>
```

![](img/b5597c749e848b27b0d305153ae16106_924_0.png)

代码文件 [4-ServerSideData\4-DataServiceWithParametersBinding1.btm] 可在 Wrox.com 下载。

当用户从列表中选择新值时，会触发 **onchange** 事件。在这里你可以使用该事件调用 `fetchParameters()` 并从服务器重新获取数据：

```javascript
function sort(orderby)
{
  var dv = $find('countryList');
  dv.fetchParameters().orderby = orderby;
  dv.fetchData();
}
```

![](img/b5597c749e848b27b0d305153ae16106_924_1.png)

代码文件 [4-ServerSideData\4-DataServiceWithParametersBinding1.btm] 可在 Wrox.com 下载。

如你所见，调用 Web 服务并使用模板在客户端显示结果是非常好的。这涵盖了大部分服务端数据场景，在这些场景中，通常将修改后的数据上传到服务器。

# 在服务器上更新数据

如果你想实现读写场景，必须将所有数据管理委托给新的 `Sys.DataContext` 类。该类封装了从服务器获取数据、在客户端进行更改以及将数据修改回服务器的所有内容。`DataContext` 实现了 `IDataProvider` 接口，这意味着你可以直接将 `DataContext` 实例作为 `DataView` 的数据源：

```
<ul
class="sys-template"
sys:attach="dv"
dv:autofetch="true"
dv:dataProvider={executionContext}
dv:fetchoperation="GetCountriesByName">
<li>
  {{ Name }} {{ Capital }}
</li>
</</ul>
```

![](img/b5597c749e848b27b0d305153ae16106_924_2.png)

代码文件 [4-ServerSideData6-DataContext.btm] 可在 Wrox.com 下载。

如你所见，`dataProvider` 属性不再直接指向 Web 服务。相反，它被一个在页面加载时创建的 `DataContext` 实例封装。（稍后会介绍。）

你可能会注意到，尽管服务 URI 被 `DataContext` 封装，但 Web 方法仍然定义在 ViewData 中。如果你觉得这有点困惑，你并不孤单，这在后续预览或 RTM 版本中可能会发生。

唯一的是 `DataContext` 实例存在于 `MicrosoftAjax.js` 文件中，因为它依赖许多其他文件，最好使用新的脚本加载器在页面上加载所需文件：

```
<script src="Start.debug.js" type="javascript"></script>
<script type="javascript">
  var dataContext;
  Sys.require([Sys.components.DataView, Sys.components.dbContext]);
  Sys.onReady(function() {
    dataContext = Sys.create.DataContext({
      serviceURI: "../Services/CountryService.asmx"
    });
  });
</script>
```

> 代码文件 [4-ServerSideData6-DataContext.htm] 可在 Wrox.com 下载。

在所需的脚本下载并初始化后，创建一个新的 `Sys.Data.DataContext` 实例，并使用 `serviceURI` 属性设置 Web URI。

如果你测试目前的代码，浏览器中不会有变化。数据被下载并显示在页面上；目前还没有特别的。然而，如果你更改 ViewData 为用户提供输入控件，就可以利用 `DataContext` 类的优势。

因此，首先重写 ViewData 模板显示文本框，并使用默认的双向绑定来通知数据源（在此例为 `DataContext`）数据已被修改：

```
<div
  id="countryList"
  class="sys-template"
  sys:attach="dv"
  dv:autofetch="true"
  dv:dataprovider={dataContext}
  fetchoperation="GetCountriesByName">
  <div>
    Name:
    <input type="text" sys:value="{ binding Name }" />
    Capital:
    <input type="text" sys:value="{ binding Capital }" />
  </div>
</div>
```

> 代码文件 [4-ServerSideData7-DataContextReadWrite.htm] 可在 Wrox.com 下载。

