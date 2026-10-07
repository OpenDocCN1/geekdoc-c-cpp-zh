
在前面的代码段中，`repaint()`方法调用`update()`方法，最后由`update()`方法调用`paint()`方法来重绘 applet 窗口。让我们在 applet 中实现多线程。

- 每个 applet 可以在多个线程中运行。许多 Web 浏览器为页面上的每个 applet 分配一个线程。执行相同任务的 applet 应该在一个带有`while`或`do`循环的线程下。为此，你将这些重复任务放在线程的`run()`方法中，并使用 applet 的`stop()`方法来停止线程。多线程的一个示例是定期间隔执行`repaint()`方法的 applet。列表 14 显示了`AppletThread.java`文件，它解释了如何在 applet 中实现多线程（你可以在光盘的（Chapter9 文件夹）中找到`AppletThread.java`文件）：

- **Listing 14**: *使用 Applet 实现多线程*

# 第 9 章

## 表 23：Graphics 类方法讨论

| 方法 | 描述 |
| :--- | :--- |
| `abstract void dispose()` | 释放图形上下文。 |
| `void draw3DRect(int x, int y, int width, boolean raised)` | 绘制矩形的 3D 高亮凸起轮廓。 |
| `abstract void drawArc(int x, int y, int width, int height, int intAngle)` | 绘制圆形或椭圆弧。 |
| `void drawBytes(byte[] data, int offset, int length, int x, int y)` | 绘制字节数组提供的文本。 |
| `void drawChars(char[] data, int offset, int length, int x, int y)` | 绘制字符数组提供的文本。 |
| `abstract boolean drawImage(Image img, int x, int y, Color color, ImageObserver observer)` | 使用指定的 img, x, y, bgcolor 和 observer 参数绘制图像。 |
| `abstract boolean drawImage(Image img, int x, int y, int width, int height, Color color, ImageObserver observer)` | 使用指定的 img, x, y 和 bgcolor 参数绘制图像。 |
| `abstract void drawLine(int x1, int y1, int x2, int y2)` | 使用当前颜色在点 (x1, y1) 和 (x2, y2) 之间绘制一条线。 |
| `abstract void drawOval(int x, int y, int width, int height)` | 绘制椭圆。 |
| `abstract void drawPolygon(int[] points)` | 绘制闭合多边形。 |
| `void drawPolygon(int[] points, int x, int y)` | 绘制 Polygon 对象定义的多边形轮廓。 |
| `abstract void drawPolyline(int[] points, int x, int y)` | 绘制 x 和 y 坐标数组定义的一系列连接线。 |
| `void drawRect(int x, int y, int width, int height)` | 绘制矩形。 |
| `abstract void drawRoundRect(int x, int y, int width, int height, int arcWidth)` | 绘制圆角矩形。 |
| `abstract void drawString(AttributedCharacterIterator iterator, int x, int y)` | 绘制 AttributedCharacterIterator 提供的文本。 |
| `abstract void drawString(String str, int x, int y)` | 绘制文本字符串。 |
| `void fill3DRect(int x, int y, int width, int height, boolean rounded)` | 使用当前颜色绘制 3D 高亮矩形。 |
| `abstract void fillArc(int x, int y, int width, int height, int startAngle, int arcAngle)` | 使用给定的矩形填充圆形或椭圆弧。 |
| `abstract void fillOval(int x, int y, int width, int height)` | 使用给定的矩形填充椭圆。 |
| `abstract void fillPolygon(int[] xPoints, int[] yPoints)` | 填充 x 和 y 坐标数组定义的闭合多边形。 |
| `void fillPolygon(Polygon p)` | 填充由给定 Polygon 类定义的多边形。 |
| `abstract void fillRect(int x, int y, int width, int height)` | 填充给定的矩形。 |
| `abstract void fillRoundedRect(int x, int y, int width, int height, int arcWidth, int arcHeight)` | 填充圆角矩形。 |
| `void finalize()` | 处理图形上下文的垃圾回收。 |
| `abstract Shape getClip()` | 获取任意形状的裁剪区域。 |
| `abstract Rectangle getBounds()` | 获取任意形状的边界矩形。 |
| `Rectangle getClipBounds(Rectangle r)` | 获取带有 r 裁剪参数的边界矩形区域。 |
| `abstract Color getColor()` | 获取图形上下文的当前颜色。 |
| `abstract Font getFont()` | 获取字体。 |
| `FontMetrics getMetrics()` | 获取字体的度量。 |
| `abstract FontMetrics getMetrics(Font f)` | 获取字体度量。 |
| `boolean hitClip(int x, int y, int width, int height)` | 如果矩形区域与裁剪区域的矩形相交则返回 true。 |
| `abstract void setClip(int x, int y, int width, int height)` | 设置由传递参数坐标形成的裁剪形状。 |
| `abstract void setClip(Shape clip)` | 将裁剪区域设置为 Shape 接口对象（clip）指定的任意形状。 |
| `abstract void setColor(Color c)` | 将此图形上下文的颜色设置为给定颜色。 |
| `abstract void setFont(Font font)` | 将此图形上下文的字体设置为 font。 |
| `abstract void setPaintMode()` | 使用当前颜色设置图形上下文的绘制模式。 |
| `abstract void setXORMode(Color c1)` | 使用 XOR 操作将绘制模式设置为切换图形上下文当前颜色和给定颜色。 |
| `abstract void draw(int x, int y)` | 使用指定的点 (x,y) 平移图形上下文的原点。 |

你可以使用表 23 中列出的方法来绘制形状，如线、矩形、椭圆、弧和多边形，并获取应用程序当前的字体和颜色。

在下一节中，我们将绘制以下形状：
- 线
- 矩形
- 椭圆
- 弧
- 多边形

我们将在接下来的小节中逐一讨论。

### 绘制线条

`Graphics`类的`drawLine`方法用于绘制线条。你可以在点`(x1, y1)`和`(x2, y2)`之间绘制一条线。使用`drawLine`的语法如下：

```java
drawLine(int x1, int y1, int x2, int y2)
```

（注：此处原文示例内容与方法名不符，已按方法逻辑修正翻译）

### 绘制矩形

`drawRect`方法用于绘制矩形。使用其语法如下：

```java
drawRect(int x, int y, int width, int height)
```

### 绘制椭圆

`drawOval`方法用于绘制椭圆。使用其语法如下：

```java
drawOval(int x, int y, int width, int height)
```

### 绘制弧

`drawArc`方法用于绘制弧。使用其语法如下：

```java
drawArc(int x, int y, int width, int height, int startAngle, int arcAngle)
```

在列表 19 中，`Graphics`类的对象`(g)`调用了`drawArc()`方法，绘制绘制了一个从坐标 200,80 开始到 80,80 结束的弧。该弧的起始角度和结束角度分别为 0 度和 180 度。图 2.1 显示了列表 19 的输出：

![](img/d3faa73f55d3d314bb5bfb277886900d_373_0.png)

**图 21：使用 drawArc() 方法绘制弧**

### 绘制多边形

`Graphics`类的`drawPolygon()`方法用于绘制任意形状。它被用于绘制具有 n 条边的多边形，其中 n 是多边形的边数。使用`drawPolygon()`方法的语法如下：

```java
void drawPolygon(int xpoints[], int ypoints[], int numPoints);
```

在这里，`drawPolygon()`方法绘制的多边形的起始位置和结束位置由`xPoints`和`yPoints`数组包含的坐标对指定。`xPoints`或`yPoints`数组中定义的元素数量等于`numPoints`变量的值。列表 20 显示了在`DrawPolygon.java`文件中使用`drawPolygon()`方法的方法（你可以在 Code/Chapter9 文件夹找到 DrawPolygon.java 文件）：

- 列表 20：DrawPolygon.java 文件

```java
import java.awt.*;

import java.awt.*;

/* <applet code="DrawPolygon.class" width=250 height=250>

</applet> */

public class DrawPolygon extends Applet
{
    public void paint(Graphics g)
    {
        int xpoints[] = {25, 75, 125, 85, 125, 75, 25, 65};
        int ypoints[] = {50, 90, 100, 150, 110, 150, 100};
        int num = 8;
        g.drawPolygon(xpoints, ypoints, num);
    }
}
```

在列表 20 中，`DrawPolygon` applet 调用了`drawPolygon()`方法，绘制了一个 8 边的多边形。图 22 显示了在 applet 上绘制的多边形形状：

![](img/d3faa73f55d3d314bb5bfb277886900d_374_0.png)

**图 22：使用 drawPolygon() 方法绘制多边形**

现在，你已经知道如何绘制矩形、椭圆和其他形状。让我们来看看如何如何在这些形状中填充颜色。

### 9.7 使用 Color 类

`java.Color`类用于创建新颜色，或使用某些预定义的颜色常量，如 applet 或独立应用程序中的红色、绿色。Java 允许我们创建最多 24 种不同的颜色。表 24 列出了 Color 类的字段：

| 表 24：讨论 Color 类的字段 |
| :--- | :--- | :--- |
| static Color black | static Color blue | static Color cyan |
| static Color darkGray | static Color gray | static Color green |
| static Color lightGray | static Color magenta | static Color orange |
| static Color pink | static Color red | static Color white |

表 24 中提供的字段用于设置 applet 的颜色或获取其当前颜色。表 25 列出了 Color 类的构造函数：

| 表 25：描述 Color 类的构造函数 |
| 构造函数 | 描述 |
| :--- | :--- |
| Color(ColorSpace cspace, float[]) | 帮助在给定 ColorSpace 的颜色空间中创建颜色。 |
| Color(float r, float g, float b) | 帮助在 0.0 到 1.0 的范围内使用给定的红色、绿色和蓝色值创建不透明颜色。 |
| Color(float r, float g, float b, float a) | 帮助在 0.0 到 | 使用给定的红色、绿色、蓝色和 alpha 值创建颜色。 |

# 第 9 章

| 表 25：描述 Color 类的构造函数 |
| 构造函数 | 描述 |
| :--- | :--- |
| Color(int rgb) | 1.0 帮助使用给定的组合 RGB 值创建不透明颜色，该值由位 16 到 23 的红色值、位 8 到 15 的绿色值以及位 0 到 7 的蓝色值组成。 |
| Color(int rgba, boolean hasalpha) | 帮助使用给定的 RGB 值创建颜色，该值由位 24 到 31 的 alpha 值、位 16 到 23 的红色值、位 8 到 15 的绿色值以及位 0 到 7 的蓝色值组成。 |
| Color(int r, int g, int b) | 帮助在 0 到 255 的范围内使用给定的红色、绿色和蓝色值创建不透明颜色。 |
| Color(int r, int g, int b, int a) | 帮助在 0 到 255 的范围内使用给定的红色、绿色、蓝色和 alpha 值创建颜色。 |

表 26 列出了 Color 类的方法：

| 表 26：讨论 Color 类的方法 |
| 方法 | 描述 |
| :--- | :--- |
| brighter() | 返回颜色的更亮版本。 |
| darker() | 返回颜色的更深版本。 |
| equals(Object obj) | 检查两个颜色是否相等。 |
| getAlpha() | 获取 0.0 到 1.0 之间的 alpha 值。 |
| getBlue() | 获取 0 到 255 之间的蓝色值。 |
| getRed() | 获取 0 到 255 之间的红色值。 |
| hashCode() | 返回颜色的哈希码。 |
| toString() | 返回颜色的字符串表示。 |

| 表 26：讨论 Color 类的方法 |
| 方法 | 描述 |
| :--- | :--- |
| brighter() | 返回颜色的更亮版本。 |
| darker() | 返回颜色的更深版本。 |
| equals(Object) | 检查两个颜色是否相等。 |
| getAlpha() | 获取 0.0 到 1.0 之间的 alpha 值。 |
| getBlue() | 获取 0 到 255 之间的蓝色值。 |
| getRed() | 获取 0 到 255 之间的红色值。 |
| hashCode() | 返回颜色的哈希码。 |
| toString() | 返回颜色的字符串表示。 |

*(注：由于原文文本中表格部分存在重复和错乱，翻译时已根据逻辑进行了对齐处理)*

### 与 GUI 工作

要创建一个新颜色，你需要传递 Color 类的 red, green, blue 作为参数。以下代码片段显示了如何创建：

```java
Color c = new Color(red, green, blue);
```

现在，使用`setForeground(c)`来设置此新颜色，如下：

```java
setForeground(c);
```

现在，你也可以像这样设置背景颜色`Color.blue`：

```java
setBackground(Color.blue);
```

事实上，你还可以使用 Graphics 方法（如`fillArc()`和`fillOval()`）填充颜色。列表 21 显示了 ColorShow.java 文件，解释了如何在 applet 中使用颜色（你可以在 Code/Chapter9 找到 ColorShow.java 文件）：

#### 列表 21：ColorShow.java 文件

```java
import java.awt.*;

import java.awt.*;

/* <applet code="ColorShow" width=300 height=200>

</applet> */

public class ColorShow extends Applet
{
