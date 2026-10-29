

Tip

你也可以使用右键四键菜单访问子对象模式。要退出子对象模式，请在四键菜单中选择 Top Level。

## FIGURE 10.3

在 Modifier Stack 中展开可编辑对象会显示其子对象。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_314_0.png)

Subobjects icons

子对象选择可以使用 Selection Lock Toggle（空格键）锁定，并可通过在主工具栏的 Named Selection Set 下拉列表中输入名称将其制作成 Selection Set。创建 Selection Set 后，只要在同一子对象模式下即可随时召回它。Named Selection Sets 然后可以使用在大多数可编辑对象中 Selection rollout 找到的 Copy 和 Paste 按钮在对象之间复制和粘贴。

## Using Soft Selection

在处理可编辑网格、poly、补丁或样条时，子对象模式下会出现 Soft Selection rollout，如图 10.4 所示。Soft Selection 会选择当前选择周围的所有子对象，并以较小程度对其应用变换。例如，如果选择一个面并移动 2 个单位，则在线性 Soft Selection 下，软选择范围内的相邻面会移动 1 个单位。整体效果是过渡更平滑。

Note

各种建模类型的 Soft Selection 选项是不同的。例如，可编辑网格包含如图 10.4 所示的标准选项集，但 Editable Poly 对象有更多选项，包括 Paint Soft Selection 模式。

## FIGURE 10.5

Soft Selection 曲线受 Falloff、Pinch 和 Bubble 值的影响。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_316_0.png)

## Tutorial: Soft selecting a heart shape from a plane

Soft Selection 使子对象之间过渡平滑，但有时你想要急剧的边缘。本教程介绍在启用和未启用 Soft Selection 的情况下移动平面对象的一些子对象顶点。

要启用和禁用 Soft Selection 移动子对象顶点，请按以下步骤操作：

- 1. 从 DVD 上的 Chap 10 目录打开 Soft selection heart.max 文件。该文件包含两个已转换为 Editable Mesh 对象的简单平面对象。已选择了形状为心形的多个顶点。
- 2. 第一个平面对象的顶点已选中；在 Vertex 子对象模式下，单击 Select and Move 按钮（或按 W 键），将光标移至所选顶点，并在 Left 视口中远离平面的方向向上拖动。
- 3. 退出子对象模式，选择第二个平面对象，并进入 Vertex 子对象模式。相同的顶点再次被选中。打开 Soft Selection rollout，启用 Use Soft Selection 选项，并将 Falloff 值设置为 40。
- 4. 单击 Select and Move 按钮（或按 W 键），并向上移动所选顶点。注意 Soft Selection 带来的差异。

图 10.6 显示了带有心形选择的两个 resulting 平面对象。

## FIGURE 10.6

Soft Selection 使被移动的子对象与未被移动的子对象之间产生平滑过渡。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_316_1.png)

## Part III: Modeling Basics

当你选择子对象时，它们会变红。未选中的子对象为蓝色，而软选中的子对象则根据其与所选子对象的距离呈现从橙色到黄色的渐变。这种视觉提示提供了有关 Soft Selection 如何影响子对象的有价值反馈。图 10.7 显示了前一教程中选中的顶点，其 Falloff 值分别为 0、20、40、60 和 80。

## FIGURE 10.7

颜色渐变显示了软选中子对象的过渡区域。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_317_0.png)

对于 Editable Poly 和 Editable Patch 对象，Soft Selection rollout 在其曲线下方包含一个 Shaded Face Toggle 按钮。此按钮使用软选择渐变颜色对表面进行着色，如图 10.8 所示。此着色表面会显示在任何着色视口中。较冷的颜色对变换的影响较小。

## FIGURE 10.8

Shaded Face Toggle 使用软选择渐变颜色对表面进行着色。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_317_1.png)

## Part III: Modeling Basics

Constant Screen Size 选项可保持 Point 对象的大小恒定，无论你如何缩放场景。Draw on Top 选项会在所有其他场景对象之上绘制 Point 对象，使其易于定位。Point 对象的主要用途是在场景中标记位置。

## Caution

Point 对象难以看到且容易丢失。如果你使用点对象，请务必为其命名，以便在 Select from Scene 对话框中轻松找到它。■

## Measuring coordinate distances

Helpers 类别还包括用于测量尺寸和方向的几个实用工具。这些是 Tape、Protractor 和 Compass 对象。所有单位均基于当前选定的系统单位。

## Using the Measure Distance tool

在 Tools 菜单中有一个 Measure Distance 命令。此工具易于使用。只需选择它，然后在起点单击一次，在终点再次单击；两次单击之间的距离会显示在界面底部的 Status Bar 中。Measure Distance 还会报告 X、Y 和 Z 方向的 Delta 值。你可以在启用 Snap 功能的情况下使用此工具进行精确测量。

## Using the Tape helper

你使用 Tape 对象来测量距离。要使用它，只需拖动你想要测量的距离，并在 Parameters rollout 中查看 resulting 尺寸。你还可以使用 Specify Length 选项设置 Tape 对象的长度。你可以使用 Select and Move 按钮移动和重新定位 Tape 对象的端点，但 Rotate 和 Scale 按钮无效。

## Using the Protractor helper

Protractor 对象的工作方式与 Tape 对象类似，但它测量两个对象之间的角度。要使用 Protractor 对象，请在视口中单击以定位 Protractor 对象。 （Protractor 对象看起来像两个尖端对齐的金字塔，表示角度的原点。）然后单击 Pick Object 1 按钮，并选择场景中的一个对象。从 Protractor 对象到所选对象会绘制一条线。接下来，单击 Pick Object 2 按钮。角度形成的对象和 Protractor 对象会显示在 Parameters rollout 中。当任一所选对象或 Protractor 移动时，该值会发生变化。

## Note

所有测量值均以灰色字段形式显示在 Parameters rollout 中。此灰色字段表示该值无法修改。■

## Using the Compass helper

Compass 对象在平面星形对象上标识 North、East、West 和 South 位置。你可以拖动 Compass 对象以增加其大小。

## Cross-Ref

Grid helper 对象与 Chapter 7 “Transforming Objects, Pivoting, Aligning, and Snapping” 中的网格一起讨论。Compass 对象主要与 Sunlight System 结合使用，你可以在 Chapter 20 “Using Lights and Basic Lighting Techniques” 中了解它。■

## Chapter 10: Accessing Subobjects and Using Modeling Helpers

## Using the Measure utility

在 Utilities panel 中还有另一个用于获取当前所选对象信息的实用工具：Measure utility。你可以打开 Measure utility 作为浮动对话框，如图 10.9 所示。此对话框显示对象的名称以及其 Surface Area、Volume、Center of Mass、Length（针对形状）和 Dimensions。它还包括锁定当前选择的选项。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_320_0.png)

## Using the Level of Detail utility

随着场景的动画制作，一些对象靠近摄像机，而另一些则远离它。渲染远离摄像机的复杂对象意义不大。使用 Level of Detail（LOD）实用工具，你可以让 Max 在对象远离摄像机时渲染模型的简化版本，在靠近摄像机时渲染更复杂的版本。

## Cross-Ref

> MultiRes modifier 也可创建实时细节级别更新。它在 Chapter 26 “Deforming Surfaces and Using the Mesh Modifiers” 中介绍。

要打开该实用工具，请单击 Utility panel 中的 More 按钮并选择 Level of Detail utility。单个 rollout 会加载到 Utility panel 中，如图 10.10 所示。要使用此实用工具，你需要创建对象的多个版本并将它们组合在一起。Create New Set 按钮可让你从视口中选择一个对象组。组内的对象会单独列在 rollout 窗格中。

如果选择列出的对象，你可以指定 Threshold Units，单位为像素或目标图像的百分比。对于每个列出的项目，你可以指定最小和最大阈值。Image Output Size 值用于指定输出图像的大小，而使用的不同模型则基于对象在最终图像中的大小。Display in Viewports 复选框会导致适当的 LOD 模型出现在视口中。

