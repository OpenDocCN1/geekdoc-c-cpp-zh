

# 开始使用 HTC Vive

如果你还没有 HTC Vive 头戴设备的自豪所有者，你可以在他们的官方网站（https://htcvive.com）上购买，或者（取决于你所在的地区）在附近的商店购买。确保你的 PC 符合最低要求。一旦拿到设备，请下载并安装软件并设置硬件。如果设备有可更新的固件，请进行更新。

在 Unity 中打开 **HTC Vive** 项目并进入 **Game** 场景：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_586_0.png)

如果你尝试，你会发现无法添加任何塔，因为它们没有显示在屏幕上。这是因为 Screen Space Canvas（屏幕空间画布）被替换成了 **World Space Canvas**（世界空间画布）。这意味着元素可以在世界中自由放置、缩放和旋转，而不是锁定在屏幕上。

再查看相机周围的浮动 UI 元素。它们是沿着网格放置的。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_586_1.png)

为了在 Unity 中使用 **Vive**，你需要从 Asset Store 下载并导入最新版本的 **SteamVR** 插件。点击 **Window ▷ Asset Store** 打开资源商店。在顶部的搜索框中输入 **SteamVR** 并按回车。向下滚动结果找到 **SteamVR Plugin**。它应该是第一个条。

Unity Games by Tutorials
Chapter 20: Virtual Reality

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_587_0.png)

点击 SteamVR 图标打开商店页面并点击 **Download** 按钮。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_587_1.png)

插件下载完成后将打开 **Asset Import** 对话框。点击右下角的 **Import** 按钮将其添加到项目。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_587_2.png)

如果弹出一个窗口要求你对 **SteamVR** 进行建议更改，请全部接受，除非它要求颜色为 **Linear** 而不是 **Gamma**。如果你这样做，项目将会变暗，因为所有光照都是为 gamma 配置的。现在你可以关闭 **Asset Store** 了；此项目不再需要它。Unity Games by Tutorials
Chapter 20: Virtual Reality

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_588_0.png)

该文件夹包含了各种脚本、制体和示例来帮助你。在下部分你将使用其中一些，现在是时候在 Unity 中进行实际设置了！

# 为 HTC Vive 配置 Unity

在 Hierarchy（层级）中，禁用 Main Camera，并将 SteamVR > Prefabs 文件夹中的 **CameraRig** 拖到场景中：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_588_1.png)

将其重命名为 ViveRig 并位置设置为 (0, 0, 0)。现在在 Scene（场景）视图中查看它：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_589_0.png)

蓝色边界代表玩家的房间。现在由于使用了真实世界单位，它与世界相比非常小。准备好你的 Vive 及其控制器并运行场景。戴上 HMD 走动一下。敌人非常巨大！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_589_1.png)

为了解决这个问题，将 ViveRig 的比例更改为 (10, 10, 10)，让房间变大：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_589_2.png)

尝试再次开启 Vive 运行场景，你会发现不同：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_590_0.png)

你现在是一个在地图上行走的巨人！走动一下并蹲下抬头看敌人。还要测试控制器是否工作正常。如果控制器不移动，通过 SteamVR Status 应用重启头戴设备。如果这不能解决问题，通过删除 SteamVR 文件夹并从资源商店导入新包来更新到最新版本的 SteamVR。下一步是通过放置塔来实现与世界的交互。

# 与世界交互

在 VR 中处理输入有多种方法。但在项目中，你将使用其中一个控制器指向世界，并使用 UI 与之交互。SteamVR 插件并没有内置这样一个系统，因此你必须手动添加它。

首先在 Hierarchy 中展开 ViveRig，以便看到它的子物体。选择 Controller (right)。右键点击它并选择 Camera 创建一个新的相机作为子物体。将其命名为 ControllerCamera。这个相机不是为了实际观察。它将纯用于向场景发射射线，以便你可以看到并交互。将相机的 Clear Flags 改为 Solid Color，将 Depth 设置为 -5并将 Target Eye 设置为 None (Main Display)。接下来，移除 Flare Layer、GUI Layer 和 Audio Listener 组件。此相机不需要渲染任何内容。它不需要听声音或音乐，所以这些组件是不必要的。最后，添加一个 Physics Raycaster 组件以便它可以向 3D 碰撞体发射射线。在 Inspector 面板中点击 Add Component 并搜索名称。

在 Prefabs 文件夹中创建一个名为 VR 的文件夹，将 ViveRig 拖入其中成为制体。下一步需要添加的是知道控制器指向何处的方法。你将通过 3D 准星和激光的来实现方便玩家：

![](img/fd5c2ca20ea33da76d2b6197cc57f6c_591_0.png)

首先是 Hierarchy 中的准星。创建一个新的 Sphere (3D Object ▸ Sphere) 并命名为 Reticle。重置其 Transform，将其比例设置为 (0.1, 0.1, 0.1) 并移除 Sphere Collider 组件。最后，将 Reticle 拖到 Prefabs ▸ VR 文件夹中成为制体。

![](img/fd5c2ca20ea33da76d2b6197cc57f6c_591_1.png)

对于激光，创建一个新的 Cube (3D Object ▸ Cube) 并命名为 Laser。重置其 Transform 并将其比例设置为 (0.1, 0.1, 1)。移除其 Box Collider。也将 Laser 拖到 VR 制体文件夹中。

![](img/fd5c2ca20ea33da76d2b6197cc57f6c_592_0.png)

你可能在疑惑为什么“激光”只是一个长

配合不发光材质，无论从哪个角度观察，立方体的宽度都是保持一致的。

