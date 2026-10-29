

## FIGURE 34.17

PRS Parameters rollout 是默认的变换控制器。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_912_0.png)

在 Parameters rollout 中，XRef 控制器是一个用于打开 XRef Object 对话框的按钮，其中 XRef Record 为高亮显示。Parameters rollout 还列出了 XRef 文件、对象和状态。

## Cross-Ref

XRefs 在第 3 章“Working with Files, Importing, and Exporting”中有详细说明。

## Position track controllers

Position track 控制器类型包括一些常见的默认控制器，可以分配给 Position track。它们通常使用代表 X、Y、Z 轴的三个唯一值。这些控制器可以从 Animation > Position Controllers 菜单中分配。菜单中许多控制器也在 Rotation and Scale Controllers 菜单中可以找到。

## Audio controller

Audio 控制器可以根据声音文件的振幅控制对象的变换、颜色或参数值。图 34.18 所示的 Audio Controller 对话框包括 Choose Sound 和 Remove Sound 按钮，用于加载或移除声音文件。您可以通过右键单击分配了 Audio Controller 的轨道并从弹出菜单中选择 Properties 菜单，或直接双击该轨道来访问 Audio Controller 对话框。

Real Time Control 下拉列表让您可以指定用于控制系统的设备。要控制声音输入，您可以指定 Sample Threshold 和 Oversampling 率。您还可以为每个轴设置 Base Point 和 Target Point 值。Channel 选项让您可以指定使用的通道：Left、Right 或 Mix。

## Part VIII: Advanced Animation Techniques

## FIGURE 34.18

Audio Controller 对话框让您根据声音文件的振幅更改值。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_913_0.png)

## Motion Clip Slave controller

Motion Clip Slave 控制器让在 Motion Mixer 中加载并定义的链接 motion clip 控制对象的变换。

## Motion Capture controller

Motion Capture 控制器允许您使用外部设备（如鼠标、键盘、操纵杆或 MIDI 设备）控制对象的变换。此控制器与 Motion Capture 实用程序配合使用以捕获运动数据。

在将 Motion Capture 控制器分配给轨道后，右键单击该轨道并从弹出菜单中选择 Properties 以打开图 34.19 所示的 Motion Capture 面板。此对话框让您选择用于控制轨道值的设备。选项包括 Keyboard、Mouse、Joystick 和 MIDI 设备。

## FIGURE 34.19

Motion Capture 控制器让您使用外部设备控制轨道值。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_913_1.png)

## Chapter 34: Using Animation Layers, Modifiers, and Complex Controllers

对于 Keyboard 控制，Keyboard Input Device rollout 会出现，如图 34.20 所示。Assign 按钮让您选择要跟踪的键。其他设置控制 Envelope Graph，该图定义了按键按下被跟踪的速度。

Motion Capture 对话框仅定义哪个设备控制哪个值。实际的数据捕获由 Motion Capture 实用程序完成。在 Utility 面板中选择 Motion Capture 实用程序会显示 Motion Capture rollout。该 rollout 包含用于启动、停止和测试数据捕获过程的按钮。

## FIGURE 34.20

Keyboard Input Device rollout 让您选择捕获哪个按键。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_914_0.png)

在使用 Start、Stop 和 Test 按钮之前，您需要从 Tracks 列表中选择要捕获的轨道。Record Range 部分让您设置 PreRoll、In 和 Out 值，即包含的帧号。您还可以设置每帧的采样数。Reduce Keys 选项在启用时可移除不必要的键。

## Tutorial: Drawing with a pencil with the Motion Capture controller

一些动作，如用铅笔作画，是我们手部的自然动作，但在尝试使用关键帧进行动画时变得非常困难。本教程使用 Motion Capture 控制器和实用程序来为用铅笔作画的自然动作制作动画。

要为铅笔在纸上作画制作动画，请按以下步骤操作：

- 1. 打开 DVD 上 Chap 34 目录中的 Drawing with a pencil.max 文件。该文件包含一个放置在纸上的铅笔对象。
- 2. 选择铅笔对象，打开 Motion 面板，并选择铅笔对象的 Position track。然后单击 Assign Controller 按钮，并双击 Position Motion Capture 选择。Motion Capture 对话框打开。
- 3. 单击 X Position 按钮，并双击 Mouse Input Device 选择。然后单击 Y Position 按钮，并再次双击 Mouse Input Device 选择。在 Mouse Input Device rollout 中，选择 Vertical 选项。这将 X Position 设置为水平鼠标移动，Y Position 设置为垂直鼠标移动。关闭 Motion Capture 对话框。

## Part VIII: Advanced Animation Techniques

- 4. 打开 Utilities 面板，并单击 Motion Capture 按钮。在 Motion Capture rollout 中，选择 Position track，并准备好移动鼠标。然后在 Record Controls 部分单击 Start 按钮，并像用鼠标作画一样移动鼠标。铅笔对象会随着鼠标移动在视口中移动。

Motion Capture 实用程序为每一帧创建一个关键帧。当达到第 100 帧时，它会停止捕获运动。

- 5. 单击 Play Animation 按钮（或按 / 键）查看结果。

图 34.21 显示了 Motion Capture 控制器计算完所有帧后的场景。

## FIGURE 34.21

Motion Capture 控制器和实用程序让您可以使用鼠标、键盘、操纵杆或 MIDI 设备进行动画制作。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_915_0.png)

## Quaternion (TCB) controller

Quaternion (TCB) 控制器产生与 Bézier 控制器类似的曲线动画路径，但它使用 Tension、Continuity 和 Bias 值来定义其曲率。此控制器的好处是它能够在不出现万向节锁问题的情况下旋转对象，而万向节锁在使用 Euler XYZ 控制器时可能会发生。万向节锁可能发生在两个旋转轴对齐时，导致对象失去一个自由度。

此控制器的参数显示在单个 Key Info rollout 中。与 Bézier 控制器 rollout 类似，Quaternion (TCB) 控制器 rollout 包括箭头和 Key、Time 和 Value 字段。它还包括 TCB 值的图表；红色加号代表当前关键帧的位置，而图表的其余部分以黑色加号显示时间的常规增量。更改图表下方字段中的 Tension、Continuity 和

Bias 值会改变其形状。右键单击轨道并从弹出菜单中选择 Properties 会打开图 34.22 所示的 TCB 图表对话框。

## Chapter 34: Using Animation Layers, Modifiers, and Complex Controllers

## FIGURE 34.22

此对话框显示由 Tension、Continuity 和 Bias 值定义的曲线，并让您控制该曲线。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_916_0.png)

Tension 值控制曲率的量：高 Tension 值会在关键帧进入和离开时产生直线，低 Tension 值会产生圆润的曲线。Continuity 值控制曲线在关键帧周围的连续性或平滑度。默认值 25 会产生最平滑的曲线，而高和低 Continuity 值会在顶部或底部产生尖锐的形状。Bias 值控制曲线进入和离开关键点的方式，高 Bias 值会在关键帧右侧产生凸起，低 Bias 值会在左侧产生凸起。

Ease To 和 Ease From 值控制接近或离开关键帧的速度。

### Note

通过在 Motion 面板中单击 Trajectory 按钮启用轨迹路径，您可以在 Key Info rollout 中进行更改时看到路径的变化。

图 34.23 显示了分配给对象 Position track 的三个 TCB 曲线。

### Note

一些控制器通过 Animation 菜单分配，其他则通过 Assign Controller 对话框分配。如果找不到特定控制器，请同时查看两者。

## FIGURE 34.23

TCB 控制器提供了一种不同方式来处理曲线。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_916_1.png)

