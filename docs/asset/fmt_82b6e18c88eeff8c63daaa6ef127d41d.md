
问题在于：游戏每当开火时都会创建一个新的 `GameObject`。由于玩家可以持续射击，这将导致子弹越来越多，直到最终你的游戏内存耗尽并崩溃。错误地创建无限制的子弹是游戏设计中的一个常见问题。

你可以删除子弹，也可以使用**对象池（pools）**来复用它们。例如，在 `GameObject` 离开游戏区域后，它会被放入对象池中供以后使用，而不是被删除。

当玩家再次射击时，游戏会检查池中是否有可用的子弹。如果没有，游戏将创建一个新子弹。否则，它将复用现有的子弹。一段时间后，游戏将复用子弹，而不是在创建和删除子弹上浪费处理时间。

在本章中，为了简单起见，你将删除对象，但如果性能成为问题，你可能想要研究对象池。有关对象池的更多信息，请查看 https://www.raywender.com/13609j/object-pooling-unity

在项目浏览器（Project Browser）中，打开 **Prefabs** 文件夹并选择 **Projectile** 制体。点击 **Add Component** 按钮并选择底部的 **New Script**。将其命名为 **Projectile**，然后点击 **Create** 和 **Add**。别忘记将脚本移动到 **Scripts** 文件夹以保持整洁。

双击脚本在编辑器中打开它，并添加以下两个方法：

```csharp
private void OnBecomeInvisible()
{
    Destroy(gameObject);
}

private void OnCollisionEnter(Collision collision)
{
    Destroy(gameObject);
}
```

`OnBecomeInvisible()` 是非常有用的方法，当对象不再被任何相机看到时会被调用。在这种情况下，当子弹飞出屏幕时调用。这是销毁子弹的完美时机，因为它不再需要了。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_107_0.png)

注意：关于这一点有两点重要的需要理解。

首先，为了这项工作，`GameObject` 必须挂载一个渲染组件（renderer component）。否则，Unity 不知道 `GameObject` 是否不可见。

其次，如果一个 `GameObject` 从所有相机来看都是不可见的，Unity 就认为它是不可见的。例如，`GameObject` 可能在 Game（游戏）窗口中可见，但如果它在你的 Scene（场景）视图中可见，那么它仍然被视为可见。

很奇怪吗？是的，但 Unity 就是这么运行的。:)

`OnCollisionEnter` 在碰撞事件期间被调用。`Collision` 对象包含了实际碰撞的信息以及目标对象的信息。例如，当子弹击中外星人或墙时会调用此方法。当这种情况发生时，你只需销毁子弹即可。

现在运行你的游戏并射击。你的子弹在碰撞对象时会消失。再做另一个测试如何？

在游戏仍运行时，选择 SpaceMarine `GameObject`。在 Character Controller（角色控制器）组件中，将 Radius（半径）设置为 5.17。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_108_0.png)

现在，开火。信你不信，枪正在射击，但子弹击中了陆战陆战队员的碰撞器（collider），然后被立即销毁，所以看起来好像什么都没有发生。你可以通过使用图层设置选择性碰撞来解决这个问题。

## 设置碰撞和图层

默认情况下，所有的 `GameObject` 都存在于一个物理层上。这意味着所有带有 `Rigidbody`（刚体）的 `GameObject` 都会相互碰撞。

从子弹与陆战队员发生碰撞中可以看出，默认设置并不是理想的。你需要子弹忽略该陆战队员——为了做到，你需要创建一个新的图层。

首先，停止游戏并导航到 `Edit > Project Settings > Tags and Layers`。检查器（Inspector）将显示 Tags 和 Layers 视图，并展开图层部分。前八层由 Unity 控制，但其余层级是完全开放的。

有一个名为 PostProcessing 的层，用于添加后期处理效果，如抗锯齿、深度场和运动模糊。（等等，这里的文本乱序了，让我们根据 Unity 标准进行重构）：

首先，停止游戏并导航到 `Edit > Project Settings > Tags and Layers`。检查器将显示 Tags 和 Layers 视图，并展开图层部分。前八层由 Unity 控制，但其余层级是完全开放的。

有一个名为 PostProcessing 的层，用于添加后期处理效果。

从第 8 层开始，添加以下内容：

| Tags | Layers |

| :--- | :--- |

| Default | 0 |

| Transparent | 1 |

| | 2 |

| | 3 |

| | 4 |

| | 5 |

| | 6 |

| | 7 |

| PostProcessing | 8 |

| Alien | 9 |

| Column | 10 |

| Floor | 11 |

| Head | 12 |

| Player | 13 |

| Wall | 14 |

| | 15 |

| | 16 |

| | 17 |

(注：由于原文文本在表格部分存在严重乱码，此处已根据 Unity 逻辑进行了对齐)

y 轴显示主体图层，x 轴显示目标图层。勾选表示主体图层是否会与目标图层产生交互。

在 Bullet 行中，取消勾选 Player 列。现在，Player 层将忽略与 Bullet 的所有交互。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_112_0.png)

# 使用关节连接 GameObjects

当你刚开始制作这个游戏时，你称它为“摇摇头大战”（Bobblehead Wars），但到目前为止，它只有战争，完全没有“摇晃”。坦率地说，Unity 物理系统通过关节（joints）来得救了。

这些并不是那种需要你身处阿姆斯特丹、俄勒冈、科罗拉多州或华盛顿州的关节，也不是电影大师斯派克·李（Spike Lee）制作的那种关节。

这些是具有常规用途的物理关节：在物理引擎定义的关系中将 `GameObjects` 连接在一起。

想一下撞击球——具体来说就是链条。每一个环都是一个 `GameObject`，你需要用关节将它们连接起来，允许每个环独立移动但会影响其邻居，反之，整个组都会受到球的影响。

你有许多关节可以使用：

- 旋转**转轴关节 (Hinge joint)** 将一个 `GameObject` 的运动绑定到另一个上——例如门铰链。

- **弹簧关节 (Spring joint)** 像两个 `GameObjects` 之间的一个隐形弹簧。

- **固定关节 (Fixed joint)** 用一个无关的 `GameObject` 限制另一个 `GameObject` 的运动。一个很好的例子（甚至在文档中都是）是粘性手榴弹。

- **角色关节 (Character joint)** 允许你约束运动以创建布娃娃（ragdoll）效果。

- **可配置关节 (Configurable joint)** 结合了其他关节的功能以及更多。本质上，你用它来修改现有的关节或创建自己的关节。

你将使用转轴关节来让头部左右摇动。

借鉴上面的例子，太空陆兵的身体是门框，他的头部是门扇。每当陆兵移动时，你都会给他的头部施加力，使其来回弹动。

# 添加关节

在层级面板（Hierarchy）中，选择 SpaceMarine 并选择 BobbleMarine-Head。然后从主菜单点击 `Component\Physics\Hinge Joint`。正如你所看到的，添加组件有多种方法。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_113_0.png)

检查检器（Inspector）。你现在可以在那里看到转轴关节。

为了让转轴关节起，连接的 `GameObjects` 必须带有刚体（Rigidbodies）；当你创建转轴关节时，Unity 会自动为你添加这些。

在 `Rigidbody` 组件中，取消勾选 Gravity（重力）属性。

在层级面板中选择 BobbleMarine-Body，并在检器中点击 Add Component（添加组件）按钮。从组件列表中选择 Physics（物理），然后选择 `Rigidbody`。点击预设（preset）按钮并选择 kinematic（运动学）。记住，这个预设会取消勾选重力并将 `Rigidbody` 设为运动学模式。

现在，在层级面板中选择 BobbleMarine-Head，查看检器中的转轴关节。你会看到很多选项！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_114_0.png)

第一个选项是 Connected Body（连接体），在这种情况下，它是头部将“铰链”连接在上面的另一个 `GameObject`。

在层级面板中，将 BobbleMarine-Body 拖到 Connected Body 属性上。现在，游戏通过物理连接连接了。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_114_1.png)

Anchor（锚点）表示关节端点在指定 `GameObject` 局部坐标空间的位置。头部坐标空间内的 (0, 0, 0) 代表颈部区域，将值保持在 (0, 0, 0) 即可。

Axis（轴）决定了物体将摆动的方向，即向上和向下。你想在 z 轴上移动它，即通过将 Axis 设置为 (0, 0, 1)。

Connected Anchor（连接锚点）指定关节另一端的锚点。如果 Connected Rigidbody 为空，此值位于场景坐标系。然而，当设置了 Connected Rigidbody 时，它指向陆兵身体的空间。

默认情况下，Unity 将 Connected Anchor 点设置为与 Anchor 点相同的位置。对于这个游戏，你希望这些值略有不同，所以取消勾选 Auto Connected Anchor。

确定连接锚点的最佳设置往往需要尝试。坦率地说，Unity 显示了你可以作为起始点的锚点位置。

将场景视图切换到线框模式（Wireframe）显示一条橙色线。这代表了锚点的位置，当你更改 Connected Anchor 时它会更新。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_115_0.png)

将 Connected Anchor 设置为 (0, 0, 0) 以将其固定在颈部。

Spring（弹簧）属性将为关节添加“弹簧”行为，Motor（电机）属性将让关节在没有任何外力的情况下移动。

Limits（限制）控制关节摆动的幅度。

勾选 Limits 复选框并展开 Limits 属性。在 Min 属性中输入 -25，并将 Max 设置为 25——这表示头部最多摆动 25 度。为了让头部产生正确的摇晃，将 Bounciness（弹性）设置为 1——这是最大值。

保持其余值不变，但注意 Break Force（断裂力）和 Break Torque（断裂扭矩）。如果你想要头部在某个阈值下断开，可以使用这些。例如，创建一个门被吹飞的效果。

这是配置好的关节：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_116_0.png)

Unity 游戏教程

第 4 章：物理

在层级面板（Hierarchy）中选择 BobbleMarine-Head。在检器（Inspector）中，为其分配 Head 层，并在确认对话框中选择“Yes, change child”。

最后，点击 `Edit\Project Settings\Physics`，在物理矩阵（physics matrix）中，取消勾选 Head行的 Player 列。

| | TransparentFX | Ignore Raycast | Water | Alien | Alien Head | Bullet | Column | Floor | Head | Player | Wall | Upgrade |

| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |

| Default | | | | | | | | | | | | |

| TransparentFX | ☑ | | | | | | | | | | | |

| Ignore Raycast | ☑ | | | | | | | | | | | |

| Water | ☑ | ☑ | | | | | | | | | | |

| UI | ☑ | ☑ | | | | | | | | | | |

| Alien | ☑ | ☑ | | ☑ | | | | | | | | |

| Alien Head | ☑ | ☑ | | ☑ | ☑ | | | | | | | |

| Bullet | ☑ | ☑ | | ☑ | ☑ | ☑ | | | | | | |

| Column | ☑ | ☑ | | ☑ | ☑ | ☑ | ☑ | | | | | |

| Floor | ☑ | ☑ | | ☑ | ☑ | ☑ | ☑ | ☑ | | | | |

| Head | ☑ | ☑ | | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | | | |

| Player | ☑ | ☑ | | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | | |

| Wall | ☑ | ☑ | | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | |

| Upgrade | | |

运行你的游戏。开始吧，这些摇头头战争已经：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_119_0.png)

raywenderlich.com

## 射线检测 (Raycasting)

在此时，你可以发射武器并推开外星人。遗憾的是，我们的英雄仍然无法转身。考虑到这些外星人喜欢啃咬后脑勺（它们确实是外星人），太空陆战员需要躲避、旋转和穿梭。

在游戏过程中，你还希望陆战员朝鼠标指针的方向射击。这听起来很简单，对吧？

从根本上说，这是一个棘手的问题：游戏存在于 3D 空间，但鼠标存在于 2D 空间。

解决方案是将鼠标指针转换为 3D 空间，然后确定它指向哪里。这听起来像是一个复杂的过程，但使用射线检测就非常简单。

射线检测从目标向终点发射一条不可见的射线，并在它击中 `GameObject` 时发送一个通知。你可能会遇到许多与射线相交的 `GameObject`。使用掩码（mask）可以让你过滤掉不需要的对象。

射线检测非常有用，并有多种用途。它们通常用于测试另一个玩家是否被弹药击中，但正如你将看到的，它们也可以帮助你测试鼠标指针下方是否有几何结构。

下面的图片显示了从立方体到锥体的射线检测。由于射线带有锥体掩码，它忽略了 iconsphere 层并向锥体报告击中。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_120_0.png)

你将从相机向鼠标指针发射一条射线。然后太空陆战员将转向射线击中的任何地方，本质上是跟随鼠标。

打开 `PlayerController.cs` 并添加以下实例变量：

```
public LayerMask layerMask;
private Vector3 currentLookTarget = Vector3.zero;
```

## Unity 游戏教程 | 第 4 章：物理

`LayerMask` 允许你指定射线应该击中的哪些层。`currentLookTarget` 是你希望陆战员盯着的地方。由于你不知道游戏开始时该看哪里，所以你将值设为零。

> 注意：随着你添加实例变量，你会发现 public 和 private 变量变得杂乱。这是为了简洁起 way。最佳实践是将它们分组。

接下来，在 `FixedUpdate()` 中添加以下内容：

```csharp
RaycastHit hit;
Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
if (Physics.Raycast(ray, out hit, 1000, layerMask))
{
    currentLookTarget = hit.point;
}
```

# 第5章：管理器与路径寻

作者 Brian Moakley

**摇头娃娃大战 (Bobblehead Wars)** 的进展非常顺利！到目前为止，你已经拥有了一个强壮的太空陆兵，他可以转身、射击并击外星人。此外，通过使用合页关节，他的头部可以左右晃动，这样他就能搞事情了。

尽管如此，*摇头娃娃大战*还没有准备好发布。首先，当太空陆兵预期有一大群敌人时，场景上只有一个外星人。其次，这个外星人目前并不不可怕——他只是在那里站着！

为了解决这个问题，你将学习如何通过管理器（GameManager）和路径寻的力量，随时间生成敌人并让它们追捕太空陆兵。让战斗开始吧！

## 介绍游戏管理器

Unity 将处理特定子系统的对象称为**管理器 (manager)**。根据你的职场经验，你可能认为这意味着他们什么都不做，把所有工作留给下属；但在 Unity 中，管理器实际上会出一份力。

例如，`InputManager`（输入管理器）是一个允许你调整游戏所有控制对象的。还有一个 `SettingsManager`（设置管理器）处理你所有的项目设置，以及一个 `NetworkManager`（网络管理器）用于管理网络游戏的状态。

在本章中，你将创建你自己的管理器。具体来说，你将创建一个管理器，以便在游戏运行时轻松地调整游戏设置。这将使得在游戏测试期间平衡游戏变得容易得多。

想象你正在玩游戏，敌人太多了。太空陆兵毫无机会。你可以对你的游戏管理器进行调整，实时减少外星人群的数量。

记住，你在游戏运行期间所做的任何更改都会丢失，对吧？这个规则有一个例外，你将在本章中尝试它。

## 创建游戏管理器

打开第 4 章“物理学 (Physics)”中的项目。如果你需要重新开始，请找到本章资源中包含的启动项目。
