
从 `AnyState` 到 `ElevatorSummon` 创建一个转换，并从 `ElevatorSummon` 到 `ElevatorRise` 创建另一个转换。它看起来如下：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_235_0.png)

你还需要启动动画，所以在你之前输入的代码之后添加此行：

```
arenaAnimator.SetBool("OnElevator", true);
```

这将在玩家进入球体碰撞器时启动动画状态并生效，但请记住碰撞器是被禁用的。它应该在平台到达时处于激活状态，在此之前不是。保存并切换到 Unity。

在层级面板中选择 `BobbleArena`。在检器中，将 `SpaceMarine` 拖到 `player` 扩展槽中。展开 `BobbleArena` 并寻找一个名为 `Elevator_Platform` 的子游戏对象。将其拖到 `BobbleArena` 的 `Elevator` 属性上。

你已经到了最后一步，即调用你的代码了。坦率说，动画事件可以做到这一点。这酷酷吗？

在 `Start()` 中，添加以下内容：

```
arenaAnimator = GetComponent<Animator>();
sphereCollider = GetComponent<SphereCollider>();
```

到目前你应该已经完成了这一步；在这里，你正在获取组件的访问。

需要一个事件链来指定当陆士兵进入触发器后会发生什么。

你想让陆士兵乘坐电梯升到天花板。动画玩家是一种可行的方法，但更简单的方法是将陆士兵设为电梯的子物体。随着电梯的上升，陆士兵只能跟随。此外，摄像机会也会尝试跟随，所以你需要禁用它。

添加以下内容：

```
void OnTriggerEnter(Collider other)
{
    Camera.main.transform.parent.gameObject.
    GetComponent<CameraMovement>().enabled = false;
    player.transform.parent = elevator.transform;
}
```

第一行代码禁用了摄像机的移动。然后将玩家设置为平台的子物体。

你需要禁用玩家控制陆士兵的能力。在 `OnTriggerEnter()` 中添加以下内容：

```
player.GetComponent<PlayerController>().enabled = false;
```

这会阻止玩家转向、射击或对陆士兵进行任何操作。

现在，你需要添加一个音频提示来提醒玩家电梯已到达。添加以下内容：

```
SoundManager.Instance.PlayOneShot(SoundManager.elevatorArrived);
```

你还需要启动动画，所以在你之前输入的代码之后添加此行：

```
arenaAnimator.SetBool("OnElevator", true);
```

这将在玩家进入球体碰撞器时启动动画状态并生效，但请记住，碰撞器是被禁用的。它应该在平台到达时处于激活状态，在此之前不是。保存并切换到 Unity。

在层级面板（`Hierarchy`）中选择 `BobbleArena`。在检器（`Inspector`）中，将 `SpaceMarine` 拖到 `player` 扩展槽中。展开 `BobbleArena` 并寻找一个名为 `Elevator_Platform` 的子游戏对象。将其拖到 `BobbleArena` 的 `Elevator` 属性上。

你已经到了最后一步，即调用你的代码了。坦率说，动画事件（animation events）可以做到这一点。这酷酷吗？

## 动画事件

动画事件非常像关键帧。你确定动画中的某一点来运行代码，然后为其分配一个方法。这种方法可以精确控制代码运行的时机。

> 注意：记住，你可以动画化所有属性，包括你已经启用的碰撞器。

你在第 1 章“你好，Unity”中导入了召唤和上升的动画，现在只需要将它们与动画控制器（`Animator`）关联起来即可。

在层级面板选定 `BobbleArena` 的状态下，打开 `Animator` 窗口。你会看到你在第 6 章“动画”中设置的墙状态。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_234_0.png)

你需要一个新的状态来召唤电梯，它应该能够从所有状态访问，因为胜利可能在任何时候发生。你可以从每个状态创建一个转换，但 Unity 已经通过“`Any State`”（任意状态）为你解决了这个问题。

在 `Animator` 中，在任何地方点击右键并选择 `Create State` ▸ `Empty`。选择 `New State`，并在检器中将其命名为 `ElevatorSummon`。将 `Motion` 设置为 `ElevatorSummon` 动画剪，并将 `Speed` 设置为 `0.5`，将电梯减慢到正常速度的一半。目前这样，它运行得有点快，并在音频片段结束前停止。减慢速度可以保持电梯与音频同步。

创建另一个空状态，命名为 `ElevatorRise`，并将 `ElevatorRise` 动画剪分配给它。

`Animator` 应该如下：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_235_0.png)

从 `AnyState` 到 `ElevatorSummon` 创建一个转换，并从 `ElevatorSummon` 到 `ElevatorRise` 创建另一个转换。它看起来如下：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_235_0.png)

## 第二节：第一人称射击游戏

在本节中，你将学习如何创建最流行的游戏类型之一：第一人称射击游戏。

在此过程中，你将创建一个名为“机器人大乱斗”（`Robot Rampage`）的游戏，你将使用各种武器和强化道具消灭一波波敌机器人。准备好你的发射筒吧！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_239_0.png)

- 第9章，“制作第一人称射击游戏”
- 第10章，“添加敌人”
- 第11章，“Unity UI”

## 第 9 章：玩家与环境

作者：Anthony Uccello

在接下来的几个章节中，你将创建一个第一人称射击游戏，或者说常说的 FPS。一些著名的 FPS 游戏包括《光环》（`Halo`）、《使命召唤》（`Call of Duty`）和《毁灭》（`Doom`）。

你将创建的游戏名为 **Robot Rampage**；你将控制一个必须通过杀死机器人来生存的玩家。机器人将成波的形式出现，玩家必须收集生命、弹药和护甲道具，以便尽可能久地消耗机器人。玩家生存得越长、杀死的机器人越多，分数越高。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_240_0.png)

这个游戏分为三个部分。在第一部分，你将设置武器、添加声音以及处理所有射击的代码。

在下一章中，你将添加机器人反派、一些强化道具和大量的飞行射物。

在最后一个章节中，你将添加所有的用户界面元素，用于跟踪分数、弹药，甚至包含一个在游戏结束后重新启动的菜单。

Unity 游戏教程

第 9 章：玩家与环境

简而言之，你将拥有一个完整的 FPS 游戏。

## 入门

要开始之前，请在 Unity 中打开启动项目。在项目浏览器（`Project browser`）中，打开 `Scenes` 文件夹并双击 `Battle` 场景打开它。

信不信由，地图大部分工作已经为你设置好了。地图本身由一个地板组成，周围环绕着一系列墙。完成教程后，你可以通过调整墙的位置为游戏创建其他配置。

为了开始工作，你需要设置 `GameObject` 以便机器人可以避开它们。因此，在本书中你一直在使用层（layers），但 Unity 还有另一种名为标签（tags）的工具。标签仅仅是用于标识 `GameObject` 的文本。每个 `GameObject` 只能有一个标签，谢天的是，它们很容易使用。通过给每个 `GameObject` 分配标签，你将能够为机器人设置一些寻路规则，让他们绕过墙移动。

在层级面板（`Hierarchy`）中，点击 `InnerWalls` `GameObject`。在检查器（`Inspector`）中，点击 `Tag` 下拉并点击 `Add Tag`（添加标签）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_241_0.png)

Unity 游戏教程

在 `Tag` 窗口中点击加号按钮并在第一个槽位输入 `Wall`：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_242_0.png)

点击层级面板中 `InnerWalls` `GameObject` 旁边的箭头以展开它。选择所有的子 `GameObject`（命名为 `Wall` 和 `WallPost`）；执行此操作快速方法是选择第一个 `GameObject`，按住 `Shift` 并点击最后一项。

在选中所有子 `GameObject` 后，点击 `Tag` 下拉并选择你刚刚创建的标签：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_242_1.png)

所有的墙都已正确标记。现在你可以为机器人制作 `NavMesh`（导航网格）。

> 注意：忘记如何制作 `NavMesh` 或者跳过了这一章？如果是这样，请查看第5章“管理器与寻路”，其中详细介绍了 `NavMesh`。

通过 `Window > AI > Navigation` 打开导航窗口。确保选择了 `Wall` 和 `WallPost` `GameObject`，并勾选 `Static` 复选框。

Unity 游戏教程

第 9 章：玩家与环境

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_243_0.png)

点击 `Bake`（烘焙）按钮。地板应该变为蓝色，表示已为可行区域生成了 `NavMesh`。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_243_1.png)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_243_2.png)

`NavMesh` 创建完成后，是时候添加玩家了。

## 添加玩家

目前，当你想要相机和玩家在荒野中嬉戏时，相机是分离状态的。坦率地说，你不需要去当媒婆。

在层级面板中，创建一个空 `GameObject` 并命名为 `Player`。在选中 `Player` 时，在检查器中找到 `Character Controller`，并将 `Position` 设置为 `(0, 1, 0)`，`Rotation` 设置为 `(0, 0, 0)`。

`FirstPersonController` 脚本还有跑步速度和步行速度的值。将 `Walk Speed` 设置为 `10`，`Run Speed` 设置为 `20`。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_244_0.png)

## 添加相机

点击 `Camera` 并将其拖入 `Player` `GameObject` 以成为 `Player` 的子物体。相机现在会随玩家移动。

将 `Camera` `position` 设置为 `(0, 0.8, 0)`，`Rotation` 设置为 `(0, 0, 0)`。

点击 `Play`（播放）；使用 `WASD` 键移动，并在移动时使用鼠标观察。你还可以按住 `Shift` 键跑步。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_245_0.png)

# 创建武器

在 Unity 中，枪只是另一个 `GameObject`。主要的区别在于视角。将它放置在相机附近可以让你获得我们都喜爱的 FPS 视角。

选择 `Camera` `GameObject`，然后右键点击它并选择 `Create Empty`（创建空物体），在 `Camera` 下创建一个空 `GameObject`。将你的新 `GameObject` 命名为 `1Pistol`。名称前的数字代表玩家将使用的按键。

从 `Project` 浏览器器中的 `Models` 文件夹中将 `RobotRampage_Pistol` 模型拖到 `1Pistol` `GameObject` 上。通过将模型父级化 `GameObject`，你之后创建的动画将在本地空间中发生。

将 `1Pistol` `GameObject` 的 `Position`（位置）设置为 `(0.69, -0.72, 1.26)`，`Rotation`（旋转）设置为 `(0, 0, 0)`。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_246_0.png)

这让你能够直接看到正前方枪的视角。在 `Inspector`（检查器）中，通过取消勾选枪名称旁边的复选框来禁用手枪。这会让它消失，这样你可以添加另一把枪。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_246_1.png)

在 `Camera` 下创建另一个空 `GameObject` 并将其命名为 `2AssaultRifle`。你通常需要调整导入模型的比例以适应你的游戏，这种情况也不例外。将 `RobotRampage_AssaultRifle` 模型拖到你新 `GameObject` 下方。将 `2AssaultRifle` 的位置设置为 `(0.54, -0.67, 0.913)`，旋转设置为 `(0, 0, 0)`，`Scale`（缩放）设置为 `(0.01, 0.01, 0.01)`。

像处理手枪一样禁用突击枪。

对散弹枪重复同样的操作，使用 `3Shotgun` 并使用 `RobotRampage_Shotgun` 模型。将 `3Shotgun` 的位置设置为 `(0.3, -0.36, 0.65)`，旋转设置为 `(0, 0, 0)`，缩放设置为 `(0.01, 0.01, 0.01)`。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_247_0.png)

此时，你现在已经向游戏中添加了三把武器。保持 `1Pistol` `GameObject` 激活状态，并禁用 `2AssaultRifle` 和 `3Shotgun` `GameObject`。

代码也将这样工作：当玩家切换武器时，你将开启激活的枪并关闭其他的。

点击 `Play`（播放）并使用其中一种武器走动。感觉不错，对吧？ :]

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_247_1.png)

现在是为每种武器设置标签（Tags）的好时机。

## 为 GameObject 添加标签

选择 `1Pistol` `GameObject`，点击 `Tag` 下拉菜单并点击 `Add Tag`（添加标签）。点击 `Tags` 下方的 `+` 按钮并输入 `Pistol`。再次点击 `+` 输入 `AssaultRifle`，最后再次点击加号输入 `Shotgun`。

现在为相应的武器分配正确的标签。

点击 **1Pistol**，然后点击 **Tags** 下拉菜单将其设置为刚刚创建的 **Pistol** 标签。对 **2AssaultRifle** 和 **3Shotgun** 执行同样的操作，并设置相应的标签：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_248_0.png)

所有标签设置完毕并准备就绪，该进入代码编辑器了。

# 创建 Constants 文件

首先，创建一个 `Constants` 文件。通过拥有其他脚本都可以使用的通用名称引用，可以让工作变得更容易。当你在此部分创建新的 C# 脚本时，要在通用的 `Scripts` 文件夹中进行。

在 `Project` 浏览器中右键点击 `Assets` 文件夹，选择 `Create > Folder` 并将文件夹命名为 *Scripts*。在 `Scripts` 文件夹中，创建一个 C# 脚本并将其命名为 **Constants**。

在脚本编辑器中打开新的 **Constants** 脚本，用以下内容替换文件内容：

```csharp
public class Constants
{
    // Scenes
    public const string SceneBattle = "Battle";
    public const string SceneMenu = "MainMenu";

    // Gun Types
    public const string Pistol = "Pistol";
    public const string Shotgun = "Shotgun";
    public const string AssaultRifle = "AssaultRifle";

    // Robot Types
    public const string RedRobot = "RedRobot";
    public const string BlueRobot = "BlueRobot";
    public const string YellowRobot = "YellowRobot";

    // Pickup Types
    public const int PickupPistolAmmo = 1;
    public const int PickupAssaultRifleAmmo = 2;
    public const int PickupShotgunAmmo = 3;
    public const int PickupHealth = 4;
    public const int PickupArmor = 5;

    // Misc
    public const string Game = "Game";
    public const float CameraDefaultZoom = 60f;
}
```

上面的注释部分代表你将在后续脚本中使用的类型。你现在不需要知道每个常量的作用，随着后续章节的进行你会学会。

从开始，你使用武器类型创建武器切换逻辑。
