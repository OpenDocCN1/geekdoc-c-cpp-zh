
## 一、建设项目基本情况

| 项目 | 内容 |
| --- | --- |
| 项目名称 | XX市XX区XX地块商业综合体建设项目 |
| 建设单位 | XX房地产开发有限公司 |
| 项目性质 | 新建 |
| 建设地点 | XX市XX区XX路与XX大道交汇处东北角 |

## 二、项目概述

本项目拟建设集商业、办公、餐饮、娱乐于一体的综合性商业综合体，总用地面积约2.5万平方米，总建筑面积约12.8万平方米，其中地上建筑面积约9.6万平方米，地下建筑面积约3.2万平方米。项目建成后将成为该区域新的商业中心，有效提升周边居民的生活便利性。

## 三、项目主要建设内容

- 商业购物中心：约5.2万平方米，含大型超市、精品零售、餐饮美食等业态；
- 写字楼：约2.8万平方米，定位为中高档商务办公空间；
- 公寓：约1.6万平方米，提供精品酒店式公寓；
- 地下车库：约3.2万平方米，设置机动车停车位约800个。

- **步骤 23：** 将此脚本应用到 Trigger-LockedDoor 触发器上。
- **步骤 24：** 在 Inspector 中填充该脚本。将 Hallway_Door_Bulkhead_Group 1 用作 Door。将 Hallway_Door_BulkheadWheel 1 用作 Bulkhead Handle，并将 Sound-DoorLocked 用作 Door Open Sound。
- **步骤 25：** 测试并运行。首先，不要拾取钥匙，直接走向触发器（图 16.9），文本应提供一些指引。然后回去拿钥匙（钥匙应高亮；图 16.10），点击后钥匙应消失（同时应在右上角显示钥匙图标）。最后，回到上锁的门前，它应该会在你强大的游戏实力面前屈服（图 16.11）。
- **步骤 26：** 将 Trigger-LockedDoor 设为 Hallway_BakedGroup 的子对象。

### 为什么？

我们不希望角色在打开灯之前就被困在寻找钥匙这件事上。首先，钥匙盒还不存在。通过将 Trigger-LockedDoor 设为 Hallway_BakedGroup 的子对象，我们

![](img/0285f88bc840f313779e011725b623a5_492_0.png)

**图 16.9** 走向上锁的门，并提供如何通过该门的提示。

![](img/0285f88bc840f313779e011725b623a5_492_1.png)

**图 16.10** 对钥匙进行射线检测，点击后钥匙消失。

![](img/0285f88bc840f313779e011725b623a5_496_0.png)

**图 17.2** 已放置的关闭 GUI 元素

### 为什么？

实际上，这两个按钮的附加功能可以追加到 OpenSceneButtonScript 中；一般来说，在我自己的项目里，为了减少脚本数量，我会这样做（并把脚本重命名为 GUIButtonsScript）。然而，以本书的形式来看，这又会变成一个非常长的脚本，有时很难看清额外脚本是如何工作的。因此，为了清晰起见，我们将新建一个脚本。

- **步骤 6：** 删除变量和 Awake 函数（这里都不需要），并调整 OnMouseDown 函数，以检查被点击按钮的名称。如果点击的是 Button-Exit，则退出游戏。如果选择的是 Button-PlayAgain，则加载关卡场景 Scene-Opening。最后，确保关卡开始时鼠标是自由的（我们会在玩过其他可能锁定光标的关卡后进入 CloseScenes）：

```csharp
function Start() {
    Screen.lockCursor = false;
}

function OnMouseEnter () {
    guiTexture.color = Color (1,1,1);
}

function OnMouseExit () {
    guiTexture.color = Color (.2,.2,.2);
}

function OnMouseDown() {
    if (name == "Button-Exit"){
        Application.Quit();
    }
    if (name == "Button-PlayAgain"){
        Application.LoadLevel("Scene-Opening");
    }
}
```

- **步骤 7：** 保存并返回 Unity。修复语法问题。
- **步骤 8：** 在 Hierarchy 中将 CloseScreenButtonScript 应用到 Button-Exit 和 Button-PlayAgain。
- **步骤 9：** 将 Button-Exit 和 Button-PlayAgain 的颜色值改为 RGB=50。记得这样做：在 Hierarchy 中选择每个按钮；然后在 GUITexture 组件中，点击颜色色块来更改数值。
- **步骤 10：** 运行并测试。点击 Exit 按钮时不会发生任何事情（不过在构建游戏后它会起作用）。点击 Play Again 按钮时，我们应该回到 Scene-Opening。
- **步骤 11：** 保存 Scene-Closing。

### 终局触发器

- **步骤 12：** 打开 Scene-Hallway。
- **步骤 13：** 创建一个触发器，放在设备所在壁橱的正前方（楼梯底部（图 17.3））。将其命名为 Trigger-Endgame。

![](img/0285f88bc840f313779e011725b623a5_497_0.png)

> **提示与技巧**
>
> 请注意，图 17.3 显示了在隐藏 Unbaked、显示 Baked 时触发器的位置（不过也可以通过禁用 Scene 视图中的光照来放置它）。

- **步骤 14：** 新建一个 JavaScript，并将其命名为 `EndgameTriggerScript`。打开它。
- **步骤 15：** 这个脚本会很简单。当我们进入该触发器时，加载关卡 Scene-Closing：

```
function OnTriggerEnter (other:Collider) {
    Application.LoadLevel("Scene-Closing");
}
```

### 为什么？

这里非常直接。如果玩家到达终点并撞到碰撞体，就会触发 Scene-Closing 场景。

- **步骤 16：** 保存并返回 Unity。修复任何语法问题。
- **步骤 17：** 停用 Hallway_UnBaked 并启用 Hallway_Baked。
- **步骤 18：** 将 FPC_AegisChung 移动到地图末端附近（这样等会儿测试时，玩家就不必跑完整个关卡）。
- **步骤 19：** 将 Scene-Closing 添加到 Build Settings。记住，要做到这一点，请选择 File > Build Settings，然后将 Scene-Closing 从 Project 面板拖到 Build Settings 窗口的 Scenes in Build 区域（图 17.4）。
- **步骤 20：** 将 EndgameTriggerScript 应用到 Trigger-Endgame 触发器。测试并运行。
- **步骤 21：** 确认一切正常后，将 FPC_AegisChung 放回关卡开头。
- **步骤 22：** 将 Trigger_Endgame 设为 Hallway_BakedGroup 的子对象。

### 为什么？

并不是说在游戏一片漆黑时（可见的是 Unbaked 版本），角色真的能到达关卡终点，但以防万一，让触发器在 Baked 版本开启之前保持不激活，有助于确保游戏按计划进行。

- **步骤 23：** 停用 Hallway_BakedGroup 并启用 Hallway_UnBaked。
- **步骤 24：** 保存 Scene-Hallway。

## 结论

太好了！他能赢了。获胜可以很有趣——但只有在你也可能失败时才会如此。让我们创建一个生命值系统，好让玩家能够失败。

**图 17.4** 确保 Scene-Closing 是 Unity 知道要播放的场景之一。

![](img/0285f88bc840f313779e011725b623a5_499_0.png)

## 教程 17.2：生命值系统

与 Unity 中通常情况一样，处理生命值系统有几种方法。我们将采用最常见的方法，创建一个附加到 FPC_AegisChung 的生命值引擎。这个生命值引擎实际上只是一个计数器。它一开始会知道角色的生命值是 100（或任意值）。然后，当角色遇到某些情况时（被子弹击中、被落石砸中、被蒸汽喷到、摔得太远——在这里发挥你扭曲的想象力），会向这个生命值引擎发送消息，从当前生命值中减去相应数值。当生命值等于 0 时，触发一个死亡函数，提醒玩家他已经挂了并输掉了游戏。

所以，首先我们需要创建生命值脚本。

- **步骤 1：** 新建一个 JavaScript。将其命名为 HealthEngineScript 并打开。
- **步骤 2：** 定义几个变量。一个（整数）将保存生命值的实际数值。第二个（GameObject）将保存显示生命值等级的 GUIText GameObject。

```
var health : int;
private var healthLevel : GameObject;
```

- **步骤 3：** 现在，我们希望告诉 Unity，在游戏开始时将生命值设为 100，然后显示该数值：

```
var health : int;
private var healthLevel : GameObject;

function Awake () {
    healthLevel = GameObject.Find("HealthLevel");
}

function Start(){
    health = 100;
    healthLevel.guiText.text = health.ToString();
}
```

### 为什么？

Start 函数的第一条命令只是定义生命值的数值。之后我们会希望在关卡之间传递这个值，这样如果 Aegis 在 EntryWay 中遇到麻烦，那么他在 Hallway 中时减少后的生命值仍然相同。但就目前而言，我们只需让它在游戏开始时设为 100。

第二条命令定义了 GameObject healthLevel 的 guiText 组件文本中应显示的内容。注意，这里使用了方便的 ToString 函数。这是 Unity 的内置函数，用于将（在本例中）整数（guiText 无法显示）转换为字符串（guiText 可以显示）。所以它只是取 health 的值，将其转换为字符串（文本集合），然后显示出来。看起来有点费劲，但这是许多脚本语言的典型做法。

现在我们还没有创建 guiText GameObject。我们稍后会处理。

- **步骤 4：** 保存并返回 Unity。修复语法。

### 创建生命值显示

- **步骤 5：** 打开 Scene-EntryWay。
- **步骤 6：** 新建一个 GUITexture（GameObject > Create Other > GUI Texture）。将其命名为 HealthLabel，并用 2D Assets 文件夹中的 HealthBG 纹理填充其 Texture。使用图 17.5 所示的设置进行定位。确保 Transform X = 0.5、Y = 1。然后确保 Pixel Inset 值设置为 X = -32、Y = -64、Width = 64、Height=64。

### 为什么？

该图像为 64x64（因此宽度和高度设置如此）。通过将 Transform 值设为 0.5、1，我们把图像的左下角放在屏幕顶部中央。将图像偏移 X = -32 会把图像中间滑到屏幕中间，然后将图像偏移 Y = -64，会把它向下滑，使图像顶部位于屏幕顶部。

