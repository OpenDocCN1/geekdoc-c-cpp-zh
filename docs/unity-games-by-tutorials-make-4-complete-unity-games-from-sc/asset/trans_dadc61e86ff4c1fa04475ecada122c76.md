

# Unity 游戏教程

现在的问题是 NavMesh 的默认属性适用于较小的代理体。在 Navigation（导航）窗口中，点击 **Bake（烘焙）标签页**。

默认情况下，代理体配置得较大。请配置以下字段：

- **Agent Radius（代理体半径）：** 决定代理体距离障碍物有多近。**将其设置为 1.45。**
- **Agent Height（代理体高度）：** 决定代理体通过的天花板最小高度。**将其设置为 6.2。**
- **Max Slope（最大坡度）：** 决定斜坡变得代理体无法通过的角度。保持原样即可。
- **Step Height（台阶高度）：** 决定台阶变为代理体无法通过的最小高度。**将其设置为 0.73。**

代理体看起来应该是：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_145_0.png)

这些魔法数字是从哪里来的？它们来自你的 NavMesh 代理体设置，即你的外星人。Unity 建议你将值设置为所使用的**最小**代理体的值。

点击 **Bake** 按钮。在完全烘焙后运行游戏。陆战陆军会迅速发现自己成了关注的焦点。

# 调整路径寻

尽管路径寻看起来运行没有问题，但你实际上有一个重大的问题需要解决。每当你为 NavMeshAgent 分配目标时，Unity 都会经过计算通往目标路线的过程。

如果这偶尔发生倒没关系，但请考虑游戏将生成许多外星人，并在每次运行时执行此计算。结合这一事实回顾你的实现。你会发现你正在每帧都计算一次路径寻。

这是不可扩展的——当外星人增多时，会有更多的路径寻计算。最终，你的帧率将会崩溃，并为玩家引发一系列悲性的连锁反应。

在代码编辑器中打开 Alien.cs。在公共变量下，添加以下内容：

```c
public float navigationUpdate;
private float navigationTime = 0;
```

navigationUpdate 是外星人更新路径所需的时间（毫秒计）。navigationTime 是一个变量，用于跟踪自上次更新以来经过了多久。

在 Update() 中，将 `agent.destination = target.position` 替换为以下内容：

```csharp
navigationTime += Time.deltaTime;
if (navigationTime > navigationUpdate)
{
    agent.destination = target.position;
    navigationTime = 0;
}
```

这段代码检查是否已经过了一段时间时间，然后更新路径。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_146_0.png)

回到 Unity。在 Project 视图中，选择 Prefabs 文件夹中的 Alien 预制体。
在 Alien 设置中，将 Navigation Update 字段设置为 0.5。

现在运行你的游戏。你会注意到外星人锁定陆战陆军的速度稍慢了一些，但在大多数情况下，他们都能追上他。

此时，你可能想要调整影响游戏体验和性能的变量，以找到平衡点。测试和对游戏进行分析是找到正确配置的唯一方法！

# 最后完善

你现在有一群外星人正在追捕一名陆战陆军。只剩下最后一件事要做——你需要当陆战陆军把他们炸碎时发生一些事情。

回到代码编辑器中的 Alien.cs，在最后一个闭合括号之前添加以下代码：

```csharp
void OnTriggerEnter(Collider other)
{
  Destroy(gameObject);
}
```

这段代码的作用类似于典型的碰撞代码，不同在于它将碰撞事件变为触发器（trigger）。为什么要用触发器？记住，你将外星人的 Rigidbody 设置为 In Kinematic，因此 Rigidbody 不会响应碰撞事件，因为导航系统在控制。

尽管如此，你可以通过触发事件获取 Rigidbody 跨越 collider 信息。这样你仍然对它们做出响应。在这种情况下，你调用 destroy() 并传入 gameObject，这将删除外星人实例。保存文件并回到 Unity。

选择 Prefabs 文件夹中的 Alien，并在 Inspector 中寻找 Sphere Collider。勾选 Is Trigger 复选框。

此时，任何与外星人碰撞的物体都会杀死它——墙、柱子、陆战陆军等。你需要排除某些碰撞。

选中 Alien 预制体后，将其分配到 Alien 层。当提示是否也将该层应用到所有子对象时，选择“否（仅此对象）”。接下来，在 Project 浏览器中，选择 Prefabs 文件夹中的 BobbleArena-Column。外星人的头部将用于其他物理计算，因此该层最好仅用于父 GameObject。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_147_0.png)

在 Layer 下拉菜单中，将其分配到 Column 层，并在后续的对话框中选择“是（更改子对象）”。

接下来，点击 **Edit Project Settings\Physics**。在碰撞矩阵中，在 Alien 行中取消以下内容的勾选：**Column, Upgrade, Alien Head, Floor, Alien。**

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_148_0.png)

运行游戏，你会注意到外星人锁定陆战陆军的速度稍慢了一些，但在大多数情况下，他们都能追上他。

此时，你可能想要调整影响游戏体验和性能的变量，以找到平衡点。测试和对游戏进行分析是找到正确配置的唯一方法！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_148_1.png)

在 Alien 设置中，将 Navigation Update 字段设置为 0.5。

| Property | Value |
| :--- | :--- |
| Max On Screen | 50 |
| Total Aliens | 50 |
| Min Time | 0 |
| Max Spawn | 3 |
| Per Spawn | 3 |

