
Start 函数会保持休眠状态，但一旦对象被激活，它就会立即启动。然而，Awake 函数中的任何内容无论对象是否激活都会运行。

这一切之所以对我们很重要，是因为我们可以让脚本自行找到两个 DataPanel，并替我们填充 OpenSceneButtonsScript 的变量（无需手动填充）。在大多数需要定义变量的情况下，都应该使用 Awake 函数，因为变量的定义应该在一开始就完成。

## 警告与常见陷阱

有些代码行的长度超出了书籍排版所允许的范围。请记住，每条语句结尾通常都会换行，并且每条语句都以“;”结束。因此，如果此处显示的某一行代码不是以“;”或“{”（对于代码块）结尾，请将其保持为连续的代码行。

**步骤 40：** 重新打开 OpenSceneButtonsScript。将变量声明替换为以下内容：

```javascript
private var dataPanelBiography : GameObject;
private var dataPanelMission : GameObject;

function Awake () {
    dataPanelBiography =
        GameObject.Find("DataPanel_Biography");
    dataPanelMission =
        GameObject.Find("DataPanel_Mission");
}

function OnMouseEnter () {
    guiTexture.color = Color (1,1,1);
}

function OnMouseExit () {
    guiTexture.color = Color (.2,.2,.2);
}

function OnMouseDown () {
    if (name == "Button_Bio") {
        dataPanelBiography.guiTexture.enabled = true;
        dataPanelMission.guiTexture.enabled = false;
    }
    if (name == "Button_Mission") {
        dataPanelMission.guiTexture.enabled = true;
        dataPanelBiography.guiTexture.enabled = false;
    }
    if (name == "Button_Begin") {
        Application.LoadLevel ("Scene-EntryWay");
    }
}
```

## 警告与常见陷阱

GameObject.Find 是一个非常方便的工具。然而，它也可能很快被滥用。例如，如果 GameObject.Find 位于 Update 函数中，那就意味着每帧都要要求 Unity 去查找一个对象。如果这样的调用非常多，Unity 就会忙于查找对象，而不是运行游戏。通常，应该在只需触发一次的情况下使用 GameObject.Find（例如在 Awake 函数中，或在另一个于特定时刻调用的函数中）。

## 为什么这样做？

这里发生了两件事。首先，每个变量声明前都添加了 private。private 变量是可以被定义的变量，但不会像我们之前那样通过拖拽项目在 Unity 编辑器中定义。虽然这些变量也可以保持为 public，但由于它们将在脚本中定义，这样可以避免其他开发者尝试（或觉得需要）去填充变量。接下来是 Awake 函数部分。它使用了方便的 GameObject.Find 功能。这些代码语句定义了前面声明的两个变量，具体做法是查找名称分别与 DataPanel_Biography 和 DataPanel_Mission 匹配的 GameObject。

- **步骤 41：** 保存并返回 Unity。
- **步骤 42：** 选择任意按钮，注意 public 变量已经消失。但请注意，在运行游戏时，一切仍然正常工作。

## Application.LoadLevel

最后一个按钮，即 Begin 按钮，使用了 Application.LoadLevel 函数。这使我们能够从一个 Unity 场景切换到另一个场景。但是，如果单击 Begin 按钮，控制台中会弹出一条警告：“无法加载关卡 'Scene-EntryWay' (-1)，因为它尚未添加到生成设置中。” 我们之前对生成（Build）的讨论不多，之后会深入讨论，但在这里先介绍一些相关内容是很重要的。

## 生成设置（Build Settings）

所谓生成（Build），实际上就是 Unity 的输出产物。玩家玩的就是 Unity 生成的这些构建版本。Unity 的优势之一在于可以一次创作，然后输出到多个平台的构建版本。Incursion 对于移动设备来说无疑过于沉重，不过只要稍微削减多边形数量并取得相应的授权，它最终也可以发布到 Android 或 iOS 上。

在 Build Settings（生成设置）中，可以定义目标平台，并指定要包含的关卡。要访问 Build Settings，请前往 文件 > Build Settings（生成设置）（图 12.6）。

![](img/0285f88bc840f313779e011725b623a5_374_0.png)

图 12.6 生成设置（Build Settings）。

Build Settings 窗口的顶部（Scenes in Build，即“生成中的场景”）是要将包含在构建中的场景拖放进去的区域。图 12.6 展示的是为 Incursion 填充此区域后的样子。其下方是定义 Platform（平台）以及该平台详细信息（Windows 与 Mac）的位置。底部还包含用于调整 Player Settings（播放器设置）的选项（此处的 Player 是指承载游戏的容器，而不是玩游戏的人）。还有 Build（生成）和 Build and Run（生成并运行）按钮。这些按钮会实际输出当前状态下的游戏。

但暂时不要输出；现在只需将 Scene-Opening 和 Scene-EntryWay 添加到 Scenes in Build 中，然后关闭窗口。

- **步骤 43：** 通过将场景文件从 Project（项目）面板拖放到 Build Settings 窗口的 Scenes in Build 区域，来填充要包含在游戏中的场景。
- **步骤 44：** 运行游戏。这一次，当按下 Begin 按钮时，你会立刻被传送到之前教程中构建的 EntryWay 场景。

## 结论

这就是你的第一个脚本。好吧，也许是第二个，但希望这是第一个让你理解这些内容是如何构建以及为什么这样构建的脚本。

实际上，这个脚本编写入门涵盖了非常多的内容。现在你已经知道如何编写代码块、什么是函数、函数的几种类型，以及如何声明变量，如何在编辑器中填充这些变量或通过脚本填充它们。

但是，仍然有很多事情要做，也有很多东西要学。在下一章中，我们将开始研究更高级的功能和配置，让玩家能够用手电筒进入漆黑的基地，找到电源开关，然后打开所有电源。

## 作业与挑战

- **挑战 1：** 从 Opening 场景切换到 EntryWay 场景虽然可行，但显得有些突兀——所有画面冻结，然后突然跳转到下一个场景。请使用 OpenSceneButtonsScript 添加一个大的加载面板（Loading Plate），当按下 Begin 按钮时显示出来，这样玩家就不会以为游戏卡死了。

**提示：**

- 1. 记住要创建一个新的 GUITexture 对象。
- 2. 在脚本中，既要在变量中考虑这个新的 GUITexture，也要在填充变量时考虑它。
- 3. 确保在跳转到新关卡的命令之前显示这个新的 GUITexture。
- 4. 注意，除了 Transform X 和 Y 之外，还有 Transform Z。它决定了哪个 GUITexture（如果有多个）更靠近摄像机，从而绘制在最上层。

![](img/0285f88bc840f313779e011725b623a5_376_0.png)

## Unity 触发器

到目前为止，我们已经研究了如何让命令在用户驱动的事件（例如鼠标悬停、鼠标按下等）上触发。我们也看了如何在游戏开始时触发命令。在本章中，我们将开始研究如何根据玩家在关卡中的位置来触发命令。我们将通过**触发器（trigger）**来实现这一点。

具体来说，我们将研究如何使用这种机制通过 GUIText 提供屏幕提示。此外，这也将提供一种从 EntryWay 关卡移动到 Hallway 关卡的新方式。不过，触发器可以用来触发任何事件。可以触发诱杀陷阱、改变光照、创建或销毁对象——所有这些都可以通过触发器完成。

First Person Controller（第一人称控制器）周围有一个碰撞器，它实际上是 Character Controller 脚本的一部分。请记住，碰撞器是 Unity 用来追踪对象何时相互碰撞或相互穿透的方式（称为**碰撞检测**）。当我们从 Maya 导入 EntryWay 关卡时，我们在 FBX 导入设置中启用了 Generate Colliders（生成碰撞器）选项。这确保了我们的角色不会从地板掉下去——关卡的碰撞器和 First Person Controller 上的碰撞器共同防止了这种情况发生。
