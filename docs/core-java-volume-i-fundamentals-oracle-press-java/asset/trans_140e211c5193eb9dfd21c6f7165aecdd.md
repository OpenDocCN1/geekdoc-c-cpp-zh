
```java
44    private static final int DEFAULT_HEIGHT = 200;

46    public void paintComponent(Graphics g)
47    {
48        var g2 = (Graphics2D) g;

50        String message = "Hello, World!";

52        var f = new Font("Serif", Font.BOLD, 36);
53        g2.setFont(f);

55        // measure the size of the message

57        FontRenderContext context = g2.getFontRenderContext();
58        Rectangle2D bounds = f.getStringBounds(message, context);

60        // set (x,y) = top left corner of text

62        double x = (getWidth() - bounds.getWidth()) / 2;
63        double y = (getHeight() - bounds.getHeight()) / 2;

65        // add ascent to y to reach the baseline

67        double ascent = -bounds.getY();
68        double baseY = y + ascent;

70        // draw the message

72        g2.drawString(message, (int) x, (int) baseY);
73        g2.setPaint(Color.LIGHT_GRAY);

76        // draw the baseline

78        g2.draw(new Line2D.Double(x, baseY, x +
79        bounds.getWidth(), baseY));

80        // draw the enclosing rectangle

82        var rect = new Rectangle2D.Double(x, y,
83            bounds.getWidth(), bounds.getHeight());
84        g2.draw(rect);
85    }
86
87    public Dimension getPreferredSize()
88    {
89        return new Dimension(DEFAULT_WIDTH, DEFAULT_HEIGHT);
90    }
```

### java.awt.Font 1.0

- `Font(String name, int style, int size)` 创建一个新的字体对象。字体名称可以是字体面名称（例如 "Helvetica Bold"）或逻辑字体名称（例如 "Serif"、"SansSerif"）。样式是 `Font.PLAIN`、`Font.BOLD`、`Font.ITALIC` 或 `Font.BOLD + Font.ITALIC` 之一。
- `String getFontName()` 获取字体面名称（例如 "Helvetica Bold"）。
- `String getFamily()` 获取字体系列名称（例如 "Helvetica"）。
- `String getName()` 如果字体是使用逻辑字体名称创建的，则获取逻辑名称（例如 "SansSerif"）；否则，获取字体面名称。
- `Rectangle2D getStringBounds(String s, FontRenderContext context)` 1.2 返回一个包围字符串的矩形。该矩形的原点位于基线上。矩形顶部的 y 坐标等于上坡度的负值。矩形的高度等于上坡度、下坡度和行距之和。宽度等于字符串宽度。
- `LineMetrics getLineMetrics(String s, FontRenderContext context)` 1.2 返回一个行度量对象，用于确定字符串的范围。
- `Font deriveFont(int style)` 1.2
- `Font deriveFont(float size)` 1.2
- `Font deriveFont(int style, float size)` 1.2 返回一个新字体，该字体与此字体相同，只是具有给定的大小和样式。

### java.awt.font.LineMetrics 1.2

- `float getAscent()` 获取字体上坡度——从基线到大写字符顶部的距离。
- `float getDescent()` 获取字体下坡度——从基线到下行字符底部的距离。
- `float getLeading()` 获取字体行距——一行文本底部与下一行顶部之间的空间。
- `float getHeight()` 获取字体的总高度——两行文本基线之间的距离（descent + leading + ascent）。

### java.awt.Graphics2D 1.2

- `FontRenderContext getFontRenderContext()` 获取一个字体渲染上下文，该上下文指定此图形上下文中的字体特征。
- `void drawString(String str, float x, float y)` 使用当前字体和颜色绘制一个字符串。

### javax.swing.JComponent 1.2

- `FontMetrics getFontMetrics(Font f)` 5 获取给定字体的字体度量。`FontMetrics` 类是 `LineMetrics` 类的前身。

### java.awt.FontMetrics 1.0

- `FontRenderContext getFontRenderContext()` 1.2 获取该字体的字体渲染上下文。

### 10.3.4 显示图像

你可以使用 `ImageIcon` 类从文件中读取图像：

```java
Image image = new ImageIcon(filename).getImage();
```

现在，变量 image 包含一个对象的引用，该对象封装了图像数据。使用 `Graphics` 类的 `drawImage` 方法显示图像。

```java
public void paintComponent(Graphics g)
{
    . . .
    g.drawImage(image, x, y, null);
}
```

我们可以再进一步，用图形图像平铺窗口。结果看起来像**图 10.11**中所示的屏幕。我们在 `paintComponent` 方法中完成平铺。首先在左上角绘制图像的一份副本，然后使用 `copyArea` 调用将其复制到整个窗口：

```java
for (int i = 0; i * imageWidth <= getWidth(); i++)
    for (int j = 0; j * imageHeight <= getHeight(); j++)
        if (i + j > 0)
            g.copyArea(0, 0, imageWidth, imageHeight, i * imageWidth, j * imageHeight);
```

![](img/0e7b74ef51a065c077b42cd87b362288_865_0.png)

**图 10.11** 使用图形图像平铺的窗口

### java.awt.Graphics 1.0

- `boolean drawImage(Image img, int x, int y, ImageObserver observer)`
- `boolean drawImage(Image img, int x, int y, int width, int height, ImageObserver observer)` 绘制未缩放或缩放后的图像。注意：此调用可能会在图像绘制完成之前返回。`imageObserver` 对象会收到渲染进度通知。这在很久以前是一个有用的特性。如今，只需传入 `null` 观察器。
- `void copyArea(int x, int y, int width, int height, int dx, int dy)` 复制屏幕的一个区域。`dx` 和 `dy` 参数是从源区域到目标区域的距离。

## 10.4 事件处理

任何支持 GUI 的操作环境都会持续监视击键或鼠标点击等事件。然后，这些事件会被报告给正在运行的程序。每个程序随后决定要针对这些事件做什么（如果有的话）。

### 10.4.1 基本事件处理概念

在 Java AWT 中，*事件源*（例如按钮或滚动条）具有允许你注册*事件监听器*的方法——这些对象会对事件执行所需的响应。

当事件监听器收到关于某个事件的通知时，有关该事件的信息会封装在一个*事件对象*中。在 Java 中，所有事件对象最终都派生自 `java.util.EventObject` 类。当然，每种事件类型都有子类，例如 `ActionEvent` 和 `WindowEvent`。

不同的事件源可以产生不同种类的事件。例如，按钮可以发送 `ActionEvent` 对象，而窗口可以发送 `WindowEvent` 对象。

总结一下，以下是 AWT 中事件处理工作方式的概述：

- 事件监听器是实现*监听器接口*的类的实例。
- 事件源是一个可以注册监听器对象并向它们发送事件对象的对象。
- 当该事件发生时，事件源会向所有已注册的监听器发送事件对象。
- 然后，监听器对象使用事件对象中的信息来确定它们对该事件的反应。

图 10.12 展示了事件处理类与接口之间的关系。

下面是一个指定监听器的示例：

```java
ActionListener listener = . . .;
var button = new JButton("OK");
button.addActionListener(listener);
```

![](img/0e7b74ef51a065c077b42cd87b362288_867_0.png)

**图 10.12** 事件源与监听器之间的关系

现在，只要按钮中发生“动作事件”，监听器对象就会收到通知。对于按钮，正如你所料，动作事件就是按钮点击。

要实现 `ActionListener` 接口，监听器类必须有一个名为 `actionPerformed` 的方法，该方法接收一个 `ActionEvent` 对象作为参数。

```java
class MyListener implements ActionListener
{
    . . .
    public void actionPerformed(ActionEvent event)
    {
        // reaction to button click goes here
        . . .
    }
}
```

每当用户点击按钮时，`JButton` 对象会创建一个 `ActionEvent` 对象，并调用 `listener.actionPerformed(event)`，传入该事件对象。像按钮这样的事件源可以有多个监听器。在这种情况下，每当用户点击按钮时，按钮会调用所有监听器的 `actionPerformed` 方法。

[图 10.13](#) 展示了事件源、事件监听器和事件对象之间的交互。
