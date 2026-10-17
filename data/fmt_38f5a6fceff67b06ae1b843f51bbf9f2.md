
```csharp
// 用于搜索的 Flickr Web 服务 URL

imagesListBox.DataSource = null; // 移除之前的数据源

imagesListBox.Items.Clear(); // 清空 imagesListBox
pictureBox.Image = null; // 清空 pictureBox
imagesListBox.Items.Add("Loading..."); // 显示 Loading...

// 调用 Flickr Web 服务根据用户的标签搜索 Flickr

flickrTask = flickrClient.GetStringAsync(flickURL);

// 使用 XDocument 和 LINQ 等待 amassTask 结果

XDocument XDocument = XDocument.Parse(await flickrTask);

// 收集所有照片的信息

var flickrPhotos = from photo in FlickrXML.Descendants("photo")
                  let id = photo.Attribute("id").Value
                  let title = photo.Attribute("title").Value
                  let secret = photo.Attribute("secret").Value
                  let server = photo.Attribute("server").Value
                  let farm = photo.Attribute("farm").Value
                  select new FlickrResult
                  {
                      Title = title,
                      URL = $"https://{farm}.staticflickr.com/{server}/{id}.jpg"
                  };

imagesListBox.Items.Clear(); // 清空 imagesListBox

// 只有在找到结果时设置 List 属性

if (flickrPhotos.Any())
{
    imagesListBox.DataSource = flickrPhotos.ToList();
    imagesListBox.DisplayMember = "Title";
}
else // 未找到匹配项
{
    imagesListBox.Items.Add("No matches");
}

// 显示选中的图片

private async void imagesListBox_SelectedIndexChanged(object sender, EventArgs e)
{
    if (imagesListBox.SelectedItem != null)
    {
        string selectedURL = (FlickrResult)imagesListBox.SelectedItem.URL;
        // 使用 HttpClient 获取图像字节
        byte[] imageBytes = await flickrClient.GetByteArrayAsync(selectedURL);
        // 在 PictureBox 中显示图像
        using (MemoryStream memoryStream = new MemoryStream(imageBytes))
        {
            pictureBox.Image = Image.FromStream(memoryStream);
        }
    }
}
```

图 23.4 使用 `HttpClient` 类异步调用 Web 服务。（3 部分中的第二部分）

# 第 23 章 使用 async 和 await 进行异步编程

- `per_page`—返回结果的最大数量（多达 500 条）。如果省略此参数，默认值为 100。
- `privacy_filter`—1 表示仅返回公开访问的照片。

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

## 23.6 使用 HttpClient 异步调用 Flickr Web 服务

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

# 第 23 章 使用 async 和 await 进行异步编程

```csharp
// 检查值是否为质数
// 并将所有倍数标记为非质数
public bool IsPrime(int value)
{
    // 如果 value 是质数，将其所有倍数
    // 标记为非质数并返回 true
    if (primes[value]) {
        // 将 value 的所有倍数标记为非质数
        for (var i = value; i < primes.Length; i += value) {
            primes[i] = false; // i 不是质数
        }
        return true;
    } else {
        return false;
    }
}

// 如果点击取消按钮，停止显示质数
private void cancelButton_Click(object sender, EventArgs e)
{
    Cancelled = true;
    getPrimesButton.Enabled = true; // 启用 getPrimesButton
    cancelButton.Enabled = false; // 禁用 cancelButton
}
```

![](img/57baed2319be0bb1b5f98674846f2711_1006_0.png)

**图 23.6** 显示异步任务的进度和中间结果。（3 部分中的 3）

## 埃拉托斯特尼筛法

第 14 行解码了所有质数数组，我们使用该数组配合埃拉托斯特尼筛法（在练习题 8.27 中描述）来寻找小于最大值的所有质数。埃拉托斯特尼筛法接收一个整数列表，从第一个质数开始，过滤掉所有质数的倍数。它移动到下一个未被过滤的数字（即下一个质数），消除它所有的倍数。该过程一直持续到所有质数都被过滤掉。在算法上，我们从 bool 数组的元素 2 开始（忽略元素 0 和 1），并将所有索引为 2 的倍数索引处的元素设置为 false，以表示它们可被 2 整除且不是质数。然后我们移动到下一个元素，检查它是否为 true，并将其所有倍数设置为 false，以表示它们可被当前索引整除。当算法完成时，所有包含 true 的索引都是质数，因为它们没有因数。本示例中的埃拉托斯特尼筛法通过方法 `FindPrimes`（第 48–77 行）和 `IsPrime`（第 81–99 行）实现。`IsPrime` 确定一个特定数字是否为质数，它立即消除该数字的所有倍数。按照目前的实现，本示例中的算法本质上是效率的。练习 23 讨论了为什么以及如何修改质数逻辑。

## 构造函数

`FindPrimesForm` 类的构造函数（第 16–21 行）将 `ProgressBar.Minimum` 属性设置为 2——第一个质数，并将 `label.Text` 设置为格式化为整数的 0。在格式指定符 `P0` 中，`P` 表示该值应格式化为百分比，`0` 表示小数位数。

## async 方法 getPrimesButton_Click

当用户在 `label.TextBox` 中输入一个数字并点击“获取质数”按钮时，方法 `getPrimesButton_Click`（第 24–45 行）会调用此声明为 `async` 的方法，因为它将等待 `FindPrimes` 方法的结果。第 27 行获取用户输入的最大值，第 30 行创建一个具有指定数量元素的 bool 数组并用 true 值填充。索引非质数的元素最终会被设置为 false。`Enumerable` 静态方法 `Repeat` 创建一个长度等于第一个参数值的元素列表。然后我们对结果调用 `ToArray` 将列表转换为数组表示。`Repeat` 是一个泛型方法——33–40 行将 `Canceled` 属性设置为 false 并重置 GUI 以准备确定质数。第 39–40 行将 `ProgressBar.Minimum` 设置为值并将 `Maximum` 设置为用户输入的新值。当我们从 2 到最大测试每个数字以判断它是否为质数时，我们将 `ProgressBar` 的属性设置为当前正在测试的数字。随着该数字的增加，`ProgressBar` 将按比例填充颜色，以显示异步任务的进度。

第 43 行调用 async 方法 `FindPrimes` 以开始寻找质数的过程。完成后，`FindPrimes` 返回小于用户输入的最大值的质数列表，应用程序在第 44 行显示该列表。

## async 方法 FindPrimes

`async` 方法 `FindPrimes` 实现了埃拉托斯特尼筛法，发现找到的质数并更新 `ProgressBar` 和完成百分比。第 50 行最初将 `primeCount` 设置为 0，表示尚未找到任何质数。第 53–66 行遍历从 2 到（但不包含）用户输入的最大值之间的值。对于每个值，第 56 行启动一个 async `Task` 来确定该值是否为质数，并等待 `Task` 的结果。当该结果返回时，如果是 true，第 58 行增加 `primeCount` 以表示找到了质数，第 59 行将数字的字符串表示分配给 `primeTextBox` 的文本——从而显示其中一个中间结果。无论某个值是否为质数，第 62–64 行都会计算到目前已完成的循环百分比并显示，第 65 行更新 `progressBar` 的值。

在 `FindPrimes` 执行期间的任何时候，用户都可以点击“取消”按钮，此时 `Cancel` 将设置为 true，循环将提前终止。如果发生这种情况，第 69–72 行将在 `primesTextBox` 中显示“已”。

## 方法 IsPrime

方法 `IsPrime`（第 81–99 行）被 async `FindPrimes` 调用以执行埃拉托斯特尼筛法的部分工作。`IsPrime` 通过检查数组 `primes` 中对应的元素（第 85 行）来测试其值是否为质数。如果 `value` 是质数，第 88–91 行将索引为 `value` 倍数的质数数组元素设置为 false，第 93 行返回 true 表示 `value` 是质数；否则，方法返回 false。

## 方法 cancelButton_Click

当用户点击“取消”按钮时，`cancelButton_Click`（第 102–107 行）将属性 `Cancel` 设置为 true，然后启用“获取质数”按钮并禁用“取消”按钮。当下一次评估第 53 行的条件时，`FindPrimes` 方法中的循环将终止。

## 23.8 总结

在本章中，你学习了如何使用 `async` 修饰符、`await` 操作符和 `wait`。

# 第 23 章 使用 async 和 await 进行异步编程

- 决定是将控制权返回给异步方法的调用者还是继续执行该异步方法，以及在异步任务完成后继续执行异步方法的执行机制，完全由编译器编写的代码处理。

## 第 23.2 节 async, await 与线程

- `async` 和 `await` 机制不会创建新线程。你调用来启动异步任务或 `await` 等待结果的方法负责创建用于执行异步任务的任何线程（例如 `Task.Run`）。

## 第 23.3.1 节 异步执行任务

- 如果在 GUI 应用中执行耗时计算，GUI 将冻结直到计算完成，且用户将无法与应用程序进行交互。
