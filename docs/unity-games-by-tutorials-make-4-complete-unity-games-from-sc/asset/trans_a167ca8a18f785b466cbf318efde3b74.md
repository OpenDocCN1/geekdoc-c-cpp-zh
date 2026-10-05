
Unity 游戏教程

第 4 章：物理

在层级面板（Hierarchy）中选择 BobbleMarine-Head。在检器（Inspector）中，为其分配 Head 层，并在确认对话框中选择“Yes, change child”。

最后，点击 Edit\Project Settings\Physics，在物理矩阵（physics matrix）中，取消勾选 Head行的 Player 列。

| | TransparentFX | Ignore Raycast | Water | Alien | Alien Head | Bullet | Column | Floor | Head | Player | Wall | Upgrade |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Default | | | | | | | | | | | | |
| TransparentFX | ☑ | | | | | | | | | | | |
| Ignore Raycast | ☑ | | | | | | | | | | | |
| Water | ☑ | ☑ | | | | | | | | | | |
| UI | ☑ | ☑ | | | | | | | | | | |
| Alien | ☑ | ☑ | | ☑ | | | | | | | | | |
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

射线检测从目标向终点发射一条不可见的射线，并在它击中 GameObject 时发送一个通知。你可能会遇到许多与射线相交的 GameObject。使用掩码（mask）可以让你过滤掉不需要的对象。

射线检测非常有用，并有多种用途。它们通常用于测试另一个玩家是否被弹药击中，但正如你将看到的，它们也可以帮助你测试鼠标指针下方是否有几何结构。

下面的图片显示了从立方体到锥体的射线检测。由于射线带有锥体掩码，它忽略了 iconsphere 层并向锥体报告击中。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_120_0.png)

你将从相机向鼠标指针发射一条射线。然后太空陆战员将转向射线击中的任何地方，本质上是跟随鼠标。

打开 PlayerController.cs 并添加以下实例变量：

```
public LayerMask layerMask;
private Vector3 currentLookTarget = Vector3.zero;
```

## Unity 游戏教程 | 第 4 章：物理

LayerMask 允许你指定射线应该击中的哪些层。currentLookTarget 是你希望陆战员盯着的地方。由于你不知道游戏开始时该看哪里，所以你将值设为零。

> 注意：随着你添加实例变量，你会发现 public 和 private 变量变得杂乱。这是为了简洁起 way。最佳实践是将它们分组。

接下来，在 FixedUpdate() 中添加以下内容：

```csharp
RaycastHit hit;
Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
if (Physics.Raycast(ray, out hit, 1000, layerMask))
{
    currentLookTarget = hit.point;
}
```
