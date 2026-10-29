

# 第四部分：材质、摄像机和灯光基础

如果您对应用到物体上的材质或贴图不满意，并且调整也无济于事，您可以随时通过移除应用到物体上的材质或任何贴图来回到起点。用于移除材质和贴图的工具是 UVW Remove 实用工具。您可以通过点击工具面板中的 More 按钮并从实用工具列表中选择 UVW Remove 来访问此实用工具。

## 图 15.4

Slate Material Editor Options 对话框为控制 Slate Material Editor 窗口提供了许多选项。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_493_0.png)

此实用工具包含一个单一的展开面板，列出了所选物体的数量。它还包含两个按钮。UVW 按钮会从所选物体中移除任何映射坐标，而材质按钮会从所选物体中移除任何材质。此按钮会将所选物体的原始物体颜色恢复。或者，您也可以选择 Set Gray 选项，这将在移除材质时使所选物体变为灰色。

## 使用 Fix Ambient 实用工具

标准材质类型始终将 Ambient 和 Diffuse 颜色锁定在一起。如果您有旧文件，其 Diffuse 和 Ambient 颜色未锁定，则可以使用 Fix Ambient 实用工具来定位并修复场景中所有具有此条件的材质。要访问此实用工具，请打开 Utilities 面板，点击 More 按钮，并选择 Fix Ambient 实用工具。点击 Find All 按钮会打开一个对话框，列出场景中所有 Diffuse 和 Ambient 颜色未锁定的材质。

## 教程：给复活节彩蛋上色

每个人都喜欢春天，喜欢它明亮的色彩和生命的焕发。季节的亮点之一就是给复活节彩蛋上色的传统。在本教程中，您将使用虚拟彩蛋——没有凌乱的染料，也没有接下来两周的蛋沙拉三明治。

# 第 15 章：使用 Slate Material Editor

要创建您的虚拟复活节彩蛋并为其应用不同的颜色，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 15 目录打开 Easter eggs.max 文件。此文件包含多个蛋形物体。
- 2. 通过选择 Rendering ➜ Material Editor ➜ Slate Material Editor（或按 M 键）打开 Slate Material Editor。
- 3. 在 Material/Map Browser 中双击 Standard 材质。在 Node View 中选择材质节点，然后在 Parameter Editor 面板中点击 Diffuse 颜色色块。从出现的 Color Selector 中，将光标在调色板上拖动直到找到您想要的颜色，然后点击 Close。
- 4. 在任意视口中选择一个蛋，然后在 Material Editor 中点击 Assign Material to Selection 按钮，或者您可以直接从材质节点的输出插槽拖动到视口物体上。
- 5. 对所有彩蛋重复步骤 4 和 5。

图 15.5 显示了我们刚刚创建的彩蛋组合。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_494_0.png)

这些彩蛋已被赋予了具有不同 Diffuse 颜色的材质。

右键弹出菜单还提供了一个创建新库的选项。新的库也可以通过右键弹出菜单保存和加载。

# 注意

Max 附带了多种材质库，包括 Backgrounds、Bricks、Concrete、Fabric、Ground、Metal、Nature、RayTraced、ReflectionMaps、Skys、Space、Stones、Wood 以及多个建筑材质集。您可以在 matlibs 目录中找到所有这些库。

使用 Material/Map Browser Options ⇨ Additional Options ⇨ Save Layout As 保存当前材质的布局。这些文件以 .mpl 扩展名保存。

# Cross-Ref

虽然材质可以保存为库，但也许在应用程序之间共享材质的最简单方法是使用 Material XML Export 实用工具或 Material ⇨ Export As XML File 命令。

# 教程：加载自定义材质库

为了练习加载材质库，我使用 Kai's Power Tools 创建的各种纹理创建了一个自定义材质库。

要将自定义材质库加载到 Slate Material Editor 中，请按照以下步骤操作：

- 1. 选择 Rendering ⇨ Material Editor（或按 M 键）以打开 Material Editor。然后确保 Material/Map Browser 处于活动状态，或选择 Tools ⇨ Material/Map Browser 菜单以打开 Material/Map Browser。
- 2. 选择 Material/Map Browser Options ⇨ Open Material Library 菜单。
- 3. 从 DVD 上的 Chap 15 目录中选择并打开 KPT samples.mat 文件。库将加载到 Material/Map Browser 中。
- 4. 在 Search 字段（样本槽上方）中输入 Bug 以定位并选择 bug eyes 材质。

图 15.7 显示了 Material/Map Browser 中打开的自定义材质库。

# 使用 Material Explorer

Scene Explorer 已得到很好的认可，并且使处理场景物体变得更加容易。容易到 Max 团队寻找其他可以采用类似界面的地方，而第一个目标就是材质。其结果就是 Material Explorer。

Material Explorer，如图 15.8 所示，让您能够在一个界面中快速查看所有场景材质及其层次结构和所有属性。它还允许您按各种属性对材质进行排序，甚至可以同时更改多个材质。您可以通过 Rendering ⇨ Material Explorer 命令访问 Material Explorer。

Material Explorer 与 Scene Explorer 完全一样，并且具有可配置的列。它分为两个面板。顶部面板显示当前场景中的所有材质；底部面板显示所选材质或子材质的层次结构。

除了菜单之外，几个工具栏按钮水平排列在菜单下方，几个显示按钮垂直排列在界面左侧。这些按钮在表 15.2 和 15.3 中进行了描述。

# 第四部分：材质、摄像机和灯光基础

## 图 15.7

Material/Map Browser 还允许您使用已保存的自定义材质库。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_497_0.png)

# Cross-Ref

要了解更多关于 Scene Explorer 界面的信息，请参阅第 6 章“Selecting Objects and Setting Object Properties。”

## 图 15.8

Material Explorer 将分层材质显示为层次结构。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_497_1.png)

Scene panel

Material panel

### 表 15.2

#### Material Explorer 显示按钮—垂直

| 工具栏按钮 | 名称 | 描述 |
|---|---|---|
| [图标] | Display Thumbnails | 以样本槽中显示的方式显示各种材质组件的缩略图 |
| [图标] | Display Materials | 在层次结构中包含材质 |
| [图标] | Display Maps | 在材质层次结构中包含贴图 |
| [图标] | Display Objects | 在材质层次结构中包含应用的物体 |
| [图标] | Display Sub-Materials/Maps | 在材质层次结构中包含任何应用的子材质/贴图 |
| [图标] | Display Unused Map Channels | 将所有未使用的贴图通道作为层次结构的一部分包含在内 |
| [图标] | Sort by Object | 根据材质应用的物体对材质进行排序并列在下方 |
| [图标] | Sort by Material | 对材质进行排序并列出下方的物体 |

### 表 15.3

#### Material Explorer 工具栏按钮—水平

| 工具栏按钮 | 名称 | 描述 |
|---|---|---|
| Find | Find 文本字段 | 允许搜索特定命名的材质和贴图 |
| [图标] | Select All Materials | 选择场景中的所有材质 |
| [图标] | Select All Maps | 选择场景中的所有贴图 |
| [图标] | Select All | 选择列表中的所有条目 |
| [图标] | Select None | 取消选择列表中的所有条目 |

*continued*

# 第四部分：材质、摄像机和灯光基础

**表 15.3（续）**

**Material Explorer 工具栏按钮—水平**

| 工具栏按钮 | 名称 | 描述 |
|---|---|---|
| [icon] | Select Invert | 反转当前选择 |
| [icon] | Lock Cell Editing | 锁定所有单元格使其无法编辑 |
| [icon] | Sync to Material Explorer | 导致在顶部面板中选择的材质在下部面板中可见 |
| [icon] | Sync to Material Level | 在启用时在下部面板中显示所选材质的整个层次结构 |

Material Explorer 允许您通过简单地将材质缩略图拖放到物体上来直接将材质应用到场景物体。您也可以将贴图拖放到其他材质和通道上。Material Explorer 也与 Material Browser 配合使用；例如，您可以将材质类型拖动并放到 Material Explorer 中的 Type 列上以更改材质类型。

# 总结

材质可以为您的模型增添很多真实感。学习使用 Material Editor、Material/Map Browser 和 Material/Map Navigator 使您能够处理材质。本章涵盖了以下主题：

- 理解各种材质属性
- 使用 Material Editor 按钮和样本槽
- 使用 Material/Map Browser 和材质库
- 使用 Material Explorer 快速查看场景中的所有材质

下一章将更深入地探讨材质主题，包括标准材质及其所有设置。

