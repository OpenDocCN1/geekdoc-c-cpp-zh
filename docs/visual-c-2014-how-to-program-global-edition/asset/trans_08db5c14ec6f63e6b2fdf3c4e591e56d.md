
# 1002 第 23 章 使用 async 和 await 进行异步编程

- per_page—返回结果的最大数量（多达 500 条）。如果省略此参数，默认值为 100。
- privacy_filter—1 表示仅返回公开访问的照片。

第 65 行调用了 `HttpClient.GetStringAsync` 方法，该方法使用作为字符串参数指定的 URL 从 Web 服务器上请求信息。由于此 URL 代表对 Web 服务的方法的调用，调用 `GetStringAsync` 将触发 Flickr Web 服务以执行搜索。`GetStringAsync` 返回一个 `Task<string>`，代表最终将返回搜索结果的承诺。第 68 行随后 `await` 等待 `Task` 的结果。此时，如果 `Task` 已完成，方法 `searchButton_Click` 将继续执行到第 71 行；否则，在结果返回后程序控制将返回 `searchButton_Click`。这允许执行的 GUI 线程处理其他事件，在搜索进行期间 GUI 能够保持响应状态。因此，你可以随时启动另一个搜索（在这种情况下，这会取消原始搜索）。

## 23.6.3 处理 XML 响应

当 `Task` 完成时，程序在 `searchButton_Click` 方法的第 68 行继续执行，应用程序开始处理 Web 服务器返回的 XML。图 23.5 显示了 XML 的示例。

```xml
<rsp stat="ok">
<photos page="1" pages="1" perpage="500" total="5">
<photo id="08701846820" owner="8832668@N04" secret="40fababf396"
  server="8130" title="fuchiaflowers" ispublic="1"
  isfriend="0" isfamily="0">
<photo id="0870026559" owner="8832668@N04" secret="97be93bb05"
  server="8130" title="redflowers" ispublic="1"
  isfriend="0" isfamily="0">
<photo id="0870023603" owner="8832668@N04" secret="54db053efd"
  server="8263" title="yellowflowers" ispublic="1"
  isfriend="0" isfamily="0">
</photos>
</rsp>
```

图 23.5 来自 Flickr API 的示例响应。

XML 元素和属性
XML 将数据表示为元素、属性和文本。XML 使用起始标签和结束标签来界定元素。起始标签由元素名组成，随后是属性-值对，全部封装在角括号内。例如，示例 XML 中的第 1 行

`<rsp stat="ok">`
是 `rsp` 元素的起始标签，包含整个 Web 服务的响应。该标签还包含属性 `stat`（对应为 `status="ok"`），表示 Flickr Web 请求成功。结束标签由在角括号内带有正斜杠（/）的元素名组成（例如第 19 行的 `</rsp>`），它表示“响应结束”。

## 23.6 使用 HttpClient 异步异步调用 Flickr Web 服务

元素的起始和结束标签包围着：

- 代表部分数据的文本，或
- 其他元素——例如，`rsp` 元素包含一个 `photos` 元素（第 2–12 行），`photos` 元素包含三个 `photo` 元素（第 3–11 行），代表 Web 服务找到的照片。

如果一个元素在其起始和结束标签之间不包含文本或嵌套元素，则它是空的。这种元素可以用以 `/>` 结尾的起始标签表示。例如，第 3–5 行定义了一个在标签中带有多个属性=值对的空元素。

## ClassDocument 和 LINQ to XML

命名空间 `System.Xml.Linq` 包含了使用 LINQ to XML 解析 XML 的类——我们使用了其中几个类来处理 Flickr 响应。应用程序接收 XML 结果的第 68 行（图 23.4）使用 `XDocument.Parse` 将 `await` 表达式返回的 XML 字符串转换为 `XDocument`。使用 LINQ 查询 `XDocument` 以从 XML 中提取数据。

第 71–83 行使用 LINQ 从 `XDocument` 的每个元素中收集定位 Flickr 对应位置所需的属性：

- `XDocument` 方法 `Descendants`（第 72 行）返回一个 `XElement` 对象列表，代表名称作为参数指定的元素——在本例例中，即 `photo` 元素。
- 第 73–77 行使用 `XElement` 方法 `Attribute` 提取代表当前照片元素 `id`、`title`、`secret`、`server` 和 `farm` 属性的 `XAttribute`。
- `XAttribute` 属性 `Value`（第 73–77 行）返回给定属性的值。

对于每张照片，我们创建一个 `FlickrResult` 类（位于此项目的 `FlickrResult.cs` 文件），包含：

- 一个 `Title` 属性——用照片元素的 `title` 属性初始化，用于在应用程序的 ListBox 中显示标题。
- 一个 `URL` 属性——由照片元素的 `id`、`secret`、`server` 和 `farm` 属性（`farm` 是互联网上的服务器集合）组装而成。每个 URL 的格式规定如下

```
http://flickr.com/services/api/misc.urls.html
```

我们在 `imagesListBox_SelectedChanged`（第 23.6.5 节）中使用 `FlickrResult` 的 URL，当用户在列表中选择它时下载相应的照片。

## 23.6.4 将照片绑定到 ListBox

如果有任何结果（第 87 行），第 89–90 行将结果绑定到 ListBox。你不能直接绑定文本，因此第 89 行使用 LINQ 进行确定，然后第 90 行在 ListBox 属性中显示 `Title`。

## 23.6.5 异步下载图像

`imagesListBox_SelectedChanged`（第 23.6.5 节）当用户在列表中选择它时下载相应的照片。

## 23.6.6 显示图像

应用程序接收 XML 结果的第 68 行（图 23.4）使用 `XDocument.Parse` 将 `await` 表达式返回的 XML 字符串转换为 `XDocument`。使用 LINQ 查询 `XDocument` 以从 XML 中提取数据。
