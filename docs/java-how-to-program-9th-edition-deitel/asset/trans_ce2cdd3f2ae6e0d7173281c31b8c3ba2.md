

### 15.6 (使用方法 drawArc 绘制同心圆)
编写一个绘制八个同心圆的应用。圆之间应相隔 10 像素。使用 Graphics 方法 drawArc。

### 15.7 (使用类 Ellipse2D.Double 绘制同心圆)
修改练习 15.6 的解决方案，使用类 Ellipse2D.Double 和类 Graphics2D 的方法 draw 来绘制椭圆。

### 15.8 (使用类 Line2D.Double 绘制随机线段)
修改练习 15.7 的解决方案，绘制随机颜色和随机线宽的随机线段。使用类 Line2D.Double 和类 Graphics2D 的方法 draw 来绘制线段。

### 15.9 (随机三角形)
编写一个应用，显示不同颜色的随机生成的三角形。每个三角形应填充不同的颜色。使用类 GeneralPath 和类 Graphics2D 的方法 fill 来绘制三角形。

### 15.10 (随机字符)
编写一个应用，随机绘制不同字体、大小和颜色的字符。

### 15.11 (使用方法 drawLine 绘制网格)
编写一个应用，绘制一个 8×8 网格。使用 Graphics 方法 drawLine。

### 15.12 (使用类 Line2D.Double 绘制网格)
修改练习 15.11 的解决方案，使用类 Line2D.Double 的实例和类 Graphics2D 的方法 draw 来绘制网格。

### 15.13 (使用方法 drawRect 绘制网格)
编写一个应用，绘制一个 10×10 网格。使用 Graphics 方法 drawRect。

### 15.14 (使用类 Rectangle2D.Double 绘制网格)
修改练习 15.13 的解决方案，使用类 Rectangle2D.Double 和类 Graphics2D 的方法 draw 来绘制网格。

### 15.15 (绘制四面体)
编写一个应用，绘制一个四面体（具有四个三角形面的三维形状）。使用类 GeneralPath 和类 Graphics2D 的方法 draw。

### 15.16 (绘制立方体)
编写一个应用，绘制一个立方体。使用类 GeneralPath 和类 Graphics2D 的方法 draw。

### 15.17 (使用类 Ellipse2D.Double 绘制圆)
编写一个应用，提示用户输入圆的半径作为浮点数，并绘制该圆，以及圆的直径、周长和面积的值。使用 3.14159 作为 π 的值。[注：你也可以使用预定义的常量 Math.PI 作为 π 的值。该常量比值 3.14159 更精确。类 Math 声明在 java.lang 包中，因此你无需导入它。] 使用以下公式（r 为半径）：

diameter = 2r
circumference = 2πr
area = πr²

用户还应被提示输入一组坐标以外的半径。然后绘制圆并显示其直径、周长和面积，使用 Ellipse2D.Double 对象表示圆并使用类 Graphics2D 的方法 draw 显示它。

### 15.18 (屏幕保护程序)
编写一个模拟屏幕保护程序的应用。该应用应使用类 Graphics 的方法 drawLine 随机绘制线段。绘制 100 条线后，应用应清除自身并重新开始绘制线段。为了使程序能够持续绘制，将对 repaint 的调用作为方法 paintComponent 中的最后一行。你的系统上是否注意到任何问题？

### 15.19 (使用 Timer 的屏幕保护程序)
包 javax.swing 包含一个名为 Timer 的类，该类能够在固定的时间间隔（以毫秒为单位指定）调用接口 ActionListener 的方法 actionPerformed。修改练习 15.18 的解决方案，从方法 paintComponent 中移除对 repaint 的调用。声明你的类实现 ActionListener。（actionPerformed 方法应仅调用 repaint。）在你的类中声明一个名为 timer 的类型为 Timer 的实例变量。在类的构造函数中，编写以下语句：

```
timer = new Timer( 1000, this );
timer.start();
```

这将创建一个类 Timer 的实例，该实例将每 1000 毫秒（即每秒）调用一次此对象的 actionPerformed 方法。

### 15.20 (随机数量线段的屏幕保护程序)
修改练习 15.19 的解决方案，使用户能够输入在应用清除自身并重新开始绘制线段之前应绘制的随机线段数量。使用 JTextField 获取值。用户应在程序执行期间的任何时间将新数字输入到 JTextField 中。使用内部类执行 JTextField 的事件处理。

### 15.21 (带形状的屏幕保护程序)
修改练习 15.19 的解决方案，使其使用随机数生成来选择要显示的不同形状。使用类 Graphics 的方法。

### 15.22 (使用 Java 2D API 的屏幕保护程序)
修改练习 15.21 的解决方案，使用 Java 2D API 的类和绘图功能。绘制矩形和椭圆等形状，并使用随机生成的渐变。使用类 GradientPaint 生成渐变。

### 15.23 (海龟绘图)
修改练习 7.21——海龟绘图——的解决方案，添加使用 JTextFields 和 JButtons 的图形用户界面。绘制线段而不是星号（*）。当海龟绘图程序指定移动时，将位置数转换为屏幕上的像素数，方法是乘以 10（或你选择的任何值）。使用 Java 2D API 功能实现绘图。

### 15.24 (骑士巡游)
制作骑士巡游问题的图形版本（练习 7.22、练习 7.23 和练习 7.26）。每次移动时，国际象棋棋盘的相应单元格应更新为正确的移动编号。如果程序的结果是完整巡游或封闭巡游，程序应显示适当的[content]

### 15.6 (使用方法 drawArc 绘制同心圆)
编写一个绘制八个同心圆的应用。圆之间应相隔 10 像素。使用 Graphics 方法 drawArc。

### 15.7 (使用类 Ellipse2D.Double 绘制同心圆)
修改练习 15.6 的解决方案，使用类 Ellipse2D.Double 和类 Graphics2D 的方法 draw 来绘制椭圆。

### 15.8 (使用类 Line2D.Double 绘制随机线段)
修改练习 15.7 的解决方案，绘制随机颜色和随机线宽的随机线段。使用类 Line2D.Double 和类 Graphics2D 的方法 draw 来绘制线段。

### 15.9 (随机三角形)
编写一个应用，显示不同颜色的随机生成的三角形。每个三角形应填充不同的颜色。使用类 GeneralPath 和类 Graphics2D 的方法 fill 来绘制三角形。

### 15.10 (随机字符)
编写一个应用，随机绘制不同字体、大小和颜色的字符。

### 15.11 (使用方法 drawLine 绘制网格)
编写一个应用，绘制一个 8×8 网格。使用 Graphics 方法 drawLine。

### 15.12 (使用类 Line2D.Double 绘制网格)
修改练习 15.11 的解决方案，使用类 Line2D.Double 的实例和类 Graphics2D 的方法 draw 来绘制网格。

### 15.13 (使用方法 drawRect 绘制网格)
编写一个应用，绘制一个 10×10 网格。使用 Graphics 方法 drawRect。

### 15.14 (使用类 Rectangle2D.Double 绘制网格)
修改练习 15.13 的解决方案，使用类 Rectangle2D.Double 和类 Graphics2D 的方法 draw 来绘制网格。

### 15.15 (绘制四面体)
编写一个应用，绘制一个四面体（具有四个三角形面的三维形状）。使用类 GeneralPath 和类 Graphics2D 的方法 draw。

### 15.16 (绘制立方体)
编写一个应用，绘制一个立方体。使用类 GeneralPath 和类 Graphics2D 的方法 draw。

### 15.17 (使用类 Ellipse2D.Double 绘制圆)
编写一个应用，提示用户输入圆的半径作为浮点数，并绘制该圆，以及圆的直径、周长和面积的值。使用 3.14159 作为 π 的值。[注：你也可以使用预定义的常量 Math.PI 作为 π 的值。该常量比值 3.14159 更精确。类 Math 声明在 java.lang 包中，因此你无需导入它。] 使用以下公式（r 为半径）：

diameter = 2r
circumference = 2πr
area = πr²

用户还应被提示输入一组坐标以外的半径。然后绘制圆并显示其直径、周长和面积，使用一个 Ellipse2D.Double 对象来表示圆并使用类 Graphics2D 的方法 draw 来显示它。

### 15.18 (屏幕保护程序)
编写一个模拟屏幕保护程序的应用。该应用应使用方法 drawLine 随机绘制线段。绘制 100 条线后，应用应清除自身并开始再次绘制线段。为了允许程序持续绘制，将对 repaint 的调用作为方法 paintComponent 中的最后一行。你的系统上是否注意到任何问题？

### 15.19 (使用 Timer 的屏幕保护程序)
包 javax.swing 包含一个名为 Timer 的类，该类能够在固定的时间间隔（以毫秒为单位指定）调用接口 ActionListener 的方法 actionPerformed。修改练习 15.18 的解决方案以移除对 repaint 从方法 paintComponent 的调用。声明你的类实现 ActionListener。（actionPerformed 方法应仅调用 repaint。）声明一个类型为 Timer 的实例变量 timer 在你的类中。在类的构造函数中，编写以下语句：

```
timer = new Timer( 1000, this );
timer.start();
```

这创建了一个类 Timer 的实例，它将每 1000 毫秒（即每秒）调用此对象的 actionPerformed 方法。

### 15.20 (随机数量线段的屏幕保护程序)
修改练习 15.19 的解决方案以允许用户输入在应用清除自身并开始再次绘制线段之前应绘制的随机线段的数量。使用 JTextField 来获取值。用户应在程序执行期间的任何时间将新数字输入到 JTextField 中。使用内部类来执行 JTextField 的事件处理。

### 15.21 (带形状的屏幕保护程序)
修改练习 15.19 的解决方案，使其使用随机数生成来选择要显示的不同形状。使用类 Graphics 的方法。

### 15.22 (使用 Java 2D API 的屏幕保护程序)
修改练习 15.21 的解决方案以使用 Java 2D API 的类和绘图功能。绘制诸如矩形和椭圆之类的形状，并带有随机生成的渐变。使用类 GradientPaint 来生成渐变。

### 15.23 (海龟绘图)
修改练习 7.21——海龟绘图——的解决方案以添加使用 JTextFields 和 JButtons 的图形用户界面。绘制线段而不是星号（*）。当海龟绘图程序指定移动时，将位置数转换为屏幕上的像素数，方法是乘以 10（或你选择的任何值）。使用 Java 2D API 功能实现绘图。

### 15.24 (骑士巡游)
制作骑士巡游问题的图形版本（练习 7.22、练习 7.23 和练习 7.26）。每次移动时，国际象棋棋盘的相应单元格应更新为正确的移动编号。如果程序的结果是完整巡游或封闭巡游，程序应显示适当的

### 15.25 (乌龟和野兔)
制作乌龟和野兔模拟的图形版本（练习 7.28）。通过绘制从窗口左下角延伸到右上角的弧来模拟山脉。乌龟和野兔应沿山脉竞赛。实现图形输出以在每次移动时实际在弧上打印乌龟和野兔。[提示：将比赛长度从 70 延长到 300 以给你更大的图形区域。]

### 15.26 (绘制螺旋线)
编写一个应用，使用 Graphics 方法 drawPolyline 绘制类似图 15.33 所示的螺旋线。

![](img/009e962758dcc71dbc43a493362e6dc0_706_0.png)

图 15.33 | 使用方法 drawPolyline 绘制的螺旋线。

### 15.27 (饼图)
编写一个程序，输入四个数字并将其作为饼图绘制。使用类 Arc2D.Double 和类 Graphics2D 的方法 fill 执行绘图。用不同的颜色绘制饼图的每个部分。

### 15.28 (选择形状)
编写一个应用，允许用户从 JComboBox 中选择一个形状，并在方法 paintComponent 中随机位置和尺寸绘制它 20 次。JComboBox 中的第一个项目应为默认形状，在第一次调用 paintComponent 时显示。

### 15.29 (随机颜色)
修改练习 15.28 以用随机选择的颜色绘制 20 个随机大小的形状中的每一个。使用一个 Color 数组中的全部 13 个预定义 Color 对象。

### 15.30 (JColorChooser 对话框)
修改练习 15.28 以允许用户从 JColorChooser 对话框中选择应绘制形状的颜色。

## （可选）GUI 和图形案例研究：添加 Java 2D

### 15.31
Java 2D 引入了许多用于创建独特而令人印象深刻的图形的新功能。我们将把这些功能的一小部分添加到你在练习 14.17 中创建的绘图应用中。在这个版本中，你将启用用户指定用于填充形状的渐变并更改用于绘制线条和形状轮廓的笔触特征。用户将能够选择构成渐变的颜色并设置笔触宽度和虚线长度。

首先，你必须更新 MyShape 层次结构以支持 Java 2D 功能。进行以下更改于类 MyShape：

- a) 将抽象方法 draw 的参数类型从 Graphics 改为 Graphics2D
- b) 将类 MyShape 中所有类型为 Color 的变量更改为类型 Paint 以启用对渐变的支持。[注：请回忆类 Color 实现接口 Paint。]
- c) 在类 MyShape 中添加一个类型为 Stroke 的实例变量，并在构造函数中添加一个 Stroke 参数以初始化新的实例变量。默认笔触应为类 BasicStroke 的实例。

类 MyLine、MyBoundedShape、MyOval 和 MyRectangle 每个都应在其构造函数中添加一个 Stroke 参数。在 draw 方法中，每个形状都应在绘制或填充形状之前设置 Paint 和 Stroke。由于 Graphics2D 是 Graphics 的子类，我们可以继续使用 Graphics 方法 drawLine、drawOval、fillOval 等来绘制形状。当调用这些方法时，它们将使用指定的 Paint 和 Stroke 设置绘制适当的形状。

接下来，你将更新 DrawPanel 以处理 Java 2D 功能。将所有 Color 变量更改为 Paint 变量。声明一个类型为 Stroke 的实例变量 currentStroke 并为其提供一个 set 方法。更新对各个形状构造函数的调用以包含 Paint 和 Stroke 参数。在方法 paintComponent 中，将 Graphics 引用强制转换为 Graphics2D 类型并在对 MyShape 方法 draw 的每次调用中使用 Graphics2D 引用。

接下来，使新的 Java 2D 功能从 GUI 可访问。创建一个用于设置 Java 2D 选项的 GUI 组件的 JPanel。在 DrawFrame 的顶部，在当前包含标准形状控件的面板下方添加这些组件（参见图 15.34）。这些 GUI 组件应包括：

- a) 一个复选框以指定是否使用渐变进行绘制。
- b) 两个 JButtons，每个按钮显示一个 JColorChooser 对话框以允许用户选择渐变中的第一种和第二种颜色。（这些将取代练习 14.17 中用于选择颜色的 JComboBox。）
- c) 一个用于输入 Stroke 宽度的文本字段。
- d) 一个用于输入 Stroke 虚线长度的文本字段。
- e) 一个用于选择是否绘制虚线或实线的复选框。

如果用户选择使用渐变绘制，则将 DrawPanel 上的 Paint 设置为用户选择的两种颜色的渐变。表达式

