

### java.awt.Graphics2D 1.2

- `void clip(Shape s)` — 将当前裁剪形状与形状 s 相交。
- `FontRenderContext getFontRenderContext()` — 返回字体渲染上下文，该上下文是构造 TextLayout 对象所必需的。

### java.awt.font.TextLayout 1.2

- `TextLayout(String s, Font f, FontRenderContext context)` — 根据给定的字符串和字体构造文本布局对象，并使用字体渲染上下文来获取特定设备的字体属性。
- `float getAdvance()` — 返回此文本布局的宽度。
- `float getAscent()` / `float getDescent()` — 返回此文本布局在基线上方和下方的高度。
- `float getLeading()` — 返回此文本布局所用字体中连续行之间的距离。

### 11.3.8 透明与合成

在标准 RGB 颜色模型中，每种颜色都由其红色、绿色和蓝色分量描述。然而，描述图像中*透明*或*部分透明*的区域也很方便。当你将图像叠加到现有绘图上时，透明像素完全不会遮挡其下的像素，而部分透明的像素则会与其下的像素混合。图 11.51 显示了将部分透明的矩形叠加到图像上的效果。你仍然可以从矩形下方看到图像的细节。

在 Java 2D API 中，透明度由*alpha 通道*描述。每个像素除了红色、绿色和蓝色颜色分量外，还有一个介于 0（完全透明）和 1（完全不透明）之间的 alpha 值。例如，图 11.51 中的矩形填充的是具有 50% 透明度的淡黄色：

```java
new Color(0.7f, 0.7f, 0.0f, 0.5f);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_758_0.png)

**图 11.51** 将部分透明的矩形叠加到图像上

现在让我们看看如果叠加两个形状会发生什么。你需要混合或**合成**源像素和目标像素的颜色与 alpha 值。计算机图形学领域的两位研究人员 Porter 和 Duff 为这种混合过程制定了 12 种可能的*合成规则*。Java 2D API 实现了所有这些规则。在进一步讨论之前，我们想指出，其中只有两个规则具有实际意义。如果你觉得这些规则晦涩难懂或令人困惑，只需使用 `SRC_OVER` 规则。它是 `Graphics2D` 对象的默认规则，并且能给出最直观的结果。

以下是这些规则背后的理论。假设你有一个 alpha 值为 α_S 的*源*像素。在图像中，已经有一个 alpha 值为 α_D 的*目标*像素。你想要合成这两者。图 11.52 中的图示展示了如何设计一条合成规则。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_758_1.png)

**图 11.52** 设计合成规则

Porter 和 Duff 将 alpha 值视为像素颜色应被使用的概率。从源的角度来看，它使用源颜色的概率为 α_S，不关心的概率为 1 − α_S。目标也是如此。在合成颜色时，让我们假设这些概率是独立的。那么有四种情况，如图 11.52 所示。如果源想使用源颜色而目标不关心，那么让源如愿似乎是合理的。这就是图中右上角标记为“S”的原因。该事件的概率是 α_S · (1 − α_D)。类似地，左下角标记为“D”。如果目标和源都想选择自己的颜色，该怎么办？这就是 Porter–Duff 规则发挥作用的地方。如果我们决定源更重要，我们也将右下角标记为“S”。该规则称为 SRC_OVER。在该规则中，你将源颜色与权重 α_S 相结合，将目标颜色与权重 (1 − α_S) · α_D 相结合。

视觉效果是源与目标的混合，并优先考虑源。特别是，如果 α_S 为 1，则完全不考虑目标颜色。如果 α_S 为 0，则源像素完全透明，目标颜色不变。

其他规则取决于你在概率图的方框中放入哪些字母。表 11.3 和图 11.53 展示了 Java 2D API 支持的所有规则。图中的图像显示了当一个 alpha 为 0.75 的矩形源区域与一个 alpha 为 1.0 的椭圆形目标区域组合时的规则结果。

**表 11.3 Porter–Duff 合成规则**

| 规则 | 说明 |
|---|---|
| CLEAR | 源清除目标。 |
| SRC | 源覆盖目标和空像素。 |
| DST | 源不影响目标。 |
| SRC_OVER | 源与目标混合并覆盖空像素。 |
| DST_OVER | 源不影响目标并覆盖空像素。 |
| SRC_IN | 源覆盖目标。 |
| SRC_OUT | 源清除目标并覆盖空像素。 |
| DST_IN | 源 alpha 修改目标。 |
| DST_OUT | 源 alpha 补数修改目标。 |
| SRC_ATOP | 源与目标混合。 |
| DST_ATOP | 源 alpha 修改目标。源覆盖空像素。 |
| XOR | 源 alpha 补数修改目标。源覆盖空像素。 |

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_760_0.png)

**图 11.53** Porter–Duff 合成规则

正如你所看到的，大多数规则并不是很有用。考虑一个极端的例子：`DST_IN` 规则。它完全不考虑源颜色，而是使用源的 alpha 来影响目标。`SRC` 规则可能很有用——它强制使用源颜色，关闭与目标的混合。

关于 Porter–Duff 规则的更多信息，请参阅 James D. Foley、Andries van Dam、Steven K. Feiner 等人所著的 *Computer Graphics: Principles and Practice, Second Edition in C*。

使用 `Graphics2D` 类的 `setComposite` 方法来安装一个实现了 `Composite` 接口的类的对象。Java 2D API 提供了一个这样的类 `AlphaComposite`，它实现了图 11.53 中的所有 Porter–Duff 规则。

`AlphaComposite` 类的工厂方法 `getInstance` 生成一个 `AlphaComposite` 对象。你需要提供规则和用于源像素的 alpha 值。例如，考虑以下代码：

```java
int rule = AlphaComposite.SRC_OVER;
float alpha = 0.5f;
g2.setComposite(AlphaComposite.getInstance(rule, alpha));
g2.setPaint(Color.blue);
g2.fill(rectangle);
```

然后矩形被绘制为蓝色且 alpha 值为 0.5。由于合成规则是 `SRC_OVER`，它会以透明方式叠加在现有图像上。

清单 11.17 中的程序让你探索这些合成规则。从组合框中选择一个规则，并使用滑块设置 `AlphaComposite` 对象的 alpha 值。

此外，该程序会显示每条规则的文字描述。请注意，这些描述是根据合成规则图计算得出的。例如，第二行中的“DS”代表“与目标混合”。

该程序有一个重要的转折。与屏幕对应的图形上下文不保证具有 alpha 通道。（事实上，通常没有。）当像素被放置到没有 alpha 通道的目标上时，像素颜色会乘以 alpha 值，然后 alpha 值被丢弃。现在，几条 Porter–Duff 规则会使用目标的 alpha 值，这意味着目标 alpha 通道很重要。因此，我们使用具有 ARGB 颜色模型的缓冲图像来合成形状。合成图像后，我们再将结果图像绘制到屏幕。

```java
var image = new BufferedImage(getWidth(), getHeight(), BufferedImage.TYPE_INT_ARGB);
Graphics2D gImage = image.createGraphics();
// now draw to image
g2.drawImage(image, null, 0, 0);
```

清单 11.17 和 11.18 展示了框架和组件类。清单 11.19 中的 Rule 类提供了每条规则的简要说明——参见图 11.54。运行该程序时，将 alpha 滑块从左向右移动，观察对合成形状的影响。特别是要注意，`DST_IN` 和 `DST_OUT` 规则之间的唯一区别是当你改变源 alpha 时目标（！）颜色如何变化。

