
`System.Windows.FrameworkElement`

`System.Windows.Controls.Control`

`System.Windows.Controls.Calendar`

你可以使用各种属性来处理 `Calendar` 类（或控件）。其中大多数属性是依赖属性和附加属性。表 17.3 列出了 `Calendar` 类的一些值得注意的属性：

表 17.3：`Calendar` 类的值得注意的属性
| Property | Description |
|---|---|
| BlackoutDates | Sets or retrieves the list of dates that cannot be selected |
| DisplayDate | Sets or retrieves a particular date that is displayed |
| DisplayDateEnd | Sets or retrieves the last date that is displayed |
| DisplayDateStart | Sets or retrieves the first date that is displayed |
| DisplayMode | Allows you to display the Calendar control in months, years, or decades |
| FirstDayOfWeek | Sets or retrieves the first day of the week |

**表 17.3：`Calendar` 类的重要属性**

| 属性 | 说明 |
| --- | --- |
| IsEnabled | 获取或设置一个值，该值指示用户是否可以与 `Calendar` 控件交互 |
| IsTodayHighlighted | 允许您指定是否突出显示当前日期 |
| SelectedDate | 设置或获取当前选定的日期 |
| SelectedDates | 获取当前选定日期的集合 |
| SelectionMode | 设置或获取一个值，该值指示所做的选择类型 |

表 17.4 列出了 `Calendar` 类的一些重要事件：

**表 17.4：`Calendar` 类的重要事件**

| 事件 | 说明 |
| --- | --- |
| DisplayDateChanged | 当 `DisplayDate` 属性更改时发生 |
| DisplayModeChanged | 当 `DisplayMode` 属性更改时发生 |
| SelectedDatesChanged | 当当前 `SelectedDates` 属性的集合发生更改时发生 |

> **注意**
> `Calendar` 控件间接使用 `DayButton` 和 `DateTime` 类。`DayButton` 类提供处理日历中特定日期或天的功能。`DateTime` 类允许您处理日期和时间。

接下来，让我们讨论 `DatePicker` 控件。

## DatePicker 控件

正如您之前所学，您可以使用 `Calendar` 控件来处理日历中的日、月和年。您还可以使用 `DatePicker` 控件来处理日期，因为它允许您选择日期。它有一个文本框和一个下拉日历，如图 17.10 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_886_0.png)

图 17.10：显示一个 `DatePicker` 控件

用户可以通过在文本框中输入日期，或在下拉日历中单击所需日期来指定日期。

`DatePicker` 类位于 Silverlight 3.0 的 `System.Windows.Controls` 命名空间中的 `System.Windows.Controls.dll` 程序集中，它扩展了 `Control` 类，允许您选择日期。`DatePicker` 类的类层次结构如下：

```
System.Object

  System.Windows.DependencyObject

    System.Windows.UIElement

      System.Windows.FrameworkElement

        System.Windows.Controls.Control

          System.Windows.Controls.DatePicker
```

`DatePicker` 类中定义了各种属性，允许您在内置文本框或日历中处理日期。这些属性主要提供对内置下拉日历的访问和操作，因此 `DatePicker` 类的某些属性与 `Calendar` 类的属性相同。表 17.5 列出了 `DatePicker` 类的重要属性：

**表 17.5：`DatePicker` 类的重要属性**

| 属性 | 说明 |
| --- | --- |
| BlackoutDates | 设置或获取不可选择日期的集合 |
| CalendarStyle | 设置或获取下拉日历的样式 |
| DisplayDate | 设置或获取要显示的特定日期 |
| DisplayDateEnd | 设置或获取下拉日历中用户可见的最后日期 |
| DisplayDateStart | 设置或获取下拉日历中用户可见的第一个日期 |
| FirstDayOfWeek | 设置或获取特定周的第一天 |
| IsDropDownOpen | 允许您指定下拉日历是可见还是折叠 |
| IsEnabled | 允许您指定 `DatePicker` 控件在 Silverlight 应用程序中是否启用 |
| IsTodayHighlighted | 获取或设置一个值，指示是否突出显示当前日期 |
| SelectedDate | 设置或获取用户当前选定的日期 |
| SelectedDateFormat | 设置或获取用于显示日期的格式 |
| Text | 设置或获取 `DatePicker` 控件上显示的文本 |

`DatePicker` 类还具有各种事件，这些事件在您选择日期时不同时间发生。表 17.6 列出了 `DatePicker` 类的重要事件：

**表 17.6：`DatePicker` 类的重要事件**

| 事件 | 说明 |
| --- | --- |
| CalendarClosed | 当下拉日历关闭时立即发生 |
| CalendarOpened | 当下拉日历打开时发生 |
| SelectedDateChanged | 当选定新日期时发生 |

接下来，让我们讨论 Silverlight 3.0 中的 `GridSplitter` 控件。

## GridSplitter 控件

`GridSplitter` 控件是 Silverlight 3.0 控件，允许用户根据需要移动行和列。使用 `GridSplitter` 控件，用户可以移动行和列以调整它们之间的空间。`GridSplitter` 控件始终调整整行或整列，而不仅仅是网格中的单个单元格。图 17.11 显示了两个 `GridSplitter` 控件：一个位于 Cell-1 的顶部，另一个位于 Cell-3 和 Cell-4 之间：

![](img/e073a4882197be4ab61103cbe0bcb394_887_0.png)

图 17.11：Silverlight 3.0 中的 `GridSplitter` 控件

`GridSplitter` 控件由 `GridSplitter` 类提供，该类位于 `System.Windows.Controls` 命名空间中的 `System.Windows.Controls.dll` 程序集中。`GridSplitter` 类的类层次结构是：

```
System.Object

  System.Windows.DependencyObject

    System.Windows.UIElement

      System.Windows.FrameworkElement

        System.Windows.Controls.Control

          System.Windows.Controls.GridSplitter
```

`GridSplitter` 类具有多种属性，您可以使用这些属性来处理 `GridSplitter` 控件。表 17.7 列出了 `GridSplitter` 类的重要属性：

**表 17.7：`GridSplitter` 类的重要属性**

| 属性 | 说明 |
| --- | --- |
| IsEnabled | 允许您指定 `GridSplitter` 控件在 Silverlight 应用程序中是启用还是禁用 |
| PreviewStyle | 设置或获取用于预览行和列更改的样式 |
| ShowsPreview | 允许您指定是否在 `GridSplitter` 控件中显示预览 |

请注意，`GridSplitter` 类主要使用 `Grid` 控件的附加属性来指定可移动的行和列。例如，您可以将 `Grid.Row`、`Grid.RowSpan`、`Grid.Column` 和 `Grid.ColumnSpan` 附加属性与 `GridSplitter` 控件一起使用。`GridSplitter` 控件调整行和列的方向由 `GridSplitter` 的 `HorizontalAlignment` 和/或 `VerticalAlignment` 属性决定。

## HyperlinkButton 控件

`HyperlinkButton` 控件是一个包含超链接的按钮。`HyperlinkButton` 控件结合了超链接和按钮的功能。当您单击 `HyperlinkButton` 控件时，您会被重定向到当前 Web 应用程序或另一个 Web 应用程序中的网页。您可以指定要重定向用户的特定窗口或框架的名称。图 17.12 显示了一个 `HyperlinkButton` 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_888_0.png)

图 17.12：Silverlight 3.0 中的 `HyperlinkButton` 控件

`HyperlinkButton` 控件是 `HyperlinkButton` 类的一个实例，该类位于 `System.Windows.Controls` 命名空间中的 `System.Windows.Controls.dll` 程序集中。`HyperlinkButton` 类的类层次结构是：

```
System.Object

  System.Windows.DependencyObject

    System.Windows.UIElement

      System.Windows.FrameworkElement

        System.Windows.Controls.Control

          System.Windows.Controls.ContentControl

            System.Windows.Controls.Primitives.ButtonBase

              System.Windows.Controls.HyperlinkButton
```

`HyperlinkButton` 类有一些属性，您可以使用这些属性来处理 `HyperlinkButton` 控件。表 17.8 列出了 `HyperlinkButton` 类的重要属性：

**表 17.8：`HyperlinkButton` 类的重要属性**

| 属性 | 说明 |
| --- | --- |
| NavigateUri | 设置或获取当用户单击 `HyperlinkButton` 控件时被重定向到的网页的 URI。该网页可以在同一个应用程序中，也可以在不同的应用程序中。 |
| TargetName | 设置或获取用户被重定向到的网页上的窗口或框架的名称。 |

接下来，让我们讨论 Silverlight 3.0 中的 `MediaElement` 控件。

## MediaElement 控件

在某些情况下，您可能希望包含一个媒体文件并在应用程序中播放它。在这种情况下，您可以将媒体包含在当前项目中；但是，您还需要播放媒体的功能。Silverlight 提供了 `MediaElement` 控件来提供此类功能。`MediaElement` 控件允许您在 Silverlight 应用程序中添加媒体。您可以使用 `MediaElement` 控件在应用程序中添加视频或音频或两者。`MediaElement` 控件为您提供一个矩形区域来显示视频或播放音频。请注意，此矩形区域没有任何用于播放、暂停或停止媒体播放的按钮。但是，您可以使用 `MediaElement` 类的属性、方法和事件来定义操作 `MediaElement` 控件中媒体播放的功能。图 17.13 显示了 `MediaElement` 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_889_0.png)

图 17.13：在 `MediaElement` 控件中托管的视频

`MediaElement` 控件是 `MediaElement` 类的一个实例，该类位于 `System.Windows.Controls` 命名空间中的 `System.Windows.Controls.dll` 程序集中。`MediaElement` 类的类层次结构是：

```
System.Object

  System.Windows.DependencyObject

    System.Windows.UIElement

      System.Windows.FrameworkElement

        System.Windows.Controls.MediaElement
```
