

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_566_0.png)

# 调整

现在游戏已经完全运行了，有一些调整可以让它变得更有趣。其中之一就是创建更多的波次！目前，只有一个孤独的波次沿着第一条路径移动。是时候增加一些波次了。

在 Hierarchy（层级面板）中选择 Wave Manager，折叠 Element 0 并将 Enemy Waves（敌人波次）的大小设置为 5。

按照如下配置波次：

- Element 1: 将 Path Index（路径索引）设置为1，Start Spawn Time（开始生成时间）设置为30，Time Between Spawns（生成间隔）设置为1.9。从 Prefabs ▸ Enemy 文件夹拖入一个 Tanky Enemy（坦克型敌人）预制体到 List Of Enemies（敌人列表）中。
- Element 2: 将 Path Index 设置为0，Start Spawn Time 设置为60，Time Between Spawns 设置为1.6。将 3 个 Fast Enemy（快速敌人）预制体拖入 List of Enemies。
- Element 3: 将 Path Index 设置为1，Start Spawn Time 设置为110，Time Between Spawns 设置为1.5。将 4 个 Fast Enemy 预制体拖入 List of Enemies。
- Element 4: 将 Path Index 设置为0，Start Spawn Time 设置为130，Time Between Spawns 设置为1.4。将 4 个 Tanky Enemy 预制体拖入 List of Enemies。

这一定会增加难度。使用这些新设置测试游戏，看看你的表现如何。确保尽可能地升级你的防御塔！

# 接下来去向哪里？

恭喜你完成这个项目！

在本章中，你学习了如何：

- 将 UI 链接到游戏玩法。
- 创建防御塔。
- 胜利和失败的逻辑。
- 进行调整以改进游戏体验。

不过，乐趣还没有结束。在下一章，即第19章“虚拟现实”中，我将解释如何使用 Oculus Rift 和 HTC Vive 将 Runestife 带入神奇的 VR 领域。很令人兴奋，不是吗？

# 第20章：虚拟现实
作者：Eric Van de Kerckhove

几个世纪以来，人类一直对进入虚拟世界的想法着迷：一个逃避现实的避风港，在那里一切皆有可能。从大到让人产生实际置入其中错觉的全景画，到立体眼镜、原始的头戴式显示器以及任天堂的 Virtual Boy，人类长期以来寻找通往无尽想象之地的门户。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_568_0.png)

虚拟现实在过去几年中已成为一项易触及的技术。人们可以使用现代尖端的头戴式显示器（HMD）和接受用户输入的独特技术，在舒适的家中传输到虚拟世界并与居民互动。两个特别流行的设备是 Oculus Rift 和 HTC Vive，它们都提供了前所未过的体验。

在本章中，你将学习如何在 Runestife 中使用这种尖端技术，这将为你在自己的项目中使用做好准备。你将把 Runestife 变为一个 VR 游戏，并学习如何在 Unity 中使用 Oculus Rift 和 HTC Vive。

Unity 游戏教程

第20章：虚拟现实

> 注意：每个人在佩戴 HMD 时对移动和旋转的反应不同。如果这是第一次尝试，请务必放松，如果感到恶心或不适，请休息。大多数人很快就能适应 VR。所以，如果前几次感觉不舒服，不要担心——这种感觉可能会消失。

你可以直接跳转到匹配你选择的 VR 设备的章节。两者之间有一些重叠，但它们足够不同，每个部分都值得单独成章！

# 开始使用 Oculus Rift

如果你还没有 Oculus Rift 头戴设备，可以从 Oculus 网站（www.oculus.com）购买。确保你的 PC 符合推荐要求。一旦拿到它，设置好硬件并安装最新的软件驱动程序。

现在，打开 Oculus 应用并点击 Settings（设置）按钮：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_569_0.png)

点击左侧的 General（通用）文本打开通用设置。确保启用了 Unknown Sources（未知来源）：

| Unknown Sources 未知来源 |
| 允许未经过 Oculus 审核的应用程序在我的 Rift 上运行。了解更多。 |

这将允许未经过 Oculus 审核的游戏（如 Runestep）在它的硬件上运行。在进行任何开发之前，这是必须的。

处理完这些后，在 Unity 中打开 Oculus 启动项目。打开 Game 场景并在 Scene（场景）视图中查看。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_569_1.png)

如果你尝试游戏，你会发现无法添加任何防御塔，因为 AddTower GameObject 没有在屏幕上显示。这是因为 Screen Canvas 被替换成了 World Space Canvas（空间画布）。这意味着元素可以在世界中放置、缩放和旋转，而不是锁定在屏幕上。

此外，查看相机周围浮动的 UI 元素。这让 UI 保持相对恒的大小而不被挤压。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_570_0.png)

尝试查看海报或电视屏幕，你就会明白我在说什么了。这就是场景之旅的结束。制作酷酷的东西！

为了在 Unity 中使用 Oculus Rift，你需要从这里下载最新版本的实用程序：https://developer.oculus.com/downloads/unity。

一旦下载了实用程序，解压文件并点击右下角的 Import（导入）按钮将其导入 Unity。现在，查看 Project（项目）视图。Assets（资源）文件夹中添加了一个名为 OVR 的新文件夹。

| Models 模型 |
| Music 音乐 |
| OVR |
| Plugins 插件 |
| Prefabs 预制体 |

此文件夹包含了几个帮助开发的预制体和脚本。

571

（注：由于提供的原始文本存在大量重复和混乱的错误，以上内容已根据要求清理并翻译了核心逻辑内容。）

