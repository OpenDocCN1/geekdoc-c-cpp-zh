
| java.awt.Graphics2D 1.2 |
| --- |
| - `void clip(Shape s)`<br>将当前裁剪形状与形状 s 相交。<br>- `FontRenderContext getFontRenderContext()`<br>返回构造 `TextLayout` 对象所必需的字体渲染上下文。 |

| java.awt.font.TextLayout 1.2 |
| --- |
| - `TextLayout(String s, Font f, FontRenderContext context)`<br>根据给定字符串和字体构造文本布局对象，并使用字体渲染上下文获取特定设备的字体属性。<br>- `float getAdvance()`<br>返回此文本布局的宽度。<br>- `float getAscent()`<br>- `float getDescent()`<br>返回此文本布局在基线上方和下方的高度。<br>- `float getLeading()`<br>返回此文本布局所用字体中相邻行之间的距离。 |

## 11.8 透明度与合成

在标准 RGB 颜色模型中，每种颜色由其红、绿、蓝分量描述。然而，描述图像中*透明*或部分透明的区域也很方便。当你将一幅图像叠加到现有绘图上时，透明像素完全不会遮挡其下方的像素，而部分透明像素则会与其下方的像素混合。图 11.21 展示了将部分透明矩形叠加到图像上的效果。你仍然可以看到图像细节从矩形下方透出来。

在 Java 2D API 中，透明度由 *alpha 通道* 描述。每个像素除了红、绿、蓝颜色分量外，还有一个介于 0（完全透明）和 1（完全不透明）之间的 alpha 值。例如，图 11.21 中的矩形填充了 50% 透明度的淡黄色：

```java
new Color(0.7F, 0.7F, 0.0F, 0.5F);
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_828_0.png)

**图 11.21** 将部分透明的矩形叠加到图像上

现在让我们看看叠加两个形状时会发生什么。你需要混合或*合成*源像素和目标像素的颜色与 alpha 值。计算机图形学领域的两位研究人员 Porter 和 Duff 为这一混合过程制定了 12 种可能的*合成规则*。Java 2D API 实现了所有这些规则。在进一步讨论之前，我们要指出，这些规则中只有两条具有实际意义。如果你觉得这些规则晦涩难懂，只需使用 `SRC_OVER` 规则即可。它是 `Graphics2D` 对象的默认规则，并且能给出最直观的结果。

下面是这些规则背后的理论。假设你有一个 alpha 值为 α<sub>S</sub> 的*源像素*。图像中已经有一个 alpha 值为 α<sub>D</sub> 的*目标像素*。你想将二者合成。图 11.22 中的图示展示了如何设计合成规则。

![](img/7dd923a566750151a3aab0dacd0cdaa5_828_1.png)

**图 11.22** 设计合成规则

Porter 和 Duff 将 alpha 值视为应使用该像素颜色的概率。从源的角度看，它希望使用源颜色的概率为 α<sub>S</sub>，而不在意的概率为 1 - α<sub>S</sub>。目标也是如此。在合成颜色时，我们假设这些概率是独立的。于是有四种情况，如图 11.22 所示。如果源希望使用源颜色而目标不在意，那么让源按自己的意愿处理似乎是合理的。这就是图中右上角标为“S”的原因。该事件的概率为 α<sub>S</sub> · (1 - α<sub>D</sub>)。类似地，左下角标为“D”。如果目标和源都希望选择自己的颜色，该怎么办？这正是 Porter-Duff 规则的用武之地。如果我们决定源更重要，就把右下角也标为“S”。该规则称为 SRC_OVER。在该规则中，你以权重 α<sub>S</sub> 组合源颜色，并以权重 (1 - α<sub>S</sub>) · α<sub>D</sub> 组合目标颜色。

视觉效果是源与目标的混合，其中优先考虑源。特别地，如果 α<sub>S</sub> 为 1，则完全不考虑目标颜色。如果 α<sub>S</sub> 为 0，则源像素完全透明，目标颜色保持不变。

其他规则取决于你在概率图的方框中填入哪些字母。表 11.1 和图 11.23 展示了 Java 2D API 支持的所有规则。图中的图像展示了将 alpha 为 0.75 的矩形源区域与 alpha 为 1.0 的椭圆形目标区域组合时各规则的结果。

如你所见，大多数规则并不是很有用。以 DST_IN 规则作为一个极端例子来考虑。它完全不考虑源颜色，但使用源的 alpha 来影响目标。SRC 规则可能有用——它强制使用源颜色，关闭与目标的混合。

有关 Porter-Duff 规则的更多信息，例如可参阅 James D. Foley、Andries van Dam、Steven K. Feiner 等人所著的 *Computer Graphics: Principles and Practice, Second Edition in C*。

使用 `Graphics2D` 类的 `setComposite` 方法安装一个实现 `Composite` 接口的类的对象。Java 2D API 提供了这样一个类 `AlphaComposite`，它实现了图 11.23 中的所有 Porter-Duff 规则。

`AlphaComposite` 类的工厂方法 `getInstance` 会生成一个 `AlphaComposite` 对象。你需要提供规则以及用于源像素的 alpha 值。例如，考虑以下代码：

**表 11.1 Porter–Duff 合成规则**

| 规则 | 说明 |
| --- | --- |
| CLEAR | 源清除目标。 |
| SRC | 源覆盖目标和空像素。 |
| DST | 源不影响目标。 |
| SRC_OVER | 源与目标混合，并覆盖空像素。 |
| DST_OVER | 源不影响目标，并覆盖空像素。 |
| SRC_IN | 源覆盖目标。 |
| SRC_OUT | 源清除目标，并覆盖空像素。 |
| DST_IN | 源 alpha 修改目标。 |
| DST_OUT | 源 alpha 补值修改目标。 |
| SRC_ATOP | 源与目标混合。 |
| DST_ATOP | 源 alpha 修改目标。源覆盖空像素。 |
| XOR | 源 alpha 补值修改目标。源覆盖空像素。 |

```java
int rule = AlphaComposite.SRC_OVER;
float alpha = 0.5f;
g2.setComposite(AlphaComposite.getInstance(rule, alpha));
g2.setPaint(Color.blue);
g2.fill(rectangle);
```

然后该矩形会以蓝色和 0.5 的 alpha 值绘制。由于合成规则是 SRC_OVER，它会透明地叠加到现有图像上。

清单 11.3 中的程序让你可以探索这些合成规则。从组合框中选择一条规则，并使用滑块设置 AlphaComposite 对象的 alpha 值。

此外，程序会显示每条规则的文字描述。请注意，这些描述是根据合成规则图计算出来的。例如，第二行中的“DS”表示“与目标混合”。

该程序有一个重要的特殊之处。不能保证与屏幕对应的图形上下文具有 alpha 通道。（事实上，它通常没有。）当像素被放置到没有 alpha 通道的目标上时，像素颜色会与 alpha 值相乘，而 alpha 值则

![](img/7dd923a566750151a3aab0dacd0cdaa5_832_0.png)

**图 11.24** CompositeTest 程序

### 清单 11.3 composite/CompositeTestFrame.java

```java
package composite;

import java.awt.*;

import javax.swing.*;

/**
 * This frame contains a combo box to choose a composition rule, a slider to change the source
 * alpha channel, and a component that shows the composition.
 */
class CompositeTestFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 400;
    private static final int DEFAULT_HEIGHT = 400;
```
