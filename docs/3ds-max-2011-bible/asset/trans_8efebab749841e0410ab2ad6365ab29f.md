

## 第六部分：高级建模

操作的执行顺序会影响结果。您可以通过选择列表中的一个操作、选择其在列表中的位置，然后单击 Reorder Ops 按钮来重新排序操作。

## 交叉引用

您还可以使用几何体展开（Geometry rollout）中为可编辑网格提供的布尔运算符，对形状应用布尔运算。第 12 章“绘制和编辑 2D 样条线和形状”介绍了这些 2D 布尔运算符。

## 图 27.25

Insert 操作仅在进行减法时保持封闭体积。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_791_0.png)

应用于 ProBoolean 结果的材料可以设置为使用 Operand Material 或保留 Original Material。如果在减法操作中使用 Operand Material，则与所选对象接触的表面会保留被移除对象的材质，而对象的其余部分则具有原始对象的材质。如果选择了 Retain Original Material 选项，则整个结果将获得原始对象的材质。

在 Advanced Options rollout 中，有用于更新场景和降低对象复杂度的选项。Decimation 值是结果中要移除的边的百分比。如果您计划对对象进行平滑处理或将其转换为 Editable Poly 对象，则希望启用 Make Quadrilaterals 选项，这会使多边形简化避免使用三角形而优先使用四边形。您还可以设置 Quad Size，并可以选择如何处理平面边。

## 第 27 章：使用复合对象

### 注意

如果您计划将网格作为蒙皮对象或布料模拟的一部分进行变形，则生成的网格必须干净，否则变形会出现问题。

### 教程：创建钥匙孔

爱丽丝透过钥匙孔看到的是什么？ProBoolean 功能是切割门把手板上钥匙孔的完美工具。

要使用 ProBoolean 对象创建钥匙孔，请按以下步骤操作：

- 1. 从 DVD 上的 Chap 27 目录打开 Doorknob.max 文件。
- 2. 选择位于钥匙孔位置的门把手板对象，并选择 Create → Compound → ProBoolean 菜单命令。在 Parameters rollout 中，选择 Subtraction 选项。
- 3. 在 Pick Boolean rollout 中，单击 Start Picking 按钮并选择位于钥匙孔应处位置的 Box 和 Cylinder 对象。

图 27.26 显示了完成的钥匙孔。

## 图 27.26

使用 ProBoolean 对象构建的钥匙孔

![](img/ebbb4844f027f7d1c580e48108d2b6cb_792_0.png)

## 使用 ProCutter

原始布尔复合对象包含一个 Cut 选项。此功能已被 ProCutter 取代，ProCutter 提供了比原始选项更多的功能。ProCutter 允许您用多个切割器对象切割单个对象（称为 Stock 对象）。

您可以使用 Cutter Picking Parameters rollout 中找到的按钮拾取 Stock 和 Cutter 对象。每次选择都有四个选项：Reference、Move、Copy 或 Instance。Auto Extract Mesh 选项会自动用提取的结果替换所选的库存对象。Explode by Elements 选项仅在启用 Auto Extract Mesh 选项时有效。它将每个切割元素分离为一个对象。

在 Cutter Parameters rollout 中，您可以从三种 Cutting Options 中进行选择。Stock Outside Cutter 选项保留位于切割器外部的库存对象部分。Stock Inside Cutter 选项则相反，保留位于切割器内部的库存部分。Cutters Outside Stock 选项保留切割器中位于库存外部的部分。

所有选定的切割器和库存对象都会添加到 Cutter Parameters 中的列表中。使用 Extract Selected 按钮，您可以恢复任何作为 Copy 或 Instance 进行操作的切割器或库存对象。Materials 和 Decimation 与 ProBoolean 对象的工作方式相同。

### 提示

ProCutter 功能有助于分割将被动画化为爆炸成碎片的对象。

### 教程：创建拼图

ProCutter 可用于创建破坏性场景，例如将玻璃粉碎成碎片和拆解建筑物，但它也可以用于建设性切割，例如创建拼图。

要使用 ProCutter 复合对象将对象分割成拼图，请按以下步骤操作：

- 1. 从 DVD 上的 Chap 27 目录打开 ProCutter puzzle.max 文件。此文件包含一个贴有风景图像的简单盒子以及几条挤出的线条，标记拼图的边缘。
- 2. 选择标记切割位置的挤出线条之一（称为切割器），并选择 Create > Compound > ProCutter 菜单命令。
- 3. 然后，单击 Pick Cutter Objects 按钮并选择所有剩余的切割器对象。在 Cutter Parameters rollout 中，同时启用 Stock Outside Cutter 和 Stock Inside Cutter 选项。还选择 Retain Original Material 选项。
- 4. 在 Cutter Picking Parameters rollout 中，启用 Auto Extract Mesh 和 Explode By Elements 选项，然后选择 Pick Stock Objects 按钮并在视口中选择 Box 对象。
- 5. 打开 Material Editor 并将图像材质拖动到每个拼图块上。

### 注意

如果您不想看到切割线，可以选择并隐藏它们。

图 27.27 显示了最终的拼图，其中一块被移开。

## 图 27.27

使用 ProCutter 复合对象切割的拼图

![](img/ebbb4844f027f7d1c580e48108d2b6cb_794_0.png)

## 总结

复合对象为您的建模工具包增加了多种额外的建模类型。从形态对象到复杂的变形放样，您可以使用这些专用类型来建模许多不同的对象。本章涵盖了以下主题：

- 各种复合对象类型
- 使用相同数量顶点的形态对象
- 使用不同数量顶点的创建 Conform 对象
- 使用样条线和网格对象创建 ShapeMerge 对象
- 使用样条线创建 Terrain 对象
- Mesher 对象
- 使用 BlobMesh 对象模拟水
- 创建 Scatter 对象
- 创建 Connect 对象以连接两个对象
- 创建 Loft 对象

## 第六部分：高级建模

- 如何控制 Loft 参数
- 使用 Loft 变形
- 修改 Loft 子对象
- 比较 Loft 对象与曲面工具的优势
- 使用 ProBoolean 和 ProCutter 对象建模

Max 通常使用多边形和网格作为默认建模类型，但 CAD 软件通常使用实体。Body Object 是在实体和网格之间工作的解决方案，下文将介绍它。

## 图 28.1

SAT Import 对话框包含导入 CAD 对象的选项。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_797_0.png)

Single Body 选项可将所有对象一起作为单个对象导入 Max。如果所有对象未焊接在一起，您可以在 Element 子对象模式下单独选择和移动它们。如果它们被焊接，则作为单个对象工作。如果您正在加载背景或某些地形数据，这可能是理想的。最后一个选项将每个修剪曲面作为单独的体对象导入。

Viewport Body Mesh Quality 设置用于设置视口中显示的网格密度。3D Trimming Tolerance 选项可让您设置导入对象的修剪精度。最好从较低的公差开始，并在出现导入问题（如缺失面）时逐步增加。

### 警告

SAT 文件可能很大，选择任何 Fine 设置都会导致巨大的 Max 文件。

启用 Automatic Face Flipping 选项会使导入器尝试纠正指向错误方向的法线。大多数 CAD 格式具有不同的坐标系统，Z 轴向上而不是 Y 轴。启用 Convert SAT Y Axis to Z Axis 选项可为导入的对象修复此问题。

Select Additional SAT Files for Import 按钮会打开一个文件对话框，您可以在其中选择更多文件以使用当前设置导入。由于导入 SAT 文件需要很长时间，因此一次选择并导入多个文件是个好主意。

## 将 Max 对象转换为 Body 对象

从 SAT 格式导入的对象在 Max 中以 Modify 面板中的 Body Object 类型出现。Max 对象可以通过在 Create 面板中打开 Body Objects 子类别找到的 Body Object 按钮转换为 Body Object 类型。只需选择要转换的对象，然后按 Body Object 按钮即可。

转换在仅用于最基本的原始对象时效果最佳。如果需要转换更复杂的网格对象，请先尝试将其转换为 NURBS 对象，然后再转换为 Body 对象。

