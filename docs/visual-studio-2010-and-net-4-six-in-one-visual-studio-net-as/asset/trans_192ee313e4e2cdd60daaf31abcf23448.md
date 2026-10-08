

属性窗口中的图像类别，如图 16-5 所示。

## Image URL 渲染

默认情况下，Chart 控件的 `RenderType` 属性设置为 `ImageTag`（如图 16-5 所示）。`ImageLocation` 和 `ImageStorageMode` 属性决定了在 HTML 页面显示图像时如何存储和检索图像。`ImageStorageMode` 默认设置为 `UseHttpPost`，你可以可以使用 `UseImageLocation` 来指定生成的图表图像所在的文件夹。

你还可以通过将 `ImageType` 属性设置为 `Bmp`、`JPEG`、`P`（默认值）或 `Emf` 之一来定义图表使用的图像类型。当你选择 Jpeg 格式时，还可以将 `Compression` 属性设置为 0 到 100 之间的值，其中 0 提供最佳画质，100 最差。

![](img/b5597c749e848b27b0d305153ae16106_721_0.png)

图 16-5：图像处理的属性

## 更改图像位置

当你将图表图片渲染为图像时，它会自动保存到文件中。`ImageLocation` 属性决定了该文件的绝对或相对位置及名称，并根据指定的图像类型自动添加文件扩展名。

打开 SimpleAspNetChart 项目以尝试图像渲染选项。在解决方案资源管理器的项目根目录下创建一个文件夹，并将其命名为 `ChartImages`。将 `ImageStorageMode` 更改为 `UseImageLocation` 将导致图像存储在我们定义的文件夹中。将 `ImageLocation` 属性设置为 `/ChartImages/ChartPic#`。此值告诉位置控件渲染的图表图片应该存储在何处。`#SEQ(4,3)` 格式程序指示图创建一个创建一个数字作为图表文件名的一部分，其中 4 是序列号，3 是图像生存时间（秒）。

按 Ctrl+F5 启动应用程序，并使用不同的参数点击“Draw the Chart”按钮三次。在不关闭程序的情况下，返回 Visual Studio。在解决方案资源管理器中，右键点击 `ChartImages` 文件夹，然后点击 Windows 资源管理器中的“打开文件夹”命令。你可以看到自应用程序启动以来渲染的所有图表图像，其标题显示如图 16-6 所示。

你可以识别出已渲染的四张图片。第一张只包含图表类型。现在，再次使用一组新参数点击“Draw the Chart!”按钮，查看 `ChartImages` 文件夹。它仍然有四张图像，但由于 `#SEQ(4,3)` 中的 4，第一张图像被代表最后一个图表的文件覆盖了。你可以在图 16-7 中查看文件夹内容。

![](img/b5597c749e848b27b0d305153ae16106_722_0.png)

图 16-6：ChartImages 文件夹中渲染的图表图片

![](img/b5597c749e848b27b0d305153ae16106_722_1.png)

图 16-7：新文件覆盖了旧文件。

当你查看图表页面的 HTML 源代码时，你会发现现在 `<img>` 标签使用对图片文件的直接引用：

```
<img id="Chart1" src="ChartImages/ChartPic_000001.png?06b79a20-fae8-47f7-8c2-255a3c9b3d9" alt="" style="height:400px;width:600px;border-width:0px />
```

## 更改图像格式

你可以更改 `ImageType` 属性来定义为图表渲染图像的文件类型。此属性的值取自 `ChartImage` 枚举。你没有太多选择，而且无法为所选的图像类型选择任何子类型。表 16-1 总结了你可以选择的类型，并为你提供了在不同场景下使用它们的几种格式。

表 16-1：ImageType 属性值

| IMAGETYPE 值 | 说明 |
|---|---|
| BMP | 这是一种具有 32 位像素深度的未压缩 BMP 格式。一张 600x400 像素的图像占用约 938 KB。这种格式在通过网络传输图片时比其他格式需要更多带宽。但在服务器端，由于缺少压缩，渲染其他格式可能需要更少的 CPU 周期。仅当你显式在客户端需要 BMP 格式——或在服务器端进行处理时使用它。 |
| JPEG | 著名的 JPEG 格式默认产生高质量。你可以使用 `Compression` 属性来定义 JPEG 值（0 到 100 之间，0 提供最佳质量，100 最差）。对于图 16-3 所示的 600x400 像素，在 `Compression` 设置为 0 的情况下分别提供 58 KB 和 15 KB 的大小。这种格式可以产生最小的文件——代价是质量下降。你可以有效地将此格式用于颜色少且大面积具有相同颜色和调性的图表。 |
| PNG | 作为图表图像的默认格式，PNG 格式在大多数场景下都是最好的。它为图表图像提供无损压缩，并在保持较小尺寸的同时高质量。PNG 使用的压缩算法对于类图位图特别有效，通常产生比 JPEG 更小的文件。图 16-3 中的图片产生大小为 18 KB 的 PNG 文件。相比之下，JPEG 文件占用 58 KB。除非你有特殊原因，否则使用 PNG 格式。 |
| EMF | 此格式使用增强型元文件 (EMF) 生成图像。这种格式记录了绘制图片时使用的图形原语，因此它是结合了存储位图能力的矢量格式。这种格式的图片通常尺寸最小，主要用于折线图。然而，与其他格式不同，EMF 文件可能会根据浏览器或其他应用程序显示出不同的效果。 |

如果你面临难以选择合适文件类型的情况，请定义场景、执行并评估它们。使用默认 PNG 格式在大多数场景下都有效。

## 在遗留网站中使用图表

通常，你必须将网页集成到遗留网站中。你可以像处理其他 ASP.NET 页面一样嵌入使用 ASP.NET Chart 控件创建的图表。一种解决方案是使用 HTML `<iframe>` 标签，定义了一个包含另一个文档的内联框架。PetCharts 项目有一个名为 `HtmlPageWithIFrame.html` 的页面，代表一个遗留网站。该页面的源代码简单，如列表 16-7 所示。

列表 16-7：HtmlPageWithIFrame.html

![](img/b5597c749e848b27b0d305153ae16106_724_0.png)

```html
<html>
<head>
<title>Legacy Page using IFRAME</title>
</head>
<body>
<h3>此示例演示了如何在现有页面的 <iframe> 标签中使用 ASP.Net Chart 控件</h3>
<iframe style="width:800px;height:400px" src="DataBindTable.aspx" border="1" width="800" height="400" scrolling="no">
<iframe style="width:200px;height:400px" src="LegacyHtml.htm" border="0" width="200" height="400" scrolling="no"></iframe>
</body>
</html>
```

HtmlPageWithIFrame.html 文件可在 Wrox.com 下载

该页面包含两个 `<iframe>` 标签。`DataBindTable.aspx` 页面产生图 16-4 所示的图表。你不需要更改页面即可将图表嵌入遗留网站。第二个 `<iframe>` 嵌入了遗留网站的另一个 HTML 页面。图 16-8 显示了显示 `HtmlPageWithIFrame.htm` 页面时看到的内容。

![](img/b5597c749e848b27b0d305153ae16106_725_0.png)

图 16-8：向遗留网站添加图表

## 二进制流渲染

当使用二进制流时，图像直接发送到客户端。当浏览器请求图表图像时，其方式与从 Web 服务器请求静态图像相同。这对于图表图像在运行时频繁修改或使用表单时特别有用。二进制流渲染方法很快，因为它不需要磁盘空间或写入临时图像文件的安全权限。

你可以通过两个页面轻松实现二进制流：

- 第一页：创建 Chart 控件的页面。这是一个简单的 .aspx 页面，其中 Chart 控件的 `RenderType` 属性设置为 `BinaryStreaming`。在此页面，所有 HTML 标签都被删除，只留下 XML 格式的 Chart 定义。你仍然可以使用后台代码动态初始化图表。
- 第二页：另一个引用带有 Chart 控件的第一页页面。此页面包含一个 `<img>` 标签（或 `<asp:Image>` 元素），其 `src`（或 `ImageURL`）属性设置为第一个页的名称。

打开 PetCharts 项目，你可以找到一个二进制渲染的示例。Chart 控件定义在 `DogSalesChart.aspx` 文件中，如列表 16-8 所示。

