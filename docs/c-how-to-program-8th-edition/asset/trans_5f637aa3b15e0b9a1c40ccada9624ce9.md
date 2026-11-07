
底部墙壁在 *y* 方向上相距 140 个单位。我们给两者都设置 5 个单位的宽度。这个宽度是任意值。你可以更改宽度，让游戏看起来符合你的期望。如果更改这个宽度，你还必须更改碰撞检测代码——当我们讨论碰撞逻辑时，你就会明白为什么。为了让左右墙壁在顶部和底部墙壁之间延伸，它们必须长 145 个单位（140 加上每面墙的半宽）。因此，左右墙壁的 *x* 缩放因子是 1.45。左右墙壁的宽度也设为 5 个单位，并在 *x* 方向上相距 185 个单位。为了让顶部和底部墙壁在左右墙壁之间延伸，它们必须长 195 个单位，因此它们的 *y* 缩放因子是 1.95。

## 添加文本

我们使用 Ogre Overlay 将游戏分数显示为文本。Overlay 指你希望在场景的 3D 元素之上渲染的任何内容。在本章中，我们仅将 Overlay 用于文本。Overlay 由保存在 `.overlay` 文件中的脚本定义。

Overlay 由 OverlayElement 组成。Overlay 中的第一个元素必须是 OverlayContainer。OverlayContainer 可以容纳任何类型的 OverlayElement。TextAreaOverlayElement 保存将显示在屏幕上的文本。Overlay 中的每个对象都有三个主要属性——度量模式、位置和大小。位置由对象的左上角确定，并且始终相对于该对象的父 OverlayContainer。大小由宽度和高度确定。度量模式决定对象如何定位和确定大小。像素模式将根据以像素声明的宽度和高度来确定对象大小。相对模式将相对于父 OverlayContainer 的大小（如果是最外层 OverlayContainer，则为窗口）来定位和确定对象大小。在相对模式下，大小和位置值的范围为 0.0 到 1.0——可以把它看作父 OverlayElement 大小的百分比。如果将元素定位在 (0.0, 0.0)，它将位于父元素的左上角；(0.5, 0.0) 将位于顶部横向 50% 处。

为了显示分数，我们创建一个 Overlay（图 27.14）。第 2 行将 Overlay 命名为 Score。单个 overlay 文件可以包含多个 overlay 定义。Ogre 将通过名称而不是文件来引用每个 Overlay。Overlay 的 *z* 顺序（第 5 行）用于定义该 Overlay 应渲染在什么之上。使用多个 Overlay 时，*z* 顺序较高的 Overlay 将渲染在 *z* 顺序较低的 Overlay 之上。第 8–58 行创建一个 PanelOverlayElement 容器，其中包含两个 TextAreaOverlayElement。该 OverlayContainer 位于屏幕左上角（第 13–14 行），并沿整个宽度延伸（第 17 行）。该容器高度为窗口高度的 10%（第 18 行）。第一个 TextAreaOverlayElement（第 21–38 行）位于容器顶部，距左侧 5%，宽度为容器的一半，高度与容器相同（第 28–31 行）。另一个 TextAreaOverlayElement（第 40–57 行）位于容器顶部横向 69% 处，并延伸到末端。TextAreaOverlayElement 还声明要使用的字体（由 PongResources 文件夹中的 `.fontdef` 文件里的脚本定义）、字符高度、字体颜色（注意英式拼写“colour”）以及 section（第 34–37 行和第 53–56 行）。

```text
52    // set font used for caption and set the size and color
53    font_name BlueBold
54    char_height 0.05
55    colour 1.0 0 0
56    caption Player 2 Score: 0
57  }
58 }
59}
```

**图 27.14** | 用于显示分数的 Overlay 脚本。（第 2 部分，共 2 部分。）

Pong 类的第 115–117 行（图 27.5）在屏幕上显示分数。我们使用 OverlayManager 类的静态成员函数 getString 获取指向 OverlayManager 对象的指针。我们使用该对象获取指向分数 Overlay 的指针，然后调用 show 函数将其显示在屏幕上。当玩家得分时，我们需要更新 Overlay 中的文本以反映变化（第 192–210 行）。首先创建新文本。然后从 OverlayManager 获取指向相应 TextAreaOverlayElement 的指针，并使用 TextAreaOverlayElement 成员函数 setCaption 替换文本。

图 27.15 是定义 BlueBold 字体的 `.fontdef` 文件。第 2 行给字体指定一个 Ogre 将引用的名称。第 5 行告诉 Ogre 它是什么类型的字体。TrueType 是一种常见的字体文件格式（`.ttf` 文件）。源文件（第 8 行）是包含字体的文件。我们将 `.ttf` 文件放在与 `.fontdef` 文件相同的文件夹中。如果将这两个文件放在不同位置，你必须在第 8 行指定 .ttf 文件的路径，或者将包含 .ttf 文件的文件夹添加为资源位置（在 27.4.8 节中讨论）。

```text
 1    // define the BlueBold font
 2    BlueBold
 3    {
 4      // define the font type
 5      type truetype
 6
 7      // set the source file for the font
 8      source bluebold.ttf
 9
10      // set the font size
11      size 16
12
13      // set the font resolution (96 is standard)
14      resolution 96
15    }
```

**图 27.15** | BlueBold 字体定义脚本。

### 27.4.4 动画与计时器

既然我们已经知道如何在屏幕上绘制球，那么让它动起来并在屏幕上移动就很简单了。函数 moveBall（图 27.8，第 54–108 行）使 Ball 在屏幕上移动。在大多数 Pong 游戏中，球可以沿许多不同角度运动。然而，由于我们刚开始使用 Ogre，我们希望尽可能保持简单。因此，在我们的 Pong 游戏中，球只有四个可能的运动方向：向右下、向右上、向左下和向左上——它们都与程序中的 x 轴和 y 轴成 45 度角。

第 56 行实际使 Ball 移动；该函数的其余部分控制与场景中各种对象的碰撞，我们很快就会看到。translate 函数接受一个 Vector3 作为参数，这是 Ogre 定义的三维向量。该向量表示移动 Ball 的方向和距离。我们将 Ball 的方向乘以要移动的距离（速度 × 时间）传递给 translate 函数，以确定最终向量。speed 参数是球每秒移动的单位数。time 参数是自上次移动 Ball 以来经过的秒数。我们稍后就会看到它从何而来。默认情况下，SceneNode 平移在父空间中完成。这意味着节点相对于其父节点的位置和方向（即节点面向的方向）进行平移。通过向 translate 函数添加另一个参数（TS_LOCAL 或 TS_WORLD），也可以在世界空间或局部空间中执行平移。世界空间中的平移是相对于场景原点 (0, 0, 0) 完成的。局部空间中的平移是相对于节点原点（无论节点位于何处以及面向哪个方向）完成的。

为了持续在屏幕上移动 Ball，每次渲染新帧时都调用 moveBall 函数。图 27.4 定义了 Pong 类，这是我们游戏的主要驱动类，它继承自 Ogre 类 FrameListener。FrameListener 是处理 Ogre::FrameEvents 的类。每当一帧开始或结束时，都会发生一个 FrameEvent。每个 FrameListener 都有两个函数：frameStarted 和 frameEnded（第 29–30 行）。这两个函数都返回 bool。Ogre 会持续渲染帧，直到其中一个函数返回 false。我们使用 frameStarted 函数（图 27.5，第 271–295 行）控制 Ball 的动画，具体是第 278 行。Ogre 在渲染每个新帧之前调用此函数。在每一帧之前，frameStarted 函数调用 Ball 类的成员函数 moveBall，从而持续在屏幕上移动 Ball。如前所述，控制动画速度对于创建平滑运动至关重要。帧率（即场景重绘的速度）在不同机器上可能差异很大，因此 Ball 在每台机器上的移动速度可能不同。因此，我们将 FrameEvent 的数据成员 timeSinceLastFrame（以秒为单位）传递给 moveBall 函数。我们将此时间乘以 Ball 的速度，以确定 Ball 应在屏幕上移动的距离。这是使用计时器控制动画的一个示例。

### 27.4.5 用户输入

现在我们讨论使用 Paddle 类的 movePaddle 函数（图 27.11，第 37–46 行）在屏幕上上下移动 Paddle。为了移动 Paddle，我们再次使用 SceneNode 函数 translate（第 39 行）。我们不是基于时间移动 Paddle，而是基于来自键盘的用户输入移动它。用户通过按相应按键指定方向（向上或向下），Paddle 便相应移动。然后该方向作为 Vector3 传递给 movePaddle。

Ogre 不直接支持来自键盘、鼠标或操纵杆等设备的用户输入。Ogre SDK 确实附带面向对象输入系统（OIS）来处理用户输入。使用 Ogre 时并不要求使用 OIS 处理输入，但这是一个好选择。

我们需要创建 InputManager、Keyboard 和 KeyListener 来处理用户输入并控制对 movePaddle 的调用。InputManager 用于创建
