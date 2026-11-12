

### 为什么？

通过将资源从 Project 面板（我们的资源库）拖到 Hierarchy 面板，第一人称控制器预制件已被放入场景中。或者，也可以将 First Person Controller 预制件拖入 Scene 窗口来完成。

### 为什么？

那么，既然现在还没有什么事可做，为什么要放置这个第一人称控制器呢？这是一个很好的问题，也是缩放过程中的一个重要部分。First Person Controller 预制件包含一些重要信息，例如尺寸。如果在 Hierarchy 面板中选中 First Person Controller 实例，Inspector 面板将显示该实例的属性。请注意，角色控制器的高度为 2（米）。

这一点很重要，因为现在我们有了一个参考对象，可以帮助我们理解之后放置的对象应该有多大。随着其他资源被放入 Unity 场景，它们将以 First Person Controller 为基准进行缩放。虽然这看起来有点反直觉——似乎将控制器缩放到适合场景会更容易——但这样做的目的是确保对象的比例符合世界尺度。这对于物理等功能尤其关键。如果场景中的物体非常大或非常小，物理模拟看起来总会不正常。

- **步骤 4：** 将 First Person Controller 实例移动到 0,1,0。在 Hierarchy 面板中选择 First Person Controller 实例。然后在 Inspector 中，找到 Transform 组件并将 Position 改为 X=0, Y=1, Z=0。

### 为什么？

将 First Person Controller 放置在 0,1,0，我们就是把它放在世界中心，并使控制器的底部贴在地面上（它的高度为 2 个单位，中心位于几何中心，因此 Y=1 会使其底部位于“地面”上）。

- **步骤 5：** 在 Scene 窗口中将 First Person Controller 居中。仍然在 Hierarchy 面板中选中 First Person Controller，在键盘上按 F 键。这将使选中的元素（First Person Controller）在 Scene 窗口中居中显示。

- **步骤 6：** 将 EntryWay 预制件放入场景中。这次，将 EntryWay 预制件从 Project 面板拖到 Scene 窗口中。

- **步骤 7：** 将 EntryWay 实例放置在世界空间的 0,0,0 处。在 Hierarchy 面板中，选中 EntryWay 实例，并在 Inspector 中将 Position 的 X、Y、Z 都设置为 0（图 5.7）。

**图 5.7** 导入并放置好的 First Person Controller 和 EntryWay（你的结果可能稍有不同）。看起来还不是完全正确，对吧？

![](img/0285f88bc840f313779e011725b623a5_125_0.png)

### 为什么？

当场景中内容很少时，将预制件移入场景可能是一种奇怪的体验。很难理解一个物体在世界空间中的位置，甚至很难理解该对象在该空间中有多大。通过将 First Person Controller 和 EntryWay 都移动到世界中心，我们可以清楚地看到导入元素的大小。

- **步骤 8：** 缩放 EntryWay 使其在场景中合适地匹配。为此，需要调整 EntryWay 预制件的导入设置。在 Project 面板中，单击一次 EntryWay。这将在 Inspector 中打开 EntryWay 的属性。具体来说，在 FBXImporter 部分，Inspector 将显示 Unity 在将 EntryWay.fbx 导入 Unity 项目时使用的设置。将 Scale Factor 改为 .5，然后按下 Apply 按钮。之后需要时再调整 Scale Factor（图 5.8）。

**图 5.8** 缩放后的 EntryWay。在本例中，设置为 0.5 是最佳选择。在你的场景中可能会有所不同。

![](img/0285f88bc840f313779e011725b623a5_125_1.png)

### 为什么？

为什么不在 Scene 视图中直接缩放对象呢？在很多情况下，这完全是可以接受的，而且在这个例子中实际上也是可行的，因为 EntryWay 预制件可能只会被使用一次。然而，当一个预制件会被多次使用时，最好调整 Scale Factor。

- **步骤 10：** 为 EntryWay 添加碰撞体。在 Project 面板中选择 EntryWay 预制件。在 Inspector 中，在 FBXImporter 下勾选 Generate Colliders 选项，然后点击 Apply。

### 提示与技巧

勾选 Generate Colliders 是一种快速且粗略的方法，以确保网格是“实心的”，也就是玩家无法穿过它。然而，从优化游戏玩法的角度来看，这并不是最高效的方法。勾选此选项后，场景中的每一个网格都会有一个 Mesh Collider，包括玩家根本无法到达的场景部分。例如，如果游戏玩法中永远不会需要爬到头顶的横梁上，那么横梁上的碰撞体真的有必要吗？

对于像这样的 PC 向游戏，使用 Mesh Collider 是可以接受的，因为在这个游戏阶段不会发生太多事情。不过，如果这是为 iOS 或 Android 开发的，甚至是要发布在配置可能不太高的机器上，那么更高效的做法是关闭 Generate Colliders 选项，而只在玩家实际会接触到的区域手动创建一些 Box Collider。

- **步骤 11：** 运行游戏。按下工具栏中的 Play 按钮。使用标准的 WASD 或方向键移动，并用鼠标环顾四周（图 5.9）。再次按下 Play 按钮即可停止运行游戏。

**图 5.9** 在场景中移动。

![](img/0285f88bc840f313779e011725b623a5_127_0.png)

### 提示与技巧

确保 First Person Controller 没有一半陷入地板中，也不要悬在半空中。在 Hierarchy 面板中选择 First Person Controller，然后在 Scene 窗口中确保它刚好略高于地面，这样在运行游戏时，控制器才能真正与地面接触。

![](img/0285f88bc840f313779e011725b623a5_130_0.png)

**图 5.12** 所选网格的 Inspector 界面。

场景中仍然能够阻挡玩家穿过，但无法被看到。

Mesh Collider 是之前步骤中在 FBXImporter 设置里勾选 Generate Colliders 时添加的组件。正是它阻止了玩家穿过墙壁。

最后，最后一个部分是这个 GameObject 上应用的 Material（材质）。注意，这里实际上有几个部分。在材质名称的正下方有一个下拉菜单，可以用来更改 Shader（着色器）。关于这一点，后面还会详细讨论。但目前只需要注意默认的着色器是“Diffuse”。漫反射着色器使用颜色纹理文件来定义材质的颜色。它没有高光或凹凸效果。这个稍后会更改，但它是开始研究材质的一个不错的方式。

在该部分下面是 Main Color（主颜色）部分，其中显示了用于定义材质颜色的纹理文件。我们感兴趣的正是这个纹理文件。

- **步骤 16：** 选择颜色纹理文件。在 Inspector 的 Main Color 部分中，点击 Main Color 纹理样本（图 5.13）。

**图 5.13** 选择材质中使用的纹理文件。注意，点击样本后，它所代表的文件会在 Project 面板中高亮显示。

![](img/0285f88bc840f313779e011725b623a5_131_0.png)

## 警告与陷阱

说实话，2048x2048 是一个很大的纹理——事实上太大了。2048x2048 的纹理并不是 1024x1024 的两倍大，而是四倍大。因此，选择使用这么大的纹理并不是一个可以轻率做出的决定。实际上，使用多套 UV 是一种技术，可以让较小的可平铺纹理叠加在更大、更粗糙的纹理之上。使用多 UV 实际上可以创造出比我们目前正在构建的游戏高效得多的游戏。然而，这是一个相当晦涩的过程，并且超出了本书的范围。因此，我们做出的折衷是使用较大的、不可平铺但又易于理解其如何应用于表面的纹理。不过，为了弥补这种折衷，请谨慎选择哪些纹理**必须**使用较大的尺寸。如果纹理在较低分辨率下看起来已经可以接受，那就保持原样。

### 为什么？

点击这个样本时，会临时发生几件事。Project 面板会展开，该样本所代表的文件会被临时高亮显示（如图 5.13 所示）。然后就可以在 Project 面板中选中该实际文件。

- **步骤 17：** 在 Project 面板中，选择高亮显示的文件。如果使用你自己的文件，请选择内墙（或实际上任何物体）。如果使用网站上提供的文件（http://www.Creating3dGames.com），这将是 EntryWay_WallsInner_Color。

### 为什么？

Inspector 会立即显示 EntryWay_WallsInner_Color 文件的属性。这一点很重要，因为现在我们可以看到该资源导入时的设置是什么，更重要的是，这些设置是可以更改的。

- **步骤 18：** 在 Inspector 中，将 Max Size 改为 2048，然后按下 Apply。

### 为什么？

Inspector 会显示纹理的预览（图 5.14）。注意在最底部，Unity 会指示纹理为 1024x1024 RGB Compressed DXT1 0.7 MB。对我们重要的是 1024x1024 这部分。这意味着 Unity 将该纹理视为 1024x1024。这是因为 Max Size 设置（可在 Inspector 稍上方看到）设置为 1024。使用该设置，无论图像有多大，Unity 都会将其缩小到 1024x1024。通过将 Max Size 改为 2048，Unity 将检查文件中是否有 2048x2048 的信息量，如果有，就会以这个更高分辨率重新导入。Scene 视图中的画质将立即发生变化。

