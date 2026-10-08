

三维图表坐标系增加了 Z 坐标（X, Y, Z）。它是图表区域深度的百分比。图表区域的后墙 Z 值为 0，图表区域的前端 Z 值为 100。

![](img/b5597c749e848b27b0d305153ae16106_662_0.png)

# 图表元素的观

在图表中，你可以使用外观属性自定义所有图表元素的观。每个图表元素都包含丰富的外观属性，这使你能够以细粒度控制图表的外观。了解如何控制元素的最佳方法是查看属性窗口中的“外观”库（Appearance gallery）。表 14-4 描述了可用于大多数线型元素的属性。

表 14-4：影响线型元素外观的属性

| 属性 | 描述 |
| --- | --- |
| LineColor, BorderRadius | 获取或设置线条（边框）的颜色。 |
| LineDashStyle, BorderDashStyle | 获取或设置线条（边框）的样式。 |
| LineWidth, BorderRadius | 获取或设置线条（边框）宽度。 |
| StartCap | 获取或设置线条起始端端点的样式。 |
| EndCap | 获取或设置线条结束端端点的样式。 |
| ShadowColor | 获取或设置线条阴影的颜色。 |
| ShadowOffset | 获取或设置线条阴影的大小。 |

图 14-41：设置 IsClustered 为 false 的三维渲染图表

表 14-5 总结了可用于表面（surfaces）的属性，包括数据点、标记和注释。当然，如果表面具有线条或边框，它们也具有表 14-4 所示的属性。

表 14-5：决定线型元素观的属性

| 属性 | 描述 |
| --- | --- |
| BackGradientStyle | 获取或设置背景渐变样式。 |
| BackHatchStyle | 获取或设置背景填充样式。 |
| BackImage | 获取或设置背景图像。 |
| BackImageAlignment | 获取或设置背景图片的对齐方式，常用于未缩放绘制模式（Unscaled drawing mode）。 |

# 表 14-5（续）

| 属性 | 描述 |
| --- | --- |
| BackImageTransparentColor | 获取或设置一种在绘制背景图像时将被替换为透明色的颜色。 |
| BackImageWrapMode | 获取或设置背景的绘制模式。 |
| BackSecondaryColor | 获取或设置次要背景颜色。当背景使用渐变样式时使用此属性。 |

你可以使用表 14-6 总结的额外属性控制文本元素。

# 表 14-6：控制文本元素观的属性

| 属性 | 描述 |
| --- | --- |
| Font | 获取或设置文本字体。 |
| ForeColor | 获取或设置文本元素的颜色。 |
| Shadow | 获取或设置阴影的颜色。此属性可以设置为任何有效的 ARGB（Alpha、红、绿、蓝）值。Alpha 值可以用于实现“真实”的阴影效果。 |
| ShadowOffset | 获取或设置文本的像素为单位的阴影偏移量。 |
| TextOrientation | 获取或设置文本的方向。 |
| TextStyle | 获取或设置文本的样式。五种可能的样式为 TextStyle.Default、TextStyle.Shadow、TextStyle.Emboss、TextStyle.Embed 和 TextStyle.Frame。 |

还有许多其他决定图表元素观的属性。大多数属性会在你设置或更改它们时在设计视图中刷新。有时，发现它们作用的最简单方法是在设计模式下尝试它们。如果你不确定它们是什么，将光标置于属性窗口中的特定属性上并按 F1 获取帮助。

与其单独设置颜色，可以使用定义了一组颜色的 Palette（调色板）对象。Chart.Palette 属性定义了用于系列和数据点的默认颜色。Series.Palette 属性同样定义了用于其数据点的默认颜色。使用这些属性为你的系列和数据点提供特定的观。为 Chart 控件自定义调色板，请使用 Chart.PaletteCustomColors。此属性优先级高于 Chart.Palette。使用 Series.PaletteCustomColors 属性指定自定义调色板。

Chart 控件可以使用抗锯齿技术平滑尖锐的颜色边界。这使得图表图像更符合视觉审美。要查看此效果，将 Chart.AntiAliasing 属性设置为 AntiAliasingStyles.Text、AntiAliasingStyles.Graphics 或 AntiAliasingStyles.All。

当为任何图表元素显示阴影时，你还可以通过将 Chart.IsSoftShadows 属性设置为 True 来平滑阴影。

图 14-42 显示了缩放倍数为二时的抗锯齿效果。

![](img/b5597c749e848b27b0d305153ae16106_664_0.png)

图 14-42：文本和图形中使用抗锯齿

图片的顶部关闭了抗锯齿选项，而底部开启了它们。

# 轴及相关图表元素

你可以自定义属于图表的轴的外观和行为。ChartArea 实例包含一个名为 Axes 的属性，它是 Axis 的一个数组。Axes 的定义表明你可以读写此属性，但你应该将其作为只读使用。你可以使用 AxisName 枚举对 Axes 元素进行索引，其值总结在表 14-7 中。

表 14-7：AxisName 枚举的值

| 值 | 描述 | 柱状图和堆叠图中的位置 | 其他图表 |
| --- | --- | --- | --- |
| X | 主 X 轴 | 左侧垂直轴 | 底部水平轴 |
| Y | 主 Y 轴 | 底部水平轴 | 左侧垂直轴 |
| X1 | 次级 X 轴 | 右侧垂直轴 | 顶部水平轴 |
| Y1 | 次级 Y 轴 | 顶部水平轴 | 右侧垂直轴 |

某些图表（极坐标、饼、环形和雷达图）使用了类似极坐标的轴。当然，它们的轴与表 14-6 所示的不同。

轴 可以使用几十个属性进行自定义。表 14-8 描述了最常用的属性。

表 14-8：轴属性

| 属性 | 描述 |
| --- | --- |
| ArrowStyle | 获取或设置二维轴的箭头样式。此样式不应用于三维图表区域。可能的样式由 AxisArrowStyle 枚举定义（None、Triangle、Lines）。 |
| InterlacedColor | 获取或设置交替条带的颜色。 |
| IsInterlaced | 获取或设置一个标志，决定轴是否显示交替条带。 |
| StripLines | 获取一个 StripLinesCollection 对象，该对象包含轴的条带。条带用于跨 ChartArea 绘制矩形，并始终跨整个区域。 |
| MajorGrid | 获取或设置一个 Grid 对象用于设置轴的网格线属性。主网格线始终与数据点作为数据一起绘制，即对于分类轴刻标记。对于值轴，主网格线默认在标签出现的地方绘制。 |
| MajorTickMark | 获取或设置一个 TickMark 对象用于设置轴的刻标记属性。主标记始终与数据点作为数据一起绘制。分类轴刻标记出现在轴上与数据点相同的位置。对于值轴，主标记默认在标签出现的地方绘制。 |
| MinorGrid | 获取或设置一个 Grid 对象用于指定轴的小要网格线属性。小要网格线在主网格线之间。 |
| MinorTickMark | 获取或设置一个 TickMark 对象用于设置轴的小要刻标记属性。 |
| Interval | 获取或设置轴的间隔。此属性决定了与轴相关的标签、主刻标记和网格线的绘制方式。 |
| IntervalAutoMode | 获取或设置一个标志，决定轴上使用固定数量的间隔，还是间隔数量取决于轴的大小。你可以使用 IntervalAutoMode 枚举的值（FixedCount、VariableCount）。 |

