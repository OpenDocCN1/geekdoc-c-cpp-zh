

## 第 13 章：使用多边形和补丁建模

**图 13.25** — 该十二面体的顶部面已被单独挤出并倒角。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_420_0.png)

**图 13.26** — 铰链多边形来自边缘对话框让你选择一个铰链。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_420_1.png)

默认情况下，多边形的一个边缘将被用作该部分旋转的铰链，但在设置对话框中，你可以点击 Pick Hinge 按钮并选择一个边缘（该边缘不需要附加到多边形）。图 13.27 显示了一个球体基元，其中心边缘周围铰接了四个多边形面。

要使用 Extrude Along Spline 功能创建章鱼，请按照以下步骤操作：

1. 打开 DVD 上 Chap 13 目录中的 Octopus.max 文件。

    该文件包含一个由压扁的球体基元创建并转换为可编辑多边形的章鱼底座。八条样条线环绕该对象。

2. 选择章鱼对象以自动打开修改面板。在 Selection 展开栏中，点击 Polygon 子对象按钮（键盘快捷键，4）并在 Selection 展开栏中启用 Ignore Backfacing 选项。

3. 右键点击透视视口标题，并从弹出菜单中选择 Edged Faces 选项（或按 F4 键）。

    这使得多边形更容易看到。

4. 点击球体对象底部的一个面对象，并点击 Extrude Along Spline 设置对话框按钮以打开 Extrude Polygons Along Spline 对话框。

5. 点击 Pick Spline 按钮，并选择面旁边的样条线。将 Segments 设置为 6，Taper Amount 设置为 −1.0，然后点击 OK。确保未选择 Align to Face Normal 选项。

6. 对章鱼周围的每条样条线重复步骤 4 和 5。

7. 在 Subdivision Surface 展开栏中，启用 Use NURMS Subdivision 选项并将 Display Iterations 值设置为 2 以平滑整个章鱼。

图 13.29 显示了 resulting 章鱼。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_422_0.png)

该章鱼的触手使用 Extrude Along Spline 功能轻松创建。

### 表面属性

在 Edit Geometry 展开栏下方有几个展开栏选项，可让你设置顶点颜色、材质 ID、平滑组和 NURMS 子分割等附加属性。

#### 顶点表面属性

在顶点子对象模式下，Vertex Properties 展开栏让你定义对象顶点的 Color、Illumination 和 Alpha 值。颜色样本让你为所选顶点选择 Color 和 Illumination 颜色。Alpha 值设置顶点的透明度。分配颜色后，你可以通过在 Select Vertices By 部分中选择一种颜色（或照明颜色）并点击 Select 按钮来召回具有相同颜色的顶点。RGB（红、绿、蓝）值匹配这些值定义的范围内所有颜色。

> **交叉引用：** 你可以在第 31 章“在视口画布中绘画和渲染表面贴图”中找到有关顶点颜色的更多信息。

#### 多边形和元素表面属性

对于多边形和元素子对象，图 13.30 所示的 Polygon Properties 展开栏包括 Material IDs 和 Smoothing Groups 选项。Material IDs 选项设置由 Multi/Sub-Object 材质类型使用，以将不同的材质应用于对象内的面或多边形。通过选择多边形子对象，你可以使用这些选项设置将唯一材质应用于所选多边形。Select ID 按钮选择具有指定材质 ID 的所有子对象，或者你可以使用 Select ID 按钮下方的下拉列表中的材质名称选择子对象。

> **交叉引用：** 你可以在第 16 章“创建和应用标准材质”中找到有关 Multi/Sub-Object 材质类型的更多信息。

**图 13.30** — Polygon Properties 展开栏包括 Material IDs、Smoothing Groups 和 Vertex Colors 的设置。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_423_0.png)

你使用 Smoothing Groups 选项将子对象分配给唯一的平滑组。为此，选择一个子对象并点击一个 Smoothing Groups 数字。Select By SG 按钮与 Select By ID 按钮类似，会打开一个对话框，你可以在其中输入一个 Smoothing Groups 数字，所有具有该数字的子对象将被选中。Clear All 按钮清除所有 Smoothing Groups 数字分配，而 Auto Smooth 按钮根据面之间的角度自动分配 Smoothing Groups 数字，该角度由 Auto Smooth 按钮右侧的值设置。

Polygon Properties 展开栏还包括用于设置顶点 Color、Illumination 和 Alpha 值的选项。

### 子分割表面

可编辑多边形对象包含一个额外的展开栏，称为 Subdivision Surface，可在启用时自动平滑对象。图 13.31 所示的 Subdivision Surface 展开栏应用一种称为 NURMS 的平滑算法，即 Non-Uniform Rational MeshSmooth。它产生的效果与 MSmooth 按钮相似，但提供了对平滑应用程度的控制；视口和渲染器的设置可以不同。

**图 13.31** — Subdivision Surface 展开栏包括 NURMS 子分割的控件。

Cage Selection color

Cage color

![](img/ebbb4844f027f7d1c580e48108d2b6cb_424_0.png)

要启用 NURMS 子分割，你需要启用 Use NURMS Subdivision 选项。Smooth Result 选项将所有多边形放入同一平滑组并将 MeshSmooth 应用于整个对象。使用高 Iterations 值应用 NURMS 会产生非常密集的网格，但 Isoline Display 选项会显示简化的边缘数量，使对象更易于操作。平滑过程会在对象上添加许多边缘，而 Isoline Display 选项仅显示等距线。Show Cage 选项使周围的笼子可见或不可见。Show Cage 选项右侧的两个颜色样本让你设置笼子和选择的颜色。

Iterations 值决定在添加额外面来平滑它之前角落必须有多尖锐。值为 0 不平滑任何角落，最大值为 1.0 平滑所有多边形。

> **警告：** 每次平滑迭代都会使面数增加四倍。如果你将迭代次数提高得太高，系统可能会迅速变得不稳定。

Render 部分中的两个复选框可用于为 Display 和 Render 部分设置不同的值。如果禁用，则视口和渲染器使用相同的设置。平滑算法可以设置为忽略跨越 Smoothing Groups 和 Materials 的平滑。

如果启用了 Show Cage 选项（在 Edit Geometry 展开栏底部），一个橙色笼子会围绕 NURMS 对象并显示如果禁用 NURMS 时多边形面的位置。此笼子使选择多边形面变得更容易。

### 教程：建模一颗牙齿

如果你曾经做过根管治疗，那么你就知道牙科工作会带来多大的痛苦。幸运的是，建模一颗牙齿完全不痛苦，正如你在本示例中看到的那样。

要使用 NURMS 建模一颗牙齿，请按照以下步骤操作：

1. 选择 Create ➜ Standard Primitives ➜ Box，并在 Top 视口中拖动以创建 Box 对象。将其尺寸设置为 140 × 180 × 110，Segments 为 1 × 1 × 1。然后右键点击，并从弹出四菜单中选择 Convert To ➜ Editable Poly。

2. 点击 Selection 展开栏中的 Polygon 图标以启用多边形子对象模式。然后选择 Top 视口，并按 B 将其更改为 Bottom 视口。然后在 Bottom 视口中点击盒子的底部多边形。

3. 点击 Select and Scale 按钮（R），并将底部多边形缩放 10%。

4. 拖动整个对象以选择所有多边形，并在 Edit Geometry 展开栏中点击 Tessellate 按钮一次以将多边形划分为更多多边形。然后选择 Edit ➜ Region ➜ Window（或点击主工具栏中的 Window/Crossing 按钮）以启用 Window 选择方法，并在 Left 视口中拖动盒子底部以仅选择底部多边形。再次点击 Tessellate 按钮。

5. 在 Selection 展开栏中选择 Vertex 子对象模式，按住 Ctrl 键并选择每个象限中心的顶点。然后在 Left 视口中将这些顶点向下移动一段距离，约为盒子高度。

6. 再次选择 Bottom 视口，并按 T 将其改回 Top 视口。在 Selection 展开栏中启用 Ignore Backfacing 选项后，选择多边形中心的单个顶点，并在 Left 视口中将其稍微向下拖动。

7. 在 Selection 展开栏中禁用 Ignore Backfacing 选项，并选择 Left 视口中整个第二行顶点。使用 Select and Scale 工具，在 Top 视口中将这些顶点向多边形中心缩放。

8. 在 Subdivision Surface 展开栏中，启用 Use NURMS Subdivision 选项并将 Iterations 值设置为 2。

图 13.32 显示了完成的牙齿。

