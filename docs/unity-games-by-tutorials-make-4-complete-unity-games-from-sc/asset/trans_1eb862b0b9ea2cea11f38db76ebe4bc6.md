

在层级（Hierarchy）中，检查 BobbleArena 并查看在 Animator（动画机）窗口中是否有以下内容：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_159_0.png)

你会发现 Walls 动画已经存在于控制器。任何新的动画片段都会自动添加到当前动画控制器中。

每个矩形表示一个动画状态：

- 绿色矩形是动画机的入口点（entry）。
- 橙色矩形表示默认状态；它总是第一个播放。
- 箭头表示状态之间的过渡。

通过向上滚动鼠标轮，你可以放大状态。同样地，向下滚动可以缩小状态。按住鼠标中间滚轮可以在状态之间平移。当屏幕上同时显示很多状态时，这些快捷键非常有用。

运行游戏并移动英雄，直到你能看到墙壁降下。动画会无限循环。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_159_1.png)

# Unity 游戏教程

Walls 动画之所以播放是因为它是被指定的默认状态。它之所以循环是因为这是默认行为。

在播放时观察动画机，查看动画的进度。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_160_0.png)

在 Project（项目）浏览器中，点击 Animations 文件夹并**选择 Walls** 动画。在 Inspector（检查器）面板中，**取消勾选 Loop Time（循环时间）。**

这就是覆盖默认设置——现在没有循环了！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_160_1.png)

遗憾的是，“Walls”并不是一个非常有描述性的名称。点击 Animator 中的 **Walls** 状态并查看检查器以查看所有可用属性。你将在整本书中学习并更改其中的许多属性。

现在，将名称从 **Walls** 改为 **WallsLower**。就这样。

Unity 游戏教程

## 第 6 章：动画

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_161_0.png)

注意该状态反映了更新后的名称。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_161_1.png)

既然你有一个 WallsLower 状态，你需要一个 WallsRaiser 状态。你可以创建一个新动画，由于这个动画与 WallsLower 动画非常相似（相反），我将为你展示一个快捷方法。

在 Animator 中**右键点击**，选择 **Create State（创建状态）**然后选择 **Empty（空）**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_161_2.png)

Unity 游戏教程

## 第 6 章：动画

你现在有一个新的空状态。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_162_0.png)

选择这个新状态并在检查器中将其命名为 WallsRaise。接下来，将 Animations 文件夹中的 Walls 动画拖到 Motion 属性上。最后，将速度设置为 -1。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_162_1.png)

Motion 属性引用实际的动画片段。在这种情况下，你使用的是在 WallsLower 中使用的相同动画片段。Speed（速度）属性允许指定片段播放的速度。将速度设置为 1 表示将以正常速度播放。数字越大，片段运行得越慢；数字越小，运行得越快。

为什么是 -1？负数会反向播放片段。在这种情况下，你正在使用相同的片段并以正常速度反向播放。

你还需要一个状态：一个空闲（idle）状态。打开 Animation 窗口，确保在层级中选择了 BobbleArena。你会在属性列表中看到当前显示动画的名称，它应该是 walls。

点击 Walls 并从下拉列表中选择 **Create New Clip...（创建新片段）**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_163_0.png)

Unity 游戏教程

## 第 6 章：动画

给它命名为 ArenaIdle.anim。就这样——你的动画片段包含一个空动画。虽然你可以创建一个没有关联动画的状态，但 Unity 会执行一些可能会破坏你计划的奇怪操作。有时，稳妥起见为空闲状态创建一个动画片段是有用的，即使它是空的。你的动画机应该像这样：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_163_1.png)

你需要对其进行组织，你将通过过渡（transitions）来实现。

## 动画状态过渡

过渡执行多种功能。它们让你了解动画的流向，但更重要的是，你可以根据条件对它们进行门控。过渡的第一部分是条件，这是你将要设置的下一个内容。

在 Animator 窗口中，**右键点击 ArenaIdle 状态**并选择 **Make Transition（制作过渡）**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_163_2.png)

一条线将跟随你的光标。点击 WallsLower 状态创建该过渡。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_164_0.png)

**注意：** 你可能会发现某个状态不在视图。通过按住鼠标滚轮，你可以在 Animator 中平移找到它。

从 **WallsLower** 到 **WallsRaiser** 创建**新过渡**，然后从 **WallsRaiser** 到 **ArenaIdle** 创建另一个。你的状态看起来应该是这样的：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_164_1.png)

这描述了整个动画流。

在观察动画的同时运行游戏。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_164_2.png)

## 动画状态条件

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_165_0.png)

点击加号并从下拉列表中选择 **Bool**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_165_1.png)

给它命名为 Lowered。虽然你在这里选择了 Bool，但注意菜单有四个选项：Float、Int、Bool 和 Trigger。除了 Trigger 外，它们都对应 C# 中的类型。

Unity 游戏教程

Trigger 是一种独特的条件类型，行为类似于 bool，但在动画后它会自动重置。选择 ArenaIdle 和 WallsLower 之间的**过渡箭头**查看检查器中的混合选项。

**取消勾选 Exit Time（退出时间）**，告诉 Unity 立即结束动画而不是等待结束。否则，Unity 将花费额外时间与下一个动画混合。

在 Conditions 部分，**点击加号**。由于你只有一个参数，Lowered 属性将填充；将其设置为 **true**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_166_0.png)

你之所以这样做是因为当你想要触发动画时会在代码中设置 Lowered 布尔值。一旦在代码中设置了它，动画就会播放。

在运行游戏之前你需要再进行一次微调。在 Animator 窗口中，**右键点击 ArenaIdle**并选择 **Set as Default State（设置为默认状态）**。

## 第6 章：动画

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_167_0.png)

此更改表示 ArenaIdle 是动画控制器的入口状态。为了一眼就能看出关系，请这样组织它们：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_167_1.png)

保持 Animator 打开，再次运行游戏。你会发现墙壁没有落下，因为条件尚未满足。在游戏仍在运行时，在 Animator 中**勾选 Lowered**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_167_2.png)

现在墙壁会下降、上升并循环，除非你取消勾选 Lowered。你需要更多的条件。

停止游戏并选择从 WallsLower 到 **WallsRaise** 的**过渡箭头**。在检查器中，**取消勾 Exit Time**。在 Conditions 部分**点击加号**并将 Lowered 设置为 false。

再次播放并**点击 Lowered**复选框。这次墙壁会落下，但由于新条件它们停在了那里。**取消勾选 Lowered** 让墙壁再次上升。

你现在准备好了动画。是时候在代码中调用它们了！

## 在代码中触发动画

此时，你已经准备好了激活动画的动画片段、动画状态和条件。

接下来，你将使用碰撞器触发（collider trigger）在代码中将一切整合在一起。

在层级中选择 **BobbleArena**，然后点击 **Create（创建）**按钮。从下拉列表中选择 **Create Entity Child（创建实体子）**并命名为 **WallTrigger**。将 **Position（位置）**设置为 **(0, 0, 0)**，并将 **Scale（缩放）**设置为 **(0.5, 0.5, 0.5)**。接下来，点击 **Add Component（添加组件）**按钮，从 **Physics（物理）**类别选择 **Box Collider（刚体碰撞器）**。

在 Box Collider 类别中，勾选 **Is Trigger（触发器）**复选框，将 **Center（中心点）**设置为 **(0, 6.72, -90.6)**，并将 **Size（大小）**设置为 **(250.55, 17.14, 66.7)**。

你应该能在场景视图的后墙处看到一个大触发器。当太空陆战兵进入这个区域时，你想让墙壁落下。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_168_0.png)

要执行操作，选择 **WallTrigger**，然后点击 **Add Component**按钮并选择 **New Script（新脚本）**。将其命名为 **ArenaWall**并点击 **Create and Add（创建并添加）**按钮。

**双击**新脚本进行编辑，并在类内部添加此变量：

```
private Animator arenaAnimator;
```

你可以将其设为公共变量以便在检查器中设置，但这不是必需的。这是因为 WallTrigger 是 BobbleArena 的子级，你可以通过访问 WallTrigger 的父属性并获取相应的组件来获取动画机的引用。

