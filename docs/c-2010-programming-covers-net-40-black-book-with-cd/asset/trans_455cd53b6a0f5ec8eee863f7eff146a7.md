

![](img/e073a4882197be4ab61103cbe0bcb394_451_0.png)

## TextBlock 控件

WPF 中的 TextBlock 控件负责为应用程序提供灵活的文本支持。TextBlock 控件通常与 WPF 中的文档一起使用。TextBlock 控件的主要属性与文本及其呈现有关。您可以使用 Text 属性向 TextBlock 控件添加文本内容。

TextBlock 控件的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.TextBlock
```

您可以使用以下代码片段将 TextBlock 控件添加到 WPF 应用程序中：

```
<TextBlock>
  <!--Inlines -->
</TextBlock>
```

### 表 10.45：TextBlock 类的注目属性

| 属性 | 描述 |
|---|---|
| BreakAfter | 检索指示文本当前行如何结束的换行条件 |
| BreakBefore | 检索指示文本当前行应在文本结束前如何换行的换行条件 |
| ContentEnd | 检索指向 TextBlock 控件中内容末尾的 TextPointer 控件 |
| ContentStart | 检索指向 TextBlock 控件中内容开头的 TextPointer 控件 |
| FontFamily | 获取或设置 TextBlock 控件的字体系列 |
| FontStretch | 确定 TextBlock 控件中字体应如何拉伸 |
| FontStyle | 获取或设置 TextBlock 控件的字体样式 |
| FontWeight | 获取或设置 TextBlock 控件的字体粗细 |
| Foreground | 获取或设置应用于 TextBlock 控件文本内容的颜色 |
| Inlines | 检索包含构成 TextBlock 控件内容的 Inline 元素的 InlineCollection 类 |
| IsHyphenationEnabled | 获取或设置一个值，该值指示是否启用或禁用单词的自动连字符 |
| LineStackingStrategy | 获取或设置用于确定 TextBlock 控件中每行文本的线框的机制 |
| Padding | 获取或设置一个值，该值指示内容区域边界与 TextBlock 控件显示的内容之间的厚度 |
| Text | 获取或设置 TextBlock 控件的文本内容 |
| TextAlignment | 获取或设置一个值，该值指示 TextBlock 控件中文本内容的水平对齐方式 |
| TextDecorations | 获取或设置包含要应用于 TextBlock 控件文本的效果的 TextDecorationCollection 控件 |
| TextEffects | 获取或设置要应用于 TextBlock 控件中文本内容的效果 |
| TextTrimming | 确定当内容溢出内容区域时文本如何被修剪 |
| TextWrapping | 确定 TextBlock 控件应如何换行文本 |

图 10.32 显示了添加到 WPF 应用程序中的 TextBlock 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_452_0.png)

### 注意

> Label 控件和 TextBlock 控件在大多数方面功能相同。两者之间的唯一区别在于这些控件可以显示的文本量。与 Label 控件相比，TextBlock 控件可以显示大量文本。

## ViewBox 控件

WPF 中的 ViewBox 控件表示一个内容装饰器，可以将单个子元素拉伸和缩放以填充 WPF 应用程序中 ViewBox 控件的可用空间。ViewBox 控件只能有一个子元素。在 ViewBox 控件中添加多个子元素可能会导致应用程序在运行时抛出 ArgumentException 异常。

ViewBox 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Decorator
              System.Windows.Controls.Viewbox
```

您可以使用以下代码片段将 ViewBox 控件添加到 WPF 应用程序中：

```
<Viewbox>
  <!--Child elements-->
</Viewbox>
```

### 表 10.46：ViewBox 类的注目属性

| 属性 | 描述 |
|---|---|
| Child | 获取或设置 Viewbox 控件的子控件 |
| Stretch | 获取或设置 Viewbox Stretch 模式，该模式确定内容如何在控件中适应 |
| StretchDirection | 获取或设置 StretchDirection 属性，该属性确定如何将缩放应用于控件的内容 |

图 10.33 显示了添加到 WPF 应用程序中的 ViewBox 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_453_0.png)

图 10.33：显示 ViewBox 控件

您将在本章的 Immediate Solutions 部分学习如何使用 ViewBox 控件。

## AccessText 控件

AccessText 控件表示用作访问键的下划线。例如，在 CTRL+C 中，C 是访问键。如果您的文本包含多个下划线，则只有第一个会被转换为访问键，其他下划线会作为普通文本出现。您可以通过在 ContentPresenter 控件中设置 RecognizeAccessKey 属性，将 AccessText 控件用作控件样式中的内容主机。

### 表 10.48：GridSplitter 类的属性

| 属性 | 描述 |
|---|---|
| DragIncrement | 检索或指定用户必须拖动鼠标的最小距离以使用 GridSplitter 控件调整行或列的大小 |
| KeyboardIncrement | 检索或指定 GridSplitter 控件每次按下箭头键时移动的距离 |
| PreviewStyle | 检索或指定自定义 GridSplitter 控件预览指示器的外观、效果或其他样式特征的样式，该指示器在 ShowsPreview 属性设置为 true 时显示。 |
| ResizeBehavior | 检索或指定相对于为其定义 GridSplitter 控件的列或行而调整大小的列或行 |
| ResizeDirection | 检索或指定一个值，该值指示 GridSplitter 控件调整行大小还是列大小 |
| ShowsPreview | 检索或指定一个值，该值指示 GridSplitter 控件是否在用户拖动控件时更新列或行大小 |

图 10.34 显示了添加到 WPF 应用程序中的 GridSplitter 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_455_0.png)

图 10.34：显示 GridSplitter 控件

## VirtualizingStackPanel 控件

在 WPF 中，您可以将数据绑定应用于容器控件。当您将项目绑定到 StackPanel 控件并且没有足够的空间显示所有项目时，可以使用 VirtualizingStackPanel 控件。该控件以单行水平或垂直排列内容。您只能在项目进行数据绑定时使用 VirtualizingStackPanel 控件。如果项目未进行数据绑定，该控件相对于 StackPanel 控件没有任何优势。VirtualizingStackPanel 控件的 IsVirtualizing 属性的默认值设置为 True。如果将该属性设置为 False，控件的行为类似于普通的 StackPanel 控件。

VirtualizingStackPanel 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Panel
              System.Windows.Controls.VirtualizingPanel
                System.Windows.Controls.VirtualizingStackPanel
```

您可以使用以下代码片段将 VirtualizingStackPanel 控件添加到 WPF 应用程序中：

```
<VirtualizingStackPanel>
<!--Child elements -->
</VirtualizingStackPanel>
```

### 表 10.49：VirtualizingStackPanel 类的注目属性

| 属性 | 描述 |
|---|---|
| CanHorizontallyScroll | 检索或指定一个值，该值指示 VirtualizingStackPanel 是否可以在水平维度上滚动 |
| CanVerticallyScroll | 检索或指定一个值，该值指示内容是否可以在垂直方向上滚动 |
| ExtentHeight | 检索包含范围垂直尺寸的值 |
| ExtentWidth | 检索包含范围水平尺寸的值 |
| HorizontalOffset | 检索包含已滚动内容的水平偏移量的值 |
| ScrollOwner | 检索或指定一个值，该值标识控制 VirtualizingStackPanel 控件中滚动行为的容器 |

VirtualizingStackPanel 控件无法从工具箱中添加。您必须通过 XAML 代码在应用程序中添加此控件。

## Calendar 控件

WPF 的 Calendar 控件类似于 Windows Forms 的 Calendar 控件。此控件允许您选择日期以及在选择日期时触发事件。您可以在另一个控件上显示所选日期或验证所选日期。您还可以使用其 Style 属性自定义 Calendar 控件的外观。Calendar 控件还可以帮助您执行各种任务，例如指定 Calendar 控件要显示的日期范围、选择特定日期范围或多个日期，以及禁用特定日期的选择。

Calendar 类的继承层次结构如下：

```
System.Object
System.Windows.Threading.DispatcherObject
System.Windows.DependencyObject
System.Windows.Media.Visual
System.Windows.UIElement
System.Windows.FrameworkElement
System.Windows.Controls.Control
System.Windows.Controls.Calendar
```

您可以使用以下代码片段将 Calendar 控件添加到 WPF 应用程序中：

```
<sdk:Calendar .../>
```

### 表 10.50：Calendar 类的注目属性

| 属性 | 描述 |
|---|---|
| BlackoutDates | 检索您不希望用户选择的日期集合 |
| DisplayDate | 检索或指定要在 Calendar 控件上显示的日期 |

