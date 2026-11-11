
上下文将按照与你提供这些变换时相反的顺序应用它们——也就是说，你最后提供的变换会最先被应用。

你可以提供任意多个变换。例如，考虑以下变换序列：

```java
g2.translate(x, y);
g2.rotate(a);
g2.translate(-x, -y);
```

最后一个变换（它最先被应用）将点 (x, y) 移到原点。第二个变换围绕原点旋转角度 a。最后一个变换将原点移回 (x, y)。总体效果是围绕中心点 (x, y) 的旋转——见图 11.19。由于围绕原点以外的点进行旋转是如此常见的操作，因此有一个快捷方法：

```java
g2.rotate(a, x, y);
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_821_0.png)

**图 11.19** 组合变换

如果你了解一些矩阵理论，你可能知道所有旋转、平移、缩放、错切及其组合都可以用以下形式的变换矩阵表示：

$$
\begin{bmatrix}x_{new}\\y_{new}\\1\end{bmatrix}=\begin{bmatrix}a&c&e\\b&d&f\\0&0&1\end{bmatrix}\begin{bmatrix}x\\y\\1\end{bmatrix}
$$

这种变换称为*仿射变换*。在 Java 2D API 中，AffineTransform 类描述了这种变换。如果你知道某个特定变换矩阵的分量，可以直接这样构造它：

```java
AffineTransform t = new AffineTransform(a, b, c, d, e, f);
```

此外，工厂方法 getRotateInstance、getScaleInstance、getTranslateInstance 和 getShearInstance 可以构造表示这些变换类型的矩阵。例如，调用

```java
t = AffineTransform.getScaleInstance(2.0f, 0.5f);
```

会返回一个对应于以下矩阵的变换：

$$
\begin{bmatrix}2&0&0\\0&0.5&0\\0&0&1\end{bmatrix}
$$

最后，实例方法 setToRotation、setToScale、setToTranslation 和 setToShear 可以将变换对象设置为新类型。下面是一个示例：

```java
t.setToRotation(angle); // sets t to a rotation
```

你可以将图形上下文的坐标变换设置为一个 AffineTransform 对象。

```java
g2.setTransform(t); // replaces current transformation
```

然而，在实践中，你不应调用 setTransform 操作，因为它会替换图形上下文可能已有的任何现有变换。例如，用于横向打印的图形上下文已经包含一个 90 度旋转变换。如果你调用 setTransform，就会抹掉那个旋转。相反，应调用 transform 方法。

```java
g2.transform(t); // composes current transformation with t
```

它会将现有变换与新的 AffineTransform 对象组合起来。

如果你只想临时应用一个变换，请先获取旧变换，将其与新变换组合，最后在完成后恢复旧变换。

```java
AffineTransform oldTransform = g2.getTransform(); // save old transform
g2.transform(t); // apply temporary transform
draw on g2
g2.setTransform(oldTransform); // restore old transform
```

### java.awt.geom.AffineTransform 1.2

- `AffineTransform(double a, double b, double c, double d, double e, double f)`
- `AffineTransform(float a, float b, float c, float d, float e, float f)`

  用以下矩阵构造仿射变换：

  $$
  \begin{bmatrix}
  a & c & e \\
  b & d & f \\
  0 & 0 & 1
  \end{bmatrix}
  $$

- `AffineTransform(double[] m)`
- `AffineTransform(float[] m)`

  用以下矩阵构造仿射变换：

  $$
  \begin{bmatrix}
  m[0] & m[2] & m[4] \\
  m[1] & m[3] & m[5] \\
  0 & 0 & 1
  \end{bmatrix}
  $$

- `static AffineTransform getRotateInstance(double a)`

  创建一个围绕原点旋转角度 $a$（以弧度为单位）的变换。变换矩阵为：

  $$
  \begin{bmatrix}
  \cos(a) & -\sin(a) & 0 \\
  \sin(a) & \cos(a) & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  $$

  如果 $a$ 介于 $0$ 和 $\frac{\pi}{2}$ 之间，该旋转会将正 $x$ 轴移向正 $y$ 轴。

- `static AffineTransform getRotateInstance(double a, double x, double y)`

  创建一个围绕点 $(x, y)$ 旋转角度 $a$（以弧度为单位）的变换。

- `static AffineTransform getScaleInstance(double sx, double sy)`

  创建一个缩放变换，将 $x$ 轴缩放 $sx$，将 $y$ 轴缩放 $sy$。变换矩阵为：

  $$
  \begin{bmatrix}
  sx & 0 & 0 \\
  0 & sy & 0 \\
  0 & 0 & 1
  \end{bmatrix}
  $$

### java.awt.geom.AffineTransform 1.2（续）

- **static AffineTransform getShearInstance(double shx, double shy)**

  创建一个错切变换，将 x 轴错切 shx，将 y 轴错切 shy。变换矩阵为：

  ```
  [ 1  shx  0 ]
  [ shy  1  0 ]
  [ 0  0  1 ]
  ```

- **static AffineTransform getTranslateInstance(double tx, double ty)**

  创建一个平移变换，将 x 轴平移 tx，将 y 轴平移 ty。变换矩阵为：

  ```
  [ 1  0  tx ]
  [ 0  1  ty ]
  [ 0  0  1 ]
  ```

- `void setToRotation(double a)`
- `void setToRotation(double a, double x, double y)`
- `void setToScale(double sx, double sy)`
- `void setToShear(double shx, double shy)`
- `void setToTranslation(double tx, double ty)`

  将此仿射变换设置为具有给定参数的基本变换。有关基本变换及其参数的说明，请参见 getXxxInstance 方法。

### java.awt.Graphics2D 1.2

- `void setTransform(AffineTransform t)`

  用 t 替换此图形上下文的现有坐标变换。

- `void transform(AffineTransform t)`

  将此图形上下文的现有坐标变换与 t 组合。

- `void rotate(double a)`
- `void rotate(double a, double x, double y)`
- `void scale(double sx, double sy)`
- `void shear(double shx, double shy)`
- `void translate(double tx, double ty)`

  将此图形上下文的现有坐标变换与具有给定参数的基本变换组合。有关基本变换及其参数的说明，请参见 AffineTransform.getXxxInstance 方法。

## 11.7 裁剪

通过在图形上下文中设置一个*裁剪形状*，可以将所有绘图操作限制在该裁剪形状的内部。

```java
g2.setClip(clipShape); // but see below
g2.draw(shape); // draws only the part that falls inside the clipping shape
```

然而，在实践中，你不应调用 setClip 操作，因为它会替换图形上下文可能已有的任何现有裁剪形状。例如，正如你将在本章后面看到的，用于打印的图形上下文带有一个裁剪矩形，以确保你不会绘制到页边距上。相反，应调用 clip 方法。

```java
g2.clip(clipShape); // better
```

clip 方法会将现有裁剪形状与你提供的新裁剪形状相交。

如果你只想临时应用一个裁剪区域，应首先获取旧裁剪区域，添加新裁剪区域，最后在完成后恢复旧裁剪区域：

```java
Shape oldClip = g2.getClip(); // save old clip
g2.clip(clipShape); // apply temporary clip
draw on g2
g2.setClip(oldClip); // restore old clip
```

在图 11.20 中，我们通过一幅相当引人注目的绘图展示了裁剪能力：一个被复杂形状——即一组字母的轮廓——裁剪的线条图案。

![](img/7dd923a566750151a3aab0dacd0cdaa5_825_0.png)

**图 11.20** 使用字母形状裁剪线条图案

要获得字符轮廓，你需要一个*字体渲染上下文*。使用 Graphics2D 类的 `getFontRenderContext` 方法。

```
FontRenderContext context = g2.getFontRenderContext();
```

接下来，使用一个字符串、一种字体和字体渲染上下文，创建一个 TextLayout 对象：

```
TextLayout layout = new TextLayout("Hello", font, context);
```

这个文本布局对象描述了一个字符序列在特定字体渲染上下文渲染时的布局。布局取决于字体渲染上下文——相同字符在屏幕上和打印机上的显示效果会不同。

对我们的应用更重要的是，getOutline 方法返回一个 Shape 对象，它描述文本布局中字符轮廓的形状。轮廓形状从原点 (0, 0) 开始，这可能不是你想要的。在这种情况下，你可以向 getOutline 操作提供一个仿射变换，以指定你希望轮廓出现的位置。

```
AffineTransform transform = AffineTransform.getTranslateInstance(0, 100);
Shape outline = layout.getOutline(transform);
```

然后，将轮廓追加到裁剪形状中。

```
GeneralPath clipShape = new GeneralPath();
clipShape.append(outline, false);
```

最后，设置裁剪形状并绘制一组线条。这些线条只会出现在字符边界内部。

```
g2.setClip(clipShape);
Point2D p = new Point2D.Double(0, 0);
for (int i = 0; i < NLINES; i++)
{
    double x = . . . ;
    double y = . . . ;
    Point2D q = new Point2D.Double(x, y);
    g2.draw(new Line2D.Double(p, q)); // lines are clipped
}
```

| java.awt.Graphics 1.0 |
|---|
| • `void setClip(Shape s)` 1.2<br>将当前裁剪形状设置为形状 s。<br><br>• `Shape getClip()` 1.2<br>返回当前裁剪形状。 |

