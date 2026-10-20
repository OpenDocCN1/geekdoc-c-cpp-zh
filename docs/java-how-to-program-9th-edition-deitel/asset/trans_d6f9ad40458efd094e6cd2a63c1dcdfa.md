

- `paintComponent` 方法可用于在任何 `JComponent` 组件中绘制图形。
- `paintComponent` 方法接收一个 `Graphics` 对象，当轻量级 Swing 组件需要重绘时，系统会将该对象传递给该方法。
- 当应用程序执行时，应用程序容器会调用 `paintComponent` 方法。要使 `paintComponent` 再次被调用，必须发生一个事件。
- 当 `JComponent` 显示时，会调用其 `paintComponent` 方法。
- 在组件上调用 `repaint` 方法（第 635 页）会更新该组件上绘制的图形。

## 第 15.3 节 颜色控制

- `Color` 类（第 632 页）声明了在 Java 程序中操作颜色的方法和常量。
- 每种颜色都由红色、绿色和蓝色分量组成。这些分量统称为 RGB 值（第 636 页）。RGB 分量分别指定颜色中红、绿、蓝的量。RGB 值越大，该特定颜色的量就越多。
- `Color` 方法 `getRed`、`getGreen` 和 `getBlue`（第 636 页）返回 0 到 255 之间的 `int` 值，分别表示红、绿、蓝的量。
- `Graphics` 方法 `getColor`（第 636 页）返回一个带有当前绘制颜色的 `Color` 对象。
- `Graphics` 方法 `setColor`（第 636 页）设置当前绘制颜色。
- `Graphics` 方法 `fillRect`（第 636 页）绘制一个用 `Graphics` 对象当前颜色填充的矩形。
- `Graphics` 方法 `drawString`（第 638 页）以当前颜色绘制一个 `String`。
- `JColorChooser` GUI 组件（第 639 页）使应用程序用户能够选择颜色。
- `JColorChooser` 静态方法 `showDialog`（第 641 页）显示一个模态 `JColorChooser` 对话框。

## 第 15.4 节 操作字体

- `Font` 类（第 632 页）包含用于操作字体的方法和常量。
- `Font` 类的构造函数接受三个参数——字体名称（第 643 页）、字体样式和字体大小。
- `Font` 的字体样式可以是 `Font.PLAIN`、`Font.ITALIC` 或 `Font.BOLD`（每个都是 `Font` 类的静态字段）。字体样式可以组合使用（例如，`Font.ITALIC + Font.BOLD`）。
- 字体大小以磅（point）为单位测量。1 磅等于 1/72 英寸。
- `Graphics` 方法 `setFont`（第 643 页）设置用于显示文本的绘制字体。
- `Font` 方法 `getStyle`（第 645 页）返回一个表示当前 `Font` 样式的整数值。
- `Font` 方法 `getSize`（第 643 页）以磅为单位返回字体大小。
- `Font` 方法 `getName`（第 643 页）以字符串形式返回当前字体名称。
- `Font` 方法 `getFamily`（第 645 页）返回当前字体所属字体族的名称。字体族的名称是平台相关的。
- `FontMetrics` 类（第 645 页）包含用于获取字体信息的方法。
- 字体度量（第 645 页）包括高度（height）、下伸量（descent）和行距（leading）。

## 第 15.5 节 绘制线条、矩形和椭圆

- `Graphics` 方法 `fillRoundRect`（第 649 页）和 `drawRoundRect`（第 649 页）绘制带圆角的矩形。
- `Graphics` 方法 `draw3DRect`（第 651 页）和 `fill3DRect`（第 651 页）绘制三维矩形。
- `Graphics` 方法 `drawOval`（第 651 页）和 `fillOval`（第 651 页）绘制椭圆。

## 第 15.6 节 绘制弧形

- 弧形（第 651 页）是作为椭圆的一部分绘制的。
- 弧形从起始角度开始，扫过由其弧角（第 651 页）指定的度数。
- `Graphics` 方法 `drawArc`（第 651 页）和 `fillArc`（第 651 页）用于绘制弧形。

## 第 15.7 节 绘制多边形和折线

- `Polygon` 类包含用于创建多边形的方法。
- 多边形是由直线段组成的闭合多边形状。
- 折线（第 654 页）是一系列相连的点。
- `Graphics` 方法 `drawPolyline`（第 656 页）显示一系列相连的线条。
- `Graphics` 方法 `drawPolygon`（第 656 页）和 `fillPolygon`（第 657 页）用于绘制多边形。
- `Polygon` 方法 `addPoint`（第 657 页）向 `Polygon` 添加 x 和 y 坐标对。

## 第 15.8 节 Java 2D API

- Java 2D API（第 657 页）提供了高级的二维图形功能。
- `Graphics2D` 类（第 632 页）——`Graphics` 的子类——用于使用 Java 2D API 进行绘制。
- Java 2D API 中用于绘制形状的类包括 `Line2D.Double`、`Rectangle2D.Double`、`RoundRectangle2D.Double`、`Arc2D.Double` 和 `Ellipse2D.Double`（第 657 页）。
- `GradientPaint` 类（第 632 页）帮助绘制颜色逐渐变化的形状——这种效果称为渐变（gradient，第 660 页）。
- `Graphics2D` 方法 `fill`（第 660 页）绘制任何实现 `Shape` 接口（第 660 页）的类型的填充对象。
- `BasicStroke` 类（第 632 页）帮助指定线条的绘制特性。
- `Graphics2D` 方法 `draw`（第 660 页）用于绘制 `Shape` 对象。
- `GradientPaint` 和 `TexturePaint` 类（第 632 页）帮助指定使用颜色或图案填充形状的特性。
- 一般路径（第 662 页）是由直线和复杂曲线构成的形状，用 `GeneralPath` 类的对象（第 662 页）表示。
- `GeneralPath` 方法 `moveTo`（第 663 页）指定一般路径中的第一个点。
- `GeneralPath` 方法 `lineTo`（第 663 页）绘制一条到路径中下一点的线。每次新的 `lineTo` 调用都会从上一个点绘制一条线到当前点。
- `GeneralPath` 方法 `closePath`（第 664 页）绘制一条从最后一点到最后一次 `moveTo` 调用所指定的点的线。这样就完成了该一般路径。
- `Graphics2D` 方法 `translate`（第 664 页）用于将绘图原点移动到新位置。
- `Graphics2D` 方法 `rotate`（第 664 页）用于旋转下一个显示的形状。

## 自测练习

### 15.1 填空（在以下每个语句中填入空白处）：

- a) 在 Java 2D 中，类 ______ 的方法 ______ 设置用于绘制形状的线条特性。
- b) 类 ______ 帮助指定形状的填充，使填充从一个颜色逐渐变为另一个颜色。
- c) `Graphics` 类的 ______ 方法在两个点之间绘制一条直线。
- d) RGB 是 ______、______ 和 ______ 的缩写。
- e) 字体大小以称为 ______ 的单位测量。
- f) 类 ______ 帮助指定使用在 `BufferedImage` 中绘制的图案来填充形状。

### 15.2

判断以下各项是否正确。如果错误，请解释原因。

- a) `Graphics` 方法 `drawOval` 的前两个参数指定椭圆中心坐标。
- b) 在 Java 坐标系中，x 坐标从左到右增加，y 坐标从上到下增加。
- c) `Graphics` 方法 `fillPolygon` 以当前颜色绘制填充多边形。
- d) `Graphics` 方法 `drawArc` 允许负角度。
- e) `Graphics` 方法 `getSize` 以厘米为单位返回当前字体大小。
- f) 像素坐标 (0, 0) 位于显示器的正中心。

### 15.3

找出以下各项中的错误，并解释如何改正。假设 `g` 是一个 `Graphics` 对象。

- a) `g.setFont( "SansSerif" );`
- b) `g.erase( x, y, w, h );    // clear rectangle at (x, y)`
- c) `Font f = new Font( "Serif", Font.BOLDITALIC, 12 );`
- d) `g.setColor( 255, 255, 0 );  // change color to yellow`

## 自测练习答案

- **15.1**  a) `setStroke`, `Graphics2D`  b) `GradientPaint`  c) `drawLine`  d) 红、绿、蓝。  e) 磅。  f) `TexturePaint`。

- **15.2**
  - a) 错误。前两个参数指定的是外接矩形的左上角。
  - b) 正确。
  - c) 正确。
  - d) 正确。
  - e) 错误。字体大小以磅为单位测量。
  - f) 错误。坐标 (0,0) 对应于进行绘制的 GUI 组件的左上角。

- **15.3**
  - a) `setFont` 方法接受一个 `Font` 对象作为参数——而不是 `String`。
  - b) `Graphics` 类没有 `erase` 方法。应使用 `clearRect` 方法。
  - c) `Font.BOLDITALIC` 不是有效的字体样式。要获得粗斜体字体，请使用 `Font.BOLD + Font.ITALIC`。
  - d) `setColor` 方法接受一个 `Color` 对象作为参数，而不是三个整数。

## 练习

### 15.4

填空（在以下每个语句中填入空白处）：

- a) Java 2D API 中的类 ________ 用于绘制椭圆。
- b) `Graphics2D` 类的 `draw` 和 `fill` 方法需要类型为 __________ 的对象作为参数。
- c) 指定字体样式的三个常量是 ________、________ 和 ________。
- d) `Graphics2D` 方法 ________ 为 Java 2D 形状设置绘制颜色。

### 15.5

判断以下各项是否正确。如果错误，请解释原因。

- a) `Graphics` 方法 `drawPolygon` 自动连接多边形的端点。
- b) `Graphics` 方法 `drawLine` 在两个点之间绘制一条直线。
- c) `Graphics` 方法 `fillArc` 使用度数来指定角度。
- d) 在 Java 坐标系中，y 轴上的值从左到右增加。
- e) `Graphics` 直接继承自 `Object` 类。
- f) `Graphics` 是一个抽象类。
- g) `Font` 类直接继承自 `Graphics` 类。

