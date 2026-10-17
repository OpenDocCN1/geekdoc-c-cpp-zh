
| `FontStyle` | 字体的样式。可以是 `Normal`（正常）、`Italic`（斜体）或 `Oblique`（倾斜，对于没有斜体样样的字体模拟斜体）。 |

# 表 A-2（续）

| 属性 | 用途 |
|---|---|
| `FontWeight` | 字体的“密度”。它可以是一个数字，或者是 `Thin`、`ExtraLight`、`Light`、`Normal`、`Medium`、`SemiBold`、`Bold`、`ExtraBold`、`Black` 或 `ExtraBlack` 中的值之一，尽管许多字体在这些许多值上的视觉效果是完全相同的。 |

## 绘图属性 (DRAWING PROPERTIES)

表 A-3 总结了决定图形对象外观的属性。

### 表 A-3

| 属性 | 用途 |
|---|---|
| `Fill` | 控件的背景颜色，通常用于圆形（`Ellipse`）和矩形（`Rectangle`）等绘制控件 |
| `Stroke` | 控件的前景色，通常用于圆形（`Ellipse`）和矩形（`Rectangle`）等绘制控件中的线条和曲线 |
| `StrokeDashArray` | 这是一个值数组，表示在制作虚线时绘制和跳过的线宽数量 |
| `StrokeDashCap` | 虚线段端点使用的样式。可以是 `Flat`（平直）、`Round`（圆角）、`Square`（方方形）或 `Triangle`（三角形）。 |
| `StrokeDashOffset` | 线条从其虚线模式中开始的距离 |
| `StrokeEndLineCap` | 线条结尾使用的样式。可以是 `Flat`（平直）、`Round`（圆角）、`Square`（方方形）或 `Triangle`（三角形）。 |
| `StrokeLineJoin` | 用于连接系列段之间拐处的样式，例如在多边形（`Polygon`）或折线形（`Polyline`）中。可以是 `Bevel`（斜角）、`Miter`（尖角）或 `Round`（圆角）。 |
| `StrokeMiterLimit` | 将进行斜角的最大尺寸。如果角太尖，则该角将变为斜角。 |
| `StrokeStartLineCap` | 线条起点使用的样式。可以是 `Flat`（平直）、`Round`（圆角）、`Square`（方方形）或 `Triangle`（三角形）。 |
| `StrokeThickness` | 绘制控件产生的线条和曲线的宽度 |

## 位图效果属性 (BITMAP EFFECT PROPERTIES)

表 A-4 总结了位图效果属性。

### 表 A-4

| 属性 | 用途 |
|---|---|
| `BevelBitmapEffect` | 给控件添加斜角边缘。 |
| `BlurBitmapEffect` | 使控件变得模糊。 |
| `DropShadowBitmapEffect` | 在控件后面添加阴影。 |
| `EmbossBitmapEffect` | 给控件浮雕外观。 |
| `OuterGlowBitmapEffect` | 在控件后面添加发光。 |

## 网格附加属性 (GRID ATTACHED PROPERTIES)

当你将控件放置在网格（`Grid`）内部时，可以使用由 `Grid` 定义的附加属性来确定控件的位置。表 A-5 总结了 `Grid` 附加属性。

### 表 A-5

| 属性 | 用途 |
|---|---|
| `Grid.Column` | 确定包含控件的列。 |
| `Grid.ColumnSpan` | 确定控件跨越的列数。 |
| `Grid.Row` | 确定包含控件的行。 |
| `Grid.RowSpan` | 确定控件跨越的行数。 |

使用 `Grid` 的 `Grid.ColumnDefinitions` 和 `Grid.RowDefinitions` 属性元素来定义网格的行和列的大小。

## 停靠面板附加属性 (DOCKPANEL ATTACHED PROPERTIES)

当你将控件放置在停靠面板（`DockPanel`）内部时，可以使用 `DockPanel.Dock` 附加属性来确定控件在 `DockPanel` 中的位置。该属性可以取 `Left`（左）、`Right`（右）、`Top`（上）和 `Bottom`（下）值。

例如，如果你将 `Label` 的 `DockPanel.Dock` 属性设置为 `Left`，那么 `Label` 将填充控件中剩余空间的左侧边缘。

如果 `DockPanel` 的 `LastChildFill` 属性为 `True`——默认情况下是如此——那么控件将使其最后一个子填充任何剩余空间。

## 画布附加属性 (CANVAS ATTACHED PROPERTIES)

当你将控件放置在画布（`Canvas`）内部时，可以使用由 `Canvas` 定义的附加属性来确定控件的位置。表 A-6 总结了 `Canvas` 附加属性。

### 表 A-6

| 属性 | 用途 |
|---|---|
| `Canvas.Bottom` | 确定控件底部边缘的位置。 |
| `Canvas.Left` | 确定控件左侧边缘的位置。 |
| `Canvas.Right` | 确定控件右侧边缘的位置。 |
| `Canvas.Top` | 确定控件顶部边缘的位置。 |
