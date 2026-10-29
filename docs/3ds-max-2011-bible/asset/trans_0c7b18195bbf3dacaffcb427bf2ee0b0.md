

## L-Ext

L-Ext 原语代表 L-Extension。你可以把它想象成两个矩形盒子以直角相互连接。要创建 L-Ext 对象，首先需要拖动以创建定义对象整体区域的矩形。接下来，拖动以定义对象的高度，最后，拖动以定义每个腿的宽度。

Parameters 展开面板包括侧面和正面长度、侧面和正面宽度以及高度的尺寸。你还可以为每个尺寸定义段数。

## C-Ext

C-Ext 原语与 L-Ext 原语相同，只是多了一个矩形盒子。C 形将三个矩形盒子以直角相互连接。

Parameters 展开面板包括侧面、正面和背面长度和宽度以及高度的尺寸。你还可以为每个尺寸定义段数。这些原语非常棒，如果你的名字是 Clive Logan 或 Carrie Lincoln。 不，实际上，这些原语用于创建建筑梁。

## Hose

Hose 原语是一个灵活的连接器，可以放置在两个其他对象之间。它就像弹簧一样工作，但没有动态属性。在 Hose Parameters 展开面板中，你可以将 Hose 指定为 Free Hose 或 Bound to Object Pivots。如果选择 Free Hose 选项，可以设置 Hose Height。如果选择 Bound to Object Pivots 选项，则会出现用于 Top 和 Bottom 对象的两个 Pick Object 按钮。一旦绑定到两个对象，软管在任一对象移动时都会在两个对象之间伸展。你还可以为每个绑定对象设置 Tension。

对于 Bound Hose 或 Free Hose，你可以设置构成软管的段数；是否启用灵活部分；沿 Sides、Segments、两者都不或全部进行平滑；软管是否可渲染；以及为应用纹理贴图而生成映射坐标。如果启用了灵活部分，则可以设置灵活部分的 Starts 和 Ends、Cycles 数量及其 Diameter。

你还可以将 Hose Shape 设置为 Round、Rectangular 或 D-Section。图 5.25 显示了一个绑定到两个球体对象的灵活软管对象。

## Tutorial: Creating a bendable straw

如果你曾经在建模果汁盒时（或喝果汁盒时想，“我该如何建模这个可弯曲的吸管？”），那么本教程适合你。Hose 原语的好处是，一旦创建了模型，你可以重新定位吸管，弯曲会根据需要变化，就像真正的吸管一样。

要创建可弯曲吸管，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 05 目录打开 Bendable straw.max 文件。
- 该文件包含两个 Tube 原语，用于表示吸管的顶部和底部部分。我已将它们的轴点定向，使 Z 轴指向 Hose 原语所在的位置。

- 2. 选择 Create > Extended Primitives > Hose，并在 Top 视口中靠近两个吸管相遇的位置拖动。选择 Bound to Object Pivots 选项，单击 Pick Top Object 按钮并选择顶部的 Tube 对象。然后单击 Pick Bottom Object 按钮并选择底部的 Tube 对象。此步骤将 Hose 对象放置在两个 Tube 部件之间。

- 3. 在 Hose Parameters 展开面板中，将 Top 对象的 Tension 设置为 35，将底部对象的 Tension 设置为 10.0。将 Segments 设置为 40，Starts 值设置为 0，Ends 值设置为 100，Cycles 设置为 10，Diameter 设置为 24。确保启用 Renderable 选项，并启用 Round Hose 选项，Diameter 为 20.0。

## FIGURE 5.25

Hose 对象在其两个绑定对象之间弯曲。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_207_0.png)

图 5.26 显示了使用 Hose 原语创建的完成的弯曲吸管。

## Modifying object parameters

原语对象为许多其他建模类型提供了良好的起点。它们也提供了一种展示基于参数建模的好方法。

所有对象都有参数。这些参数有助于定义对象的外观。例如，考虑原语对象。Max 中包含的原语对象是参数化的。参数化对象是数学定义的，你可以通过修改其参数来更改它们。最简单的对象修改就是简单地更改这些参数。例如，半径为 4 的球体可以通过在 Radius 字段中简单输入 10 变成半径为 10 的球体。按下 Enter 键时，视口会自动显示这些更改。

## Note

创建对象时，其参数会显示在 Create 面板的 Parameters 展开面板中。只要对象保持为当前对象，你就可以使用此展开面板修改其参数。在选择不同的工具或对象后，Parameters 展开面板将无法从 Create 面板访问，但如果选择该对象并打开 Modify 面板，则可以更改所选对象的全部参数。

## FIGURE 5.26

使用 Hose 原语连接两个对象。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_208_0.png)

## Tutorial: Filling a treasure chest with gems

我最近没有找到很多宝箱，但如果我没记错的话，它们通常装满了明亮、闪烁的宝石。在本教程中，你将用多个 Hedra 原语填充宝箱，并在 Modify 面板中更改对象属性，以创建多样化的宝石。

要创建装有许多独特宝石的宝箱，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 05 目录打开 Treasure chest of gems.max 文件。
- 该文件包含一个简单的宝箱模型。
- 2. 选择 Create > Extended Primitives > Hedra 以在 Create 面板中打开 Extended Primitives 子类别。在 Object Type 展开面板顶部，启用 AutoGrid 选项并选择 Hedra 按钮。
- AutoGrid 选项会在其他对象的表面创建所有新对象。
- 3. 创建几个 Hedra 对象。
- 此时对象的大小并不重要。
- 4. 打开 Modify 面板，并选择其中一个 Hedra 对象。
- 5. 修改 Parameters 展开面板中的值以产生漂亮的宝石。
- 6. 对宝箱中的所有 Hedra 对象重复步骤 5。

图 5.27 显示了具有各种宝石的结果宝箱。

## FIGURE 5.27

通过更改对象参数快速创建的装满宝石的宝箱

![](img/ebbb4844f027f7d1c580e48108d2b6cb_209_0.png)

## Using Architecture Primitives

如果你在 Autodesk 的各个部门游荡，你会遇到几个处理建筑可视化产品的团队，包括众所周知的 AutoCAD 产品。该产品被大量工程师和建筑师用来设计建筑物理结构的布局。

与 AutoCAD 配套的是 Revit，另一个非常受欢迎的软件包，可被视为 Max 的近亲。AutoCAD Revit 用于创建 AutoCAD 数据的可视化，并且像 Max 一样处理建模、渲染和着色 3D 对象。事实上，Max 中找到的许多新功能最初是为 Revit 开发的。

## Using AEC Objects

从 AutoCAD 世界迁移过来的功能中包括建筑中常见的各种建筑对象。所有这些对象都可以在 Create AEC Objects 菜单中找到。AEC Objects 菜单包括许多不同的建筑原语：Foliage、Railings、Walls、Doors、Stairs 和 Windows。

## Foliage

Foliage 类别包括几种不同的植物，所有这些植物都列在 Favorite Plants 展开面板中，并在图 5.28 中显示。可用植物包括 Banyan tree、Generic Palm、Scotch Pine、Yucca、Blue Spruce、American Elm、Weeping Willow、Euphorbia、Society Garlic、Big Yucca、Japanese Flowering Cherry 和 Generic Oak。

## Caution

各种植被对象都是大型模型，如果向场景中添加多个副本，场景会迅速变慢。例如，单个 Banyan tree 有超过 100,000 个多边形。将几个这样的树添加到场景中会使其变得非常缓慢。

### FIGURE 5.28

Favorite Plants 展开面板显示了各种植物的缩略图。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_210_0.png)

在 Favorite Plants 展开面板底部有一个名为 Plant Library 的按钮，打开一个对话框，你可以在其中查看所有植物的详细信息，包括总面数。获胜者是具有 100,000 个面的 Banyan tree。使用 Parameters 展开面板，你可以为每种植物设置 Height、Density 和 Pruning 值。此外，根据树木类型，你可以选择显示 Leaves、Trunk、Fruit、Branches、Flowers 和 Roots，并且可以设置 Level of Detail 为 Low、Medium 或 High。

## Tip

一段时间后，Foliage 集合开始感觉相当有限。你可以使用 Help > 3ds Max on the Web > Download Vegetation 菜单访问 Autodesk Seek 网站。该网站保存了建筑相关对象的存储库，包括大量植物和树木。

## Railings

Railings 选项让你选择护栏将遵循的路径。然后你可以选择用于创建护栏的 Segments 数量。对于 Top Rail，你可以选择使用 No Railing 或 Round 或 Square Profile 并设置 Depth、Width 和 Height。你还可以为 Lower Rails、Posts（出现在任一端）和 Fencing（支撑护栏的垂直隔板）设置参数。

Lower Rails、Posts 和 Fencing 部分具有可用于设置这些元素 Spacing 的图标。打开的 Spacing 对话框看起来与 Spacing Tool 使用的对话框相同，你可以指定 Count、Spacing 值和 Offsets。

## Walls

Walls 很简单，具有 Width 和 Height 参数。你还可以将 Justification 设置为 Left、Center 或 Right。创建墙对象的好处是你可以像连接几个墙对象一样连接它们

