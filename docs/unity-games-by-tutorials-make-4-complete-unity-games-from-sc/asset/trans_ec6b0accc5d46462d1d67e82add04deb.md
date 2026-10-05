

# 教程：Unity 游戏制作

# 第 1 节：你好 Unity

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_37_0.png)

为了保持整洁，将 Bobble Wars 陆陆队的纹理从 Models 文件夹移动到 Textures 文件夹。纹理是材质（Materials）的基础。

你可能会问，什么是材质？材质根据光照条件为你的模型提供颜色和纹理。材质就是我们所知的着色器（shaders），它们最终决定了屏幕上显示的内容。着色器是用特定的着色器语言编写的小程序，这远超本入门书的范围。你可以通过 Unity 自带的文档学习更多关于材质的知识。

返回 Models 文件夹并选择 BobbleMarine-Body。Inspector（检检器）现在将显示该模型的特定信息以及一个预览。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_37_1.png)

如果你没有看到预览，说明你的窗口关闭了。在 Inspector 的底部找到一条灰色条，然后用鼠标向上拖动以展开预览。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_38_0.png)

Inspector 允许你修改模型的配置，并允许更改任何所选对象的属性。由于不同对象之间可能存在巨大差异，Inspector 会根据所选对象切换上下文。

# 安装 Blender

此时，你已经导入了太空陆陆队的模型和纹理。模型是 FBX 格式，纹理是 .PSD 格式。

我们以 .FBX 格式向你提供了太空陆陆队模型，因为这是艺术家交付资产的流行格式。但还有另一个流行的格式你也应该学会如何使用：Blender 文件。

与 .FBX 不同，Blender 文件包含源模型数据。这意味着你实际上可以在 Blender 内部编辑这些文件，并且更改将立即在 Unity 中生效，而 .FBX 文件则不然。

使用 .FBX 时，你每次更改模型都需要将其导出并重新导入 Unity。

所有这些强大的功能也需要一个小小的权衡。为了让 Unity 能够与 Blender 文件配合工作，你需要在电脑上安装 Blender。Blender 是免费的，而且你会高兴地知道，在几章节之后你将用它制作自己的模型。

在以下 URL 下载并安装 Blender：https://www.blender.org/download/

# 创意从这里开始

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_39_0.png)

**注意：** Blender 的演进非常快，因此你在桌面上看到的版本可能与此截图不同。

安装 Blender 后，运行程序然后退出。就是这样——你现在可以在 Unity 中使用 Blender 文件了。

## 导入包

现在你已经安装了 Blender，可以导入其余资产了。

其余资产被组合在一个名为 **Unity package**（Unity 包）的单个包中。这是艺术家为 Unity 交付资产的常用方式，特别是当你从 Unity 商店购买它们时。

让我们尝试导入包。选择 **Assets\Import Package\Custom Package...**，导航到资源文件夹并选择 **BobbleheadWars.unitypackage**，然后点击 **Open**（打开）。

你将看到该包中包含的资产列表，所有资产默认都已选中。注意，其中一些是 Blender 文件，还有其他如纹理和声音的文件。点击 Import（导入）按钮将它们导入 Unity。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_40_0.png)

导入将为你的项目添加许多额外的资产。如果你收到警告，直接忽略它即可。

为了保持整洁，单击新生成的 Materials 文件夹（在 Models 文件夹中）并将其重命名为 Models。将此新文件夹拖到父级 Materials 文件夹中。

# 将模型添加到 Scene 视图

此时，你已将所有内容导入到 Unity。是时候开始制作你的游戏了，你将通过将模型添加到 Scene（场景）视图来启动。

Scene 视图是游戏创作的地方。这是一个 3D 窗口，你可以在其中放置、移动、缩放和旋转对象。

首先，确保选中 Scene 视图标签页。然后在 Project Browser（项目浏览器）中，从 Models 子文件夹选择 BobbleArena 并将其拖入 Scene 视图。

# 教程：Unity 游戏制作

# 第 1 节：你好 Unity

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_41_0.png)

查看 Scene 视图中的竞技场：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_41_1.png)

很酷对吧？
Scene 视图为你提供了一种在 3D 空间中导航游戏的方法：

- **右键点击并旋转鼠标**环顾四周。
- **按住右键**并使用 **WASD 键** 实际穿过场景移动。
- 移动太慢了？按住 **Shift** 键。
- **滚动滚轮**进行缩放。
- **移动鼠标**进行平移。

# 教程：Unity 游戏制作

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_41_0.png)

# 教程：Unity 游戏制作

默认情况下，视图以着色模式显示所有内容。你可以切换到线框模式（wireframes）。让我们尝试一下。在 Scene 标签中，点击下拉菜单并选择 Wireframe。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_42_0.png)

# 教程：Unity 游戏制作

将 Scene 视图切换回着色。你会注意到右角有一个坐标轴（gizmo）。这意味着视图处于透视模式；离你远的物体更大。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_42_1.png)

# 教程：Unity 游戏制作

点击轴将改变你的视角。例如，点击绿色 y 轴，场景将从俯看。这种感觉如何？

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_43_0.png)

# 教程：Unity 游戏制作

点击中心框将视图切换到正交（Isometric）模式。本质上，无论远近，物体的大小都是相同的。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_43_1.png)

# 教程：Unity 游戏制作

# 添加英雄

此时，你已经设置好了竞技场，但还缺少主角！
为了修复这个问题，在 Project Browser 中找到并打开 Models 文件夹，然后将 **BobbleMarine-Body** 拖入 Hierarchy（层级视图）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_44_0.png)

在 Unity 中，游戏按场景（scenes）组织。现在，你可以将场景看作一个关卡。Hierarchy 视图是当前场景中所有对象的列表。

注意你的场景已经包含了几个对象。此时，它包含了竞技场、太空陆陆队以及两个默认对象：主摄像和一个方向光。

在保持模型体被选中状态的情况下，将鼠标悬停在 Scene 视图上并按 **F** 键缩放到陆陆队。当你场景中有许多对象并需要快速找到其中一个时，这个快捷键非常有用。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_45_0.png)

不要担心你的太空陆陆队没有放在这个精确的位置。稍后我们会修复。

你会注意到当一个对象被选中时，该对象周围会出现一个轮廓。Unity 经常根据版本更改选中对象的轮廓颜色。

在 Unity 2018 中，新项目具有红色轮廓。这是由于编辑器新的默认颜色空间引起的。颜色空间决定了引擎如何混合颜色。它还决定了游戏可以支持哪些设备和平台。

目前，最好使用默认颜色设置，但你可以轻松地将红色改为橙色。你可以通过选择 Windows 上的 **Edit,Preferences** 或 macOS 上的 **Command-,** 来更改颜色。在 Preference 窗口中选择 **Colors**，你将看到所有可以自定义的颜色列表。要更改选择轮廓字段。

