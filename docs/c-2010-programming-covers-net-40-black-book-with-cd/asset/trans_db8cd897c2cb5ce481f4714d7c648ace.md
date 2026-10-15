

Table 11.10: 显示 DocumentViewer 类的属性

| Property | Description |
|---|---|
| ShowPageBorders | 获取或设置一个值，该值指示是否显示带阴影的页面边框 |
| VerticalOffset | 获取或设置垂直滚动位置 |
| VerticalPageSpacing | 获取或设置显示页面之间的垂直间距 |
| ViewportHeight | 检索可滚动内容区域的垂直尺寸 |
| ViewportWidth | 检索可滚动内容区域的水平尺寸 |
| ViewThumbnailsCommand | 检索显示页面缩略图表示的命令 |
| Zoom | 获取或设置文档缩放百分比 |

## The FixedDocument Class

FixedDocument 类托管一个便携、高保真且固定格式的文档。它具有用户文本选择、键盘导航和搜索功能的读取访问权限。FixedDocument 类包含在 System.Windows.Documents 命名空间中。FixedDocument 类的唯一允许的子元素是 PageContent 类。

FixedDocument 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.ContentElement
        System.Windows.FrameworkContentElement
          System.Windows.Documents.FixedDocument
```

以下代码片段显示了如何将 FixedDocument 添加到 WPF 应用程序中：

```
<FixedDocument>
  <!--Pages-->
</FixedDocument>
```

FixedDocument 类的属性列在表 11.11 中：

Table 11.11: 显示 FixedDocument 类的属性

| Property | Description |
|---|---|
| DocumentPaginator | 检索为 FixedDocument 提供分页服务的分页器，类似于从一页移动到下一页 |
| IsInputMethodEnabled | 检索一个值，该值指示是否启用了输入法系统以处理此类输入 |
| LogicalChildren | 检索一个枚举器，用于访问 PageContent 子类中的文档 |
| Pages | 检索文档的 PageContent 元素的集合 |
| PrintTicket | 获取或设置与当前文档关联的打印设置 |
| ToolTip | 获取或设置在用户界面中为 FixedDocument 类显示的工具提示对象 |

FixedDocument 类包含以下子类，列示如下：

- FixedPage
- PageContent

让我们详细讨论这些类。

## The FixedPage Class

FixedPage 类为固定文档中的高保真、固定格式页面提供内容。它在内容的开始和结束处自动定义分页符。

FixedPage 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Documents.FixedPage
```

以下代码片段显示了如何将 FixedPage 类添加到 WPF 应用程序中：

```
<FixedPage>
  <!--Children-->
</FixedPage>
```

FixedPage 类的属性列在表 11.12 中：

Table 11.12: 显示 FixedPage 类的属性

| Property | Description |
|---|---|
| Children | 检索 FixedPage 类的子元素集合。 |
| ContentBox | 获取或设置内容区域的边界矩形。此区域指的是页边距内的页面。 |
| DesiredSize | 检索固定页面的大小，该大小在实现控件的布局行为时计算得出。 |
| PrintTicket | 获取或设置与将要打印的页面关联的打印设置。 |

## The PageContent Class

PageContent 类提供有关 FixedDocument 类中 FixedPage 元素的信息。它不需要加载各个页面。PageContent 类的实例是 FixedDocument 类的唯一允许的子元素。FixedDocument 中 PageContent 元素的顺序定义了页面顺序。PageContent 类的 Source 依赖属性定义了相应 FixedPage 的 URI。

PageContent 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Documents.PageContent
```

以下代码片段显示了如何将 PageContent 类添加到 WPF 应用程序中：

```
<PageContent>
  <!--Child-->
</PageContent>
```

PageContent 类的属性列在表 11.13 中：

Table 11.13: 显示 PageContent 类的属性

| Property | Description |
|---|---|
| LinkTargets | 检索可以链接到其他文档或同一文档其他部分的页面上的元素集合 |
| Source | 获取或设置 FixedPage 内容数据流的 URI |
| Triggers | 检索直接在 PageContent 类的元素上或其子元素上建立的触发器集合 |

## Flow Documents

Flow 文档旨在为用户提供更好的内容显示和可读性。Flow 文档在窗口调整大小时自动调整其内容。它还提供高级文档功能，例如优化可读性的查看模式以及更改字体大小和外观的能力。Flow 文档的各种优势如下：

- 允许您对整个文档执行全文搜索。
- 为您提供不同的页面查看模式选项，例如单页查看模式、双页查看模式或连续滚动查看模式。
- 包含内置页面导航控件，其中包括一个按钮，可帮助您移动到下一页或上一页。该控件还提供当前页码和总页数的指示器。
- 包含缩放控件，可通过分别单击加号或减号按钮来帮助增加或减少缩放级别。缩放控件还包括用于调整缩放级别的滑块。

Flow 文档包含以下组件：

- Flow document controls
- Flow content elements

让我们逐一详细讨论这些内容。

## Flow Document Controls

Flow 文档控件用于显示 Flow 文档的内容。Flow 文档中内容的显示取决于用于托管流内容的对象的外观。Flow 文档控件的不同类型如下：

- FlowDocumentScrollViewer
- FlowDocumentReader
- FlowDocumentPageViewer
- RichTextBox

其中，FlowDocumentReader 控件、FlowDocumentPageViewer 控件和 FlowDocumentScrollViewer 控件为只读控件。

## The FlowDocumentScrollViewer Control

FlowDocumentScrollViewer 控件允许您以连续滚动模式查看流内容。它以滚动条显示整个文档，并在内容超出显示区域大小时允许您浏览内容。如果内容适合窗口大小，则滚动条不可见。默认情况下，选择显示为 FlowDocumentScrollViewer 时始终显示垂直滚动条。如果 HorizontalScrollBarVisibilty 属性设置为 True，则水平滚动条可见。Flow 文档是 FlowDocumentScrollViewer 控件的唯一允许子元素。

FlowDocumentScrollViewer 控件的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.FlowDocumentScrollViewer
```
