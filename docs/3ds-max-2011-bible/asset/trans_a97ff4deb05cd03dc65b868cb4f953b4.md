

## 浏览 Schematic View 窗口

随着节点数量的增加，定位并查看要操作的正确节点可能会变得棘手。Schematic View 窗口底部边缘有几个导航按钮，其工作原理与 Viewport Navigation Control 按钮类似。使用这些按钮，您可以平移、缩放以及缩放至所有节点的范围。这些按钮在表 25.2 中进行了描述。

Schematic View 导航按钮也可以通过 View 菜单访问。这些菜单命令包括 Pan Tool（Ctrl+P）、Zoom Tool（Alt+Z）、Zoom Region Tool（Ctrl+W）、Zoom Extents（Alt+Ctrl+Z）、Zoom Extents Selected（Z）和 Pan to Selected。

### Tip

您还可以使用鼠标及其滚动轮浏览 Schematic View 窗口。滚动鼠标滚轮可分步放大和缩小窗口。按住 Ctrl 键并使用滚动轮按钮拖动可平滑放大和缩小窗口。拖动滚动轮可在窗口内平移。

## TABLE 25.2

## Schematic View Navigation Buttons

| Toolbar Button | Name | Description |
|---|---|---|
|  | Zoom Selected Viewport Object | 将焦点缩放到与所选视口对象对应的节点上 |
| Search | Search Name field | 输入名称时定位对象节点 |
|  | Pan | 拖动窗口时移动节点视图 |
|  | Zoom | 在窗口中拖动鼠标时缩放 |
|  | Region Zoom | 拖动轮廓选择区域时缩放至该区域 |
|  | Zoom Extents | 放大窗口视图直到所有节点都可见 |
|  | Zoom Extents Selected | 放大窗口视图直到所有所选节点都可见 |
|  | Pan to Selected | 在当前缩放级别下将节点视图移动到所选对象 |

## Working with Schematic View nodes

场景中显示的每个对象都有一个节点——一个代表对象或属性的简单矩形框。每个节点都包含一个标签，并且节点的颜色取决于节点类型。

### Node colors

节点具有配色方案以帮助识别它们。各种节点的颜色在表 25.3 中列出。

## Part VI: Advanced Modeling

**TABLE 25.3**

### Schematic View Node Colors

| Color | Name |
|---|---|
| White | Selected node |
| Blue | Geometry Object node |
| Cyan | Shape/Object node |
| Yellow | Light Object node |
| Dark Blue | Camera Object node |
| Green | Helper Object node |
| Purple | Space Warp Object node |
| Goldenrod | Modifier node |
| Dark Yellow | Base Object node |
| Brown | Material node |
| Dark Green | Map node |
| Salmon | Controller node |
| Magenta | Parameter Wires |

### Note

如果您不喜欢这些颜色中的任何一种，可以使用 Customize ▸ Customize User Interface 对话框的 Colors 面板设置 Schematic View 中使用的颜色。

## Selecting nodes

单击 Select（S）按钮时，您将进入选择模式，这使您可以通过单击对象节点在 Schematic View 窗口中选择节点。您可以通过拖动轮廓围绕它们来选择多个对象。按住 Ctrl 键同时单击对象节点可选择或取消选择它。所选节点显示为白色。

Select 菜单包含多个选择命令，可让您快速选择（或取消选择）多个节点，包括 Select All（Ctrl+A）、Select None（Ctrl+D）、Select Invert（Ctrl+I）、Select Children（Ctrl+C）和 Deselect Children。

如果 Select 菜单中的 Select ▸ Sync Selection 选项已启用，则在视口中选择的任何对象的节点也会在 Schematic View 窗口中被选中，反之亦然。如果禁用 Sync Selection 选项，则可以同时在视口和 Schematic View 中选择不同的对象。视口中选中的对象的节点以白色轮廓显示，所选节点的内部为白色。要在未启用 Sync Selection 选项的情况下选择与所选节点匹配的视口中的所有对象，只需使用 Select ▸ Select to Scene。Select ▸ Select From Scene 会为视口中选择的所有对象选择节点。

### Tip

所有动画对象的节点边框均以红色绘制。

## Chapter 25: Working with the Schematic View

## Rearranging nodes

Schematic View 包含多个排列节点的选项。在 Options 菜单中，您可以在 Hierarchy 和 Reference 模式之间切换。Hierarchy 模式以垂直方式显示节点，子对象在其父对象下方缩进。Reference 模式以水平方式显示节点，为每个父节点下的各种引用节点提供充足的显示空间。图 25.2 并排显示了这两种模式。

## FIGURE 25.2

Schematic View 窗口可以自动以两种不同模式排列节点：Hierarchy 和 Reference。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_724_0.png)

您可以移动节点并按任意顺序重新排列它们。要移动节点，只需单击并将其拖动到新位置。当节点被拖动时，所有选中的节点一起移动，任何链接都会跟随节点移动。如果子节点被移动，所有剩余的子节点会收拢在一起以保持指定的排列模式。移动后的节点随后变为自由状态，这由节点左侧边缘的开放矩形表示。图 25.3 显示了两个被移动从而变为自由的节点。其他子节点会自动靠拢以填补移动节点留下的空隙。

使用 Layout ⇨ Free Selected（Alt+S）和 Free All（Alt+F）菜单命令，您可以释放所选节点或所有节点。您还可以使用 Layout ⇨ Arrange Children 菜单命令指定节点的全部子节点自动排列，或仅排列所选节点（Layout ⇨ Arrange Selected）。Options ⇨ Move Children（Alt+C）命令会在父节点移动时将其所有子节点一起移动。这会导致自由和非自由节点随其父节点移动。

如果启用了 Options ⇨ Always Arrange 选项，则 Max 会使用 Hierarchy 或 Reference 模式自动排列所有节点，但在启用此选项时您无法移动任何节点。如果在选择了 Always Arrange 选项时移动了任何节点，将出现一个对话框，提示您的自定义布局将被丢失。如果启用了 Always Arrange 选项，则 Arrange Children、Free All（Alt+F）、Free Selected（Alt+S）、Move Children（Alt+C）以及所有 Align 选项都将被禁用。如果选择了两个或多个节点，您可以使用 Layout ⇨ Align 菜单将它们对齐。选项包括 Left、Right、Top、Bottom、Center Horizontal 和 Center Vertical。

## Hiding, shrinking, and deleting nodes

如果您的 Schematic View 窗口开始变得杂乱，您始终可以隐藏节点以简化视图。要隐藏节点，请选择要隐藏的节点并使用 Display ⇨ Hide Selected 菜单命令。Display ▸ Unhide All 菜单命令可用于再次显示隐藏的节点。

## FIGURE 25.4

Shrunken nodes appear as simple dots in the Schematic View.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_726_0.png)

要重新排列太阳系节点，请按照以下步骤操作。

- 1. 从 DVD 上的 Chap 25 目录打开 Ordered solar system.max 文件。
  该文件包含几个代表太阳系的命名球体。
- 2. 选择 Graph Editors ▸ New Schematic View 以打开 Schematic View 窗口。
  所有行星都显示为太阳对象下的蓝色节点。
- 3. 选择 Options ▸ Reference Mode（如果尚未选择）以将所有节点水平放置。单击主工具栏上的 Select 工具（或按 S 键）。
- 4. 确保 Options ▸ Always Arrange 选项已禁用。然后单击并拖动 Mercury 节点到左侧，并将其放置在 Venus 节点前面。
- 5. 选择 Options ▸ Move Children（Alt+C）菜单命令，并将 Saturn 节点拖放到 Jupiter 和 Uranus 节点之间。
  启用 Move Children 选项时，Saturn rings 节点会随其父节点移动。
- 6. 将 Pluto 节点拖放到 Neptune 节点之外。
- 7. 选择所有行星节点，然后选择 Layout ▸ Align ▸ Top 以将所有节点对齐。

### Note

尽管天文学家不再将 Pluto 分类为行星，但我怀疑这本书是天文学家必读的。我想我们可以继续称 Pluto 为行星。

图 25.5 显示了重新排列的层次结构，所有行星按顺序排列。

