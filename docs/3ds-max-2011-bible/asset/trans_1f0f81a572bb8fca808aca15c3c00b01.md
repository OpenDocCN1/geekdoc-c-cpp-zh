

## FIGURE 13.39

使用 Bind 和 Weld 按钮将不同分辨率的两个补丁组合在一起。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_435_0.png)

在分配颜色后，您可以通过在 Select Vertices By 部分中选择一种颜色（或照明颜色）并单击 Select 按钮来召回具有相同颜色的顶点。RGB 值匹配这些值定义的范围内所有颜色。例如，如果 RGB 范围值全部设置为 255，则会选择每个顶点。

## Editing handles

Handle 子对象模式可让您直接访问顶点句柄，而不会受到顶点或边的干扰。您仍然可以在 Vertex 子对象模式下使用句柄，但 Handle 子对象模式更方便，并且您无需担心在过程中意外移动顶点。

启用 Handle 子对象模式时，整个补丁对象的全部顶点句柄都可见。可以同时选择和转换多个句柄。此模式也提供 Copy 和 Paste Tangent 选项。

## Editing edges

边是连接两个顶点之间的线。您可以通过按住 Ctrl 键同时单击边来选择多条边，或按住 Alt 键以从当前选择集中移除所选边。

## Chapter 13: Modeling with Polygons and Patches

Geometry rollout 中的许多功能与 Vertex 子对象的工作方式相同，但 Geometry rollout 还包括在 Edge 子对象模式下启用的一些功能，如以下各节所述。

## Subdivide

您可以使用 Subdivide 按钮增加补丁的分辨率。这是通过将一条边分割成两条独立的边，并在原始边的中心处分割来实现的。要使用此功能，请选择一条或多条边并单击 Subdivide 按钮。Propagate 选项会导致边或相邻补丁也被细分。使用未启用 Propagate 选项的 Subdivide 可能会导致补丁出现裂缝。Subdivide 按钮在 Patch 子对象模式下也有效。

在图 13.40 中，我在选择右上角边角边后将 Quad Patch 边细分了三次。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_436_0.png)

通过细分边子对象，您可以控制分辨率最大的位置。

## Add Tri and Add Quad

您可以向补丁的任何开放边添加 Quad 和 Tri 补丁。为此，请选择开放边或边，然后单击 Add Tri 或 Add Quad 按钮。您可以使用 Selection rollout 中的 Select Open Edges 按钮找到所有开放边。新的补丁会沿着补丁当前的曲率延伸。要向封闭表面（如盒子）添加补丁，您首先需要分离其中一个补丁以创建开放边。此功能提供了一种扩展当前补丁的方法。

图 13.41 显示了一个简单的四边形补丁，它已被细分，然后使用 Add Quad 按钮进行了添加。这提供了一种快速创建要建模对象的粗略轮廓的简便方法。

## Create Shape

您可以使用 Geometry rollout 底部在 Edge 子对象模式下出现的 Create Shape 按钮，从所有选定的边创建样条形状。要使用此按钮，请选择几个边子对象并单击该按钮。会出现一个对话框，允许您为新形状命名。然后您可以使用 Select by Name 对话框（键盘快捷键，H）选择新创建的形状。

## Tutorial: Modeling a shell

现在您已经看到了各种工具，是时候尝试一些了。您可以使用 Patch 对象创建一个常见的海滩贝壳，就像本教程中要做的那样。

要使用补丁建模贝壳，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 13 目录打开 Patch seashell.max 文件。
  该文件包含一个已转换为 Editable Patch 对象的简单圆盘，并且所有下部顶点都已焊接在一起。

## Part III: Modeling Basics

## FIGURE 13.41

通过选择边子对象并添加 Quad 补丁创建了一个钥匙的快速轮廓。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_437_0.png)

- 2. 选择贝壳对象并打开 Modify 面板。单击 Modifier Stack 中 Editable Patch 对象左侧的小加号图标，然后从层次结构中选择 Edge（或按 2）。您现在处于 Edge 子对象模式。

- 3. 在 Front 视口中按住 Ctrl 键选择贝壳中每隔一个内部径向边集。确保选择前后边。Shell Selection rollout 底部的 Info 行会告诉您选择了什么（应选择 14 条边）。选择边后，按空格键锁定选择。

- 4. 单击 Select and Move 按钮（或按 W），并在 Top 视图中向上移动边。补丁表面会出现锯齿状图案。

图 13.42 显示了完成的贝壳。

## Editing patch and element subobjects

仅包含一个补丁的补丁对象的变换在子对象模式下与正常变换的工作方式相同。对包含多个补丁的对象使用补丁子对象可让您变换单个补丁。使用补丁子对象的关键优势是使用 Geometry rollout 中的按钮控制其 Geometry。以下各节讨论了在补丁子对象模式下可用的附加功能。

## Detach

Detach 按钮将所选补丁或元素子对象与对象的其余部分分离。使用此按钮会打开 Detach 对话框，您可以在其中命名分离的子对象。Reorient 选项会重新对齐分离的子对象补丁，使其与当前活动补丁的位置和方向相匹配。Copy 选项会创建分离子对象的副本。

## FIGURE 13.42

该贝壳是由移动每隔一个内部边创建的 Editable Patch。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_438_0.png)

## Note

此功能与 Delete 不同。Detach 保留子对象并为其分配单独的名称，但 Delete 功能会消除子对象。

## Extrude

Extrude 按钮通过复制补丁表面并创建连接新补丁表面与原始表面的侧面，为补丁添加深度。例如，被挤出的正方形补丁网格会形成一个立方体。要使用此功能，请选择一个补丁，单击 Extrude 按钮，然后在视口中拖动——补丁会交互式显示挤出深度。达到所需距离时释放按钮。

或者，您可以在 Extrusion spinner 中指定挤出深度。Outlining 值可让您调整挤出补丁的大小。正向轮廓值会导致挤出变大，而负值

Surface Properties rollout 包括 Flip 和 Unify 按钮，用于控制法线向量的方向。Flip 会反转每个所选面的法线方向；Unify 会根据多数情况使所有法线朝同一方向。Flip Normal Mode 按钮激活一种模式，您可以在其中单击单个面并翻转其法线。该模式保持激活状态，直到您再次单击 Flip Normal Mode 按钮或在视口中右键单击为止。

Material IDs 由 Multi/Sub-Object 材质类型使用，用于将不同材质应用于对象内的不同补丁。通过选择补丁子对象，您可以使用此控件为每个补丁应用独特的材质。

## Cross-Ref

您可以在第 16 章“Creating and Applying Standard Materials”中了解有关 Multi/Sub-Object 材质类型的更多信息。

您还可以将补丁分配给唯一的 Smoothing Group。为此，请选择一个补丁并单击一个 Smoothing Group 数字。

## Tutorial: Creating a maple leaf from patches

由于补丁是建模有机物体的良好类型，让我们通过尝试创建枫叶来测试它。由于叶子的对称性，您实际上只需要创建叶子的半部分。然后您可以使用 Mirror 工具创建另一半。

要使用补丁建模枫叶，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 13 目录打开 Maple leaf.max 文件。
  该文件包含一个真实枫叶的背景图像，已加载到 Front 视口中。
- 2. 选择 Create→ Patch Grids→ Tri Patch，并在 Front 视口中拖动，从茎基部创建一个正方形补丁网格到叶子的左上内侧区域。补丁的右边缘应沿着叶子的中线向上运行约一半。
- 3. 在 Modify 面板中，右键单击 Tri Patch 名称并从弹出菜单中选择 Convert to Editable Patch。
- 4. 在 Modifier Stack 中，选择 Element 子对象模式（或按 4 键），然后选择补丁元素。在选中 Propagate 选项的情况下，单击 Subdivide 按钮。
- 5. 选择 Edge 子对象模式（或按 2 键），并选择一条完全位于背景叶图像内部区域的边。然后按 Add Tri 按钮扩展补丁。重复此步骤，直到为叶子外周边的每个点添加了补丁。
- 6. 选择 Vertex 子对象模式（或按 1 键）。使用主工具栏上的 Select and Move 按钮，选择并拖动边顶点，使其与背景叶的角对齐。移动所有内部顶点，使其位于叶区域内。选择位于叶子外边缘的每个顶点，并移动其句柄，使补丁边缘与背景叶的边界对齐。如果句柄一起移动，请按住 Shift 键以单独移动它们。
- 7. 取消选择 Vertex 子对象模式。在 Surface Properties rollout 中启用所有选项，并将 Relax Value 设置为 1.0，将 Iterations 设置为 50。这会平滑补丁中的皱纹。

图 13.44 显示了完成的枫叶补丁（至少是其中一半）。要完成这片叶子，请使用 Mirror 工具并添加一个样条对象作为茎。

