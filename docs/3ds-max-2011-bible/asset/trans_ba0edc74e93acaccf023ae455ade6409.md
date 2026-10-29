

## Cross-Ref

在 Align 按钮的弹出菜单中还有两种常见的对齐方式：Align Camera 和 Place Highlight（Ctrl+H）。要了解这些功能，请分别参阅第 19 章“Configuring and Aiming Cameras”和第 20 章“Using Lights and Basic Lighting Techniques”。

## Aligning to a view

Align to View 命令提供了一种简便快捷的方式，将对象重新定位到其中一个轴上。要使用此命令，请选择一个对象并选择 Tools ◇ Align ◇ Align to View。Align to View 对话框会出现，如图 7.15 所示。在此对话框中更改设置会在视口中显示结果。您可以使用 Flip 命令来改变对象点的方向。如果没有选择对象，则无法使用 Align to View 命令。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_264_0.png)

## FIGURE 7.15

Align to View 对话框是快速将对象与轴对齐的方法。

Align to View 命令在您在错误视图中创建对象时特别有用，用于修正对象的方向。所有对齐都是相对于对象的局部坐标系完成的。如果选择了多个对象，每个对象都会根据其局部坐标系重新定向。

## Note

对对称对象（如球体）使用 Align to View 命令在视口中不会产生任何明显差异。

## Using Grids

启动 Max 时，唯一可见的元素是 Home Grid。该网格用于在 3D 空间中创建对象时提供参考点。每个网格的中心都有两条较暗的线。这些线在世界坐标系的原点相交，其中 X、Y 和 Z 的坐标均为 0.0。所有对象默认都放置在此点。

除了 Home Grid 之外，您还可以在场景中创建和放置新的网格。这些网格不会被渲染，但您可以使用它们来帮助您在 3D 空间中定位和对齐对象。

## The Home Grid

您可以通过选择 Tools ◇ Grid and Snaps ◇ Show Home Grid 来打开和关闭 Home Grid。（您也可以使用 G 键为活动视口打开和关闭 Home Grid。）如果 Home Grid 是场景中唯一的网格，则默认情况下它也是构造网格，新创建的对象会放置在此网格上。

要使用 AutoGrid，请在选择要创建的对象类型后单击 AutoGrid 选项。如果场景中没有对象，则对象会按常规方式创建。如果场景中有对象，光标会在对象的表面上移动，其坐标轴垂直于光标所在表面。单击并拖动会根据鼠标下方对象的精确位置创建新对象。

AutoGrid 选项会一直保持活动状态，直到您通过取消选中该框将其关闭为止，为您创建的所有新对象启用该选项。

**Tip**
在创建对象之前按住 Alt 键会使新的构造网格可见，禁用 AutoGrid 选项，并使所有新对象使用新的活动构造网格。您可以通过再次启用 AutoGrid 选项来禁用此活动构造网格。

## Tutorial: Creating a spyglass

当您开始为现有场景构建对象时，如果为创建的新对象启用 AutoGrid 功能，则远离场景原点的工作会容易得多。此功能使您可以将新对象放置在（或靠近）附近对象的表面上。它适用于具有位于边缘的轴点的对象效果最佳，例如 Box 和 Cylinder 对象。

在此示例中，您使用 AutoGrid 快速创建了一个望远镜对象，而无需执行额外的移动操作。

要使用 AutoGrid 和 Snap 功能创建望远镜，请按照以下步骤操作：

- 1. 开始前，单击左侧视口并大幅缩放，以便可以看到望远镜零件的高度。
- 2. 选择 Create > Standard Primitives > Cylinder，并在 Top 视口中从原点拖动以创建 Cylinder 对象。将 Radius 值设置为 40，Height 值设置为 200。然后在 Object Type 展开面板中启用 AutoGrid 选项。
- 3. 再次在 Top 视口中从原点拖动以创建另一个 Cylinder 对象。将其 Radius 设置为 35，Height 设置为 200。重复此步骤三次，每次将 Radius 减少 5。

图 7.17 显示了 resulting 望远镜对象。

## Using Snap Options

通常，当对象正在变换时，您确切知道要将其放置在何处。Snap 功能可以使对象精确到达应有的位置。例如，如果您使用盒状基元构建一组楼梯，可以启用 Edge Snap 功能，使每个相邻台阶沿着前一个台阶的边缘精确对齐。启用 Snap 功能后，当您将其放置得足够接近时，对象会自动移动（或吸附）到指定的吸附位置。如果启用了 Snap 功能，它们会影响场景中进行的任何变换。

吸附点在 Grid and Snap Settings 对话框中定义，您可以通过选择 Tools > Grid and Snaps > Grid and Snap Settings 或右键单击主工具栏上的前三个 Snap 按钮中的任何一个来打开该对话框。（这些 Snap 按钮中带有小磁铁图标。）图 7.18 显示了 Standard 和 NURBS 对象的 Grid and Snap Settings 对话框的 Snaps 面板。NURBS 代表 Non-Uniform Rational B-Splines。它们是一种由样条曲线创建的特殊类型的对象。

**Cross-Ref**
除了标准对象的吸附点之外，Snaps 面板还包括 NURBS 对象的吸附点列表。有关 NURBS 的更多信息，请参阅 DVD 上的附录第 3 章“Working with NURBS”。

## Part II: Working with Objects

## FIGURE 7.17

此望远镜对象使用 AutoGrid 选项快速轻松地创建。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_267_0.png)

## FIGURE 7.18

Snaps 面板包含许多不同的吸附点，具体取决于对象类型。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_267_1.png)

定义吸附点后，主工具栏上的 Snap 按钮可激活 Snap 功能，或您可以按 K 键。第一个 Snap 按钮包含一个弹出菜单，其中有三个按钮：3D Snap 切换、2.5D Snap 切换和 2D Snap 切换。2D Snap 切换按钮将所有吸附限制在活动构造网格上。2.5D Snap 切换按钮可吸附到构造网格上的点以及场景中对象投影的点。3D Snap 切换按钮可吸附到 3D 空间中的任何点。

## Chapter 7: Transforming Objects, Pivoting, Aligning, and Snapping

启用吸附时，轴点中心会出现一个小圆圈。这是吸附已启用的视觉提醒。当您在启用吸附的情况下移动对象时，可以拖动小圆圈在吸附点之间自由移动对象，或拖动 Move 工具的控件来约束对象的移动。

拖动对象时，会标记其起始位置，并在该起始点与目标点之间绘制一条线。可用的吸附点用一组十字准线标记。如果释放对象，它会吸附到高亮的十字准线组上。当对象位于可用吸附点上方时，连接起始点和终点以及吸附点十字准线的线条为绿色；否则为黄色。

除了小圆圈图标和 Move 工具控件之外，您还可以将鼠标移至对象上，对象上任何可用的吸附点都会被高亮显示。例如，如果在 Grid and Snap Settings 对话框中启用了 Vertex 选项，将鼠标移至盒状对象的其中一个角上时，该角会用一组黄色十字准线高亮显示。在顶点十字准线高亮显示时拖动，可以将所选角吸附到另一个位置。

## New Feature

视觉标记和选择并吸附特定对象位置的能力是 3ds Max 2011 的新功能。

## Tutorial: Creating a 2D outline of an object

2.5D 吸附可能令人困惑。它将吸附限制在活动构造网格上，但在活动网格内，它可以吸附到投影到活动网格上的 3D 点。您可以通过吸附到悬空对象的顶点来创建 3D 对象的 2D 表示。

要创建圆柱对象的 2D 轮廓，请按照以下步骤操作：

- 1. 选择 Create > Standard Primitives > Cylinder 菜单以创建简单的圆柱对象。
- 2. 选择并旋转圆柱，使其悬空并以角度位于构造网格上方。
- 3. 单击并按住 Snap 切换按钮，选择 2.5D Snap 弹出选项。然后右键单击 Snap 切换并在 Snaps 面板中仅选择 Vertex 选项。然后关闭 Grid and Snap Settings 对话框。
- 4. 选择 Create > Shapes > Line 菜单，并在 Top 视口中通过吸附到构成圆柱轮廓的点来创建线条。

图 7.19 显示了完成的轮廓。

## Tip

右键单击 Snap 切换会打开 Grid and Snap Settings 对话框，除了 Spinner Snap 切换，它会打开 Preference Settings 对话框。

这些 Snap 按钮控制平移的吸附。右侧还有另外两个按钮：Angle Snap 切换和 Percent Snap。这些按钮控制旋转和缩放的吸附。

## Note

打开和关闭 Snap 功能的键盘快捷键是 S 键。

