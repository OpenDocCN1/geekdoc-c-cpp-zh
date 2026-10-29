

## FIGURE 39.19

使用 Setup  rollout 来定义人群系统。

Scatter

Object/Delegate Associations
Biped/Delegate Associations
Multiple Delegate Editing
Behavior Assignments
Cognitive Controllers

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1031_0.png)

## Cross-Ref

各种克隆方法在第 8 章“克隆对象和创建对象数组”中有所介绍。

单击 Scatter 按钮会打开如图 39.20 所示的 Scatter Objects 对话框。此对话框包含多个面板，用于随机化克隆委托的 Position、Rotation 和 Scale。在 Clone 面板中，你可以选择要克隆的 Object 以及要创建的 How Many 个克隆。设置正确后，单击 Generate Clones 按钮即可创建副本。

## FIGURE 39.20

Scatter Objects 对话框可让你快速创建对象人群。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1031_1.png)

## Chapter 39: Animating with CAT and Creating Crowds

## Setting delegate parameters

每个选定的委托都有可在 Modify 面板中设置的参数，包括其尺寸、Speed、Acceleration 和 Turning 值。选中 Crowd 对象后，你可以单击 Multiple Delegate Editing 按钮打开如图 39.21 所示的对话框，该对话框可让你同时更改多个委托的参数。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1032_0.png)

Edit Multiple Delegates 对话框可让你快速设置多个委托的参数。

在左上角，你可以使用 Add 按钮选择要更改的委托对象。然后你可以为参数指定两个值。如果指定了 Random 选项，则参数会在两个值之间随机取值。你还可以使用界面左下角的下拉列表保存设置集。

## Assigning behaviors

在 Crowd 对象的 Setup rollout 中有一个 New 按钮，可让你添加可与人群系统一起使用的新行为。添加到人群系统的所有行为都会出现在下拉列表中。通过在列表中输入新名称，你可以为每个行为命名。可用行为包括以下内容：

- **Avoid:** 防止场景对象与其他委托发生碰撞
- **Orientation:** 控制委托面向的方向
- **Path Follow:** 强制委托仅沿指定路径移动
- **Repel:** 强制委托远离目标对象

## Part IX: Working with Characters

- **Scripted:** 使委托使用 MAXScript 行为
- **Seek:** 使委托朝向目标对象移动
- **Space Warp:** 使用 Space Warp 对象控制行为
- **Speed Vary:** 在场景中移动时改变委托的速度
- **Surface Arrive:** 使委托朝向表面移动
- **Surface Follow:** 使委托在表面上移动
- **Wall Repel:** 使用网格对象排斥委托
- **Wall Seek:** 使用网格对象吸引委托
- **Wander:** 使委托随机移动

从 Setup rollout 选择行为后，会出现所选行为的参数自定义 rollout。使用这些参数，你可以控制行为的运作方式并选择目标对象。

设置完行为的参数后，你可以在如图 39.22 所示的 Behavior Assignments and Teams 对话框中为特定委托或委托团队分配使用某些行为。此对话框可通过 Setup rollout 中的 Behavior Assignment 按钮打开。

## FIGURE 39.22

Behavior Assignments and Teams 对话框可让你组织委托团队并将其分配给行为。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1033_0.png)

所有行为分配都列在中心窗格中，每个分配都可以赋予权重。如果委托有两个冲突的行为需要遵循，则它会遵循权重值最大的那个。

## Solving the simulation

流程的最后一步是求解模拟。此步骤为场景中的所有运动创建关键帧。要求解模拟，请单击 Solve rollout 中的 Solve 按钮，或单击 Step Solve 按钮一次求解一帧。默认情况下，解决方案为每一帧保存关键帧，但你可以增加 Positions 和 Rotations 值以更快地计算模拟。

## Tutorial: Rabbits in the forest

本示例使用链接到兔子网格的委托基元在森林中导航。通过数组对象移动多个对象手工操作起来可能很耗时，但 Crowd 系统使其变得简单。

要将一组兔子委托通过树木阵列移动，请按以下步骤操作：

- 1. 打开 DVD 上 Chap 39 目录中的 Bunny in the forest.max 文件。此文件包含几棵松树和一群兔子。
- 2. 选择 Create→ Helpers→ Crowd 菜单命令，并在视口中拖动以创建 Crowd 对象。使 Crowd 对象足够大以便轻松选择。
- 3. 选择 Create→ Helpers→ Delegate 菜单命令，并在 Left 视口中拖动以创建位于树木外部的 Delegate 对象。旋转兔子以设置其方向，然后将兔子链接到委托对象。然后 Shift+拖动委托以创建总共六个位于立方体周围的委托兔子。
- 4. 选择人群对象，单击 Modify 面板中 Setup rollout 的 New 按钮，选择 Avoid 行为并将其命名为 Avoid trees。在 Avoid Behavior rollout 中，单击 Multiple Selection 按钮。在出现的 Select 对话框中，选择所有树对象并单击 Select 按钮。启用 Display Hard Radius 按钮，然后将 Hard Radius 值减小到 0.2，以便兔子可以通过树木。
- 5. 再次单击 New 按钮。这次选择 Seek 行为并将其命名为 Seek hole。在 Seek Behavior rollout 中，单击 None 按钮并选择代表洞的红色盒子对象。
- 6. 在 Setup rollout 中，单击 Behavior Assignment 按钮打开 Behavior Assignment and Teams 对话框。单击 New Team 按钮，选择所有委托对象并单击 OK。然后选择 Team0 团队和 Avoid cubes 行为，并单击中间的 New Assignment 按钮（带右向箭头的长细按钮）。再次选择 Team0 团队和 Seek goal 行为，并再次单击 New Assignment 按钮。两个分配都列在中心窗格中；单击 OK。
- 7. 将 Solve time 设置为动画长度 300 帧。在 Solve rollout 中，单击 Solve 按钮。
- 人群系统求解所有委托朝向目标移动的运动。
- 8. 单击 Play Animation 按钮查看 resulting 解决方案。

图 39.23 显示了模拟结束后的委托位置。请注意各个委托的随机位置。

## Part IX: Working with Characters

## FIGURE 39.23

Crowd 模拟会自动计算如何移动委托兔子以到达目标同时避开树木。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1035_0.png)

## Summary

本章介绍了 CAT 并涵盖了使用 CAT  rig 的各个方面，包括其预设、自定义 rig 和动画。Character Studio 的 Crowd 功能对于为遵循指定行为的委托制作动画很有用。以下主题已涵盖：

- 学习创建角色的基本工作流程
- 创建和编辑 CAT rigs
- 创建自定义 CAT rig
- 为 CAT rigs 制作动画
- 使用 CAT Motion 对话框创建步行循环
- 使用肌肉 strands 和肌肉 planes
- 使用辅助对象创建人群
- 分配行为

无论你使用的是自定义 rig 还是 CAT rig，下一步都是开始蒙皮过程，这将在下一章介绍。蒙皮用网格皮肤包围骨架并匹配皮肤与底层 rig 的对齐和移动方式。

