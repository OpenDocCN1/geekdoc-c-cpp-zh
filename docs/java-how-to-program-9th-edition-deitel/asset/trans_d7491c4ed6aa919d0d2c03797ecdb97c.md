

## 14.12（温度转换）编写一个温度转换应用程序，将华氏温度转换为摄氏温度。华氏温度应通过键盘输入（通过 JTextField）。应使用 JLabel 来显示转换后的温度。使用以下公式进行转换：

```
Celsius = 5/9 × ( Fahrenheit - 32 )
```

## 14.13（温度转换修改）通过添加开尔文温标来增强练习 14.12 中的温度转换应用程序。该应用程序还应允许用户在任意两个温标之间进行转换。除练习 14.12 中的公式外，还使用以下开尔文与摄氏度之间的转换公式：

```
Kelvin = Celsius + 273.15
```

## 14.14（猜数字游戏）编写一个应用程序来玩“猜数字”游戏，方法如下：你的应用程序通过在 1–1000 范围内随机选择一个整数来选择要猜的数字。然后应用程序在标签中显示以下内容：

```
I have a number between 1 and 1000. Can you guess my number?
Please enter your first guess.
```

应使用 JTextField 输入猜测。每输入一次猜测，背景颜色应更改为红色或蓝色。红色表示用户正在“变暖”，蓝色表示“变冷”。JLabel 应显示“Too High”或“Too Low”以帮助用户缩小范围。当用户猜对时，应显示“Correct!”并且用于输入的 JTextField 应更改为不可编辑。应提供一个 JButton 以允许用户再次玩游戏。当单击 JButton 时，应生成一个新的随机数，并且输入的 JTextField 应更改为可编辑。

## 14.15（显示事件）在应用程序执行期间显示发生的事件通常很有用。这可以帮助你了解事件何时发生以及它们是如何生成的。编写一个应用程序，使用户能够生成并处理本章中讨论的每个事件。应用程序应提供来自 ActionListener、ItemListener、ListSelectionListener、MouseListener、MouseMotionListener 和 KeyListener 接口的方法，以在事件发生时显示消息。使用方法 toString 将在每个事件处理程序中接收到的事件对象转换为可以显示的字符串。方法 toString 创建一个包含事件对象中所有信息的字符串。

## 14.16（基于 GUI 的 Craps 游戏）修改第 6.10 节的应用程序，以提供一个 GUI，使用户能够单击 JButton 来掷骰子。应用程序还应显示四个 JLabels 和四个 JTextFields，每个 JTextField 一个 JLabel。JTextFields 应用于在每次掷骰后显示每个骰子的值和骰子之和。当用户在第一次掷骰时未赢或未输时，点数应显示在第四个 JTextField 中，并且应一直显示直到游戏失败。

## （可选）GUI 和图形案例研究练习：扩展界面

## 14.17（交互式绘图应用程序）在本练习中，你将实现一个 GUI 应用程序，使用 GUI 和图形案例研究练习 10.2 中的 MyShape 层次结构来创建交互式绘图应用程序。你将为 GUI 创建两个类，并提供一个启动应用程序的测试类。MyShape 层次结构的类不需要进行任何额外更改。

要创建的第一个类是 JPanel 的子类 DrawPanel，它表示用户绘制形状的区域。类 DrawPanel 应具有以下实例变量：

- a) 一个类型为 MyShape 的数组 shapes，用于存储用户绘制的所有形状。
- b) 一个整数 shapeCount，用于计算数组中的形状数量。
- c) 一个整数 shapeType，用于确定要绘制的形状类型。
- d) 一个 MyShape currentShape，表示用户当前正在绘制的形状。
- e) 一个 `Color currentColor`，表示当前绘图颜色。
- f) 一个 `boolean filledShape`，用于确定是否绘制填充形状。
- g) 一个 `JLabel statusLabel`，表示状态栏。状态栏将显示当前鼠标位置的坐标。

类 `DrawPanel` 还应声明以下方法：

- a) 重写方法 `paintComponent`，绘制数组中的形状。使用实例变量 `shapeCount` 来确定要绘制多少个形状。方法 `paintComponent` 还应调用 `currentShape` 的 draw 方法，前提是 `currentShape` 不为 null。
- b) `shapeType`、`currentColor` 和 `filledShape` 的设置方法。
- c) 方法 `clearLastShape` 应通过递减实例变量 `shapeCount` 来清除上一个绘制的形状。确保 `shapeCount` 不小于零。
- d) 方法 `clearDrawing` 应通过将 `shapeCount` 设置为零来删除当前绘图中的所有形状。

方法 `clearLastShape` 和 `clearDrawing` 应调用 `repaint`（从 `JPanel` 继承）以刷新 `DrawPanel` 上的绘图，通过指示系统应调用方法 `paintComponent`。

类 `DrawPanel` 还应提供事件处理以使用鼠标绘图。创建一个同时扩展 `MouseAdapter` 并实现 `MouseMotionListener` 的内部类，以在一个类中处理所有鼠标事件。

在内部类中，重写方法 `mousePressed`，使其为 `currentShape` 分配一个由 `shapeType` 指定的类型的新形状，并将两个点都初始化为鼠标位置。接下来，重写方法 `mouseReleased` 以完成当前形状的绘制并将其放入数组中。将 `currentShape` 的第二个点设置为当前鼠标位置并将 `currentShape` 添加到数组中。实例变量 `shapeCount` 确定插入索引。将 `currentShape` 设置为 null 并调用方法 `repaint` 以使用新形状更新绘图。

重写方法 `mouseMoved` 以设置 `statusLabel` 的文本，使其显示鼠标坐标——这将在用户在 `DrawPanel` 内移动（但不拖动）鼠标时每次更新标签的坐标。接下来，重写方法 `mouseDragged`，使其将 `currentShape` 的第二个点设置为当前鼠标位置并调用方法 `repaint`。这将允许用户在拖动鼠标时看到形状。还在 `mouseDragged` 中使用当前鼠标位置更新 `JLabel`。

为 `DrawPanel` 创建一个只有一个 `JLabel` 参数的构造函数。在构造函数中，使用传递给参数的值初始化 `statusLabel`。还将数组 `shapes` 初始化为 100 个条目，`shapeCount` 初始化为 0，`shapeType` 初始化为表示线的数值，`currentShape` 初始化为 null，`currentColor` 初始化为 `Color.BLACK`。构造函数然后应将 `DrawPanel` 的背景颜色设置为 `Color.WHITE` 并注册 `MouseListener` 和 `MouseMotionListener`，以便 `JPanel` 正确处理鼠标事件。

接下来，创建一个名为 `DrawFrame` 的 `JFrame` 子类，提供一个 GUI，使用户能够控制绘图的各个方面。对于 `DrawFrame` 的布局，我们建议使用 `BorderLayout`，组件位于 NORTH 区域，主要绘图面板位于 CENTER 区域，状态栏位于 SOUTH 区域，如图 14.49 所示。在顶部面板中，创建下面列出的组件。每个组件的事件处理程序应调用类 `DrawPanel` 中的适当方法。

- a) 一个按钮用于撤消上一个绘制的形状。
- b) 一个按钮用于清除绘图中的所有形状。
- c) 一个组合框用于从 13 种预定义颜色中选择颜色。
- d) 一个组合框用于选择要绘制的形状。
- e) 一个复选框指定形状应为填充还是未填充。

在 `DrawFrame` 的构造函数中声明并创建界面组件。你需要在创建 `DrawPanel` 之前创建状态栏 `JLabel`，以便可以将 `JLabel` 作为参数传递给 `DrawPanel` 的构造函数。最后，创建一个测试类来初始化并显示 `DrawFrame` 以执行应用程序。

