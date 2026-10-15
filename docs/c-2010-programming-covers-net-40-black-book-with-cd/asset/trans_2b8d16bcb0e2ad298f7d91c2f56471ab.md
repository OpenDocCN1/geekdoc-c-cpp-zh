
| 表12.1：GDI+的命名空间 |
| 命名空间 | 描述 |
| System.Drawing.Imaging | 包含提供高级图像处理功能的类 |
| System.Drawing.Printing | 包含协助打印的类 |
| System.Drawing.Design | 包含扩展设计时UI逻辑和绘图的类 |
| System.Drawing.Text | 包含提供高级GDI+排版功能的类 |

## 基本GDI+托管类

许多类与Graphics类协同工作以获得渲染效果。例如，DrawLine()方法接收一个Pen对象，该对象包含要绘制线条的属性。重要的GDI+托管类包括Graphics类、Pen类和Brush类。除了这些类，Windows Forms应用程序还定义了颜色结构，帮助您设计图形。让我们在以下章节中详细讨论所有这些内容。

## Graphics类

Windows Forms中的GDI+绘图由Graphics类表示，因为它提供了用于绘制对象的方法，如CreateGraphics()方法。它位于System.Drawing命名空间中，并且不能被继承。您可以使用FromImage()方法从图像创建Graphics对象。此外，您可以使用Graphics对象的不同方法绘制许多不同的形状和线条，例如DrawLine()、DrawArc()、DrawClosedCurve()、DrawPolygon()和DrawRectangle()。您还可以使用Graphics类的DrawImage()和DrawIcon()方法绘制图像。Graphics类的继承层次结构如下：

+   System.Object
+     System.MarshalByRefObject
+       System.Drawing.Graphics

Graphics类的值得注意的属性列于表12.2中：

| 表12.2：Graphics类的属性 |
| 属性 | 描述 |
| Clip | 获取或设置限定Graphics对象绘制区域的区域。 |
| ClipBounds | 检索限定Graphics对象剪辑区域的RectangleF结构。 |
| CompositingMode | 检索指定如何将合成图像绘制到Graphics对象上的值。合成图像是指将来自不同图像源的图像组合成单个图像，产生一种仿佛所有这些图像都是该单个图像的一部分的错觉。 |
| DpiX | 检索Graphics对象的水平分辨率。 |
| DpiY | 检索Graphics对象的垂直分辨率。 |
| InterpolationMode | 获取或设置与Graphics对象关联的插值模式。插值模式确定如何计算两个端点之间的中间值。 |
| IsClipEmpty | 检索一个值，该值指示Graphics对象的剪辑区域是否为空。 |
| IsVisibleClipEmpty | 检索一个值，该值指示Graphics对象的可见剪辑区域是否为空。 |
| PageScale | 获取或设置Graphics对象的世界单位与页面单位之间的缩放比例。 |
| PageUnit | 获取或设置Graphics对象中页面坐标使用的度量单位。该度量单位用于测量Windows Forms应用程序中Graphics对象的坐标。 |
| PixelOffsetMode | 获取或设置一个值，该值指定在Graphics对象渲染期间如何偏移像素。 |
| RenderingOrigin | 获取或设置Graphics对象用于抖动和阴影画笔的渲染原点。 |
| SmoothingMode | 获取或设置Graphics对象的渲染质量。 |
| TextContrast | 获取或设置用于渲染文本的伽马校正值。伽马校正值用于渲染ClearType文本。它必须在0到12之间，默认值为4。 |
| TextRenderingHint | 获取或设置与Graphics对象关联的文本的渲染模式。 |
| Transform | 获取或设置Graphics对象变换的副本。 |
| VisibleClipBounds | 检索Graphics对象剪辑区域范围的边界矩形。 |

Graphics类的值得注意的方法列于表12.3中：

| 表12.3：Graphics类的方法 |
| 方法 | 描述 |
| BeginContainer | 保存一个图形容器，其中包含Graphics对象的当前状态，并打开和使用一个新的图形容器 |
| Clear | 清除整个绘制表面，并用指定的背景色填充它 |
| CopyFromScreen | 执行从屏幕到Graphics对象绘制表面的颜色数据位块传输 |
| Dispose | 释放Graphics对象使用的所有资源 |
| DrawArc | 绘制表示椭圆一部分的弧 |
| DrawBezier | 绘制由四个点结构定义的贝塞尔曲线 |
| DrawBeziers | 绘制一系列贝塞尔曲线 |
| DrawClosedCurve | 绘制一条封闭的基数曲线 |
| DrawCurve | 绘制一条基数曲线 |
| DrawEllipse | 绘制由边界矩形定义的椭圆 |
| DrawIcon | 绘制由指定图标表示的图像 |
| DrawIconUnstretched | 绘制图像而不缩放图像 |
| DrawImageUnscaled | 在指定位置使用图像的原始物理尺寸绘制图像 |
| DrawImageUnscaledAndClipped | 绘制指定图像而不缩放，并裁剪以适合矩形 |
| DrawLine | 绘制一条连接由坐标对指定的两个点的线 |
| DrawLines | 绘制一系列连接点数组的线段 |
| DrawPath | 绘制一系列连接的线和曲线 |
| DrawPie | 绘制由椭圆定义的饼形 |
| DrawPolygon | 绘制由Point结构数组定义的多边形 |
| DrawRectangle | 绘制由坐标对、宽度和高度指定的矩形 |
| DrawRectangles | 绘制一系列由Rectangle结构定义的矩形 |
| DrawString | 在指定位置使用Brush和Font对象绘制文本字符串 |
| EndContainer | 关闭当前图形容器并恢复Graphics对象的状态 |
| Equals | 确定指定对象是否等于当前对象 |
| FillClosedCurve | 填充基数曲线的内部 |
| FillEllipse | 填充椭圆的内部 |
| FillPath | 填充GraphicsPath类的内部 |
| FillPie | 填充饼形部分的内部 |
| FillPolygon | 填充多边形的内部 |
| FillRectangle | 填充矩形的内部 |
| FillRectangles | 填充一系列矩形的内部 |
| FillRegion | 填充图形形状区域的内部 |
| Finalize | 使对象能够在销毁对象之前释放资源并执行清理操作 |
| Flush | 强制执行所有挂起的图形操作，并立即返回执行，而不等待操作完成 |
| FromHdc | 从指定点创建新的Graphics对象 |
| FromHdcInternal | 为特定设备上下文返回Graphics对象 |
| FromHwnd | 创建一个Graphics对象 |
| FromHwnd | 从指定的窗口句柄创建新的Graphics对象 |
| FromHwndInternal | 为窗口句柄创建新的Graphics对象 |
| FromImage | 从图像创建新的Graphics对象 |
| GetContextInfo | 检索累积的图形上下文 |
| IsVisible | 指示由坐标对指定的点是否包含在Graphics对象的可见剪辑区域内 |
| MeasureCharacterRanges | 检索区域对象数组 |
| MeasureString | 测量指定的字符串 |
| MultiplyTransform | 乘以Graphics对象的变换 |
| ResetTransform | 将Graphics对象的变换矩阵重置为单位矩阵 |
| Restore | 将图形状态恢复到GraphicsState类所表示的状态 |
| RotateTransform | 将指定的旋转应用于Graphics对象的变换矩阵 |
| Save | 保存Graphics对象的当前状态，并使用GraphicsState类标识已保存的状态 |
| ScaleTransform | 将指定的缩放操作应用于Graphics对象的变换矩阵 |
| SetClip | 将Graphics的剪辑区域设置为指定图形的Clip属性 |
| ToString | 返回表示Graphics类的String值 |
| TransformPoints | 将点数组从一个坐标空间变换到另一个坐标空间 |
| TranslateClip | 按水平和垂直方向上的指定量更改Graphics对象的剪辑区域 |
| TranslateTransform | 更改坐标系的原点 |
