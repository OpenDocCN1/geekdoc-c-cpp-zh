

## 教程 16.2：钥匙

希望这会是一个有趣的教程。在教程过程中，我们将运用之前教程中涵盖的技术。通过以新的方式组合这些技能，我们将在游戏中实现一个新机制。

过程如下：首先，我们需要创建一个触发器，当玩家进入时检查玩家是否拥有钥匙。如果玩家确实拥有钥匙，门就会打开；如果没有，则会弹出一段文字提示，提醒玩家需要钥匙。我们将创建一个 PickUpKey 函数，当玩家的射线投射到钥匙上并点击时触发。当玩家点击钥匙时，我们让钥匙从场景中消失，但创建一个 GUI 元素来指示钥匙已在玩家身上。这会很有趣！

- **步骤 1：** 创建一个新的 GUITexture 来显示钥匙。新建一个 GUITexture（`GameObject>Create Other>GUITexture`）并将其命名为 `KeyIcon`。使用 2D Assets 文件夹中的 `Icon-Key` 纹理来定义其纹理。

- **步骤 2：** 将钥匙放置在屏幕右上角。在层级（Hierarchy）中选择 `KeyIcon`，并在检查器（Inspector）中将 Transform 的 X 和 Y 值改为 1。将像素内边距（Pixel inset）值改为 X = -70, Y = -70, Width = 64, Height = 64（图 16.6）。

![](img/0285f88bc840f313779e011725b623a5_485_0.png)

### 为什么？

图像是 64x64。当 GUITexture 位于 1,1,0 时，图像的左下角位于屏幕的左上角，这意味着图像超出了屏幕。通过在 X 和 Y 两个方向上将像素偏移 -70，我们将图像移回屏幕，并在上方和右侧留下 6 像素的缓冲。

- **步骤 3：** 既然你已经看到了它可见时的样子，现在将它移出屏幕。在层级（Hierarchy）中选择 `KeyIcon`，并在检查器（Inspector）中，将 Transform X = 1，Y = 1 更改。

> **为什么？**
>
> 我们只是将它滑出屏幕，这样当钥匙真正被获得时，它就能滑回来。

- **步骤 4：** 将 KeyIcon 设为 GUIElements 的子物体。继续操作，打破预制件（prefab）。然后，一旦 KeyIcon 成为 GUIElements 的子物体，务必按下 Prefab Apply 按钮。

### 访问状态引擎

- **步骤 5：** 打开 AC_ToolFunctionalityScript。

**为什么？**

我们的状态引擎存在于 AC_ToolFunctionalityScript 中。请记住，这是我们在跟踪 flashlightActive、pistolActive、empActive 和 empGhostActive 的地方。我们需要添加一个新的状态（一个新的布尔值）：keyAcquired。

- **步骤 6：** 让状态引擎感知一个新的潜在状态：keyAcquired。在变量声明中添加以下这组代码：

```javascript
private var flashlightActive : boolean;
private var pistolActive : boolean;
private var empActive : boolean;
private var empGhostActive : boolean;
private var keyAcquired : boolean;
```

**为什么？**

从技术上讲，我们可以将这个布尔值存储在其他地方，但当需要调试时，将所有布尔值放在一个地方确实很有帮助。如果所有状态都存储在一个地方，当状态没有按预期工作时，我们就能确切知道该查看哪个位置。

### 基于射线投射机制

回想一下，之前我们在 AC_ToolFunctionalityScript 中设置了一个射线投射机制。在 Update 函数部分查找，会看到以下代码块存在：

```javascript
if (hitObj.name == "Hallway_Key"){
    AddHighlight(hitObj);
}
```

这段代码位于射线投射机制内，意思是：“如果我们射线投射到的对象命名为 'Hallway_Key'，就触发 AddHighlight 函数。”这实际上只是后面真正要发生的事情的一个占位符。

实际上，如果被射线投射到的对象命名为 Hallway_Key，我们需要高亮它，然后如果用户点击鼠标，我们需要触发一个名为 PickUpKey 的新函数。

- **步骤 7：** 重新编写此部分，使其如下所示：

```javascript
if (hitObj.name == "Hallway_Key") {
    AddHighlight(hitObj);
    if (Input.GetMouseButtonDown(0)) {
        PickUpKey();
    }
}
```

> **为什么？**
>
> 所以这里我们说的是：“如果射线投射到的对象命名为 Hallway_Key，则高亮它，然后（如果被投射的对象仍然是 Hallway_Key）如果用户点击鼠标按钮，就触发函数 PickUpKey。”

### 充实 PickUpKey

现在我们可以处理实际拾取钥匙时的所有动作了。

- **步骤 8：** 向下滚动并创建一个名为 PickUpKey 的新函数。按如下方式充实该函数：

```javascript
function PickUpKey(){
    var keyIcon : GameObject = GameObject.Find("KeyIcon");
    iTween.MoveTo (keyIcon, Vector3 (1.1,0), 1);
    var keyGeometry : GameObject = GameObject.Find("Hallway_Key");
    keyGeometry.active = false;
    keyAcquired = true;
}
```

> **为什么？**
>
> 这里做了一些有趣的事情。首先，注意声明了两个局部变量（keyIcon 和 keyGeometry）。我们只会使用它们一次（角色只会拾取一次钥匙），因此与其让本已拥挤的变量声明块变得更加混乱，我们将在需要时声明这些新变量。
>
> 在声明每个变量之后，甚至在同一行中，我们告诉 Unity 通过特定名称查找对象来填充它们。通常，在函数中使用 GameObject.Find 可能很危险，

![](img/0285f88bc840f313779e011725b623a5_489_0.png)

图 16.7 将被锁住的门。

- 步骤 14：旋转组，使门处于关闭状态。Rotation XYZ 应均为 0。

- 步骤 15：确保组（及其子物体）设置为非静态（non-Static）。在检查器（Inspector）中通过取消勾选 Static 选项来完成。

**为什么？**

该组最初可能被设置为 Static，因为需要将其包含在烘焙中。然而，如果它仍被标记为 Static，我们就无法使用 iTween（或其他任何脚本驱动的方法）对其设置动画。

- 步骤 16：创建一个名为 Trigger-LockedDoor 的触发器。作为复习，请记住可以通过创建 Cube（GameObject>Create Other Cube）来完成。在检查器（Inspector）中关闭其 Mesh Renderer。在 Box Collider 中启用 Is Trigger 选项，并调整大小和位置，如图 16.8 所示。

![](img/0285f88bc840f313779e011725b623a5_489_1.png)

图 16.8 Trigger-LockedDoor。

- 步骤 17：创建一个包含门开时吱呀声的 AudioSource。确保关闭 Play on Awake。将 AudioSource 放置在门旁，并将其命名为 Sound-DoorLocked。

- **步骤 18：** 创建一个新的 JavaScript。将其命名为 HallwayDoorsLockedTriggerScript。在脚本编辑器中打开该脚本。

### 为什么？

我能听到你们这些硬核脚本作者在远处尖叫：“直接使用 HallwayDoorsTriggerScript，然后修改它使其能够检查布尔状态就可以了。”你完全正确。一个更高效的方法是创建一个几乎适用于所有情况的门开启脚本；然而，我们将再构建一个脚本来回顾触发器的工作原理，并让书中的脚本易于阅读。

- **步骤 19：** 为门、舱壁把手（bulkheadHandle）、开门声音（doorOpenSound）、主摄像机（mainCamera）和 GUI 文本提示（guiTextHints）定义变量：

```javascript
var door : GameObject;
var bulkheadHandle : GameObject;
var doorOpenSound : GameObject;
private var mainCamera : GameObject;
private var guiTextHints : GameObject;
```

### 为什么？

door 是要打开的对象。bulkheadHandle 是转动的轮子。doorOpenSound 是当这扇大门打开时播放的声音。接下来两个私有变量使我们能够定位状态引擎所在的位置（附加在主摄像机上），并在玩家尚未获得钥匙时驱动屏幕提示。

- **步骤 20：** 在 Start 中，让脚本填充 mainCamera 和 guiTextHints：

```javascript
function Start() {
    mainCamera = GameObject.Find("Main Camera");
    guiTextHints = GameObject.Find("GUITextHints");
}
```

### 为什么？

那么为什么要把 mainCamera 和 guiTextHints 设为私有变量并在脚本中填充，而不对其他变量这样做呢？好问题；答案是，这将使该脚本适用于其他上锁门的情境。在门被锁住（并且我们希望能够打开它）的几乎所有情况下，都会访问状态引擎，并显示屏幕提示。由于这两个对象不会改变，硬编码它们可以省去在 Unity 中填充的步骤。但如果此脚本在其他地方使用，门本身确实可能会改变，因此将其（连同门把手和门播放的声音）保留为公共变量，将使此脚本有更多用途。

