

## FIGURE 7.10

Transform Gizmo 位于对象的枢轴点处。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_258_0.png)

## Note

在使用其中一种模式选中的情况下使用缩放变换会改变所选对象，但对枢轴点或链接没有影响。

## Aligning pivot points

在模式按钮下方还有三个用于对齐枢轴点的按钮。这些按钮仅在选择了模式时才处于活动状态。这些按钮为 Center to Object/Pivot、Align to Object/Pivot 和 Align to World。前两个按钮根据所选模式在 Object 和 Pivot 之间切换。您一次只能选择一种模式。按钮在选中时变为浅蓝色。

Center to Object 按钮将枢轴点移动使其与对象中心对齐，而 Center to Pivot 按钮将对象移动使其在其自身枢轴点上居中。Align to Object/Pivot 按钮旋转对象或枢轴点，直到对象的局部坐标系与枢轴点对齐。Align to World 按钮将对象或枢轴旋转到世界坐标系。例如，如果选择了 Affect Object Only 模式并且对象与枢轴点分离，点击 Center to Pivot 按钮会将对象移动使其中心位于枢轴点上。

在这三个对齐按钮下方还有一个标记为 Reset Pivot 的按钮，您可以使用它将枢轴点重置到其原始位置。

## Using the Working Pivot

在 Adjust Pivot 展开面板下方是 Working Pivot 展开面板。如果您想使用临时枢轴定位对象而无需更改默认对象枢轴，Working Pivot 非常方便。要定位 Working Pivot，请点击 Edit Working Pivot 按钮。这会进入一种模式，就像前面描述的 Affect Pivot Only 按钮一样，只是它适用于工作枢轴。

在 Working Pivot 就位后，您可以通过点击 Use Working Pivot 按钮选择使用它而不是对象枢轴。Working Pivot 保持激活状态，直到您在层级面板中禁用它。Working Pivot 对场景中的所有对象都有效。当 Working Pivot 处于活动状态时，提醒文字 “USE WP” 会出现在所有视口的视口名称下方；当 Edit Working Pivot 模式启用时，此文字显示为 “EDIT WP。”

## Tutorial: A bee buzzing about a flower

通过调整对象的枢轴点，您可以控制对象在场景中如何变换。在此示例中，您通过重新定位翅膀的枢轴点来为蜜蜂的拍打翅膀制作动画。然后您重新定位整个蜜蜂的枢轴点，使其能够绕花对象旋转。

要控制蜜蜂如何绕花旋转，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 07 目录打开 Buzzing bee.max 文件。此文件包含一个由基本体创建的蜜蜂和由 Zygote Media 创建的花模型。
- 2. 点击蜜蜂对象将其选中，并按 Z 在所有视口中放大。点击右翼，打开层级面板并点击 Affect Pivot Only 按钮。这会在翅膀表面中心显示枢轴点。从主工具栏的列表中选择 Local 坐标系。这会使变换小工具的朝向与枢轴的朝向匹配。沿其 X 轴拖动翅膀的枢轴点到翅膀接触身体对象的位置。然后禁用 Affect Pivot Only 按钮。然后选择并对左翼重复此步骤。
- 3. 点击 Auto Key 按钮（或按 N）以启用动画模式，并将时间滑块拖到第 1 帧。然后，使用选择和旋转按钮（E），在前视口中将翅膀绕其 Z 轴旋转，直到几乎垂直。注意翅膀如何绕其新的枢轴点旋转。然后将时间滑块拖到第 2 帧，并将翅膀旋转回其原始位置。再次点击 Auto Key 按钮（N）以禁用关键帧模式。
- 4. 如果您想使用 Track View 使这些旋转在整个动画中重复，请右键单击翅膀对象并在出现的弹出四菜单中选择 Curve Editor。这将打开一个 Track View，其中选择了旋转轨道。在 Track View 中，选择 Controller > Out-of-Range Types 以打开 Param Out-of-Range Types 对话框，选择 Loop 选项，然后点击 OK。然后关闭 Track View。

### Cross-Ref

> **Working with the Track View** 超出了本章的范围，但您可以在第 36 章“Working with Function Curves in the Track View”中找到有关 Track View 的更多信息。

- 5. 对第二个翅膀对象重复步骤 3 和 4。按播放动画按钮查看两个翅膀在整个动画中拍打。
- 6. 在顶视口中选择组成蜜蜂的所有部件，选择 Group > Group，并将对象命名为 Bee。然后在左视口中选择蜜蜂和花，并按 Z 放大。
- 7. 在选择蜜蜂组的情况下，在层级面板中点击 Affect Pivot Only 按钮并将枢轴点移动到前视口中花的中心。再次点击 Affect Pivot Only 按钮以禁用它。

### Note

> **如果您不想在步骤 7 中移动对象枢轴，您可以使用 Working Pivot 使蜜蜂绕花旋转，或者您可以选择 Pick 坐标系并选择花。**

- 8. 再次启用 Auto Key 按钮（N），并拖到第 35 帧。使用选择和旋转按钮（E），在顶视口中将蜜蜂绕花旋转三分之一。然后将时间滑块拖到第 70 帧，并将蜜蜂再旋转三分之一。在时间滑块位于第 100 帧时完成旋转。再次点击 Auto Key 按钮以显示关键帧模式。
- 9. 点击播放按钮查看最终旋转的蜜蜂。

图 7.11 显示了蜜蜂绕其枢轴点所在的花移动的情况。

## Part II: Working with Objects

## FIGURE 7.11

通过移动蜜蜂的枢轴点，您可以控制它如何绕花旋转。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_261_0.png)

## Using the Align Commands

Align 命令是自动变换对象的简便方法。您可以使用这些命令对齐对象中心或边缘、对齐法线和高光、对齐视图和网格，甚至对齐摄像机。

## Aligning objects

任何可以变换的对象都可以对齐，包括灯光、摄像机和 Space Warps。在选择要对齐的对象后，点击主工具栏上的 Align 飞出按钮或选择 Tools → Align → Align（或按 Alt+A）。光标变为 Align 图标。现在，点击您想要对齐所有所选对象的目标对象。点击目标对象会打开 Align Selection 对话框，并在对话框的标题中显示目标对象的名称，如图 7.12 所示。

Align Selection 对话框包括用于对齐所选或目标对象边界框的最小值、中心、枢轴点或最大值尺寸的 X、Y 和 Z 位置设置。当您在对话框中更改设置时，对象会重新定位，但实际变换要等到您点击 Apply 或 OK 时才会发生。

### Cross-Ref

> 另一种对齐对象的方法是使用 Clone and Align 工具，该工具在第 8 章“Cloning Objects and Creating Object Arrays”中介绍。

## Part II: Working with Objects

## FIGURE 7.13

Normal Align 对话框允许您在对齐法线时定义偏移值。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_263_0.png)

## Tutorial: Aligning a kissing couple

对齐法线会将两个对象面直接相对放置，那么练习此工具的最佳方法莫过于对齐两个面。

要使用 Normal Align 命令连接接吻情侣，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 07 目录打开 Kissing couple.max 文件。
- 此文件包含男孩和女孩的两个挤出形状。挤出形状为您提供了易于对齐的平面。
- 2. 选择女孩形状，并选择 Tools▹Align▹Normal Align 菜单命令（或按 Alt+N）。然后点击并拖动光标越过挤出形状，直到蓝色向量从嘴唇前方指向外部，如图 7.14 所示。
- 3. 然后点击并拖动光标越过男孩形状，直到绿色向量从嘴唇前方指向外部。此从面指向外部的向量是表面法线。然后点击并释放鼠标，Normal Align 对话框会出现。在 Z-Axis Offset 字段中输入值 5，然后点击 OK。

图 7.14 显示了法线对齐面后的 resulting couple。

## FIGURE 7.14

使用 Normal Align 功能，您可以对齐对象面。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_263_1.png)

