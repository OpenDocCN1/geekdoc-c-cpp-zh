
你无疑已经看到了可以对游戏进行的一些调整。尝试不同的地图布局；添加或更改出生位置；甚至为地图上的强化道具设置有限的生存寿命——慢一秒，就会错失良机！

创建一个 FPS 游戏是一门真正的艺术，它既要足够直观以便于上手，又需要一些时间来精通；游戏在前几个关卡要足够简单以吸引玩家，但需要通过反复游戏来学习征服游戏的微妙策略。任何游戏最重要的部分都是与各种玩家进行测试玩，以找到创造沉浸式体验的“平衡点”。

祝射击愉快！

## 第三节：2D 平台游戏

到目前为止，你一直在使用 Unity 制作 3D 游戏。但 Unity 也提供了高级的 2D 支持，这本节的重点。

具体来说，你将学习如何使用 Unity 创建一个节奏快速 2D 平台游戏，其中一个脆弱的豆腐块将直面恐怖的关卡：**超级大豆小子（Super Soy Boy!）**

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_326_0.png)

- 第 12 章，“Unity 2D 入门”
- 第 13 章，“更多 Unity 2D”
- 第 14 章，“保存数据”

## 第 12 章：Unity 2D 入门
作者：Sean Duffy

你想学习如何用 Unity 制作 2D 游戏吗？你来对地方了。在本章中，你将学习如何利用 Unity 的 2D 工具和组件来创建一个游戏，其中一个脆弱的豆腐块将直面恐怖的关卡。

你将从学习 2D 基础开始，然后编写一个非常有趣的平台游戏。在整个过程中，你将学会如何自信地处理自己的 2D 项目！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_327_0.png)

这款游戏是一个控制极其灵敏的 2D 平台游戏。你将引导超级大豆小子在障碍物中穿梭，同时进行、跳跃和贴墙。他正急着去到达关卡末尾的一碗热腾腾的面条。

虽然缓慢、深思地通过障碍是可能的，但最有趣的游戏体验将来自于以一个连贯的动作通过关卡。这并不是为了欣赏风景或仔细计算你的下一步！

### 入门

Unity 丰富的特性列表和组件使你能够创建引入胜目的 2D 游戏。除了精灵（sprites）、动画和物理碰撞体等标准组件外，你还获得了专门的物理、关节（joints）和区域效应器组件。在你创建超级大豆小子时，你将探索最常用且实用的 2D 组件。它们通常与碰撞体配合工作。

要开始你的 2D 之旅，请在 Unity 中打开本章的启动项目（Starter project）。它包含了你所需的所有资源和精灵。加载位于 Scenes 子文件夹下的 Game 场景。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_328_0.png)

### 精灵（Sprites）：2D 游戏的构建块

你所需的所有精灵都在 Assets Sprites 子文件夹中。在 Sprites 文件夹中找到 `single-block.png` 精灵，然后将其拖入 Scene 窗口。

### 教程系列 Unity 游戏

恭喜！你创建了你的第一个精灵。就这么简单。

Unity 自动创建了一个 GameObject，并挂载了 SpriteRenderer，同时分配了精灵纹理。查看检查器（Inspector）以确认 GameObject 在创建时带有 Transform 和 SpriteRenderer 组件。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_329_0.png)

你可能想奇 Sprites 子文件夹中的白色精灵是怎么回事。答案很简单：你可以轻松地在游戏中为它们上色，或者在编辑器中使用你选择的颜色上色，而无需为每种颜色都创建精灵。

`single-block` 精灵将作为地面的基础块——即超级大豆小子运行的平台。基于此，你将其涂成棕色以代表地形。

在层级面板（Hierarchy）中，选择 `single-block` GameObject 并点击检查器中的 Color 调出颜色选择器。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_329_1.png)

输入十六进制值：#59443C。关闭颜色选择器。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_329_2.png)

由于精灵的基础颜色是白色的，新的棕色完美地填充了它。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_330_0.png)

> 注意：你可以像操作任何其他 GameObject 一样操作精灵。例如，你可以使用 Transform 组件和编辑器中的 Unity 工具更改它的缩放、位置和旋转。

精灵有几种可以设置的不同模式。你将关注 Single（单图）和 Multiple（多图）。你在创建 `single-block` GameObject 时已经看到了如何使用精灵，但 Multiple 模式呢？它们是使用多个元素的特殊精灵，通常称为纹理图集（texture atlas）。

-   **Single**: 单个图像精灵。
-   **Multiple**: 具有多个元素的精灵。例如，它可能有几个版本——如手臂、腿和躯干。使用 single 意味着游戏中的每张图像都占用一个绘制调用（draw call），如果你只处理几个精灵，这并不是什么问题。然而，随着游戏复杂性和规模的增长，single 会导致性能问题。使用精灵集（spritesheets），你只需为多个精灵执行一次绘制调用，从而降低性能消耗。

大豆小子使用 Multiple 模式，这样动画帧——跑步、跳跃和滑行——就存储在一个精灵集中。在 Sprites 子文件夹中选择 `SuperBoySpriteSheet.png`，并确保 Sprite Mode 设置为 Multiple。如果你更改了设置，点击 Apply。

## 教程系列 Unity 游戏第 12 章：Unity 2D 入门

| 纹理类型 (Texture Type) | 精灵 (2D and UI) |
| :--- | :--- |
| 纹理形状 (Texture Shape) | 2D |
| 精灵模式 (Sprite Mode) | Multiple |
| 打包标签 (Packing Tag) | |
| 单位像素 (Pixels Per Unit) | 100 |
| 网格类型 (Mesh Type) | Tight |
| 边缘挤出 (Extrude Edges) | 1 |
| 生成物理形状 (Generate Physics Shape) | |

| Sprite Editor | |

点击 Sprite Editor 按钮打开其窗口。你会看到精灵集的放大视图。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_331_0.png)

你有几种方法可以将精灵集切分为单个精灵。对于本次练习，你使用 Grid By Cell Size 方法。

| 按单元格大小网格切片 | |
| :--- | :--- |
| 像素大小 (Pixel Size) | 48 40 |
| 偏移 (Offset) | 0 0 |
| 间距 (Padding) | 0 0 |
| 轴心 (Pivot) | Center |
| 自定义轴心 (Custom Pivot) | Slice |

点击 Sprite Editor 左上角的下拉菜单将 Type 改为 Grid By Cell Size。将 Pixel Size 设置为 (48, 40)，保持其他选项不变。所有大豆小子的动画帧都是 48x40 像素。因此，你使用了这些值进行切片。点击。

查看 Sprite editor。你会看到精灵周围的边界框，显示了应用网格切片的位置。

### 应该还有三行精灵。第一行包含所有的跑步精灵，中间行是跳跃，底部是单个的滑行精灵。

在 Sprite editor 中选择每个精灵并相应命名：

- 第一行：run_0, run_1, run_2, ..., run_14
- 中间行：jump_0, jump_1, jump_2, ..., jump_14
- 底部：slide_0

这种命名规范让你清晰地看出哪些帧属于哪些动画。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_332_0.png)

点击 Apply 将更改提交到精灵。关闭 Sprite editor。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_332_1.png)

还有其他切片模式虽然你现在用不到，但了解它们是有用的：

-   **Automatic（自动）**: 尝试通过寻找边界框来自动定位并切割精灵。在处理复杂形状时，它并不总是准确。
-   **Grid By Cell Count（按单元格数量网格切片）**: 你将精灵集划分为定义的列和行。
-   **Grid By Cell Size（按单元格大小网格切片，已在上）**: 你根据精灵的宽度和高度进行分割。只要它们排列在一起，这种技术就有效。

