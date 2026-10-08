
| 如果你需要针对以下问题的快速解决方案： | 参见页码： |
|--- |--- |
| 使用 WPF 控件 | 386 |
| 使用资源、样式和模板 | 399 |
| 使用触发器 (Triggers) | 408 |
| 在控件中使用 WPF 命令 | 411 |
| 在 WPF 应用程序中托管 Windows Forms 控件 | 411 |
| 在 Windows Forms 应用程序中托管 WPF 控件 | 412 |

# 第 2 章：使用 WPF 4.5 控件、资源、样式、模板和命令

## 深入探讨

Windows Presentation Foundation (WPF) 帮助你从代码视图设计设计视图；从而允许你一次处理一个视图。你的代码可以在设计视图中直接查看，因为 WPF 是基于所见即所得 (WYSIWYG) 原的。WPF 应用程序是借助扩展应用程序标记语言 (XAML) 设计的。这种语言还定义了 WPF 应用程序中控件的层次结构。你可以使用 XAML 控制它们并赋予它们额外的功能。在 WPF 中编程与在 Windows Forms 中编程非常相似。两者唯一区别在于存在 WPF 设计视图。WPF 中的控件是交互元素，它们继承自 `System.Windows`、`Microsoft.Win32` 和 `System.Documents` 命名空间。

本章描述了 WPF 中执行的控件。你还将学习 WPF 中使用的样式、模板和资源。此外，本章还讨论了控件响应命令所需的触发器 (triggers)。

## WPF 4.5 控件

WPF 拥有一套丰富的控件，其中某些控件与 Windows Forms 类似。Windows Forms 和 WPF 应用程序的控件在外观和行为上不同。你可以使用 XAML 修改控件。当你更改 XAML 中控件的代码时，设计视图中控件的外观和行为会自动更改。在 WPF 应用程序中，控件的 XAML 代码以树的形式显示。WPF 中控件的运行取决于两个类：`FrameworkElement` 和 `Control` 类。`Control` 类是派自 `FrameworkElement` 类的基类。

WPF 提供了各种可用的控件，如 `Grid`、`TextBox` 和 `RichTextBox` 控件。WPF 中的每个控件都归类以下类别之一：

- 容器控件 (Container controls)
- 简单控件 (Simple controls)
- 内容控件 (Content controls)
- 带有头部的内容控件 (Headered content controls)
- 项目控件 (Items controls)
- 带头部的项目控件 (Headered items controls)
- 杂控件 (Miscellaneous controls)

让我们在接下来的章节中详细查看这些类别。

### 容器控件

WPF 中的容器控件包括 `Grid`、`UniformGrid`、`Canvas`、`DockPanel`、`StackPanel` 和 `WrapPanel`。这些控件为子控件提供了内置的布局功能。子控件是放置在容器内的控件。例如，在 `Grid` 中使用的 `Label` 就是一个子控件。容器控件处理子控件的布局和定位。

现在让我们学习以下控件：

- Grid
- UniformGrid
- Canvas
- DockPanel
- StackPanel
- WrapPanel

#### 深入探讨

### Grid 控件

最常见的容器控件是 `Grid` 控件。每当你向 WPF 应用程序添加新窗口时，默认情况下都包含一个 `Grid`。`Grid` 控件包含单个单元格。你可以在 `Grid` 内部添加额外的行和列。`Grid` 中的子元素按行和列排列。`Grid` 控件还可以包含另一个 `Grid` 作为其子元素。

`Grid` 由 `Grid` 类表示，该类派自 `Panel` 类。`Grid` 类的继承体系如下：

```
System.Object
System.windows.Threading.DispatcherObject
System.windows.DependencyObject
System.windows.Media.Visual
System.windows.Framework.UIElement
System.windows.Controls.Panel
System.windows.Controls.Grid
```

你可以使用以下代码向 WPF 应用程序添加 `Grid`：

```xml
<Grid>
  <!--Child elements-->
</Grid>
```

表 9.1 显示 Grid 类的重要属性

| 属性 | 描述 |
|---|---|
| ColumnDefinitions | 获取 `Grid` 控件中定义的 `ColumnDefinition` 类。`ColumnDefinition` 类提供了对 `Grid` 列有序集合的访问。 |
| RowDefinitions | 获取提供对 `Grid` 行有序集合访问的 `RowDefinition` 类。 |
| ShowGridLines | 获取或指定指示 Grid 网格线可见性的值。 |

除了表 9.1 列出的属性外，`Grid` 类还有一些附加属性。XAML 中的附加属性引用可以在任何对象上设置的全局属性。

`Grid` 类的附加属性如 9.2 所示：

表 9.2：显示 Grid 类的附加属性

| 属性 | 描述 |
|---|---|
| Column | 获取或指定值，以便在 `Grid` 控件的特定列中显示特定内容 |
| ColumnSpan | 获取或指定值，显示子控件在 `Grid` 控件中跨越的列总数 |
| IsSharedSizeScope | 获取或指定值，显示多个 `Grid` 元素可以与其他 `Grid` 元素共享大小信息 |
| Row | 获取或指定值，显示哪些行内容出现在 `Grid` 控件中 |
| RowSpan | 决定子控件在 `Grid` 控件中跨越的行数 |

WPF 默认添加 `Grid`。

图 9.1 显示了添加了 `Grid` 控件的 WPF 应用程序默认视图：

# 第 9 章：使用 WPF、资源、样式、模板和命令

![](img/17af790174c480761404624aeed9b30b_375_0.png)

图 9.1：Grid 控件

### UniformGrid 控件

`UniformGrid` 控件包含 Grid 控件中的所有内容，使得网格中的单元格保持相同的大小。当你向 `UniformGrid` 控件添加不同的控件时，所有控件将以网格模式排列。`UniformGrid` 的单元格会自动调整以适应不同类型和大小的控件。

`Uniform` 由 `UniformGrid` 类表示，该类派自 `Panel` 类。`UniformGrid` 类的继承关系如下：

- `System.object`
- `System.windows.Threading.Dispatcherobject`
- `System.windows.DependencyObject`
- `System.windows.UI.FrameworkElement`
- `System.windows.Controls.Panel`
- `System.windows.Controls.Primitives.UniformGrid`

你可以使用以下代码段将 `UniformGrid` 添加到 WPF 应用程序中：

```
<UniformGrid>
    <!-- child elements -->
</UniformGrid>
```

表 9.3 显示了 `UniformGrid` 类的重要属性：

| 表 9.3：UniformGrid 类的重要属性显示 |
| --- | --- |
| Columns | 获取或设置 Grid 控件的列数 |
| FirstColumn | 获取或设置 Grid 控件第一行中空白单元格的数量 |
| Rows | 获取或设置 Grid 控件的行数 |

图 9.2 显示了添加到 WPF 应用程序中的 UniformGrid 控件：

336

![](img/17af790174c480761404624aeed9b30b_376_0.png)

图 2：UniformGrid 控件

> 注意
>
> 在 WPF 中，每当你从工具箱将控件添加到 WPF 设计器时，系统会自动为该控件生成相应的 XAML 代码。

#### Canvas 控件

Canvas 控件是最简单的控件，它通过使用相对于 Canvas 控件的坐标来支持其子元素的绝对定位。当你将控件放置在 Canvas 控件中，必须指定一个水平属性和一个垂直属性来指定控件在 Canvas 内部的起始位置。该控件是唯一没有内置布局的控件。默认情况下，Canvas 的 Height 和 Width 属性设置为零。

要在 Canvas 控件上定位子元素，你需要设置其 `Canvas.Top`、`Canvas.Left`、`Canvas.Right` 或 `Canvas.Bottom`。

Canvas 由 `Canvas` 类表示，该类派自 `Panel` 类。Canvas 类的继承层次结构如下：

```
System.object
System.windows.DependencyObject
System.windows.Media.Visual
System.windows.UI.Element
System.windows.Framework
System.windows.Controls.Panel
System.windows.Controls.Canvas
```

你可以使用以下代码段将画布添加到到 WPF 应用程序中：

```
<Canvas>
    <child elements/>
</Canvas>
```

表 9.4 描述了 `Canvas` 类显著非附加属性（Not Attached properties）：

| 属性 | 描述 |
|---|---|
| Bottom | 获取或设置一个表示控件底部与其父控件底部之间距离的值 |
| Left | 获取或设置一个表示控件左侧与其父控件左侧之间距离的值 |

337

# 第 9 章：使用 WPF 4.5 控件、资源、样式、模板和命令

| 表 9.4：Canvas 类的重要附加属性显示 |
| --- | --- |
| Right | 获取或设置一个表示画布右侧与其父控件右侧之间距离的值 |
| Top | 获取或设置一个表示画布顶部与其父控件顶部之间距离的值 |

图 9.3 添加到 WPF 应用程序中的 Canvas 控件：

![](img/17af790174c480761404624aeed9b30b_377_0.png)

图 9.3： Canvas 控件

### DockPanel

DockPanel 控件定义了一个区域，你可以在该区域内相对地垂直或水平地排列子元素。你可以使用 `Top`、`Left`、`Right` 或 `Bottom` 设置子元素在 DockPanel 中的位置。

默认情况下，DockPanel 中的元素会扩展到宽度。如果你想更改子元素的大小，可以使用 `Height` 和 `Width`。例如，如果你在 DockPanel 中放置一个控件，它将填充剩余空间。`LastChild` 属性默认是 `true`，你可以通过将其设置为 `False` 来覆盖它。简而言之，DockPanel 的最后一个元素会占据所有空间。

DockPanel 控件由 `DockPanel` 类表示，该类派自 `Panel` 类。DockPanel 的继承层次结构如下：

```
System.object
System.windows.Threading.Dispatcher
System.windows.Media.Visual
System.windows.FrameworkElement
System.windows.Controls.Panel
System.windows.Controls.DockPanel
```

338

你可以使用以下代码段将 DockPanel 添加到 WPF 应用程序中：

```
<DockPanel>
    <child elements/>
</DockPanel>
```

表 9.5 描述了 `Canvas` 类显著的非附加属性：

| 属性 | 描述 |
|---|---|
| LastChild | 获取或设置一个指示最后一个元素是否填充剩余空间的值 |

带有 DockPanel 的重要属性，表 9.6：

| 属性 | 描述 |
|---|---|
| Dock | 获取或设置一个表示控件位置的值 |

图 9.4 显示了添加到 WPF 应用程序中的 DockPanel：

![](img/17af790174c480761404624aeed9b30b_378_0.png)

图 9.4：DockPanel

### StackPanel 控件

StackPanel 控件将子元素排列在单行中，可以是垂直或水平的。默认设置为垂直，你可以通过 `Orientation` 属性进行更改。StackPanel 根据需要进行对齐。StackPanel 拥有 `HorizontalAlignment` 和 `VerticalAlignment` 属性。默认情况下这些属性都设置为 `Stretch`，因此 StackPanel 会填充容器。

StackPanel 控件由 `StackPanel` 类表示，该类派自 `Panel` 类。`StackPanel` 类的继承关系如下：

- `System.object`
- `System.windows.Threading.Dispatcherobject`
- `System.windows.DependencyObject`
- `System.windows.UI.FrameworkElement`
- `System.windows.Controls.Panel`
- `System.windows.Controls.StackPanel`

你可以使用以下代码段将 StackPanel 添加到 WPF 应用程序中：

```
<StackPanel>
    <!-- child elements -->
</StackPanel>
```

表 9.7 显示了 `StackPanel` 类的重要属性：

| 表 9.7：StackPanel 类的重要属性显示 |
| --- | --- |
| HorizontallyScroll | 获取或设置一个指示 StackPanel 是否可以在水平方向滚动的值 |
| CanVerticallyScroll | 获取或设置一个指示 StackPanel 是否可以在垂直方向滚动的值 |
| ExtentHeight | 获取一个包含垂直扩展大小的值 |
| ExtentWidth | 获取一个包含水平扩展大小的值 |
| HorizontalOffset | 获取或设置一个包含滚动内容水平位置的值 |
| Orientation | 获取或设置一个指示子元素在 StackPanel 内部如何堆叠的值 |
| ScrollOwner | 获取或设置一个标识 StackPanel 中控制滚动行为的值 |
| VerticalOffset | 获取一个包含滚动内容垂直位置的值 |
| ViewportHeight | 获取一个包含内容垂直大小的值 |
| ViewportWidth | 获取一个包含内容水平大小的值 |

图 9.5 显示了添加到 WPF 应用程序中的 StackPanel 控件：

![](img/17af790174c480761404624aeed9b30b_379_0.png)

图 9.5：StackPanel 控件

# 深入解析

你可以看到，当你从工具箱添加 StackPanel 控件时，该控件的 XAML 代码会自动添加到应用程序中。

> 注意

你可以选择 StackPanel 或 DockPanel 控件来堆叠子元素；然而，这两个容器控件并不总是产生相同的结果。放置子元素的顺序会影响 DockPanel 控件中子元素的大小，但在 StackPanel 控件中不会。

### WrapPanel 控件

WrapPanel 容器按顺序排列其子元素。子元素的顺序取决于 `Orientation` 属性的值。`WrapPanel.Orientation` 的默认值为 `Horizontal`（水平），这意味着子元素从左到右排列。你可以更改默认行为，并将子元素从上往下排列。

WrapPanel 由 `WrapPanel` 类表示，该类派自 `Panel` 类。WrapPanel 类的继承层次如下：

```
System.Object
System.windows.DispatcherObject
System.windows.DependencyObject
System.windows.Visual
System.windows.UIElement
System.windows.Controls.Panel
System.windows.Controls.WrapPanel
```

你可以使用以下代码片段向 WPF 应用程序中添加 WrapPanel：

```
<WrapPanel>
  <!--子元素-->
</WrapPanel>
```

表 9.8 显示了 WrapPanel 类的 属性

| 属性 | 描述 |
| --- | --- |
| ItemHeight | 获取或设置指定 WrapPanel 控件内包含的所有项的高度的值 |
| ItemWidth | 获取或设置指定控件内包含的所有项的的值 |
| Orientation | 获取或设置指定子元素排列方式的值 |

图 9.6 显示了添加到 WPF 应用程序中的 WrapPanel 控件：

![](img/17af790174c480761404624aeed9b30b_380_0.png)

# 第9 章：使用 WPF 4.5 控件、资源、样式、模板和命令

## 简单控件
