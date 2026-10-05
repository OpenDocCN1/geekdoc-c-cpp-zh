

让我们逐节回顾这一部分：

- 1. `Instantiate()` 是一个内置方法，用于为特定的制体创建 GameObject 实例。在这种情况下，它将根据子弹制体创建一个子弹。由于 `Instantiate()` 返回类型为 `Object`，结果必须强制转换为 `GameObject`。

- 2. 子弹的位置被设置为发射器的位置 —— 稍后你将为枪管设置发射器。

- 3. 由于子弹上挂载了 `Rigidbody`，你可以指定它的速度让子弹以恒定速率移动。方向由挂载此脚本的对象的 `transform` 决定 —— 你将把它挂载到太空陆军的身上，确保子弹的飞行方向与陆军士兵的方向一致。

**保存并返回 Unity。** 在 Hierarchy（层级面板）中，展开 SpaceMarine GameObject 并选择 **BobbleMarine-Body** GameObject。

在 Inspector（检器面板）中，点击 **Add Component** 按钮，在组件列表的底部附近选择 **Scripts**。从脚本列表中选择 **Gun**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_91_0.png)

你会发现你的脚本组件已经添加到陆军的身上。你还会注意到有两个新字段：**Bullet Prefab**（子弹制体）和 **Launch Position**（发射位置）。这些听起来熟悉吗？

点击 **Bullet Prefab** 旁边的圆圈。在 Select GameObject 对话框中，点击 **Assets** 选项卡。从生成的列表中选择 **Projectile**。现在你已经加载了子弹，只需要设置发射位置即可。

# Unity 游戏教程

## 第三章：组件

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_92_0.png)

在 Hierarchy 中，在 PC 上按住 **Alt** 键或在 Mac 上按住 **Option** 键，点击 **BobbleMarine-Body** 旁边的**收起三角形**。你会看到一个子 GameObject 列表。寻找 **Gun**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_92_1.png)

**选择**该 **GameObject** 并点击 **Create** 按钮。选择 **Create Empty Child** 并将其重命名为 **Launcher**。这个新的 GameObject 位于枪管的中心，代表子弹生成的位置 —— 如果你想调整生成位置，可以随心在场景中移动它。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_92_2.png)

保持所有 GameObject 展开状态并选择 **BobbleMarine-Body**，以便 Inspector 显示所有组件。将新的 **Launcher**-GameObject 拖入 Gun 组件的 **Launch Position** 字段中。

注意，当你将 GameObject 添加到 transform 字段时，Unity 会自动找到并引用挂载的 transform。

正式搞定！陆军的枪已经上好膛并准备就绪。剩下的就是射击代码了。

raywendlich.com

93

Unity 游戏教程

第三章：组件

幸运的是，这非常简单。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_93_0.png)

切回代码编辑器并打开 `Gun.cs`。

当用户按下鼠标按钮时枪应该射击，当用户松开按钮时停止。

你可以简单地在 `Update()` 中检查按钮是否被按下，如果是则调用 `fireBullet()`。由于 `Update()` 每帧都会被调用，这意味着你的太空陆军每秒将射击 60 次！我们的太空陆军可以射得快，但没那么快。

你需要在它们之间设置一个微小的延迟。为了实现这一点，在 `Update()` 中添加以下代码：

使用 `Input.GetMouseButton(0)` 检查左键是否按下，如果是则调用 `InvokeRepeating()`。

> 注意：如果你想检查右键，可以传入 1；对于中键，可以传入 2。

`InvokeRepeating()` 需要一个方法名称、开始时间和重复频率，直到调用 `CancelInvoke()`。

raywendlich.com

94

在该代码之后，添加以下内容：

```csharp
if (Input.GetMouseButtonUp(0))
{
    CancelInvoke("fireBullet");
}
```

这段代码让用户松开鼠标按钮时停止射击。
**保存**工作并返回 Unity，然后**运行**游戏。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_94_0.png)

按住鼠标按钮。你有子弹打了！

## 接下来做什么？

到目前，你应该对 Unity 更加熟悉了。你有一个会走的陆军。你学习了：

- **组件**以及它们如何赋予 GameObject 行为。
- **脚本**以及如何使用脚本创建自定义行为。
- **管理器**以及如何从代码访问它。
- **游戏窗口**以及如何测试你的游戏。

## 第四章：物理

物理是你将学习的主题之一。在本章中，你将学习 Unity 如何工作。

## 入

碰撞器（Collider）具有多种功能。它们允许你定义 GameObject 用于碰撞的边界，并有助于防止 GameObject 掉落地。

通常对于碰撞器，你会使用原始形状，如球体和箱体。例如，我们将创建一个与外星大小相当的球体。它不会完美匹配外星的形状，但对于碰撞检测目的来说，这通常是“足够”的。如果你需要更精确的碰撞检测，可以使用网格碰撞器（mesh collider）——我们稍后会详细介绍。

首先，让我们阻止那个外星人掉下地板。

在 Hierarchy 中选择 Alien GameObject，点击 Inspector 中的 **Add Component** 按钮。选择 Physics 类别，从组件列表中选择 **Sphere collider**。

你会看到该碰撞器及其许多选项出现在 Inspector 中。

| Edit Collider | |
|---|---|
| Is Trigger | None (Physics Material) |
| Material Center | X 0 Y 0 Z 0 |
| Radius | 0.5 |

