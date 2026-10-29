

## Cross-Ref

Projection 修改器用于创建法线贴图，并在第 33 章“创建烘焙纹理和法线贴图”中进行了介绍。

## UVW Map 修改器

UVW Map 修改器让你可以为对象指定映射坐标。基本体、放样对象和 NURBS 可以自行生成映射坐标，但你需要使用此修改器为网格对象和面片应用映射坐标。

### Note

自行创建映射坐标的对象会将其应用到贴图通道 1。如果将 UVW Map 修改器应用到已拥有映射坐标的对象的贴图通道 1，则应用的坐标会覆盖现有的坐标。

你可以将 UVW Map 修改器应用到不同的贴图通道。应用此修改器会在对象上放置一个贴图小工具。你可以移动、缩放或旋转此小工具。要转换 UVW Map 小工具，必须从子对象列表中选择它。缩放小于对象的 Gizmo 可以进行平铺。

存在许多不同类型的映射，此修改器的参数展开面板让你可以选择使用哪一种。Length、Width 和 Height 值是 UVW Map 小工具的尺寸。你也可以在所有方向上设置平铺值。

### Note

最好在 UVW Map 修改器中调整平铺，而不是在材质编辑器中进行，因为材质编辑器中的更改会影响所有应用了该材质的对象，而修改器的更改仅影响该对象。

Alignment 部分提供八个按钮来控制 Gizmo 的对齐方式。Fit 按钮将 Gizmo 适配到对象的边缘。Center 按钮将 Gizmo 中心与对象中心对齐。Bitmap Fit 按钮会打开文件对话框，让你将 Gizmo 与所选位图的分辨率对齐。Normal Align 按钮让你可以在对象表面拖动，松开鼠标按钮时，Gizmo 原点会与法线对齐。View Align 按钮将 Gizmo 对齐以匹配当前视口。Region Fit 按钮让你可以在视口中拖动一个区域并将 Gizmo 匹配到该区域。Reset 按钮将 Gizmo 移回其原始位置。Acquire 按钮将 Gizmo 与另一个对象的坐标对齐。

图 32.1 显示了使用球面映射将砖块贴图应用到雨伞上。

## Tutorial: Using the UVW Map modifier to apply decals

在映射坐标自动应用或使用 UVW Map 修改器应用之后，你可以使用 UVW XForm 修改器移动、旋转和缩放映射坐标。

大多数对象都可以自动生成映射坐标——网格除外。对于网格，你需要使用 UVW Map 修改器。UVW Map 修改器包含七种不同的映射选项。每种映射选项以不同的方式包裹贴图。选项包括 Planar、 Cylindrical、 Spherical、 Shrink Wrap、 Box、 Face 和 XYZ to UVW。

在本教程中，你将使用 UVW Map 修改器将贴花应用到火箭模型上。Zygote Media 创建了该火箭模型。

## Chapter 32: Unwrapping UVs and Mapping Textures

## FIGURE 32.1

UVW Map 修改器让你可以为材质贴图指定各种映射坐标。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_854_0.png)

要使用 UVW Map 修改器，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 32 目录打开 Nasa decal on rocket.max 文件。
- 此文件包含一个已应用适当材质的火箭模型。DVD 上的 Chap 32 目录还包含一张 300 × 600 的图像，图像中 NASA 一词以黑色大写字母显示在白色背景上。此图像的背景颜色设置为透明，并以 .gif 格式保存。

### Note

GIF 格式通常用于网页，可以轻松使图像区域透明。这些透明区域在加载到 Max 时会成为 alpha 通道。

- 2. 打开材质编辑器（或按 M 键），并在材质/贴图浏览器中双击 Standard 材质。将材质命名为 NASA Logo。单击漫反射颜色色块并选择白色颜色。然后在材质/贴图浏览器中双击位图贴图按钮。找到 DVD 上 Chap 32 目录中的 NASA 图像，然后单击打开。位图图像加载，位图参数在展开面板中显示。在 Coordinates 展开面板中，在 W Angle 字段中输入值 −90。字母会垂直旋转。然后，在 Bitmap Parameters 展开面板中，选择 Image Alpha 选项。

## UVW XForm modifier

UVW XForm 修改器让你可以调整映射坐标。它可以应用于自动创建的映射坐标，也可以应用于使用 UVW Map 修改器创建的映射坐标。参数展开面板包括 UVW Tile 和 UVW Offsets 的值。你还可以选择要使用的贴图通道。

## Map Scaler modifier

Map Scaler 修改器同时作为 Object-Space 修改器和 World-Space 修改器提供。此修改器的 World-Space 版本在对象本身被调整大小时保持应用到对象的全部贴图的大小。Object-Space 版本将贴图绑定到对象，因此贴图会随对象一起缩放。Wrap Texture 选项通过将纹理首尾相接放置直到整个对象被覆盖，从而将纹理包裹在对象周围。

## Camera Map modifier

Camera Map 修改器基于摄像机位置创建平面映射坐标。它有两种形式——一种使用 Object-Space 应用，另一种使用 World-Space 应用。

此修改器的唯一参数是 Pick Camera。要使用此修改器，单击 Pick Camera 按钮并选择一个摄像机。映射坐标会应用到所选对象。

## Using the Unwrap UVW Modifier

Unwrap UVW 修改器让你可以控制贴图如何应用到子对象选择上。它也可以用于展开对象的现有映射坐标。然后你可以根据需要编辑这些坐标。你也可以使用 Unwrap UVW 修改器将多个平面贴图应用到对象上。你可以通过为对象的各个面创建平面贴图，然后在 Edit UVWs 界面中编辑映射坐标来实现此任务。

Unwrap UVW 修改器让你可以精确控制贴图如何应用到对象上。Unwrap UVW 修改器具有 Vertex、Edge 和 Face 子对象模式。在子对象模式下，你可以选择一个子对象，相同的选择会在 Edit UVWs 界面中显示，反之亦然。Edit UVW 窗口与视口之间的这种同步有助于确保你始终在处理相同的子对象。当选择 Edge 子对象时，Ring 和 Loop 按钮会变为活动状态。

在 Modify 面板中你会找到两个展开面板：Selection Parameters 和 Parameters。Selection Parameters 展开面板包含一个带加号的按钮和一个带减号的按钮。这些按钮会扩大或缩小当前选中的子对象选择。你还可以选择 Ignore Backfacing、Select by Element（而不是面）、设置 Planar Angle，或按材质 ID 或平滑组选择。

## The Edit UVWs interface

Parameters 展开面板包含一个名为 Edit 的按钮。此按钮会打开 Edit UVWs 界面，如图 32.3 所示，适用于一个简单的立方体。你还可以使用 Parameters 展开面板中的 Save 和 Load 按钮加载和保存编辑后的映射坐标，而 Reset UVWs 按钮会重置所有映射坐标。保存的映射坐标文件具有 .uvw 扩展名。Parameters 展开面板的 Display 部分让你可以设置平面贴图边缘的显示方式。选项包括 Show Seam、Show Map Seam、

Thin Seam Display 和 Thick Seam Display。通过使接缝可见，你可以轻松判断纹理在何处与对象的折痕不匹配。

## FIGURE 32.3

Edit UVWs 界面让你可以控制不同平面贴图如何与模型对齐。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_857_0.png)

表 32.1 显示并描述了 Edit UVWs 对话框中的按钮。

## TABLE 32.1

## Edit UVW Interface Buttons

| Buttons | Name | Description |
|---|---|---|
| Move, Move Horizontal, Move Vertical | Moves the selected vertices when dragged. |
| Rotate | Rotates the selected vertices when dragged. |

