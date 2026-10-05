

现在是给你的游戏进行测试了。在编辑器正上方寻找播放控制。点击 Play（播放）按钮。

> 注意：你会发现控制按钮提供了两个额外选项：**Pause（暂停）**和**pause stepper（暂停步进器）**。暂停允许你暂停运行中的游戏。步进器允许你一次一帧地通过动画，这对于调试动画问题特别有用。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_85_0.png)

现在，查看 Game（游戏）窗口并按下方向键或 WASD 键来移动你的角色。看……生命诞生了！

# Game 窗口

Game 窗口是你实际玩游戏的地方。在玩过程中，有两个生死攸关的问题需要记住。

首先，当你开始玩游戏时，界面会变暗，以提供视觉提示说明你正处于播放模式。

其次，当你玩游戏时，你可以更改它的任何内容（包括更改检查器中组件的值），但当你停止运行游戏时，所有的更改都将丢失。这既是祝福也是诅咒。祝福是你有能力在没有任何后果的情况下调整游戏；诅咒是，有时你会忘记自己处于播放模式，继续游戏，然后由于某种原因，游戏停止了。*砰！更改全没了！*

幸运的是，你可以（也应该）让播放模式变得非常明显。在 PC 上选择 **Edit > Preferences** 或在 Mac 上选择 **Unity > Preferences** 来弹出选项列表。

**选择（Select）** **Colors（颜色）**部分。寻找 **Playmode tint（播放模式着色）**。点击旁边的**颜色框**，给它一个显而易见的颜色——比如 1 红色。现在运行你的游戏，看看它是否足够显著。

# 相机移动

太空陆兵的移动只有一个问题：他会滑屏幕。你希望相机跟随英雄环竞技场移动，这样他才不会离开你。

通过一点脚本，你可以让陆兵保持在焦点上。

首先，确保你不在播放模式以停止播放陆兵，再次点击 **play** 按钮。

在 Hierarchy（层级）中，点击 Create 按钮并选择 **Empty（空物体）**。将其命名为 **CameraMount**。

基本思想是，你希望 CameraMount 代表相机应该聚焦的位置，并让相机相对于此位置。初始情况下，你希望相机聚焦在太空陆兵所在，所以让我们配置 CameraMount 位于与陆兵完全相同的位置。要做到这一点，选择 **space marine**，点击 Transform 组件右上角的齿轮按钮，并选择 **Copy Component（拷贝组件）**。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_86_0.png)

现在选择 **CameraMount**，点击 Transform 组件右上角的齿轮按钮，并选择 **Paste Values（粘贴值）**。接下来，将 **Main Camera（主相机）** GameObject 拖入 **CameraMount** GameObject 中。

太了！现在当你移动玩家时，你可以移动 CameraMount 让它随玩家移动，相机就会追踪玩家。你只需要编写一个脚本来实现。

在选中 CameraMount 的情况下，点击 Inspector（检查器）中的 Add Component 按钮并选择 New Script（新建脚本）。将其命名为 CameraMovement 然后点击 Add。

> 注意：当你点击 Add 按钮创建脚本时，Unity 会在 assets 文件夹的根目录下创建脚本。养成一看到资产就将其移动到相应文件夹的习惯。

将你的新文件从 assets 根目录拖入 Scripts 文件夹。双击 CameraMovement 脚本以在你的代码编辑器中打开它。在类定义下方，添加以下变量：

```cs
public GameObject followTarget;
public float moveSpeed;
```

followTarget 是你希望相机跟随的目标，moveSpeed 是它应该移动的速度。通过将这些创建为公共变量，Unity 将允许你在 Unity 编辑器内部中设置这些值，因此你可以将 followTarget 设置为太空陆兵并调整 moveSpeed，你很快就能看到。

在 Update() 中添加以下内容：

```cs
if (followTarget != null)
{
    transform.position = Vector3.Lerp(transform.position,
    followTarget.transform.position, Time.deltaTime * moveSpeed);
}
```

这段代码检查是否有可用目标。如果没有，相机就不会跟随。接下来，调用 Vector3.Lerp() 来计算 CameraMount 所需的移动。

Lerp() 接受三个参数：3D 空间中的起始位置、3D 空间中的结束位置，以及一个 0 到 1 之间的值，代表起始和结束位置之间的某一点。例如，如果最后一个值设置为 0，则 Lerp() 将返回起始位置。如果最后一个值是 1，它返回结束位置。如果最后一个值是 0.5，它返回起始和结束位置正中间的点。在这种情况下，你提供相机挂载位置作为起始，将玩家位置作为结束。最后，你将自帧时间乘以速度倍数，为最后一个参数获取一个合适的值。实际上，这使得相机挂载位置平滑地移动到玩家所在。

保存代码并返回 Unity。在 Hierarchy 中选择 CameraMount，并查看 Inspector。你会看到两个名为 Follow Target 和 Move Speed 的字段。如之前提到的，这些是 Unity 根据你刚刚添加到脚本的公共变量自动派生的。这些变量可能需要一些值。

在 Hierarchy 中仍保持选中 CameraMount 的情况下，将 SpaceMarine 拖入 Follow Target 字段，并将 Move Speed 设置为 20。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_88_0.png)

运行你的游戏看看发生了什么变化。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_88_1.png)

陆兵现在是一个真正的超级巨了，还配有专属的相机移动。诚然，他不能转身，而且像 Kitty Pryde 一样直接穿过物体，但这些都是容易解决的问题，你将在下一章第4章“物理学”中处理。

> 注意：move speed 越大，相机挂载移动玩家的速度就越快。越小，相机“滞后”太空陆兵的位置就越多，让玩家“领先”相机。尝试将移动速度更改为较小的值（如 2），看看会发生什么！

# 添加射击战斗

遗憾的是，外交的精妙之处对于游戏中这些食肉反派来说毫无意义。最好的办法是给英雄一些火力，以便他可以在糟糕的放松（糟糕？）的假期里保护自己。

首先，你需要创建一个子弹。在 Hierarchy 中，点击 Create 按钮。从下拉菜单中选择 3D Object 在 Scene（场景）视图中创建一个球体。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_89_0.png)

将其命名为 Projectile（投影体）。选中它后，查看 Inspector。你会发现许多新组件。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_89_1.png)

## 第3章：组件

三个新组件是：

- 1. Mesh Filter（网格过滤器）是一个包含你的模型网格数据的组件，并将其传递给渲染器。
- 2. Mesh Renderer（网格渲染器）显示网格。它包含了大量关于照明的信息，例如投影和接收影子。
- 3. 最后，你会发现球包含一个 Sphere Collider（球体碰撞体）。此组件作为 GameObject 的边界。你将在第4章学习碰撞体。

由于你希望子弹参与 Unity 的物理计算，它需要一个 Rigidbody。幸运的是，你以前做过。点击 Add Component 按钮并在 Physics 类别中选择 Rigidbody。取消勾选 Gravity（重力）。

由于我们会消耗大量投影体，将其从 Hierarchy 拖入 Project Browser 中的 Prefabs 文件夹。从 Hierarchy 中删除该投影体，因为你不需要它（它是制体）。

此时，你需要创建一个脚本来发射投影体。在 Project Browser 中选择 Scripts 文件夹，然后点击 Create。选择 C# Script 并命名为 Gun。双击文件以在代码编辑器中打开。

在类定义下方添加以下几个属性：

```cs
public GameObject bulletPrefab;
public Transform launchPosition;
```

再次，当你在脚本上创建公共变量时，Unity 会在编辑器中暴露这些变量。你把 bulletPrefab 指定为你刚刚创建的子弹制体，并将 launchPosition 指定为太空陆兵枪口的位置。

接下来，添加以下方法：

```cs
void fireBullet()
{
// 1
GameObject bullet = Instantiate(bulletPrefab) as GameObject;
// 2
bullet.transform.position = launchPosition.position;
// 3
bullet.GetComponent<Rigidbody>().velocity = transform.parent.forward * 100;
}
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_90_0.png)

