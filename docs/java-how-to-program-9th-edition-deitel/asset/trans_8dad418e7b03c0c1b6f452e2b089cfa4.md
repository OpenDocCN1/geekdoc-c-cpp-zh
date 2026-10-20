

## 方法 startAnimation

在 LogoAnimatorJPanel 构造函数加载图像后，图 24.5 中的 main 方法设置了动画将出现的窗口（第 12–17 行），第 19 行调用 LogoAnimatorJPanel 的 startAnimation 方法（在图 24.4 的第 76–93 行声明）。此方法在第一次启动程序的动画或重新启动程序先前停止的动画。动画由类 Timer 的一个实例驱动（来自包 javax.swing）。

程序首次运行时，调用方法 startAnimation 开始动画。虽然我们提供了此方法在动画被停止时重新启动动画的功能，但示例并未为此目的调用该方法。我们添加了此功能，以防读者选择添加 GUI 组件以使用户能够启动和停止动画。

Timer 以毫秒为单位的固定间隔生成 ActionEvents（通常指定为 Timer 构造函数的参数），并且每次发生 ActionEvent 时通知其所有 ActionListeners。第 78 行确定 Timer 引用 animationTimer 是否为 null。如果是，则方法 startAnimation 被第一次调用，需要创建一个 Timer 以便动画开始。第 80 行将 currentImage 设置为 0，这表示动画应从数组 images 的第一个元素开始。第 83–84 行将一个新的 Timer 对象分配给 animationTimer。Timer 构造函数接收两个参数——以毫秒为单位的延迟（ANIMATION_DELAY 为 50，如第 18 行指定）和将响应 Timer 的 ActionEvents 的 ActionListener。对于第二个参数，创建了一个 TimerHandler 类的对象。此类实现了 ActionListener，声明在第 114–121 行。第 86 行调用 Timer 对象的 start 方法启动 Timer。一旦启动，animationTimer 将每 50 毫秒生成一个 ActionEvent 并调用 Timer 的事件处理程序 actionPerformed（第 117–120 行）。第 119 行调用 LogoAnimatorJPanel 的 repaint 方法以安排调用 LogoAnimatorJPanel 的 paintComponent 方法（第 64–73 行）。请记住，任何绘制的子类 JComponent 都应在 paintComponent 方法中进行绘制。请回忆，paintComponent 方法中的第一条语句应调用超类的 paintComponent 方法，以确保 Swing 组件正确显示。

如果动画先前已启动，则我们的 Timer 已被创建，第 78 行的条件评估为 false。程序继续执行第 90–91 行，这将重新启动程序先前停止的动画。第 90 行的 if 条件使用 Timer 方法 isRunning 来确定 Timer 是否正在运行（即生成事件）。如果它未运行，第 91 行调用 Timer 方法 restart 以指示 Timer 应再次开始生成事件。一旦发生这种情况，方法 actionPerformed（Timer 的事件处理程序）将再次以固定间隔被调用。

## 方法 paintComponent

第 68 行调用 ImageIcon 的 paintIcon 方法以显示数组中元素 currentImage 存储的图像。参数表示要绘制的 Component（this）、执行绘制的 Graphics 对象（g）以及图像左上角的坐标。第 71–72 行确定 animationTimer 是否正在运行，如果是，则通过将 currentImage 增加 1 为下一个要显示的图像做准备。余数计算确保当 currentImage 增加超过数组中的最后一个元素索引时，其值被设置为 0（以重复动画序列）。 

if 语句确保如果在 Timer 停止时调用 paintComponent，则会显示相同的图像。如果提供了一个允许用户启动和停止动画的 GUI，这将很有用。例如，如果动画被停止并且用户用另一个窗口覆盖它，然后将其取消覆盖，则会调用 paintComponent 方法。在这种情况下，我们不希望动画显示下一张图像（因为动画已停止）。我们只希望窗口在动画重新启动之前显示相同的图像。

## 方法 stopAnimation

方法 stopAnimation（第 96–99 行）通过调用 Timer 方法 stop 来停止动画，以指示 Timer 应停止生成事件。这会阻止 actionPerformed 调用 repaint 以启动数组中下一张图像的绘制。与重新启动动画一样，此示例定义但未使用方法 stopAnimation。我们提供了此方法用于演示目的，或允许用户修改此示例以停止和重新启动动画。

## 软件工程观察 24.1

> 在为在 applet 中使用而创建动画时，提供一种机制以在用户浏览与动画 applet 所在页面不同的新网页时禁用动画。

## 方法 getPreferredSize 和 getMinimumSize

通过扩展类 JPanel，我们正在创建一个新的 GUI 组件。因此，我们必须确保它在布局目的上像其他组件一样工作。布局管理器通常使用组件的 getPreferredSize 方法（继承自类 java.awt.Component）来确定组件的首选宽度和高度。如果新组件具有首选宽度和高度，它应重写方法 getPreferredSize（第 108–111 行）以返回该宽度和高度作为类 Dimension（包 java.awt）的对象。Dimension 类表示 GUI 组件的宽度和高度。在此示例中，我们提供的图像宽 160 像素，高 80 像素，因此方法 getPreferredSize 将返回包含数字 160 和 80 的 Dimension 对象（如果使用这些图像）。

## 外观观察 24.1

> JPanel 对象的默认大小为宽 10 像素，高 10 像素。

## 外观观察 24.2

> 当子类化 JPanel（或任何其他 JComponent）时，如果新组件具有特定的首选宽度和高度，请重写方法 getPreferredSize。

第 102–105 行重写方法 getMinimumSize。此方法确定组件的最小宽度和高度。与方法 getPreferredSize 一样，新组件应重写方法 getMinimumSize（也继承自类 Component）。方法 getMinimumSize 只是调用 getPreferredSize（一种常见的编程实践）以指示最小尺寸和首选尺寸相同。一些布局管理器忽略这些方法指定的尺寸。例如，BorderLayout 的 NORTH 和 SOUTH 区域仅使用组件的首选高度。

## 外观观察 24.3

如果新的 GUI 组件具有最小宽度和高度（即更小的尺寸将使组件在显示上无效），请重写方法 getMinimumSize 以返回最小宽度和高度作为类 Dimension 的实例。

## 外观观察 24.4

对于许多 GUI 组件，方法 getMinimumSize 的实现是返回对组件 getPreferredSize 方法的调用结果。

## 编译应用程序

编译和运行此应用程序需要包含 JNLP API 的 jnlp.jar 文件。要编译应用程序，请使用以下命令：

```
javac -classpath PathToJnlpJarFile *.java
```

其中 PathToJnlpJarFile 包括路径和文件名 jnlp.jar。

## 为 Java Web Start 打包应用程序

要将应用程序打包以与 Java Web Start 一起使用，必须创建一个包含 applet 代码和 jnlp.jar 文件的 JAR 文件。为此，请使用命令

```
jar cvf LogoAnimator.jar *.class PathToJnlpJarFile
```

其中 PathToJnlpJarFile 包括路径和文件名 jnlp.jar。

## LoadImageAndScale Applet 的 JNLP 文档

图 24.6 中的 JNLP 文档与图 24.2 中的类似。此文档中唯一的新的功能是 application-desc 元素（第 16–19 行），它指定了应用程序的名称及其主类。要运行此应用程序，请使用命令

```
javaws LogoAnimator.jnlp
```

请记住，您也可以通过网页中的链接运行 Java Web Start 应用程序，如我们在图 23.13 中所示。

```
1 <?xml version="1.0" encoding="UTF-8"?>
2 <jnlp codebase="file:." href="LogoAnimator.jnlp">
3
4     <information>
5         <title>LogoAnimator</title>
6         <vendor>Deitel</vendor>
7         <offline-allowed/>
8     </information>
9
10    <resources>
11        <java version="1.6+"/>
12        <jar href="LogoAnimator.jar" main="true"/>
13        <jar href="jnlp.jar"/>
14    </resources>
15
```

Fig. 24.6 | JNLP document for the LoadImageAndScale applet. (Part 1 of 2.)

