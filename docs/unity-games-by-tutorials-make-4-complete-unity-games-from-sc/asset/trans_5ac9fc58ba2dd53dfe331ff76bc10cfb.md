

# 添加声音

游戏大部分设置已经完成，现在只需要一点音效。

打开 Robot 脚本，并在顶部添加以下内容：

```
[SerializeField]
private AudioClip deathSound;
[SerializeField]
private AudioClip fireSound;
[SerializeField]
private AudioClip weakHitSound;
```

保存更改并返回 Unity。通过 Shift+点击（或在 Mac 上使用 Command+点击）在 Resources 文件夹中选择 YellowRobot、RedRobot 和 BlueRobot 预制，并将 Fire Sound（射击声）设置为 `missile`，Death Sound（死亡声）设置为 `deadRobot`，Weak Hit Sound（命中声）设置为 `weakHit`。

打开 Robot 脚本，在 `Fire()` 函数的右括号之前添加以下代码，以播放射击声：

```
GetComponent<AudioSource>().PlayOneShot(fireSound);
```

现在，更新 `TakeDamage()` 来播放一些声音。将 `if (health <= 0)` 替换为以下内容：

```cs
if (health <= 0)
{
    isDead = true;
    robot.Play("Die");
    StartCoroutine("DestroyRobot");
    GetComponent<AudioSource>().PlayOneShot(deathSound);
}
else
{
    GetComponent<AudioSource>().PlayOneShot(weakHitSound);
}
```

保存文件并返回 Unity。开始开火吧，你将听到很多声音！

# 接下来该去哪里？

本章的内容就此结束；走到这里你太棒了！如果你在过程中遇到问题，可以随时使用下一章中的初始项目，但尝试自己解决问题总是很有启发性的。

在第 11 章“UI 简介”中，你将通过 UI、更多的音效、更多的动画以及一些调整过的游戏机制（如波次生成）为游戏添加最后的一层润色打磨。

# 第 11 章：引入 UI

作者：Anthony Uccello

在第 10 章“添加敌人”中，你为游戏添加了拾取物、机器人生成器和飞行子弹。现在，是时候添加用户界面 (UI)、波次生成机制、增强的音效和音乐，以及针对正确的机器人使用正确的武器来造成额外伤害的能力了。

在 Unity 4.0 之前，UI 工具非常困难。在大多数情况下，你必须在 `MonoBehaviour()` 内部编写一切，随着你的 UI 复杂性增加，代码也随之增长。坦率地说，Unity 听取了开发者的意见，在多年多年之后，他们在 Unity 4.6 中发布了新的 UI。

# 入门

在第 9 章“制作第一人称射击游戏”中，你创建了一个名为 GameUI 的画布（Canvas）。画布是所有 UI 元素的根对象。你覆盖画布（overlay canvas），但还有其他选项。例如，世界空间（world space）允许你创建可以在游戏中直接访问的界面！想象一下《毁灭战士 3》中的计算机终端即可。

要让画布有用，你需要控件，而 Unity 提供了许多控件。最常见的 UI 元素是 Image（图像）、Button（按钮）和 Text（文本）。

# Unity 游戏教程

画布由一个巨大的白色方框表示——你会发现它巨大！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_297_0.png)

这是因为画布假设屏幕上的一个像素是 Unity 内部的一个单位。可以使用 **canvas scaler**（画布缩放器）更改画布的像素密度。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_297_1.png)

缩放器有一个 **UI Scale Mode**（UI 缩放模式）属性，带有有趣的选项：

- **Constant Pixel Size**（固定像素大小）意味着无论屏幕大小如何，UI 元素的大小相同。
- **Scale with Screen Size**（随屏幕大小缩放）意味着 UI 元素随屏幕一起变大。
- **Constant Physical Size**（固定物理尺寸）意味着无论屏幕大小或分辨率如何，UI 元素始终保持相同。

这个组件决定了你的 UI 在不同屏幕尺寸和分辨率下的外观。在本章中，将使用默认值。虽然画布共享相同的空间，但你可以有效地忽略它。像任何其他 GameObject 一样，你始终可以禁用它以保持整洁的“桌面空间”。

Image 是一个 UI 对象类，允许你通过 **Sprite**（精灵）在屏幕上渲染图像。逻辑上显而易见，**Text** 允许你在屏幕上渲染文本。**Button** 允许你配置悬停和点击事件。你将在整个教程中使用这些功能。

所以你可能在好奇控件是如何放置的？Unity 使用 **anchors**（锚点），它们看起来像彼此指向的箭头。

Unity 游戏教程
第 11 章：引入 UI

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_298_0.png)

锚点的作用就像现实生活中的锚：它将某个物体固定在位置。如果你想将 UI 元素放置在左上角，并始终相对于该左上角，你只需要将其锚点设置为左上角即可。

锚点还可以拉伸控件。如果你希望控件根据屏幕尺寸扩展或收缩，这非常有用。锚点会分解成单个箭头以形成一个矩形。这允许你定义拉伸的大小。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_298_1.png)

在谈论锚点时，理解 **pivot**（心点）至关重要。心点是 Image 上应用位置的点，它是锚点用于保持物体在正确位置的依据。心点是 Image 上应用位置的点，它是锚点用于保持物体在正确位置的依据。如果你想将 UI 元素放置在左上角，并始终相对于该左上角，你只需要将其锚点设置为左上角即可。心点是 Image 上应用位置的点，它是锚点用于保持物体在正确位置的依据。心点是 Image 上应用位置的点，它是锚点用于保持物体在正确位置的依据。心点是归一化坐标，这意味着对于 (0,0) 是左下角，(1,1) 是右上角。心点是归一化坐标，这意味着对于高度和宽度都是 0 到 1。心点由蓝色圆圈表示：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_298_0.png)

在整个教程中，你会使用这些功能。为了设置位置，![](img/fd5c2ca20ea33da76d2b61297cc57f6c_299_1.png)

Rect Tool 是 2D 操作的瑞士军刀。它允许你缩放、旋转甚至重置点。

# 添加 UI 元素

你将在第 10 章“添加敌人”中创建了 GameUI。选择 GameUI 对象，在层级面板（Hierarchy）中右键点击，选择 **UI** ▸ **Image**，并将其命名为 **BottomBar**。选择图像并查看检查器。你会发现它发生了变化。

位置属性被一组专门为 UI 设计的新属性取代了。这就是 **Rect Transform**。

当你要在代码中设置控件的位置时，使用 RectTransform 而不是普通的 Transform。

为了将此图像位于屏幕的左下角，点击 **anchor presets**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_300_0.png)

你会得到一组对应屏幕位置的选项。在底部和右侧，你也会看到预设。

### Anchor Presets（锚点预设）
Shift: Also set pivot Alt: set position

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_300_1.png)

将 Pivot 设置为 (0, 0)，Pos 设置为 (-40, -50, 0)，Width 设置为 520，Height 设置为 100，Source Image 设置为 Pink_Grey_Texture。

你将在画布的左下方得到这样一个图像：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_301_0.png)

> 注意：由于这是一个叠加 UI，将场景视图切换到等轴测模式（Isometric）很有帮助。在场景视图中，只需点击坐标轴中心的立方体即可切换模式，然后再次点击返回透视模式（Perspective）。

Pos 字段相对于锚点工作。在你的案例中，你将 PosY 设置为 -50。这的效果是将图像从画布的左下角向下移动 50 单位。

