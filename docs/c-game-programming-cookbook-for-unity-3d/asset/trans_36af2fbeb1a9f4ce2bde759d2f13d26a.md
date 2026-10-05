

# RaycastHit;

射线检测从路点位置（来自 `tempVEC`）开始，并向上增加了 300 个单位，以确保射线从地面下方开始。射线方向为 `-Vector3.up`（正下方），但在此 `Physics.Raycast` 调用中，没有设置距离，射线应该检测下方的所有物体，无论距离有多远：

```csharp
if (Physics.Raycast(tempV + (Vector3.up * 300),
    -Vector3.up, out hit))
{
    tempVEC.y=hit.point.y-15;
}
```

`myTransform` 准备好设置为新的位置和旋转：

```csharp
// reposition the player at tempVEC (the waypoint position)
// with a corrected y value via raycast and also we set the
// player rotation to the waypoint's rotation so that we are
// facing in the right direction after respawning
myTransform.rotation=tempTR.rotation;
myTransform.position=tempVEC;
```

重生后，玩家将变为无敌状态（通过调用 `MakeInvulnerable` 函数）。使用 `Invoke()` 来调度在 3 秒后调用 `MakeInvulnerable`，从而限制玩家的无敌时间：

```csharp
// we need to be invulnerable for a little while
MakeInvulnerable();

Invoke ("MakeVulnerable", 3);
```

每当发生重生时，武器都会重置为使用第一个槽位的默认设置：

```csharp
// revert to the first weapon
if (weaponControl==null)
    weaponControl.SetWeaponSlot(0);
```

`MakeInvulnerable()` 和 `MakeVulnerable()` 函数分别将 `isInvulnerable` 布尔变量设置为 `true` 或 `false`。当 `isInvulnerable` 为 `true` 时，此脚本之前的碰撞函数（OnCollisionEnter()`）将忽略与弹药层的碰撞：

```csharp
void MakeInvulnerable()
{
    isInvulnerable=true;
}

void MakeVulnerable()
{
    isInvulnerable=false;
}
```

`PlayerFinished()` 让玩家知道比赛已经结束。除了将 `canFire` 设为 `false` 以禁用发射外，该函数还禁用了所有可能驱动或转向玩家的操作：

```csharp
public void PlayerFinished()
{
    // disable this vehicle
    isAIControlled = false;
    canControl = false;
    canFire = false;
    AIController.canControl = false;
    motor = 0;
    steer = 0;
}
```

为了保持车辆直立，`Check_If_Car_Is_Flipped()` 函数只需检查车辆的 `localEulerAngles`，以查看其旋转是否超出常。。这些值并不精确；它所检查的旋转值是通过尝试决定的，直到感觉合适并且能检测到大多数情况：

```csharp
void Check_If_Car_Is_Flipped()
{
    if((myTransform.localEulerAngles.z > 80 &&
myTransform.localEulerAngles.z < 280) || (myTransform.localEulerAngles.x > 80 && myTransform.localEulerAngles.x < 280))
}
```

当车辆处于奇怪的角度时，`resetTimer` 通过 `Time.deltaTime` 递增。这为车辆可能翻了多久提供了一个参考：

```csharp
resetTimer += Time.deltaTime;
} else {
    resetTimer = 0;
}
```

当 `resetTimer` 达到 `resetTime` 时，玩家将重生：

```csharp
if(resetTimer > resetTime)
    Respawn();
}
```

当比赛结束时，比赛控制器调用 `PlayerFinishedRace()`，并将最终的比赛位置作为整数传递：

```csharp
void PlayerFinishedRace( int whichPositionDidFinish )
{
```

如果此玩家不是由 AI 控制，那么它必须是用户。这里游戏控制器知道游戏结束，然后 AI 将接管车辆的控制：

```csharp
if(!isAIControlled )
{
    // tell game controller that the game is finished
    Controller_MVD.Instance.RaceComplete(whichPositionDidFinish);

    // take over the car with AI control
    isAIControlled=true;
    InitAI();
}
```

## 12.3.5 用户界面

此游戏的用户界面是带有 UI 组件的 gameObject 集合。它们存在于游戏场景中（作为 gameObject），并由游戏控制器引用和管理。这里有：

- Final_Position—一个带有 UI 组件的 gameObject，显示游戏结束时向用户展示的消息，告知其最终位置。
- in_1—一个包含显示数字 1 图像的 UI 组件，用于比赛开始。
- in_2—一个包含显示数字 2 图像的 UI 组件，用于倒计时。
- in_3—一个包含显示数字 3 图像的 UI 组件，用于倒计时。
- Text_Lap—一个位于屏幕左上角的 UI 对象，显示玩家已完成多少圈比赛。
- Text_Position—一个位于屏幕右上角的 UI 对象，显示玩家的当前比赛位置。
- WrongWay—一个位于屏幕正中央上方的 UI 对象。每当用户的车辆在赛道上反向行驶时，其 gameObject 将变为激活状态。

## 13 坦克

1974年，Atari, Inc. 的子公司 Kee Games 发布了一款名为《Tank!》的街机游戏。这是一款双人游戏，玩家必须迷宫中行驶并摧毁另一个玩家的坦克。尽管它的图形从固定的俯视视角来看是简单的黑白图形，但该游戏在当时是非常先进的。它的控制系统非常出色；它使用双轴（上下）摇杆来引导每辆车辆，因为每个摇杆都控制着坦克每侧的独立履带。《Tank!》需要两个玩家才能玩；没有人工智能。也许这是因为 AI 编程的复杂性和那个时代的技术限制，也可能这是一种设计决定；它对成功没有明显影响，而且该游戏大获成功。在单人坦克游戏进入街机厅之前还要等很长时间。我个人记得在 20 世纪 70 年代后期在街机厅玩坦克游戏的荣幸；我玩过一个俯视坦克游戏，但那是很久以前的事了，我不确定它是否是原始的《Tank!》。从截图来看，至少看起来非常眼熟。《Tank!》的变体出现在 1977 年发布的名为《Combat》的卡带上，其中包含了五种游戏类型，全部组合在一起。

