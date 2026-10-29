

## Gradient map

Gradient map 使用三种颜色创建渐变图像。Gradient Parameters 展开面板包含每个颜色的颜色样本和贴图按钮。您可以使用 Color 2 Position 值旋钮将中间颜色放置在两端之间的任意位置。该值范围为 0 到 1。展开面板让您在 Linear 和 Radial 渐变类型之间进行选择。

Noise Amount 如果其值不为零则会为渐变添加噪点。Size 值缩放噪点效果，而 Phase 控制噪点随时间变化的速度。可以选择的三种噪点类型为 Regular、Fractal 和 Turbulence。Levels 值决定噪点函数应用的次数。High 和 Low Threshold 以及 Smooth 值设置噪点函数的限制以消除不连续性。

Figure 17.12 显示了线性渐变和径向 Gradient maps。

### FIGURE 17.12

Gradient map 可以是线性的（左）或径向的（右）。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_526_0.png)

## Gradient Ramp map

这种 Gradient map 的高级版本可以使用许多不同的颜色。Gradient Ramp Parameters 展开面板，如 Figure 17.13 所示，包含一个颜色条，其底部边缘有几个标记。您只需沿底部边缘单击即可添加标记。您也可以拖动标记重新定位它们，或通过将内部标记一直拖到任一端直到变红来删除它们。

要定义每个标记的颜色，请右键单击该标记，然后从弹出菜单中选择 Edit Properties。Flag Properties 对话框也会在 Figure 17.13 中显示，以便您可以选择要使用的颜色或纹理。

Gradient Ramp Parameters 展开面板中的 Gradient Type 下拉菜单提供各种 Gradient Types，包括 4 Corner、Box、Diagonal、Lighting、Linear、Mapped、Normal、Pong、Radial、Spiral、Sweep 和 Tartan。您还可以从包括 Custom、Ease In、Ease In Out、Ease Out、Linear 和 Solid 在内的几种 Interpolation 类型中进行选择。

Figure 17.14 显示了 Gradient Ramp map 可用的几种渐变类型。

### FIGURE 17.13

Flag Properties 对话框使您能够指定 Gradient Ramp 中要使用的颜色及其位置。

Gradient Marker

![](img/ebbb4844f027f7d1c580e48108d2b6cb_527_0.png)

Show/hide in Track View

### FIGURE 17.14

Gradient Ramp map 提供几种不同的渐变类型，包括（从左上到右下）Box、Diagonal、Normal、Pong、Spiral 和 Tartan。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_527_1.png)

## Swirl map

Swirl map 创建两种颜色的漩涡图像：Base 和 Swirl。Swirl Parameters 展开面板包含两个颜色样本和贴图按钮来指定这些颜色。Swap 按钮交换两种颜色。其他选项包括 Color Contrast，控制两种颜色之间的对比度；Swirl Intensity，定义漩涡颜色的强度；以及 Swirl Amount，即 Swirl 颜色混合到 Base 颜色中的程度。

## Chapter 17: Adding Material Details with Maps

### Note

所有使用两种颜色的贴图都包含一个 Swap 按钮用于在颜色之间切换。

Twist 值设置漩涡的数量。负值会导致漩涡改变方向。Constant Detail 值决定漩涡中包含的细节量。

使用 Swirl Location X 和 Y 值，您可以移动漩涡的中心。随着中心远离材质中心移动，漩涡环变得更紧。Lock 按钮使两个值同等变化。如果禁用锁定，则可以独立更改这些值。

Random Seed 设置漩涡效果的随机性。

Figure 17.15 显示了具有三种不同 Twist 值的 Swirl map。从左到右，Twist 值分别为 1、5 和 10。

### FIGURE 17.15

Swirl map 将两种颜色以漩涡图案组合。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_528_0.png)

## Tiles map

Tiles map 创建砖块图案。Standard Controls 展开面板包含一个 Preset 下拉列表，其中列出了瓷砖集图案。这些图案是流行的瓷砖图案，包括 Running Bond、Common Flemish Bond、English Bond、½ Running Bond、Stack Bond、Fine Running Bond 和 Fine Stack Bond。

在 Advanced Controls 展开面板下的 Tile 和 Grout Setup 两个部分中，您可以使用自定义纹理贴图和颜色。您可以指定 Tiles 的水平和垂直数量以及 Grout 的水平和垂直间隙，以及两者各自的颜色和 Fade Variance 值。水平和垂直间隙可以锁定以始终相等。对于 Grout，您还可以定义孔洞的百分比。孔洞是指瓷砖被遗漏的地方。Rough 值控制砂浆的粗糙度。

Random Seed 值控制图案的随机性，而 Swap Texture Entries 选项交换瓷砖纹理与砂浆纹理。

在 Stacking Layout 部分，Line Shift 和 Random Shift 值用于将每一行瓷砖移动定义的或随机的距离。

Row and Column Editing 部分提供选项，可让您更改每行或每列的瓷砖数量以及每行或每列的更改（或剩余）量。

Figure 17.16 显示了三种不同的 Tile map 样式。

## Part IV: Materials, Cameras, and Lighting Basics

### FIGURE 17.16

从 Standard Controls 展开面板，您可以从多个预设 Tile 样式中进行选择，包括 Running Bond、English Bond 和 Fine Running Bond。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_529_0.png)

## 3D maps

3D maps 是程序化创建的，这意味着这些贴图不仅仅是一组像素；它们实际上是使用数学算法创建的。该算法以三维方式定义贴图，因此如果对象的某一部分被切除，贴图将在每个边缘对齐。

3D maps 的 Coordinates 展开面板与 2D maps 的 Coordinates 展开面板类似，但有几个例外；差异包括 Coordinate Source 选项为 Object XYZ、World XYZ、Explicit Map Channel 和 Vertex Color Channel。X、Y、Z 轴还有 Offset、Tiling 和 Angle 值，以及 Blur 和 Blur offset 选项。

## Cellular map

Cellular 3D map 创建称为 cells 的小型物体图案。在 Cellular Parameters 展开面板的 Cell Color 部分，您可以指定单个 cells 的颜色或应用贴图。设置 Variation 值可以改变 cell 颜色。

在 Division Colors 部分，使用两个颜色样本来定义 cells 之间出现的颜色。这个空间是两种颜色之间的渐变。

在 Cell Characteristics 部分，您可以通过选择 Circular 或 Chips 来控制 cells 的形状、Size 以及 cells 的分布方式。Bump Smoothing 值平滑 cells 的锯齿状。Fractal 选项会导致 cells 使用分形算法生成。Iterations 值决定算法应用的次数。Adaptive 选项自动确定要完成的迭代次数。Roughness 设置决定 cells 表面有多粗糙。

Size 值影响贴图的整体比例，而 Threshold 值指定单个 cells 的特定大小。设置包括 Low、Mid 和 High。

Figure 17.17 显示了三个 Cellular maps：第一个使用 Circular cells 且 Size 值为 20，第二个使用 Chips cells，最后一个启用了 Fractal 选项。

## Dent map

Dent 3D map 作为 bump map 工作，在物体表面创建凹痕。在 Dent Parameters 展开面板中，Size 值设置凹痕的整体大小。Strength 值决定凹痕的深度，而 Iterations 值设置算法计算的次数。您还可以指定 Dent map 的颜色。默认颜色为黑色和白色。黑色定义被压入的区域。

## Chapter 17: Adding Material Details with Maps

### FIGURE 17.17

Cellular map 创建小而规则形状的 cells。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_530_0.png)

Figure 17.18 显示了三个球体，Dent map 作为 bump mapping 应用。三个球体从左到右的 Size 值分别为 500、1000 和 2000。

### FIGURE 17.18

当 Dent map 作为 bump mapping 应用时，会在物体上造成凹痕。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_530_1.png)

## Falloff map

Falloff 3D 根据表面法线的方向创建灰度图像。法线与视图平行的区域为黑色，法线与视图垂直的区域为白色。该贴图通常作为不透明度贴图应用，使您能够更好地控制物体的不透明度。

### Tip

Falloff map 也可用于通过其反射在釉面表面上创建 Fresnel 效果。■

Falloff Parameters 展开面板包含两个颜色样本、各自的 Strength 值以及可选的贴图。还有用于设置 Falloff Type 和 Falloff Direction 的下拉列表。Falloff Types 包括 Perpendicular/Parallel、Towards/Away、Fresnel、Shadow/Light 和 Distance Blend。Falloff Direction 选项包括 Viewing Direction（Camera Z axis）；Camera X Axis；Camera Y Axis；Object；Local X、Y 和 Z Axis；以及 World X、Y 和 Z Axis。

在 Mode Specific Parameters 部分，多个参数基于 Falloff Type 和 Direction。如果选择 Object 作为 Falloff Direction，则激活一个按钮让您选择对象。Fresnel Falloff Type 基于折射率并提供覆盖材质折射率值的选项。Distance Blend Falloff Type 提供 Near 和 Far 距离的值。

