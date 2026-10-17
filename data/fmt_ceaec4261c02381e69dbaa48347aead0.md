
## 深度解析

| 表 14.2: Silverlight 5.0 中的控件 |

| 控件 | 描述 |

| :--- | :--- |

| AutoCompleteBox | 代表一个文本框的控件，用户可以在其中输入内容，并包含一个根据用户输入显示所有匹配项的下拉列表。 |

| DataPager | 提供一个 UI，帮助以多页的形式显示大量数据集合。 |

| TreeView | 以分级方式显示数据项。 |

```xml
XAML 元素示例
<input: AutoCompleteBox xName="ACB">
<my:DataPager xName="DPI"
PageSize="5"
AutoEllipses=True
NumsButtonCount="3"
DisplayMode="PreviousNext"/>
<my:TreeView Header="Object-Oriented Programming Languages>>
<my:TreeView Header="Silverlight" />
</my:TreeView>
```

您应该注意，XAML 元素示例中提供的语法可能会根据您的 Silverlight 中添加的命名空间而变化。例如，如果向应用程序添加了 `xmlns:namespace="clr:System.Windows.Controls"` 命名空间，则控件将带有 `my` 前缀添加。

Silverlight 5.0 包含了新的控件，例如 `MultiScaleImage` 控件，允许您查看并更改多分辨率图像的大小和位置。`MultiScaleImage` 控件是 Deep Zoom 技术的核心。Silverlight 5.0 为 Silverlight 5.0 控件（如 `HyperLink` 和 `Button` 控件）引入了 `ToolTip` 属性。`ToolTipService` 替换了 Silverlight 2.0 Beta 1 中的 `ToolTip` 控件。

Silverlight 5.0 控件间接继承自 `FrameworkElement` 类，该类本身派生自 `UI` 类。因此，由 `FrameworkElement` 类及其基类定义的属性、方法和事件供 Silverlight 控件使用。

现在，让我们逐一讨论每个 Silverlight 5.0 控件。

### Calendar 控件

`Calendar` 控件提供了处理日期、天、月份和年份的功能。该控件显示年份、月份和日期，允许用户从月份或年份中选择特定日期。您可以在月份、年份之间切换，或使用箭头显示用户可见且可选的日期范围，并隐藏日历控件中的特定日期范围。此外，您可以通过操作控件的属性来修改日历控件的外观和感受。图 14.9 显示了一个日历控件：

![](img/17af790174c480761404624aeed9b30b_698_0.png)

## 第 14 章：使用 Silverlight 5.0 增强 Web

`Calendar` 控件是 `Calendar` 类的实例，它存在于 `System.Windows.Controls` 命名下的 `PresentationFramework.dll` 程序集中。`Calendar` 类的类层次结构为：

`System.Object`

`System.Windows.Threading.DispatcherObject`

`System.Windows.Media.Visual`

`System.Windows.UIElement`

`System.Windows.Framework`

`System.Windows.Controls.Control`

`System.Windows.Controls.Calendar`

有很多属性可以用于处理 `Calendar` 类（或控件）。这些属性大部分是依赖属性和附加属性。表 14.3 列出了 `Calendar` 类的一些值得关注的属性：

表 14.3: Calendar 类的值得关注的属性

| 属性 | 描述 |

| :--- | --- |

| BlackDates | 设置无法选择的日期列表 |

| DisplayDate | 获取当前显示的特定日期 |

| DisplayDateEnd | 设置显示的最后一个日期 |

| DisplayDateStart | 设置显示的第一个日期 |

| DisplayMode | 允许您以月份、年份或十年为单位显示日历控件 |

| FirstOfWeek | 设置每周的第一天 |

| IsEnabled | 获取一个值，指示用户是否可以与日历控件交互 |

| IsTodayHighlighted | 允许指定当前日期是否高亮 |

| SelectedDate | 设置当前选择的日期 |

| SelectedDates | 获取所选日期的集合 |

| SelectionMode | 设置选择类型的值 |

表 14.4 列出了 `Calendar` 类的一些重要事件：

表 14.4: Calendar 类的值得关注的事件

| 事件 | 描述 |

| :--- | --- |

| DisplayChanged | 当 `DisplayDate` 属性更改时触发 |

| DisplayModeChanged | 当 `DisplayMode` 属性更改时触发 |

| SelectedDatesChanged | 当 `SelectedDates` 属性更改时触发 |

> 注意

`Calendar` 控件间接使用 `CalendarDayButton` 和 `DateTime` 类。`CalendarDayButton` 类提供了处理日历中特定天或日期的功能。`DateTime` 类允许处理日期和时间。

接下来，让我们讨论 `DatePicker` 控件。

正如您之前学到的，可以使用 `Calendar` 控件处理日历中的天、月份和年份。您也可以使用 `DatePicker` 控件来处理日期，因为它允许您选择日期。它有一个文本框和一个下拉日历，如图 14.10 所示：

## 深度解析

![](img/17af790174c480761404624aeed9b30b_700_0.png)

图 14.1: 显示 `DatePicker` 控件

用户可以通过在框中输入或在下拉列表中选择指定日期。

`DatePicker` 类存在于 `System.Windows.Controls` 命名下的 `PresentationFramework.dll` 程序集中，它允许用户选择日期。`DatePicker` 的层次结构为：

```
System.Object
System.windows.DispatcherObject
System.windows.DependencyObject
System.windows.Media.Visual
System.windows.UIElement
System.windows.FrameworkElement
System.windows.Controls.Control
```

`DatePicker` 中定义了许多属性，允许您处理文本框或日历，某些属性与 `Calendar` 类相同。表 14.5 列出了 `DatePicker` 的值得关注的属性：

表 14.5: Calendar 的值得关注的属性

| 属性 | 描述 |

| :--- | --- |

| BlackDates | 设置日期集合 |

| CalendarStyle | 设置或获取 `DatePicker` 的样式 |

| DisplayDate | 获取特定日期 |

| DisplayEndDate | 设置可见最后一个日期 |

| DisplayStart | 设置可见第一个日期 |

| FirstOfWeek | 获取每周的第一天 |

| IsEnabled | 允许指定下拉日历是否启用 |

| IsTodayHighlighted | 允许指定当前日期是否高亮 |

| SelectedDate | 设置当前选择的日期 |

| SelectedDates | 获取所选日期的集合 |

| SelectionMode | 设置选择类型的值 |

`DatePicker` 类还有在选择日期时发生的事件。表 14.6 列出了值得关注的事件：

表 14.6: Calendar 类的值得关注的事件

| 事件 | 描述 |

| :--- | --- |

| CalendarClosed | 当下拉日历关闭时触发 |

| CalendarOpened | 当下拉日历打开时触发 |

| SelectedChanged | 当选择新日期时触发 |

接下来，让我们讨论 Silverlight 5.0 中的 `GridSplitter` 控件。

### GridSplitter 控件

`GridSplitter` 控件是一种 Silverlight 5.0 控件，允许用户移动行和列。通过 `GridSplitter` 控件，用户可以移动行和列以适应它们之间的空间。`GridSplitter` 控件总是调整整个行或整个列，而不仅仅是一个单元格。图 14.11 显示了两个 `GridSplitter`：一个位于 Cell-1 顶部，另一个位于 Cell-3 和 Cell-4 之间。

![](img/17af790174c480761404624aeed9b30b_701_0.png)

`GridSplitter` 控件由 `GridSplitter` 类提供，该类存在于 `System.Windows.Controls` 命名下的 `PresentationFramework.dll` 程序集中。`GridSplitter` 类的层次结构为：

+   * System.object

* System.windows.Threading.DispatcherObject

* System.windows.DependencyObject

* System.windows.Media.Visual

* System.windows.UIElement

* System.windows.FrameworkElement

* System.windows.Controls.Control

* System.windows.Controls.Primitives.Thumb

* System.windows.Controls.GridSplitter

`GridSplitter` 类有许多可以与 `GridSplitter` 控件一起使用的属性。表 14.7 列出了 `GridSplitter` 类的一些值得关注的属性：

| 表 14.7: GridSplitter 类的值得关注的属性 |

| 属性 | 描述 |

| :--- | --- |

| IsEnabled | 允许指定 `GridSplitter` 控件在应用程序中启用或禁用 |

| PreviewStyle | 设置预览行列变化的样式 |

| ShowsPreview | 允许指定在 `GridSplitter` 控件中显示预览 |

注意，`GridSplitter` 类主要使用控件的附加属性来指定可移动的行和列。例如，您可以在 `GridSplitter` 控件在使用 `Grid.Row`、`Grid.RowSpan`、`Grid.Column` 和 `Grid.ColumnSpan` 附加属性。`GridSplitter` 控件调整行和列的方向由 `GridSplitter` 的 `HorizontalAlignment` 和/或 `VerticalAlignment` 属性决定。

# 深入解析

## 超链接控件 (Hyperlink Control)

`HyperlinkButton` 是一个包含超链接的按钮。`HyperlinkButton` 控件结合了超链接和按钮的特性。当你点击 `HyperlinkButton` 控件时，你将被重定向到当前 Web 应用程序或不同 Web 应用程序中的 Web 页面。你可以指定重定向用户的特定窗口或帧。图 14.12 显示了一个 `HyperlinkButton` 控件：

![](img/17af790174c480761404624aeed9b30b_702_0.png)

图 14.12：Silverlight 5.0 中的 `HyperlinkButton` 控件

`HyperlinkButton` 类是 `HyperlinkButton` 类的实例，存在 `System.Windows.Controls` 命名空间下的 `System.Windows.dll` 程序集中。`HyperlinkButton` 类的层级结构为：

```
System.Object
System.Windows.DependencyObject
System.Windows.UIElement
System.Windows.FrameElement
System.Windows.Controls.ContentControl
System.Windows.Controls.Primitives.ButtonBase
System.Windows.Controls.HyperlinkButton
```

`HyperlinkButton` 类具有一些你可以用于操作 `HyperlinkButton` 控件的属性。表 14.8 列出了 `HyperlinkButton` 类的属性：

| 表 14.8：HyperlinkButton 类的创新特性 |

| 属性 | 描述 |

| --- | --- |

| NavigateUri | 设置或获取用户点击 `HyperlinkButton` 控件时重定向到的 Web 页面的 URI。该 Web 页面可以是相同应用程序或不同应用程序中的。 |

| TargetName | 设置或获取用户重定向到的 Web 页面上的窗口或帧。 |

接下来，让我们讨论 Silverlight 5.0 中的 `MediaElement` 控件。

## MediaElement 控件 (MediaElement Control)

在某些情况下，你希望在应用程序包含并播放媒体文件。在这种情况下，你可以将媒体包含在当前项目中；但你还需要播放媒体的功能。Silverlight 提供的 `MediaElement` 控件允许你在 Silverlight 应用中添加媒体。你还可以使用 `MediaElement` 控件在应用程序中添加视频、音频或两者。

`MediaElement` 控件为你提供了一个矩形区域来显示视频或播放音频。请注意，这个矩形区域没有任何播放、暂停或停止媒体播放的按钮。然而，你可以使用 `MediaElement` 类的属性、方法和事件来定义操作 `MediaElement` 控件中媒体播放的功能。图 14.13 显示了 `MediaElement` 控件。

# 第 14 章：使用 Silverlight 5.0 增强 Web 应用程序

![](img/17af790174c480761404624aeed9b30b_703_0.png)

图 14.13：在 `MediaElement` 控件中托管视频

`MediaElement` 控件是 `MediaElement` 类的实例，存在 `System.Windows.Controls` 命名空间下的 `PresentationFramework.dll` 程序集中。`MediaElement` 类的层级结构：

- System.Object

- System.Windows.Threading.DispatcherObject

- System.Windows.DependencyObject

- System.Windows.Media.Visual

- System.Windows.UI.Element

- System.Windows.FrameworkElement

- System.Windows.Controls.MediaElement

`MediaElement` 类具有多个属性、方法和事件，允许你通过 `MediaElement` 控件添加和操作媒体。表 14.9 列出了 `MediaElement` 类中值得关注的属性：

| 表 14.9：MediaElement 类值得关注的属性 |

| 属性 | 描述 |

| --- | --- |

| Attributes | 获取作为 `MediaElement` 控件中媒体源的高级流读取器 (ASS) 文件中当前条目的属性集合。 |

| AudioStreamCount | 获取当前打开文件中音频流的数量。 |

| AudioStreamIndex | 设置或获取与视频同时播放的音频流索引。此属性的默认值为空引用。 |

| AutoPlay | 设置或获取一个值，表示媒体在媒体加载后是否自动开始播放。默认情况下，此属性的值为 true。 |

| Balance | 设置或获取立体扬声器之间的平衡比例。此属性的默认值为零，范围从 -1 到 1。如果你将此属性的值设置为 -1，则左扬声器以全音量播放。如果你将此属性的值设置为 1，则右扬声器以全音量播放。

# 深入解析

| 表 14.9：MediaElement 类值得关注的属性 |

| 属性 | 描述 |

| --- | --- |

| BufferingProgress | 获取一个表示当前媒体缓冲量的值。此属性的默认值为零，任何到 1 的分数均可。 |

| BufferingTime | 设置缓冲时间的偏移量。此属性的默认值为零。 |

| CanPause | 设置或获取一个值，表示媒体是否可以暂停。 |

| CanSeek | 获取一个值，表示是否可以更改媒体的位置。

| CurrentState | 获取媒体的状态。 |

| DownloadProgress | 获取下载进度。 |

| State | 获取一个值，可以取- Buffering, Opening, Stopped。 |

| Duration | 获取媒体的总时长。 |

| Position | 获取媒体的位置。 |

| RenderedPerSecond | 获取渲染的帧数。 |

| Source | 设置或获取媒体源。 |

| Stretch | 获取一个值，可以取 None、Uniform 或 Fill。 |

| Volume | 设置或获取媒体的音量。 |

| 表 14.10：MediaElement 值得关注的方法 |

| 方法 | 描述 |

| --- | --- |

| Pause | 暂停媒体。 |

| Play | 播放媒体。 |
