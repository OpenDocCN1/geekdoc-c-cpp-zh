
当布尔变量 `isRaceRunning` 为 `false` 时，该玩家的比赛已结束，`LateUpdate()` 函数需要忽略输入。此代码没有为车辆获取输入，而是直接禁用了 `canControl` 脚本，这样在游戏结束后没有人可以射击：

```csharp
if (isAIControlled) {
    // 因为比赛没有运行，我们将告诉 canControl 暂时不要射击
    canControl = false;
}
```

无论比赛是否仍在运行，比赛控制器都需要跟踪路点用于位置跟踪和圈数计数。`raceControl` 没有保留自己的更新函数，因此 `LateUpdate()` 的下一部分部分调用 `UpdateWaypoints()` 来保持持续更新：

```cs
// 告诉比赛控制器更新
UpdateWaypoints();
```

代码继续调用 `CheckLock()` 来检查车辆是否被固定在原地，然后调用 `raceControl` 的 `CheckWrongWay()`：

```cs
// 检查我们的车是否应该停在原地
CheckLock();
// 告诉比赛控制检查我们是否在逆向行驶
CheckWrongWay();
```

当 `raceControl` 检测到车辆沿着错误方向绕赛道行驶时，假设非 AI 控制的玩家将是用户。以下代码通过调用 `GameController.Instance.UpdateWrongWay()` 游戏控制器更新其逆向状态：

```cs
// 检查我们是否在逆向行驶并对此采取行动
if(raceControl.goingWrongWay) {
    if (isAIControlled)
        GameController.Instance.UpdateWrongWay(true);
}
```

当 `raceControl` 首次检测到车辆朝着错误方向时，这个 `timeWayStarted` 变量充当时间戳，因为它设置为系统 `Time.time` 的值。此代码检查 `raceControl.timeWayStarted` 和 `Time.time`，以查看车辆逆向行驶的时间是否超过了 `resetTime` 设置的时间：

```cs
// 如果在逆向行驶，比较从开始到现在的时间以查看我们是否需要重新生成
if(raceControl.timeWayStarted != -1)
    timedIf = Time.time - raceControl.timeWayStarted;
if(timedIf > resetTime)
```

如果车辆逆向行驶时间过长，将调用 `Respawn()` 函数将其放回赛道并朝向正确的方向：

```cs
// 已经在错误方向行驶了 x resetTime 秒，让我们重新生成这个家伙儿吧：
Respawn();
} else if (isAIControlled) {
```

当满足此条件时，车辆没有在逆向行驶，且它不是 AI 控制的车辆，因此会调用游戏控制器 `UpdateWrongWay()`，告诉它我们没有在逆向行驶，以便 UI 相应更新：

```cs
GameController.Instance.UpdateWrongWay(false);
}
```

### 橡皮带机制

在赛游戏中，保持游戏趣味性的一种常用方法是使用类似“橡皮带机制”（rubber banding）的东西。它的名字源于这种效果：当赛手落后太远时最高速度会增加，当他们领先太远时速度会降低——玩家在主玩家的前后像橡皮筋一样拉伸。

处理得当的橡皮带机制可以帮助每次都提供兴奋的比赛。如果处理不当，这种效果可能会令人沮丧，因为 AI 玩家会获得玩家领先时的领先优势，所以请谨慎使用！这确实是游戏中需要仔细平衡的隐藏部分，但尽管对游戏性有如此巨大的影响，大多数玩家甚至不会注意到。

为了判断 AI 玩家何时应该快一点，何时应该慢一点，这里的代码使用 `RacePosition` 来查看该玩家的位置。如果 `myRacePosition` 大于 3——这意味着该玩家处于第四名或更后——那么车辆的最大加速度（变量 `accelMax` 中）将设置为 `catchUpAccelMax` 以使其变快。如果该玩家的位置是第一（`myRacePosition < 2`），则 `accelMax` 将设置为由 `originalAccelMax` 保持的原始加速度乘以 0.25，从而减慢车辆：

```cs
accelMax = originalAccelMax;
// 如果这辆车在比赛中落后了，追赶
if(isRaceRunning && isAIControlled) {
    if(myRacePosition > 3) {
        // 加速
        accelMax = catchUpAccelMax;
    } else {
        accelMax = originalAccelMax;
    }
}
// 第一名，让我们慢下来！
if(myRacePosition < 2) {
    accelMax = originalAccelMax * 0.25f;
}
```

函数的最后一部分将根据车辆的当前速度更新引擎音调。这发生在 `UpdateEngineAudio()` 函数中，它在此被调用：

```cs
// 更新音频
UpdateEngineAudio();
```

### 输入处理

`GetInput()` 函数重写了 `BaseVehicle` 脚本中的原始函数。它的工作原理几乎相同，增加了重新生成功能和武器支持：

```cs
public override void GetInput() {
    // 计算转向
    steer = Math.Clamp(default_input.GetHorizontal(), -1, 1);
    // 油门深度是多少？
    motor = Math.Clamp(default_input.GetVertical(), 0, 1);
    // 刹车是多少？
    brakes = -1 * Math.Clamp(default_input.GetVertical(), -1, 0);
}
```

`default_input` 对象类型是 `Keyboard_Input`，它支持重新生成。判断用户是否按下重新生成键是调用 `default_input.GetRespawn()`，它将返回 true 或 false。如果用户按下重新生成键，车辆尚未重新生成且 `canRespawn` 为 true，则调用 `Respawn()` 函数重置缓存，并设置变量 `isRespawning` 和 `canRespawn` 以禁用任何进一步的重新生成。当通过 `Invoke()` 函数安排在 2 秒后调用 `resetRespawn` 时，它们将被重置：

```cs
if(default_input.GetRespawn() && !isRespawning && canRespawn) {
    isRespawning = true;
    Respawn();
    canRespawn = false;
    Invoke("resetRespawn", 2);
}
```

为了保持在没有武器控制器的情况下仍能工作的灵活性，射击输入代码首先对 `weaponControl` 进行空值检查。如果 `default_input.Fire()` 为 true 且 `canFire` 为 true，则调用 `weaponControl.Fire()` 让当前武器执行其动作：

```cs
// 首先，我们确保存在一个武器控制器
//（否则不需要射击！）
if(weaponControl != null)
```

```cs
// 如果我们需要则射击
if( default_input.GetFire() && canFire)
{
    // 告诉武器控制器处理射击
    weaponControl.Fire();
}
}
```

发生重生时，调用 `resetRespawn()` 会重置 `canRespawn` 状态，以允许未来的重生：

```cs
void resetRespawn()
{
    canRespawn=true;
}
```

当汽车由 AI 控制时，会调用 `GetAIInput()`。AI 车辆从 AI 控制器脚本获取输入；转向和电机输入来自 `AIController` 对象，而不是输入对象：

```cs
public void GetAIInput()
{
    // 计算转向量
    steer= Mathf.Clamp( AIController.GetHorizontal(), -1, 1);
    // 油油门开启多大？
    motor= Mathf.Clamp( AIController.GetVertical() , 0, 1);
}
```

比赛结束时，将调用 `FinishedRace()` 来停止对车辆的控制，并告诉比赛控制（raceControl）该玩家已完成：

```cs
public void FinishedRace()
{
    // 停止允许控制车辆
    canControl = false;
    brake = 1;
    motor = 0;
    // 设置标记位，以便于判断我们何时完成
    raceControl.RaceFinished();
}
```

`SetAIInput()` 用于告诉此脚本玩家是否应该由 AI 控制：

```cs
public void SetAIInput(bool aiFlag)
{
    isAIControlled = aiFlag;
}
```

当调用函数 `IsFinished()` 时，它会查看比赛控制器（布尔值）返回的结果：

```cs
public bool IsFinished () {
    return raceControl.GetIsFinished();
}
```

`GetCurrentLap()` 查看比赛控制器以确定玩家当前正在比赛哪圈，并作为返回值：

```cs
public int GetCurrentLap() {
    return raceControl.GetCurrentLap();
}
```

比赛控制器可以通过 `GetCurrentWaypointNum()` 告诉我们玩家当前位于哪个路点：

```cs
public int GetCurrentWaypointNum() {
    return raceControl.GetCurrentWaypointNum();
}
```

比赛控制器跟踪玩家到下一个路点之间的距离，可以通过 `GetCurrentWaypointDist()` 函数获取：

```cs
public float GetCurrentWaypointDist() {
    return raceControl.GetCurrentWaypointDist();
}
```

当所有路点都已通过，但玩家还没有通过起点/终点线增加圈数时，`IsLapDone()` 将返回 `true`。再次，这是由比赛控制器持有的：

```cs
public bool IsLapDone() {
    return raceControl.GetIsLapDone();
}
```

当玩家被游戏控制器生成时，它会调用 `SetWayController()` 告诉比赛控制器它应该使用的 `Waypoints_Controller` 实例：

```cs
public void SetWayController(Waypoints_Controller aControl) {
    raceControl.SetWayController(aControl);
}
```

当车辆的碰撞器与游戏世界中的另一个碰撞器发生碰撞时，会调用 `OnCollisionEnter`：

```cs
void OnCollisionEnter(Collision collision) {
}
```

### RaycastHit

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
```
