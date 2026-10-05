
## 第3 章：组件
作者：Brian Moakley

到此时，你已经完成了让所有主要演员就绪的目标，但本质上这还是一个空舞台。当然，你可能会因为对缺乏自由意志的深刻见解而获得某些先锋奖，但这并不能帮你付账。

在本章中，你将通过使用**组件（Components）**为你的游戏添加一些交互性，组件是 Unity 游戏开发的基础。如果你将 GameObject（游戏对象）比作一个名词，那么组件就是一个动词，或者说是执行动作的部分；组件会代表 GameObject 执行某些操作。

你已经对组件有了一些了解。在之前的章节中，你学习了每个 GameObject 都有一个必不可少的组件：Transform（变换）组件，它存储了 GameObject 的位置、旋转和缩放。

| Transform | X | Y | Z |
|---|---|---|---|
| Position (位置) | -4.9 | 12.54 | 2.58 |
| Rotation (旋转) | 0 | 0 | 0 |
| Scale (缩放) | 1 | 1 | 1 |

Unity 提供的组件远不止于此。例如，有一个可以产生声音的音频组件（audio）。甚至还有一个粒子系统（particle system）组件，可以生成一些惊叹的视觉效果。当然，如果没有某个能实现你需求的组件，你可以编写自己的。

在本章中，你将学习几种类型的组件，包括 Rigidbody（刚体）组件、脚本（script）组件等。到本章结束时，你的陆战员将能够跑起来并射击了！

# 入门

如果你完成了上一章，请**打开**你当前的 **Bobblehead Wars**（摇头娃娃大战）项目，从你离开的地方继续。如果你卡住了或跳过了，请打开本章资源文件中的 **Bobblehead Wars** 起始项目。

目前，这个太空陆战员只会像雕像一样站着。他需要移动，否则他就会变成外星人的点心。

你将添加的第一个组件是 **Rigidbody**（刚体）组件，它让 GameObject 加入物理引擎。通过添加它，你可以让 GameObject 能够与其他 GameObject 发生碰撞。

当你到达第 4 章“物理（Physics）”时，将学习更多关于刚体和碰撞的知识。现在，只需接受它的现状并继续前进。

# 添加 Rigidbody 组件

在 Hierarchy（层级）中，选择 **SpaceMarine** GameObject，点击 Inspector（检器）中的 **Add Component**（添加组件）按钮。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_73_0.png)

你会看到许多不同的类别。当你知道需要哪个组件时，只需按名称搜索。否则，选择一个类别并挑选最佳选项。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_73_1.png)

点击 Physics（物理）类别，然后选择 Rigidbody。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_74_0.png)

你会看到 GameObject 上挂载了一个 Rigidbody 组件。恭喜你！你添加了第一个组件。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_74_1.png)

每个组件都有自己的一套属性，这些值可以在 Inspector 或代码中更改。组件还有自己的图标，方便一眼看出它们的类型。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_74_2.png)

# 教程系列：Unity 游戏 (Unity Games by Tutorials)

# 第3 章：组件

你会注意到每个组件的右上角有一些图标，如下：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_75_0.png)

第一个图标是引用（Reference）图标。点击它。它会打开另一个窗口，显示该组件的文档页面。如果你安装了文档，页面就在你的电脑上——是的，还有搜索栏。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_75_1.png)

第二个图标是 Unity 2018 的新功能。这是预设（presets）按钮。当你自定义组件时，你可能更喜欢之前创建的某个预设配置。

在 Rigidbody 组件中，勾选 IsKinematic 复选框。同时，取消勾选 Use Gravity（使用重力）选项。你稍后会学习这些选项。一旦取消勾选它们，点击预设按钮。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_75_2.png)
